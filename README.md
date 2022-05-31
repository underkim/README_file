# top, ps, jobs, kill 명령어와 vim 매크로



---

### 1. top
+ 시스템의 상태를 전반적으로 가장 빠르게 파악 가능(CPU, Memory, Process)
+ 옵션 없이 입력하면 interval 간격(기본 3초)으로 화면을 갱신하며 정보를 보여줌
+ top 실행 전 옵션
   + 순간의 정보를 확인하려면 -b 옵션 추가(batch 모드)
   + -n : top 실행 주기 설정(반복 횟수)
+ top 실행 후 명령어
  + shift + p : CPU 사용률 내림차순
  + shit + m : 메모리 사용률 내림차순
  + shift + t : 프로세스가 돌아가고 있는 시간 순
  + k : kill. k 입력 후 PID 번호 작성. signal은 9
  + f : sort field 선택 화면 -> q 누르면 RES순으로 정렬
  + a : 메모리 사용량에 따라 정렬
  + b : Batch 모드로 작동
  + 1 : CPU Core별로 사용량 보여줌
+ ps와 top의 차이점
  + ps는 ps한 시점에 proc에서 검색한 cpu 사용량
  + top은 proc에서 일정 주기로 합산해 cpu 사용율 출력

* top -b -n 1 
![image](https://user-images.githubusercontent.com/51310308/171113804-af0b9027-aebd-4a33-8ae9-8deb5bfb2758.png)

  + 3:58 : 3시간 58분 전에 서버가 구동
  + load average : 현재 시스템이 얼마나 일을 하는지를 나타냄. 3개의 숫자는 1분, 5분, 15분 간의 평균 실행/대기 중인 프로세스의 수. CPU 코어수 보다 적으면 문제 없음
  + Tasks : 프로세스 개수
  + KiB Mem, Swap : 각 메모리의 사용량
  + PR : 실행 우선순위
  + VIRT, RES, SHR : 메모리 사용량 => 누수 check 가능
  + S : 프로세스 상태(작업중, I/O 대기, 유휴 상태 등)
