# 시스템 구축시 고려사항

## 보안 부문

### 요약

1. 문서, 산출물 보안 통제
2. 저장매체 통제
3. 내/외부망 접근
4. 코드 보안 취약점
5. 모의 해킹 환경
6. 작업 PC S/W 최신 버전
7. application, server S/W 최신 버전
8. 보안 서약서
9. 저작권

### 1. 정보에 대한 보안 관리

- 사업 과정에서 생산된 모든 산출물에 대한 데이터 식별 및 보안 통제
- 모든 산출물에 대한 저장/보관 및 암호화 등 데이터에 대한 보안 통제
- 모든 산출물은 지정된 보안 책임자가 인가하지 않은 비인가자에게 제공/대여/열람 등을 금지
- 산출물 관련 정보 유출 사고 발생 시에 대비한 관리 방안

### 2. 물리적 보안 관리

- 참여 업체 공간에 대한 물리적 통제 및 출입 이력 관리
- 참여 인력이 반출입하는 PC 등의 장치 및 다양한 저장매체(USB, CD/DVD 등)에 대한 통제

### 3. 내/외부망 접근에 대한 보안

- 사업 참여 전산망에서 웹메일, 클라우드 파일 공유, P2P 등 데이터 유출 가능한 인터넷 사용 통제
- 내부 시스템 접근 필요 시 필요 인력 별 계정 생성 및 로그인/작업 이력 등 로깅

### 4. 산출물 소스코드 감사 및 관리

- 보안 취약점이 존재하는지 확인하기 위해 당사에서 코드 감사를 정기 및 비정기로 요청 가능
- 사업 참여 담당자는 코드 감사에 협조해야 하며 문제점이 발견될 시 신속히 조치할 책임이 있음
- 코드 감사자는 당사직원이 될 수도 있으며, 필요할 경우 제 3의 업체를 통해 진행 가능함

### 5. 실서비스 환경에 준하는 테스트 환경 제공

- 실서비스 환경에서는 적극적인 모의 해킹을 할 수 없는 민감한 영역의 서비스 구간이 존재할 수 있음
- 실서비스 환경과 동일하거나 그에 준하는 수준의 스테이징 환경을 구성하여, 당사직원 혹은 제3의 모의 해커가 실전과 유사하게 모의해킹 업무를 수행할 수 있도록 지원 필요

### 6. 사업 참여자 PC 최신 소프트웨어 버전 유지

- 사업에 참가하는 모든 관계자의 컴퓨터에 설치된 소프트웨어들은 (운영체제, 웹 브라우저 등 기타 주요 소프트웨어) 항상 최신 버전으로 유지하여야 함
- 특별한 사유가 있어서 구버전을 사용해야 경우, 당사 담당자와 사전 협의 필요

### 7. 개발 산출물 관련 소프트웨어 최신 버전 유지

- 참여 업체는 오픈소스 등 외부 리소스를 활용하여 개발할 경우 최신 버전으로 개발해야 함
- 참여 업체는 향후 시스템 유지 시에도 보안 취약점이 발생하였을 때 신속한 패치가 이루어질 수 있는 체계를 만들어야 함
- 특히, 웹 서버 등 외부에 직접적으로 노출되는 소프트웨어일 경우, dependency 등의 이슈 없이 최신 패치가 즉시 적용될 수 있는 구조여야 함
- 또한 업데이트 체계는 중간자 공격(MITM)으로부터 안전하도록 공개키 기반 등의 인증 방식을 가져야 함

### 8. 사업 참여 인력에 대한 보안 관리 대책 제시

- 보안 서약서 제출

### 9. 저작권 관리 대책 제시

- 사업 과정에서 필요한 기술 및 장비 등을 적용함에 있어 저작권을 침해하지 않아야 함
- 관련 저작권 침해 발생 시에 제안에 제시한 내용과 다름으로 인해 발생한 법률적 책임은 제안사가 부담함