# ☁️ AWS EC2 환경에서 3-Tier 통신 구조 기반 웹 서비스 구현 프로젝트 (2차)

## 1️⃣ 프로젝트 소개

본 프로젝트는 **AWS EC2 환경에서 3-Tier(Web–App–DB) 통신 구조를 직접 구현하고,  
운영 환경을 고려한 인프라 설계를 실습하는 것을 목표로 한 프로젝트**입니다.

외부 사용자의 요청이  
**Load Balancer → Web Tier → Application Tier → Database Tier**로 전달되는  
전체 통신 흐름을 직접 구성하여,  
각 계층의 역할과 네트워크 분리를 명확히 이해하는 데 중점을 두었습니다.

또한 실제 운영 환경을 가정하여  
- **VPC를 PRD / DEV 환경으로 분리**
- **VPC Peering을 통한 제한적 네트워크 연결**
- **환경별 Bastion Host 분리 구성**
- **Auto Scaling Group을 통한 확장 및 복구 구조 검증**

을 함께 설계·구현했습니다.

> 본 프로젝트의 웹 서비스(경마 시뮬레이터)는  
> **3-Tier 통신 구조와 인프라 설계를 검증하기 위한 테스트용 서비스**입니다.

---

## 2️⃣ 프로젝트 핵심 목표

- AWS EC2 기반 3-Tier(Web–App–DB) 통신 구조 구현
- VPC 분리를 통한 환경 단위 네트워크 격리 이해
- VPC Peering을 활용한 PRD–DEV 간 안전한 통신 구성
- Bastion Host 분리를 통한 접근 제어 구조 설계
- Auto Scaling Group 적용 및 인프라 안정성 검증

---

## 3️⃣ 인프라 아키텍처


::contentReference[oaicite:0]{index=0}


### 🔹 전체 통신 및 네트워크 구조

#### ① 사용자 요청 흐름
1. 사용자 요청 → **Application Load Balancer**
2. ALB → **Web Tier (Nginx, EC2)**
3. Web Tier → **Application Tier (Tomcat, EC2)**
4. Application Tier → **Database Tier (RDBMS, EC2)**
5. 처리 결과 역방향 응답

#### ② 네트워크 환경 분리
- **PRD VPC**
  - 실제 서비스 운영 환경
  - Web / App / DB Tier 구성
- **DEV VPC**
  - 개발 및 테스트 환경
  - 동일한 3-Tier 구조 유지

#### ③ VPC Peering 구성
- PRD VPC ↔ DEV VPC 간 **VPC Peering 연결**
- 라우팅 테이블을 통해 **필요한 통신만 허용**
- 환경 간 완전 통합이 아닌 **논리적 분리 유지**

---

## 4️⃣ Bastion Host 설계

- **PRD Bastion Host**
  - 운영 환경 접근 전용
  - 외부에서 직접 Private 인스턴스 접근 차단
- **DEV Bastion Host**
  - 개발 및 테스트 환경 접근 전용
- 각 VPC에 **독립적인 Bastion Host 구성**
- SSH 접근 경로 단일화로 보안 및 접근 관리 강화

---

## 5️⃣ 제공 웹 서비스 (테스트용)

- 간단한 웹 기반 **경마 시뮬레이터**
- 페이지 요청 및 결과 조회 중심의 단순 구조
- 복잡한 비즈니스 로직보다 **통신·부하 테스트 목적**
- Auto Scaling 및 장애 상황 검증을 위한 트래픽 유발용 서비스

---

## 6️⃣ Auto Scaling 적용 목적

- Web / Application Tier에 Auto Scaling Group 적용
- Health Check 실패 시 인스턴스 자동 교체 확인
- 트래픽 증가 시 인스턴스 확장 흐름 검증
- 3-Tier 통신 구조가 확장 환경에서도 유지되는지 확인

---

## 7️⃣ 주요 구현 내용

- PRD / DEV VPC 분리 설계
- VPC Peering 기반 환경 간 연결
- Public / Private Subnet 구성
- 환경별 Bastion Host 이중 구성
- ALB + Target Group 구성
- EC2 Auto Scaling Group 생성 및 테스트

---

## 8️⃣ 적용 기술 스택

### ☁️ AWS
- EC2
- Application Load Balancer (ALB)
- Auto Scaling Group
- VPC / Subnet / Route Table
- VPC Peering

### 🌐 Web / Application
- Nginx
- Apache Tomcat
- Java Web Application (WAR/JAR)

### 🗄️ Database
- RDBMS (EC2 기반)

### 🛠️ OS & Tools
- Linux (Ubuntu)
- SSH
- AWS Management Console

---

## 9️⃣ 프로젝트 성과

- 3-Tier 통신 구조 직접 설계 및 구현
- PRD / DEV 환경 분리를 통한 운영 구조 이해
- VPC Peering을 활용한 환경 간 통신 제어 경험
- Bastion Host 분리로 보안 접근 구조 체득
- Auto Scaling 기반 인프라 안정성 검증

---

## 🔟 한 줄 요약

> **AWS EC2 환경에서 3-Tier 통신 구조를 구현하고,  
> VPC 분리·Peering·Bastion 설계를 통해  
> 운영 환경을 고려한 인프라 아키텍처를 구축한 프로젝트**
