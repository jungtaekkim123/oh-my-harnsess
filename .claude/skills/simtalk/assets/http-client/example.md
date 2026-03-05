# HTTP 클라이언트 — SimTalk 2.0 코드 예제

> 상호 참조: `references/18-fn-http.md` — 전체 함수 시그니처 참조

## 패턴 1: 간단한 GET 요청

**사용 시점:** REST API에서 데이터를 조회할 때

```simtalk
// 기본 GET 요청 — URL만 지정하여 응답 받기
var url: string := "https://api.example.com/items"
var responseBody: json

var statusCode: integer := httpGetRequest(url, responseBody)

if statusCode = 200
    print "성공: " + to_str(responseBody)
else
    print "실패 — HTTP " + to_str(statusCode)
end
```

**핵심 포인트:**
- `httpGetRequest`는 HTTP 상태 코드(integer)를 반환
- `responseBody`를 `json` 타입으로 선언하면 자동으로 JSON 파싱
- `string` 타입으로 선언하면 원시 텍스트로 수신

---

## 패턴 2: 헤더를 포함한 GET 요청

**사용 시점:** 인증 토큰, Content-Type 등 커스텀 헤더가 필요할 때

```simtalk
// Bearer 토큰 인증을 사용한 GET 요청
var url: string := "https://api.example.com/users/42"
var requestHeaders: json
requestHeaders["Authorization"] := "Bearer eyJhbGciOiJIUzI1..."
requestHeaders["Accept"] := "application/json"

var responseBody: json
var responseHeaders: json

var statusCode: integer := httpGetRequest(url, responseBody, requestHeaders, responseHeaders)

if statusCode = 200
    print "사용자 이름: " + responseBody["name"]
    // 응답 헤더에서 Content-Type 확인
    print "Content-Type: " + to_str(responseHeaders["Headers"]["Content-Type"])
elseif statusCode = 401
    print "인증 실패 — 토큰을 확인하세요"
end
```

**핵심 포인트:**
- `RequestHeader`는 json 또는 string 타입 모두 가능
- json 타입이면 `headers["키"] := "값"` 형태로 설정
- `ResponseHeader`는 `byref`로 전달 — 변수를 선언만 하면 자동으로 채워짐

---

## 패턴 3: JSON 본문을 포함한 POST 요청

**사용 시점:** 새 리소스를 생성하거나 서버에 데이터를 전송할 때

```simtalk
// JSON 페이로드로 POST 요청 보내기
var url: string := "https://api.example.com/items"

// 요청 본문 구성
var requestBody: json
requestBody["name"] := "Conveyor Belt A"
requestBody["type"] := "transport"
requestBody["speed"] := 2.5
requestBody["active"] := true

// 헤더 설정 — json 본문이면 Content-Type은 자동으로 application/json 설정됨
var requestHeaders: json
requestHeaders["Authorization"] := "Bearer eyJhbGciOiJIUzI1..."

var responseBody: json
var responseHeaders: json

var statusCode: integer := httpPostRequest(url, requestBody, requestHeaders, responseHeaders, responseBody)

if statusCode = 200 or statusCode = 201
    print "생성 완료 — ID: " + to_str(responseBody["id"])
else
    print "생성 실패 — HTTP " + to_str(statusCode)
    print "에러: " + to_str(responseBody)
end
```

**핵심 포인트:**
- `RequestBody`가 json 타입이면 Content-Type `application/json`이 자동 추가됨
- `httpPostRequest` 시그니처: `(URL, RequestBody[, RequestHeader, byref ResponseHeader, byref ResponseBody]) -> integer`
- 동일한 POST를 반복하면 매번 다른 결과를 반환할 수 있음 (비멱등)

---

## 패턴 4: PUT 요청으로 리소스 수정

**사용 시점:** 기존 리소스를 업데이트할 때

```simtalk
// PUT 요청 — 기존 리소스 전체 교체
var itemId: integer := 42
var url: string := "https://api.example.com/items/" + to_str(itemId)

var requestBody: json
requestBody["name"] := "Conveyor Belt A (Updated)"
requestBody["type"] := "transport"
requestBody["speed"] := 3.0
requestBody["active"] := false

var responseBody: json
var responseHeaders: json

var statusCode: integer := httpPutRequest(url, requestBody, "", responseHeaders, responseBody)

if statusCode = 200
    print "업데이트 완료"
elseif statusCode = 404
    print "항목을 찾을 수 없음 — ID: " + to_str(itemId)
end
```

**핵심 포인트:**
- `httpPutRequest`는 멱등 — 동일한 요청을 반복해도 같은 결과
- 시그니처: `(URL, RequestBody[, RequestHeader, byref ResponseHeader, byref ResponseBody]) -> integer`
- `RequestHeader`에 빈 문자열 `""`을 넘기면 기본 헤더만 사용

---

## 패턴 5: DELETE 요청

**사용 시점:** 서버에서 리소스를 삭제할 때

```simtalk
// DELETE 요청 — 리소스 삭제
var itemId: integer := 42
var url: string := "https://api.example.com/items/" + to_str(itemId)

var requestHeaders: json
requestHeaders["Authorization"] := "Bearer eyJhbGciOiJIUzI1..."

var responseHeaders: json
var responseBody: string

var statusCode: integer := httpDeleteRequest(url, requestHeaders, "", responseHeaders, responseBody)

switch statusCode
    case 200
        print "삭제 완료"
    case 204
        print "삭제 완료 (응답 본문 없음)"
    case 404
        print "이미 삭제되었거나 존재하지 않는 항목"
    case 401
        print "인증 실패"
end
```

**핵심 포인트:**
- `httpDeleteRequest` 시그니처: `(URL[, RequestHeader, RequestBody, byref ResponseHeader, byref ResponseBody]) -> integer`
- DELETE도 RequestBody를 보낼 수 있음 (서버에 따라 다름)
- `switch`/`case`로 다양한 상태 코드를 처리

---

## 패턴 6: URL 동적 구성

**사용 시점:** 쿼리 파라미터가 있는 URL을 안전하게 조합할 때

```simtalk
// httpCreateURL로 URL 요소를 조합하여 올바른 URL 생성
var urlData: json
urlData["Scheme"] := "https"
urlData["Server"] := "api.example.com"
urlData["Port"] := 443
urlData["Path"] := "/v2/search"

// 쿼리 파라미터를 Extra에 json으로 지정
var queryParams: json
queryParams["q"] := "conveyor belt"
queryParams["limit"] := "10"
queryParams["offset"] := "0"
urlData["Extra"] := queryParams

var url: string := httpCreateURL(urlData)
print url
// 결과: https://api.example.com/v2/search?q=conveyor%20belt&limit=10&offset=0

// form-url-encoded 문자열 직접 생성도 가능
var formData: json
formData["username"] := "admin"
formData["password"] := "p@ssw0rd"
var encoded: string := httpCreateFormUrlEncodedString(formData)
print encoded
// 결과: username=admin&password=p%40ssw0rd
```

**핵심 포인트:**
- `httpCreateURL`은 json 구조에서 올바른 URL 문자열을 생성
- `Extra`에 json을 넣으면 쿼리 파라미터가 자동으로 URL 인코딩됨
- `httpCreateFormUrlEncodedString`은 특수문자를 Quoted-Printable 인코딩 처리

---

## 패턴 7: 타임아웃 설정

**사용 시점:** 네트워크가 느린 환경이나 응답 시간 제한이 필요할 때

```simtalk
// 현재 타임아웃 값 조회 (밀리초 단위)
var resolve: integer
var connect: integer
var send: integer
var receive: integer
httpGetTimeouts(resolve, connect, send, receive)
print "현재 타임아웃 — Resolve: " + to_str(resolve) + "ms, Connect: " + to_str(connect) + "ms"
// 기본값: resolve=-1(무한), connect=60000, send=30000, receive=30000

// 타임아웃 설정 변경
// (ResolveTimeout, ConnectionTimeout, SendTimeout, ReceiveTimeout)
httpSetTimeouts(120000, 60000, 15000, 15000)
// resolve: 120초, connect: 60초, send/receive: 각 15초

// 설정 후 HTTP 요청 수행
var responseBody: json
var statusCode: integer := httpGetRequest("https://api.example.com/data", responseBody)
```

**핵심 포인트:**
- 모든 타임아웃 값은 밀리초(ms) 단위
- 값이 `0` 또는 `-1`이면 무한 대기 (타임아웃 없음)
- 음수(-1 제외)를 지정하면 유효하지 않은 파라미터 오류 발생
- 타임아웃은 전역 설정 — 한번 변경하면 이후 모든 HTTP 요청에 적용

---

## 패턴 8: 에러 처리

**사용 시점:** HTTP 요청 실패 시 안전하게 처리하고 싶을 때

```simtalk
// 에러 처리를 위한 ErrorHandler 패턴
//
// 메인 메서드: FetchData
var url: string := "https://api.example.com/data"
var responseBody: json
var responseHeaders: json

var statusCode: integer := httpGetRequest(url, responseBody, "", responseHeaders)

// HTTP 상태 코드 기반 분기 처리
switch statusCode
    case 200
        print "성공"
        // 응답 데이터 처리
        var contentType: string := to_str(responseHeaders["Headers"]["Content-Type"])
        print "응답 타입: " + contentType
    case 401
        print "인증 오류 — 토큰이 만료되었을 수 있습니다"
    case 403
        print "접근 거부 — 권한을 확인하세요"
    case 404
        print "리소스를 찾을 수 없음"
    case 500
        print "서버 내부 오류 — 잠시 후 재시도하세요"
    else
        print "예상치 못한 상태 코드: " + to_str(statusCode)
end
```

```simtalk
// ErrorHandler 메서드 — 런타임 에러를 잡아서 처리
// (Method의 사용자 정의 속성으로 ErrorHandler를 지정)
//
// ErrorHandler 시그니처:
//   param error: string, method_path: string, line_number: integer -> any

param error: string, method_path: string, line_number: integer -> any

if strIncl(error, "timeout") or strIncl(error, "connection")
    // 네트워크 에러 → 에러 로그를 남기고 에러를 삼킴
    print "네트워크 오류 [" + method_path + ":" + to_str(line_number) + "]: " + error
    error := ""   // 에러 메시지를 비우면 에러가 처리된 것으로 간주
    return false
end

// 처리하지 않은 에러 → 호출 체인 위로 전파
error := "HTTP 오류 in " + method_path + ": " + error
```

**핵심 포인트:**
- SimTalk는 `try/catch` 대신 `ErrorHandler` 메서드 패턴을 사용
- ErrorHandler에서 `error := ""`로 비우면 에러가 "처리됨"으로 간주
- 에러 메시지를 비우지 않으면 호출 체인의 상위 ErrorHandler로 전파
- HTTP 상태 코드는 항상 반환되므로, 먼저 상태 코드로 분기 처리하는 것이 권장됨
