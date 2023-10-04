# section 1
## 1. 블루프린트와 이벤트 그래프
- 선으로 이어진 툴박스로 이동
### 간단한 용어
- Event Graph : 블루프린트를 그릴 캔버스
- Node : 사전에 만들어진 함수들
- String : text
- Event : 언제 노드가 실행되는지를 알려주는 것
    - Event BeginPlay
- Input Pin : 노드를 언제 실행할지
- Output Pin : 실행할때 무엇을 할지

## 2. 물리설정
- 기본적으로 물리설정을 안해놔서 오브젝트를 올려놔도 그대로 고정된 상태를 유지함
- detail창의 physics에서 simulate physics 활성화 
- enable gravity 둥둥 떠다니는 상태
- Mass 기본적으로 false

## 3. object and references
- 1. object 
- object : 데이터와 기능의 집합체
- Actors : 레벨에 투입할 수 있는 오브젝트
- Component : Actors 에 들어가는 오브젝트
    - ex : static mesh component

- 2. references
- 구조체
- 주소 또는 메모리에서 이 오브젝트를 찾기 위해 가야할 위치
- 나중에 할거임 ㅇㅇ 일단 지금은 단순한 주소라는것을 인지
-  큐브르 선택후 레벨 블루프린트로 이동 > create a reference 선택 > 큐브의 주소를 알려주는것.

- 3. data pin
- data pin : 노드를 위한 입출력 데이터
- 블루프린트에서 볼 수 있는 레퍼런스의 푸른색 원
- 노드에서 왼쪽에 있으면 입력이고 노드가 다룰 수 있는 데이터라는 뜻, 오른쪽에 있으면 그 노드가 제공하는 데이터
- excution pin : 노드를 언제 실행할 지 결정
- 데이터핀은 노드로 무엇을 실행할지 정하며 실행핀이 실행 시간을 결정

## 4. adding impulse
- force는 정해진 시간동안 가해지는 반면 impulse 는 즉각적임
* Force = Mass * Acceleration
* IMpulse = Mass * Velocity Change
- bp 에서 space bar 검색
- 스페이스바를 눌럿을때에 대한 노드하나, 뗄때 반응하는 노드하나 총 두개가 존재
- static mesh component에서 시작한 노드로 impuse를 검색 add impulse 사용. 이것을 space bar와 연결
- z축의 impulse에 질량값의 100정도를 곱한값을 사용해보기
- val change : 질랴을 무시하고 내가 원하는 속력만 쓰도록 사용가능

## 5. blueprint class and instances
- detail창에서의 bp버튼을 누르면 프리팹같이 재사용할 수 있는 블루프린트 객체를 생성가능
- 대부분 BP_{obj_name} 식으로 네이밍 작성
- BP 객체가 에디터에서 프로퍼티를 변경하면 모든 instance에 대해 해당 속성이 변경됨
- simulate physics

## 6. spawning actors
- spawn actor 검색
- press 버튼에서 연결해서 생성
- 만들 bp클래스를 지정 드롭다운 박스를 사용해서 스폰할 물체를 선택
- transform > location, rotation, scale
- split struct pin 선택으로 위치 회전 스케일을 설정 가능
- return value pin > output of a node
- 우리가 생성한 오브젝트에 impulse를 연결 
- 오브젝트를 생성 > static mesh component를 가져오고 > 그 컴포넌트에 impulse를 추가

## 7. data types
- 진짜흔오야 이거는 모르면 안되는거 알지?