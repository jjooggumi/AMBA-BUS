# AMBA-BUS
 **AMBA**(Adavanced Microcontroller Bus Architecture): ARM에서 개발한 버스 protocol
 * 버스(Bus)
   : Chip의 모듈 간의 신호를 주고 받는 통로
 
 * 버스 종류
   
   <img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/8463a4e2-f2a2-4ef3-a947-ce71ee9de13f" />

    출처: https://www.arm.com/architecture/system-architectures/amba
   
   : 여러가지 종류가 있지만 대부분 APB, AHB, AXI 버스를 주로 사용
   : 모듈마다 동작속도가 다르기에, 비슷한 속도(clk)를 가진 모듈끼리 같은 버스에 연결해 시스템 동작을 최적화 시킴
   - APB : 저속 peripheeral 제어 등 단순 제어용 (UART, GPIO, ...)  
   - AHB : APB보다 고성능이 필요한 장치용
   - AXI : AHB보다 더 high performance, high frequency system용
   

---
참고: https://rtlearner.com/amba-apb-bus/?utm_source=chatgpt.com
