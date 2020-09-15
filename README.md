# model_checker_theseus
소프트웨어 공학 기말 과제 : 퍼즐게임을 model checker(smv)를 이용해서 자동으로 해결하는 프로그램 만들기

# 과제 설명

Theseus and the Minotaur 라는 퍼즐 게임을 model checker 중 하나인 NuSmv를 이용해서 자동으로 해답찾는 코딩하기.

## 게임 규칙

- 매 턴, 테세우스는 최대 1칸, 미노타우르스는 최대 2칸 까지 움직일 수 있음.
- 테세우스가 탈출구로 이동하면 승리.
- 미노타우르스는 항상 다음과 같이 움직임:

  1. 미노타우르스가 가로로 움직여 테세우스와 가까워질 수 있는가? 그렇다면 2번, 아니면 3번.
  2. 테세우스를 향해 가로로 한 칸 움직인 후 5번.
  3. 미노타우르스가 세로로 움직여 테세우스와 가까워질 수 있는가? 그렇다면 4번, 아니면 5번.
  4. 테세우스를 향해 세로로 한 칸 움직인 후 5번.
  5. 한 턴 종료
  
 ## 과제를 하기 위해 필요했던 지식
 
 - 약간의 smv 코딩에 대한 지식 : 기존에 알고 있던 어셈블리어와 비슷함
 - model checker에 대한 지식 : model checker은 finite state model에 대해서 주어진 specification을 만족하는지 안하는지 T/F로 알려주는 프로그램.
 - 자동적으로 해결하기 위해 spec 6가지 명세에 대해서 알기 (G,F,U,X,A,E)
    - G : global - 모든 것에 대해 만족
    - F : future - 미래에 언젠가 한번은 만족
    - U : Until  - 어느시점 전까지는 항상 어떤 것을 만족
    - X : neXt - 바로 다음상태에서만 만족
    - A : for the all path
    - E : there is Exist a path
    
 ## solution
 
 - 미노타우르스와 테세우스가 움직일 수 있는 모든 칸을 수로 표현 - 탈출구는 999
 
 ![Inkedlv87_LI](https://user-images.githubusercontent.com/52481037/93231368-a2c13880-f7b3-11ea-85f0-5c129933d349.jpg)
 
 - 움직일 수 있는 방향 (r,l,u,d)을 지정한 뒤, 벽으로 막혀있는 부분을 명시함
 
 - 테세우스와 미노타우르스(각각 red, black 변수)의 움직임의 차이(1턴의 차이)를 turn이라는 변수로 지정
 
 - case문을 이용하여 벽이 아니고 움직일 수 있다면 다음 상태로 이동시키는 코드 작성. 만약 red가 goal에 도착했다면 999로 보내버림
 
 - 검증하고자 하는 명세에 대해 기술하기 : G(F((red != 999)|(red = black)))
 
 - 명세에 따라 검사하고 False가 나온 후 왜 false가 나왔는지 trace하는 description을 txt로 옮기기 - 그것이 바로 퍼즐의 해답
 
 ## level 2와 level 87 smv로 코딩 후 명세로 나온 경로 표시
 
 
![2판경로](https://user-images.githubusercontent.com/52481037/93232703-27f91d00-f7b5-11ea-9c48-bf61e8100264.jpg)

![87판경로](https://user-images.githubusercontent.com/52481037/93232654-1ca5f180-f7b5-11ea-8113-e93ad2e7880d.jpg)
