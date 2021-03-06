# Top, Ps, Jobs, Kill 명령어, Vim에디터에서 매크로 사용방법
컴퓨터공학과 20205102 김재영
---

## Top

### 정의
Top 명령어는 현재 OS의 상태를 나타내주는 CLI 어플리케이션입니다.  
메모리 사용량, CPU 사용량 등을 나타내주며 top를 실행하는 동안에는 주기적인 업데이트로 실시간에 근접한 내용을 보여줍니다.

### 사용법 및 용어정리 

사용법: $ top  

![top](https://user-images.githubusercontent.com/106536020/172018001-71f76081-06d2-46a5-b7e4-a225bd1b1f67.PNG)


### 요약영역  
요약 영역은 top에서 상단에 위치하고 있습니다. 이 요약영역은 전체 프로세스가 OS에 대해서 리소스를 어느정도 차지하고 있는지를 알려줍니다. 요약 영역에 나타나는 대표적인 값은 시간, 유저, 로드 에버리지(Load Average), 테스크(Tasks), CPU, 메모리(memory)입니다.

##### 1. System time, Uptime, User  
시스템 현재 시간, OS가 살아있는 시간, 그리고 유저의 세션수가 표시되는 영역으로 시스템의 현재시간으로 GMT 기준 16:29:09 이다. up 8:26는 OS가 얼마나 살아있는지를 나타낸다. days와 시간으로 표시되며 사진에는 8분26초 살아있었다. 다음표시(0 users)는 현재 접속중인 유저 세션 수입니다.

##### 2. 로드 애버리지(Load Average)  
해당 영역은 CPU Load(CPU가 수행하는 작업의 양)의 이동 평균를 표시합니다. 앞에서 부터 1분, 5분, 그리고 15분에 대한 평균값입니다.

##### 3. Tasks  
Tasks는 현재 프로세스들의 상태를 나태내주는 영역입니다. Total은 전체 프로세스, running은 running 상태인 프로세스, sleeping은 대기상태인 process, stopped는 종료된 프로세스, zombies는 좀비상태인 프로세스의 수를 나타냅니다.

##### 4. CPU 사용량
%Cpu(s)라는 영역으로 이 영역은 CPU가 어떻게 사용되고 있는지 그 사용율을 보여주는 영역입니다.

- us : 프로세스의 유저 영역에서의 CPU 사용률
- sy : 프로세스의 커널 영역에서의 CPU 사용률
- ni : 프로세스의 우선순위(priority) 설정에 사용하는 CPU 사용률
- id : 사용하고 있지 않는 비율
- wa : IO가 완료될때까지 기다리고 있는 CPU 비율
- hi : 하드웨어 인터럽트에 사용되는 CPU 사용률
- si : 소프트웨어 인터럽트에 사용되는 CPU 사용률
- st : CPU를 VM에서 사용하여 대기하는 CPU 비율

##### 5. 메모리 사용량  
메모리와 관련된 영역으로 첫번째 줄은 RAM의 메모리 영역으로 Mem이라 표시되어있는 부분입니다. 그리고 아랫줄은 디스크를 메모리 처럼 이용하는 Swap 메모리 영역입니다. 일반적으로 Mem의 사용량이 거의 가득 찼을때 Swap 메모리 영역을 사용합니다. 이 영역은 디스크이기 때문에 RAM 메모리보다 속도가 많이 느린 단점을 가집니다.

- total : 총 메모리 양

- free : 사용가능한 메모리 양

- used : 사용중인 메모리 양

##### 6. buff/cache  
IO와 관련되어 사용되는 버퍼에 사용되는 메모리를 말합니다. 이 메모리가 있으므로써 IO에 상대적으로 빠른 속도를 가질 수 있습니다. avail Mem은 swap 메모리를 사용하지 않고 사용할 수 있는 메모리의 크기를 말합니다.

##### 7. 디테일 영역  

- PID: 프로세스 ID이며 프로세스를 구분하기 위한 겹치지않는 고유한 값입니다.
- USER: 해당 프로세스를 실행한 USER 이름 또는 효과를 받는 USER의 이름입니다.
- PR : 커널에 의해서 스케줄링되는 우선순위입니다.
- NI : PR에 영향을 주는 nice라는 값입니다.  
VIRT, RES, SHR, %MEM 해당 필드들은 프로세스의 메모리와 관련있습니다.
- VIRT : 프로세스가 소비하고 있는 총 메모리입니다. 프로그램이 실행중인 코드, heap, stack과 같은 메모리, IO buffer 메모리를 포함합니다.
- RES : RAM에서 사용중인 메모리의 크기를 나타냅니다.
- SHR : 다른 프로세스와의 공유메모리(Shared Memory)를 나타냅니다.
- %MEM : RAM에서 RES가 차지하는 비율을 나타냅니다.
- S : 프로세스의 현재 상태를 나타냅니다.
- TIME+ : 프로세스가 사용한 토탈 CPU 시간
- COMMAND : 해당 프로세스를 실행한 커맨드를 나타냅니다.

### top 실행후 명령어

|옵션|내용|
|:---|:------------------------------|
|shift + p| CPU 사용률이 높은 프로세스 순서대로 표시|
|shift + m|메모리 사용률이 높은 프로세스 순서대로 표시|
|shift + t|프로세스가 돌아가고 있는 시간 순서대로 표시|
|- k| 프로세스  kill  - k 입력 후 종료할 PID 입력 signal을 입력하라고 하면 kill signal인 9를 입력
|- a|메모리 사용량에 따라 정렬|
|- b|Batch 모드 작동|
|- c|명령행/프로그램 이름 토글|
|- d|지연 시간 간격은 다음과 같다. -d ss. tt (seconds.tenths)
|- h|도움말|
|- H|스레드 토글|
|- i|유휴 프로세스 토글|
|- m|VIRT/USED 토글|
|- M|메모리 유닛 탐지|
|- n|반복 횟수 제한 : -n number|
|- p|PID를 다음과 같이 모니터 : -pN1 -pN2 ... or -pN1, N2 [, ...] 
|- s|보안 모드 작동|
|- S|누적 시간 모드 토글|
|- u|사용자별 모니터링 : -u somebody|
|- U|사용자별 모니터링 : -U somebody|
|- v|version|
|space bar|refresh|
|- u |입력한 유저의 프로세스만 표시 - which u|
|숫자 1|CPU Core별로 사용량을 보여준다|


## Ps(Process Status)

### 정의

현재 실행중인 프로세스 목록과 상태를 보여줍니다.
ps의 옵션은 전통적인 유닉스인 System V, BSD, GNU에 따라 결과가 다르게 나타나고 표기법에도 차이를 보이기에 원하는 프로세스의 상태를 출력하려면 정확한 옵션 사용이 중요합니다.

### ps 사용법, 용어정리
$ ps [option]

<ps명령어만 단독으로 사용하였을 때>

![ps](https://user-images.githubusercontent.com/106536020/172018654-f40c7e03-9355-49b2-b24f-0d929dde1678.PNG)

### ps로  알 수 있는 정보

|항목|내용|
|:---|:------------------------------|
|USER|BSD계열에서 나타나는 항목으로 프로세스 소유자의 이름|
|UID|SYSTEM V계열에서 나타나는 항목으로 프로세스 소유자의 이름|
|PID|프로세스의 식별변호|
|PPID|부모 프로세스 ID|
|%CPU|CPU 사용 비율의 추정치(BSD)|
|%MEM|메모리의 사용 비율의 추정치 (BSD)|
|VSZ|K단위 또는 페이지 단위의 가상메모리 사용량|
|RSS|실제 메모리 사용량 (Resident Set Size)|
|TTY|프로세스와 연결된 터미널|
|S, STAT|현재 프로세스의 상태 코드 (S: Sys V, STAT: BSD)|
|TIME|총 CPU 사용 시간|
|COMMAND|프로세스의 실행 명령행|
|STIME|프로세스가 시작된 시간 혹은 날짜|
|C, CP|짧은 기간 동안의 CPU 사용률 (C: Sys V, CP: BSD)|
|F|프로세스의 플래그|
|PRI|실제 실행 우선순위|
|NI|nice 우선순위 번호|



### 대표적인 ps 옵션

특정 프로세스를 확인하는데 주로 grep이라는 명령어(특정 파일에서 지정한 문자열이나 정규표현식을 포함한 행을 출력해주는 명령어)와 함께 사용합니다.
자세한 명령어는 man 명령어를 통해 알아볼 수 있다.

|옵션|내용|
|:---|:------------------------------|
|-A|	모든 프로세스를 출력한다.|
|a| (BSD계열) 터미널과 연관된 프로세스를 출력하는 옵션이다. 보통 x 옵션과 연계하여 모든 프로세스를 출력할 때 사용한다. |
|-a|	세션 리더(일반적으로 로그인 셸)을 제외하고 데몬 프로세스처럼 터미널에 종속되지 않은 모든 프로세스를 출력한다.|
|-e|	커널 프로세스를 제외한 모든 프로세스를 출력해 준다.|
|-f|	풀 포맷으로 보여준다 유닉스 스타일로 출력해주는 옵션으로 UID, PID, PPID등이 함께 표시된다.|
|-l| (sys V) l (BSD계열) 긴 포맷으로 보여준다. , 프로세스의 정보를 길게 보여주는 옵션으로 우선순위와 관련된 PRI와 NI값을 확인할 수 있다.| 
|-o| 값	출력 포맷을 지정하는 옵션으로 값으로는 pid, tty, time, cmd 등을 지정할 수 있다.|
|-M|	64비트 프로세스들을 보여준다.|
|-m|	프로세스들 뿐만 아니라 커널 스레드들도 보여준다. |
|-p|	특정 PID를 지정할 때 사용합니다 |
|-r|	현재 실행 중인 프로세서를 보여준다. |
|u| (BSD계열) 	프로세스의 소유자를 기준으로 출력한다. (ps ax만 하면 USER 기준의 정보가 안뜸, 따라서 aux 이렇게 같이 대게 써준다) |
|-u|	특정 사용자의 프로세스 정보를 확인할 때 사용한다. 사용자를 지정하지 않으면 현재 사용자를 기준으로 정보를 출력한다. |
|x (BSD계열)|	데몬 프로세스처럼 터미널에 종속되지 않는 프로세스를 출력한다. 보통 a옵션과 결합하여 모든 프로세스를 출력할 때 사용한다.|
|-x|	로그인 상태에 있는 동안 아직 완료되지 않은 프로세서들을 보여준다. 유닉스 시스템은 사용자가 로그아웃 한 후에도 임의의 프로세서가 게속 동작하게 할 수 있다. 그러면 그 프로세서는 자신을 실행시킨 셸이 없이도 계속 자신의 일을 수행하는데 이러한 프로세스는 일반적인 ps 명령으로 확인할 수 잆다. 이 때 -x 옵션을 사용하면 자신의 터미널이 없는 프로세서들을 확인할 수 있다. |
 

ex)
$ ps –ef : 모든 프로세스를 풀 포맷으로 출력  
![ps 사용법 예시1](https://user-images.githubusercontent.com/106536020/172019335-56154c9d-82f5-47ff-8ab0-5931bacfabfb.PNG)
$ ps –ef | grep ‘프로세스명’ : ‘프로세스명’의 프로세스 구동 확인  
![ps 사용법 예시2](https://user-images.githubusercontent.com/106536020/172019343-676f5fab-1bcf-4624-917f-ca5fa2db194a.PNG)


## Kill 명령어 

### 정의
kill 명령어는 대개 프로세스를 죽일 때 사용합니다. 하지만 내부적으로는 프로세스에 시그널을 보내 원하는 작업을 하게 하는 명령어입니다.  
$ kill [options] <pid> [...]

### 사용법 
 
#### 1. 사용자 지정 시그널 전송 방법  
kill 명령어의 default 시그널은 TERM(15) 입니다. 하지만 -s 명령으로 다른 시그널을 보낼 수 있습니다.
 
$ kill [옵션 or 시그널]pid  
사용 가능한 시그널 목록
 
kill –l 명령어를 통해 지원하는 시그널 목록

![kill 옵션](https://user-images.githubusercontent.com/106536020/172019466-2237871d-2155-4d19-a422-f466597e0e18.PNG)

### 주요 시그널

|시그널|내용|
|:---|:------------------------------| 
|1) SIGHUP|세션이 종료될 때 시스템이 내리는 시그널|
|2) SIGINT|Ctrl + C, 종료 요청 시그널|
|9) SIGKILL|강제 종료 시그널|
|11) SIGSEGV|메모리 침범이 일어날 때 시스템이 보내는 시그널|
|15) SIGTERM|기본 값, 종료 요청 시그널|
|20) SIGTSTP|Ctrl + Z 일시 중지 요청 시그널|
  

#### 2. 프로세스 죽이는 방법  
 
명령어: $ kill [pid]
 
kill 명령으로 종료되지 않는 프로세스가 있다면 -9 옵션을 이용하여 프로세스를 강제 종료시킴.

![kill 명령어](https://user-images.githubusercontent.com/106536020/172019571-e1433041-29d1-42a0-b008-4550b967d85c.PNG)

위 그림처럼 ps 명령어를 통해 pid 값을 얻어서 171 pid를 삭제 한 걸 볼 수 있다.  
만일 kill 명령으로 종료되지 않는다면 kill –9 [PID 명령어] 이용해서 강제 종료시킬수있다.  
kill –HUP [PID 명령어]를 이용하면 종료된 프로세스를 되살릴 수 있다.  


## Jobs 명령어

### 정의
jobs 명령어는 작업의 상태를 표시하는 명령어다.
현재 쉘 세션에서 실행시킨 백그라운드 작업의 목록이 출력되며, 각 작업에는 번호가 붙어 있어 kill 명령어 뒤에 '%번호' 등으로 사용할 수 있다.

### 사용방법
$ jobs [옵션][작업번호]

![jobs](https://user-images.githubusercontent.com/106536020/172019618-2d9525fb-5395-4bf4-bee6-41d0059f234b.PNG)
 
(현재 쉘 프로세스의 자식 백그라운드 프로세스들을 보여주고 있다.)
  
### jobs 명령어 옵션
|옵션|내용|
|:---|:------------------------------| 
|-l|프로세스 그룹 ID를 state 필드 앞에 출력|
|-n|프로세스 그룹 중에 대표 프로세스 ID를 출력|
|-p|각 프로세스 ID에 대해 한 행씩 출력|
|command|지정한 명령어를 실행|
  
### jobs로 출력되는 백그라운드 작업의 상태값
 
|상태|내용|
|:---|:------------------------------| 
|Running|작업이 계속 진행중임|
|Done|작업이 완료되어 0을 반환|
|Done(code)|	작업이 종료되었으며 0이 아닌 코드를 반환|
|Stopped|	작업이 일시 중단|
|Stopped(SIGTSTP)|SIGTSTP 시그널이 작업을 일시 중단|
|Stopped(SIGSTOP)|SIGSTOP 시그널이 작업을 일시 중단|
|Stopped(SIGTTIN)|SIGTTIN 시그널이 작업을 일시 중단|
|Stopped(SIGTTOU)|SIGTTOU 시그널이 작업을 일시 중단|

## Vim 에디터 매크로 사용방법

### 매크로 저장하기
q [저장할 매크로 문자] -> 동작수행 -> q

### 매크로 사용하기
1. 특정문자에 저장한 매크로 실행
@ [저장한 매크로 문자] 
2. 매크로 반복실행
반복횟수 @ [저장한 매크로 문자]
3. 마지막에 수행한 매크로 실행

ex)  
q [a] -> 20205102 엔터키 -> q 로 매크로 저장 -> @ [a] 로 실행
![매크로](https://user-images.githubusercontent.com/106536020/172019806-a9c328d9-1959-4887-a7d3-467500d8e224.PNG)
q [a] -> 20205102 엔터키 -> q 로 매크로 저장 -> @ @ 로 마지막에 수행한 매크로 실행
![매크로1](https://user-images.githubusercontent.com/106536020/172019813-28fd57b9-611e-421b-a814-3d6556b2b3f2.PNG)
ex2)
q [a] -> 20205102 엔터키 -> q 로 매크로 저장 -> 10 @ [a] 로 실행 (10번의 매크로 실행)
![매크로2](https://user-images.githubusercontent.com/106536020/172019816-72591555-9cc5-4d84-9711-968ddf8ae3b2.PNG)
