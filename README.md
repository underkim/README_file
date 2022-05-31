# top, ps, jobs, kill 명령어와 vim 매크로



---

### 1. top
**실시간으로 CPU 사용률 체크를 해주는 명령어**
+ 시스템의 상태를 전반적으로 가장 빠르게 파악 가능(CPU, Memory, Process)
+ 옵션 없이 입력하면 interval 간격(기본 3초)으로 화면을 갱신하며 정보를 보여줌
  
  **top 옵션**
  |옵션|설명|
  |:------:|:----------:|
  |-b|배치모드 옵션(실행 전 옵션)|
  |-n|top 실행 주기를 설정(실행 전 옵션)|
  |shift + p|CPU 사용률 내림차순|
  |shit + m|메모리 사용률 내림차순|
  |shift + t|프로세스가 돌아가고 있는 시간 순|
  |k|kill. k 입력 후 PID 번호 작성. signal은 9|
  |f|sort field 선택 화면 -> q 누르면 RES순으로 정렬|
  |a|메모리 사용량에 따라 정렬|
  |b|Batch 모드로 작동|
  |c|명령행/프로그램 이름 토글|
  |d|지연 시간 간격은 다음과 같다. -d ss. tt(seconds.tenths)|
  |h|도움말|
  |H|스레드 토글|
  |i|유휴 프로세스 토글|
  |m|VIRT/USED  토글|
  |M|메모리 유닛 탐지|
  |n|반복 횟수 제한(-n number)|
  |p|PID를 다음과 같이 모니터(-pN1 -pN2 ... or -pN1,N2[,...]|
  |s|보안 모드 작동|
  |S|누적 시간 모드 토글|
  |u|사용자별 모니터링(u somebody)|
  |U|사용자별 모니터링(U somebody)|
  |숫자 1|CPU Core별로 사용량을 보여줌|
  
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


### 2. ps
**현재 실행중인 프로세스 목록과 상태를 보여주는 명령어**
