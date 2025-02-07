
![6fabcb82-3a28-4de6-9870-3c466a61b775](https://github.com/user-attachments/assets/3aec18f1-cd7a-4445-bc9c-3cbf518cee63)



## URI (Uniform Resource Identifier) 
- URI (Uniform Resource Identifier) 는 인터넷에서 자원을 식별하기 위한 문자열입니다.
- URI는 URL과 URN을 포함하는 상위 개념입니다. 즉, 특정 자원을 식별하기 위한 포괄적인 방법을 제공하며, 자원의 위치나 이름을 나타낼 수 있습니다.


---


## URL (Uniform Resource Locator)
- URL (Uniform Resource Locator) 는 URI의 한 형태로, 인터넷상에서 자원의 위치를 나타내는 방식입니다.
- 자원이 어디에 있는지를 설명하는데 사용되며, 자원에 접근하기 위한 프로토콜을 포함합니다.
- 예를 들어, 웹페이지의 URL은 해당 페이지가 위치한 서버의 주소와 접근 방법(예: HTTP)을 포함합니다. ex) https://www.example.com/path/to/resource


---


## URN (Uniform Resource Name)
- URN (Uniform Resource Name) 은 URI의 또 다른 형태로, 자원의 위치와 상관없이 자원의 이름을 식별하는 방식입니다.
- 자원의 위치가 변하더라도 동일한 식별자를 유지할 수 있게 합니다. 특정 스키마를 따르며, 자원에 대한 영구적인 식별자를 제공합니다.
- ex) urn:isbn:0451450523 (특정 책의 ISBN 번호)


---
---

> ## 추가 학습자료

### **📌 URI, URL, URN의 차이점**  
URI, URL, URN은 인터넷에서 **리소스를 식별하는 방식**을 설명하는 개념입니다.  

---

### **✅ 1. URI (Uniform Resource Identifier) - "자원의 식별자"**  
- **URI는 인터넷의 모든 자원을 식별하는 통합 개념**입니다.  
- URI에는 **URL과 URN이 포함**됩니다.  
- 즉, **"URL도 URI의 한 종류"**이고, **"URN도 URI의 한 종류"**입니다.  

✅ **예제**  
- `https://example.com/index.html` (URL) → 웹 페이지의 위치  
- `urn:isbn:0451450523` (URN) → 책의 ISBN(고유 식별자)  

✔ **즉, URI는 "리소스를 유일하게 식별할 수 있는 모든 식별자"를 의미합니다.**  

---

### **✅ 2. URL (Uniform Resource Locator) - "자원의 위치"**  
- **URL은 "어디(Where)에서 리소스를 가져올 것인지"를 나타냅니다.**  
- 즉, 특정 리소스가 **어디에 위치해 있는지(주소)**를 포함하는 식별자입니다.  
- URL은 **스킴(Scheme)**(http, https, ftp 등), **도메인명(IP), 경로(path)** 등을 포함합니다.  

✅ **URL 예제**  
```plaintext
https://www.example.com/index.html
ftp://files.example.com/download.zip
```
✔ **URL은 "웹 주소" 또는 "파일 위치"를 나타냅니다.**  

---

### **✅ 3. URN (Uniform Resource Name) - "자원의 이름"**  
- **URN은 "무조건 유일한 이름"으로 리소스를 식별합니다.**  
- 하지만 **URN 자체로는 해당 리소스가 어디에 있는지는 알 수 없습니다.**  
- 예를 들어, **ISBN(도서번호), DOI(논문번호), UUID(고유 식별자)** 등이 URN에 해당합니다.  

✅ **URN 예제**  
```plaintext
urn:isbn:0451450523  (책의 ISBN 번호)
urn:uuid:6fa459ea-ee8a-3ca4-894e-db77e160355e (UUID)
```
✔ **URN은 "리소스의 고유한 이름"을 정의하지만, 위치 정보는 포함하지 않습니다.**  

---

### **✅ 4. URI, URL, URN 관계 정리**
📌 **URI는 URL과 URN을 포함하는 개념**입니다.  
```
URI
 ├── URL (어디에서 찾을 수 있는지)
 ├── URN (이름만으로 리소스를 식별)
```

✅ **URI, URL, URN 예제 비교**  
| 개념 | 예제 | 설명 |
|------|-------------------------------|-------------------------------|
| **URI** | `https://example.com/book.pdf` | 리소스를 식별하는 식별자 (URL 포함) |
| **URL** | `https://example.com/book.pdf` | 특정 리소스의 "위치"를 포함한 주소 |
| **URN** | `urn:isbn:0451450523` | 특정 책의 "고유한 이름", 위치 정보 없음 |

---

### **✅ 5. 결론**
| 구분 | URI | URL | URN |
|------|------------------|------------------|------------------|
| **의미** | 리소스를 식별하는 통합 개념 | 리소스의 "위치" (어디에서 찾을 수 있는지) | 리소스의 "이름" (어디 있는지는 모름) |
| **포함 관계** | URI는 URL과 URN을 포함 | URL ⊂ URI | URN ⊂ URI |
| **예제** | `urn:isbn:0451450523` 또는 `https://example.com` | `https://example.com/book.pdf` | `urn:isbn:0451450523` |

💡 **즉, URL은 "위치를 포함하는 URI"이고, URN은 "위치를 포함하지 않는 URI"입니다.** 🚀
