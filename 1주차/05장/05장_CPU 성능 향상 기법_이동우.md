# Chapter05 CPU 성능 향상 기법

- 5-1 빠른 CPU를 위한 설계 기법
- 5-2 명령어 병렬 처리 기법
- 5-3 CISC & RISC
<br><br>
## 5-1 빠른 CPU를 위한 설계 기법

- 클럭
- 코어와 멀티코어
- 스레드와 멀티스레드

---

### 클럭 

1. 컴퓨터 부품은 ‘클럭 신호’에 맞춰 일처리
2. CPU는 ‘명령어 사이클’이라는 정해진 흐름에 맞춰 명령어를 실행.
<br>

**클럭속도**

- 클럭 신호가 빠르게 반복 = 클럭 속도가 빠르다.
- 초당 몇 번 반복, 헤르츠 단위
- 클럭 속도가 높아지면 CPU의 성능향상이 있다. (오버클럭킹: 최대 클럭 속도를 강제로 더 끌어올리는 것)
- 클럭 속도가 높을 수록 발열이 심해져서 성능 향상에 한계가 있음. 또한 클럭은 항상 일정하지 않음.
  
---
<br>

### 코어와 멀티 코어
![Untitled](https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/44070ed4-4e6f-4f8d-80d5-cd61ed20ac9e)



- 과거엔 단일 cpu를 사용. 오늘날엔 코어가 명령어를 실행하는 부품이고 cpu에 포함.

<br>

**멀티코어 CPU** 또는 **멀티코어 프로세서** 

- 코어를 여러 개 포함하고 있는 CPU
- 일반적으로 멀티 코어의 처리속도가 단일 코어보다 빠름.
- 하지만 코어 수가 많다고 해도 처리할 연산과 명령어들을 분배하는 방식에 따라 연산 속도는 크게 달라짐.

---
<br>

### 스레드와 멀티스레드
<br>

**스레드**

- 실행 흐름의 단위 , 독립적으로 진행되는 최소 논리적 흐름의 단위
- cpu에서 사용되는 **하드웨어적 스레드** & 프로그램에서 사용되는 **소프트웨어적 스레드**가 있음

![hwsw](https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/0e53dd81-8540-4793-b88f-fce5cdd02922)

<br>

**하드웨어적 스레드**

- ‘하나의 **코어**가 동시에 처리하는 명령어의 단위’, CPU에서 사용되는 스레드를 뜻함.

<br>

**멀티스레드 프로세서** 또는 **멀티스레드 CPU**

- 하나의 코어로 여러 명령어(여러 스레드를 이용)를 동시에 처리하는 CPU
- 코어에 스레드만큼의 레지스터 세트를 가지고 있음
    - 대표적으로 intel의  하이퍼스레딩

|듀얼코어 4스레드 레지스터|
|--|
|<img width="418" alt="6" src="https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/2c8c1b3a-2ad4-4178-b7c5-e6989cefd0cb">|

<br>

**소프트웨어적 스레드**

- ‘하나의 **프로그램**에서 독립적으로 실행되는 단위’ , 프로그래밍 언어나 운영체제에 사용되는 스레드를 뜻함.




|![1](https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/0ee523e9-9c2d-4bf0-8124-ab8547d0843c)|![2](https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/dd7784a9-a918-4589-a14b-cd86fa1a454e)|
|--|--|

- 워드로 예를 들면
    1. 입력 받은 내용을 화면에 보여 주는 기능
    2. 맞춤법 맞는지 검사하는 기능
    3. 자동 저장 기능
    - 기능들을 작동시키는 코드를 각각의 스레드로 만들어 동시에 실행할 수 있음.
<br>

**멀티스레드 프로세서**

|싱글 코어 싱글 스레드|듀얼코어 4스레드(하이퍼 스레딩)|
|--|--|
|<img width="975" alt="3" src="https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/0fd89e77-f828-4192-a697-7917ed5ecfdb">|<img width="1052" alt="4" src="https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/27213744-211e-4942-b1e5-5b20f38da413">|

- 2코어 4 스레드 cpu는 한 번에 네 개의 명령어를 처리 가능하여 쿼드 코어 스케줄링을 함.
- 그래서 하드웨어 스레드를 논리 프로세서라고 부르기도 함.

|논리 프로세서|
|--|
|![5](https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/502023fd-0cb0-4e5c-a7c5-71b4af882955)|

---
<br>

## 5-2 명령어 병렬 처리기법
- 명령어 파이프라인
- 슈퍼스칼라
- 비순차적 명령어 처리

> 클럭속도를 과하게 높이면 발열문제 발생.
> cpu를 어떻게 극한으로 짜낼까? => 명령어 파이프라인

---
<br>

### 명령어 파이프라인

- 시간적 병렬 프로세서 구조
- 클럭 단위별 명령어 처리과정
    1. 명령어 인출 (Instruction Fetch)- 무조건 실행
        - 기억 장치로부터 명령어 읽기
    2. 명령어 해석 (Instruction Decode)-무조건 실행
        - 해당 명령어 해독
    3. 명령어 실행 (Execute Instruction)
    4. 결과 저장 (Write Back)
    - 책마다 과정을 나누는 기준이 판이하게 다름
    - 같은 단계가 겹치지만 않는 다면 cpu는 각 단계를 동시에 실행할 수 있음.
<br>

- 명령어 파이프라인 사용 X
<img width="584" alt="7" src="https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/ffdf6161-a191-46d9-a590-5fe5f10e8684">

- 명령어 파이프라인 사용 O

<img width="516" alt="8" src="https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/ee178141-2a8f-46cd-b789-d4862c5dc86f">
    
    
  - 명령어 파이프라인을 사용하면 적은 시간동안 더 많은 작업량을 처리할 수 있음.
    - 파이프라인을 처리하는 도중 문제가 생기면 전체 연산과정에 문제가 생길 수 있음.
    - 각기 다른 메모리 주소를 사용하여 메모리 사용량이 높아짐.
<br>
    
**파이프라인 위험**

<img width="314" alt="11" src="https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/f2500a97-e31e-4a52-9264-8e0cce7b96fb">

1. 데이터 위험 
    - ‘데이터 의존성’에 의해 발생.
    ![12](https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/a45dffbd-9a81-4214-a49b-db2f797c78ad)

2. 제어 위험
    - 분기 등으로 ‘프로그램 카운터의 갑작스러운 변화’에 의해 발생.
![13](https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/c6d7db99-f25c-4c9e-b70b-807b4a16269c)

    
3. 구조적 위험
    - 서로 다른 명령어가 동시에 ALU, 레지스터 등 CPU부품 또는 메모리를 사용하려고 할 때,
    - 하드웨어가 병행 수행을 지원하지 않는 경우 자원 충돌이 발생.
![14](https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/e11cca3b-797a-4c60-a139-66889082f23d)
    
---
<br>

### 슈퍼스칼라

- 여러 개의 파이프라인 이용.
![16](https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/da1ecded-ea99-4dfa-9370-cc96d2e722a1)

---
<br>

### 비순차적 명령어 처리

> OoOE: Out-of-order execution
> 파이프라인의 중단을 방지하기 위해 명령어를 순차적으로 처리하지 않는 명령어 병렬 처리 기법
**= ‘합법적 새치기‘**

- 데이터 위험 같이 데이터간의 의존성이 있는 경우
- 순서를 바꿔도 무방한 명령어를 먼저 실행
- 처리가 끝나면 새치기

|③은 ①,②에 데이터 의존|②까지 끝나고 ③진행|
|--|--|
|![16](https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/fc5ac737-bf63-45b2-9a1b-c7c4cb956635)|![17](https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/ef45bd37-9f98-4168-9a53-9ab2c442cba5)|

---
<br>

## 5-3 CISC & RISC
- ISA(Instruction Set)
- CISC
- RISC

> 파이프라이닝 하기 쉬운 명령어?

---
<br>

### ISA(Instruction Set)

- 명령어 집합 또는 명령어 집합 구조
- 일종의 CPU언어
- CPU마다 ISA가 다를 수 있음
    - Intel CPU : x86, x84-64 ISA
    - Apple CPU : ARM ISA

|x86-65, ARM의 ISA|
|--|
|![21](https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/41247b79-5c02-4550-aef4-fd95875c401f)|


- ISA가 다르면 명령어가 다름.
    - 제어장치가 명령어를 해석하는 방식
    - 사용되는 레지스터의 개수, 종류
    - 메모리 관리 방식
    - 실행파일도 명령어로 이루어져 있음
        
        같은 소스 코드로 이루어진 프로그램이라도 ISA가 다르면 
        
        CPU가 이해할 수 있는 명령어도 달라지고 어셈블리어도 달라짐.

---
<br>        

### CISC

> Complex Instruction Set Computer
> ex) Intel x-86, x86-64

**가변 길이 명령어**
![22](https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/e2ca5e47-6804-4e6e-97bd-6c681eb45835)


- 명령어의 형태와 길이가 다양함.
    - 상대적으로 적은 명령어로도 프로그램을 실행 = 메모리 공간을 절약
- 적은 명령어로 프로그램 실행 = 명령어가 복잡 = 크기와 실행되는 시간이 일정하지 않음
- 즉 명령어 하나를 실행하는데 여러 클럭주기가 필요
- 다양한 명령어가 있지만 주로 사용되는 명령어는 일부분
    
    ⇒ 파이프라인을 만들기 어렵다.

---
<br>    

### RISC

1. 일정한 명령어 길이
2. 적은 명령어의 종류
3. 메모리 접근을 단순화
    1. 메모리를 직접 접근하는 명령어를 load, store 두 개로 제한
<img width="261" alt="23" src="https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/361621e0-2495-4be1-8df0-d687d9910921">


- 대신 레지스터를 적극적으로 활용
    - CISC보다 레지스터 이용이 많고 범용 레지스터의 개수도 많다.
- 명령어가 단순한만큼 프로그램에 실행되는 명령어의 개수가 많다.
