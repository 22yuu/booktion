### 암묵적인 형 변환을 주의하라

자바스크립트는 데이터형 오류에 놀라울 정도로 관대하다.

```js
3 + true; // 4
```

NaN 자신을 동등하지 않다고 처리한다.

```js
var x = NaN;
x === NaN; // false
```

표준 `isNaN` 라이브러리 함수는 스스로 암묵적인 형변환, 즉 값을 테스트하기 전에 인자를 숫자로 바꾸기 때문에 신뢰할 만하지 않다. 따라서 NaN으로 강제 형변환할 수 없는 값들은 isNaN으로 구별할 수 없다.

```js
isNaN("foo"); // true
isNaN(undefined); // true
isNaN({}); // true
isNaN({ valueOf: "foo" }); // true
```

undefined 값을 테스트할 때는 트루시니스를 이용하기 보다 typeof를 사용하거나 undefined와 비교하는 것이 좋다.

```js
function point(x, y) {
  if (!x) {
    x = 320;
  }
  if (!y) {
    y = 240;
  }
  return { x: x, y: y };
}

potin(0, 0); // {x: 320, y: 240}
```

```js
function point(x, y) {
    if( typeof x === "undefined") {
        x = 320;
    }
    if ( typeof === "undefined") {
        y = 240;
    }
    return { x: x, y: y}
}

point(); // {x: 320, y: 240}
point(0, 0); // { x:0, y:0}
```

### 기억할 점

- 데이터형 에러는 암묵적인 강제 형변환에 의해 은밀하게 감춰질 수 있다.
- - 연산자는 인자의 데이터형에 따라 덧셈이나 문자열 병합으로 오버로딩된다.
- 객체는 valueOf를 통해 숫자형으로, toString을 통해 문자열로 강제 형변환된다.
- valueOf 메서드를 가지는 객체는 반드시 valueOf에 의해 생성되는 숫자 값의 문자열 표현을 생성하는 toString 메서드를 구현해야 한다.
- undefined 값을 테스트할 때 트루시니스를 사용하기보다는 typeof를 사용하거나 undefined와 비교하는 것이 좋다.
