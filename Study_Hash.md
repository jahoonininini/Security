# 비밀번호
## 비밀번호를 서버에 저장할 때는 보안성을 높이기 위해 해시 알고리즘을 사용
1. bcrypt : 비밀번호 해싱에 특화된 알고리즘으로, 느린 해시 함수를 사용하여 brute-force 공격에 대한 저항력을 높임
2. Argon2 : 2015년 패스워드 해싱 대회에서 우승한 알고리즘, 메모리와 CPU 자원을 많이 소모하여 공격자가 비밀번호를 추측하기 어렵게 만듬.
3. PBKDF2 : 키 유도 함수로, 여러 번의 해시 연상르 통해 비밀번호를 해싱. 이로 인해 공격자는 해시 역산이 어려움.

이 외에도 SHA-256과 같은 일반적인 해시 함수도 사용될 수 있지만, 비밀번호 저장에는 적합하지 않음. 해시된 비밀번호는 솔트(salt)와 함께 저장하여 동일한 비밀번호라도 서로 다른 해시 값을 생성하도록 하는 것이 중요함.

솔트의 역할 : 솔트는 해시 함수에 추가되는 임의의 데이터로, 동일한 비밀번호라도 서로 다른 해시 값을 생성한다. 이를 통해 레인보우 테이블 공격을 방지. 솔트가 없으면 동일한 비밀번호는 항상 동일한 해시 값을 가지므로, 공격자는 미리 계산된 해시 값과 비교하여 쉽게 비밀번호 탈취 가능.

# 해시 함수
1. 입력 데이터의 변환 : 해시 함수는 임의 길이를 가진 입력 데이터를 받아들여, 이를 고정된 길이의 축력(해시 값)으로 변환한다. 예를 들어, SHA-256 해시 함수는 어떤 길이의 입력 데이터라도 256비트(32바이트 16진수의 64자리) 길이의 해시 값을 생성.
2. 결정성 : 동일한 입력 데이터에 대해 상상 동일한 해시 값을 생성. 즉, 같은 비밀번호를 해싱하면 항상 같은 해시 값이 나옴.
3. 비가역성 : 해시 함수는 비가역적이다. 즉, 해시 값을 통해 원래의 입력 데이터를 복원하는 것은 매우 어렵다. 이는 해시 함수의 중요한 특성으로, 보안에 기여
4. 충돌 저항성 : 서로 다른 두 입력 데이터가 동일한 해시 값을 생성하는 경우를 '충돌'이라고 한다. 좋은 해시 함수는 충돌이 발생할 확률이 매우 낮아야 한다. 즉, 해시 함수는 입력 데이터의 작은 변화에도 해시 값이 크게 달라지도록 설계되어야 한다.
5. 효율성 : 해시 함수는 입력 데이터를 처리하여 해시 값을 생성하는 과정이 빠르고 효율적이어야 한다. 이는 대량의 데이터를 처리할 때 중요.
