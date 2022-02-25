0. complexity 표기법 (그림 첨부)
 complexity "abc"
 a : operator, 1 - multiplication, 2 - division, 3 - exponential
 b : 첫번째 항, 0 - red, 1- green
 c : 두번째 항, 0 - red, 1 - green

1. Session_atari_pygame_bf_complexity.py
 추가한 DS
 temp_seq : integer list. consisting element must be in {0, 1, 100, 101, 110, 111, 200, 201, 210, 211, 300, 301, 310, 311}
 reward_sess_2 : reward_sess 와 동일한 기능인듯. 각 세션 별 유효 점수 저장
 reward_tot : 각 세션 별 유효 점수 누적 합
 order : 1이나 2 값 가짐. 1이면 항1에 해당, 2이면 항2에 해당한다는 뜻. render() 안에 변수로 들어감

 수정한 호출방식
 env.render(prev = prev_reward, seq = render_seq,  game = block, order = order)
 prev_reward : reward_sess_2 통해 구함
 render_seq : 현재 complexity + UI에 나타낼 5개의 complexity 까지 자른 list
 game : 게임별로 점수 가리는 위치 달라서 block을 인자로 넘김
 order : order

 *참고
  현재는 temp_seq의 element 다 빠지면 루프 break 하도록 해놓음 (next game으로 넘어가지 x)

2. environment.py
 수정한 함수
 1) render() 
 인자값 늘어남. 대부분이 SimpleImageViewer 생성자에 그대로 전달.

 2) step()
 reward>0 일 때 rendering.py에 있는 simpleimageviewer class 의 update 함수 호출하여 UI에 반영

 3) close()
 return값 생김. rendering.py에 있는 simpleimageviewer class 의 close 함수 호출하고 output으로 받은 점수 return

3. rendering.py
 수정한 함수
 1) get_window(width, height, display, **kwargs) 에 fullscreen = True 추가함

 2) class SimpleImageViewer(object) 대거수정
 이미지 경로 변경해야 됨
 UI 상에 나타내는 함수 포함. 그림이나 그림 위치 등 여기서 수정해야
 연산함수 포함. 계산 방식 변경시 여기서 수정해야
 구체적인 기능은 주석으로 설명 써놓았으니 읽어보면 될듯!