## 17. function
- BP에서 노드들을 선택 한 후 함수로 묶기를 사용하면 예쁘게 묶어줌
- 내 블루프린트 창에서(level bp에서 켤수있음) 함수를 추가해서 직점 만들기 가능
- 오른쪽에 입/출력값을(input/return)노드를 만들어서 level bp에서 입출력을 받아올수있게 할 수 있음

## 18. pure function
- side effect : 눈에보이는 효과가 있는 함수
- pure function : 뭔가를 가져오거나, return만 하는 함수들(side effect가 없는 함수)

## 19. member function
- bp로 작성한 코드가 데이터와(프리팹) 함께 공존할수있게끔 해줌.
- 특정 인스턴스에 함수를 만드는 것 
- bp객체를 선택하고 blue print창을 열어 함수창에서 함수를 추가
- 멤버함수 > 클래스의 함수로 항상 특정 인스턴스에서 호출되는 함수
- 멤버함수에서 self를 가져와 자신의 속성값을 알수있음
    - get display name을 이용해 자신의 이름을 출력