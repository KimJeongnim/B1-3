# 자동화 도구 비교 및 자동화 구현 프로젝트

## 과제 정보

| 항목 | 내용 |
|------|------|
| 과제명 | 자동화 도구 비교 및 자동화 구현 |
| 사용 도구 | n8n, Make |
| 연동 서비스 | Google Sheets, Discord |
| 작성자 | 김정님 |
| 제출일 | 2026-07-16 |

---

# 프로젝트 1. 자동화 도구 비교 구현

## 1. 프로젝트 개요

Google Sheets에 학생의 출석 정보(입실/퇴실)가 새로 등록되면 Discord 채널로 자동 알림을 전송하는 워크플로우를 구현하였다.

동일한 자동화 구조를 n8n과 Make에서 각각 구현하고, 두 도구의 기능과 사용성을 비교하였다.

Google Sheets에 새로운 출석 정보가 등록되면 Trigger가 자동 실행되고, 조건 분기를 통해 입실과 퇴실을 구분하여 Discord 채널로 자동 알림을 전송하도록 구성하였다.

두 도구 모두 동일한 기능을 수행하였지만, 워크플로우 구성 방식과 사용자 인터페이스에서 차이가 있음을 확인할 수 있었다.

---

## 2. 사용 기술

| 도구 | 용도 |
|------|------|
| Google Sheets | 출석 정보 저장 |
| Discord | 알림 전송 |
| n8n | 자동화 워크플로우 구현 |
| Make | 자동화 워크플로우 구현 |

---

# 3. 워크플로우 구조

## 공통 흐름

```text
Google Sheets
      │
      ▼
Google Sheets Trigger
      │
      ▼
조건 분기(IF / Router)
      │
 ┌────┴────┐
 ▼         ▼
입실 알림   퇴실 알림
Discord    Discord
```

Google Sheets에 새로운 행이 추가되면 Trigger가 실행되고, 이벤트 값(입실/퇴실)에 따라 조건 분기를 수행한 뒤 Discord 채널로 알림을 전송한다.

---

# 4. n8n 구현

## 워크플로우 구성

<img width="713" height="400" alt="n8n워크플로우" src="https://github.com/user-attachments/assets/1ee5fc46-6a7a-496e-9a90-d6d53ffacc9a" />


### 설명

- Google Sheets Trigger
- IF 조건 분기
- Discord 메시지 전송

---

## 실행 결과 (입실)

<img width="1095" height="650" alt="n8n테스트샷1" src="https://github.com/user-attachments/assets/d9e0ef93-8a4f-471f-8933-b6e9f80b069e" />


### 결과

- Google Sheets Trigger 실행
- 입실 조건(True) 만족
- Discord 입실 알림 전송 성공

---

## 실행 결과 (퇴실)

<img width="1076" height="647" alt="n8n테스트샷2" src="https://github.com/user-attachments/assets/10f4e959-813f-4f52-8587-8539043dc695" />


### 결과

- Google Sheets Trigger 실행
- 퇴실 조건(False) 만족
- Discord 퇴실 알림 전송 성공

---

# 5. Make 구현

## 워크플로우 구성

<img width="907" height="617" alt="make워크플로우" src="https://github.com/user-attachments/assets/51dcac1e-b9d3-4ea4-8492-2022909a3b82" />


### 설명

- Google Sheets Watch New Rows
- Router 조건 분기
- Discord 메시지 전송

---

## 실행 결과

<img width="1186" height="741" alt="make테스트샷" src="https://github.com/user-attachments/assets/aade7bb7-4f53-41ca-9bfa-3cba052583ff" />

<img width="1170" height="707" alt="make테스트샷1" src="https://github.com/user-attachments/assets/20b965ec-c1b0-4c03-add2-d998ad572d90" />


### 결과

- Google Sheets에서 새로운 행 감지
- Router 조건 분기 수행
- Discord 메시지 전송 성공

---

## 실행 상세

<img width="1463" height="938" alt="테스트샷2" src="https://github.com/user-attachments/assets/0343a88a-824a-4f94-95a5-ae79d574888b" />


### 결과

- Google Sheets 데이터 정상 수신
- Discord API 호출 성공
- 메시지 정상 전송 확인

---

# 6. Discord 실행 결과

## 입실 알림

<img width="290" height="200" alt="입실알림" src="https://github.com/user-attachments/assets/373ae318-29be-46cf-8c1a-e7d1b4923ec2" />


Google Sheets에 입실 정보가 추가되면 Discord 채널에 입실 알림이 자동으로 전송된다.

---

## 퇴실 알림

<img width="270" height="141" alt="퇴실알림2" src="https://github.com/user-attachments/assets/76fb16eb-482f-4d47-8808-922444ccd20e" />


Google Sheets에 퇴실 정보가 추가되면 Discord 채널에 퇴실 알림이 자동으로 전송된다.

---

테스트 결과 Google Sheets에 새로운 출석 정보가 등록될 때마다 자동으로 워크플로우가 실행되었으며, 이벤트 종류에 따라 Discord 채널에 입실 또는 퇴실 알림이 정상적으로 전송되는 것을 확인하였다.

---

# 프로젝트 1 비교 분석

## 구현 과정 요약

동일한 자동화 구조를 n8n과 Make에서 각각 구현하였다.

Google Sheets에 새로운 출석 정보가 등록되면 워크플로우가 자동으로 실행되며, 입실과 퇴실 여부를 조건 분기로 판단하여 Discord 채널에 알림을 전송하도록 구성하였다.

---

## 비교 분석

| 비교 항목 | n8n | Make |
|-----------|------|------|
| UI/UX | 개발자 친화적 노드 방식 | 직관적인 드래그앤드롭 방식 |
| 설정 난이도 | 초기 설정이 다소 복잡 | 초보자도 쉽게 설정 가능 |
| Google Sheets 연동 | 지원 | 지원 |
| Discord 연동 | Webhook 또는 API 사용 | Discord 기본 모듈 제공 |
| 조건 분기 | IF Node | Router |
| 무료 플랜 | 무료 범위가 넓음 | Operation 제한 |
| 실행 로그 | Execution에서 상세 확인 가능 | Scenario History 확인 |
| 확장성 | 오픈소스로 매우 높음 | 제공 모듈 중심 |
| 유지보수 | 복잡한 워크플로우에 유리 | 간단한 워크플로우에 유리 |
| 학습 난이도 | 다소 높음 | 비교적 쉬움 |

두 도구 모두 동일한 자동화를 구현할 수 있었으나, Make는 직관적인 UI로 빠르게 구축하기에 적합했고, n8n은 다양한 조건 분기와 높은 확장성을 제공하여 복잡한 자동화에 더 적합하였다.

---

## n8n 장점

- 무료 플랜 활용 범위가 넓다.
- 조건 분기를 다양하게 구현할 수 있다.
- 실행 로그 확인이 편리하다.
- 오픈소스 기반이라 확장성이 높다.

### 단점

- 초기 설정이 다소 어렵다.
- 초보자가 사용하기에는 학습 시간이 필요하다.

---

## Make 장점

- UI가 직관적이다.
- Router 구성이 이해하기 쉽다.
- 초보자도 쉽게 자동화를 구현할 수 있다.

### 단점

- 무료 플랜의 Operation 제한이 있다.
- 복잡한 자동화에서는 제약이 발생할 수 있다.

---

## 적합한 활용 환경

### n8n

복잡한 조건 분기와 다양한 자동화가 필요한 프로젝트에 적합하다.

### Make

간단한 자동화를 빠르게 구축하거나 자동화 입문자가 사용하기에 적합하다.

---

# 프로젝트 2. 자유 주제 자동화

# 12시간 이상 퇴실 기록이 없는 학생 자동 알림 시스템

---

# 1. 프로젝트 개요

학생의 출석 정보를 Google Sheets에서 주기적으로 확인하여 **입실 후 12시간이 지났음에도 퇴실 기록이 없는 학생을 자동으로 탐지하고 Discord로 알림을 전송하는 시스템**을 구현하였다.

기존에는 관리자가 직접 Google Sheets를 확인하여 퇴실 기록이 없는 학생을 찾아야 했지만, 자동화를 통해 누락된 퇴실 기록을 자동으로 확인하고 즉시 안내할 수 있도록 구현하였다.

또한 알림이 전송된 학생은 Google Sheets의 **상태(Status)** 컬럼을 자동으로 업데이트하여 동일한 학생에게 중복 알림이 전송되지 않도록 하였다.

---

# 2. 자동화 업무 정의

자동화 대상 업무는 **입실 후 12시간 이상 경과했지만 퇴실 기록이 없는 학생을 자동으로 확인하고 Discord로 안내하는 업무**이다.

Google Sheets를 일정 시간마다 조회하여 모든 출석 기록을 확인한 후,

- 입실 기록인지 확인
- 입실 후 12시간 이상 경과했는지 확인
- 이후 퇴실 기록이 존재하는지 확인

위 조건을 모두 만족하면 Discord로 알림을 전송하고 상태를 업데이트하도록 구성하였다.

---

# 자동 실행 구조

```text
Schedule Trigger
        │
        ▼
Google Sheets 조회
        │
        ▼
Code(JavaScript)
(12시간 이상 미퇴실 학생 검색)
        │
        ▼
Google Sheets 상태 업데이트
        │
        ▼
Discord 알림 전송
```

---

# 자동화 전/후 비교

## 자동화 전

```text
Google Sheets 확인
        ↓
관리자가 미퇴실 학생 검색
        ↓
Discord 공지 작성
        ↓
학생 확인
```

## 자동화 후

```text
Schedule Trigger
        ↓
Google Sheets 조회
        ↓
12시간 이상 미퇴실 학생 검색
        ↓
Google Sheets 상태 업데이트
        ↓
Discord 자동 알림
```

---

# 3. 선정한 도구

## n8n

## 선정 이유

본 프로젝트에서는 n8n을 선택하였다.

n8n은 Google Sheets와 Discord를 쉽게 연동할 수 있으며 JavaScript Code 노드를 이용하여 복잡한 조건을 구현할 수 있었다.

또한 Schedule Trigger를 사용하여 일정 시간마다 자동으로 데이터를 확인할 수 있고 실행 로그를 쉽게 확인할 수 있어 테스트와 오류 수정이 편리하였다.

---

# 4. 워크플로우 설계

```text
Schedule Trigger
        │
        ▼
Google Sheets
        │
        ▼
Code(JavaScript)
        │
        ▼
Google Sheets Update Row
        │
        ▼
Discord
```

---

# 5. 워크플로우 설명

1. Schedule Trigger가 일정 시간마다 실행된다.
2. Google Sheets에서 출석 데이터를 조회한다.
3. Code(JavaScript) 노드에서 다음 조건을 확인한다.
   - 입실 기록인지 확인
   - 입실 후 12시간 이상 경과했는지 확인
   - 이후 퇴실 기록이 존재하는지 확인
4. 조건을 만족하면 Google Sheets의 상태 컬럼을 "퇴실 알림 발송"으로 변경한다.
5. Discord에 자동으로 안내 메시지를 전송한다.

---

# 6. 구현 화면

<img width="1040" height="245" alt="테스트샷1" src="https://github.com/user-attachments/assets/802f5f15-1abb-4ad4-964f-fe5c424d3dab" />


### 워크플로우 설명

- Schedule Trigger가 주기적으로 실행된다.
- Google Sheets에서 전체 출석 기록을 조회한다.
- Code(JavaScript)에서 미퇴실 학생을 탐색한다.
- Google Sheets 상태를 업데이트한다.
- Discord로 자동 알림을 전송한다.

---

# 7. 실행 결과

## Google Sheets 조회

<img width="714" height="792" alt="테스트샷3" src="https://github.com/user-attachments/assets/039b49c5-15db-4b20-9cfa-ab6123a3a7ea" />


### 결과

- 출석 데이터를 정상적으로 조회하였다.

---

## Code(JavaScript) 실행

<img width="502" height="154" alt="테스트4" src="https://github.com/user-attachments/assets/16b119ee-bf73-4197-8bb9-28b97c1f0f73" />


### 결과

- 퇴실 기록이 없는 학생을 정상적으로 탐지하였다.
- row_number와 학생 정보를 반환하였다.

---

## Google Sheets 상태 업데이트

<img width="723" height="150" alt="테스트5" src="https://github.com/user-attachments/assets/082f786f-1916-4e67-86c8-632f47ed94af" />


### 결과

- 상태(Status) 컬럼이 "퇴실 알림 발송"으로 변경되었다.

---

## Discord 알림

<img width="326" height="209" alt="테스트6" src="https://github.com/user-attachments/assets/ef32c86a-3242-4c59-bb52-a220d2d6f25b" />


### 결과

- 퇴실 기록이 없는 학생에게 안내 메시지가 정상적으로 전송되었다.

---

# 자동화 효과

- 관리자가 직접 출석부를 확인하지 않아도 된다.
- 퇴실 기록 누락을 자동으로 감지할 수 있다.
- 학생에게 즉시 안내가 가능하다.
- Google Sheets 상태를 자동으로 기록하여 중복 알림을 방지할 수 있다.
- 반복 업무를 자동화하여 업무 효율성과 정확성을 높일 수 있다.

---

# 보안 처리

제출 화면에 포함된 API Key, Webhook URL, Discord Token 및 Google 계정 정보는 모두 마스킹(***) 처리하여 민감한 정보가 노출되지 않도록 하였다.

---

# 느낀 점

이번 프로젝트에서는 n8n을 활용하여 Google Sheets와 Discord를 연동하고, JavaScript Code 노드를 이용하여 실제 업무에서 활용 가능한 자동화 시스템을 구현하였다.

특히 단순히 데이터를 전달하는 수준이 아니라 입실 후 12시간이 경과한 학생을 탐지하고, 퇴실 기록 여부를 판단하는 로직을 직접 구현하면서 조건 기반 자동화의 활용 방법을 이해할 수 있었다.

또한 Google Sheets의 상태를 자동으로 업데이트하여 중복 알림을 방지하는 기능까지 구현함으로써 실제 운영 환경에서도 활용 가능한 자동화 시스템을 경험할 수 있었다.

이번 프로젝트를 통해 반복 업무를 자동화하는 과정뿐만 아니라 데이터 처리, 조건 분기, 외부 서비스 연동 등 자동화 시스템 구축 전반에 대한 이해를 높일 수 있었다.
