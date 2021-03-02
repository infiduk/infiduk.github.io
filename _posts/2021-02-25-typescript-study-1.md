---
title: "[TypeScript] 타입스크립트(TypeScript) 뿌시기 1 (변수 선언)"
date: 2021-02-25 09:18:04 +09:00
tags: study typescript javascript
comments: true
---

타입스크립트(TypeScript) 뿌시기 1 (변수 선언)
Studying TypeScript 1

## 변수 선언

ES5 까지는 변수를 선언할 수 있는 방법이 var 선언자를 이용하는 방법 밖에 없었습니다.

var 선언자는 아래와 같은 특징을 가지고 있었는데요,

변수가 선언된 위치와 관계없이 스코프(scope)의 최상위로 끌어올림 되어 같은 스코프라면 어디서든 호출되는 특징과, 블록 레벨 스코프(Block Level Scope)가 지원되지 않는 특징입니다.

### var 선언자의 특징 1

var 선언자의 첫 번째 특징은 호이스팅(Hoisting) 이라고 불리는 녀석입니다.

호이스팅이란 위에서 말씀드렸다시피 선언한 변수가 스코프의 최상위로 끌어올라가지는 현상입니다.

변수 선언을 나중에 하고 변수에 값 할당을 먼저 해도, 자바스크립트에서는 변수를 먼저 선언하고 할당한 것 처럼 호이스팅하여 처리하므로 이러한 특징을 가질 수 있게 된 것입니다.

아래 예제 코드를 보시면, favoriteLanguage 라는 변수에 javascript 를 할당한 이후 변수를 선언했음에도 불구하고 정상적으로 console 에 javascript 라는 값이 출력된 것을 보실 수 있습니다.

```typescript
// favoriteLanguage 변수에 javascript 라는 값이 할당됨
favoriteLanguage = "javascript";

console.log(favoriteLanguage);

// 변수 선언
var favoriteLanguage;

/*
----- 출력 결과 -----
javascript
-------------------
*/
```

하지만 예제 코드와 같은 방식은 거의 사용하지 않는 방식이고 가독성을 떨어뜨리는 코드, 디버깅이 어렵다 라는 단점을 가지고 있습니다.

### var 선언자의 특징 2

var 선언자는 함수 레벨 스코프(Function Level Scope) 를 지원합니다.

즉, 함수 내부에서 var 선언자로 선언된 변수는 해당 함수 내에서만 유효하고 함수 외부에서는 참조할 수 없다는 특징이 있습니다.

```typescript
// 전역 스코프 변수
var favoriteFood = "chicken";

// 함수 레벨 스코프
function sayFavoriteFood() {
  // 함수 레벨 스코프 변수
  // 스코프가 다르기 때문에, 전역 스코프의 favoriteFood 와 sayFavoriteFood 함수 안의 favoriteFood 는 다른 변수입니다.
  var favoriteFood = "pizza";

  console.log(`(in) Favorite Food: ${favoriteFood}`);
}

sayFavoriteFood();
console.log(`(out) Favorite Food: ${favoriteFood}`);

/*
----- 출력 결과 -----
(in) Favorite Food: pizza
(out) Favorite Food: chicken
-------------------
*/
```

문제는 var 선언자가 블록 레벨 스코프(Block Level Scope) 를 지원하지 않는다는 점인데요,

블록 레벨 스코프란 블록({ }) 내에서만 유효하고 블록 내부에서는 참조할 수 없는 스코프를 의미합니다.

```typescript
// 전역 스코프 변수
var favoriteFood = "chicken";

// 블록 레벨 스코프
if (true) {
  // 블록 레벨 스코프 변수
  // 같은 레벨 스코프에 있으므로 위에서 선언한 변수의 값이 덮어씌워집니다.
  var favoriteFood = "pizza";

  console.log(`(in) Favorite Food: ${favoriteFood}`);
}

console.log(`(out) Favorite Food: ${favoriteFood}`);

/*
----- 출력 결과 -----
(in) Favorite Food: pizza
(out) Favorite Food: pizza
-------------------
*/
```

if 문 안의 변수와 외부의 변수 모두 var 선언자로 선언되었기 때문에 함수 레벨 스코프를 지원합니다.

즉, 블록 레벨 스코프가 적용되지 않아 if 문 내부의 변수가 if 문 외부의 변수에 영향을 주는 현상이 나타나게 되었습니다.

변수가 블록 내에서만 유효 범위를 갖게 하려면 let, const 선언자 또는 클래스(Class), 인터페이스(Interface), type alias, enum 등을 활용하여 변수를 선언하면 됩니다.

### let 선언자의 특징

let 선언자는 변수를 선언할 때 블록 레벨 스코프를 지원합니다.

이는 같은 블록 내에서 같은 이름의 변수를 선언할 수 없다는 것을 의미하고, 이러한 특징으로 인해 블록 내/외부의 변수가 서로 영향을 주는 현상을 방지할 수 있습니다.

```typescript
let person;
let person; // Uncaught SyntaxError: Identifier 'person' has already been declared
```

중첩 블록의 경우, let 선언자는 어떤 방식으로 적용될까요?

```javascript
// A 영역
{
  // B 영역
  {
    // C 영역
  }
  // B 영역
}
// A 영역
```

먼저 var 선언자를 이용해 변수를 선언했을 경우를 살펴보겠습니다.

A 영역에 var 선언자를 이용해 favoriteBlock 이라는 이름으로 변수를 선언하고자 할 때,
B, C 영역에 같은 조건(var 선언자 이용, 변수 이름 favoriteBlock)으로 선언된 변수가 있다면 A 영역에 선언할 변수에 영향을 줄 수 있습니다.

이러한 점은 변수에 블록 레벨 스코프가 적용되지 않아서 생기는 문제점입니다.

하지만 let 선언자를 이용해 변수를 선언할 경우 블록 레벨 스코프가 적용됩니다.

A 영역에 let 선언자를 이용해 favoriteBlock 이라는 이름으로 변수를 선언하고자 할 때,
B, C 영역에 같은 조건(let 선언자 이용, 변수 이름 favoriteBlock)으로 선언된 변수가 있어도 서로 영향을 주지 않습니다.

아래 예제 코드로 다시 한번 설명해드리겠습니다.

```typescript
// A 영역
// A 영역 변수, favoriteBlock
let favoriteBlock = "A";

// B 영역
if (true) {
  // B 영역 변수, favoriteBlock
  let favoriteBlock;
  favoriteBlock = "B";

  console.log(`(in) Favorite Block: ${favoriteBlock}`);
}

// A 영역
console.log(`(out) Favorite Block: ${favoriteBlock}`);

/*
----- 출력 결과 -----
(in) Favorite Block: B
(out) Favorite Block: A
-------------------
*/
```

B 영역에서 선언한 변수가 A 영역의 변수에 영향을 주지 않는 것을 볼 수 있습니다.

또한 let 연산자는 변수를 초기화하기 전, 변수에 접근할 수 없게 해서 호이스팅을 방지합니다.

```typescript
console.log(person);
let person = "Serena"; // Uncaught ReferenceError: person is not defined
```

### 상수(const) 선언

const 는 let 선언자처럼 ES6에 추가되어 사용되고 있습니다.

const 의 특징으로는 let 선언자와 같은 블록 레벨 스코프를 지원한다는 점과 호이스팅을 일으키지 않는다는 점이 있습니다.

if 문 내부의 변수 favoriteColor 는 if 문 외부의 변수 favoriteColor 와 다른 변수이기 때문에, 서로 영향을 주지 않습니다.

```typescript
// 전역 스코프 변수
const favoriteColor = "pink";

// 블록 레벨 스코프
if (true) {
  // 블록 스코프 변수
  const favoriteColor = "blue";
  console.log(`(in) Favorite Color: ${favoriteColor}`);
}

console.log(`(out) Favorite Color: ${favoriteColor}`);

/*
----- 출력 결과 -----
(in) Favorite Color: blue
(out) Favorite Color: pink
-------------------
*/
```

const 로 변수를 선언하면 선언할 때 초기화는 가능하지만 다른 값으로 재할당하지 못하게 하는 읽기 전용(read only) 변수로 만들 수 있습니다.

예외적으로, const 로 선언한 변수라도 객체 리터럴의 속성으로는 변경할 수 있습니다.

이는 값 자체를 재할당하는 것은 허용하지 않지만 속성 값의 변경은 허용하는 특징이 있기 때문입니다.

아래 예제 코드로 설명해드리겠습니다.

```typescript
const favoriteMonth = "12";

favoriteMonth = "9"; // Uncaught TypeError: Assignment to constant variable.

const person = {
  name: "Serena",
  month: 12,
};

person = {
  name: "Sena",
  month: 9,
}; // Uncaught TypeError: Assignment to constant variable.

// 객체 리터럴의 속성으로는 값 변경이 가능합니다.
person.name = "Sera";
person.month++;
```

## 참고

- TypeScript Quick Start (타입스크립트 퀵스타트) (도서)
