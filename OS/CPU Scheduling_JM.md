# CPU 스케줄링

- 준비큐에 있는 프로세스에 대해 CPU를 할당하는 방법
    - 우리가 컴퓨터에서 유튜브를 보면서 카톡을 하면서 게임을 할 때 동시에 실행되고 있는 것이 아니다.
    - 실행되고 있는 프로세스들이 준비큐라는 곳에 들어있다.
    - 하나씩 실행되면서 왔다갔다 하는 것이다.
- 선점 VS 비선점
    - 선점 : 너 나와
    - 비선점 : 기다려줄게
- 비선점 스케줄링
    - FCFS (First Come First Served)
        - 먼저 CPU를 요청하는 프로세스를 처리하는 방식
            
            ![fcfs](https://github.com/user-attachments/assets/73e31f55-77c8-40e5-800b-91125d83421d)
            
    - SJF(Shortest Job First)
        - 시간이 짧은 프로세스를 먼저 실행하는 방식
            
            ![sjf](https://github.com/user-attachments/assets/56bd286f-8256-4b45-adbb-60b45f876507)
            
        - Burst Time: CPU가 사용하는 시간
        - P2가 가장 작으니까 첫번째
        - 2→1→4→3
- 선점 스케줄링
    - SRT(Shortest Remaining Time)
        - 남은 시간이 짧은 것을 우선
        - 얘가 지금 나보다 실행해야 되는 시간이 더 많아 그럼 내가 얘껄 뺏고 들어가는 것
            
            ![srt](https://github.com/user-attachments/assets/fa59647e-a53b-429c-974a-36362c00effe)
            
        - CPU가 P1을 처리중에 1초 후에 P2가 왔다.
        - 1초가 실행되어 P1은 7초가 남았는데 P2는 4초 짜리 이다.
        - 너 나와 하고 P2가 실행된다.
    - RR(Round Robin)
        - 지금까지는 하나 실행되고 다른 것이 실행되는 형식이었다면 라운드로빈은 공평하게 1초씩 실행되는 형식
        - 1초는 정해진 것은 아니고 조율 가능
            
            ![rr](https://github.com/user-attachments/assets/b4239471-fef5-4205-95cc-fdff51d93567)
            
        - Time Quantum, Time Slice → 실행되는 시간
        - 시간을 100초(큰 수)로 설정한다면 FCFS와 다를 것이 없다.
        - 0.1초(매우 작은 수)로 설정한다면 매우 좋다. RR의 의도가 모든 것을 공평하게 실행하자 이기 때문에 의도와는 맞다.
        - 문제는 P1을 실행하다가 P2를 실행하러 갈 때 비용이 발생하게 된다. 프로세스를 처리하는데 시간을 쓰는 것이 아니라 왔다갔다 하는데 시간을 쓰게 된다. (Context Switch)가 많이 일어나게 된다.
        - Time Slice를 적당하게 정하는 것이 중요하다.
    - Priority Scheduling(우선 순위 스케줄링)
        - 우선순위가 높은 프로세스를 먼저 할당하는 방식
        - 우선순위는 알아서 정한다.
        - 시간 제한, 메모리 요구량, 프로세스의 중요성, 자원사용 비용등에 따라 달라진다.

### CPU 스케줄러가 뭐예요?

- 준비큐에 있는 프로세스에 대해서 CPU를 할당하는 방법입니다.
- 크게 다섯가지가 있는데요, FCFS, SJF, SRT, Round Robin, Priority Scheduling이 있습니다.
- 각 스케줄러에 대한 대답