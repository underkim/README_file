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
  |p|PID를 다음과 같이 모니터(-pN1 -pN2 ... or -pN1,N2[,...])|
  |s|보안 모드 작동|
  |S|누적 시간 모드 토글|
  |u|사용자별 모니터링(u somebody)|
  |U|사용자별 모니터링(U somebody)|
  |숫자 1|CPU Core별로 사용량을 보여줌|
  
+ ps와 top의 차이점
  + ps는 ps한 시점에 proc에서 검색한 cpu 사용량
  + top은 proc에서 일정 주기로 합산해 cpu 사용율 출력

 __`top -b -n 1`__
![image](https://user-images.githubusercontent.com/51310308/171113804-af0b9027-aebd-4a33-8ae9-8deb5bfb2758.png)

  + 3:58 : 3시간 58분 전에 서버가 구동
  + load average : 현재 시스템이 얼마나 일을 하는지를 나타냄. 3개의 숫자는 1분, 5분, 15분 간의 평균 실행/대기 중인 프로세스의 수. CPU 코어수 보다 적으면 문제 없음
  + Tasks : 프로세스 개수
  + KiB Mem, Swap : 각 메모리의 사용량
  + PR : 실행 우선순위
  + VIRT, RES, SHR : 메모리 사용량 => 누수 check 가능
  + S : 프로세스 상태(작업중, I/O 대기, 유휴 상태 등) 


----------------
### 2. ps
**현재 실행중인 프로세스 목록과 상태를 보여주는 명령어**

|옵션|설명|
|:--:|:---:|
|-A|모든 프로세스를 출력|
|a(BSD계열)|터미널과 연관된 프로세스를 출력|
|-a|세션 리더를 제외하고 데몬프로세스처럼 터미널에 종속되지 않은 모든 프로세스를 출력|
|-e|커널 프로세스를 제외한 모든 프로세스를 출력|
|-f|풀 포맷으로 보여줌|
|-l(sys V), l(BSD계열)|긴 포맷으로 보여줌|
|-o 값|출력 포맷을 지정하는 옵션(값으로 PID,tty 등을 지정)|
|-M|64비트 프로세스들을 보여줌|
|-m|프로세스들 뿐만 아니라 커널 스레드들도 보여줌|
|-p|특정 PID를 지정할때 사용|
|-r|현재 실행 중인 프로세서를 보여줌|
|u(BSD계열)|프로세스의 소유자를 기준으로 출력|
|-u|특정 사용자의 프로세스 정보를 확인할 때 사용|
|x(BSD계열)|데몬 프로세스처럼 터미널에 종속되지 않는 프로세스 출력|
|-x|로그인 상태에 있는 동안 아직 완료되지 않은 프로세서들을 보여줌|

__`ps -ef`__


![image](https://user-images.githubusercontent.com/51310308/171796426-803f7d56-9f1e-4700-a834-b4a50a299689.png)


__`ps aux`__


![image](https://user-images.githubusercontent.com/51310308/171796780-ed49863e-d6bd-4e05-8596-5a22133f082c.png)

 + PID : 프로세스 ID입니다.
 + TTY : 프로세스의 제어 터미널 이름입니다.
 + TIME : 프로세스의 누적 CPU 시간(분 및 초)입니다.
 + CMD : 프로세스를 시작하는 데 사용된 명령의 이름입니다.
 + UID : 프로세스를 실행하는 사용자인 USER와 동일합니다.
 + PPID : 상위 프로세스의 ID입니다.
 + C : %CPU와 동일, 프로세스 CPU 활용도입니다.
 + STIME : 명령이 시작된 시간인 START와 동일합니다.
 + USER : 프로세스를 실행하는 사용자입니다.
 + %CPU : 프로세스의 CPU 사용률입니다.
 + %MEM : 시스템의 물리적 메모리에 대한 프로세스 상주 설정 크기의 백분율입니다.
 + VSZ : KiB에 있는 프로세스의 가상 메모리 크기입니다.
 + RSS : 프로세스가 사용 중인 실제 메모리의 크기입니다.
 + STAT : Z(줌비), S(절전) 및 R(실행)과 같은 프로세스 상태 코드입니다.
 + START : 명령이 시작된 시간입니다.


-----------------------
### 3. jobs
**작업의 상태를 표시하는 명령어**


|옵션|설명|
|:--:|:--:|
|-l|프로세스 그룹 ID를 state 필드 앞에 출력|
|-n|프로세스 그룹 중에 대표 프로세스 ID를 출력|
|-p|각 프로세스 ID에 대해 한 행씩 출력|
|command|지정한 명령어를 실행|


__`jobs`__


![image](https://user-images.githubusercontent.com/51310308/171798127-3e2236c1-bc6d-4017-8c2a-23c30c8d8dd5.png)


|상태|설명|
|:--:|:--:|
|Running|작업이 일시 중단되지 않았고 종료하지 않고 계속 진행 중임|
|Done| 작업이 완료되어 0을 반환하고 종료 했음을 의미|
|Done(code)|작업이 정삭적으로 완료되었으며, 0이 아닌 코드를 반환 했음을 의미|
|Stopped|작업이 일시 중단|
|Stopped(SIGTSTP)|SIGTSTP 신호가 작업을 일시 중단|
|Stopped(SIGSTOP)|SIGSTOP 신호가 작업을 일시 중단|
|Stopped(SIGTTIN)|SIGTTIN 신호가 작업을 일시 중단|
|Stopped(SIGTTOU)|SIGTTOU 신호가 작업을 일시 중단|


*********
### 4. kill
**프로세스에 시그널을 보내는 명령어**
+ 기본동작이 프로그램 종료
+ kill [옵션 or 시그널] PID

__`kill -l`__


![image](https://user-images.githubusercontent.com/51310308/171799411-9486cc15-4077-4b5f-8fdf-2d8c703eaa58.png)

__`kill -9 PID`__


![image](https://user-images.githubusercontent.com/51310308/171808014-91b242c3-55b7-4369-ba74-5fc0a64a421e.png)


***
### 5. 매크로
