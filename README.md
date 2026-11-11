- Project1 과제 설명

1. sslab_my_stack.c
<br />

먼저 integer node 형태를 이용하는 stack 구조를 사용하기 위해 os_2026_stack_node 구조체를 정의하였다.

구조체 내부에 들어가는 구성요소는 해당 node가 가지고 있는 값인 val, stack 구조상 내 밑에 있는 node의 주소를 가리키는 next가 있다.

이후 stack의 관리를 용이하게 하기 위해 해당 구조체의 맨 위를 가리키는 목적인 top을 선언했고,코드상에서 한 stack을 동시에 사용할 가능성이 있는 global variable을 의미하기에 mutual exclusion을 위해 DEFINE_MUTEX로 mutex를 선언하고 각 함수의 처음과 끝에 mutex_lock, mutex_unlock을 넣어주었다.

각 함수에서 현재 stack을 출력해야하므로 os2026_print_stack_locked로 자주 사용할 함수를 미리 만들어두었다.

push는 val로 입력값을 사용하고 next로 현재 top이 가리키는 node를 가리키는 새로운 node를 추가 후 top이 새로운 node를 가리키게 해 stack의 최상단에 새로운 node가 추가되도록 했다.

pop은 stack이 비어있으면 작동하지 않고, 그렇지 않다면 현재 top이 가리키는 node를 free하면서 top이 바로 밑에 있던 node를 가리키게 해 stack의 최상단에 있는 node가 삭제되도록 했다.

clear는 top에서부터 stack을 순차적으로 순회하며 모두 free하는 작업을 통해 stack을 초기화시키는 기능을 하도록 했다.
<br />


2. call_my_stack.c
<br />

system call을 위해 unistd.h, srand와 rand를 위해 stdlib.h, time.h를 사용했고, 테스트 및 예상 결과와의 비교를 위해 push값을 저장할 리스트와 pop 및 clear 시 return값을 받을 num을 선언했다.

먼저 stack 초기화를 위해 syscall(337)을 실행했다. srand와time을 통해 난수 시드를 생성하고 1부터 100 사이의 무작위 난수를 생성 및 리스트에 저장 후 syscall(335, r[i])을 통해 stack에 추가하는 과정을 5회 반복했다.
