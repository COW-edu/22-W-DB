# Chapter 6 - 데이터 모델링

## 데이터 모델링의 개념

- **데이터 모델링**: 현실 세계의 복잡한 개념을 단순화하고 추상화시켜 데이터베이스화 하는 과정

- **DB 생명주기**
    
    - 데이터 모델링 ⇒ 요구사항 수집 및 분석 ~ 설계까지의 과정을 말함
    
- **요구사항 수집 및 분석**
    - 현실 세계를 파악하고 사용자의 요구사항을 수집 및 분석하는 단계
    - 요구사항 수집을 위해 사용하는 방법
        - 실제 문서를 수집하고 분석
        - 담당자와의 인터뷰나 설문조사를 통해 요구사항을 직접 수렴
        - 기존의 DB를 분석
    - 수집된 자료는 **모호성을 제거**하고 최대한 **구체적**이고 **명확하게 정리해야 함**

- **개념적 모델링 (Conceptual modeling)**
: 요구사항을 수집하고 분석한 결과를 토대로 업무의 **핵심적인 개념을 구분**하고 전체적인 뼈대를 만드는 과정
    - 핵심적인 개념을 구분한다는 것 ⇒ entity를 추출하고 각 entity들 간의 관계를 정의해 E-R Diagram을 만드는 과정까지를 말함
    - **entity**: 구체적으로 표현할 수 있는 실체
    - **ER Diagram**: 이러한 entity들의 관계를 표현한 것
    
    - PK나 각 개체 간의 관계를 정의한다.
    
- **논리적 모델링 (Logical modeling)**
: conceptual modeling에서 만든 ER Diagram을 사용하고자 하는 DBMS에 맞게 **매핑**해 실제 DB로 구현하기 위한 모델을 만드는 과정
    
    - 논리적 모델링 과정: conceptual modeling에서 추출하지 않았던 상세 속성들을 모두 추출 → **정규화**를 수행 → 데이터의 표준화를 수행
    
- **물리적 모델링 (Physical modeling)**
: 작성된 logical model을 실제 컴퓨터의 저장 장치에 저장하기 위한 물리적 구조를 정의하고 구현하는 과정
    
    - 물리적 모델링을 할 때 고려할 사항
        - 응답시간을 최소화
        - 얼마나 많은 트랜젝션을 동시에 발생시킬 수 있는지
        - 데이터가 저장될 공간을 효율적으로 배치해야 함
    

## ER 모델

- ER model: 데이터 모델링 과정 중 conceptual modeling에 사용하는 모델
    - 세상의 사물을 entity와 entity 간의 관계 (relationship) 로 표현
    - entity는 entity의 특성을 나타내는 속성 (attribute)으로 식별하고, entity끼리 서로 관계를 가짐

- **Entity (개체)**
    - 특징
        - 유일한 식별자에 의해 식별이 가능
        - 꾸준한 관리를 필요로 하는 정보
        - 두 개 이상 영속적으로 존재
        - 업무 프로세스에 이용
        - 반드시 자신의 특징을 나타내는 속성을 포함
        - 다른 개체와 최소 한 개 이상의 관계를 맺고 있음
        
    - Entity는 **Strong entity (보통의 entity)** 와 **weak entity**로 구분할 수 있음
        - weak entity: 독자적으로는 존재할 수 없는 entity

- **Attribute (속성)**
: 개체가 가진 성질
    
    - attribute → 타원
    - pk일 경우 이름에 밑줄그음
    
    - weak entity에서 개별 개체를 구분하는 속성인 partial key (부분키) = 식별자
        - 표현할 때에는 이름에 점선 그음
        
    
    - **유형**
        - simple attribute / composite attribute
            - simple → 더 이상 분해가 불가능함
            - composite → 독립적인 의미를 가진 속성으로, 분해할 수 있음
            
        - single-valued attribute / multi-valued attribute
            - single-valued: 하나의 값만을 가지는 속성
            - multi-valued: 여러 개의 값을 가지는 속성
            
        - 저장 속성 / 유도 속성
            - 저장속성: 다른 속성의 영향 없이 단독으로 저장되는 속성
            - 유도속성: 다른 저장 속성으로부터 유도된 (계산되어진) 속성
            
    
- 관계 타입: 개체 타입과 개체 타입 간의 연결 가능한 관계를 정의한 것
    
    → 마름모로 표현
    
    - **유형**
        - 차수에 따른 유형
            - 차수 → 관계 집합에 참가하는 entity type의 수
            
        
        - 관계 대응 수 (Cardinality) 에 따른 유형
            - cardinality → 두 개체 타입의 관계에 실제로 참여하는 개별 개체 수
            
        - ISA 관계: 상위 개체 타입의 특성에 따라 하위 개체 타입이 결정되는 형태
            - 상위 개체 타입: 슈퍼클래스
            - 하위 개체 타입: 서브클래스
            
    - **참여 제약 조건**
        - 전체 참여: 개체 집합의 모든 개체가 관계에 참여 (두줄 실선)
        - 부분 참여: 일부만 참여 (단일 실선)

- ER 모델 외의 다른 표기법
    - IE 표기법
    

## ER 모델을 관계 데이터 모델로 매핑

- **1:1 관계**

- **1:n 관계**
    - N에 위치해 있는 relation에 1에 위치한 relation의 pk를 fk로 사용

- **m:n 관계**
    - 새로운 table을 만들고, 각각의 relation의 pk를 새로운 table의 pk로 놓음

- **multi-valued attribute**
    - 새로운 table을 만듦