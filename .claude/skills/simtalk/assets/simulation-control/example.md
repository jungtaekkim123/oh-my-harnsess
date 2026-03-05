# 시뮬레이션 제어 — SimTalk 2.0 Code Examples

> Cross-reference: `references/21-fn-misc-simulation.md` for full function signatures

## Pattern 1: init 메서드 — 초기화 로직

**Use when:** 시뮬레이션 시작 시 객체 초기값 설정, 테이블 초기화, 옵저버 등록 등 초기 설정이 필요할 때. EventController의 init 콜백에 연결합니다.

```simtalk
// init 메서드 — EventController의 "Init" 콜백으로 등록
// 시뮬레이션 시작 전 초기값을 설정합니다

// 테이블 초기화
ResultTable.delete
ResultTable[1,1] := "Time"
ResultTable[2,1] := "Throughput"
ResultTable[3,1] := "WIP"

// 카운터 변수 초기화
TotalProduced.value := 0
TotalScrapped.value := 0

// 처리 시간 분포 설정
Station1.ProcTime := z_uniform(1, 50, 70)
Station2.ProcTime := z_normal(1, 60, 5)

// 애니메이션 리프레시율 설정 (성능 최적화)
setAnimationRefreshRate(25)

// MU 추적 메서드 등록
setMUTraceRouteMethod(&.traceMethod)

print "=== 시뮬레이션 초기화 완료 ==="
```

**Key points:**
- `init`은 EventController의 초기화 콜백에 연결하여 시뮬레이션 시작 전에 자동 실행됩니다
- `z_uniform`, `z_normal` 등 분포 함수로 확률적 처리 시간을 설정합니다
- `setMUTraceRouteMethod`로 MU 이동 추적을 등록할 수 있습니다 (reset 시 자동 해제)

---

## Pattern 2: reset 메서드 — 정리 및 리셋 로직

**Use when:** 시뮬레이션 리셋 시 커스텀 변수/테이블 정리, 파일 핸들 닫기 등이 필요할 때. EventController의 reset 콜백에 연결합니다.

```simtalk
// reset 메서드 — EventController의 "Reset" 콜백으로 등록
// 시뮬레이션 리셋 시 정리 작업을 수행합니다

// 결과 테이블 초기화
if ResultTable.yDim > 1
   for var row := ResultTable.yDim downto 2
      ResultTable.deleteRow(row)
   next
end

// 커스텀 변수 초기화
TotalProduced.value := 0
TotalScrapped.value := 0
WarmUpComplete.value := false

// 랜덤 스트림 리셋
resetRandomNumberStream(1)
resetRandomNumberStream(2)

// 로그 파일 닫기 (열려 있는 경우)
if LogFile.opened
   LogFile.close
end

print "=== 시뮬레이션 리셋 완료 ==="
```

**Key points:**
- `reset`은 EventController의 리셋 콜백에 연결합니다
- `downto`를 사용하여 테이블 행을 역순으로 삭제해야 인덱스 문제가 발생하지 않습니다
- `resetRandomNumberStream`으로 특정 랜덤 스트림을 초기 상태로 되돌립니다

---

## Pattern 3: endSim 메서드 — 시뮬레이션 종료 핸들러

**Use when:** 시뮬레이션 종료 시 결과 수집, 통계 리포트 생성, 데이터 내보내기가 필요할 때. EventController의 endSim 콜백에 연결합니다.

```simtalk
// endSim 메서드 — EventController의 "EndSim" 콜백으로 등록
// 시뮬레이션 종료 시 결과를 수집하고 내보냅니다

var ec := currentEventCtl

// 최종 결과 기록
var lastRow := ResultTable.yDim + 1
ResultTable[1, lastRow] := ec.SimTime
ResultTable[2, lastRow] := TotalProduced.value
ResultTable[3, lastRow] := Drain1.StatNumIn

// 가동률 기록
ResultTable[4, lastRow] := Station1.StatPortion("working")
ResultTable[5, lastRow] := Station2.StatPortion("working")

// 통계 리포트 표시
var statObjects: list
statObjects.append(&Station1)
statObjects.append(&Station2)
statObjects.append(&Buffer1)
showStatisticsReport(statObjects)

// 결과 파일 내보내기
ResultTable.saveAs("C:\Results\sim_result.xlsx")

// CPU 처리 시간 출력
print "=== 시뮬레이션 종료 ==="
print "총 생산량:", TotalProduced.value
print "CPU 처리 시간:", processTime, "초"
```

**Key points:**
- `currentEventCtl`로 현재 EventController 객체에 접근합니다
- `showStatisticsReport`는 list에 등록된 객체들의 통계 리포트를 표시합니다
- `processTime`은 시뮬레이션이 아닌 실제 CPU 소요 시간(초)을 반환합니다

---

## Pattern 4: EventController 속성 접근

**Use when:** 현재 시뮬레이션 시간, 종료 시간, 속도 등 EventController 정보를 조회하거나 제어할 때

```simtalk
// EventController 속성 접근 패턴
var ec := currentEventCtl

// 시뮬레이션이 실행 중인지 확인
if ec /= void
   // 현재 시뮬레이션 시간
   print "현재 시뮬 시간:", ec.SimTime

   // 시뮬레이션 종료 시간
   print "종료 시간:", ec.EndTime

   // 시뮬레이션 속도
   print "현재 속도:", ec.Speed

   // 절대 시간 형식 사용 여부
   print "절대시간 형식:", ec.AbsTimeFormat

   // EventController가 속한 Frame
   print "실행 Frame:", ec.location
end
```

```simtalk
// EventController 속성을 활용한 조건부 로직
var ec := currentEventCtl
if ec /= void
   // 시뮬레이션 진행률 계산
   var progress := ec.SimTime / ec.EndTime * 100
   print "진행률:", progress, "%"

   // 시뮬레이션 후반부에만 통계 수집
   if ec.SimTime > ec.EndTime * 0.5
      collectDetailedStats
   end
end
```

**Key points:**
- `currentEventCtl`이 `void`인 경우는 시뮬레이션이 실행 중이 아닌 상태입니다
- `SimTime`은 현재 시뮬레이션 시간, `EndTime`은 설정된 종료 시간입니다
- `ec.location`으로 EventController가 위치한 Frame을 확인할 수 있습니다

---

## Pattern 5: Warm-up 처리 — 통계 수집 시 워밍업 기간 제외

**Use when:** 시뮬레이션 초기 과도 상태(warm-up period)를 제외하고 안정 상태에서만 통계를 수집할 때

```simtalk
// 센서 또는 Station의 Exit Control에서 warm-up 체크
// Warm-up 기간(예: 처음 480분)을 제외하고 통계 수집

var ec := currentEventCtl
var warmUpPeriod := 480  // 8시간 = 480분

if ec.SimTime > warmUpPeriod
   // warm-up 이후에만 통계 수집
   TotalProduced.value += 1

   // 리드타임 기록
   var leadTime := ec.SimTime - @.CreationTime
   LeadTimeTable[1, LeadTimeTable.yDim + 1] := leadTime
end
```

```simtalk
// processTime을 활용한 CPU 시간 기반 성능 모니터링
// 시뮬레이션 성능을 주기적으로 체크합니다

var startCPU := processTime

// ... 복잡한 연산 수행 ...
for var i := 1 to 1000
   ResultTable[1, i] := z_normal(1, 100, 10)
next

var elapsed := processTime - startCPU
print "연산 소요 CPU 시간:", elapsed, "초"

if elapsed > 5.0
   print "경고: 연산이 5초 이상 소요되었습니다"
end
```

**Key points:**
- `SimTime`과 warm-up 기간을 비교하여 통계 수집 시점을 제어합니다
- `processTime`은 실제 CPU 시간(초, real 타입)을 반환하며, 시뮬레이션 시간과 다릅니다
- `@.CreationTime`으로 MU의 생성 시점을 알 수 있어 리드타임 계산에 활용합니다

---

## Pattern 6: setAnimationRefreshRate — 애니메이션 속도 제어

**Use when:** 시뮬레이션 애니메이션 프레임율을 조절하여 실행 속도를 최적화하거나 부드러운 시각화가 필요할 때

```simtalk
// 시뮬레이션 단계별 애니메이션 속도 조절
var ec := currentEventCtl

if ec /= void
   if ec.SimTime < 100
      // 초기 단계: 부드러운 애니메이션으로 동작 확인
      setAnimationRefreshRate(60)
   elseif ec.SimTime < 1000
      // 중간 단계: 적당한 속도
      setAnimationRefreshRate(30)
   else
      // 후반 단계: 빠른 실행 우선
      setAnimationRefreshRate(5)
   end
end
```

```simtalk
// init 메서드에서 실험 모드에 따라 리프레시율 설정
if ExperimentMode.value
   // 실험 실행: 최소 리프레시율로 속도 극대화
   var prevRate := setAnimationRefreshRate(1)
   print "이전 리프레시율:", prevRate
else
   // 데모 실행: 부드러운 애니메이션
   setAnimationRefreshRate(50)
end
```

**Key points:**
- 리프레시율은 `1`~`100` 사이 정수로 설정합니다
- 낮은 값 = 빠른 시뮬레이션 속도, 높은 값 = 부드러운 애니메이션
- `setAnimationRefreshRate`는 이전 설정값을 integer로 반환합니다
- 실험 자동화 시 `1`로 설정하면 시뮬레이션 속도를 극대화할 수 있습니다
