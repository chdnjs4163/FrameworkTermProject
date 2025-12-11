# ⚾ ALL IN ONE BASEBALL (베이스캠프)
> **Spring Boot & JPA 기반의 올인원 야구 정보 제공 및 팬 커뮤니티 플랫폼**
>

<img width="911" height="849" alt="image" src="https://github.com/user-attachments/assets/3725cea3-71f1-4c8a-82a6-f9c83f523a69" />


<br>

## 📝 프로젝트 소개 (Introduction)
**ALL IN ONE BASEBALL**은 야구 팬들이 경기 일정, 실시간 순위, 선수 기록 등 파편화된 정보를 한곳에서 확인하고, 응원하는 팀과 선수를 설정하여 맞춤형 정보를 제공받을 수 있는 통합 플랫폼입니다.

기존 정적 웹페이지의 한계를 넘어, **Spring Boot와 JPA**를 활용해 데이터를 동적으로 관리하고, 실시간 크롤링(Jsoup) 과  데이터 시각화(Chart.js) 를 통해 생동감 있는 사용자 경험을 제공합니다.

<br>

## 🛠 기술 스택 (Tech Stack)

| 구분 | 상세 기술 |
| :--- | :--- |
| **Backend** | Java 17, Spring Boot 3.4.0, Spring Data JPA |
| **Frontend** | HTML5, CSS3, JavaScript, Thymeleaf |
| **Database** | MySQL |
| **Library** | Chart.js (시각화), Jsoup (크롤링), Lombok |
| **Tools** | IntelliJ IDEA, Git/GitHub, MySQL Workbench |

<br>

## ⚙️ 시스템 아키텍처 (Architecture)
본 프로젝트는 **MVC (Model-View-Controller) 패턴**을 준수하여 설계되었습니다.

<img width="321" height="784" alt="image" src="https://github.com/user-attachments/assets/cd30681e-0e1f-4f80-98f5-e7b8143e6cd3" />



<br>

## 💾 데이터베이스 설계 (ERD)
회원과 선수 간의  N:M 관계 를 해소하기 위해 중간 테이블(`Favorite`)을 설계하여 데이터 무결성을 확보했습니다.

<img width="339" height="834" alt="image" src="https://github.com/user-attachments/assets/2a18b746-f86e-4e8c-aed9-dc705e6df855" />


<br>

## ✨ 주요 기능 (Key Features)

### 1. 메인 대시보드 & 실시간 뉴스
- 사용자별 맞춤형 환영 메시지 제공
- Jsoup을 활용하여 네이버/다음 스포츠 야구 뉴스를 실시간 크롤링하여 제공
- 직관적인 카드 UI로 주요 기능 접근성 강화

### 2. 경기 일정 관리 (Calendar)
- 월별 경기 일정을 캘린더 형태로 조회
- 관리자(Admin) 권한: 일정 등록 및 삭제 가능 (DB 연동)

### 3. 선수 검색 및 찜하기 (Favorites)
- 팀별, 포지션별 선수 필터링 검색
- 즐겨찾기(찜하기): 별(★) 아이콘 클릭 시 즉시 내 보관함에 추가/삭제 (Toggle 방식)
- 복합 유니크 키** 적용으로 중복 찜하기 방지

### 4. 실시간 순위 시각화 (Chart.js)
- DB에 저장된 구단별 승률 데이터를 조회
- Chart.js를 활용하여 막대그래프로 시각화, 순위 경쟁 상황을 직관적으로 전달

### 5. 회원 관리 시스템
- 회원가입 (BCrypt 비밀번호 암호화, 이메일/ID 중복 검사)
- 로그인/로그아웃 (HttpSession 관리)
- 관리자 모드: 전체 회원 조회 및 강제 탈퇴 기능

<br>

## 🔥 기술적 도전 및 성과 (Troubleshooting)

### ✅ 1. 다대다(N:M) 관계의 데이터 정합성 문제 해결
- **문제:** 한 명의 회원이 여러 선수를 찜하고, 한 선수가 여러 회원에게 찜 당하는 구조에서 데이터 관리가 복잡함.
- **해결:** 중간 엔티티 `Favorite`을 설계하고, **`@UniqueConstraint`**를 사용하여 `(member_id, player_id)` 조합이 중복되지 않도록 DB 레벨에서 제약 조건을 설정함.

### ✅ 2. 대량 데이터 정렬 최적화
- **문제:** 실시간 순위 조회 시, 애플리케이션 메모리에서 정렬할 경우 성능 저하 우려.
- **해결:** **Spring Data JPA Query Method** (`findAllByOrderByRankingAsc`)를 사용하여 DB 조회 단계에서 정렬을 수행, 메모리 부하를 줄이고 속도를 개선함.

### ✅ 3. 비용 효율적인 크롤링 파이프라인
- **문제:** 뉴스 데이터를 DB에 저장할 경우 최신성 유지 문제와 스토리지 낭비 발생.
- **해결:** 메인 페이지 요청 시점에 **Jsoup**이 실시간으로 뉴스를 가져와 Model에 담아 뿌려주는 휘발성 방식을 채택하여 **비용 0, 최신성 100%**를 달성함.

<br>

## 🚀 실행 방법 (How to run)

**1. 레포지토리 클론**
```bash
git clone [https://github.com/본인아이디/ALL-IN-ONE-BASEBALL.git](https://github.com/본인아이디/ALL-IN-ONE-BASEBALL.git)
