# MU 핸들링 — SimTalk 2.0 Code Examples

> Cross-reference: `references/03-general-access.md` for object access patterns
> Cross-reference: `references/12-control-flow.md` for control flow and `waituntil` syntax

## Pattern 1: @ 연산자로 MU 접근 — 센서/Station에서 MU 속성 읽기/쓰기

**Use when:** 센서(Sensor)나 Station의 컨트롤(입구/출구 제어)에서 현재 MU의 속성을 읽거나 변경할 때

```simtalk
// 센서 Exit Control — @ 는 센서를 트리거한 MU를 참조
// Transporter의 목적지 확인 후 하역 또는 통과
if @.destination = current
   // 목적지가 현재 위치: MU의 적재물을 워크스테이션으로 이동
   @.Cont.move(Workstation)
else
   // 목적지가 다른 곳: 다음 후속 객체로 이동
   @.move(current.succ(1))
end
```

```simtalk
// Station Exit Control — @ 는 Station 위의 MU를 참조
// MU의 커스텀 속성 읽기
var productType := @.ProductType       // 사용자 정의 속성
var batchID := @.BatchID               // 사용자 정의 속성
var processingTime := @.ProcTime       // MU의 처리 시간

print "제품:", productType, " | 배치:", batchID
print "처리 시간:", processingTime
```

```simtalk
// Station Entrance Control — MU가 진입할 때 속성 설정
@.color := "green"                     // MU 색상 변경
@.EntranceTime := currentEventCtl.SimTime  // 진입 시간 기록 (사용자 정의 속성)
```

**Key points:**
- `@`는 현재 컨트롤을 트리거한 MU(Mobile Unit)를 참조하는 익명 식별자입니다
- `@.Cont`는 MU 위에 적재된 MU(컨테이너 내용물)를 참조합니다
- `?`는 현재 메서드를 호출한 객체(caller)를 참조합니다
- 사용자 정의 속성은 MU 클래스에 미리 정의해두면 `@.속성명`으로 접근 가능합니다

---

## Pattern 2: MU.move — 특정 목적지로 MU 이동

**Use when:** MU를 현재 위치에서 다른 Station, Buffer, Conveyor 등 특정 목적지로 이동시킬 때

```simtalk
// 기본 이동: MU를 다음 Station으로 이동
@.move(Station2)
```

```simtalk
// 조건부 이동: MU 속성에 따라 다른 목적지로 이동
if @.ProductType = "A"
   @.move(StationA)
elseif @.ProductType = "B"
   @.move(StationB)
else
   @.move(DefaultStation)
end
```

```simtalk
// 컨테이너(Transporter) 위 MU를 다른 위치로 이동
// Transporter Exit Control
if @.NumMU > 0
   // 적재된 MU를 Workstation으로 이동
   @.Cont.move(Workstation)
end
```

```simtalk
// waituntil과 조합: 목적지가 비어있을 때까지 대기 후 이동
waituntil Station1.empty prio 1
@.move(Station1)
```

```simtalk
// 후속 객체(successor)를 통한 이동
// current.succ(n)으로 n번째 후속 객체에 접근
@.move(current.succ(1))   // 첫 번째 후속 객체로 이동
@.move(current.succ(2))   // 두 번째 후속 객체로 이동
```

**Key points:**
- `@.move(destination)`은 MU를 지정 목적지로 즉시 이동시킵니다
- 목적지가 이미 occupied 상태면 런타임 에러가 발생할 수 있으므로, `waituntil`이나 `empty` 체크를 선행합니다
- `current.succ(n)`으로 현재 객체의 n번째 후속 객체에 접근합니다
- `@.Cont`로 적재된 MU에 접근하여 이동시킬 수 있습니다

---

## Pattern 3: MU 속성 설정 — 커스텀 속성, 이름, 우선순위

**Use when:** MU에 커스텀 데이터를 부여하거나, 이름/색상/우선순위 등 기본 속성을 변경할 때

```simtalk
// MU 기본 속성 설정
@.name := "Part_" + to_str(TotalProduced.value)  // MU 이름 변경
@.color := "blue"                              // MU 색상 변경
@.Priority := 5                                // 우선순위 설정 (높을수록 우선)
@.Speed := 1.0                                 // Transporter 속도 설정
```

```simtalk
// 사용자 정의 속성 설정 (MU 클래스에 미리 정의 필요)
@.ProductType := "TypeA"
@.BatchID := 1001
@.QualityGrade := "Premium"
@.DueDate := currentEventCtl.SimTime + 480  // 현재 시간 + 8시간

// 품질 검사 결과에 따른 속성 갱신
if z_uniform(1, 0, 1) > 0.95
   @.Defective := true
   @.color := "red"
else
   @.Defective := false
   @.color := "green"
end
```

```simtalk
// MU에 소요 시간 추적 속성 설정
// Station Entrance Control
@.StationEntryTime := currentEventCtl.SimTime

// Station Exit Control (같은 Station의 다른 메서드)
var stayTime := currentEventCtl.SimTime - @.StationEntryTime
print @.name, " 체류 시간:", stayTime
```

**Key points:**
- 사용자 정의 속성은 MU 클래스(Class Library)에서 미리 정의해야 합니다
- `@.name`, `@.color`, `@.Priority`, `@.Speed` 등은 빌트인 속성입니다
- `to_str()` 함수로 숫자를 문자열로 변환하여 이름에 사용할 수 있습니다
- `SimTime`을 MU 속성에 저장하면 경과 시간 추적이 가능합니다

---

## Pattern 4: 라우팅 로직 — 조건에 따른 후속 객체 선택

**Use when:** MU의 속성이나 시스템 상태에 따라 다른 경로로 MU를 보내야 할 때

```simtalk
// Station Exit Control — 제품 타입별 라우팅
switch @.ProductType
case "A"
   @.move(LineA_Buffer)
case "B"
   @.move(LineB_Buffer)
case "C"
   @.move(LineC_Buffer)
else
   @.move(DefaultBuffer)
end
```

```simtalk
// 부하 분산 라우팅: 가장 적게 차 있는 Buffer로 이동
var minLoad := Buffer1.NumMU
var target := &Buffer1

if Buffer2.NumMU < minLoad
   minLoad := Buffer2.NumMU
   target := &Buffer2
end
if Buffer3.NumMU < minLoad
   target := &Buffer3
end

@.move(target)
```

```simtalk
// 품질 검사 후 분기: 불량품은 Scrap, 정상품은 다음 공정으로
if @.Defective
   @.move(ScrapBin)
   TotalScrapped.value += 1
   print currentEventCtl.SimTime, " 불량 폐기:", @.name
else
   // 빈 Station 찾기
   if Station_1.empty
      @.move(Station_1)
   elseif Station_2.empty
      @.move(Station_2)
   elseif Station_3.empty
      @.move(Station_3)
   else
      // 모든 Station이 사용 중이면 대기
      waituntil Station_1.empty OR Station_2.empty OR Station_3.empty prio @.Priority
      if Station_1.empty
         @.move(Station_1)
      elseif Station_2.empty
         @.move(Station_2)
      else
         @.move(Station_3)
      end
   end
end
```

**Key points:**
- `switch`를 사용하면 여러 경로 분기를 간결하게 표현할 수 있습니다
- 부하 분산 시 `NumMU`로 현재 점유 수를 비교합니다
- `&Buffer1` 구문은 객체 참조를 변수에 저장합니다 (SimTalk 2.0)
- `waituntil`에서 `OR` 조건을 사용하면 여러 목적지 중 하나가 비는 즉시 진행합니다

---

## Pattern 5: MU 생성 및 삭제 — 프로그래밍 방식의 MU 관리

**Use when:** Source 객체 없이 코드로 직접 MU를 생성하거나, 특정 조건에서 MU를 삭제할 때

```simtalk
// MU 프로그래밍 방식 생성
// Class Library의 MU 클래스에서 인스턴스를 생성하여 목적지에 배치
var newMU := .MUs.Part.create(Station1)
newMU.name := "CustomPart_1"
newMU.ProductType := "Special"
newMU.color := "yellow"
```

```simtalk
// 주기적 MU 생성 패턴
// init 메서드에서 호출하여 주기적으로 MU를 투입합니다
var mu: object
repeat
   if not InputStation.occupied
      mu := .MUs.Container.create(InputStation)
      mu.name := "Batch_" + to_str(BatchCounter.value)
      BatchCounter.value += 1
   end
   wait 120  // 2분 간격
until false
```

```simtalk
// 조건부 MU 삭제
// Station Exit Control — 만료된 MU 삭제
var ec := currentEventCtl
var age := ec.SimTime - @.CreationTime

if age > 1440  // 24시간(1440분) 초과
   print ec.SimTime, " 만료 삭제:", @.name, " (수명:", age, "분)"
   @.delete
   return  // 삭제 후 더 이상 처리하지 않음
end

// 정상 MU는 다음 공정으로
@.move(NextStation)
```

```simtalk
// Station 위의 모든 MU 일괄 삭제
while ParallelStation.NumMU > 0
   ParallelStation.MU(1).delete
end
```

```simtalk
// MU 복제: 기존 MU를 복제하여 분기 처리
var original := @
var copy := .MUs.Part.create(InspectionStation)

// 원본 속성을 복제본에 복사
copy.name := original.name + "_copy"
copy.ProductType := original.ProductType
copy.BatchID := original.BatchID

// 원본은 다음 공정으로, 복제본은 검사 라인으로
original.move(MainLine)
```

**Key points:**
- `.MUs.Part.create(destination)`으로 Class Library의 MU 클래스를 인스턴스화하여 목적지에 배치합니다
- `@.delete`는 MU를 즉시 삭제합니다 — 삭제 후에는 `@`에 접근할 수 없으므로 `return`을 사용합니다
- `ParallelStation.MU(n)`으로 n번째 MU에 접근합니다 (1-based 인덱스)
- MU 복제 시 속성을 수동으로 복사해야 합니다
- `@.CreationTime`으로 MU가 생성된 시뮬레이션 시간을 확인할 수 있습니다
