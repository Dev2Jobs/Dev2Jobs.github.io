---
layout: post
title:  "Objective-C block"
---
# Welcome

**Hello world**, this is my first Jekyll blog post.


https://yulran.tistory.com/125

Objective-C block에서 캡쳐에 대한 고찰



예제 1

[someObject messageWithBlock:^{

[self someMessage];

...

}];



예제 2

__weak typeof(self) weakSelf = self;

[someObject messageWithBlock:^{

__strong typeof(weakSelf) strongSelf = weakSelf;

[strongSelf someMessage];

...

}];



다음과 같은 예제가 있다 무슨 차이가 있을까?

1. 예제 2가 예제1에 비해 안전하다.(weak로 self가 dealloc 되더라도 nil이 셋팅되기 때문에)

이것 밖에 없을까??? 아니다.

2. self의 life cycle이 서로 다르다.

block이 셋팅될 때 캡쳐된 변수를 retain 하기 때문에 그 전에 self가 날아가지 않는다면 예제 1은 block 안에서 항상 self가 살아 있다고 할 수 있다. 하지만 예제 2의 경우 block이 호출되기 전에 self가 날아가면 nil이 되므로 아무것도 하지 않는다.
