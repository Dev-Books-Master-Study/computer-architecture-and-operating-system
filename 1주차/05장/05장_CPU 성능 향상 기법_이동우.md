# Chapter05 CPU 성능 향상 기법

- 5-1 빠른 CPU를 위한 설계 기법
- 5-2 명령어 병렬 처리 기법
- 5-3 CISC & RISC
<br><br>
## 5-1 빠른 CPU를 위한 설계 기법

- 클럭
- 코어와 멀티코어
- 스레드와 멀티스레드

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

### 스레드와 멀티스레드
<br>

**스레드**

- 실행 흐름의 단위 , 독립적으로 진행되는 최소 논리적 흐름의 단위
- cpu에서 사용되는 **하드웨어적 스레드** & 프로그램에서 사용되는 **소프트웨어적 스레드**가 있음

![hwsw](https://github.com/dongwooooooo/computer-architecture-and-operating-system/assets/137749703/0e53dd81-8540-4793-b88f-fce5cdd02922)


**하드웨어적 스레드**

- ‘하나의 **코어**가 동시에 처리하는 명령어의 단위’, CPU에서 사용되는 스레드를 뜻함.

**멀티스레드 프로세서** 또는 **멀티스레드 CPU**

- 하나의 코어로 여러 명령어(여러 스레드를 이용)를 동시에 처리하는 CPU
    - 대표적으로 intel의  하이퍼스레딩
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

- 멀티스레드 프로세서
    
    싱글 코어 싱글 스레드
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c8ed0d2f-d253-4da7-8436-940629ab0276/Untitled.png)
    
    듀얼코어 4스레드(하이퍼 스레딩)
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a870aaed-e0e4-4761-834f-71bc4f87c520/Untitled.png)
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a7fbd78d-0cfd-4141-accb-4f081b0d8bf5/Untitled.png)
    

- 2코어 4 스레드 cpu는 한 번에 네 개의 명령어를 처리 가능하여 쿼드 코어 스케줄링을 함.
- 그래서 하드웨어 스레드를 논리 프로세서라고 부르기도 함.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7cfc5d40-776f-458f-bf93-7abff468e144/Untitled.png)

레지스터 세트 : 프로그램 카운터, 스택 포인터, 데이터 버퍼 레지스터, 데이터 주소 레지스터 등

## 5-2 명령어 병렬 처리기법

클럭속도를 과하게 높이면 발열문제 발생.

cpu를 어떻게 극한으로 짜낼까?

---

### **명령어 파이프라인**

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

- 명령어 파이프라인을 사용하지 않으면

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e74a76bc-dc7c-4264-9e9f-5291f29b0555/Untitled.png)

- 명령어 파이프라인을 사용하면
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1bfe2739-6814-41e6-9198-d473b2bf1512/Untitled.png)
    
    - 명령어 파이프라인을 사용하면 적은 시간동안 더 많은 작업량을 처리할 수 있음.
        - 파이프라인을 처리하는 도중 문제가 생기면 전체 연산과정에 문제가 생길 수 있음.
        - 각기 다른 메모리 주소를 사용.
    
    ### 파이프라인 위험
    

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/16aac26d-15da-4a19-8a07-4b52bfc4ab1e/Untitled.png)

1. 데이터 위험 
    - ‘데이터 의존성’에 의해 발생.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/99df8bce-05d4-4440-bd60-4fed72dae205/Untitled.png)
    
2. 제어 위험
    - 분기 등으로 ‘프로그램 카운터의 갑작스러운 변화’에 의해 발생.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/51c971e0-86b3-4218-9dcf-2a3d18bd3583/Untitled.png)
    
3. 구조적 위험
    - 서로 다른 명령어가 동시에 ALU, 레지스터 등 CPU부품 또는 메모리를 사용하려고 할 때,
    - 하드웨어가 병행 수행을 지원하지 않는 경우 자원 충돌이 발생.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ee0346be-343d-4e4f-8816-f3fbab5385be/Untitled.png)
    

### 슈퍼스칼라

- 여러 개의 파이프라인 이용.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f6077b86-f415-463f-9f48-6c147096a9e2/Untitled.png)

### 비순차적 명령어 처리

> OoOE: Out-of-order execution
> 

파이프라인의 중단을 방지하기 위해 명령어를 순차적으로 처리하지 않는 명령어 병렬 처리 기법

= ‘합법적 새치기‘

- 데이터 위험 같이 데이터간의 의존성이 있는 경우
- 순서를 바꿔도 무방한 명령어를 먼저 실행
- 처리가 끝나면 새치기

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e22297be-157e-4401-aa2a-ce3ab3bff12f/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/70dbfc9e-0d68-443c-b75d-bbb540dbdb87/Untitled.png)

## 5-3 CISC & RISC

파이프라이닝 하기 쉬운 명령어?

---

### ISA(Instruction Set)

- 명령어 집합 또는 명령어 집합 구조
- 일종의 CPU언어
- CPU마다 ISA가 다를 수 있음
    - Intel CPU : x86, x84-64 ISA
    - Apple CPU : ARM ISA

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/869e8f81-b179-45d4-9f48-a148bf172f9c/Untitled.png)

- ISA가 다르면 명령어가 다름.
    - 제어장치가 명령어를 해석하는 방식
    - 사용되는 레지스터의 개수, 종류
    - 메모리 관리 방식
    - 실행파일도 명령어로 이루어져 있음
        
        같은 소스 코드로 이루어진 프로그램이라도 ISA가 다르면 
        
        CPU가 이해할 수 있는 명령어도 달라지고 어셈블리어도 달라짐.
        

### CISC

> Complex Instruction Set Computer
> 

ex) Intel x-86, x86-64

**가변 길이 명령어**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3f16a0a8-2470-4564-ba4c-0c79b3d561e2/Untitled.png)

- 명령어의 형태와 길이가 다양함.
    - 상대적으로 적은 명령어로도 프로그램을 실행 = 메모리 공간을 절약
- 적은 명령어로 프로그램 실행 = 명령어가 복잡 = 크기와 실행되는 시간이 일정하지 않음
- 즉 명령어 하나를 실행하는데 여러 클럭주기가 필요
- 다양한 명령어가 있지만 주로 사용되는 명령어는 일부분
    
    ⇒ 파이프라인을 만들기 어렵다.
    

### RISC

1. 일정한 명령어 길이
2. 적은 명령어의 종류
3. 메모리 접근을 단순화
    1. 메모리를 직접 접근하는 명령어를 load, store 두 개로 제한

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/432f4a51-a0e5-487d-8cae-608872d002c9/Untitled.png)

- 대신 레지스터를 적극적으로 활용
    - CISC보다 레지스터 이용이 많고 범용 레지스터의 개수도 많다.
- 명령어가 단순한만큼 프로그램에 실행되는 명령어의 개수가 많다.
