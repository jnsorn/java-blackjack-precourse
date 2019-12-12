# 블랙잭
우아한 테크코스 2기 프리코스 3주차 (2019.12.11~2019.12.17)

## 용어 정리
- **블랙잭(black jack)** 처음 받은 카드 두 장의 합이 21일 경우
    - Ace 한 장과 10, J, Q, K로 이루어진 카드를 받은 경우
    - 베팅금액의 1.5배를 돌려준다.
- **버스트(bust)** 카드 숫자의 합이 21을 초과하는 경우
- **힛(hit)** 처음 2장의 상태에서 카드를 더 뽑는 것
- **스탠드, 스테이(stand, stay)** 카드를 더 뽑지 않고 차례를 마치는 것
- **푸쉬(push)** 플레이어와 딜러가 무승부인 경우



## 기능 요구사항

1. 카드 초기화
    - 모양: heart, diamond, spade, club
    - 수: jack(10), queen(10), king(10), ace(1 or 11), 1~10
    - 모양x수 만큼의 카드가 존재한다. 

2. 게임에 참여할 플레이어의 이름을 입력받는다.
    - 예외 처리
        - 인원이 0명일 경우
        - 이름에 공백으로만 이루어진 경우 그 플레이어는 제외
        - 이름이 중복되는 경우
        - 이름이 "딜러"와 같은 경우

3. 플레이어들의 베팅금액을 입력받는다.
    - 모든 플레이어들을 순차적으로 돌면서 입력받는다.
    - 예외 처리
        - 숫자가 아닌 경우
        - 1보다 작은 경우

4. 카드를 2장씩 나누어 준다.

5. 카드 합계를 계산한다.
    - 카드의 숫자계산은 카드 숫자를 기본으로 한다.

6. 카드를 공개한다.
    - 대상 : 게임에 참여중인 모든 플레이어. 이때 딜러도 포함된다.
    - blackjack 판단

7. blackjack 판단
    - 플레이어
        - 해당 플레이어를 게임 참여자 list에서 제외시킨다.
    - 딜러(구현 중 수정 가능성 있음)
        - 딜러가 blackjack인 경우에 대한 명세가 없다.
        - 딜러가 할 수 있는 행동
            1. 아무런 행동을 하지 않는다. 즉, 무시한다
            2. 플레이어 패배
        - 이 프로그램에서는 딜러가 blackjack이면 플레이어는 패배한다.
            - 이유: 명세서에서 블랙잭과 21을 구분하기 때문에 플레이어가 추가 카드를 얻어도 21은 만들 수 있지만 블랙잭으로 만드는 것은 불가능하기 때문이다. 

8. 카드를 1장 더 받을지 묻는다.
    - 대상: 게임에 참여중인 플레이어와 딜러.
    - 딜러는 가장 마지막에 묻는다.
        - 플레이어
            - Y: N이 나올 때까지 같은 플레이어가 게임 진행
            - N: 다음 플레이어가 게임 진행
        - 딜러
            - 16점 이하면 1장의 카드를 추가로 받는다.
            - 17점 이상이면 추가로 받을 수 없다.

9. bust 판단
    - 플레이어
        - 해당 플레이어를 게임 참여자 list에서 제외시킨다.
    - 딜러
        - 그 시점까지 남아있던 플레이어들은 가지고 있는 패에 상관없이 승리한다.
    - 플레이어&딜러
        - 플레이어는 베팅한 돈을 다시 돌려받는다.
        - 해당 플레이어를 게임 참여자 list에서 제외시킨다.
        - 그 시점까지 남아있던 플레이어들은 가지고 있는 패에 상관없이 승리한다.

10. 카드를 공개한다
    - 대상: 모든 플레이어
    - bust판단

11. 최종 수익을 계산한다.
    - 대상: 모든 플레이어
    - blackjack
        - 플레이어 blackjack: 베팅 금액의 1.5배
        - 플레이어 & 딜러 blackjack: 0
    - bust
        - 플레이어 bust: - 본인 베팅금
        - 딜러 bust: 그 시점까지 남아있던 플레이어들은 가지고 있는 패에 상관없이 베팅 금액의 1배
        - 플레이어 & 딜러 bust: 0
    - 그 외의 경우: 플레이어와 딜러 중 21에 가까운 플레이어가 승리한다.
        - 플레이어 == 딜러: 0
        - 플레이어>딜러(21내에서): 베팅 금액의 1배
        - 플레이어<딜러(21내에서): - 본인 베팅금

---

용어 및 룰 참고 : [나무위키 블랙잭(카드게임)](https://namu.wiki/w/%EB%B8%94%EB%9E%99%EC%9E%AD(%EC%B9%B4%EB%93%9C%EA%B2%8C%EC%9E%84))