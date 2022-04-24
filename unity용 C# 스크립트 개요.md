# C# 스크립트의 시작

```c#
// 한 줄 주석
/* 
 여러줄 주석을 달 경우 사용
 이 안에 있는 텍스트는 모두 주석 처리
*/
```



### 1. 스크립트

#### 스크립트란?

게임 엔진이 어떻게 작동할 지 작성한 텍스트 파일

유니티는 스크립트 언어로 C#, JavaScript를 사용

유니티를 제대로 사용하려면 C# 스크립트를 이해해야 한다



#### 스크립트의 적용

스크립트를 사용할 오브젝트에 드래그하거나 컴포넌트 추가를 해서 연결 가능



#### 유니티에서 스크립트 생성 시 주의사항

유니티는 스크립트 파일을 생성하면 파일 이름과 동일한 클래스 이름이 자동으로 결정

**추후에 파일 이름을 변경하면 클래스 이름은 변경되지 않아 에러 발생**

생성 후 이름을 바꿔야 할 경우에는 안에 있는 클래스 명도 바꿔야 작동

파일 이름에 띄어쓰기가 가능하기는 한데 클래스명은 붙여서 생성된다

혼동을 방지하기 위해 가급적 띄어쓰기는 사용하지 않는다

(_는 사용 가능하기는 한데 주로 카멜 표기법을 사용한다)



### 2. 주석, 네임스페이스, Class, Start, Update

#### Unity 3D 내 스크립트 기본 구조

```c#
using System.Collections; // using 네임스페이스
using System.Collections.Generic; // 네임스페이스에 포함된 명령 라이브러리 사용하겠다
using UnityEngine; // Unity Engine 네이스페이스에 존재하는 코드를 사용하겠다 
// 어떤 프로그램 사용할 지 명시하는 부분으로 여기서는 UnityEngine을 사용하고 있다는 것을 의미 (console 등 다른 프로그램도 가능)

public class Study01 : MonoBehaviour 
 //public class Study01 <-- Study01이라는 이름을 가진 클래스를 생성하겠다
 // Study01: MonoBehaviour <- Study01이 MonoBehaviour 클래스를 상속받겠다 선언
 // 유니티 C#스크립트는 기본적으로 MonoBehaviour 클래스를 상속받는다
     
{ // study01의 시작
    // Start is called before the first frame update
    // 해당 스크립트 컴포넌트가 포함된 오브젝트가 사용될 때 첫 프레임이 실행되면서
    // 자동으로 실행되는 함수
    // 해당 오브젝트의 초기 값, 초기 기능을 설정해 주는데 사용
    void Start() // MonoBehaviour가 정의
    {
     	Debug.Log("Start World"); // C#에서는 ;을 반드시 명령 끝에 사용해준다 
	}

	// Update is called once per frame 
    // 유니티는 별도의 정의를 해주지 않는 이상 초당 60프레임을 실행
    // 해당 오브젝트가 활성화 되어 있을 경우
    // 매 프레임마다 자동으로 실행되는 함수
	void Update() // MonoBehaviour가 정의
	{
    	Debug.Log("Update World");	
	}

} // study01의 끝
```



### 3. 변수

#### 변수의 개념

변수란: 변할 수 있는 값이 들어갈 수 있는 장소

변수를 사용하는 이유: 원하는 값을 기억하고 다시 사용하기 위해서

변수에 저장한 값은 게임 도중 언제든지 접근하고 수정할 수 있다

(변하지 않는 값은 상수)



#### 변수를 사용하는 이유

원하는 데이터를 저장하고 불러다 슨다는 것은 일일이 직접 값을 쓰는 것보다 편리함을 제공

값을 잘못 입력한 실수로 인한 오류를 줄일 수 있음



#### 변수의 선언

Lua와 다르게 C#에서는 변수를 처음 정의할 때 변수 앞에 해당 변수와 사용할 데이터의 종류(타입)을 표시해야 한다.

변수를 만들고 타입을 정하는 것을 '변수를 선언한다'라고 한다

```c#
int MyAge; // MyAge라는 이름을 가진 int타입의 변수를 선언한다
int _MyAge1;
int myAge;  // 위의 3개 모두 다른 변수다
int 내나이; //되긴 하는데 잘 안 쓴다.(플랫폼마다 안 되는 경우도 많다)
          // 동음이의어가 워낙 많기도 하다
```



#### 변수의 이름

영문과 숫자를 이용해서 작성 가능 + 언더바(_)도 사용 가능 

대소문자도 당연히 구분한다. (한글도 사용 가능하긴 한데 잘 안 쓴다)

유니티나 C#에서 이미 사용하는 키워드, 변수 이름과 중복되면 안 된다



#### 변수의 데이터 타입

변수에 어떤 종류의 데이터를 저장할 것인지를 정의

정의한 값과 다른 형태의 값을 저장하면 에러가 발생

변수의 데이터 타입에는 정수, 실수, 문자열, 논리형 등이 존재



##### 정수 타입

int(정수형): 소수점이 없는 숫자를 저장하는 타입

```c#
int PlayerLevel = 10; //(변수를 선언하면서 값을 지정하는 것을 "변수의 초기화")
```



##### 실수 타입

float(실수형): 소수점을 가질 수 있는 숫자를 저장하는 타입 float타입 숫자 뒤에는 반드시 f 붙여줄 것

(정수는 해당 사항 없음 = 자동으로 float으로 변환해 저장 / 하지만 소수점을 가질 경우에는 f 붙여라)

소수점은 최대 7자리까리 계산이 되고, 그 이상은 근사값으로 처리 

더 많은 자리의 소수점을 계산하려면 double을 사용해야 한다

```c#
float PlayerSpeed = 1.34f; //뒤에 f가 없으면 '1이라는 숫자가 가진 34라는 속성불러라' 됨
//정수를 넣어도 인식은 된다(소수점이 들어갈 때는 반드시 f 추가해야)
```



##### 문자열 타입

문자열( = 문자 1개 이상)을 저장하는 타입

여러개의 문자를 묶을 경우 + 사용

```c#
string PlayerHobby = "게임" +  "영화" + "맛집탐방";
string talkText = "₩대화 ₩n 내용₩"
// char 캐릭터형(문자 1개를 저장), 저장할 때는 '' 사용
```



##### 논리(T/F)

```c#
bool isPlayerLive = true;
```

=는 대입연산자 (오른쪽에 있는 값을 왼쪽의 변수에 저장)



C#에서는 여러 개의 변수 값 형태로 초기화가 안 된다.

즉, 각자 다른 변수가 선언된다

예시)

```c#
int num A;, int num B;, int num C; 
// 같은 타입의 변수는 콤마로 구분지어 동시에 선언 됨 
```



###### 실제 Unity C# 스크립트 내에서 변수 선언 예시

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Study02 : MonoBehaviour
{
    int PlayerLevel = 10;
    // Start is called before the first frame update
    void Start()
    {
        Debug.Log("플레이어 레벨 :" + PlayerLevel); 
        //한 번 만들어진 변수는 이름만 표기하여 사용 가능
    }

// Update is called once per frame
void Update()
{
    
}

}
```



#### Unity 3D 엔진에서 별도로 지원하는 데이터 타입

Unity 3D에서는 C# 언어가 기본적으로 제공하는 데이터 타입 외에도 Unity가 독자적으로 제공하는 데이터 타입도 존재

```c#
GameObject Monster; 
// GameObject 타입의 데이터를 담을 수 있는 타입

Transform monsterTransform; 
// Transform 컴포넌트의 타입의 데이터를 담을 수 있다

Rigidbody monsterRigidbody; 
// Rigidbody 컴포넌트 타입의 데이터를 담을 수 있다

Collider monsterCollider; 
// Collider 컴포넌트 타입의 데이터를 담을 수 있다
```



#### 참조 형식의 이해

C#에서 제공하는 데이터 타입에 데이터를 담는다는 것은 해당 변수에 지정한 값을 실제로 넣어둔다는 직관적인 방법이지만, 유니티가 제공하는 데이터 타입에 데이터를 담는다는 것은 실제 데이터를 넣는 게 아니라 해당 데이터가 담겨 잇는 곳을 접근하는 방법을 지정하는 것 

(윈도우의 바로가기 아이콘과 비슷한 개념)

예를 들어, Monster라는 게임 오브젝트를 만들면 이 오브젝트를 담기 위해 유니티는 메모리에 저장 하게 됨

메모리에는 주소라는 게 있어서 이걸 어딘가에 저장해야 접근이 가능함

GameObject monster는 GameObject 타입의 데이터가 잇는 메모리 주소를 저장해 둔다는 의미

이런 방식을 "참조한다"라고 표현함

```c#
GameObject monster1 = GameObject.Find("Monster") ; // 씬 안에 있는 오브젝트들 중에서
// Monster라는 이름을 가진 오브젝트를 찾아서 주소를 넘겨줘라
// Monster라는 GameObject의 이름이 Orc로 세팅되어 있다고 가정
```

```c#
GameObject monster1 = GameObject.Find("Monster");
GameObject monster2 = GameObject.Find("Monster");
GameObject monster3 = GameObject.Find("Monster");
GameObject monster4 = GameObject.Find("Monster");
// monster 1 ~ 4 모두 Monster라는 오브젝트가 담겨있는 같은 메모리 주소를 참조
// monster 2 ~ 4도 이름을 출력하려고 참조한 주소의 오브젝트의 이름을 가져오다보니 이름이 Orc로 바뀌어 있음

void Update()
    {
        Debug.Log(monster1.name);

        monster1.name = "Orc";
// monster1이 참조하고 있는 오브젝트의 name이라는 속성값에 Orc라는 값을 넣어라        
        
    }
}
```



#### 값 형식의 이해

참조 형식은 대상 데이터 메모리 주소를 저장하고 있지만, 값 형식은 자신만의 데이터를 실제로 가지고 있다

C# 스크립트에서 int, float, bool 형식의 데이터 타입은 모두 '값 형식'



#### 변수의 사용 범위

변수를 만들었을 때 선언한 줄을 포함하는 중괄호 범위를 벗어나서 사용할 수 없다

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Study04 : MonoBehaviour
{
   private int numA = 10; //num A 변수는 class Study04의 중괄호 안에서 만들어졌기 때문 
  //그 안에 포함된 Start(), Update() 범위 안에서 모두 사용 가능
  // 클래스 내부에서 선언되어, 클래스 안의 모든 곳에서 접근, 사용 						 //가능한 변수
    			   // 기본적으로 클래스 내부에서만 사용할 수 있게 private 속성을 가진다
    // Start is called before the first frame update
    void Start()
    {
     Debug.Log(numA);
     int numB = 100;
        
/* Start의 중괄호 안에서 만들어졌기 때문에 Start 안에서는 얼마든지 사용 가능
Update()에서는 범위를 벗어났기 때문에 사용할 수 없음
기본적으로 클래스 내부에서만 사용할 수 있게 private 속성을 가진다*/
     Debug.Log(numB);   
}

// Update is called once per frame
void Update()
{
  Debug.Log(numA);
  int numC = 50;
  Debug.Log(numC);   
}

}
```



##### public 변수와 private 변수의 차이

private 변수는 해당 클래스 내부에서만 접근, 사용 가능한 변수

public 변수는 해당 클래스 바깥에서도 접근, 사용 가능한 변수

변수의 데이터 타입 앞에 아무런 표시를 해주지 않으면 자동으로 private 처리한다

데이터 타입 앞에 public을 붙여 주면 public 변수가 된다

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Study05 : MonoBehaviour
{
    public string myName = "콜라맛포도";
//public 변수는 인스펙터에 표시되며, 이 곳에서 값을 바꾸는 것이 가능
// 단, 인스펙터에서 값을 바꾸면 프로그램을 변경해도 반영이 안 되기 때문에 리셋을 해야 된다

// Start is called before the first frame update
	void Start()
	{
    	Debug.Log(myName);
	}

// Update is called once per frame
	void Update()
	{
    
	}

}
```



##### 변수의 선언 및 명령어 선언 응용 예시

플레이어가 몬스터를 공격해서 몬스터를 처치하는 코드

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Player //1개 스크립트에 여러개의 스크립트가 있을 수 있다. --> 실제 객체를 만들기 위한 설계도 
{
    public int HP = 100; // Player 클래스가 갖고 있는 속성
    // 
    public int power = 50;

    public void Attack()
    {
        Debug.Log(this.power + "데미지를 입혔다"); // 플레이어의 power만큼 데미지를 입힌다
    }

    public void Damage(int damage) // Damage라는 명령어 정의
    {
        this.HP -= damage; // this를 쓰는 이유는 다른 범위에 있는 같은 이름을 가진 변수와의 혼동을 방지하기 위함
        // Player 클래스로 만들어진 인스턴스 객체 자신에 속해 있는 HP라는 변수를 지정
        Debug.Log(damage + "데미지를 입었다");
        
    }
}

public class Study01 : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        Player myPlayer = new Player(); // Player 클래스의 객체를 담을 수 있는 myPlayer라는 변수를 만들었다.
        //new Player(); <-- Player클래스를 이용해 객체 하나를 생성했다.(인스턴스)
        myPlayer.Attack(); //myPlayer의 Attack 속성 참조
        myPlayer.Damage(30); // myPlayer에 Damage 함수 실행
        Debug.Log(myPlayer.HP); //위의 this.HP와 동일한 역할
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}
```



변수 선언 및 명령어 선언을 이용한 플레이어 캐릭터 이동

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Study02 : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        Vector2 playerPos = new Vector2(3.0f, 4.0f);
        //new Vector2는 Unity에만 지원하는 내장함수
        //new Vector2는 2차원 평면에서 오브젝트 이동 함수
        playerPos.x  += 8.0f;
        playerPos.y  += 5.0f;
        Debug.Log(playerPos);
    }

    // Update is called once per frame
    void Update()
    {
       
    }
}

```



