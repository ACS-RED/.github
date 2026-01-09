# ☁️ AWS EC2 환경에서 3-Tier 통신 구조 기반 웹 서비스 구현 프로젝트 (2차)

## 1️⃣ 프로젝트 소개

본 프로젝트는 **AWS EC2 환경에서 3-Tier(Web–App–DB) 통신 구조를 직접 설계·구현하고,  
실제 운영 환경을 고려한 인프라 아키텍처를 검증하는 것을 목표로 한 프로젝트**입니다.

외부 사용자의 요청이  
**Load Balancer → Web Tier → Application Tier → Database Tier**  
순서로 전달되는 전체 통신 흐름을 직접 구성함으로써,

- 각 Tier의 역할 분리
- 네트워크 단위의 보안 경계 설정
- 확장 환경에서도 안정적인 통신 구조 유지

를 중점적으로 학습하고 구현했습니다.

또한 단순한 구성에 그치지 않고,

- PRD / DEV VPC 분리
- VPC Peering을 통한 제한적 환경 간 연결
- 환경별 Bastion Host 분리
- Auto Scaling Group 기반 확장 및 복구 구조
- Internal / External ALB 분리 설계

등 **실제 서비스 운영을 가정한 인프라 설계 요소**를 함께 반영했습니다.

> 본 프로젝트에서 제공하는 웹 서비스(경마 시뮬레이터)는  
> **3-Tier 통신 구조와 인프라 설계를 검증하기 위한 테스트용 서비스**입니다.

---

## 2️⃣ 프로젝트 핵심 목표

- AWS EC2 기반 3-Tier(Web–App–DB) 통신 구조 구현
- PRD / DEV 환경 분리를 통한 네트워크 격리 이해
- VPC Peering을 활용한 안전한 환경 간 통신 구성
- Bastion Host 분리를 통한 접근 제어 구조 설계
- Auto Scaling Group 적용 및 인프라 안정성 검증
- Sticky Session 기반 세션 유지 구조 이해

---

## 3️⃣ 인프라 아키텍처

![Architecture Diagram](./docs/images/architecture-placeholder.png)

### 🔹 전체 통신 흐름

1. 사용자 요청 → **External ALB (Internet-facing)**
2. External ALB → **Web Tier (Nginx, EC2, ASG)**
3. Web Tier → **Internal ALB**
4. Internal ALB → **Application Tier (Spring Boot / Tomcat, EC2, ASG)**
5. Application Tier → **Database Tier (RDS MySQL)**
6. 처리 결과 역방향 응답

---

### 🔹 네트워크 환경 분리

#### PRD VPC
- 실제 서비스 운영 환경
- Web / App / DB Tier 구성
- External / Internal ALB 분리

#### DEV VPC
- 개발 및 테스트 환경
- PRD와 동일한 3-Tier 구조 유지

#### VPC Peering
- PRD ↔ DEV VPC 간 Peering 연결
- 라우팅 테이블을 통해 필요한 통신만 허용
- 환경 간 논리적 분리 유지

---

## 4️⃣ Bastion Host 설계

- **PRD Bastion Host**
  - 운영 환경 접근 전용
  - 외부에서 Private Subnet 직접 접근 차단
- **DEV Bastion Host**
  - 개발 및 테스트 환경 접근 전용
- 각 VPC에 독립적인 Bastion Host 구성
- SSH 접근 경로 단일화로 보안 및 관리 효율 향상

---

## 5️⃣ 제공 웹 서비스 (테스트용)

- 간단한 웹 기반 **경마 시뮬레이터**
- 페이지 요청 및 결과 조회 중심 구조
- 복잡한 비즈니스 로직보다  
  **통신 흐름 · 트래픽 · 오토스케일링 검증 목적**
- 인프라 동작 확인을 위한 테스트 서비스

---

## 6️⃣ Auto Scaling & 운영 관점 설계

### 🔹 Auto Scaling 적용 목적

- Web / Application Tier에 Auto Scaling Group 적용
- Health Check 실패 시 인스턴스 자동 교체
- 트래픽 증가 시 인스턴스 자동 확장
- 확장 환경에서도 3-Tier 통신 구조 유지 여부 검증

### 🔹 Sticky Session 적용

- **External ALB**
  - 사용자 ↔ Web Tier 세션 고정
- **Internal ALB**
  - Web Tier ↔ Application Tier 세션 고정
- 스케일 아웃 환경에서 로그인 유지 문제 해결

---

## 7️⃣ 주요 구현 내용

- PRD / DEV VPC 분리 설계
- VPC Peering 기반 환경 간 통신 구성
- Public / Private Subnet 분리
- 환경별 Bastion Host 이중 구성
- External / Internal ALB 분리 설계
- EC2 Auto Scaling Group 생성 및 동작 검증

---

## 8️⃣ 적용 기술 스택

### ☁️ Cloud / Infra
- AWS EC2
- Application Load Balancer (ALB)
- Auto Scaling Group
- VPC / Subnet / Route Table
- VPC Peering

### 🌐 Web / Application
- Nginx
- Spring Boot / Apache Tomcat
- Java Web Application (JAR)

### 🗄️ Database
- MySQL (AWS RDS)

### 🛠️ OS & Tools
- Linux (Ubuntu / Amazon Linux)
- SSH
- AWS Management Console

---

## 9️⃣ 프로젝트 성과

- 3-Tier 통신 구조를 설계부터 구현까지 직접 수행
- PRD / DEV 환경 분리를 통한 운영 구조 이해
- VPC Peering을 활용한 환경 간 통신 제어 경험
- Bastion Host 기반 보안 접근 구조 체득
- Auto Scaling 환경에서의 서비스 안정성 검증

---

## 🔟 한 줄 요약

> **AWS EC2 환경에서 3-Tier 통신 구조를 구현하고,  
> VPC 분리·Peering·Bastion·Auto Scaling 설계를 통해  
> 실제 운영을 고려한 인프라 아키텍처를 구축한 프로젝트**
