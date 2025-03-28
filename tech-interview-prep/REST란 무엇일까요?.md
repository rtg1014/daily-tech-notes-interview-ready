## REST(Representational State Transfer) 는 자원의 표현을 이용하여 상태를 주고받는 것을 의미합니다.
- 여기서 자원이란 소프트웨어가 관리하는 모든 것을 의미하며 자원의 표현은 자원을 나타내기 위한 이름을 의미합니다.
- 가령, 서버가 관리하는 주문 데이터는 order 라고 표현할 수 있습니다.
- 최근에는 일반적으로 자원의 상태를 나타내기 위해 JSON 포맷을 사용합니다.
- REST는 네트워크 상에서 클라이언트와 서버의 통신 방식 중 하나이며, HTTP 프로토콜을 사용합니다.
- 구체적으로는 HTTP URI를 활용하여 자원을 명시하고 HTTP METHOD를 통해 CRUD 연산을 적용하는 것을 의미합니다.

  <br>

---

  <br>

  

## 여기서 API(Application Programming Inteface) 란?
- 컴퓨터 프로그램 간 정보를 주고받을 수 있도록 하는 일종의 출입구와 같은 역할을 수행합니다. API가 REST 기반으로 구현되어 있다면, 이를 `REST API` 라고 부릅니다.



  <br>

---

  <br>

  

  

## REST의 장단점은? 
- REST는 서버와 클라이언트의 역할을 명확하게 분리해 주며, HTTP 프로토콜을 따르는 모든 플랫폼에서 사용할 수 있습니다.
- 또한, CURL, Postman을 사용하여 간단하게 테스트할 수 있다는 장점도 존재합니다.
- 반면, 요청 및 응답 스타일의 통신만 지원하며 HTTP 메서드로 행위를 표현하기 어려운 경우도 존재하며 요청 한 번으로 여러 자원을 가져오기 어렵다는 단점이 존재합니다.
- 그리고 REST 방식의 경우 자원의 상태를 전송하기 위해서 JSON 메시지 포맷을 사용합니다.
- JSON과 같은 텍스트 포맷은 자기 서술적이며, 메시지 소비자가 자신이 관심이 있는 값만 골라서 사용하고 나머지는 무시하면 되므로 메시지 구조가 자주 바뀌어도 하위 호환성을 보장하는 것이 유리합니다.
- 하지만, 메시지가 다소 길다는 것이 단점입니다. 메시지가 길다면 네트워크 트래픽을 더욱 사용하며 전송 속도가 느릴 수 있으며, 메시지를 해석하는 데에 오버헤드가 발생할 수 있습니다.





## 추가 학습자료 (GPT)

### 🚀 **REST란? 그리고 REST API란?**

---

## 💡 **REST (REpresentational State Transfer)란?**
REST는 **웹 아키텍처 스타일(설계 원칙)** 중 하나로, **HTTP 프로토콜**을 기반으로 **리소스(Resource)**를 주고받는 **규칙과 구조**를 정의합니다.  
쉽게 말하면, **"서버와 클라이언트가 데이터를 주고받는 방식에 대한 설계 원칙"**입니다.

---

## 🧱 **REST의 6가지 주요 설계 원칙 (제약 조건)**

RESTful API가 되기 위해선 다음 **6가지 제약 조건**을 따라야 합니다.

1️⃣ **클라이언트-서버 구조**  
   - 클라이언트와 서버는 **분리**되어야 함.
   - 클라이언트는 요청만 보내고, 서버는 응답만 함.

2️⃣ **무상태성(Stateless)**  
   - 서버는 **이전 요청의 상태를 기억하지 않음**.
   - 모든 요청은 **완전한 정보**를 포함해야 함.

3️⃣ **캐시 가능(Cacheable)**  
   - 서버 응답을 **클라이언트가 캐시**할 수 있도록 해야 함.

4️⃣ **계층형 구조(Layered System)**  
   - 클라이언트는 서버 외에 **중간 레이어(게이트웨이, 프록시)**가 있을 수 있음을 알 필요 없음.

5️⃣ **인터페이스 일관성(Uniform Interface)**  
   - 리소스에 접근하는 **방식(URL, 메서드)**이 일관되어야 함.

6️⃣ **코드 온 디맨드(Code on Demand)** (선택)  
   - 서버가 클라이언트에게 **코드를 전송**해서 실행할 수 있게 할 수 있음 (JavaScript).

---

## 🔧 **REST API란?**
REST API는 **REST 아키텍처 스타일을 따르는 API**를 말합니다.  
즉, 클라이언트가 **HTTP 요청**을 보내면, 서버가 **리소스 정보**를 **JSON, XML** 등의 형태로 응답하는 방식입니다.

**REST API**는 다음과 같은 요청 메서드를 사용합니다.

| **HTTP 메서드** | **설명**         | **예시 (URL)**            |
|----------------|------------------|-------------------------|
| `GET`          | 리소스 조회      | `GET /users`            |
| `POST`         | 리소스 생성      | `POST /users`           |
| `PUT`          | 리소스 전체 수정 | `PUT /users/1`          |
| `PATCH`        | 리소스 부분 수정 | `PATCH /users/1`        |
| `DELETE`       | 리소스 삭제      | `DELETE /users/1`       |

---

## 🌐 **REST API 설계 예시**

### 📋 **요구사항**  
- 사용자를 생성하고, 조회하고, 수정하고, 삭제하는 API 설계

### 🖋 **URL 설계**
| **기능**             | **HTTP 메서드** | **URL**        |
|----------------------|-----------------|----------------|
| 사용자 목록 조회      | `GET`           | `/users`       |
| 특정 사용자 조회      | `GET`           | `/users/{id}`  |
| 사용자 생성          | `POST`          | `/users`       |
| 사용자 수정 (전체)    | `PUT`           | `/users/{id}`  |
| 사용자 수정 (부분)    | `PATCH`         | `/users/{id}`  |
| 사용자 삭제          | `DELETE`        | `/users/{id}`  |

---

## 🔨 **예제 코드 (Java Spring Boot)**

### ✅ **사용자 목록 조회 API (`GET /users`)**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    private final List<String> users = new ArrayList<>(List.of("Alice", "Bob", "Charlie"));

    // 사용자 목록 조회
    @GetMapping
    public List<String> getUsers() {
        return users;
    }
}
```

### ✅ **특정 사용자 조회 API (`GET /users/{id}`)**

```java
@GetMapping("/{id}")
public String getUser(@PathVariable int id) {
    if (id >= users.size()) {
        throw new ResponseStatusException(HttpStatus.NOT_FOUND, "User not found");
    }
    return users.get(id);
}
```

---

## 🧩 **RESTful API의 장점**
1. **클라이언트-서버 분리**로 개발이 용이함.
2. **표준 HTTP 메서드**를 사용해 직관적이고 이해하기 쉬움.
3. **JSON, XML** 등을 사용해 다양한 클라이언트에서 쉽게 사용 가능.
4. **캐시**를 통해 성능을 최적화할 수 있음.

---

## ❓ **REST API와 일반 API의 차이**

| **항목**      | **REST API**                                   | **일반 API**                          |
|---------------|-----------------------------------------------|---------------------------------------|
| **설계 원칙** | REST 아키텍처 원칙을 따름                     | 제한 없음                             |
| **HTTP 메서드** | `GET`, `POST`, `PUT`, `DELETE`, `PATCH` 사용  | `POST`에 모든 기능을 몰아넣기도 함    |
| **리소스 URL** | **명확하게 리소스를 나타내는 URL** 사용       | URL이 명확하지 않을 수 있음           |

---

## 🔥 **기술 면접에서 자주 묻는 질문**
1. **REST와 RESTful의 차이점은 무엇인가요?**
   - **REST**는 아키텍처 스타일이고, **RESTful**은 그 원칙을 잘 지킨 API를 의미합니다.

2. **GET과 POST의 차이점은 무엇인가요?**
   - `GET`은 **리소스 조회**에 사용되고, **URL에 데이터를 포함**하며, **캐시 가능**합니다.  
   - `POST`는 **리소스 생성**에 사용되며, **요청 본문에 데이터를 포함**하고, **캐시 불가**입니다.

---

