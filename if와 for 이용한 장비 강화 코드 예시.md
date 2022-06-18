#### if와 for문을 이용하여 무기 강화 시스템 만들기



##### 시스템 요구 사항

클릭하면 소지한 강화석을 모두 소진해서 자동으로 강화하는 시스템



##### 세부 조건

무기 기본 공격력은 12

강화 성공 확률은 1단계 100%, 2단계 80%, 3단계: 64% 이런 식으로 이전 단계 확률의 20%감소

강화 성공 시 공격력 3 증가 

강화에 실패하면 70%로 강화석만 소진, 20%  강화레벨 1하락, 10% 무기 파괴

무기 파괴되면 처음부터 다시 강화

보유한 강화석은 10000개



##### 도출해내야 하는 결과값

최대 강화 레벨? 

파괴된 무기 개수?

최종 무기 공격력?



```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Enforcement : MonoBehaviour
{
    int WeaponAttack = 12;
    int Stone=10;
    int Destroyed;
    int EnforcementLevel = 0;
    float Success = 100;
    // Enforcement라는 강화 함수를 정의

    private void OnMouseDown() // 클릭을 했을 때
    {
        Debug.Log("강화를 시작합니다");
        for (int i=0;i<=10;i++)
        {
            if (Stone >= 1)
            {
                Stone--;
                if (EnforcementLevel == 0) // 1강 시도를 하면 무조건 성공한다
                {
                    Debug.Log("1레벨 자동 강화 성공");
                    EnforcementLevel += 1;
                    WeaponAttack += 3;
                    Debug.Log("강화 레벨 =" + EnforcementLevel);
                    Debug.Log("무기 공격력 =" + WeaponAttack);
                }
                else
                {
                    Good();
                    Debug.Log("들어왔지?");
                    Debug.Log("강화 레벨 = " + EnforcementLevel);
                    Debug.Log("무기 공격력 =" + WeaponAttack);
                }
            }
            else 
            {
            Debug.Log("강화석이 부족합니다");
            }
        }
    }

    void Good() // 강화 성공 확률
    {
        Debug.Log("함수호출 성공~");
        for (Success=100; Success >= 0; Success *= 0.2f) 
        {
            float Specup = Random.Range(1, Success *= 0.2f); //성공했을 시 
            if(Specup >= Success * 0.2f)
            {
                WeaponAttack += 3;
                EnforcementLevel++;
                Debug.Log("강화 성공");
            }
            else
            {
                float Failure = Random.Range(1, 101); // 실패했을 시
                if (Failure >= 30)
                {
                    Stone--;
                }
                else if (Failure >= 10) 
                {
                    EnforcementLevel--;
                    WeaponAttack -= 3;
                }
                else
                {
                    Destroyed++;
                    WeaponAttack = 0;
                    Debug.Log("ㅎㅎ파괴됐지롱ㅋㅋㅋㅋ");
                    Debug.Log("니가 깨먹은 무기 개수는" + Destroyed);
                }
            }
        }
    }


    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}
```

  