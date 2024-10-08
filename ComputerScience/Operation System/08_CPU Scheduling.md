# CPU Scheduling

### 1. 스케줄링

> 메모리에 있는 준비 상태 프로세스들의 우선순위와 요구사항에 따라 CPU 자원을 할당하는 방법

#### 스케줄링 방법

> 프로세스의 규모와 적용 시기에 따라 구분된다.  

> 각 스케줄링 단계는 시스템 전체 성능과 CPU 활용률을 결정하는 중요한 역할을 한다.

- 장기 스케줄링 (Long-term scheduler)

    - 시스템에 새로운 프로세스가 들어올 때, 어떤 프로세스를 메모리에 올릴 것인지 결정하는 단계

    - 전체 시스템의 부하를 고려하여 작업 요청을 받아들일지, 거부할지 결정한다.

        - 이 결정에 따라 시스템 내의 프로세스 총 개수(degree of multiprogramming)가 정해진다.

    - 프로세스의 수행 시간, 우선순위, 입출력 요구 등을 고려하여 결정된다.

- 중기 스케줄링 (Medium-term scheduler, Swapper)

    - 시스템 과부하를 막기 위해 활성화된 프로세스들의 중지 여부를 결정하여 활성화된 프로세스 수를 조절한다. (swap-out)

    - swap-out : 여유 공간 마련을 위해 프로세스를 통째로 메모리에서 디스크로 빼내는 것

        - degree of multiprogramming을 제어하는 것

    - 메모리 부족 상황에서 필요하고, 프로세스들의 입출력 요구를 고려하여 결정된다.

- 단기 스케줄링 (Short-term scheduler, CPU scheduler)

    - CPU를 할당받기 위해 대기 중인 프로세스들 중에서 어떤 프로세스를 선택하여 CPU를 할당할 것인지 결정하는 단계

    - **어떤 기준에 따라 프로세스를 선택 (스케줄링 알고리즘)**하고 **어느 정도 자원을 배분**(Time slice)할지에 따라 시스템에 큰 영향을 끼친다.

    - 프로세스의 우선순위, 수행 시간 등을 고려하여 결정된다.

<br>

### CPU 스케줄링 종류

- 선점형 스케줄링

    - 운영체제가 프로세스 실행 중간에 다른 프로세스로 제어권을 뺏어 해당 프로세스를 일시 중지시키고, 우선순위가 더 높은 프로세스에게 제어권을 넘겨주는 스케줄링 방식

    - Round Robin

        - 각 프로세스에게 일정한 시간 할당을 해주고 할당된 시간이 지나면 다음 프로세스에게 CPU를 넘기는 방식

        - 여기서 넘겨주는 시간을 할당 시간이라고 한다.
        
            - 할당 시간이 짧으면 CPU를 빨리 넘겨줄 수 있지만 문맥 교환(Context Switching)이 자주 발생하여 오버헤드가 커질 수 있다.
    
            - 할당 시간이 길면 문맥 교환, 오버헤드는 줄어들지만, 프로세스의 대기시간이 길어질 수 있다.

    - Priority Scheduling

        - 우선순위가 높은 프로세스부터 실행하는 방식

        - 중요한 작업부터 처리할 때 유용하다.

        - 하지만 우선순위가 높은 프로세스가 계속해서 들어올 경우, 우선순위가 낮은 프로세스는 계속 대기하게 되어 기아 상태가 발생할 수 있다.

- 비선점형 스케줄링

    - 프로세스가 종료되거나 입출력 등의 이벤트가 발생할 때까지 해당 프로세스가 제어권을 유지하는 스케줄링 방식

    - FCFS (First-Come, First-Served)

        - 먼저 도착한 프로세스를 먼저 실행하는 방식

        - CPU가 현재 수행 중인 작업을 완료하면, 대기 중인 프로세스 중에서 가장 먼저 들어온 프로세스를 실행한다.

        - 장점 : 구현이 간단하고 공정한 방식

        - 단점 : 대기 시간이 길어질 수 있고, 작업시간이 긴 프로세스가 먼저 실행되는 경우에 평균 대기시간이 길어질 수 있다.

    - SJF (Shortest Job First)

        - 대기시간이 가장 짧은 작업을 우선적으로 실행하는 방식

        - 실행시간이 긴 프로세스보다 짧은 프로세스가 먼저 실행되기 때문에 평균 대기시간이 짧아진다.

            - 그럴려면 작업시간을 미리 알고 있어야 하고, 작업시간을 알 수 없을 경우에는 예측 오류로 인해 평균 대기시간이 길어질 수 있다.

        - 작업 시간이 짧은 프로세스가 지속적으로 들어올 경우, 작업시간이 긴 프로세스는 계속 대기해야하기 때문에 기아 상태(Starvation)가 발생할 수 있다.


<br>

#### 문제
CPU 스케줄링은 어떤 ⓐ에 따라 프로세스를 선택 (스케줄링 알고리즘)하고 ⓑ을 배분(Time slice)할지에 따라 시스템에 큰 영향을 끼친다.

<br>

##### [참고]
[CPU 스케줄링이란?](<https://superohinsung.tistory.com/125>)

[CPU 스케줄링의 개념](<https://kjhoon0330.tistory.com/entry/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9COS-CPU-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81>)

[스케줄링 알고리즘](<https://kjhoon0330.tistory.com/entry/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9COS-CPU-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81-2-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98>)
