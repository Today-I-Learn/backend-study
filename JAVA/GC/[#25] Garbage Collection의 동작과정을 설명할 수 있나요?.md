### Garbage Collection의 동작과정을 설명할 수 있나요?<br>
GC의 동작방식은 공통적으로 2가지의 단계를 따르게 됩니다.
1. Stop The World : Stop The World는 가비지 컬렉션을 실행하기 위해 JVM이 애플리케이션의 실행을 멈추는 작업입니다. <br>
                    GC가 실행될 때는 GC를 실행하는 쓰레드를 제외한 모든 쓰레드들의 작업이 중단되고, GC가 완료되면 작업이 재개됩니다. <br>
                    당연히 모든 쓰레드들의 작업이 중단되면 애플리케이션이 멈추기 때문에, <br>
                    GC의 성능 개선을 위해 튜닝을 한다고 하면 보통 stop-the-world의 시간을 줄이는 작업을 하는 것입니다. <br>
                    또한 JVM에서도 이러한 문제를 해결하기 위해 다양한 실행 옵션을 제공하고 있습니다.
2. Mark and Sweep : Stop The World를 통해 모든 작업을 중단시키면, <br>
                    GC는 스택의 모든 변수 또는 Reachable 객체를 스캔하면서 각각이 어떤 객체를 참고하고 있는지를 탐색하게 됩니다. 
                    그리고 사용되고 있는 메모리를 식별하는데, 이러한 과정을 Mark라고 합니다. <br>
                    이후에 Mark가 되지 않은 객체들을 메모리에서 제거하는데, 이러한 과정을 Sweep라고 합니다. 
                    


### Garbage Collection의 종류를 말할 수 있나요?
1. Serial GC : 적은 메모리, 적은코어에 적합한 방식으로 Serial GC의 Young 영역은 알고리즘(Mark Sweep)대로 수행됩니다. <br>
                하지만 Old 영역에서는 Mark Sweep Compact 알고리즘이 사용되는데, 기존의 Mark Sweep에 Compact라는 작업이 추가되었습니다. <br>
                Compact는 Heap 영역을 정리하기 위한 단계로 유요한 객체들이 연속되게 쌓이도록 <br>
                힙의 가장 앞 부분부터 채워서 객체가 존재하는 부분과 객체가 존재하지 않는 부분으로 나누는 것입니다.
2. Parallel GC : Serial GC와 기본적인 알고리즘은 같으나, Parallel GC는 멀티 쓰레드를 사용합니다.<br>
                 이로 인해 stop-the-world하는 시간이 줄어 애플리이케이션 성능을 개선하였습니다. <br>
                 따라서 Parallel GC는 메모리 크기가 클 때와 다중 코어에서 유리합니다.<br>
                 이는 CMS GC를 사용해서 얻는 latency(지연) 단축에 대한 것보다 throughput(성능)이 더 중요할 때 사용 됩니다.
3. Parallel Old GC : Parallel GC는 Old 영역의 GC 알고리즘이 Mark-Summary-Compaction을 거칩니다. <br>
                     Summary 단계는 Sweep과 달리 GC를 수행한 영역에 대한 객체 식별을 거칩니다. 
4. G1(Garbage First) GC : Young Generation과 Old 영역이 존재하나, 고정된 크기와 위치로 존재하지 않습니다.<br><br>
                          G1 GC는 CMS GC를 대체하기 위해서 만들어진 GC로 <br>
                          Heap Space를 Region이라는 일정 크기로 나누어 각 Region에 Young, Old를 동적으로 부여합니다.
5. Concurrent Mark Sweep(CMS) : CMS GC는 Parallel GC와 마찬가지로 여러 개의 쓰레드를 이용합니다. <br>
                                하지만 기존의 Serial GC나 Parallel GC와는 다르게 Mark Sweep 알고리즘을 Concurrent하게 수행합니다.
