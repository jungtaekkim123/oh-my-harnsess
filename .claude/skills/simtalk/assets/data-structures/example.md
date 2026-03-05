# 데이터 구조 — SimTalk 2.0 Code Examples

> Cross-reference: `references/08-datatypes-array.md`, `references/09-datatypes-json.md`, `references/10-datatypes-collections.md` for full function signatures

---

## Pattern 1: 배열 기본 — 선언, 초기화, 인덱싱, 순회

**Use when:** 고정 크기/가변 크기 배열을 선언하고 값에 접근할 때

```simtalk
// 고정 크기 1차원 배열 (크기 5, 기본값 0)
var scores : integer[5]
scores[1] := 100
scores[2] := 85
scores[3] := 92

// 가변 크기 배열 (초기 크기 없음)
var names : string[]

// 리터럴로 초기화
var primes : integer[] := [2, 3, 5, 7, 11]

// any 타입 배열 — 서로 다른 타입 저장 가능
var mixed : any[] := ["Station1", 42, 3.14, true]

// for 루프로 배열 순회 (인덱스는 1부터 시작)
for var i := 1 to primes.dim
    print "primes[", i, "] = ", primes[i]
next

// 빈 배열 확인
var empty : real[]
if empty.empty
    print "배열이 비어 있습니다. dim = ", empty.dim
end
```

**Key points:**
- 배열 인덱스는 **1-based** (0이 아님)
- `var a : integer[5]`는 고정 크기, `var a : integer[]`는 가변 크기
- `any[]` 타입은 서로 다른 타입의 값을 혼합 저장 가능

---

## Pattern 2: 배열 메서드 — append, sort, contains, find, delete, join

**Use when:** 배열 내 요소를 동적으로 추가/삭제/검색할 때

```simtalk
// append: 가변 크기 배열에 요소 추가
var fruits : string[]
fruits.append("Apple")
fruits.append("Banana")
fruits.append("Cherry")
fruits.append("Banana")
print fruits          // [Apple, Banana, Cherry, Banana]
print fruits.dim      // 4

// contains: 값 포함 여부 확인
if fruits.contains("Banana")
    print "Banana 존재"
end

// find: 값의 인덱스 반환 (없으면 0)
var idx := fruits.find("Cherry")
print "Cherry 위치: ", idx  // 3

// find with StartIndex: 특정 위치부터 검색
var idx2 := fruits.find("Banana", 3)
print "두 번째 Banana 위치: ", idx2  // 4

// sort: 오름차순/내림차순 정렬
var nums : integer[] := [4, 2, 1, 3]
nums.sort            // 오름차순 (기본값)
print nums           // [1, 2, 3, 4]
nums.sort(true)      // 내림차순
print nums           // [4, 3, 2, 1]

// delete: 인덱스로 요소 삭제
fruits.delete(2)     // 인덱스 2의 "Banana" 삭제
print fruits         // [Apple, Cherry, Banana]

// deleteValue: 값으로 첫 번째 일치 항목 삭제
fruits.deleteValue("Banana")
print fruits         // [Apple, Cherry]

// join: 배열을 구분자로 결합하여 문자열로 변환
var tags : string[] := ["urgent", "production", "line-A"]
var result := tags.join(", ")
print result         // urgent, production, line-A

// pop: 마지막 요소 제거 후 반환
var stack : integer[] := [10, 20, 30]
var last := stack.pop
print last           // 30
print stack          // [10, 20]

// insert: 특정 위치에 삽입
stack.insert(1, 5)
print stack          // [5, 10, 20]

// appendArray: 다른 배열 전체를 이어 붙이기
var extra : integer[] := [40, 50]
stack.appendArray(extra)
print stack          // [5, 10, 20, 40, 50]

// min, max, sum
var values : real[] := [1.1, 2.2, 3.3, 4.4, 5.5]
print values.min     // 1.1
print values.max     // 5.5
print values.sum     // 16.5
```

**Key points:**
- `append`, `delete`, `insert`, `pop`은 **가변 크기** 배열에만 적용
- `find`는 못 찾으면 **0**을 반환 (1-based이므로 0은 "없음")
- `sort`의 기본값은 오름차순 (`false`), `true`로 내림차순 지정

---

## Pattern 3: 2차원 배열 — 선언, xDim, yDim 접근

**Use when:** 행렬 형태의 데이터나 좌표 기반 데이터를 다룰 때

```simtalk
// 2차원 배열 선언: real[열수, 행수]
var matrix : real[3, 4]   // 3열 x 4행

// 차원 확인
print matrix.xDim    // 3 (열 수)
print matrix.yDim    // 4 (행 수)

// 중첩 for 루프로 값 채우기
for var x := 1 to matrix.xDim
    for var y := 1 to matrix.yDim
        matrix[x, y] := x * 10 + y
    next
next
print matrix
// [11, 12, 13, 14][21, 22, 23, 24][31, 32, 33, 34]

// 3D 좌표 배열 — X, Y, Z 속성 사용
var pos : real[3] := [100.0, 200.0, 50.0]
print pos.X          // 100 (= pos[1])
print pos.Y          // 200 (= pos[2])
print pos.Z          // 50  (= pos[3])
pos.X := 150.0       // pos[1] := 150.0

// 1차원 vs 2차원 구별: yDim이 0이면 1차원
var arr1d : real[] := [1.0, 2.0, 3.0]
if arr1d.yDim = 0
    print "1차원 배열입니다"
end
```

**Key points:**
- 2차원 배열은 `real[xDim, yDim]` 형식 — `[열, 행]` 순서
- `X`, `Y`, `Z` 속성은 크기 3인 고정 배열 전용 (3D 좌표용)
- `yDim = 0`이면 1차원 배열로 판별 가능

---

## Pattern 4: JSON 생성 및 파싱

**Use when:** 외부 시스템과 데이터를 주고받거나 구조화된 데이터를 관리할 때

```simtalk
// JSON 객체 생성 — 이름-값 쌍
var person : json
person["Name"] := "Kim"
person["Age"] := 35
person["Department"] := "Production"

// 중첩 JSON — getOrCreateJSON으로 하위 객체 생성
var address := person.getOrCreateJSON("Address")
address["City"] := "Seoul"
address["ZipCode"] := "06123"

// 중첩 값 접근
print person["Address"]["City"]  // Seoul

// JSON 배열 저장
person["Skills"] := ["SimTalk", "Python", "SQL"]

// 문자열 변환 (직렬화)
var jsonStr := person.asString(false)  // 한 줄 출력
print jsonStr

// 문자열 → JSON 파싱
var parsed : json
parsed.parse("{\"count\": 42, \"label\": \"test\"}")
print parsed["count"]   // 42
print parsed["label"]   // test

// JSON 순회 — 인덱스 기반 접근 (.Name, .Value)
var config : json
config["host"] := "192.168.1.100"
config["port"] := 8080
config["protocol"] := "TCP"
for var i := 1 to config.dim
    print config[i].Name, " = ", config[i].Value
next

// contains: 키 존재 여부 확인
if person.contains("Name")
    print "Name 키가 존재합니다"
end

// delete: 특정 키 삭제 (대소문자 구분!)
person.delete("Age")

// copy: 독립 복사본 생성 (기본 대입은 참조 공유)
var backup := person.copy
backup["Name"] := "Lee"
print person["Name"]   // Kim (원본 유지)
print backup["Name"]   // Lee
```

**Key points:**
- JSON 이름은 **대소문자 구분** — `"Name"`과 `"name"`은 다른 키
- 일반 대입(`a := b`)은 **참조 공유**, `.copy`를 써야 독립 복사
- `getOrCreateJSON`은 중첩 JSON을 안전하게 생성/접근하는 핵심 메서드

---

## Pattern 5: JSON ↔ 테이블 변환

**Use when:** JSON 배열 데이터를 DataTable에 넣거나 테이블 데이터를 다른 형태로 가공할 때

```simtalk
// JSON 배열 → 테이블 열(column)에 복사
var data : json
data["partNames"] := ["PartA", "PartB", "PartC"]
data["partNames"].copyToTableColumn(DataTable, 1)
// DataTable의 1열에 PartA, PartB, PartC가 들어감

// JSON 배열 → 테이블 행(row)에 복사
var row : json
row["values"] := ["Line1", 100, 95.5]
row["values"].copyToTableRow(DataTable, 2)
// DataTable의 2행에 Line1, 100, 95.5가 들어감

// JSON 파싱 후 테이블에 일괄 기록
var rawJson : string := "{\"items\": [\"X1\", \"X2\", \"X3\"]}"
var j : json
j.parse(rawJson)
j["items"].copyToTableColumn(ResultTable, 1)
```

**Key points:**
- `copyToTableColumn`은 JSON 배열을 테이블의 세로 열에 배치
- `copyToTableRow`는 JSON 배열을 테이블의 가로 행에 배치
- 배열 요소 개수만큼 테이블 셀이 채워짐

---

## Pattern 6: 배열 ↔ 테이블 변환

**Use when:** 배열 데이터를 테이블로 내보내거나, 테이블 데이터를 배열로 읽어올 때

```simtalk
// 배열 → 테이블 열에 복사
var stations : string[] := ["Station_A", "Station_B", "Station_C"]
stations.copyToTableColumn(DataTable, 1)

// 배열 → 테이블의 특정 위치에 복사
var throughputs : real[] := [125.5, 98.3, 110.7]
throughputs.copyToTable(DataTable, 2, 1)  // 2열, 1행부터

// 테이블 열 → 배열로 읽기
var readNames : string[]
readNames.copyFromTableColumn(DataTable, 1)
print readNames  // [Station_A, Station_B, Station_C]

// 테이블 전체 → 배열로 읽기
var allData : any[]
allData.copyFromTable(DataTable)

// putValuesIntoTable: 속성의 허용 값 목록을 테이블에 채우기
var valueList : list[string]
valueList.create
MyStation.ResourceType.putValuesIntoTable(valueList)
// valueList에 "Production", "Transport", "Storage" 등이 채워짐
```

**Key points:**
- `copyToTableColumn` / `copyFromTableColumn`은 단일 열 단위 변환
- `copyToTable`은 시작 위치(열, 행)를 지정할 수 있음
- `putValuesIntoTable`은 드롭다운 속성의 허용 값 목록을 가져올 때 사용

---

## Pattern 7: createNestedList — 중첩 리스트/테이블

**Use when:** 테이블 안에 하위 테이블(서브테이블)을 만들어 계층적 데이터를 저장할 때

```simtalk
// 테이블 타입 열을 가진 테이블 생성
var masterTable : table[string, table]
masterTable.create(3)

// 1행에 서브테이블 생성
masterTable[1, 1] := "Line_A"
masterTable.createNestedList(2, 1)  // 2열 1행에 서브테이블 생성
masterTable[2, 1][1, 1] := "Product_X"
masterTable[2, 1][2, 1] := 500

// 2행에 서브테이블 생성
masterTable[1, 2] := "Line_B"
masterTable.createNestedList(2, 2)
masterTable[2, 2][1, 1] := "Product_Y"
masterTable[2, 2][2, 1] := 300

// 서브테이블 참조로 접근
var sub : table := masterTable[2, 1]
print sub[1, 1]  // Product_X

// List 타입으로 중첩 리스트 생성
var outerList : list[list]
outerList.create(2)
var innerList := outerList.createNestedList(1, 1)
innerList.insert(1, "Hello")
innerList.insert(2, "World")
print outerList[1, 1][1, 1]  // Hello

// 중첩 any 배열 — 배열 안의 배열
var nested : any[] := [[1, 2, 3], ["A", "B"], [true, false]]
print nested[1]       // [1, 2, 3]
print nested[2]       // [A, B]
print isArray(nested[1])  // true
```

**Key points:**
- `createNestedList(Column, Row)`로 셀 안에 하위 테이블/리스트 생성
- 중첩 접근: `masterTable[2,1][1,1]` — 외부 셀 → 내부 셀 순서
- `any[]` 배열도 중첩 가능하며 `isArray()`로 타입 확인
- 중첩 구조의 열 타입은 반드시 `table`, `list`, `stack`, `queue` 중 하나
