## 분기문: if

프로그램을 흐름을 조건에 따라 나누는 제어 구문

if의 기본형태

```c#
if (조건1)
{
	조건1을 충족했을 때 수행할 명령;
}
else if(조건2)
{
    조건1을 충족하지 않고, 조건2를 충족할 때 수행할 명령;
}
else
{
 	   조건1과 조건2 모두 아닐 때 수행할 명령;
}
```

위의 기본 구조에서 else if까지 들었지만 상황에 따라 조건이 하나라면 if 하나만 쓰면 된다.

특정 조건을 만족하는지 여부만 확인하면 되는 경우에는 if ~ else까지만

여러 개의 조건에 따라 흐름을 제어해야 하는 경우에는 else if 구문도 같이 활용하여 각 조건에 맞게 분기를 나눌 수 있다.



#### 실습1: if문을 활용하여 전투 구현하기

앞의 if ~ else 구문만을 이용하여 몬스터와 플레이어 간 전투 구현하기

전투는 update 영역이 아닌 start 영역에서만 진행하는 것으로 한다



##### 구현하기 전에 생각해야 할 것들

- 공격 조작은 어떻게 할 거야? 
  - 공격은 클릭 한 번으로 할까 
  - 클릭 한 번에 교대로 공격하게 할 지 
  - 플레이어만 공격하게 할 지
- 선공 판정: 매 턴마다 적과, 플레이어 둘 중 하나가 선공을 랜덤 지정 
  - 랜덤 방식은 어떻게 정할까? 
  - 랜덤 확률은 적과 플레이어 각각 1:1로 한다 
  - 턴이 종료되면 선공은 상대 캐릭터에게 넘어간다. 
- 서로 공격 한 번 씩 해야 하고
- 공격은 일반 공격, 크리티컬, 회피, 방어의 결과가 나올 수 있다.
- 일반 공격(회피나 막기가 발동되지 않았을 때 발생):  
  - 공격자의 공격력 - 방어자의 방어력
- 일반 공격 중에 확률에 따라 크리티컬이 발동한다
- 크리티컬이 발생할 확률은? : 캐릭터가 가진 크리티컬 발생 확률을 이용
- 크리티컬 데미지는?: 
- 한 쪽의 HP가 0이 되면 전투는 종료한다.
- 플레이어가 사망했을 때는 "게임 오버"를 출력한다.
- 적이 사망했을 경우에는 경험치, 골드를 얻는다.
- 플레이어의 HP가 50이하가 되면 힐링 스킬을 사용



예시)

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Test1 : MonoBehaviour
{
    int PlayerAtt = 50;
    int PlayerDef = 20;
    int PlayerHP = 1000;
    int MonsterAtt = 30;
    int MonsterDef = 10;
    int MonsterHP = 2000;
    int player_exp = 0;
    int player_gold = 0;

int PlayerDmg;
int MonsterDmg ;

// 진행에 앞서 플레이어와 몬스터의 공격력, hp, 방어력 등 정의
// 플레이어의 데미지와 몬스터의 데미지는 정수 변수로만 정의
    
private void OnMouseDown()

{ // 공격 진행 할 건데. 공격은 매 턴마다 랜덤으로 선공 지정
    
    int firstAtt = Random.Range(1, 3); 
    // 적과 1:1 확률을 가지기 위해
// 선공이 정해지면 서로 1번 씩 공격한다. 1 = 플레이어, 2 = 몬스터
    if (firstAtt == 1) // 플레이어 선공 처리 되었을 때
    {
 // 플레이어 공격: 플레이어 데미지 계산, 피격 이펙트, 플레이어 애니메이션, 피격 애니메이션, 데미지 출력, UI에서 HP 감소 
        // 몬스터 공격
        // 선공은 한 번만 지정하고 그 뒤로는 교대로 선공을 받는다.
        Debug.Log("선공 처리");
        MonsterHP -= PlayerDmg;
        Debug.Log("몬스터 체력 :" + MonsterHP);
        
        if(MonsterHP <= 0)
        {
            Debug.Log("와 잡았다");
            Destroy(gameObject);
            player_exp += 10;
            player_gold += 100;
        }

        PlayerHP -= MonsterDmg;
        Debug.Log("플레이어 체력:"+ PlayerHP);
            
        if(PlayerHP <=0)
        {
            Debug.Log("사망");
            Destroy(gameObject);
        }

    }
    else // 몬스터 선공 처리 되었을 때
    {
        Debug.Log("후공 처리");
        PlayerHP -= MonsterDmg;
        Debug.Log("플레이어 체력:"+ PlayerHP);
        if (PlayerHP <= 0)
        {
            Debug.Log("사망");
            Destroy(gameObject);
        }

        MonsterHP -= PlayerDmg;
        Debug.Log("몬스터 체력:"+ MonsterHP);
        if (MonsterHP <= 0)
        {
            Debug.Log("와 잡았다");
            Destroy(gameObject);
            player_exp += 10;
            player_gold += 100;
        }

    }

}

// Start is called before the first frame update
void Start()
{
    PlayerDmg = PlayerAtt - MonsterDef;
    MonsterDmg = MonsterAtt - PlayerDef;

// 게임이 실행되면 플레이어의 데미지와 몬스터 데미지를 계산

}

// Update is called once per frame
void Update()
{
    
}

}
```



## 반복문 for 구문

어떤 일을 조건이 충족하는 동안 반복시키기 위해 사용

for 문과 while문을 많이 사용 (foreach도 사용하는데 이건 나중에)



1. ### for 문?

예를 들어 "Hello World"를 출력하는 명령을 13번 만들어야 한다면?

같은 명령을 여러 번 만들어야 한다면 만들기도 어렵고 정확하게 그만큼 작성했는 지 확인 불가하여 오류 발생 할 수 있다.

이런 경우 정해진 횟수만큼 반복하라고 정의해줄 수 있는 구문이 for문이다.

#### 1) for문의 기본형태

```c#
for(초기값; 반복 조건; 초기값 변화)
{
반복할 명령어 
}
```

초기 값 : 처음 카운트를 시작할 값의 정의, 보통 정수형 값

반복 조건 :  반복이 얼마나 이루어져야 할 지 판단하는 순간

초기값 변화: 반복할 명령어를 1회 실행한 후 초기값을 어떻게 변화시킬 것인가를 정의

```c#
 void Start()
    {
        for (int i = 0; i < 13; i++) // int i = 0 <-- 초기 값으로 사용할 로컬 변수 i										를 정수형으로 만들고 0을 대입해 초기화 해라
            						// i<13 <-- i값이 13보다 작으면 계속 반복해라
									// i++ <-- 중괄호 안의 명령들을 다 처리하고 나면 										처리해야 할 명령
            						// i++을 i--로 만들면 i는 항상 i<13을 충족하여 무										  한 루프가 발생
        {
            if (i % 2 == 1)
            {
                Debug.Log("Hello World" + i);
            }
        }
    }
```

제어 문 안에 제어 문을 또 쓸 수 있다.

##### 주의사항: 반복조건을 탈출할 수 있는 방법이 없으면 무한 루프가 발생한다

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Study10 : MonoBehaviour
{ int a; // 각 단은 1~9까지 곱한 값을 출력한다
  int b; // 1~9까지 곱한 값을 출력하면, 1 증가한 단수를 출력한다. 2~9단까지 출력한다
  int c = 0;
        //구구단의 모든 결과 값의 합? --> 숫자 0에서 구구단 하나가 실행될 때마다 결과값은 더해준다
        // 구구단의 모든 결과값 숫자 중 홀수는 몇 개니? --> 홀수는 결과값을 나눠서 나머지 값이 1이 나오면 홀수 --> 홀수 일 때만 카운트 숫자를 올린다.
  int sumTotal = 0;

// Start is called before the first frame update
void Start()
{

    for (b = 2; b < 10; b++)
    {
        for (a = 1; a < 10; a++)
        {
            Debug.Log(b+"x" + a + "=" + b * a);
            sumTotal += b * a; // 모든 결과 값을 더하려면 매번 같은 값을 더해준다.

            if (b*a%2 == 1) // 결과값이 홀수면
            {
                c++; // 갯수를 증가시킨다
            }
        }
        Debug.Log(sumTotal);
        Debug.Log(c);
    } 

}

// Update is called once per frame
void Update()
{
    
}

}


```

예시: 11연차 가차

1. 큐브 클릭 시 총 11개 카드 뽑혀야 : 큐브를 클릭하는 기능
2. 3성에서 6성까지 카드가 뽑힐 수 있다: 11개의 카드가 뽑히는 기능(11개의 각 카드는 등급이 정해져 있다.)
3. 각 확률은 3성(70%), 4성(20%), 5성(9%), 6성(1%) : 확률을 정하는 기능 / 3~6성 카드를 만드는 기능 / 11개의 카드는 어떤 카드가 나왔는지 보여줘야 한다
4. 최소한의 1장의 카드는 5성 이상 보장: 보장해야 할 카드 수를 뺀 나머지 카드 중에 5성이 한 개도 없으면 나머지 카드는 5성 이상만 확률 계산을 해야 한다(10장까지 5성 이상의 개수를 체크하고 갯수가 0이면 11번 째는 5성 이상이 나와줘야 한다)
5. 작업할 할 내용을 세분화(분리) 

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Gotcha : MonoBehaviour
{
   int Threestar = 0;
   int Fourstar = 0;
   int Fivestar = 0;
   int Sixstar = 0;
   int randomGrade;
    private void OnMouseDown()
    {
       

    for (int a = 1; a < 12; a++) // 11개의 카드를 뽑는 기능
    {
        if (a == 10 && Fivestar + Sixstar == 0)
        {
        RandomCard(1, 11);
        }// 5성 이상 카드가 단 하나도 안 나왔을 때
        RandomCard(1,101); // 카드를 확률에 따라 만들어 주는 함수
    }
    Debug.Log("일반 카드 :" + Threestar + "/" + "히기 카드 :" + Fourstar + "/" + "영웅 카드 :" + Fivestar + "전설 카드 :" + Sixstar);

}

   void RandomCard(int min, int max)
    {
        int randomGrade = Random.Range(1, 101); //확률을 만들어주는 기능
        if (randomGrade > 99)
        {
            Sixstar++;
            Debug.Log("오~~~! 전설 카드~~!");
        }
        else if (randomGrade > 90)
        {
            Fivestar++;
            Debug.Log("영웅 카드");
        }
        else if (randomGrade > 70)
        {
            Fourstar++;
            Debug.Log("히기 카드");
        }
        else
        {
            Threestar++;
            Debug.Log("일반 카드");
        }


        

}
```



