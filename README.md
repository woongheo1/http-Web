# HTTP 

**인터넷에서 서버와 클라이언트 간의 데이터를 주고 받기 위한 프로토콜(상호 간에 정의한 규약)** 입니다.

<br></br>

## 1. HTTP 프로토콜 특징

**비연결 지향(Connectionless)적이고 무상태(stateless)적인 프로토콜**입니다. 비연결적이고 상태가 없다라는 말은 각각의 데이터 요청이 서로 독립적으로 이루어진다는 말입니다. 즉, 모든 트랜젝션이 단 한 번의 응답과 요청 사이클을 가지며, 이 사이클이 끝나면 연결이 끊깁니다.

이러한 특징으로 다수의 요청 처리 및 서버 부하를 줄일 수 있는 성능 상의 이점이 생기기도 하지만, 반대로 클라이언트의 이전 상황을 알 수 없는 무상태라는 단점을 해결하기 위해 `Cookie`, `Session`, `Local Storage` 등이 등장하였습니다.

또한 HTTP 프로토콜은 일반적으로 TCP/IP 통신 위에서 동작하며, **80번** 포트를 사용합니다.

<br></br>

## 2. HTTP Request & HTTP Response

HTTP 프로토콜로 데이터를 주고받기 위해서는 아래와 같이 클라이언트에서 요청(Request) 를 보내고 서버에서 응답(Response)를 받아야 합니다.



클라이언트란 요청을 보내는 쪽을 의미하며 일반적으로 웹 관점에서는 브라우저를 의미합니다. 서버란 요청을 받는 쪽을 의미하며 일반적으로 데이터를 보내주는 원격지의 컴퓨터를 의미합니다.

HTML 문서만이 HTTP 통신을 위한 유일한 정보는 아닙니다. Plain Text 부터 JSON 데이터 및 이미지, 영상 등 어떤 데이터 형태도 전송할 수 있게끔 설계되어있습니다

<br></br>

## 3. URL

숫자로 된 IP 주소를 대체하는 **도메인 네임 시스템**입니다. URL(또는 URI) 이라는 단어 자체는 네트워크 상에서 특정 자원에 대한 주소를 나타내기 위한 정식적인 규약 명칭입니다.


### 3-2. URL 구조

#### Protocol

프로토콜은 해당 URL 이 어떤 서비스를 위한 것인지 명시합니다. http 및 https는 웹 서비스를 위한 프로토콜, ftp는 파일 서버가 사용하는 프로토콜을, ssh는 리눅스 기반 통신 프로토콜입니다.

#### 최상위 도메인(TLD, Top Level Domain)

최상위 도메인은 com, net, kr 처럼 도메인 주소의 끝에 붙는 녀석입니다.

#### 서브 도메인(Sub-domain)

도메인 주소의 오른쪽에 있는 TLD 부터 점을 구분하여 나열되는 각 문자들을 **서브 도메인**이라 합니다. naver.com 에서 naver 가 서브 도메인이 되는데, 일반적으로 우리가 도메인을 구입하면 example.com 형식으로 할당받기 때문에 example 이나 naver 처럼 TLD 바로 옆에 있는 도메인은 주로 **메인 도메인**이라고 부릅니다. 메인 도메인 왼쪽부터 서브 도메인이라 칭하는 것이 일반적입니다.

<br></br>

### 4-1. HTTP 요청 메시지 형식


- Start Line : HTTP Request 의 첫 라인으로써, 3 부분으로 구성됩니다.

  - HTTP Method : `GET`, `POST` 등 action 을 정의
  - Request Target : 요청이 전송되는 URI
  - HTTP Version

- Headers : Request 에 대한 Meta 정보를 담고 있으며, key: value 값으로 되어 있습니다.

  - Host : 요청이 전송되는 Target 의 Host URI
  - User-Agent : 요청을 보내는 클라이언트에 대한 정보 (ex. 웹브라우저의 정보)
  - Accept : 해당 요청이 받을 수 있는 응답(Response) 타입.
  - Connection : 해당 요청이 끝난 후에 클라이언트와 서버가 계속해서 네트워크 컨넥션을 유지 할것인지 아니면 끊을것인지에 대해 지시하는 부분. (Keep-alive or cancel)
  - Content-Type : 해당 요청이 보내는 메세지 body의 타입. 예를 들어, JSON을 보내면 application/json.
  - Content-Length : 메세지 Body 의 길이

- Empty Line : 요청에 대한 메타 정보가 전송되었음을 알립니다.

- Body : 해당 Request 의 실제 내용이 들어가있으며, `POST` 또는 `PUT` 메서드의 경우에만 존재합니다.

<br></br>

### 4-2. HTTP 응답 메시지 형식


- Start Line : HTTP Response 의 첫 라인으로써, 3 부분으로 구성됩니다.

  - HTTP Version
  - Status Code : 요청에 대한 응답 상태를 보여주는 코드
  - Status Text : 응답 상태의 설명(ex. Not Found)

- Headers : Response 에 대한 Meta 정보를 담고 있으며, Response Header 에서만 사용되는 값들이 있습니다.

- Empty Line : 요청에 대한 메타 정보가 전송되었음을 알립니다.

- Body : 실제 응답 리소스 데이터입니다. 상태에 따라 body 가 존재하지 않을 수 있습니다.

<br></br>

## 5. HTTP Request Method

URL(Uniform Resource Locators) 주소를 이용하면 서버에 특정 데이터를 요청할 수 있습니다. 아래와 같은 HTTP 요청 메서드(HTTP Request Methods)를 주로 이용합니다.

- **GET** : 존재하는 자원에 대한 **요청**
- **POST**: 새로운 자원을 **생성**
- **PUT**: 존재하는 자원에 대한 **변경**
- **DELETE**: 존재하는 자원을 **삭제**

이와 같이 데이터에 대한 조회, 생성, 변경, 삭제를 HTTP 요청 메서드로 정의할 수 있으며, 때에 따라서는 POST 로 PUT, DELETE 의 동작도 수행할 수 있습니다. 아래 메서드들은 자주 사용되지는 않지만 알아두어야 할 메서드들입니다.

- **HEAD** : HTTP Header 정보만 요청하는 메서드. 해당 자원이 존재하는지 혹은 서버에 문제가 없는지를 확인
- **OPTIONS** : 웹 서버가 지원하는 메서드의 종류를 요청
- **TRACE** : 클라이언트의 요청을 그대로 반환하는 메서드.

<br></br>

## 6. HTTP Status Code

URL 과 요청 메서드가 클라이언트에서 설정해야 할 정보라면 HTTP 상태 코드(HTTP Status Code) 는 서버에서 설정해주는 응답(Response) 정보입니다.

서버로부터 받는 이 상태 코드를 이용하여 프론트엔드에서 에러 처리를 할 수 있습니다.

### 2xx - 성공

200번대의 상태 코드는 대부분 성공을 의미합니다.

- 200 : GET 요청에 대한 성공
- 204 : No Content. 성공했으나 응답 본문에 데이터가 없음
- 205 : Reset Content. 성공했으나 클라이언트의 화면을 새로 고침하도록 권고
- 206 : Partial Content. 성공했으나 일부 범위의 데이터만 반환

### 3xx - 리다이렉션

300번대의 상태 코드는 대부분 클라이언트가 이전 주소로 데이터를 요청하여 서버에서 새 URL 로 리다이렉트를 유도하는 경우입니다.

- 301 : Moved Permanently, 요청한 자원이 새 URL에 존재
- 303 : See Other, 요청한 자원이 임시 주소에 존재
- 304 : Not Modified, 요청한 자원이 변경되지 않았으므로 클라이언트에서 캐싱된 자원을 사용하도록 권고. ETag와 같은 정보를 활용하여 변경 여부를 확인

### 4xx - 클라이언트 에러

400번대 상태 코드는 대부분 클라이언트의 코드가 잘못된 경우입니다. 유효하지 않은 자원을 요청했거나, 요청이나 권한이 잘못된 경우에 발생합니다. 가장 익숙한 코드는 요청한 자원이 서버에 없다는 의미를 가지는 404 상태 코드입니다.

- 400 : Bad Request, 잘못된 요청
- 401 : Unauthorized, 권한 없이 요청. Authorization 헤더가 잘못된 경우
- 403 : Forbidden, 서버에서 해당 자원에 대해 접근 금지
- 405 : Method Not Allowed, 허용되지 않은 요청 메서드
- 409 : Conflict, 최신 자원이 아닌데 업데이트 하는 경우. ex) 파일 업로드 시 버전 충돌

### 5xx - 서버 에러

500번대 상태 코드는 서버 쪽에서 오류가 난 경우입니다.

- 501 : Not Implemented, 요청한 동작에 대해 서버가 수행할 수 없는 경우
- 503 : Service Unavailable, 서버가 과부하 또는 유지 보수로 내려간 경우
