# C# 스크립트의 시작 2

### 변수의 연산

1. C# 스크립트의 연산자

가감승제(+, -, *, /, %)등을 계산하는 연산자를 산술 연산자라고 한다

정수형은 정수형을 나누다 보면 결과값이 소수점이 발생하는 경우가 있음

정수형끼리만 연산을 하면 소수점을 버리고 정수형으로 만들어 버림



```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Study06 : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        int numA = 10;
        int numB = 3;
        int numC;
        float numD;
        int numE = 10;

        numC = numA + numB;
        Debug.Log(numC);
        numC = numA - numB;
        Debug.Log(numC);
        numC = numA *numB;
        Debug.Log(numC);
        numC = numA / numB;
        Debug.Log(numC);
        numC = numA % numB;
        Debug.Log(numC);
        numD = 1.0f * numA / numB;
        Debug.Log(numD);
// 대입 연산자는 오른쪽의 값이 계산이 다 되고 난 후 왼쪽에 값을 넣는다
// 그래서 정수형끼리 계산한 값은 이미 정수형으로 값이 정해져서 float형인 numD에는 3만 넘어오게 된다
// 이를 방지하기 위해서는 1.0f를 미리 곱해서 float형으로 변환할 수 있다.
		numE = numE + 5;
        Debug.Log(numE);
        numE += 5; // +=와 같이 -=, *=, /=도 사용 가능
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}

```

증감 연산자

1씩 증가하거나 감소하는 경우 ++(증가연산자), --(감소연산자)로 표기 가능

```c#
numE++; // numE = numE +1; 과 동일, num += 1;과도 동일
```

2. 문자열의 계산

```C#
 string strA = "Hello";
        string strB = "World";
        string message = strA + strB;
        Debug.Log(message);

  strA += strB; // 문자열은 += 연산자만 사용 가능
  Debug.Log(strA);
```

```c#
string strC = "My Level is";
int MyLevel = 233;
message = strC + MyLevel; // 문자열과 숫자가 더해지면 숫자가 문자열로 변환
Debug.Log(message);
Debug.Log(MyLevel.ToString()); // 숫자를 강제로 문자로 변환도 가능(변환해서 참조해주세요)
```



## 함수의 이해

### 함수 = 클래스 내부의 함수를 메소드라고 한다. 

### 즉, 함수 = 메소드



여러 명령어들의 묶음을 하나의 일로 추상화해서 사용하는 것

예를 들면, 수업 중에 필기 하기 / 설명 듣기 / 실습 하기 등의 여러 과정이 반복되면 이것을 "수업 진행"이라는 하나의 명칭으로 추상화할 수 있다.

그러면 "수업 진행"이라는 함수를 만들고 그 안에 필기, 설명, 실습의 과정을 정의하여 필요할 때마다 "수업 진행"이라는 함수를 실행하려 여러 명령을 동시에 수행할 수 있다.

기획을 할 때도 기본적으로 추상적으로 대상을 만들고 세부적인 것들을 정의한다. 속성에 해당하는 것들을 "변수"라는 것을 이용하여 세부 정의를 하고 행동에 해당하는 것을 이용하여 세부 정의를 한다.

전투 기획을 한다면 우리는 공격하기, 스킬 사용하기 등으로 추상적인 것들을 대상화한다

각 추상화된 대상을 세부적인 구현 방향을 설계한다



예를 들어, 공격하기하고 하면

1. 공격 모션 취하기
2. 피격 판정하기
3. 데미지 산출하기



피격 판정하기는 

​		1) 공격자의 명중률 계산

​		2) 피격자의 회피율, 막기 확률 계산

​		3) 크리티컬 판정 계산

​		4) 피격 이펙트 출력

​		5) 피격 모션 출력



데미지 산출하기도

​		1) 공격자의 공격력 계산하기(스탯 값 계산, 장비 값 계산, 버프 값 계산 등)

​		2) 방어자의 방어력 계산하기 (스탯 값 계산, 장비 값 계산, 버프 값 계산 등)

​		3) 공격력과 방어력의 감산 처리 (얼마만큼 HP를 감소시킬 것인지 계산)

​		4) 데미지 숫자 출력



```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Study06 : MonoBehaviour
{
    int PlayerAttack = 100;
    int PlayerSword = 50;
    int MonsterDef = 30;
    int MonsterHP = 1000;
    int PlayerDamage;
    int AttackResult;


    // Start is called before the first frame update
    void Start()
    {  
        Debug.Log("몬스터 HP :" + MonsterHP);
        Debug.Log("첫번째 공격");
        PlayerDamage = PlayerAttack + PlayerSword;
        Debug.Log("플레이어 공격력:" + PlayerDamage);
        AttackResult = PlayerDamage - MonsterDef;
        Debug.Log("몬스터가 받은 데미지:" + AttackResult);
        MonsterHP -= AttackResult;
        Debug.Log("몬스터 HP" + MonsterHP);
    }

    // Update is called once per frame
    void Update()
    {
       
    }
}
```



이 방법으로 했을 때 문제점

1. 공격에 크리티컬 판정이나 보스 데미지 등을 추가하고 싶을 때 모든 코드를 다 찾아서 일일이 수정해야 된다

2. 오타로 인한 엉뚱한 결과가 나올 수 있다

3. 그래서 공격에 해당하는 기능을 하나의 함수로 만들어 놓으면 공격에 해당하는 하나의 함수로 만들 수 있다.

   

```c#
 void Attack()
        {
            PlayerDamage = PlayerAttack + PlayerSword;
            Debug.Log("플레이어 공격력:" + PlayerDamage);
            AttackResult = PlayerDamage - MonsterDef;
            Debug.Log("몬스터가 받은 데미지:" + AttackResult);
            MonsterHP -= AttackResult;
            Debug.Log("몬스터 HP" + MonsterHP);
        }
```

2. 함수의 기본 표기

반환데이터타입 함수명(매개 변수)  *매개 변수 = 파라미터, 보조 변수

{ 함수의 범위 산정

​	함수가 호출되면 실행해야 되는 명령어 묶음들

​	return 반환 값;

}

함수도 변수와 마찬가지로 어디에 정의되었느냐에 따라서 사용 범위가 정해진다



예시)

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Study06 : MonoBehaviour
{
    int PlayerAttack = 100;
    int PlayerSword = 50;
    int MonsterDef = 30;
    int MonsterHP = 1000;
    int PlayerDamage;
    int AttackResult;

// Start is called before the first frame update
void Start()
{
    Debug.Log("몬스터 HP :" + MonsterHP);
    Debug.Log("첫번째 공격");
    PlayerDamage = PlayerAttack + PlayerSword;
    Debug.Log("플레이어 공격력:" + PlayerDamage);
    AttackResult = PlayerDamage - MonsterDef;
    Debug.Log("몬스터가 받은 데미지:" + AttackResult);
    MonsterHP -= AttackResult;
    Debug.Log("몬스터 HP" + MonsterHP);

    void Attack() // Player attacks monster or monster attacks player
    {
        PlayerDamage = PlayerAttack + PlayerSword;
        Debug.Log("플레이어 공격력:" + PlayerDamage);
        AttackResult = PlayerDamage - MonsterDef;
        Debug.Log("몬스터가 받은 데미지:" + AttackResult);
        MonsterHP -= AttackResult;
		Debug.Log("몬스터 HP" + MonsterHP);
    }

}

// Update is called once per frame
void Update()
{

}

}
```

Attack()함수는 Start()함수 안에 만들어졌기 때문에 Start()안에서는 사용 가능

Update()함수 안에서는 사용 불가

함수명은 변수명과 동일한 규칙을 가진다. 단, 변수와 구붖ㄴ하기 위해 변수는 소문자, 함수는 대문자로 시작한다.

함수는 세미콜론(;)이 아닌 { }로 범위를 지정해서 정의한다



3. 함수의 유형들

함수는 반환값이 있냐 없냐 / 매개 변수가 필요하냐 아니냐를 가지고 정의



1) 반환 값이 없고 매개 변수도 없이 실행만 되는 함수 = 실행하는 데 호출만 하면 되는 함수(예: start, update 함수)



2)  반환 값은 있고 매개 변수는 없는 함수

반환 값이란 return을 통해서 반환하는 값

반환값이 있을 경우, 반환값의 데이터타입을 지정해줘야 한다.

반환값은 반 드시 한 개의 값만 반환이 가능

반환값의 데이터 타입은 변수의 데이터 타입과 마찬가지로 

값 형식 int, float, bool, string..

참조형식: GameObject, transform, Rigidbody ... 모두 사용 가능

```c#
 void Update()
    {
        int randomnumA = RandomDice();
        Debug.Log("주사위 값은" + randomnumA);
    }
// 반환 값이 없으며, 파라미터도 존재하지 않는 함수

    int RandomDice()
    {
        Debug.Log("주사위는 던져졌다!");
        int randomVal = Random.Range(1, 7);
        return randomVal;
// 반환 값은 있지만, 파라미터(매개 변수)가 없는 함수
    }

    void ShoutName(string name, string shout)
    {
        string uiText = name + ":" + shout;
        Debug.Log(uiText);
    }
    void Shout(string shout)
    {
        Debug.Log(shout);
    }
    void AddNum(int numA, int numB)
    {
        Debug.Log(numA + numB);
    }
}
```



3) 반환값은 없고, 매개변수는 필요한 함수

실행하는 데 필요한 값을 함수에 전달해서 해당 값을 이용해 계산을 하거나 일을 수행하는 함수

함수를 실행할 때 매개변수의 데이터 값고 개수를 일치시켜야 한다

매개 변수는 함수 내에서만 작용하는 일종의 로컬 변수

매개 변수는 필요한 만큼 정의해서 사용할 수 있다

매개 변수는 데이터타입 변수명으로 지정이 가능하고 함수를 사용할 때 같은 데이터 타입의 값을 전달해서 사용

```c#
ShoutName("콜라맛포도", "소리 질러!"); // 함수이름(실제 전달한 값); 형태로 호출 가능
```

함수를 실행할 때 매개변수와 데이터 값과 개수를 무조건 일치시켜야 한다



4) 반환 값과 매개변수가 모두 필요한 함수	

실행하는데 필요한 값을 전달해서 해당 값을 이용해서 일을 수행하고 그 결과를 알려주는 함수



예시) 데미지를 계산하여 데미지를 출력하는 함수

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Study07 : MonoBehaviour
{
    

// Start is called before the first frame update
void Start()
{
    CalDamage(1,2);
   int CalDamage(int att, int def)
    {
        float damage = att - def;
        float critical = Random.Range(1.0f, 1.5f);
        damage *= critical;
        int damageReturn = (int)damage;
        return damageReturn;
    }

}

// Update is called once per frame
void Update()
{
    
}

}
```

```c#
 private void OnMouseDown() // void OnMouseDown() <-- 콜라이더 있는 오브젝트를 클릭햇을 때 자동으로 실행하는 유니티 내장 함수
// 라이브러리에(엔진) 기본적으로 정의되어 있는 함수를 내장 함수라고 한다. 프로그래머가 직접 만든 함수는 커스텀 함수
// 내장 함수를 사용할 때 대소문자를 정확하게 적지 않으면 커스텀 함수로 간주
// 그리고 내장 함수의 데이터 타입, 매개변수의 유무를 다르게 사용해도 다른 함수로 간주한다.
    {
        Debug.Log("마우스 클릭");
    }
```

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Study06 : MonoBehaviour
{
    int PlayerAttack = 100;
    int PlayerSword = 50;
    int MonsterDef = 30;
    int MonsterHP = 1000;
    int PlayerDamage;
    int AttackResult;

// Start is called before the first frame update
void Start()
{
    Debug.Log("몬스터 HP :" + MonsterHP);
    Debug.Log("첫번째 공격");
    PlayerDamage = PlayerAttack + PlayerSword;
    Debug.Log("플레이어 공격력:" + PlayerDamage);
    AttackResult = PlayerDamage - MonsterDef;
    Debug.Log("몬스터가 받은 데미지:" + AttackResult);
    MonsterHP -= AttackResult;
    Debug.Log("몬스터 HP" + MonsterHP);
    Attack();

    idle();
   CalDamage(1,2);
   ShoutName("콜라맛포도", "소리 질러!");
    Shout("롤 하자");
    AddNum(3, 4);
}
void Attack() // Player attacks monster or monster attacks player
{
    PlayerDamage = PlayerAttack + PlayerSword;
    Debug.Log("플레이어 공격력:" + PlayerDamage);
    AttackResult = PlayerDamage - MonsterDef;
    Debug.Log("몬스터가 받은 데미지:" + AttackResult);
    MonsterHP -= AttackResult;
    Debug.Log("몬스터 HP" + MonsterHP);
}


int CalDamage(int att, int def)
{
    float damage = att - def;
    float critical = Random.Range(1.0f, 1.5f);
    damage *= critical;
    int damageReturn = (int)damage;
    return damageReturn;
}

private void OnMouseDown() // void OnMouseDown() <-- 콜라이더 있는 오브젝트를 클릭햇을 때 자동으로 실행하는 유니티 내장 함수
// 라이브러리에(엔진) 기본적으로 정의되어 있는 함수를 내장 함수라고 한다. 프로그래머가 직접 만든 함수는 커스텀 함수
// 내장 함수를 사용할 때 대소문자를 정확하게 적지 않으면 커스텀 함수로 간주
// 그리고 내장 함수의 데이터 타입, 매개변수의 유무를 다르게 사용해도 다른 함수로 간주한다.
{
    Attack();
    transform.Rotate(0, 30, 0); // 오브젝트 회전
    transform.Translate(1, 0, 0); //오브젝트 이동

}

void idle()
{
    Debug.Log("숨쉬고 있자");
    Debug.Log("가끔은 기지개도 하자");
    Debug.Log("가끔은 두리번 거리기도 하자");
}
// Update is called once per frame
void Update()
{
    int randomnumA = RandomDice();
    Debug.Log("주사위 값은" + randomnumA);
}

int RandomDice()
{
    Debug.Log("주사위는 던져졌다!");
    int randomVal = Random.Range(1, 7);
    return randomVal;
}

void ShoutName(string name, string shout)
{
    string uiText = name + ":" + shout;
    Debug.Log(uiText);
}
void Shout(string shout)
{
    Debug.Log(shout);
}
void AddNum(int numA, int numB)
{
    Debug.Log(numA + numB);
}

}
```

