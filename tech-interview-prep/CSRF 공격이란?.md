## 사이트 간 요청 위조(Cross-site Request Forgery, CSRF)
- 사이트 간 요청 위조(Cross-site Request Forgery, CSRF) 공격은 사용자가 자신의 의지와 상관없이 공격자가 의도한 행위를 특정 웹사이트에 요청하도록 하는 것을 의미합니다.

- 예를 들어, 특정 사용자가 매일메일 서비스에서 로그인을 수행하고 서버는 해당 사용자에 대한 세션 ID를 Set-Cookie 헤더에 담아서 응답합니다. 그리고, 클라이언트는 쿠키를 저장하고 요청마다 자동으로 전달합니다.

- 이러한 사용자를 대상으로 공격자는 악성 스크립트가 담긴 페이지에 접속하도록 유도합니다.
- 유도하는 방법은 다양한데요. 악성 스크립트가 포함된 메일이나 게시글을 작성하거나, 악성 스크립트가 포함된 공격자 사이트 접속 링크를 전달하는 것이 대표적입니다.

- 사용자가 악성 스크립트가 포함된 페이지에 접속하게 되면 악성 스크립트가 실행됩니다. 이 스크립트는 사용자의 의도와 상관없는 특정한 요청(결제, 비밀번호 변경)을 공격 대상 서버로 보내도록 구현되어 있습니다. 해당 요청은 브라우저에 의해서 자동으로 쿠키에 저장된 세션 ID가 함께 전달됩니다.



- 예를 들어, 공격자가 만든 사이트 내부에는 다음과 같은 태그가 존재할 수 있습니다.
  
```
<img src ="https://maeil-mail.com/member/changePassword?newValue=1234" />
```

-공격자 사이트에 방문한 사용자는 자신의 의지와 무관하게 img 태그로 인해 세션 ID가 포함된 쿠키와 함께 비밀번호 변경 요청을 매일메일 서버로 전달합니다

---

## CSRF 공격은 어떻게 방어할 수 있나요? 
- 교차 출처인 상황에서의 요청을 막는 방식으로 CSRF를 방어할 수 있습니다.

### 첫 번째로, HTTP 헤더 중에 하나인 Referer 요청 헤더를 사용하는 방법이 있습니다.
- Referer 요청 헤더로 현재 요청을 보낸 페이지의 주소를 알 수 있는데요. 해당 주소와 Host(서버의 도메인 이름) 헤더를 비교하여 다른 경우, 예외를 발생시킬 수 있습니다.
- 하지만, Referer 요청 헤더는 조작될 수 있다는 점에서 한계가 있습니다.

### 두 번째로, 템플릿 엔진 기술을(JSP, 타임리프, Pug, Ejs 등) 사용하고 있는 경우라면 CSRF 토큰 방법을 사용해 볼 수 있습니다. 
- 페이지를 생성하기 이전에 사용자 세션에 임의의 CSRF 토큰을 저장합니다.
- 그리고, 특정 API 요청에 대한 제출 폼을 생성할 때 해당 CSRF 토큰값이 설정된 input 태그를 추가합니다.

```
<input type = "hidden" name = "csrf_token" value = "csrf_token_12341234" />
```


- 실제로 요청이 전달될 때, 해당 input 태그의 CSRF 토큰과 사용자 세션 내부에 존재하는 CSRF 토큰의 일치 여부를 판단하여, CSRF 공격에 대해 방어할 수 있습니다.

- 이외에도 SameSite 쿠키를 사용하여 크로스 사이트에 대한 쿠키 전송을 제어하거나, 브라우저의 SOP(Same Origin Policy) 정책을 사용하고, CORS 설정으로 교차 출처 접근을 일부분 허용하는 방식으로도 CSRF 공격을 방어할 수 있습니다.

---

<br>

> ## 추가 학습자료

### **📌 CSRF (Cross-Site Request Forgery) 공격이란?**
CSRF(사이트 간 요청 위조) 공격은 **악의적인 웹사이트에서 사용자의 의도와 관계없이 사용자의 인증된 세션을 이용해 공격자가 원하는 요청을 서버에 전송하는 공격 기법**입니다.

💡 **쉽게 말하면?**  
사용자가 로그인된 상태에서 **공격자가 유도한 악성 페이지**를 방문하면, 사용자의 **인증 정보를 도용하여 서버에 요청을 보내는 공격**입니다.

---

## **🔍 CSRF 공격 원리**
CSRF 공격이 성공하려면 **두 가지 조건**이 충족되어야 합니다.

1️⃣ **사용자가 로그인된 상태에서 요청을 보낼 수 있어야 함**  
   - 예를 들어, 사용자가 은행 사이트에 로그인한 상태에서 악성 웹사이트를 방문하면 공격이 가능함.

2️⃣ **서버가 요청을 사용자의 요청으로 신뢰해야 함 (자동으로 인증이 포함됨)**  
   - 많은 웹사이트에서 쿠키를 통해 인증 세션을 유지하므로, 요청을 보낼 때 **자동으로 인증 정보가 포함됨**.

---

### **📌 CSRF 공격 예시**
#### **💡 공격 시나리오 (사용자가 로그인된 상태)**
1️⃣ **사용자가 A 사이트(https://bank.com)에 로그인하여 세션이 유지됨.**  
2️⃣ **공격자는 악성 웹사이트(https://evil.com)에 사용자를 방문하도록 유도함.**  
3️⃣ **악성 웹사이트에서 보낸 HTML 또는 JavaScript 코드가 A 사이트에 요청을 보냄.**
4️⃣ **사용자의 세션이 유지되고 있어 서버는 요청을 정상적인 사용자 요청으로 처리함.**  
5️⃣ **결과적으로 공격자는 사용자의 계좌에서 송금하는 등의 악의적인 행동을 수행할 수 있음.**

#### **🚨 실제 코드 예시 (CSRF 공격 코드)**
```html
<img src="https://bank.com/transfer?account=attacker&amount=1000" />
```
- 사용자가 악성 사이트에 접속하면 자동으로 **A 사이트(https://bank.com)** 에 요청을 보냄.
- **사용자의 인증된 세션 쿠키가 자동으로 포함됨 → 요청이 정상 요청으로 처리됨.**

---

## **🛡 CSRF 방지 방법**
CSRF 공격을 방지하는 주요 방법을 정리하면 다음과 같습니다.

### **✅ 1. CSRF Token 사용 (가장 강력한 방법)**
- **CSRF 토큰**이란, 사용자의 요청이 **정상적인 요청인지 확인하기 위해** 랜덤한 값을 포함한 토큰을 함께 보내는 방식입니다.
- 클라이언트에서 요청을 보낼 때 **CSRF 토큰을 포함해야 서버가 요청을 처리함**.

**📌 CSRF 토큰 방식의 흐름**
1️⃣ **사용자가 로그인하면 서버에서 CSRF 토큰을 생성하고 클라이언트(브라우저)에 전달**  
2️⃣ **사용자는 요청을 보낼 때 해당 토큰을 요청 본문, 헤더, 혹은 쿠키에 포함하여 전송**  
3️⃣ **서버는 요청을 받을 때 CSRF 토큰을 검증하고 유효하면 요청을 처리함.**  

✔ **CSRF 토큰 예시 (Spring Security)**
```java
// CSRF Token 활성화 (Spring Security)
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    @Bean
    SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .csrf(csrf -> csrf.csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse()));
        return http.build();
    }
}
```

✔ **HTML 폼에 CSRF 토큰 포함**
```html
<form action="/transfer" method="POST">
    <input type="hidden" name="_csrf" value="TOKEN_VALUE">
    <button type="submit">송금</button>
</form>
```

✔ **AJAX 요청에 CSRF 토큰 추가**
```javascript
fetch("/transfer", {
    method: "POST",
    headers: {
        "X-CSRF-Token": "TOKEN_VALUE"
    }
});
```

✅ **CSRF 토큰 방식의 장점**  
✔ 공격자는 **사용자의 CSRF 토큰을 알 수 없으므로 요청을 위조할 수 없음**  
✔ **POST 요청뿐만 아니라 GET 요청도 보호 가능**

---

### **✅ 2. SameSite 쿠키 속성 설정**
CSRF 공격은 기본적으로 **쿠키가 자동으로 포함**되는 특징을 이용하는데,  
이를 방지하기 위해 **SameSite 속성을 설정**하면 **다른 사이트에서의 요청 시 쿠키가 포함되지 않도록 설정**할 수 있습니다.

✔ **SameSite 설정 예시**
```java
response.setHeader("Set-Cookie", "SESSIONID=abc123; HttpOnly; Secure; SameSite=Strict");
```

✔ **SameSite 정책 종류**
| SameSite 속성 | 설명 |
|--------------|--------------------------------------------|
| **Strict**   | 다른 사이트에서의 모든 요청에 대해 쿠키를 포함하지 않음 (강력한 보안) |
| **Lax**      | 안전한 GET 요청(링크 클릭)에는 허용하지만, POST 요청에는 포함되지 않음 |
| **None**     | 모든 요청에서 쿠키를 포함 (Secure 속성과 함께 사용해야 함) |

✅ **SameSite 쿠키 설정의 장점**  
✔ **CSRF 공격을 원천적으로 차단 가능**  
✔ 브라우저에서 지원하므로 **추가적인 개발 없이 쉽게 적용 가능**

---

### **✅ 3. Referer & Origin 검증**
**CSRF 공격은 다른 사이트에서 발생**하기 때문에, 요청이 실제로 **신뢰할 수 있는 출처(Origin)에서 온 것인지 확인**하는 방법입니다.

✔ **백엔드에서 Origin 확인 (Spring)**
```java
@RequestMapping(value = "/transfer", method = RequestMethod.POST)
public ResponseEntity<String> transfer(HttpServletRequest request) {
    String origin = request.getHeader("Origin");
    if (!"https://trusteddomain.com".equals(origin)) {
        return ResponseEntity.status(HttpStatus.FORBIDDEN).body("CSRF 공격 감지!");
    }
    return ResponseEntity.ok("송금 성공");
}
```

✅ **Referer & Origin 검증의 장점**  
✔ **다른 도메인에서 온 요청을 차단할 수 있음**  
✔ CSRF 공격을 상당 부분 방어할 수 있음

🚨 **단점**  
❌ 일부 브라우저에서는 Referer 헤더를 제거할 수도 있음  
❌ VPN, 프록시 사용 시 Referer가 변조될 가능성이 있음

---

### **✅ 4. GET 요청으로 중요한 데이터 변경하지 않기**
- CSRF 공격은 **사용자가 GET 요청을 무의식적으로 보낼 때 발생할 가능성이 높음**.
- 중요한 동작(예: 결제, 계좌이체 등)은 **GET 대신 POST, PUT, DELETE 요청을 사용**해야 함.

✔ **잘못된 예시 (GET 요청으로 중요한 데이터 변경)**
```html
<img src="https://bank.com/transfer?account=attacker&amount=1000" />
```

✔ **올바른 예시 (POST 요청 사용)**
```html
<form action="https://bank.com/transfer" method="POST">
    <input type="hidden" name="account" value="attacker">
    <input type="hidden" name="amount" value="1000">
    <button type="submit">송금</button>
</form>
```

✅ **POST 요청을 사용하면 CSRF 방어가 더욱 쉬워짐**  
✔ CSRF 토큰을 적용할 수 있음  
✔ 브라우저에서 자동 요청을 차단할 가능성이 높아짐

---

## **📌 CSRF 방어 정책 정리**
| 방법 | 설명 | 적용 난이도 | 효과 |
|------|------|----------|------|
| **CSRF Token 사용** | 랜덤한 토큰을 포함하여 요청을 검증 | 중간 | 강력한 보안 |
| **SameSite 쿠키 설정** | CSRF 공격 시 쿠키 포함 차단 | 쉬움 | 기본적인 보안 |
| **Referer & Origin 검증** | 요청 출처 확인 | 쉬움 | CSRF 공격 방어 가능 |
| **GET 요청 제한** | GET 요청으로 중요한 동작을 하지 않음 | 쉬움 | CSRF 위험 감소 |

---

## **🚀 결론 (백엔드 개발자가 알아야 할 내용)**
1️⃣ **CSRF는 인증된 사용자의 세션을 악용하는 공격으로, 서버가 요청을 신뢰하는 점을 악용한다.**  
2️⃣ **백엔드 개발자는 CSRF 방어를 위해 CSRF 토큰, SameSite 쿠키, Referer 검증을 적극 활용해야 한다.**  
3️⃣ **GET 요청으로 중요한 데이터를 변경하는 기능을 제공하지 말아야 한다.**  
4️⃣ **보안은 단일 방법이 아닌, 여러 가지 방어 정책을 조합하여 적용해야 한다.**  

💡 **"완벽한 보안은 없다. 하지만 CSRF는 적절한 보안 정책을 적용하면 충분히 방어할 수 있다!"** 🚀
