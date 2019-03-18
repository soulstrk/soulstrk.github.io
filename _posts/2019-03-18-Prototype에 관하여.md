---
layout: post
title:  "Prototype에 관하여"
date:   2016-03-15
excerpt: "prototype link와 prototype object 그리고 프로토타입을 왜 사용할까?"
tag:
- prototype 
comments: true
---

# prototype

---

자바스크립트는 프로토타입 기반 언어라고 불립니다.

프로토타입이 무엇인지 깨우친 순간 자바스크립트가 재밌어지고, 숙련도가 올라가는 느낌을 받을 수 있습니다.

## Prototype vs Class

---

클래스는 객체지향언어에서 빠질 수 없는 개념입니다. 그런데 중요한 점은 자바스크립트도 객체지향언어란는 것입니다. 프로토타입이 클래스 역할을 흉내낼 수 있습니다.

    function Person() {
      this.eyes = 2;
      this.nose = 1;
    }
    var kim  = new Person();
    var park = new Person();
    console.log(kim.eyes);  // => 2
    console.log(kim.nose);  // => 1
    console.log(park.eyes); // => 2
    console.log(park.nose); // => 1

kim과 park은 eyes와 nose를 공통적으로 가지고 있는데, 메모리에는 nose와 eyes가 각각 두 개씩 총 4개가 할당됩니다. 객체를 100개 만들면 200개의 변수가 메모리에 할당되겠죠?

바로 이런 문제를 프로토타입으로 해결할 수 있습니다.

    function Person() {}
    
    Person.prototype.eyes = 2;
    Person.prototype.nose = 1;
    
    var kim  = new Person();
    var park = new Person():
    
    console.log(kim.eyes); // => 2
    ...

간단히 설명하자면 Person.prototype이라는 빈 오브젝트가 어딘가에 존재하고, Person 함수로부터 생성된 객체들은 어딘가에 존재하는 Object에 들어있는 값을 모두 갖다쓸 수 있습니다.

프로토타입을 깊게 파보면 엄청나게 복잡하지만 개발자가 사용하는 부분만 본다면 이게 거의 전부입니다. 하지만 개발자는 사용법만 알고있는게 아니라 언제나 왜?를 생각해야합니다

## prototype Link와 prototype Object

---

- prototype Object - 객체는 언제나 함수(function)으로 생성됩니다.

    function Person() {} // => 함수
    var personObject = new Person(); // => 함수로 객체를 생성

personObject 객체는 Person이라는 함수로 생성된 객체입니다. 이렇듯 언제나 객체는 함수에서 시작됩니다. 여러분이 많이 쓰는 일반적인 객체 생성도 예외는 아닙니다.

    var obj = new Object();

위 코드에서 Object가 자바스크립트에서 기본적으로 제공하는 함수입니다.

Object와 마찬가지로 Function, Array도 모두 함수로 정의되어 있습니다. 이것이 첫 번째 포인트입니다.

그렇다면 이것이 Prototype Object랑 무슨 상관이있느냐? 함수가 정의될 때는 2가지 일이 동시에 이루어집니다.

1. *해당 함수에 Constuctor 자격 부여*

Constructor자격이 부여되면 new를 통해 객체를 만들어 낼 수 있게 됩니다.

이것이 함수만 new 키워드를 사용할 수 있는 이유입니다.

2. *해당 함수의 prototype Object 생성 및 연결*

함수를 정의하면 함수만 생성되는 것이 아니라 prototype Object도 같이 생성 됩니다.

![](-917e08d5-b0b1-4dc7-a1e5-c273c5fa91fauntitled)

그리고 생성된 함수는 prototype이라는 속성을 통해 Prototype Object에 접근할 수 있습니다. Prototype Object는 일반적인 객체와 같으며 기본적인 속성으로 constructor와 __proto__를 가지고 있습니다.

constructor는 Prototype Object와 같이 생성되었던 함수를 가리키고 있습니다.

    function Person() {
      this.eyes = 2;
      this.nose = 1;
    }
    var kim  = new Person();
    var park = new Person();
    console.log(kim.eyes);  // => 2
    console.log(kim.nose);  // => 1
    console.log(park.eyes); // => 2
    console.log(park.nose); // => 1

Prototype Object는 일반적인 객체이므로 속성을 마음대로 추가/삭제 할 수 있습니다. kim과 park은 Person 함수를 통해 생성되었으니 Person.prototype을 참조할 수 있게 됩니다.
