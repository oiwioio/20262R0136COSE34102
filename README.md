- Project1 과제 설명

1. sslab_my_stack.c
<br />
먼저 integer node 형태를 이용하는 stack 구조를 사용하기 위해 os_2026_stack_node 구조체를 정의하였다.
<br />
구조체 내부에 들어가는 구성요소는 해당 node가 가지고 있는 값인 val, stack 구조상 내 밑에 있는 node의 주소를 가리키는 next가 있다.
<br />
이후 stack의 관리를 용이하게 하기 위해 해당 구조체의 맨 위를 가리키는 목적인 top을 선언했고,코드상에서 한 stack을 동시에 사용할 가능성이 있는 global variable을 의미하기에 mutual exclusion을 위해 DEFINE_MUTEX로 mutex를 선언하고 각 함수의 처음과 끝에 mutex_lock, mutex_unlock을 넣어주었다.
<br />
각 함수에서 현재 stack을 출력해야하므로 os2026_print_stack_locked로 자주 사용할 함수를 미리 만들어두었다.
<br />
push는 val로 입력값을 사용하고 next로 현재 top이 가리키는 node를 가리키는 새로운 node를 추가 후 top이 새로운 node를 가리키게 해 stack의 최상단에 새로운 node가 추가되도록 했다.
