# ALU와 제어장치

## ALU(arithmetic and logical unit)란?

<aside>
💡 덧셈, 뺄셈 같은 두 숫자의 산술연산과 배타적 논리합, 논리곱, 논리합 같은 논리연산을 계산하는 
디지털 회로

레지스터, 제어장치로부터 받아들인 피연산자와 제어신호를 산술연산, 논리 연산 등 다양한 연산을 수행한다

</aside>

### ALU의 작업수행 과정
![ALU_process](https://github.com/yoojaeyoonGit/computer-architecture-and-operating-system/assets/110767749/7ce68901-bfa9-41bc-92c3-984eb55f4c69)



**연산 필요사항** 

- ALU는 레지스터를 통해 피연산자
- 제어 장치로 부터 수행할 연산을 알려주는 제어 신호

<br>

결괏값

- 일반 결괏값과 플래그를 결괏값으로 내보낸다.

### 플래그

ALU 계산 결과에 추가적인 정보를 전달

![flag](https://github.com/yoojaeyoonGit/computer-architecture-and-operating-system/assets/110767749/5bc41039-4572-4d91-acbf-e39794eb71d3)

ALU가 연산을 수행하고 결괏값에 따라 부호 플래그가 1이라면 연산결과는 음수 <br>
<img width="401" alt="flag1" src="https://github.com/yoojaeyoonGit/computer-architecture-and-operating-system/assets/110767749/363727ac-0969-4c17-992c-38f97fd311a2">

ALU가 연산을 수행하고 결괏값에 따라 제로 플래그가 0이라면 연산결과는 0 <br>
<img width="401" alt="flag2" src="https://github.com/yoojaeyoonGit/computer-architecture-and-operating-system/assets/110767749/6cbe33ab-383c-44b6-8b86-75eb90f96f13">



> ALU를 통한 연산은 모두 레지스터에 저장된다. <br>
CPU가 메모리에 접근하는 시간을 줄일 수 있기 때문이다.
> 

<br>
<br>

## 제어장치(control unit, CU)란?

<aside>
💡 <strong>제어장치</strong>는 주기억 장치에 저장되어 있는 명령어(프로그램)을 순서대로 호출하여 해독한 후, <br>
<strong>제어 신호</strong>(컴퓨터 부품을 관리, 작동시키는 일종의 전기 신호)를 발생시켜 
컴퓨터의 각 장치를 동작하도록 하는 장치

</aside>

<br>
<br>

![control_unit process](https://github.com/yoojaeyoonGit/computer-architecture-and-operating-system/assets/110767749/0e2b260c-1f1c-4728-bd5e-0e3eaad2bc54)

### 제어 장치가 받아들이는 정보

1. 클럭신호
    - 클럭이란 컴퓨터 모든 부품을 움직일 수 있게 하는 시간 단위이다. 
    주의 해야 할 점은 클럭이라는 박자에 맞춰 작동할 뿐 명령 하나가 한 클럭마다 작동완료 되는 것이 아니라 여러 클럭에 걸쳐 실행된다.
    
2. 해석해야 할 명령어 
    - CPU가 해석해야할 명령어는 명령어 레지스터에 저장된다. 
    제어장치는 명령어 레지스터에서 해석할 명령어를 받아들이고 해석한 뒤 제어 신호를 발생 시킨다.

1. 플래그 레지스터의 플래그 값
    - 제어 장치는 연산결과의 추가적인 상태 정보인 플래그를 고려하여 제어신호를 발생시킨다.

1. 시스템 버스 중 제어버스로 전달된 제어신호
    - 제어버스를 통해 외부로부터 전달된 제어 신호를 받아들이기도 한다.
      
<br>

### 제어 장치가 내보내는 정보

**CPU 외부에 전달하는 제어 신호**

- 메모리에 전달하는 제어 신호
- 입출력장치에 전달하는 제어 신호

<br>

**CPU 내부에 전달하는 제어 신호**

- ALU에 전달하는 제어신호
    - 수행할 연산을 지시
- 레지스터에 전달하는 제어 신호
    - 레지스터 간에 데이터를 이동시키거나 레지스터에 저장된 명령어를 해석하는 작업

---

# 레지스터

## 레지스터란?

<aside>
💡 <strong>CPU(Central Processing Unit)가 요청을 처리하는 데 필요한 데이터를 일시적으로 저장하는 기억장치이다.</strong>

</aside>
<br>
<br>

![register](https://github.com/yoojaeyoonGit/computer-architecture-and-operating-system/assets/110767749/c1cbb2f9-e861-41c6-af2d-3a0fd0593773)

Register 데이터 이동 패턴

## 알아야할 주요 레지스터

### 프로그램 카운터

- 메모리에서 가져올 (다음 번에 실행할) 명령어 주소를 저장하는 레지스터

### 명령어 레지스터

- 메모리에서 읽어 들인 (현재 실행 중인) 명령어를 저장하는 레지스터

### 메모리 주소 레지스터

- 메모리의 (데이터의) 주소를 저장하는 레지스터

### 메모리 버퍼 레지스터

- 메모리와 주고받을 값을 저장하는 레지스터
    - 메모리에 쓰고 싶은 값과 메모리로부터 전달 받은 값이 메모리 버퍼 레지스터를 거친다.
<br>

![register_process](https://github.com/yoojaeyoonGit/computer-architecture-and-operating-system/assets/110767749/36ef3011-56d3-4b28-a680-6f5c41d01183)

### 범용 레지스터

- 메모리 버퍼 레지스터는 데이터 버스로 주고받은 값만 저장하고, 메모리 주소 레지스터는 주소 버스로 내보낼 주소값만 저장하지만 범용 레지스터는 데이터와 주소를 모두 저장한다.

### 플래그 레지스터

- 플래그 레지스터 연산 결과 또는 CPU 상태에 대한 부가적인 정보를 저장하는 레지스터

### 주소 지정 방식 (스택 주소 지정 방식, 변위 주소 지정 방식)

- <strong>“스택 주소 지정 방식”</strong>이라는 주소 지정 방식에는 스택 포인터를 사용
- <strong>“변위 주소 지정 방식”</strong>이라는 주소 지정 방식에는 프로그램 카운터와 베이스 레지스터 사용

<details>
  <summary> <h3>스택 주소 지정 방식</h3> </summary>

### - **스택 주소 지정 방식**

스택과 스택 포인터를 이용한 주소 지정 방식.


**스택과 스택 포인터**

- **스택**은 흔히 알고있는 LIFO 형식의 저장공간
- **스택 포인터**는 스택에 마지막으로 저장한 값의 위치를 저장하는 레지스터
![stack_pointer](https://github.com/yoojaeyoonGit/computer-architecture-and-operating-system/assets/110767749/2d3b23aa-7eca-482f-9a69-66d7e8463369)



스택은 메모리 안에 존재한다. 이 곳을 <strong>“스택영역”</strong>이라고 한다.

</details>

<details>
  <summary><h3>변위 주소 지정 방식</h3></summary>
  

오퍼랜드 필드의 값(변위)과  특정 레지스터 값을 더하여 유효 주소를 얻어내는 주소 지정 방식

![displacement-addressing-mode.webp](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/62574191-46f6-4d1b-aa8c-89822026bc5f/displacement-addressing-mode.webp)

변위 주소 지정 방식은 오퍼랜드 필드의 주소와 어떤 레지스터를 더하는지에 따라 **상대 주소 지정 방식, 베이스 레지스터 주소 지정 방식** 등으로 나뉜다.

### 상대 주소 지정 방식

오퍼랜드와 프로그램 카운터의 값을 더하여 유효 주소를 얻는 방식
![PCRelativeMode1](https://github.com/yoojaeyoonGit/computer-architecture-and-operating-system/assets/110767749/20c267ae-547a-4071-ae23-2500d32d6292)

프로그램 카운터에는 PC  읽어들일 명령어의 주소가 저장되어 있다. 오퍼랜드의 수에 따라 CPU는 읽기로한 명령어로부터 오퍼랜드 수만큼 더한 번지의 명령어를 실행한다.

상대 주소 지정 방식은 if문과 유사하게 특정 주소의 코드를 실행할 때 사용한다.

### 베이스 레지스터 주소 지정 방식

오퍼랜드와 베이스 레지스터의 값을 더하여 유효 주소를 얻는 방식
![base_register2](https://github.com/yoojaeyoonGit/computer-architecture-and-operating-system/assets/110767749/1c1fa94c-0e3b-49aa-819a-94976d097163)

**오퍼랜드와 베이스 레지스터**

- 베이스 레지스터는 기존 주소
- 오퍼랜드는 기준 주소로부터 떨어진 거리

정리하자면 베이스 레지스터 주소 지정 방식은 베이스 레지스터 속 기준 주소로부터 얼마나 떨어져 있는 주소에 접근할 것인지를 연산하여 유효 주소를 얻어내는 방식이다.

</details>

---

# 명령어 사이클과 인터럽트

## 명령어  사이클이란?

<aside>
💡 하나의 명령어를 처리하는 정형화된 흐름

</aside>
<br>
<br>
<img width="536" alt="instruction_cycle" src="https://github.com/yoojaeyoonGit/computer-architecture-and-operating-system/assets/110767749/b58bf537-cd72-447a-a225-4ec8f5e4fa5f">

### 인출 사이클 (fetch cycle)

- 메모리에 있는 명령어를 CPU로 가져오는 단계

### 실행 사이클 (execution cycle)

- 제어장치가 명령어 레지스터에 담긴 값을 해석, 제어신호를 발생시키는 단계

### 간접 사이클 (indirect cycle)

- 간접 주소 지정 방식으로 명령어를 가져왔다면 바로 실행이 불가하고 메모리 접근을 한번 더 해야 실행이 가능하다. 이 단계를 간접 사이클이라고 부른다. <br>
![indirect__2](https://github.com/yoojaeyoonGit/computer-architecture-and-operating-system/assets/110767749/e3c55b54-e78f-4e85-9eeb-438ac9aa2095)

<br>
<br>

## 인터럽트란?

<aside>
💡 CPU에서 정해진 흐름에 따라 명령어를 처리하는 도중 흐름이 끊어지는 상황

</aside>

### 인터럽트 종류

<details><summary><h3>동기 인터럽트</h3></summary>


CPU에 의해 발생한 인터럽트

- CPU가 명령어를 수행하는 과정에서 프로그래밍상 오류같은 예외적 상황에서 발생하는 인터럽트
  <strong>“예외”</strong> 라고도 표현함
    
</details>

<details><summary><h3>비동기 인터럽트</h3></summary>



입출력 장치에 의해 발생하는 인터럽트

- 하드웨어 장치가 특정 입력을 받았을 때 CPU에 보내는 인터럽트
    
    <strong>“인터럽트”</strong>라고 표현함
    


<details><summary><h3>하드웨어 인터럽트 처리 순서</h3></summary>


1. 입출력장치는 CPU에 **인터럽트 요청 신호**를 보냄.
2. CPU는 실행 사이클이 끝나고 명령어를 인출하기 전 항상 인터럽트 여부를 확인함.
3. CPU는 인터럽트 요청을 확인하고 **인터럽트 플래그**를 통해 현재 인터럽트를 받아들일 수 있는지 확인함
4. 인터럽트를 받아들일 수 있다면 CPU는 지금까지의 작업을 백업함
5. CPU는 **인터럽트 백터**를 참조하여 **인터럽트 서비스 루틴**을 실행함
6. 인터럽스 서비스 루틴 실행이 끝나면 (4)에서 백업해 둔 작업을 복구하여 실행을 재개함.


</details>


**인터럽트 요청 신호**

- 컴퓨터 시스템의 하드웨어나 소프트웨어에서 중앙 처리 장치(CPU)에 특정 사건이나 조건에 대한 처리가 필요함을 알리는 신호
- CPU가 인터럽트 요청 신호를 수용하기 위해 인터럽트 플래그가 활성화 되어 있어야한다.

**인터럽트 플래그**

- CPU가 하드웨어 인터럽트를 받아들일지 거부할 지 결정하는 플래그
    
    CPU가 처리중인 작업의 중요도에 따라 플래그를 설정한다.
    
    가장 먼저 처리해야 하는 하드웨어 인터럽트는 무시할 수 없다 (정전, 하드웨어 고장 등) <br>
    ![interrupt-hard](https://github.com/yoojaeyoonGit/computer-architecture-and-operating-system/assets/110767749/066732a9-ab1e-4c36-9f44-30dc79ba9824)
    

**인터럽트 서비스 루틴**

- 인터럽트를 어떻게 처리하고 작동해야 할지에 대한 정보로 이루어진 프로그램
    
    <strong>“인터럽트 핸들러”</strong>라고도 함
    

**인터럽트 백터**

- 수 많은 인터럽트 서비스 루틴을 식별하기 위한 정보
    - 서비스 루틴 수행 중 인터럽트 서비스 루틴이 실행 중에 인터럽트가 발생하면 인터럽트 백터를 참조하여 인터럽트 서비스 루틴의 주소를 알아내고 실행한다.<br>
![interrupt_service_routine2](https://github.com/yoojaeyoonGit/computer-architecture-and-operating-system/assets/110767749/5869c6ca-c870-490d-9c18-315df60714ac)


> 인터럽트가 발생하기 전 서비스 루틴 과정에서 
레지스터에 저장되어 있던 값들은?
> 

인터럽트 서비스 루틴 실행 전에 해당 작업 내역들을 모두 **스택에 백업** 시키고 돌아와서 다시 실행한다. <br>

<br>
<br>
</details>

<br>
<br>

<h3>전체 명령어 사이클</h3>
<img width="671" alt="ㅇㅇㅇㅇㅇ" src="https://github.com/yoojaeyoonGit/computer-architecture-and-operating-system/assets/110767749/0b94ac4a-cce8-427d-93b9-f3fe078890a4">

