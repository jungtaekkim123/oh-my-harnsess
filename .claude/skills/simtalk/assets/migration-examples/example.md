# 마이그레이션 — SimTalk 1.0 → 2.0 변환 예제

> 상호 참조: `references/02-migration.md` — 전체 비교 테이블 및 Outdated 함수 목록

## 패턴 1: 변수 선언

**사용 시점:** 기존 1.0 코드의 변수 선언을 2.0으로 변환할 때

### SimTalk 1.0 (이전)
```simtalk
is
    s: string;
    count: integer;
    rate: real;
do
    s := "hello";
    count := 0;
    rate := 1.5;
end;
```

### SimTalk 2.0 (현재)
```simtalk
var s: string := "hello"
var count: integer := 0
var rate: real := 1.5
```

**주요 변경:**
- `is ... do ... end;` 블록 구조가 제거됨 — `var` 키워드로 어디서든 선언
- `local` 키워드 → `var` 키워드로 대체
- 세미콜론(`;`) 불필요 — 줄바꿈으로 문장 구분
- 선언과 동시에 초기화 가능

---

## 패턴 2: 반복문 (Loop)

**사용 시점:** `do...loop`, `do...while` 등 1.0 반복문을 변환할 때

### SimTalk 1.0 (이전)
```simtalk
-- for 루프
for local i := 1 to 10 loop
    print i;
next;

-- while 루프
while a < 10 loop
    a := a + 1;
    print a;
end;

-- repeat 루프
repeat
    a := a + 1;
    print a;
until a > 10;
```

### SimTalk 2.0 (현재)
```simtalk
// for 루프 — loop 키워드 제거
for var i := 1 to 10
    print i
next

// while 루프 — loop 키워드 제거
while a < 10
    a += 1
    print a
end

// repeat 루프 — 동일한 구조, 세미콜론만 제거
repeat
    a += 1
    print a
until a > 10
```

**주요 변경:**
- `for` 문: `loop` 키워드 제거, `local` → `var`
- `while` 문: `loop` 키워드 제거
- `repeat` 문: 구조는 동일, 세미콜론만 제거
- `a := a + 1` → `a += 1` 복합 대입 연산자 사용 가능
- 주석: `--` → `//` (한 줄), `/* */` (여러 줄)

---

## 패턴 3: 조건문 (If/Else)

**사용 시점:** `if...then...end;` 구문을 2.0으로 변환할 때

### SimTalk 1.0 (이전)
```simtalk
if a > 3 then
    print a;
end;

if x = 1 then
    print "one";
elseif x = 2 then
    print "two";
else
    print "other";
end;

-- inspect (switch의 이전 이름)
inspect a
    when 1 then print 1;
    when 2 then print 2;
end;
```

### SimTalk 2.0 (현재)
```simtalk
if a > 3
    print a
end

if x = 1
    print "one"
elseif x = 2
    print "two"
else
    print "other"
end

// inspect → switch/case
switch a
    case 1
        print 1
    case 2
        print 2
end
```

**주요 변경:**
- `then` 키워드 제거 — `if 조건` 바로 다음 줄에 본문 작성
- `inspect ... when ... then` → `switch ... case`
- 모든 세미콜론 제거

---

## 패턴 4: 메서드 파라미터 선언

**사용 시점:** 메서드의 인자 선언 방식을 변환할 때

### SimTalk 1.0 (이전)
```simtalk
-- 메서드 시그니처 (괄호 안에 세미콜론으로 구분)
(v1, v2: integer; name: string)
is
do
    print v1 + v2;
    print name;
end;
```

### SimTalk 2.0 (현재)
```simtalk
// param 키워드로 선언, 콤마로 구분
param v1, v2: integer, name: string

print v1 + v2
print name
```

**주요 변경:**
- 괄호 `(...)` 제거 → `param` 키워드 사용
- 세미콜론 구분 → 콤마(`,`)로 그룹 구분
- `is ... do ... end;` 블록 제거 — 바로 본문 작성

---

## 패턴 5: 반환값 선언

**사용 시점:** 메서드의 반환 타입 선언을 변환할 때

### SimTalk 1.0 (이전)
```simtalk
-- 반환 타입을 콜론으로 선언
(x: integer; y: integer): real
is
do
    result := sqrt(x * x + y * y);
end;
```

### SimTalk 2.0 (현재)
```simtalk
// 화살표(->)로 반환 타입 선언
param x: integer, y: integer -> real

return sqrt(x * x + y * y)
```

```simtalk
// 파라미터 없이 반환 타입만 선언할 때
-> string

return "Hello, SimTalk 2.0"
```

**주요 변경:**
- `: 반환타입` → `-> 반환타입` 화살표 표기법
- `result := 값` → `return 값` 명시적 반환문
- 빈 메서드(`is do end;`)가 더 이상 필요하지 않음

---

## 패턴 6: 연산자 변경

**사용 시점:** 1.0과 2.0 사이의 연산자 차이를 확인할 때

### SimTalk 1.0 (이전)
```simtalk
-- 근사 비교 (about-equal)
if a == b then
    print "approximately equal";
end;

-- 나눗셈 / 나머지
var quotient: integer := x // y;
var remainder: integer := x \ y;

-- 누적 연산 (복합 대입 없음)
count := count + 1;
total := total - x;
factor := factor * 2;

-- 참조 연산자
var m: method := .ref(.Models.Model.Method);
```

### SimTalk 2.0 (현재)
```simtalk
// 근사 비교 — ~= 연산자
if a ~= b
    print "approximately equal"
end

// ~= 변형: 이상 근사, 이하 근사
if a >~= b
    print "a is approximately >= b"
end

// 나눗셈 / 나머지 — 키워드 연산자
var quotient: integer := x div y
var remainder: integer := x mod y

// 복합 대입 연산자 (SimTalk 2.0에서 추가)
count += 1
total -= x
factor *= 2

// 참조 연산자 — & 사용
var m: method := .Models.Model.&Method
```

**주요 변경:**
- 근사 비교: `==` → `~=`, `<==` → `<~=`, `>==` → `>~=`
- 정수 나눗셈: `//` → `div`
- 나머지 연산: `\` → `mod`
- 복합 대입: `+=`, `-=`, `*=` 신규 추가 (1.0에서는 없었음)
- 참조: `.ref(.Path)` → `.Path.&Name` (`&` 연산자)

---

## 패턴 7: Outdated 함수 이름 변환

**사용 시점:** 이전 버전의 함수/속성 이름을 현재 이름으로 변환할 때

### SimTalk 1.0 (이전)
```simtalk
-- 속성 접근 (이전 이름)
var isAvail := myStation.Available;
var cnt := myStation.numIn;
var outCnt := myStation.numOut;

-- 객체 생성/삭제
myFrame.createBuildingBlock("Entity", ".MUs.Entity");
myFrame.deleteBuildingBlock("OldEntity");

-- 속성 조작
myObj.createAttribute("Priority", 0);
myObj.deleteAttribute("OldAttr");
myObj.numAttributes;

-- 상태 제어
myStation.setActive;
myStation.setInactive;
myStation.stop;
myStation.continue;

-- 기타 유틸리티
promptMessage("정말 삭제하시겠습니까?");
print version;
var localTime := getLocalTime;
```

### SimTalk 2.0 (현재)
```simtalk
// 속성 접근 (현재 이름)
var isFailed := myStation.Failed
var isPaused := myStation.Pause
var isUnplanned := myStation.Unplanned
var cnt := myStation.StatNumIn
var outCnt := myStation.StatNumOut

// 객체 생성/삭제
myFrame.derive("Entity", ".MUs.Entity")
myFrame.deleteObject("OldEntity")

// 속성 조작
myObj.createAttr("Priority", 0)
myObj.deleteAttr("OldAttr")
myObj.NumAttr

// 상태 제어
myStation.endPause          // setActive →
myStation.startPause        // setInactive →
myStation.Stopped := true   // stop →
myStation.Stopped := false  // continue →

// 기타 유틸리티
messageBox("정말 삭제하시겠습니까?")
print applicationVersion
var localTime := sysDate
```

**주요 변경 (자주 사용되는 항목):**

| 1.0 이전 이름 | 2.0 현재 이름 |
|---|---|
| `Available` | `Failed` / `Pause` / `Unplanned` |
| `numIn` / `numOut` | `StatNumIn` / `StatNumOut` |
| `createBuildingBlock` | `derive` 또는 `duplicate` |
| `deleteBuildingBlock` | `deleteObject` |
| `createAttribute` | `createAttr` |
| `deleteAttribute` | `deleteAttr` |
| `numAttributes` | `NumAttr` |
| `setActive` | `endPause` |
| `setInactive` | `startPause` |
| `stop` / `continue` | `Stopped := true/false` |
| `promptMessage` | `messageBox` |
| `version` | `applicationVersion` |
| `getLocalTime` | `sysDate` |
| `stDev` | `standardDeviation` |
| `methcall` | `executeIn` |
| `newCallChain` | `executeNewCallChain` |
| `increment` | `+=` 연산자 |
| `paste` | `insertList` |
| `pasteRow` | `insertRow` |
| `pasteColumn` | `insertColumn` |

> **팁:** Plant Simulation의 Debugger 리본 탭에서 **Find Outdated Functions** 명령을 사용하면
> 시뮬레이션 모델 내 모든 Outdated 함수를 자동으로 찾아줍니다.
> Method 편집기에서 **New Syntax** 버튼을 클릭하면 1.0 → 2.0 자동 변환도 지원됩니다.
