## Recursion(재귀)

### Recursion (재귀, 되부름) in Computer Science
프로그램에서 어떤 함수(혹은 프로시져, 서브프로그램)에서 직접적으로 혹은 간접적으로 자기 자신 함수를 다시 호출하는 것
- base case : 직접 함수 값을 계산할 수 있는 경우.
  -Recursion에서는 제일 먼저 입력값이 base case에 해당하는 지를 먼저 검사하고 처리함.
  -적어도 한 개 이상의 base case가 있어야 함.
- recursive step : 직접 함수값을 계산할 수 없는 경우에는 base case를 이용하여 처리할 수 있도록 base case가 만들어 질 때까지
계속 자신을 재귀호출해 나가면서 계산하는 과정
  -적절한 base case가 없으면 무한 loop 발생(실제로는 stack overflow!)
---------------------------------------------------------------------------------

## Type of Recursion
- unary recursion : 코드 안에 recursive call이 하나만 있는 경우.
  ex) factorial, linear sum, reversing array, computing powers
- Binary recursion : 코드 안에 recursive call이 두 번 있는 경우
  ex) 피보나치 수, 하노이 탑, merge sorting, quick sorting
- Multiple recursion : 코드 안에 recursive call이 여러번 있는 경우
  ex) flood fill, knight's tour

---------------------------------------------------------------------------------------

## Call Stack

-필요성 : 프로그램 실행중 함수를 호출 할 때, 현재 실행 중인 함수는 "지역 변수" 등 자신이 가지고 있는 정보를 저장할 필요가 있다.
특히 재귀에서 새로운 함수 수행이 완료 되었을 때, 다시 원래 호출했던 함수로 제어가 돌아와야 하고, 그 함수에서 사용하던 지역 변수등과 같은 정보를 복원해서
사용해야 한다. 또, 원래 함수로 되돌아 왔을때 수행해야할 프로그램의 주소도 저장해야한다.

현재 함수가 가지고 있던 정보를 저장하는 연속적인 메모리 공간을 "Activation record"라 하고, 이 activation record를 "call stack" 이라는 
공간에서 관리함.

-why stack?
 함수를 호출하고 반환하는 과정이 "last call first return"이므로 함수의 activation record를 Lifo 구조인 stack에 저장하는 것이 가장 적합.
(call stack의 maximum depth : 10000)

---------------------------------------------------------------------------------------

## unary recursion ex - Computing powers 

p(x,n) = x^n

p(x,n) = 1 (n=0) ( base case )
       = x * p(x,n-1) (n>0) ( recursive step )
---------------------------------------------------------------------------------------


### binary recursion ex - Fibonacci Number
[fn+1 fn]
[fn   fn-1]  = [1 1]^n
               [1 0]

이는 수학적 귀납법으로 증명이 가능하다.
