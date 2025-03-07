
## CI 개요
- 개발자가 작성한 작은 코드 변경을 코드 베이스에 통합합니다. 변경한 부분이 통합되면, 자동으로 새로운 시스템을 빌드하고 현재 시스템에 존재하는 모든 테스트를 실행합니다.
- 만약 이전에 동작했던 어떤 부분이 망가졌다면, 개발자는 해당 부분을 다시 수정합니다.
- 이러한 일련의 과정을 포함하는 소프트웨어 개발 방식을 지속적 통합(Continuous Integration) 이라고 합니다.
- 지속적 통합의 핵심 목표는 소프트웨어의 품질을 개선하고, 새로운 소프트웨어의 변경 사항을 검증하는데 소요되는 시간을 단축 시키며, 버그를 조기에 발견하기 위함입니다.

---



## CD 개요
- 지속적 배포(Continuous Deployment) 는 지속적 통합을 통해서 빌드된 코드(빌드 아티팩트)를 프로덕션 환경에 자동으로 배포하는 것을 의미합니다.
- 지속적 전달(Continuous Delivery) 은 빌드 아티팩트를 프로덕션 환경에 바로 배포하기 위해서 수동으로 작업해야 한다는 점에서 지속적 배포와 차이가 있습니다.
- CD 과정에는 빌드 아티팩트를 관리 및 저장하는 공간이 필요할 수도 있습니다. 예를 들어, AWS S3, Docker Registry, Nexus를 사용할 수 있습니다.



- 일반적으로 위 방식들을 합쳐 CI/CD 파이프라인이라고 부르며, CI/CD 파이프라인을 구축하기 위한 도구로 Jenkins, Travis CI, Github Action 등이 존재합니다.


<br>

---
---

<br>

> ## 추가학습자료

[10분 테코톡] 도비의 CI/CD와 Github Action
출처 : https://www.youtube.com/watch?v=SKILL1pT6f4



### 🚀 **CI/CD와 GitHub Actions 완벽 가이드**  

---

## **📌 1. GitHub Actions란?**  

GitHub Actions는 **GitHub에서 제공하는 CI/CD 자동화 도구**입니다.  
✔ **CI/CD 플랫폼 역할을 한다** (Continuous Integration & Continuous Deployment)  
✔ **자동화(Automation) 중심** → 개발자가 반복적인 작업에서 벗어나 코드에 집중 가능  

GitHub Actions는 **레포지토리 단위**로 실행됩니다.  
✔ 특정 이벤트(예: Push, PR 등)가 발생하면 **트리거(trigger) 작동**  
✔ 트리거된 이벤트는 **Workflow를 실행**  
✔ Workflow는 **Runner → Job → Step** 순서로 동작  

---

## **📌 2. GitHub Actions의 기본 구조**  

GitHub Actions의 실행 과정은 다음과 같습니다.  

🔹 **이벤트(Event)** → Workflow 실행 트리거 (예: Push, PR, Issue 생성 등)  
🔹 **Workflow** → 실행 단위 (YAML 파일로 정의)  
🔹 **Job** → 독립적인 실행 단위 (여러 개의 Job이 병렬 또는 직렬 실행 가능)  
🔹 **Runner** → Job이 실행되는 환경 (GitHub 제공 또는 Self-Hosted)  
🔹 **Step** → Job 내에서 순차적으로 실행되는 작업 (스크립트 실행, 명령어 수행 등)  

> **📌 예제: 간단한 GitHub Actions Workflow**
```yaml
name: Example Workflow
on: push  # 'push' 이벤트가 발생하면 실행됨

jobs:
  example-job:
    runs-on: ubuntu-latest  # Runner 환경 설정
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3  # 코드 다운로드
      - name: Run a command
        run: echo "Hello, GitHub Actions!"  # 간단한 명령어 실행
```

✔ **on:** 실행 트리거 (Push 발생 시 실행)  
✔ **runs-on:** 실행 환경 (Ubuntu 최신 버전 사용)  
✔ **steps:** 실행할 작업 정의 (코드 다운로드 후 echo 명령 실행)  

---

## **📌 3. GitHub Actions의 실행 과정**  

1️⃣ **GitHub 이벤트 발생 (예: PR 생성, 코드 Push 등)**  
2️⃣ **해당 이벤트를 트리거로 Workflow 실행**  
3️⃣ **Runner에서 Job 실행**  
4️⃣ **각 Job 내부에서 Step 실행**  
5️⃣ **CI/CD 결과 확인 (GitHub Actions 콘솔에서 로그 확인 가능)**  

> **📌 실제 실행 화면 예시**  
- GitHub에서 PR이 생성되면 자동으로 Workflow 실행  
- 실행이 완료되면 **GitHub Actions Logs**에서 실행 내역 확인 가능  

---

## **📌 4. GitHub Actions의 핵심 개념: Context & Secrets**  

GitHub Actions는 내부적으로 **Context**와 **Secrets**를 관리합니다.  
✔ **Context** → 자동으로 생성되는 환경 변수 (예: `${{ github.event }}`)  
✔ **Secrets** → 보안이 필요한 환경 변수 저장소 (예: API Key, DB 비밀번호 등)  

> **📌 예제: Context & Secrets 활용**
```yaml
steps:
  - name: Print GitHub Context
    run: echo "Repository: ${{ github.repository }} | Actor: ${{ github.actor }}"

  - name: Use Secrets
    run: echo "Using Secret Key"
    env:
      SECRET_KEY: ${{ secrets.API_KEY }}
```
✔ `${{ github.repository }}` → 실행 중인 레포지토리 정보 출력  
✔ `${{ github.actor }}` → 실행한 사용자 출력  
✔ `${{ secrets.API_KEY }}` → GitHub Secrets에서 API Key 가져오기  

---

## **📌 5. GitHub Actions를 활용한 CI/CD 구축**  

### **1️⃣ CI (Continuous Integration) - 코드 테스트 자동화**  
✔ 코드가 변경될 때마다 자동으로 빌드 & 테스트 실행  
✔ 테스트 커버리지 확인 및 PR에 리포트 추가  

> **📌 예제: CI Workflow**
```yaml
name: CI Pipeline
on: pull_request  # PR 발생 시 실행

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3
      - name: Setup JDK
        uses: actions/setup-java@v3
        with:
          java-version: '17'
      - name: Run Tests
        run: ./gradlew test
```
✔ PR 발생 시 테스트 자동 실행  
✔ JDK 17 환경 설정 후 테스트 수행  

---

### **2️⃣ CD (Continuous Deployment) - 자동 배포**  
✔ 빌드된 애플리케이션을 Docker Hub에 Push  
✔ 서버에서 배포 자동화  

> **📌 예제: CD Workflow**
```yaml
name: CD Pipeline
on:
  push:
    branches:
      - main  # Main 브랜치에 Push될 때 실행

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3
      - name: Build Application
        run: ./gradlew build
      - name: Build Docker Image
        run: docker build -t my-app .
      - name: Push to Docker Hub
        run: docker push my-app
        env:
          DOCKER_USERNAME: ${{ secrets.DOCKER_USERNAME }}
          DOCKER_PASSWORD: ${{ secrets.DOCKER_PASSWORD }}

  deploy:
    needs: build  # Build가 완료된 후 실행
    runs-on: self-hosted  # 자체 호스팅된 서버에서 실행
    steps:
      - name: Deploy Application
        run: docker-compose up -d
```
✔ **Main 브랜치에 Push 시 자동 실행**  
✔ **Docker Image 빌드 & Docker Hub에 Push**  
✔ **배포 서버에서 Docker Compose 실행하여 컨테이너 실행**  

---

## **📌 6. GitHub Actions 활용 사례**  

### **1️⃣ PR 리뷰 알림 (Slack 연동)**  
✔ 특정 이벤트 발생 시 Slack으로 알림 전송  
✔ GitHub Actions의 `uses` 키워드를 활용하여 Slack App 호출  

> **📌 예제: Slack 알림 Workflow**
```yaml
name: Slack Notification
on: pull_request

jobs:
  notify:
    runs-on: ubuntu-latest
    steps:
      - name: Send Slack Message
        uses: rtCamp/action-slack-notify@v2
        with:
          webhook-url: ${{ secrets.SLACK_WEBHOOK }}
          message: "새로운 PR이 생성되었습니다! 🚀"
```
✔ PR 생성 시 Slack 채널에 알림 전송  

---

## **📌 7. CI/CD & GitHub Actions 요약**  

✔ **GitHub Actions는 CI/CD를 자동화하는 강력한 도구**  
✔ **이벤트(Trigger) 기반으로 Workflow 실행 → Job → Step 순으로 동작**  
✔ **CI (테스트 자동화) & CD (배포 자동화) 구축 가능**  
✔ **Secrets & Context 활용 가능 (보안 변수, 환경 변수 저장)**  
✔ **Slack, Docker Hub 등 다양한 서비스와 연동 가능**  

🎤 *"CI/CD 자동화를 통해 개발 생산성을 높이고, GitHub Actions를 적극 활용해 보세요! 긴 시간 발표 들어주셔서 감사합니다!"* 👏👏👏
