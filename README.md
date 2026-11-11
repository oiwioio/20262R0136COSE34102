- Project1 과제 설명

1. sslab_my_stack.c
<br />
먼저 integer node 형태를 이용하는 stack 구조를 사용하기 위해 os_2026_stack_node 구조체를 정의하였다.
<br />
구조체 내부에 들어가는 구성요소는 해당 node가 가지고 있는 값인 val, stack 구조상 내 밑에 있는 node의 주소를 가리키는 next가 있다.
<br />
이후 stack의 관리를 용이하게 하기 위해 해당 구조체의 맨 위를 가리키는 목적인 top을 선언했고,코드상에서 한 stack을 동시에 사용할 가능성이 있는 global variable을 의미하기에 mutual exclusion을 위해 DEFINE_MUTEX로 mutex를 선언하고 각 함수의 처음과 끝에 mutex_lock, mutex_unlock을 넣어주었다.
