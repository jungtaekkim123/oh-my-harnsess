# 이벤트 스케줄링 — SimTalk 2.0 Code Examples

> Cross-reference: `references/21-fn-misc-simulation.md` for `callEvery`, `processTime` signatures
> Cross-reference: `references/12-control-flow.md` for `waituntil`, `wait`, `stopuntil` syntax

## Pattern 1: callEvery — 주기적 작업 실행

**Use when:** 모든 하위 Frame에서 동일 이름의 메서드를 재귀적으로 호출할 때 (예: 주기적 로깅, 통계 수집)

```simtalk
// 주기적 로깅을 위한 callEvery 사용
// init 메서드에서 반복 호출 스케줄링

repeat
   // .Models 프레임 아래 모든 "logStatus" 메서드를 호출
   callEvery(.Models, "logStatus")
   wait 60  // 60초마다 반복
until false
```

```simtalk
// callEvery에 파라미터 전달
// 모든 하위 Frame의 "updateConfig" 메서드에 인수를 전달합니다

var newSpeed := 1.5
var mode := "turbo"
callEvery(.ProductionLine, "updateConfig", newSpeed, mode)
```

```simtalk
// logStatus 메서드 (각 Frame에 배치)
// callEvery에 의해 호출되는 대상 메서드

var ec := currentEventCtl
print ec.SimTime, " | ", ?.name, " | WIP:", ?.NumMU
```

**Key points:**
- `callEvery(Frame, MethodName, [params])`는 지정 Frame과 모든 하위 Frame에서 해당 이름의 메서드를 depth-first로 검색/실행합니다
- 호출된 메서드가 모두 완료될 때까지 `callEvery`가 포함된 메서드 실행이 중단됩니다
- 선택적 파라미터를 전달하여 호출 대상 메서드에 인수를 넘길 수 있습니다

---

## Pattern 2: waituntil — 조건부 대기

**Use when:** 특정 조건이 충족될 때까지 메서드 실행을 중단하고, 조건 충족 시 즉시 재개할 때

```simtalk
// Buffer가 비어있을 때까지 대기
waituntil Buffer1.empty prio 1
print "Buffer가 비었습니다. 다음 작업을 진행합니다."
@.move(Station1)
```

```simtalk
// 복합 조건: Station이 비어있고 MU가 준비된 경우
waituntil Station1.empty AND SourceBuffer.NumMU > 0 prio 1
SourceBuffer.Cont.move(Station1)
```

```simtalk
// 시간 제한이 있는 waituntil
// 60초 이내에 Station이 비지 않으면 대체 경로로 이동
waituntil Station1.empty wait 60
if waitExpired
   // 타임아웃: 대체 경로로 이동
   @.move(AlternativeStation)
   print "타임아웃 — 대체 경로 사용"
else
   // 조건 충족: 원래 경로로 이동
   @.move(Station1)
end
```

```simtalk
// 우선순위를 활용한 경쟁적 대기
// 여러 Transporter가 같은 Station을 기다리는 경우
// 용량이 큰 Transporter가 우선
waituntil Station.empty prio @.Capacity
@.move(Station)
```

**Key points:**
- `waituntil`은 조건이 false이면 메서드를 중단하고, 감시 대상 속성이 변경될 때 조건을 재평가합니다
- `prio` 키워드로 여러 대기 메서드 간 우선순위를 지정합니다 (값이 클수록 높은 우선순위)
- `wait timespan`으로 타임아웃을 설정하고, `waitExpired`로 타임아웃 여부를 확인합니다
- 조건에 사용자 정의 메서드 호출이나 테이블 접근은 사용할 수 없습니다 (watchable 속성만 가능)

---

## Pattern 3: wait — 단순 시간 지연

**Use when:** 메서드 실행을 지정된 시간만큼 중단한 후 재개할 때 (EventController 필요)

```simtalk
// 단순 대기: 120초 후 재개
wait 120
print "120초 경과"
```

```simtalk
// 반복 생성 패턴: 일정 간격으로 MU 생성
var mu: object
repeat
   if not Station.occupied
      mu := .MUs.Container.create(Station)
   end
   wait 120
   if mu /= void
      mu.delete
   end
   wait 30
until false
```

```simtalk
// 시간 리터럴을 사용한 대기
wait 1:30        // 1분 30초 대기
wait 1:0:0       // 1시간 대기
wait 0:0:30      // 30초 대기
```

**Key points:**
- `wait`은 EventController가 필요합니다 (시뮬레이션 이벤트로 처리)
- `wait` 중에도 시뮬레이션은 계속 진행되며, 다른 메서드가 실행될 수 있습니다
- `waituntil`과 달리 조건 기반이 아닌 순수 시간 기반 중단입니다
- 시간 리터럴(`1:30`, `1:0:0`)을 사용하면 가독성이 향상됩니다

---

## Pattern 4: 이벤트 기반 패턴 — callEvery와 조건 로직의 결합

**Use when:** 주기적 체크와 조건부 동작을 결합하여 복잡한 이벤트 기반 로직을 구현할 때

```simtalk
// 주기적 모니터링 + 조건부 알림 패턴
// init 메서드에서 실행

repeat
   // 매 300초마다 체크
   wait 300

   var ec := currentEventCtl

   // WIP 수준 체크
   var currentWIP := Buffer1.NumMU + Buffer2.NumMU
   if currentWIP > 50
      print ec.SimTime, " [경고] WIP 초과:", currentWIP
      // 투입 속도 감소
      Source1.Interval := Source1.Interval * 1.2
   elseif currentWIP < 10
      print ec.SimTime, " [정보] WIP 부족:", currentWIP
      // 투입 속도 증가
      Source1.Interval := Source1.Interval * 0.8
   end
until false
```

```simtalk
// 교대근무 스케줄링 패턴
// 8시간(480분) 간격으로 교대를 시뮬레이션

var shift := 1
repeat
   print "=== 교대 ", shift, " 시작 ==="

   // 교대별 처리 시간 변경
   switch shift
   case 1
      Station1.ProcTime := z_normal(1, 60, 5)   // 주간: 정상
   case 2
      Station1.ProcTime := z_normal(1, 65, 8)   // 야간: 약간 느림
   case 3
      Station1.ProcTime := z_normal(1, 70, 10)  // 심야: 더 느림
   end

   wait 480  // 8시간 대기

   // 교대 로테이션
   shift := (shift mod 3) + 1
until false
```

```simtalk
// waituntil과 wait 조합: 자원 해제 대기 후 작업 수행
waituntil AGV.empty prio 1
@.move(AGV)
wait 30  // 적재 시간 30초
AGV.move(Destination)
```

**Key points:**
- `repeat ... until false`와 `wait`을 조합하면 주기적 실행 패턴을 구현할 수 있습니다
- `callEvery`는 모든 하위 Frame을 순회하고, `wait` 루프는 단일 메서드에서 반복합니다
- `switch`와 조합하면 시간대별/교대별 동작 변경이 가능합니다
- `waituntil` → `wait` 순서로 조합하면 "조건 충족 후 일정 시간 소요" 패턴을 표현합니다

---

## Pattern 5: processTime — CPU 처리 시간 추적

**Use when:** 시뮬레이션의 실제 CPU 소요 시간을 측정하여 성능 분석, 벤치마크, 실행 시간 예측에 활용할 때

```simtalk
// 시뮬레이션 구간별 CPU 시간 측정
var t0 := processTime

// 무거운 연산 수행
for var i := 1 to ResultTable.yDim
   ResultTable[2, i] := ResultTable[1, i] * 1.15 + z_normal(1, 0, 0.5)
next

var elapsed := processTime - t0
print "테이블 연산 CPU 시간:", elapsed, "초"
```

```simtalk
// endSim에서 전체 시뮬레이션 CPU 시간 리포트
// (init에서 StartCPU.value := processTime 으로 저장해둠)

var totalCPU := processTime - StartCPU.value
var simDays := currentEventCtl.SimTime / 1440  // 분 → 일

print "=== 성능 리포트 ==="
print "시뮬레이션 기간:", simDays, "일"
print "총 CPU 시간:", totalCPU, "초"
print "CPU 시간/시뮬 1일:", totalCPU / simDays, "초"
```

**Key points:**
- `processTime`은 실제 CPU 시간(초)을 `real` 타입으로 반환하며, 밀리초 수준의 해상도를 가집니다
- 시뮬레이션 시간(`SimTime`)과는 완전히 독립적인 측정값입니다
- 구간 측정을 위해 시작점에서 `processTime`을 저장하고 종료점에서 차이를 계산합니다
- 실험 자동화 시 성능 저하 구간을 식별하는 데 유용합니다
