--- 
title: "클라우드 & DevOps 기초 | Cloud & DevOps" 
date: 2025-04-11 09:00:00 +0900
achieved: 2025-04-11 10:00:00 +0900
math: true
categories: [CS, Cloud & DevOps]
tags: [CS, Cloud, DevOps]
---
---------- 	
> 내가 볼려고 작성한 CS 공부. 
{: .prompt-info } 

# ⚙️ 클라우드 & DevOps 기초

## ✅ 1. 클라우드 컴퓨팅 기초

### 1.1 클라우드란?

> 클라우드는 **컴퓨팅 자원을 네트워크를 통해 제공받는 서비스 모델**이다.  
> 직접 서버를 구축하지 않고, 필요할 때 빌려 쓰는 구조

#### 대표적인 자원

| 자원 | 예시 |
|------|------|
| 컴퓨팅 | 가상 서버 (EC2, Compute Engine) |
| 스토리지 | 파일 저장소 (S3, GCS) |
| 데이터베이스 | RDS, BigQuery, Firestore |
| 네트워크 | 로드밸런서, VPC, CDN |

> 💡 클라우드는 **개발 속도 향상, 비용 효율화, 확장성 확보**를 위해 등장함

### 1.2 온프레미스 vs 클라우드

| 항목 | 온프레미스 | 클라우드 |
|------|------------|-----------|
| 인프라 소유 | 기업이 서버 직접 보유 | 외부 업체가 제공 (AWS 등) |
| 설치/운영 | 수동 설치 및 유지보수 | 자동화된 설정 및 관리 |
| 초기 비용 | 매우 큼 (서버 구매 등) | 적음 (필요한 만큼 사용) |
| 확장성 | 제한적, 시간 오래 걸림 | 수 분 내 확장 가능 (Auto Scaling) |
| 유연성 | 낮음 | 매우 높음 (리전, 존, 스케일 조절 가능) |

> 💡 **클라우드는 자원 유연성과 비용 최적화가 핵심 장점**

### 1.3 클라우드 서비스 3계층 (IaaS / PaaS / SaaS)

| 구분 | 개념 | 사용자가 관리 | 제공업체가 관리 | 예시 |
|------|------|----------------|------------------|------|
| IaaS | 인프라 서비스 | OS, 애플리케이션 등 | 하드웨어, 네트워크 | AWS EC2, GCP Compute |
| PaaS | 플랫폼 서비스 | 애플리케이션 코드만 | OS, 미들웨어 포함 전체 | Heroku, Google App Engine |
| SaaS | 소프트웨어 서비스 | 없음 (사용만 함) | 전체 | Gmail, Notion, Figma |

#### 예시 흐름

- **IaaS**: 서버를 내가 구성해서 배포 (Docker, Flask, DB도 내가 설치)
- **PaaS**: 코드만 업로드하면 실행해줌 (환경은 플랫폼이 관리)
- **SaaS**: 이미 만들어진 서비스 사용 (사용자 계정만 있으면 됨)

> 💡 백엔드 엔지니어는 보통 **IaaS + PaaS**를 조합해 사용

### 1.4 클라우드 도입 시 고려 요소

| 항목 | 설명 |
|------|------|
| 비용 모델 | 종량제(시간/초 단위 과금) 또는 예약 인스턴스 |
| 보안 & 인증 | VPC, IAM 정책, 암호화 등 설계 필수 |
| 지역(Region) 선택 | 사용자 가까운 곳에 위치한 리전 선택 필요 |
| 벤더 락인 | 특정 클라우드에 의존적이면 이전이 어려움

### 1.5 클라우드의 실전 활용 예

- **서비스 배포**: EC2 + RDS + S3 조합
- **파일 저장소**: S3 → 대용량 정적 파일 저장
- **AI 학습 서버**: EC2 + GPU 인스턴스, Auto Scaling 설정
- **서버리스 웹훅**: Lambda + API Gateway + SQS


## ✅ 2. AWS/GCP 필수 서비스 이해


### 2.1 EC2 – 가상 서버 (AWS)

> EC2(Elastic Compute Cloud)는 **필요한 만큼의 가상 서버(인스턴스)를 생성하고 관리**할 수 있는 서비스

#### 주요 개념

| 요소 | 설명 |
|------|------|
| 인스턴스 | 실제 실행되는 가상 서버 |
| AMI | 서버의 OS, 설정을 담은 이미지 |
| EBS | EC2에 연결된 저장 장치 (디스크) |
| 키페어 | SSH 접속을 위한 공개/개인 키 |
| 보안 그룹 | 인바운드/아웃바운드 트래픽 제어 방화벽 역할

> 💡 EC2는 클라우드에서 "내가 직접 관리하는 리눅스 서버"와 같음

### 2.2 S3 – 객체 스토리지

> S3(Simple Storage Service)는 **이미지, 문서, 동영상 등 정적 파일을 저장하는 공간**

#### 특징

- 객체 단위로 저장 (파일 + 메타데이터)
- 버킷(bucket) 단위로 관리
- HTTP 기반 접근 가능 → 정적 웹 호스팅도 가능
- 버전 관리, 백업, 암호화 가능

#### 예시 사용

- 사용자 이미지 저장
- 로그 백업 및 분석
- CDN 연결로 정적 웹사이트 서빙

### 2.3 RDS – 관계형 데이터베이스

> RDS(Relational Database Service)는 **MySQL, PostgreSQL 등 DBMS를 클라우드에서 손쉽게 실행할 수 있는 서비스**

#### 장점

- 설치/패치/백업 자동화
- 스냅샷, 모니터링, 복제 지원
- Multi-AZ로 고가용성 구성 가능

> 💡 RDS는 실제로 DB 인스턴스를 띄우고, **내부적으로 EC2에 DB를 설치해 관리해주는 서비스**


### 2.4 Lambda – 서버리스 컴퓨팅

> Lambda는 **서버 없이 코드만 업로드해서 실행하는 서비스**

#### 특징

- 이벤트 기반 실행 (API 호출, 파일 업로드 등)
- 코드 실행 시간만큼만 요금 부과 (100ms 단위)
- Python, Node.js, Java 등 지원
- 최대 15분 실행 제한 (장기 작업에는 부적합)

#### 활용 예

- API 요청 처리 (→ API Gateway와 연결)
- 이미지 업로드 후 자동 썸네일 생성
- 데이터 수집 후 S3 저장

### 2.5 IAM – 권한 및 인증 관리

> IAM(Identity and Access Management)은 **AWS 리소스에 대한 접근 제어 시스템**

#### 주요 요소

| 요소 | 설명 |
|------|------|
| 사용자(User) | 실제 개발자나 시스템 사용자 |
| 그룹(Group) | 사용자 묶음 |
| 역할(Role) | AWS 서비스 자체가 부여받는 권한 |
| 정책(Policy) | JSON 형식으로 정의된 허용/거부 규칙

#### 예시 정책

- "S3 버킷 A만 읽기 가능"
- "Lambda는 S3에 쓸 수 있음"

> 💡 최소 권한 원칙(Least Privilege)을 적용해야 보안이 강화됨


### 2.6 VPC – 가상 네트워크

> VPC(Virtual Private Cloud)는 **내 프로젝트 전용 가상 네트워크 공간**

#### 주요 구성

| 구성 | 설명 |
|------|------|
| 서브넷 | 퍼블릭/프라이빗 영역 나누는 단위 |
| 라우팅 테이블 | 트래픽 흐름 제어 |
| 인터넷 게이트웨이 | 외부 인터넷과 연결 |
| NAT 게이트웨이 | 프라이빗 서브넷 → 외부 접근 허용

> 💡 클라우드에서도 **서버 간 통신, 인터넷 연결을 명확히 설계해야 함**

### 2.7 GCP에서 자주 쓰는 서비스

| 서비스 | 설명 |
|--------|------|
| Compute Engine | EC2와 유사한 가상 서버 |
| Cloud Storage | S3와 동일한 객체 저장소 |
| Cloud SQL | RDS와 유사한 관리형 DB |
| Cloud Functions | Lambda와 유사한 서버리스 함수 |
| Pub/Sub | Kafka처럼 메시지 큐 처리 가능 |
| BigQuery | 초대용량 데이터 분석 플랫폼

> AWS와 GCP는 개념은 거의 동일하지만, **이름과 콘솔 구조가 조금 다름**

### 2.8 서비스 조합 예시

#### 웹 서비스 기본 구성

- EC2 + RDS + S3 + VPC
- 또는 Cloud Functions + Firebase + Firestore (서버리스)

#### AI 모델 배포 구성

- EC2 (GPU) + S3 (모델 파일) + Lambda or FastAPI 서버 + IAM + CloudWatch


## ✅ 3. DevOps 개념과 핵심 구성요소

### 3.1 DevOps란?

> DevOps는 **개발(Development)**과 **운영(Operations)**의 합성어  
> 코드 작성부터 배포·운영까지를 **자동화하고 협업 중심으로 운영**하는 문화이자 도구 세트

### 3.2 DevOps가 등장한 배경

| 과거(전통 개발 방식) | DevOps 이후 |
|--------------------|---------------------|
| 개발팀과 운영팀이 분리 | 협업 및 자동화 중심 |
| 배포는 수동으로, 주기적으로 | 잦고 작은 배포 반복 |
| 테스트는 릴리즈 직전에 | 개발 단계부터 자동화 테스트 |
| 문제가 생기면 원인 추적 어려움 | 실시간 로그/모니터링 활용 |

> 💡 DevOps는 **“작게, 자주, 안전하게”** 배포하는 환경을 만든다

### 3.3 CI / CD 개념

#### CI (Continuous Integration)

> 코드를 **자주 병합하면서, 빌드/테스트를 자동화**하는 것

- git push → 자동 테스트 실행
- 코드 품질 유지 + 빠른 피드백

#### CD (Continuous Delivery / Deployment)

> 코드를 **자동으로 배포**하거나, **누르면 바로 배포 가능한 상태**로 유지하는 것

- Continuous **Delivery**: 자동 배포 전까지 준비 → 승인 후 배포  
- Continuous **Deployment**: 승인 없이도 자동 배포까지 진행

> 💡 CI = "코드 통합 & 테스트" / CD = "자동 배포"

### 3.4 DevOps 핵심 도구 구성

| 단계 | 역할 | 대표 도구 |
|------|------|-----------|
| VCS | 코드 버전 관리 | Git, GitHub, GitLab |
| CI | 테스트 자동화 | GitHub Actions, Jenkins, CircleCI |
| CD | 배포 자동화 | ArgoCD, GitLab CI/CD |
| 컨테이너 | 실행 환경 통일 | Docker |
| 오케스트레이션 | 컨테이너 자동 관리 | Kubernetes |
| 모니터링 | 운영 상태 확인 | Prometheus, Grafana, CloudWatch |
| 알림 | 장애 감지 및 응답 | Slack, PagerDuty |


### 3.5 Git과 GitHub 기반 DevOps

> DevOps는 보통 **Git**을 기반으로 동작하며, GitHub / GitLab 등과 연동하여 구성됨

#### Git 기반 기본 흐름

1. 개발자가 PR 생성 → 테스트 자동 실행
2. 리뷰/승인 → 병합 후 자동 배포 파이프라인 시작
3. 배포 로그 + 모니터링 대시보드로 운영 상태 확인

### 3.6 GitHub Actions 소개

> GitHub에 내장된 **워크플로우 자동화 도구**  
> `.github/workflows/*.yml` 파일로 정의

#### 주요 기능

- PR 생성 시 자동 테스트
- 특정 브랜치 푸시 → 자동 빌드 및 배포
- Docker 이미지 생성 → Docker Hub에 푸시
- AWS CLI, Slack 알림, S3 업로드 등도 가능

> 💡 GitHub Actions는 DevOps 입문자가 가장 쉽게 CI/CD를 체험할 수 있는 도구

### 3.7 DevOps의 핵심 효과

| 효과 | 설명 |
|------|------|
| 빠른 배포 | 매일/수시로 배포 가능 |
| 안정성 증가 | 자동 테스트 및 롤백 설계 |
| 개발자 경험 향상 | 배포 걱정 ↓, 코드 퀄리티 ↑ |
| 협업 효율 ↑ | 통합된 작업 흐름, 로그 추적 가능 |


### 3.8 DevOps와 백엔드 개발자의 연결고리

- PR 작성 → 테스트 자동 실행 → Merge 후 자동 배포  
- AWS EC2 or K8s에 자동으로 반영  
- Sentry, CloudWatch 등으로 장애 감지

> 💡 지금은 "코드를 잘 짜는 것"보다  
> **"잘 배포하고, 잘 운영하는 구조를 짜는 것"이 더 중요해지는 시대**

## ✅ 4. Docker & 컨테이너 구조

### 4.1 컨테이너란?

> 컨테이너는 **애플리케이션과 실행 환경(OS, 라이브러리 포함)**을  
> **하나의 패키지로 묶어 어디서나 똑같이 실행되게 해주는 기술**

#### 컨테이너의 핵심 특징

- 가볍다 (VM보다 훨씬 작음)
- 격리된다 (서로 다른 환경 충돌 없음)
- 어디서든 실행 가능 (리눅스/윈도우/Mac 상관없음)
- 빠르게 시작된다 (수 초 내 실행 가능)

### 4.2 Docker란?

> Docker는 **컨테이너를 쉽게 만들고 실행**할 수 있도록 도와주는 대표적인 도구

#### Docker를 쓰면 좋은 이유

- "내 컴퓨터에서는 잘 되는데…"를 없애줌
- 서버와 개발 환경을 완전히 동일하게 유지
- 애플리케이션 배포가 자동화되기 쉬움


### 4.3 이미지 vs 컨테이너

| 개념 | 설명 | 비유 |
|------|------|------|
| Docker Image | 실행 가능한 패키지 | 설계도 |
| Docker Container | 실제로 실행 중인 인스턴스 | 완성된 제품 |

> 💡 이미지는 **변경 불가한 읽기 전용**  
> 컨테이너는 이미지 기반으로 **읽기/쓰기 가능하게 실행된 상태**

### 4.4 Docker 주요 개념 정리

| 용어 | 설명 |
|------|------|
| Dockerfile | 이미지 생성을 위한 명령어 모음 |
| Image | 빌드된 실행 패키지 |
| Container | 실행 중인 인스턴스 |
| Volume | 외부 저장소 연결 (컨테이너 재시작 시에도 데이터 유지) |
| Network | 컨테이너 간 통신 구성 (브리지, 호스트 등) |
| Registry | 이미지 저장소 (Docker Hub, GitHub Container Registry 등)


### 4.5 Dockerfile 예시

```Dockerfile
FROM python:3.9

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

CMD ["python", "main.py"]
```
> 💡 이 Dockerfile은 Python 3.9 이미지 위에  
> 필요한 라이브러리 설치하고, main.py를 실행하도록 설정한 것

### 4.6 Docker 명령어 요약

| 명령 | 설명 |
|------|------|
| `docker build -t myapp .` | 이미지 빌드 |
| `docker run -d -p 8000:8000 myapp` | 컨테이너 실행 |
| `docker ps -a` | 실행 중/중지된 컨테이너 목록 |
| `docker exec -it 컨테이너명 bash` | 컨테이너 내부 접속 |
| `docker stop 컨테이너명` | 컨테이너 정지 |

### 4.7 실전 예시: FastAPI 서버 도커라이징

1. `Dockerfile` 생성  
2. `docker build -t fastapi-app .`  
3. `docker run -d -p 8000:8000 fastapi-app`  
4. 브라우저에서 `http://localhost:8000/docs` 접속

> 💡 코드만으로 실행 환경 전체를 패키징할 수 있다 → 서버에 그대로 옮기면 끝

### 4.8 Docker의 장단점

| 장점 | 단점 |
|------|------|
| 환경 통일 | 네트워크/보안 구성에 주의 필요 |
| 배포 자동화 | 실행 상태 관리는 별도 툴 필요 |
| 확장성 ↑ | 데이터 영속성 이슈 발생 가능 |

> 그래서 실전에서는 **Kubernetes(K8s)**와 함께 많이 사용됨 (→ 다음에서 설명)

## ✅ 5. Kubernetes 기초

### 5.1 Kubernetes란?

> Kubernetes(K8s)는 **여러 개의 컨테이너를 자동으로 배포, 운영, 복구, 확장해주는 오케스트레이션 플랫폼**

#### 핵심 목표

- 컨테이너를 **자동으로 실행/감시/교체/확장**
- 컨테이너 간 통신 및 로드밸런싱 자동 구성
- 설정 기반으로 **"셀프 힐링"** 운영 환경 구성

### 5.2 Kubernetes 구성요소 요약

| 구성 요소 | 설명 |
|-----------|------|
| **Pod** | 컨테이너 1개 이상을 묶은 최소 단위 |
| **Node** | Pod가 실제로 실행되는 물리 또는 가상 서버 |
| **Cluster** | 여러 Node들의 집합 |
| **Deployment** | 원하는 상태를 정의 → 자동 배포/업데이트 |
| **Service** | 외부 접근, 로드밸런싱, 내부 DNS 제공 |
| **Ingress** | HTTP 라우팅 (도메인별 경로 설정 등) |
| **Volume** | Pod 간 데이터 공유 또는 영속 저장소 연결

> 💡 Kubernetes는 **클러스터 전체를 하나의 컴퓨터처럼 관리**할 수 있게 해준다

### 5.3 쿠버네티스 동작 흐름 예시

```plaintext
개발자가 YAML 설정 작성
→ kubectl apply
→ Deployment가 Pod 생성
→ Node에 Pod가 배치됨
→ Service가 외부 트래픽을 Pod로 라우팅
→ 상태 모니터링 및 장애 발생 시 자동 복구
```

### 5.4 Deployment 예시 (YAML)

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: fastapi-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: fastapi
  template:
    metadata:
      labels:
        app: fastapi
    spec:
      containers:
        - name: fastapi
          image: myrepo/fastapi-app:latest
          ports:
            - containerPort: 8000
```

> 💡 위 YAML은 FastAPI 서버를 3개 Pod로 실행하고, 자동 복구/업데이트까지 정의한 것


### 5.5 Kubernetes의 주요 기능

| 기능 | 설명 |
|------|------|
| 오토 스케일링 | CPU/메모리 사용량에 따라 Pod 수 자동 조절 |
| 롤링 업데이트 | 하나씩 교체하며 무중단 배포 |
| 셀프 힐링 | Pod 장애 발생 시 자동 재시작 |
| 서비스 디스커버리 | 클러스터 내부 DNS로 통신 자동 구성 |
| 리소스 제어 | CPU, 메모리 사용량 제한 가능 (Quota 설정)

### 5.6 Kubernetes vs Docker Compose

| 항목 | Docker Compose | Kubernetes |
|------|----------------|------------|
| 설치/학습 | 간단 | 복잡 |
| 규모 | 소규모 (개발용) | 대규모 서비스용 |
| 기능 | 기본 실행, 의존 관계 구성 | 자동 확장, 장애 복구, 배포 전략 |
| 운영환경 | 단일 서버 중심 | 다수 서버/클러스터 중심 |

> 💡 실무에서는 보통 **Docker로 개발 → Kubernetes로 배포 및 운영**


### 5.7 실전 흐름 요약

1. 개발자는 Docker 이미지 빌드
2. 이미지를 레지스트리에 업로드 (Docker Hub, ECR 등)
3. Kubernetes YAML 정의 (Deployment, Service 등)
4. `kubectl apply -f`로 배포
5. 오토스케일링, 장애 복구 자동 실행

### 5.8 쿠버네티스가 필요한 이유

> 컨테이너 수가 많아질수록, 수동 배포는 불가능

- 3대 서버에 15개 컨테이너 실행
- A 서버가 죽으면 자동으로 B, C로 재배치
- 사용량 급증 시 Pod 수 자동 증가
- 모든 로그, 상태를 대시보드로 모니터링

> 이런 자동화, 확장성, 안정성을 K8s가 책임져줌

## ✅ 6. CI/CD 파이프라인 실전 흐름

### 6.1 실전 배포 흐름 요약

```plaintext
git push → 
테스트 자동 실행 (CI) → 
Docker 이미지 빌드 → 
이미지 업로드 (Docker Hub, ECR 등) → 
Kubernetes 배포 파일 적용 (kubectl apply) → 
서비스에 자동 반영
```
> 💡 이 모든 과정을 `.yml` 설정 한 번으로 자동화 가능!

### 6.2 GitHub Actions 파이프라인 구조

> GitHub Actions는 `.github/workflows/deploy.yml` 파일로 구성한다

#### 기본 구성 예시

```yaml
name: Deploy FastAPI

on:
  push:
    branches: [ "main" ]  # main 브랜치에 push 될 때만 작동

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest  # GitHub이 제공하는 Ubuntu VM에서 실행

    steps:
    - name: Checkout code
      uses: actions/checkout@v3  # 저장소 코드를 받아옴

    - name: Set up Docker
      uses: docker/setup-buildx-action@v2  # Docker 빌드 환경 설정

    - name: Build Docker image
      run: docker build -t myapp:${{ github.sha }} .  # 현재 커밋 해시를 태그로 이미지 빌드

    - name: Login to Docker Hub
      run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u ${{ secrets.DOCKER_USERNAME }} --password-stdin
      # GitHub Secrets를 이용해 Docker Hub 로그인

    - name: Push image
      run: docker push myapp:${{ github.sha }}  # 빌드한 이미지를 Docker Hub에 푸시

    - name: Deploy to Kubernetes
      run: |
        kubectl apply -f k8s/deployment.yaml  # 쿠버네티스에 배포 (사전 설정 필요)

```

### 6.3 필수 개념 정리

| 용어 | 설명 |
|------|------|
| `on.push` | main 브랜치에 push되면 실행 |
| `jobs` | 실제 실행할 일의 집합 |
| `runs-on` | 어떤 환경에서 실행할지 |
| `steps` | 실행할 구체적인 명령 단계 |
| `${{ github.sha }}` | 커밋 해시 (버전 태깅용) |
| `secrets.*` | GitHub 저장소의 보안 정보 (Docker PW 등)

### 6.4 CI 단계에서 수행하는 일

- 코드 checkout (가져오기)
- 테스트 실행 (`pytest`, `npm test` 등)
- 빌드 (Docker, React, Java 등)
- Lint / Type Check
- 슬랙 알림 / Sentry 등록 등 부가 작업

### 6.5 CD 단계에서 수행하는 일

- Docker 이미지 빌드 + 푸시
- Kubernetes 배포 스크립트 실행
- Helm chart 기반 배포도 가능
- 롤링 업데이트, Canary 배포 전략 설정

### 6.6 실전에서 활용되는 CI/CD 흐름

| 단계 | 역할 | 도구 예시 |
|------|------|-----------|
| GitHub Push | 트리거 | GitHub |
| 테스트 자동 실행 | 품질 확인 | GitHub Actions, CircleCI |
| 이미지 빌드 | 실행 환경 생성 | Docker |
| 이미지 푸시 | 배포 준비 | Docker Hub, ECR |
| 배포 실행 | 적용 반영 | kubectl, ArgoCD, Helm |
| 모니터링 | 상태 추적 | Prometheus, Grafana, Slack 알림

### 6.7 CI/CD를 통해 얻는 효과

| 효과 | 설명 |
|------|------|
| 배포 속도 향상 | 개발자가 배포 버튼을 누를 필요 없음 |
| 신뢰성 ↑ | 자동 테스트로 오류 사전 감지 |
| 생산성 ↑ | 배포가 자동이므로 개발에 집중 가능 |
| 협업 효율 ↑ | 명확한 작업 기록 & 로깅

> 💡 결국 DevOps의 핵심은  
> **“코드는 git에 올리고, 나머지는 자동화가 해준다”**는 철학

### 6.8 추가로 알아두면 좋은 것들

- **Slack 연동** → 배포 성공/실패 알림
- **Rollback 스크립트** → 이전 버전 자동 복원
- **다중 환경 배포** → dev, staging, prod 분리
- **Helm Chart** → K8s 리소스 관리의 템플릿화


