# Burp Suite
## 1. 웹 프록시 툴 정의
웹 프록시는 사용자와 서버간의 통신시 사용자의 요청과 서버의 응답에 대한 데이터를 중간에 가로채어 확인할 수 있는 툴.
쉽게 설명을 이어간다면 사용자는 특정 A사이트에 접속 및 로그인 시도. 이때 사용자는 계정정보를 입력하고 로그인 완료. 이와 같이 짧고 단순해보이는 과정이지만 사용자가 입력한 값을 서버에서는 이를 받아 확인하고 검증을 통해 다시 사용자에게 결과를 반환.
이때 사용자가 입력하여 서버로 요청을 보낼 때 프록시 툴을 이용하면 서버로 바로 데이터가 넘어가는 것이 아니라 툴에 한번 걸리면서 잠시 대기 상태가 되는것. 이때 툴 사용자는 툴을 통해 통신중인 데이터를 확인할 수 있으며 어떤 정보가 서로 주고 받는지 확인이 가능. 이를 통해 툴 사용자는 요청 값 및 응답 값을 확인 및 변조를 할 수 있으며  보통 WEB 등의 HTTP 통신을 사용하는 것을 도청 가능.

### C2 IP (Command and Control IP)
- 정의 : C2 IP는 Command and Control IP의 약자로, 악성 소프트웨어가 감염된 시스템을 원격으로 제어하기 위해 사용하는 서버의 IP 주소. 이 서버는 해커가 감염된 시스템에 명령을 보내고 데이터를 수집하는 데 사용.
- 기능 :
1. 명령 전송 : C2 서버는 감염된 시스템에 명령을 전송하여 특정 작업을 수행
2. 데이터 수집 : 감염된 시스템에서 수집된 데이터를 C2 서버로 전송
3. 악성 코드 업데이트 : C2 서버는 감염된 시스템에 새로운 악성 코드를 다운로드하거나 기존 코드를 업데이트할 수 있음.
- 위험성 : C2 IP는 사이버 공격의 중심으로, 해커가 시스템을 제어하고 데이터를 유출할 수 있는 경로를 제공. 따라서 보안 시스템에서 C2 IP를 차단하는 것이 중요.

### X-Forwarded-For(XFF)
- 정의 : X-Forwarded-For는 HTTP 헤더의 일종으로, 클라이언트의 실제 IP 주소를 서버에 전달하기 위해 사용. 주로 프록시 서버나 로드 밸런서를 통해 요청이 전달될 때 사용
- 기능 : 
1. IP 주소 전달 : 클라이언트의 IP 주소를 서버에 전달하여, 서버가 클라이언트의 실제 위치를 알 수 있도록 한다.
2. 트래픽 분석 : 웹 서버는 XFF 헤더를 통해 클라이언트의 IP를 확인하여 트래픽을 분석, 보안 로그를 기록할 수 있다.
- 구조 : XFF 헤더는 여러 개의 IP 주소를 포함할 수 있으며, 각 IP는 요청이 전달된 경로를 나타냄. 예를 들어. X-Forward-For: client, proxy1, proxy2와 같은 형식으로 나타냄.
- 명칭 :
1. X-접두사 : X-접두사는 비표준 헤더를 나타내기 위해 사용. 이는 원래 HTTP 사양에 포함되지 않은 헤더로, 특정 기능을 위해 추가된 것임을 나타냄. X-접두사는 여러 비표준 헤더에서 일반적으로 사용되는 관례
2. Forwarded : 이 단어는 요청이 중간 프록시 서버를 통해 전달되었음을 나타냄. 즉, 클라이언트의 요청이 여러 서버를 거쳐서 최종 서버에 도달할 때, 원래의 클라이언트 IP 주소를 전달하기 위해 사용
3. For : 이 단어는 해당 IP 주소가 누구를 위한 것인지를 명확히 하기 위해 사용. 즉, 이 헤더는 클라이언트의 IP 주소를 나타내며, 요청을 보낸 주체럴 식별하는 데 사용.

결과적으로, X-Forwarded-For는 "프록시를 통해 전달된 클라이언트의 IP 주소"라는 의미를 내포함.

## 2. 웹 프록시 툴 종류
- Burp Suite
Ver. Community : 필수 수동 도구 기능
Ver. Professional : 웹 취약점 스캐너, 고급 수동도구
Ver. Enterprise : 예약 및 반복 스캔, 무제한 확장성, CI 통합기능 제공
- ZAP
Proxy, PortScan(Active Scan), Crawling(normal, AJAX), Forced Browsing, Fuzzer, Encode./Decode/Hash
- Fiddler
HTTP Protocol Debugging, 네트워크 편집

## 3. Burp Suite 설정 저장 방법 및 불러오는 방법 그리고 Proxy
### 설정 저장하기
- Setting - Manager Global settings - Project setting - Save project settings
- 저장확장자는 *.json 파일로 저장
#### JSON
JSON(JavaScript Object Notation)은 데어티 교환 현식으로 널리 사용되는 경량의 텍스트 기반 포맷. JSON은 사람에게 읽기 쉽고 기계가 분석하고 생성하기 쉬운 구조를 가지고 있음. 주로 웹 애플리케이션에서 클라이언트와 서버 간의 데이터 전송에 사용
##### JSON의 주요 특징
1. 구조 : JSON은 두 가지 기본 구조로 이루어져 있음.
- 객체(Object) : 중괄호 {}로 감싸진 키-값 쌍의 집합. 예:{"name": "Alice", "age": 30}
- 배열(Array) : 대괄호 []로 감싸진 값의 순서 있는 목록. 예:\["apple", "banana", "cherry"\]
2. 데이터 타입 : JSON은 다음과 같은 데이터 타입을 지원
- 문자열(String):큰따옴표로 감싸진 텍스트 (예: "Hello, World!")
- 숫자(Number): 정수 또는 부동 소수점 숫자 (예: 42, 3.14)
- 불리언(Boolean): true 또는 false
- null: 값이 없음을 나타내는 null
- 객체(Object): 중괄호로 감싸진 키-값 쌍
- 배열(Array): 대괄호로 감싸진 값의 목록
3. 사용 용도 :
- 웹 API에서 데이터 전송
- 데이터 저장 형식 (예:NoSQL 데이터베이스)
- 설정 파일 형식
##### JSON 예시
```Json
{
  "name": "Alice",
  "age": 30,
  "isStudent": false,
  "courses": ["Math", "science", "History"],
  "address": {
    "street": "123 main ST",
    "city": "Anytown",
    "zip": "12345"
  }
}
```
### 설정 불러오기
Burp Suite 시작 - Load from config file 에서 json 셋팅 불러오기
## 4. Burpsuite "Interface"와 "Proxy > Intercept"에서 표시되는 텍스트 크기 조절 방법
### 글씨 폰트 조정
- setting - User interface - Display
- setting - User interface - message editor - HTTP message display
### Proxy 설정
- Proxy - Proxy settings - Response interception rules - Intercept responses based on the following rules 체크
### 브라우저 열기
- Proxy - Open browser
## Proxy 확인
이제 Proxy Intercept(가로채다)에 대한 준비는 됐다. Intercept is on 으로 변경하면
브라우저에 요청(www.google.com)을 하면 패킷을 확인 할 수 있다.
```md
(프록시 설정 전) 크롬 -> 구글
(프록시 설정 후) 크롬 -> Burp suite -> 구글
```
## 4. 요청 수정
"labs"라고 의도적으로 취약한 웹사이트를 사용하여 실제 취약성을 확인해 보는 파트
### 4.1 Burp 브라우저에서 취약한 웹사이트에 접근
- Burp suite 에서 Proxy -> Intercept off
- Burp 브라우저를 실행하고 URL 방문
```md
https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-excessive-trust-in-client-side-controls
```
- 로그인 후 'Access Lab' 클릭
### 4.2 쇼핑 계정에 로그인
- 쇼핑 웹사이트에서 로그인
```md
Username : wiener
Password : peter
```
- 100 달러가 있는것을 확인
### 4.3 구매할 물건 찾기
"Lightweight "l33t" Leather Jacket" 세부 정보 확인
### 4,4 장바구니에 담기
Burp 에서....
아아 귀찮아
일단 메뉴얼 링크 그냥 걸어둠
```mb
https://portswigger.net/burp/documentation/desktop/getting-started/modifying-http-requests
```
