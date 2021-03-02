---
title: "[TypeScript] 타입스크립트(TypeScript) 뿌시기 2 (타입 검사와 선언)"
date: 2021-02-25 09:18:04 +09:00
tags: study typescript javascript
comments: true
---

타입스크립트(TypeScript) 뿌시기 2 (타입)
Studying TypeScript 2

## 타입 검사와 선언

언어에 따라 수행하는 타입 검사의 종류는 크게 정적 타입 검사(statically type checking)과 동적 타입 검사(dynamically type check)로 나뉩니다.

먼저 정적 타입 검사란, 컴파일 시(런타임 이전)에 변수의 타입을 검사하는 방식입니다.

이러한 이유로 컴파일 시 에러가 발생하기 때문에 에러 확인을 빠르고 편하게 할 수 있디는 특징이 있습니다.

동적 타입 검사란 런타임 시 변수의 타입을 검사하는 방식입니다.

타입이 입력 값에 따라 결정되므로 예상치 못한 에러를 발생하기 어렵다는 특징이 있습니다.

### 정적 타입 검사를 사용하는 언어와 동적 타입 검사를 사용하는 언어

정적 타입 검사를 사용하는 언어로는 크게 자바(Java), C++ 등이 있고, 동적 타입 검사를 사용하는 언어로는 자바스크립트가 있습니다.

### 타입스크립트(Typescript)는?

타입스크립트의 경우 점진적 타입 검사(gradually type checking) 방식을 사용합니다.

타입스크립트 이외의 점진적 타입 검사를 사용하는 다른 언어로는 파이썬, 자바스크립트 등이 있습니다.

점진적 타입 검사란, 컴파일 시간에 타입 검사를 수행하면서 필요에 따라 타입 선언의 생략을 허용하는 검사 방식입니다.

타입 선언을 생략할 경우 암시적(implicit) 형변환이 일어나게 됩니다.

아래 예제로 설명해드리곘습니다.

```typescript
function add(x, y) {
  return x + y;
}

add(10, 20);
```

add 함수의 매개변수 x 와 y 에 타입을 선언하지 않았지만 컴파일러가 매개변수 x, y 를 오류로 취급하지 않아 오류가 발생하지 않습니다.

이처럼 필요에 따라 타입을 생략할 수도 있고, 점진적으로 타입을 추가할 수도 있습니다.

타입스크립트에서 점진적 타이핑(gradual typing) 을 설명할 때 사용하는 적절한 타입으로는 any 가 있습니다.

any 타입은 모든 타입의 최상위 타입이며, 동적 타입과 정적 타입의 경계선에 있는 타입입니다.

타입스크립트에서 any 타입으로 선언된 변수는 어떤 타입의 변수도 받아들일 수 있으며 심지어 타입이 없는 변수도 받아들입니다.

## 자바스크립트의 동적 타이핑

자바스크립트에는 기본 타입(primitive types) 과 객체 타입(object types) 가 있습니다.

자바스크립트는 타입이 있지만, 타입을 강제할 수는 없고 값을 할당할 때 타입을 추론합니다.

값을 변수에 할당할 때 타입이 정해지는 것을 동적 타이핑(dynamic typing) 이라고 하며 타입스크립트에서는 타입을 선언하지 않으면 입력 값에 따라 타입이 결정됩니다.

하지만 타입을 명시하지 않고 값을 할당하면 정해질 타입을 예측할 수 없다는 점 때문에 변수의 안전한 사용을 위해 타입 검사 로직을 추가해야 합니다.

위의 방법대로 타입 검사 로직을 수행하면 안전하겠지만, 불필요한 코드를 작성해야 하고 런타임 시 비교 연산을 수행해야 하므로 성능에도 좋지 않습니다.

## 타입스크립트(TypeScript) 타입 계층도

타입스크립트는 점진적 타입 검사를 수행하기 때문에 타입 시스템의 계층 구조를 알아두면 좋습니다.

모든 타입을 받을 수 있는 any 타입이 가장 상위에 있고, 밑으로 기본타입, Union, Intersction, Object 등이 있습니다.

## 기본 타입(Primitive types)

기본 타입(Primitive types) 은 보편적으로 많이 사용되는 내장 타입으로, 타입스크립트에서 지원하는 기본 타입의 종류는 다음과 같습니다.

1. string, number, booolean
2. symbol(ECMA 2015에 추가)
3. enum
4. 문자열 리터럴

기본 타입 중 string, number, boolean 은 각각 문자열, 숫자, true/false 값을 다룰 때 사용합니다.

### string

string 타입은 작은 따옴표나 큰 따옴표를 사용해 문자열을 변수에 할당합니다. (타입스크립트 스타일 가이드는 큰 따옴표를 이용할 것을 권장합니다.)

```typescript
const favoriteFruit: string = "Apple";
```

문자열을 표현할 때 역땨옴표(backtick/backquote) 를 이용할 수 있는데, 역따옴표를 이용하면 줄 구분 없이 문장을 입력할 수 있습니다.

또한, 역따옴표 내에는 내장 표현식을 이용할 수 있는데 `${}` 형태를 사용하면 됩니다.

```typescript
const animal: string = "lion";

// 내장 표현식
const favoriteAnimal: string = `My favorite Animal
is ${animal}.
Thx :)
`;

console.log(favoriteAnimal);

/*
----- 출력 결과 -----
My favorite Animal
is lion.
Thx :)
-------------------
*/
```

### number

number 타입은 10진수, 16진수, 2진수, 8진수를 지원합니다.

```typescript
// 10진수
const decimal: number = 11;

// 16진수
const hex: number = 0xb;

// 2진수
const binary: number = 0b1011;

// 8진수
const octal: number = 0o13;
```

### boolean

boolean 타입은 true, false 값을 할당할 수 있습니다.

## 객체 타입

객체 타입은 속성을 포함하고 있으며, 호출 시그니처(call signature), 생성자 시그니처(construct signature) 등으로 구성된 타입입니다.

타입스크립트에서 지원하는 객체 타입은 다음과 같습니다.

1. Array
2. Tuple
3. Function
4. 생성자
5. Class
6. Interface

### Array

Array 는 배열 요소에 대응하는 타입입니다.

배열 요소가 number 라면 `number[]`, string 이라면 `string[]` 이 됩니다.

```typescript
// number array
const favoriteNumber: number[] = [12, 26];

// string array
const favoriteFood: string[] = ["chicken", "pizza"];
```

### Tuple

Tuple 은 배열 요소가 n 개로 정해질 때 각 요소별로 타입을 지정한 타입입니다.

```typescript
let person: [string, number];
person = ["Serena", 10];
```

### 생성자

클래스로부터 생성된 하나의 객체가 여러 생성자의 시그니처르 구성될 때 포함될 수 있는 타입입니다.

생성자 타입 리터럴을(constructor type literal)을 사용해 정의합니다.

생성자 타입 리터럴은 타입 매개변수, 매개변수 목록, 반환 타입으로 구성되며 아래와 같이 선언합니다.

```typescript
new<타입, 타입2, ...>(매개변수1, 매개변수2, ...) => 타입
```

## 기타 타입

그 밖에 다음과 같은 타입을 지원합니다.

1. 유니언(union)
2. 인터섹션(intersection)
3. 특수 타입

### 유니언(union)

유니언 타입은 2개 이상의 타입을 하나의 타입으로 정의한 것입니다.

```typescript
let favroriteThings: string | number;
```

### 인터섹션(intersection)

인터섹션 타입은 두 타입을 합쳐 하나로 만들 수 있는 타입입니다.

```typescript
interface Cat {
  leg: number;
}
interface Bird {
  wing: number;
}

// Cat 과 Bird 각각에 선언된 속성을 합쳐서 하나의 속성처럼 사용할 수 있습니다.
// Cat, Bird 이외의 속성은 허용되지 않습니다.
const catBird: Cat & Bird = { leg: 2, wing: 4 };
```

### 특수 타입 1. void

void 는 함수의 반환 값이 없을 때 사용하는 타입입니다.

```typescript
function say(): void {
  console.log("Hello!");
}

// 변수의 경우 변수에 undefined 나 null 의 값을 할당하는 것은 흔치 않으므로 void 타입을 사용하는 것이 유용하지 않을 수 있습니다.
let unusable: void = undefined;
```

### 특수 타입 2. undefined

undefined 는 null 과 함께 다른 모든 타입의 하위 타입(sub type) 이고, undefined 를 제외한 어떠한 빈 값으로도 초기화되지 않는 타입입니다.

```typescript
let hateThings: undefined = undefined;
```

### 특수 타입 3. null

undefined 와 마찬가지로 null 타입의 변수는 null 이외의 값으로는 초기화 되지 않습니다.

```typescript
let hateThings: null = null;
```

## 자바스크립트의 타입과 차이점

타입스크립트의 타입은 기존 자바스크립트의 타입을 확장한 형태입니다.

객체 타입의 상위 타입으로 any 타입이 추가되었고, 하위 타입으로는 array, interface, tuple 이 추가되었습니다.

any 타입의 특수 타입으로 유니언 타입과 인터섹션 타입이 추가되었습니다.

## 참고

- TypeScript Quick Start (타입스크립트 퀵스타트) (도서)
