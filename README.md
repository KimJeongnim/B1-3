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

동일한 자동화 구조를 n8n과 Make에서 각각 구현하였다.

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
- 퇴실 조건(False) 분기 실행
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

# 프로젝트 1 비교 분석

## 구현 과정 요약

동일한 자동화 구조를 n8n과 Make에서 각각 구현하였다.

Google Sheets에 새로운 출석 정보가 등록되면 자동으로 실행되며, 입실과 퇴실 여부를 조건 분기로 판단하여 Discord 채널에 알림을 전송하도록 구성하였다.

---

## 비교 분석

| 비교 항목 | n8n | Make |
|-----------|------|------|
| UI/UX | 개발자 친화적 노드 방식 | 직관적인 드래그앤드롭 방식 |
| 설정 난이도 | 초기 설정이 다소 복잡 | 초보자도 쉽게 설정 가능 |
| Google Sheets 연동 | 지원 | 지원 |
| Discord 연동 | Webhook 또는 API 사용 | 기본 모듈 제공 |
| 조건 분기 | IF Node | Router |
| 무료 플랜 | 무료 범위가 넓음 | Operation 제한 |
| 실행 로그 | Execution에서 상세 확인 가능 | Scenario History 확인 |
| 확장성 | 오픈소스로 매우 높음 | 제공 모듈 중심 |
| 유지보수 | 복잡한 워크플로우에 유리 | 간단한 워크플로우에 유리 |
| 학습 난이도 | 다소 높음 | 비교적 쉬움 |

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

## 1. 프로젝트 개요

학생의 출석 정보가 Google Sheets에 새로운 행으로 등록되면 Discord 채널에 자동으로 출석 알림을 전송하는 반복 업무를 자동화하였다.

기존에는 Google Sheets의 출석 정보를 확인한 후 Discord에 직접 공지를 작성해야 했지만, 자동화를 통해 새로운 행이 등록되는 즉시 알림이 전송되도록 구현하였다.

---

## 2. 자동화 업무 정의

자동화 대상 업무는 학생의 입실 및 퇴실 정보를 Discord 채널에 안내하는 반복 업무이다.

Google Sheets에 새로운 출석 정보가 등록되면 자동으로 실행되어 Discord에 해당 정보를 전송하도록 구성하였다.

---

## 자동 실행 구조

Google Sheets에 새로운 행이 등록되는 순간 Google Sheets Trigger가 자동으로 실행된다.

이후 IF 노드에서 입실과 퇴실을 구분하고, 조건에 맞는 Discord 메시지를 자동으로 전송하도록 구현하였다.

## 자동화 전/후 비교

### 자동화 전

```text
Google Sheets 출석 정보 등록
          ↓
담당자가 출석 정보 확인
          ↓
Discord 공지 작성
          ↓
학생 확인
```

### 자동화 후

```text
Google Sheets 출석 정보 등록
          ↓
Google Sheets Trigger
          ↓
IF 조건 분기
          ↓
Discord 자동 알림
          ↓
학생 확인
```

---

## 3. 선정한 도구

### n8n

### 선정 이유

본 프로젝트에서는 n8n을 선택하였다.

n8n은 무료 플랜에서도 다양한 자동화 기능을 사용할 수 있으며 Google Sheets와 Discord를 쉽게 연동할 수 있다.

또한 IF 노드를 이용하여 입실과 퇴실을 조건에 따라 분기할 수 있었고 실행 로그를 확인하기 쉬워 테스트와 오류 수정이 편리하였다.

오픈소스 기반이므로 향후 기능을 확장하기에도 적합하다고 판단하였다.

---

## 4. 워크플로우 설계

```text
Google Sheets
      │
      ▼
Google Sheets Trigger
      │
      ▼
IF
 ┌────┴────┐
 ▼         ▼
입실       퇴실
 │          │
 ▼          ▼
Discord   Discord
```

---

## 5. 워크플로우 설명

1. Google Sheets에 새로운 출석 정보가 등록된다.
2. Google Sheets Trigger가 실행된다.
3. IF 노드에서 이벤트 종류를 확인한다.
4. 입실이면 입실 Discord 메시지를 전송한다.
5. 퇴실이면 퇴실 Discord 메시지를 전송한다.
6. Discord 채널에서 자동으로 결과를 확인할 수 있다.

---

## 6. 구현 화면

<img width="713" height="400" alt="n8n워크플로우" src="https://github.com/user-attachments/assets/516b4792-5def-4736-8294-f6218ffc0799" />

- Google Sheets Trigger를 통해 새로운 행을 감지한다.
- IF 노드에서 입실과 퇴실을 구분한다.
- 조건에 따라 Discord 채널로 자동 알림을 전송한다.

---

## 7. 실행 결과

### 입실

<img width="1077" height="606" alt="n8n입실테스트" src="https://github.com/user-attachments/assets/b3b7bd1a-2661-45f5-ba33-c23c8555a191" />

---

### 퇴실

<img width="1081" height="640" alt="n8n퇴실알림" src="https://github.com/user-attachments/assets/ef0d3a03-a11d-4c2e-8a5f-fa9e733b3ec5" />

Google Sheets에 출석 정보가 등록되면 Discord 채널에 입실 또는 퇴실 알림이 자동으로 전송되는 것을 확인하였다.

---

### Discord 결과

<img width="264" height="132" alt="입실알림1" src="https://github.com/user-attachments/assets/7ae1c0d6-5f02-41fd-a2cc-96955c44de83" />

<img width="247" height="157" alt="퇴실알림1" src="https://github.com/user-attachments/assets/c29b52e9-df07-477b-b29e-52e5deba02d5" />

---

# 자동화 효과

- 반복적인 Discord 공지 작성 업무를 제거하였다.
- 출석 정보 등록 즉시 실시간 알림이 가능하다.
- 관리자의 업무 시간을 절약할 수 있다.
- 학생들에게 즉시 출석 현황을 전달할 수 있다.
- 사람의 실수로 인한 누락 가능성을 줄일 수 있다.
- 반복 업무의 표준화를 통해 업무 일관성을 확보할 수 있다.
---

# 보안 처리

제출 화면에 포함된 API Key, Webhook URL, Discord Token 및 Google 계정 정보는 모두 마스킹(***) 처리하여 민감한 정보가 노출되지 않도록 하였다.

---

# 느낀 점

이번 프로젝트를 통해 n8n과 Make를 직접 사용하며 동일한 자동화 시스템을 구현하고 두 도구를 비교할 수 있었다.

Make는 직관적인 인터페이스를 제공하여 빠르게 워크플로우를 구성할 수 있었고, n8n은 조건 분기와 실행 로그 확인 기능이 뛰어나 복잡한 자동화에 적합하다는 점을 확인하였다.

또한 Google Sheets와 Discord를 연동하여 실제로 동작하는 자동화 시스템을 구현하면서 반복 업무를 자동화하는 과정을 경험할 수 있었으며, 자동화 도구의 활용 방법과 장단점을 이해하는 계기가 되었다.

특히 동일한 자동화를 서로 다른 플랫폼에서 구현해 보면서 각 도구의 특징과 차이점을 직접 비교할 수 있었다.

이번 프로젝트를 통해 자동화 기술은 반복 업무의 효율성과 정확성을 높이는 데 매우 효과적이라는 점을 확인할 수 있었으며, 앞으로도 다양한 업무에 자동화를 적극 활용해 보고자 한다.
