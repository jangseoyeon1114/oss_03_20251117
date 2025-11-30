![header](https://capsule-render.vercel.app/api?type=Cylinder&color=d6ace6&height=200&section=header&text=리눅스%20명령어에%20대해%20공부해%20보자!&fontSize=50)

:heavy_check_mark: ### top, ps, jobs, kill을 중심으로

--------------------------------

##  1. `top`
   
- 사용하는 방법
  ```
  $ top
  ```
  
> top 명령어란?
- 현재 시스템의 **CPU/메모리 사용량, 실행 중인 프로세스, 로드(avg)** 등을 실시간으로 보여 주는 모니터링 도구이다.
  - 화면에서 보이는 주요 정보
    : PID, USER, %CPU, %MEM, TIME+, COMMAND

## :computer: 예시

<img width="845" height="164" alt="top" src="https://github.com/user-attachments/assets/24af9ccc-9c8e-4cc7-b7dc-bf05abf377c6" />

## 상단 요약 정보

- `16:17:30` : 현재 시간
- `up 2 min` : 부팅 후 2분 경과
- `0 users` : 로그인한 사용자 수
- `load average: 0.29, 0.26, 0.11`  
  → 1분, 5분, 15분 평균 부하 (1 이하면 여유 있음)
- `Tasks` : 프로세스 상태
- `%Cpu` : CPU 사용률
- `Mib Mem` : 물리 메모리
- `Mib Swap` : 스왑 메모리

## 프로세스 목록 (주요 정보)

| PID | USER | %CPU | %MEM | TIME+   | COMMAND |
|-----|------|------|------|---------|---------|
| 1   | root | 0.0  | 0.0  | 0:00.02 | bash    |
| 13  | root | 0.0  | 0.1  | 0:00.00 | top     |

```
이 외에도 다양한 옵션들
-p [PID] : 지정한 PID 값을 가진 프로세스 정보 출력
-d [초] : 업데이트 주기를 설정 (기본 주기는 3초, 초 단위 설정)
-n [n] : top을 갱신할 횟수 지정 (n번 갱신 후 종료, -b와 함께 사용)
-b : 배치 모드로 정보를 출력
```

--------------------------------

## 2. `ps`
   
- 사용하는 방법
  ```
  $ ps [옵션]
  ```
  
> ps 명령어란?
-  "process status"의 약자로, **현재 실행 중인 프로세스를 출력**하는 명령어이다.
  - 프로세스의 ID, 사용자, CPU 및 메모리 사용량, 실행 시간 등의 정보를 얻을 수 있다.
 

## :computer: 예시

<img width="577" height="55" alt="ps" src="https://github.com/user-attachments/assets/6d1da3c7-1075-4f7a-bd8f-20fc781bf462" />

## 상단 요약 정보

- `PID` : 프로세스 ID
- `TTY` : 터미널 타입
- `TIME` : 프로세스가 사용한 총 CPU 시간
- `CMD` : 실행된 명령어

## 주요 옵션

```
ps -ef      # 전체 프로세스 출력 (full format)
ps aux      # BSD 스타일 출력 (CPU, 메모리 사용량 포함)
```

> ps -ef

  <img width="509" height="55" alt="ps -ef" src="https://github.com/user-attachments/assets/92278722-c1a1-4bca-8e25-70fa787c4e1b" />


## :heavy_plus_sign: 추가되는 정보

- `USD` (프로세스를 실행한 사용자 ID)
- `PPID` (부모 프로세스 ID)
- `C` (CPU 사용률 (단기))
- `STIME` (프로세스 시작 시간)
- `TTY` (연결된 터미널)가 추가

> ps -aux

  <img width="578" height="53" alt="ps -aux" src="https://github.com/user-attachments/assets/69fe37fd-0fa6-433e-a3fc-cec87d1b0f95" />

## :heavy_plus_sign: 추가되는 정보

- `USER` (실행한 사용자)
- `%CPU` (CPU 사용률)
- `%MEM` (메모리 사용률)
- `VSZ` (가상 메모리 크기)
- `RSS` (실제 메모리 사용량)
- `STAT` (프로세스 상태 코드)
- `START` (시작 시간)
  
```
이 외에도 다양한 옵션들
-e : 현재 실행 중인 모든 프로세서를 출력
-f : 실제 유저명, 개시-시간 등을 표시
-l : 프로세서 상태, 우선도 등의 상세정보 표시
```

--------------------------------

## 3. `jobs`

- 사용하는 방법
  ```
  $ jobs [옵션] [jobID]
  ```
  
> jobs 명령어란?

- 셸에서 실행한 **프로세스 목록**을 확인한다.
- **백그라운드로 실행 중인 프로세스**를 확인한다.
- 현재 **중지된 프로세스**를 확인한다.

## :computer: 예시

<img width="465" height="35" alt="jobs" src="https://github.com/user-attachments/assets/905ac8f5-1d0e-4a9c-b2ad-83182f8f4c4c" />

- 실행 중인 작업이 없다면 **아무 내용도 출력이 되지 않는다.**
  
<img width="418" height="56" alt="jobs 목록" src="https://github.com/user-attachments/assets/dda3b737-dc52-4981-aff1-4d5e7d59853c" />

- `[1]`, `[2]`, `[3]`: 각 작업의 고유한 작업 번호
- `Stopped`: 해당 작업이 중지된 상태
- `Running`: 해당 작업이 현재 실행 중인 상태
- `top`, `bash`, `sleep 100 &`: 각 작업에서 실행 중인 명령어

```
$ jobs -p
```

<img width="407" height="56" alt="jobs -p" src="https://github.com/user-attachments/assets/f08626ae-f707-412e-9211-89f002724e4a" />

- 작업 번호나 상태 없이 각 작업의 **PID**만 출력한다.

```
$ jobs -n
```

- 상태가 변경된 작업만 출력한다. (예를 들어 작업이 **실행** 중에서 **중지** 상태로 바뀌었거나 **중지** 상태에서 **실행** 중으로 바뀌었을 때 등)

```
이 외에도 다양한 옵션들
-l : 프로세스 ID와 함께 목록 출력
-r : 실행 중인 job만 출력
-s : 중지된 job만 출력
```

> jobs 출력 시 상태값

| 상태                  | 내용                                |
|-----------------------|-------------------------------------|
| `Running`             | 실행 중인 작업                     |
| `Done`                | 작업이 완료되고 0을 반환           |
| `Done(code)`          | 작업이 종료되었으며 0이 아닌 코드 반환 |
| `Stopped`             | 작업이 중지됨                      |
| `Stopped(SIGTSTP)`    | SIGTSTP 시그널로 일시 중지 (Ctrl+Z 등) |
| `Stopped(SIGSTOP)`    | SIGSTOP 시그널로 일시 중지         |
| `Stopped(SIGTTIN)`    | SIGTTIN 시그널로 일시 중지         |
| `Stopped(SIGTTOU)`    | SIGTTOU 시그널로 일시 중지         |

--------------------------------

## 4. `kill`

- 사용하는 방법
  ```
  $ kill [옵션] [프로세스ID]
  ```

> kill 명령어란?
- 프로세스에 신호를 보내어 **특정 프로세스를 종료해 주는** 명령어이다.
- 백그라운드에서 실행되고 있는 작업이 있거나 더 이상 응답이 없는 프로그램을 **강제 종료**할 때 주로 사용한다.

## 주요 옵션

| 옵션                  | 설명                                |
|-----------------------|-------------------------------------|
| -l            | 모든 시그널 목록을 표시                       |
| -s            | 저장한 시그널을 보냄                          |
| -9            | SIGKILL 시그널을 보내어 강제 종료              |
| -15           | SIGTERM 시그널을 보내어 정상 종료를 요청       |

## 주요 시그널

| 시그널                  | 설명                                |
|-----------------------|-------------------------------------|
| SIGHUP            | 세션 종료 시그널                         |
| SIGINT            | 인터럽트 시그널                          |
| SIGKILL           | 강제 종료 시그널                         |
| SIGTERM           | 정상 종료 요청 시그널                     |
| SIGSTOP           | 프로세스 일시 정지 시그널                 |

## :computer: 예시 

<img width="1091" height="252" alt="kill 예시" src="https://github.com/user-attachments/assets/ab8d2f19-57f4-4ae0-b961-98a94088df04" />

- 백그라운드에서 실행되게 sleep 300 &을 통해 만들고 **프로세스의 PID를 확인**한다.
- **-15 55**를 통해 정상 종료를 요청한다.
- 다시 ps 명령어를 통해 확인해 보면 백그라운드 job이 종료되었음을 알 수 있다.

<img width="587" height="124" alt="kill -9" src="https://github.com/user-attachments/assets/bd9022de-fb7a-43e1-8577-2d1a74ff2039" />

- 다시 300초 동안 대기하는 명령을 백그라운드로 실행한다.
- ps 명령어를 통해 확인하면 여기서 **PID는 60**인 것을 알 수 있다.
- 이번엔 -9 옵션을 줬다. **-9는 강제로 즉시 종료**를 하게 하며 다시 ps를 통해 확인하면 Killed(강제 종료됨)을 볼 수 있다.

--------------------------------

> 요약

| 명령어                  | 설명                               |
|-----------------------|-------------------------------------|
| `top`                 | 실시간 프로세스/자원 확인             |
| `ps`                  | 현재 실행 중인 프로세스 목록           |
| `jobs`                | 백그라운드 작업 목록                  |
| `kill`                | 프로세스 종료                         |

<img src="https://img.shields.io/badge/OS-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black">




