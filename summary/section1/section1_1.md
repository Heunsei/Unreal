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
- bp간 연결 끊으려면 alt + 클릭
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

## 8. pawns and actor position
- F8을 길게눌러서 카메라를 옮겨 확인해보면 까만 구체가 보임, 이것을 pawn이라고 부름
- 게임을 플레이하는 말이라는 뜻, 게임 월드에서 플레이어의 물리적 묘사를 표현
- 기본적으로 씬 안에 폰을 스폰하고, Player start에 배치
- 레벨 bp로 이동해 빈곳을 우클릭하고 pawn을 검색하면 get player pawn이 있음
    - 기본적으로 실행핀은 없지만, 입출력 핀은, 존재함
    - 싱글플레이에서 인덱스 0은 자기 자신을 의미함
    - pawn output 핀을 이용해 get actor location을 이용해 위치를 받아옴
    - 새 반환색은 노란색의 벡터반환 output 이것을 spawnactor 의 location에 연결
    - 그리고 impuls 방향을 z을 없애고 앞 방향을 뜻하는 x축을사용. 이떄 방향을 잘 확인해서 양수값을 줄지 음수값을 줄지 잘 확인

## 9. rotation
- 레벨 블루프린트에서 plyer pawn 에서 get actor rotation을 사용
- 이것을 spawn actor의 transform rotation으로 연결
- 카메라의 회전과 actor pawn의 회전을 별개로 취급함
    - 그회전을 반영하기위해 player pawn의 get control rotation을 사용

## 10. get forward vecotr
- 위에서 작업한 대로 하면 발사되는 발사체는 카메라 회전의 영향을 받게 됨.
- 전방벡터는 회전한 x방향, 회전한 다음 x축을 바라보는 방향
- 그 벡터의 길이는 항상 1임 따라서 충격량을 구하려면 우리가 원하는 값으로만 곱하면됨
- 새로운 발사체에 쿼리를 줌으로써 회전을 구현
- spawn actor 또는 static mesh component에서 get forward vector를 검색, get actor forward vector를 가져와서 add impulse에 넣어줌
- get actor forward vector에서 return 값에서 multiply 를가져와 이것을 사용 
    - 두번쨰 핀(노란색 아래)을 우클릭하면 convert핀으로 float으로 변환 그 값을 add impulse에 넣어줌

## 11. Geometry brushes
- file > new level > template default > create
- tool bar > Place Actor's panel > geometry
- 만들면서 지오매트리를 구성하거나, 빼면서 조각 하기 가능
- outliner의 설정에서 box geometry를 수정 brush settings에서 크기수정을 추천, cm단위니까 0을 더붙여서 크기조절
- box brush를 하나 더 만들고, 이전의 박스를 좀 더 크게
방금 생성한 box는 설정에서 brush type을 subtract로 변경
- ctrl + s 로 저장 루트폴더에서 main으로 설정
- settrings > project settings > maps & modes 
    - editor startup map, game default map을 설정  
- alt 를 누른 채 position 핀을 움직이면 복사가능
- outliner에서 move to > create new folder > 오브젝트 묶기 가능

## 12. materials and lighting
- bp창에서 ctrl + a , ctrl + s로 복사 후 새로운 레벨로 가서 붙여넣기
- light source를 회전시켜 그림자의 방향 조절가능

## 13. actor components
- 지지대에 선반을 올려도 하나의 아이템처럼 구성되어 있지 않음
- content에서 화면으로 드래그가 아닌 detail의 meshcomponent로 넣어줌 > static mesh components의 자식으로 설정
- 이 때 자식의 position은 부모를 기준 상대적으로 표시

## 14. collision meshes
- 배럴을 쌓아 올렸을 때 퉁하고 튕겨져 올라감 > unreal에서 처리하는 물리 효과 때문 좌상단 lit을 틀러서 탭에서 구조 및 mesh 확인가능
- content에서 object를 더블클릭하면 해당 오브젝트의 mesh확인가능
- 툴바의 collision 버튼에서 remove collision을 클릭하면 모든 충돌을 제거 > 땅을 뚫고 떨어져버림 > 충돌을 못하니까
- 툴바의 10DOP-Z simplified collision
    - 4개의 z축 정렬 모서리가 기울어진 box collision mesh를 생성

## 15. Variables
- bp를 이용해 생성
- level bp > windows > My Blueprint > variables
- ammo > int로 생성
- default값 생성을 하려면 왼쪽 위 compile > detail창에서 default value 설정
- my bp창에서 bp로 변수를 그대로 드래그해서 level bp에서 사용가능 
    - get > 값을 가져오고  (ctrl 누른채 드래그)
    - set > 값을 수정     (alt 누른채 드래그)
- 언제 set을 할지 알려주는 실행핀이 필요
- begin play에서 처음으로 setting 하기
    - print string(게임시작 안내)핀 다음 새로운 print string핀 생성
    - get ammo(ctrl)의 return 값을 print string의 파란 노드로 연결 
    - subtract 검색후 노드 생성 (ctrl)로 ammo를 가져오고 변수연결
    - 빈칸에 숫자 1 입력 후 return 핀에 set ammo를 가져옴 
    - > 모양 실행핀을 add impulse에서 끌어서 연결해줌
    - 그후 print string을 가져와 return값을 연결하고 실행핀을 연결

## 16. booleans and branches
- branch node -> 분기노드
- greater 검색 및 추가
- ammo변수를 ctrl클릭으로 끌어온뒤 분기노드에 연결
- greater노드에서 branch노드를 추가 
- space bar의 실행핀을 branch에 연결
- true를 actor spawn에 연결
- false에 print string으로 out of ammo 출력
