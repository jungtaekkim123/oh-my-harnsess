# 문자열 처리 — SimTalk 2.0 Code Examples

> Cross-reference: `references/16-fn-strings.md` for full function signatures

---

## Pattern 1: 기본 문자열 함수 — strLen, strCopy, strIncl, strLPos, strRpos

**Use when:** 문자열의 길이, 부분 추출, 위치 검색, 삽입 등 기본 조작이 필요할 때

```simtalk
var text : string := "Plant Simulation 2404"

// strLen: 문자열 길이
print strLen(text)             // 21

// strCopy: 부분 문자열 추출 (위치, 길이)
print strCopy(text, 1, 5)     // "Plant"
print strCopy(text, 7, 10)    // "Simulation"
print strCopy(text, 18, 10)   // "2404" (범위 초과 시 가능한 만큼 반환)

// strRcopy: 오른쪽에서 n자 복사
print strRcopy(text, 4)       // "2404"

// strLPos: 왼쪽부터 첫 번째 검색 (없으면 0)
print strLPos("Sim", text)    // 7

// strRpos: 오른쪽부터 마지막 위치 검색
var path : string := "C:\Models\SubFolder\Model.spp"
var lastSlash := strRpos("\", path)
print lastSlash                // 20
print strCopy(path, lastSlash + 1, strLen(path))  // "Model.spp"

// strIncl: 특정 위치 앞에 문자열 삽입
print strIncl("NEW_", "Station1", 1)    // "NEW_Station1"
print strIncl("_v2", "Station1", 9)     // "Station1_v2"

// strOmit: 특정 위치에서 n자 삭제
print strOmit("Hello World!", 6, 1)     // "HelloWorld!"
print strOmit("PREFIX_Data", 1, 7)      // "Data"
```

**Key points:**
- 모든 위치 인덱스는 **1-based**
- `strLPos`/`strRpos`는 못 찾으면 **0** 반환
- `strCopy`는 범위를 초과해도 에러 없이 가능한 만큼 반환

---

## Pattern 2: 문자열 분할 — splitString, splitStringToNum

**Use when:** 구분자로 연결된 문자열을 개별 값으로 분리할 때

```simtalk
// 기본 분할: 콤마 구분자
var csv := "Apple,Banana,Cherry,Date"
var items : string[] := splitString(csv, ",")
print items          // [Apple, Banana, Cherry, Date]
print items.dim      // 4

// 복수 구분자: 콤마와 세미콜론 동시 처리
var mixed := "one,two;three;four,five"
var parts := splitString(mixed, ",;")
print parts          // [one, two, three, four, five]

// 빈 항목 유지: KeepEmptyItems 옵션
var sparse := "A;;B;;C"
print splitString(sparse, ";")        // [A, B, C]
print splitString(sparse, ";", true)  // [A, , B, , C]

// 글자 단위 분해: 빈 구분자 사용
var word := "SimTalk"
var letters := splitString(word, "")
print letters        // [S, i, m, T, a, l, k]

// 숫자 문자열 분할: splitStringToNum
var numStr := "1.5;2.8;3.14;4.0"
var nums : real[] := splitStringToNum(numStr, ";")
print nums           // [1.5, 2.8, 3.14, 4.0]
print nums.sum       // 11.84

// 복수 구분자로 숫자 분할
var data := "10.5;20.3!30.1;40.8"
var values := splitStringToNum(data, ";!")
print values         // [10.5, 20.3, 30.1, 40.8]
```

**Key points:**
- 구분자에 여러 문자를 넣으면 **각 문자가 독립적으로** 구분자 역할
- `splitStringToNum`은 결과를 `real[]`로 반환 — 수치 파싱에 편리
- `KeepEmptyItems`를 `true`로 설정하면 빈 토큰도 배열에 포함

---

## Pattern 3: 검색 및 치환 — strSearchAndReplace

**Use when:** 문자열 내 특정 패턴을 다른 문자열로 일괄 치환할 때

```simtalk
// 기본 치환: 부분 문자열 교체
var original := "The quick brown fox jumps over the lazy dog"
var result := strSearchAndReplace(original, "fox", "cat")
print result         // "The quick brown cat jumps over the lazy dog"

// 구분자 변경: 세미콜론 → 콤마
var csvLine := "A;B;C;D;E"
var converted := strSearchAndReplace(csvLine, ";", ",")
print converted      // "A,B,C,D,E"

// 공백 제거
var padded := "  Station_01  "
var trimmed := strSearchAndReplace(padded, " ", "")
print trimmed        // "Station_01"

// 경로 구분자 변환
var winPath := "C:\Models\SubFolder\File.spp"
var urlPath := strSearchAndReplace(winPath, "\", "/")
print urlPath        // "C:/Models/SubFolder/File.spp"

// 태그 제거 예시
var tagged := "[ERROR] Connection failed"
var clean := strSearchAndReplace(tagged, "[ERROR] ", "")
print clean          // "Connection failed"
```

**Key points:**
- 모든 일치 항목이 **일괄** 치환됨 (첫 번째만이 아님)
- 복잡한 패턴 매칭이 필요하면 `regex_replace` 사용 권장
- 대소문자를 **구분**하여 치환

---

## Pattern 4: 정규표현식 — regex_search, regex_search2, regex_replace

**Use when:** 복잡한 패턴 매칭, 데이터 추출, 고급 텍스트 변환이 필요할 때

```simtalk
// regex_search: 첫 번째 매칭 문자열 반환
var log := "Error at 14:30pm in module Station_01"
var timeMatch := regex_search(log, "((1[0-2])|(0?[1-9])):([0-5][0-9])((am)|(pm))")
print timeMatch      // "14:30pm" — 실제로는 시간 형식에 맞는 첫 매칭

// 숫자 추출
var msg := "Throughput: 1234 parts/hour"
var numStr := regex_search(msg, "\\d+")
print numStr         // "1234"

// regex_search2: 모든 캡처 그룹을 배열로 반환
var email := "John.Doe@acme.com"
var parts := regex_search2(email, "(\\w*)\\.(\\w*)@(\\w*)\\.(\\w*)")
print parts
// [John.Doe@acme.com, John, Doe, acme, com, , ]
// parts[1] = 전체 매치, parts[2..5] = 캡처 그룹, 마지막 2개 = 전후 텍스트

// 이메일에서 도메인만 추출
var domain := parts[4] + "." + parts[5]
print domain         // "acme.com"

// regex_replace: 패턴 치환
// 모든 공백 제거
print regex_replace("Hello World Test", " ", "")
// "HelloWorldTest"

// 날짜 형식 변환: 2024/03/15 → 2024-03-15
var dateStr := "2024/03/15 12:30"
var converted := regex_replace(dateStr, "[/: ]", "-")
print converted      // "2024-03-15-12-30"

// 역참조($1, $2)를 사용한 재배치
var name := "Doe, John"
var reordered := regex_replace(name, "(\\w+), (\\w+)", "$2 $1")
print reordered      // "John Doe"

// HTML 태그 추출
var html := "before<h1>Title</h1>after"
var tag := regex_search(html, "<(.+)>(.*)</(\1)>")
print tag            // "<h1>Title</h1>"
```

**Key points:**
- SimTalk에서 백슬래시는 이스케이프 문자 — `\d`는 `"\\d"`로 작성
- `regex_search2`는 `[전체매치, 그룹1, ..., 그룹N, 앞텍스트, 뒤텍스트]` 배열 반환
- 백슬래시 자체를 검색하려면 `"\\\\\\\\"` (4개) 필요

---

## Pattern 5: 문자열 포매팅 — num_to_str + 문자열 조립

**Use when:** 숫자를 특정 형식의 문자열로 변환하거나 보고용 텍스트를 생성할 때

```simtalk
// 기본 문자열 결합 (+ 연산자)
var stationName := "Station"
var stationNum := 3
var label := stationName + "_" + to_str(stationNum)
print label          // "Station_3"

// num_to_str: 숫자를 형식 지정 문자열로 변환
var throughput := 1234.567
print num_to_str(throughput, "#,##0.00")   // "1,234.57"
print num_to_str(throughput, "0.0")        // "1234.6"

// 퍼센트 형식
var rate := 0.956
print num_to_str(rate * 100, "0.0") + "%"  // "95.6%"

// 여러 값을 조합한 보고 문자열 생성
var partName := "PartA"
var count := 150
var avgTime := 23.456
var report := "Part: " + partName + " | Count: " + to_str(count) + " | AvgTime: " + num_to_str(avgTime, "0.00") + "s"
print report
// "Part: PartA | Count: 150 | AvgTime: 23.46s"

// 배열을 join으로 조합하여 CSV 행 생성
var row : string[] := [partName, to_str(count), num_to_str(avgTime, "0.00")]
var csvRow := row.join(";")
print csvRow         // "PartA;150;23.46"
```

**Key points:**
- `to_str()`은 기본 형식으로 변환, `num_to_str()`은 포맷 문자열 지정 가능
- `#`은 선택적 자릿수, `0`은 필수 자릿수를 의미
- 문자열 결합은 `+` 연산자 또는 `print`의 콤마 구분 사용

---

## Pattern 6: 대소문자 변환 및 트리밍 — strToLower, strToUpper, strTrim

**Use when:** 사용자 입력 정규화, 비교용 변환, 공백 제거가 필요할 때

```simtalk
// 대문자로 변환
print strToUpper("hello world")      // "HELLO WORLD"
print strToUpper("Station_01a")      // "STATION_01A"

// 소문자로 변환
print strToLower("PRODUCTION LINE")  // "production line"

// 대소문자 무시 비교
var input := "Station_A"
if strToLower(input) = strToLower("station_a")
    print "동일한 스테이션입니다"
end

// strTrim: 앞뒤 공백, 탭, 캐리지리턴 제거
print strTrim("  hello  ")           // "hello"
print strTrim("	data	")              // "data" (탭 제거)

// 트리밍 후 비교 — 공백 차이 무시
if strTrim("  hello  ") = strTrim("hello    ")
    print "트리밍 후 동일합니다"       // 항상 도달
end

// strAscii + strChr: 문자 코드 변환
print strAscii("A")                  // 65
print strChr(65)                     // "A"
print strChr(9)                      // 탭 문자

// 특수 문자 포함 문자열 생성
var header := "Name" + strChr(9) + "Value" + strChr(9) + "Unit"
print header         // "Name	Value	Unit" (탭 구분)
```

**Key points:**
- `strTrim`은 앞뒤 공백만 제거 — 중간 공백은 유지
- `strToLower`/`strToUpper`는 특수문자와 숫자를 변환하지 않음
- `strChr(9)`는 탭, `strChr(10)`은 줄바꿈 — CSV/TSV 생성에 유용
