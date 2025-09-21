# AMBA-BUS
 **AMBA**(Adavanced Microcontroller Bus Architecture): ARM에서 개발한 버스 protocol
 * 버스(Bus)
   : Chip의 여러 block들이 데이터를 주고 받는 통로

 ---
## 1. 버스가 필요한 이유
   - IP 블록 간 통신 경로 단일화 -> 여러 블록 간 연결 복잡도를 줄이고, 확장성 확보
   - Protocol 규칙 필요 -> **주소/데이터/제어 신호**를 어떤 순서로, **어떤 타이밍**에 보낼지 약속

## 2. 속도/성능에 따른 분리 설계

   <img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/8463a4e2-f2a2-4ef3-a947-ce71ee9de13f" />
   
   출처: https://www.arm.com/architecture/system-architectures/amba
  
   - APB : 저속 peripheeral 제어 등 단순 제어용 (UART, GPIO, Timer...)  
   - AHB : APB보다 고성능이 필요한 장치용
   - AXI : AHB보다 더 high performance, high frequency system용
   - 느린 모듈을 고속 버스에 바로 붙이면 전체 시스템 성능이 떨어짐 -> Bridge 설계 필요

## 3. 신호 정의
   - 성능이 높은 버스일 수록 신호가 많아지고 복잡함
        - Address Data, Read/Write Control, Handshake(Ready/Vaild) 등
   - APB는 최소한의 신호로 동작 (PADDR, PWRITE, PSEL, PENABLE, PREADY, PWDATA, PRDATA)

## 4. 동작 원리 (Transfer 단계)
**(1) 버스 요청 & 중재 (Bus Request / Arbitration)**
- 여러 Master가 동시에 “나 데이터 보낼래!” 하고 버스 요청(Request) 신호를 올림.
- Arbiter가 우선순위(priority) 규칙에 따라 Grant 신호를 주어 한 Master만 버스 사용 가능.

**(2) 주소 단계 (Address Phase)**
- 선택된 Master가 Address Line에 원하는 주소를 올리고, Control Line에 Read/Write 신호를 셋팅.
- 이걸 Slave들이 보고 자기 주소인지 디코드(decode)해서 반응할지 결정.

**(3) 데이터 단계 (Data Phase)**
- Read라면 Slave가 Data Line에 데이터 올리고,
- Write라면 Master가 Data Line에 데이터 올려 Slave가 받아감.
- 대부분의 프로토콜은 핸드셰이크(Handshake) 신호(예: VALID/READY, HREADY 등)를 써서 데이터가 제대로 전송됐는지 확인.

**(4) 응답 단계 (Response)**
- Slave가 “전송 성공” 또는 “에러” 응답을 보냄.
- AXI 같은 경우는 OKAY, SLVERR 같은 응답 코드까지 있음.

**(5) 버스 해제**
- Master가 버스를 놓고, 다음 요청 대기 중인 Master에게 Arbiter가 권한을 넘김.


---

##  - 버스 기본 구성요소

  - **Adress Line**
      - CPU가 데이터를 주고 받기 위해 접근할 메모리 주소 또는 I/O 장치의 주소를 지정할 때 사용되는 단방향 통로 , 주소 버스 폭 = 접근 가능한 최대 주소 공간
  - **Data Line**
      - 실제 데이터를 CPU, 메모리, I/O 장치 등 시스템 구성요소 간에 양방향으로 주고 받는 통로, 데이터 버스 폭 = 데이터의 크기
  - **Control Line**
      - 데이터 읽기/쓰기, 인터럽트, 클럭 등 시스템 각 요소의 동작을 제어하는 다양한 신호선, 양방향 통로

---


