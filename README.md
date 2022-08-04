# Apache NiFi

Apache NiFi 는 미국 국가안보국 NSA 가 Apache 재단에 기증한 Dataflow 엔진이다. 
NiFi 는 시스템 간 데이터 전달을 효율적으로 처리, 관리, 모니터링하기 위한 최적의 시스템이다. 대량의 데이터를 수집, 처리하기 위해 만들어졌다.

NiFi 의 특징으로는 
<sub>(1)</sub> GUI 를 제공하여 Dataflow 를 쉽게 개발하고 시스템 간의 데이터 이동 내용을 볼 수 있다는 점,
<sub>(2)</sub> Multi-tenant; 여러 조직이 자원을 공유해서 사용하는 기능을 지원하는 점,
<sub>(3)</sub> 데이터 출처를 추적할 수 있다는 점 
등.. 이있다.

NiFi는 FBP <sub>Flow Based Programming</sub> 의 개념을 구현했으며,

## Nifii 구성요소

NiFi 에서 쓰이는 용어에는 <code>FlowFile</code>, <code>FlowFile Processor</code>, <code>Connection</code>, <code>Flow Controller</code>, <code>ProcessGroup</code> 등.. 이 존재한다.
이에 대한 설명은 아래와 같다

| NiFi | FBP | Description |
|:---:|:---:|:---:|
| FlowFile | Information Packet | NiFi 에서 데이터를 표현하는 객체; Key-Value 형태이며, 이를 통해서 여러 시스템 간의 데이터 이동이 가능 |
| FlowFile Processor | Black Box | FlowFile 은 여러 단계를 거쳐 변경된다. 이때 사용되는 것이 FlowFile Processor 이다. |
| Connection | Bounded Buffer | Processor 간 연결을 말한다. Queueing, Routing, BackPressure, 우선순위 제어, Monitoring 등.. 을 제공 |
| Flow Controller | Scheduler | Processor 의 실행 간격, 시점 등.. 스케줄링을 담당한다. |
| Process Group | Subnet | 여러 단위로 Processor 를 묶을 수 있으며, Group 간의 데이터 이동이 가능하다. |

## Architecture

![NiFi Architecture](./images/nifi_architecture.png)

NiFi 는 위 사진과 같이 설계되어 있다.

1. Web Server   
앞서 설명함과 같이 NiFi 는 UI 를 제공한다. Web Server 에서 제공하는 UI System 을 통해 DataFlow 를 개발, 제어, 모니터링이 가능하다.

2. Flow Controller   
NiFi 의 Scheduling 을 담당한다.

3. Extension   
NiFi 가 제공하는 기본 Processor 외, 개발자가 프로세스를 개발해 확장이 가능하다. 

4. FlowFile Repository   
데이터 선행 기입 (Write-Ahead-Log) 방식으로 FlowFile 을 저장한다. 일반적으로 Raid 10 으로 디스크를 구성한다. 시스템 장애 시 데이터가 유실되지 않도록 주의해야한다. 

5. Content Repository   
FlowFile 가 저장되며, 이 또한 Raid 10 구성이 일반적이다. 

6. Provenance Repository
데이터의 처리 단계별로 데이터를 보관한다. 각 데이터는 인덱스 되어 검색가능하다.

7. FlowFile, Processor
NiFi의 핵심 컴포넌트이다. FlowFile은 Processor에 의해 생성되며, FlowFile은 속성 정보와 데이터가 들어있다.

* ref : <https://www.popit.kr/apache-nifi-overview-and-install/>

## Nifi 사용해보기

