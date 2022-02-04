# for...in vs for...of

1. for...in

2. for...of

for in 반복 대상
Iterable object이면 모두 반복할 수 있는 대상이 됩니다.
for of 반복 대상
Iterable object이지만, prototype chain에 의한 Iterable은 반복 대상에서 제외됩니다.

# Iterator

순서를 정의하고, 종료시 반환 값을 잠재적으로 정의하는 객체이다.

{value , done} 을 반환하는 next() 메소드를 사용하여 객체의 Iterator protocol을 구현 했는지 여부를 말한다.
