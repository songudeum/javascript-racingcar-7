# javascript-racingcar-precourse

## 기능 요구 사항

-   주어진 횟수 동안 n대의 자동차는 전진 또는 멈출 수 있다.
-   각 자동차에 이름을 부여할 수 있다. 전진하는 자동차를 출력할 때 자동차 이름을 같이 출력한다.
-   자동차 이름은 쉼표(,)를 기준으로 구분하며 이름은 5자 이하만 가능하다.
-   사용자는 몇 번의 이동을 할 것인지를 입력할 수 있어야 한다.
-   전진하는 조건은 0에서 9 사이에서 무작위 값을 구한 후 무작위 값이 4 이상일 경우이다.
-   자동차 경주 게임을 완료한 후 누가 우승했는지를 알려준다. 우승자는 한 명 이상일 수 있다.
-   우승자가 여러 명일 경우 쉼표(,)를 이용하여 구분한다.
-   사용자가 잘못된 값을 입력할 경우 "[ERROR]"로 시작하는 메시지와 함께 Error를 발생시킨 후 - 애플리케이션은 종료되어야 한다.

## 로직 순서

1. 경주할 자동차 이름을 입력한 문자열을 ,기준으로 분리해서 배열로 저장(객체로 할 지는 좀 더 고민)

-   자동차 경주이므로 자동차가 한 대면 에러 반환
-   5자 이하의 이름이 아닐 경우 에러 반환

2. 몇 번 이동할 건지 받아와야 함

-   숫자가 아닌 문자면 에러 반환

3. 유저가 입력한 이동 횟수를 바탕으로 자동차마다 무작위 값을 구해서 전진인지 멈춤인 지를 각 턴마다 저장함

-   while문으로 결과 배열의 길이가 이동 횟수만큼까지만 실행되도록 함
-   무작위 값을 구해서 4이상이면 해당 자동차가 key인 value에 1을 더해줌
-   결과를 저장할 객체의 배열에 자동차의 전진 결과값이 담긴 객체를 push함

4. 저장된 결과값을 화면에 출력할 수 있는 문자열로 바꿔줘야 함

-   게임 결과에서 최종 우승자가 누군지 알아낼 수 있어야 함
-   게임 결과를 바탕으로 출력 문구들을 만들고 화면에 출력해야 함

## 구현해야 할 기능

1.  입력값을 받아서 자동차 목록을 만들어줄 RaceInfo class

-   field는 자동차 이름에 대한 입력값을 저장할 carNames와 이동횟수에 대한 입력값을 저장할 round 존재
-   setter로 ,로 구분했을 때 자동차가 한 대거나 5자 이하의 이름이 아닐 경우 에러를 반환해야 함
-   자동차 이름은 공백을 제외했을 때 중복이 아니어야 함
    ex\_"하치" or "모몽가나쁜넘, 치이" or "치이-하치" or "치이,치이"
-   ","을 기준으로 구분해서 자동차 이름들을 string[]로 저장함
-   이동횟수또한 setter로 숫자가 아닌 경우 에러를 반환해야 함
    ex\_"3번" or "일"
-   getter에서는 가공된 carNames와 round를 반환할 수 있도록 함

2.  RaceInfo에서 나온 자동차 이름 배열과 이동횟수를 받아서 게임 결과를 도출할 Race class

-   field는 자동차 이름 배열을 저장할 carNames와 이동횟수 저장할 round
-   배열로 온 자동차 이름을 기반으로 이름이 key가 되고 value가 0이 되는 객체가 들어있는 배열을 초기값으로 셋팅함
-   초기값을 기반으로 while문을 결과의 length가 이동횟수랑 같아질 때까지 반복함 자동차마다 무작위 값이 4이상이면 전진이면 value에 1을 더해줌
-   위의 과정을 모든 자동차가 진행되면 결과값을 배열에 push함

3.  경기 결과에 대한 데이터를 화면에 출력할 대사를 만들어주는 Script class

-   field는 Race class에서 나온 경기 결과가 든 배열을 저장하는 raceResult 존재
-   Race class에서 받은 각 단계별 결과값이 든 객체의 배열을 바탕으로 경주 결과 문자열을 생성함
-   최종 우승자가 누구인지 알아내서 최종 우승자 결과 문자열을 생성함
