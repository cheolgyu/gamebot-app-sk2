# gamebot-app-sk2
세븐나이츠2
```

자동카테고리
1. 시나리오진행
스마트키가 동작하지 않는다면 클릭해준다. 
스킵이 나오면 스킵해주고 스킵팝업창도 확인눌러준다.
한번하고 안하는 튜토리얼이라던지 도움팝업창같은 경우는 제외한다.
튜토리얼이 나오면 취소를 누른다?



2. 방치형 필드
방치토벌쾌에서는 가방이 가득차면 멈추는데
가방이 어느정도 차면 일반템을 분해시켜주기
방치토벌진행은
절전모드에서 가방의 수가 40번대라면 동작하는데
자리가 있다. 무슨자리냐면 인식되는 순서의 자리.
방치토벌쾌진행을 설정에서 선택하였다면?
방치토벌쾌 순서대로 인식을 대기한다. 예로 
방치토벌쾌의 필요한 기능은
가방의 채움정도를 인식하고 
가방을 누르고
가방의 분해를 누르고
가방의 일반을 선택하고
갑방의 분해버튼을 누른다.
이 순서대로만 클릭한다.
인식여부와 상관없이 이 순서대로 판을 짜놓는것이다. 그래서 
이 순서대로 들어온 인식정보를 가지고 판에 놓아서 방치토벌쾌진행 기능을 수행한다.
클릭틀 만들고 인식된것을 넣어 클릭틀이 다채워지면 비움한번이 성공한것이다.

+
부가적으로 비움 프로세스 후에 절전모드로 가면좋고 비움 프로세스가 끝난후에도 가득이 어느정도 가득 찼다면 카카오톡 개인메세지나 메일 보내기
방치토벌쾌 진행중 사망. ==> 메일발송.
펫 엑티브스킬 사용

틀만들기. frame
frame 만들기.

가방이 가득차다- 메인(빨강색 퍼센트),절전화면(빨강색 텍스트) 
절전이면 좌->우 스와이프 
메인화면.가방 아이콘
가방화면.타이틀
가방화면.분해버튼
가방화면.분해등급-일반,고급,희귀
가방화면.분해버튼
가방화면.팝업창.분해버튼
분해결과.터치하여 닫기
홍
펫.액티브 클릭(모든펫 3분).
메뉴
메뉴.절전모드

frame은 안드로이드에 있어야하고 
frame은 기능별로 나누자.
채움인식
분해화면가기
분해화면처리하기
분해화면처리후에도 채움이 인식된다면 alert 
절전모드가기

안드설정화면에-비움카운트 노출 
그런데 인식 쓰레드에서 반환된 값으로 
frame배열에 채워 넣는데 .. 
아무래도 연속으로 채움이 인식되었다고 온다. 채움 인식될 떄마 틀배열을 생성한다면 망한다.
그러면 채움인식 되면 물이 켜지면 어떤가? 3분간 활성화가 된다. 첫번째 채움이 온다음 3분간 활성화 되고 
채움인식 올때마다 3분간 채움프로세스가 활성화된다.
첫 채움이 도착시각 +3분 간 유치되고 유지기간에 들어오 채움인식은 무시된다.  분해결과인식이 오면 채움활성시간은 0으로 된다.
인식번호가 전체채움,절전채움잉 오면 도착시간이 채움동작시각 변수에 저장되고 그 다음 채움이 오면 채움도착시각과 채움동작시각 비교하여 3분이 넘어가면 무시한다.

전체채움이면 전체채움좌표로 클릭이벤트 발생시켜 가방화면으롤 이동한다. 
분해버튼이 인식되면 클릭하고 
사용자가 선택한 일반, 고급에 따라 
일반이 인식되면 일반클릭하고 일반클릭변수에 현재 시각 넣고 고급이 인식되면 고급활성화변수에 현재시각넣고 클릭하고 일반과 고급이 인식이 들어오면 활성화변수의 값이 있으니 무시한다.
그리고 분해이 인식되면 분해버튼을 누른다.
분해팝업창이 나오고 분해팝업창의 확인이 인식되면 클릭이벤트를 발생시키고 정말분해시각 변수에 저장한다음 10 초안에 분해결과가 인식안되면 분해를 다시 전해한다. 이유는 새 아이템이 들어오면 분해결과로 안넘어간다.
분해버튼-우가 여전히 인식된다면 정말분해시각이랑도 비교해 봐야한다.  이유는 새아이템 등장으로 분해결과로 안넘어가니깐
분해.우가 인식된다면 분해.우의 인식시각과 변수중 정말분해시각과 비교해봐서 
분해결과이후 분해활성상태로 넘어간다. 분해활성상태란 분해.좌를 클릭한 상태인데 이때는 일반,고급이 인식되는 상태이다. 
그러므로 일반,고급,분해.우가 인식되어 들어온다면 분해결과시각 변수의 값과 비교해봐야한다. 이유는 처음 인식된것과 분해결과후에 인식된것과 차이를 모르기 때문에
분해진행상태를 인식여부에서는 모르기 때문이다.
분해진행상태롤 변수로 저장하고 있어야 한다.  
첫 채움인식후 - 분해.좌 -  분해대상(사용자변수) - 분해.우 - 정말분해 - 분해결과 - 홈 - 메뉴 -   절전모드
            클릭      클릭                    클릭     클릭       클릭       클릭  클릭   클릭         클릭   
                                                            정말분해중 뉴아이템 등장시 분해대상 부터 다시선택


방치형필드 구조체를 만들면

class 방치형필드
var 채움인식,분해.좌
set 채움인식(
    timer 180s 
)
set 분해.좌(
    timer 60s 
)

    inner class 분해(분해대상)
    var 분해대상,분해.우,정마라분해,분해결과
    





인식 번호에 따라 전체화면의 채움이나 아니면 절전모드의 채움 (가방의 채움은 빨강색이 안나오므로 인식안됨)이 결정나고 
절전모드의 채움이면 
스와이프-가방클릭-가방화면.분해-가방화면.분해.일반-가방화면.분해-팝업창.정말분해-분해결과-홈-메뉴-메뉴.절전모드
전체화면의 채움이면
         가방클릭-가방화면.분해-가방화면.분해.일반-가방화면.분해-팝업창.정말분해-분해결과-홈-메뉴-메뉴.절전모드













인식대상(튜토리얼 전)


=============기본기능=============
전체화면.SKIP
전체화면.SKIP-팝업창.확인
전체화면.NEXT


홈.NEW.가방버튼
(가방화면.기본케릭의 장비화면)
(가방화면.맨왼쪽부터 케릭터 클릭하여 캐릭장비화면 노출 필요함.)
가방.<캐릭>.활성아이템표시
가방.<캐릭>.활성아이템표시.자동장착버튼
가방.<캐릭>.활성아이템표시.자동장착버튼.팝업창.적용O.확인버튼
가방.<캐릭>.활성아이템표시.자동장착버튼.팝업창.적용X.확인버튼
가방.홈버튼


<이동,사냥,대화,수집,튜토리얼,시나리오>
홈.스마트키<>.비활성 
홈.스마트키<>.활성
홈.스마트키<튜토리얼>.활성-팝업.진행버튼
홈.스마트키<시나리오>.활성-팝업.다음장 이동
홈.스마트키<시나리오>.활성-팝업.방치형 필드이동

전체화면.팻액티브스킬

=============부가기능=============
홈.NEW.우편
우편.탭.NEW
우편.탭.NEW-받기
우편.탭.NEW-받기.케릭수령권 이면 캐릭선택창 이동됨.......우편 NEW 는 취소로..


전체화면.피업음(빨강 테두리) VS 공격범위
전체화면.귀환
죽으면.팝업창.귀환버튼


=============튜토기능=============
튜토리얼-미니대화창(우선순위1)
튜토리얼-미니클릭(우선순위0,원형모양클릭(라벨링 난이도 최상))

홈.팝업창<팀변경>.진행
홈.팝업창<정보>.닫기
홈.팝업창<광고>.닫기


=============일일도전=============
<골드,영혼석,엘릭서,룬,경험치>
싱글던전.스와이프
싱글던전.홈버튼
싱글던전.입장가능
싱글던전-<>화면.싱글도전

무한의탑.완료.화면터치 시 다음화면으로 넘어갑니다.
무한의탑.완료.화면터치 시 다음화면으로 넘어갑니다.무한의탑화면.홈버튼


```
