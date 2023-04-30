# Unity
## 오브젝트 컨트롤하기
### 1. Player 움직이기(앞, 뒤, 옆)
1. 필요 Inspector Component
   1. Component란?
   - 게임 오브젝트의 동작을 제어하기 위해 추가하는 기능 모듈
   2. Collider
   - 게임 오브젝트 끼리의 충돌 검사를 한다.
   - 두 오브젝트에 추가해야 서로 통과되지 않는다.
   3. Rigidbody
   - 게임 오브젝트에 물리적 특성을 부여한다.

2. 코드 순서
   1. Rigidbody 변수 선언하여 Player의 Rigidbody로 지정
   2. 키보드 축 입력을 받는다.
   3. 입력 받은 축 값으로 transform으로 변환 
   4. 변환된 값을 합친 후 정규화하여 백터로 변환
     - 정규화란?<br>
     백터를 단위 백터(Unit Vector)로 변환는 것을 의미한다. 백터의 길이를 1로 변환하여 방향을 나타내도록 한다.
   5. Player의 Rigidbody를 이동시킨다.

3. 코드
 ```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    [SerializeField]
    private float walkSpeed;
    
    private Rigidbody PlayerRigidbody;

    void Start()
    {
        PlayerRigidbody = GetComponent<Rigidbody>();
    }

    void Update()
    {
        Move();
    }

    private void Move()
    {
        float _moveDirX = Input.GetAxisRaw("Horizontal");
        float _moveDirZ = Input.GetAxisRaw("Vertical");
        bool wDown = Input.GetButton("Run");

        Vector3 _moveHorizontal = transform.right * _moveDirX;
        Vector3 _moveVertical = transform.forward * _moveDirZ;
        Vector3 _velocity = (_moveHorizontal + _moveVertical).normalized * walkSpeed;
        PlayerRigidbody.MovePosition(transform.position + _velocity * Time.deltaTime);
    }
}
 ```
### 오브젝트
