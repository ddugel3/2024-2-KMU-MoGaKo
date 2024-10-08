## What is Software Architecture?

- 소프트웨어 아키텍처란 무엇일까?
    - 소프트웨어 시스템은 조직의 **비즈니스 목표를 충족**시키기 위해 구축된다.

- 소프트웨어 아키텍처는 다리이다.
    - 소프트웨어 아키텍처는 비즈니스 및 임무 목표 달성을 지원하는 것으로 알려진 기술을 사용하여 **설계, 분석, 문서화 및 구현**될 수 있다.
    - 복잡성을 길들여 다루기 쉽게 만들 수 있다.

- 건축 예시
    - 강아지집 → 가정집 → 고층건물
    - 더 크고 복잡한 건물을 지으려고 할 수록 **최적의 설계**가 필요하다.
    - 또한 건축에서 여러 사항을 고려하는 것처럼 프로젝트를 진행할 때도 여러 사항들을 고려해야한다.
        
        
        | Scale | 규모 |
        | --- | --- |
        | Cost | 비용 |
        | Schedule | 일정 |
        | Stakeholders | 이해당사자들, 이해관계자들 |
        | Skills of development teams | 팀원들의 능력 |
        | Materials and technologies | 자원들, 기술들 |
        | Risks | 위험 요소들 |
        | Development Process | 개발 공정 |

- 소프트웨어 아키텍처의 정의
    - 소프트웨어아키텍처는 구조(체)가 있다.
    → 여기에는 이 구조가 왜 필요한 지가 따라가야한다.
    - 그리고 구조체 안에 다양한 구성요소가 있고, 그 구성요소의 특징과 구성요소 간의 관계도 중요하다.
    - ⇒ 그러한 것이 왜 필요한지 설명하는 것이 모두 포함된 게 소프트웨어아키텍처이다

- 모듈
    - 모듈을 만들 때(= 클래스를 만들 때 ), 이 클래스가 해야하는 역할과 일을 정리해야한다.
    - **재사용성**: 모듈을 잘 만들어두면 다른 프로젝트에서도 사용할 수 있다.
    - 상속: 이전에 만들어둔 구조체를 사용하면서 새로운 기능을 확장하여 사용할 수 있다.
    - 해당 프로젝트를 다시 사용할 때, 유지관리 할 수 있는 상황을 만들어주어야 한다.
- Dynamic Structures
    - 런타임할 때 일어나는 것
    - 실행하면서 코드를 집어넣어도 다시 시스템을 다운로드하지 않아도 된다.
- Mapping

- 아키텍처는 구조체를 만들 때, 왜 이 구조체를 왜 만드는지 이유가 있으면 그게 바로 아키텍처가 되는 것이다.
