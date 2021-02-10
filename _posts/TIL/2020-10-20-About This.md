---
title: '[TIL-10202020] About This'
search: true
categories: 
  - TIL
tags:
    - OOP
    - KR
toc: true
toc_sticky: true
toc_label: " Index"
toc_icon: "heart"
comments: true
show_date: true
read_time: true
related: true
share: true
---

# This

- `this`는 함수 실행시 invocation 방식에 따라 결정되는 객체를 가르키는 키워드이다.
- 함수실행시, 실행되는 excution context에 따라 this는 다르게 설정된다.

## this를 결정하는 다섯가지 Function Invocation 방식

1. 📌 Global

   - global 영역에서 this는 browser 기준으로 window객체, node.js기준으로 module.exports 객체를 바라본다.

     ```js
     console.log(this)
     ```

2. 📌 Function Invocation

   - global 영역에서 생성한 함수를 실행 할 때는 browser 기준으로 window 객체, node.js기준으로 global 객체를 바라본다.

   ```js
   function foo() {
     console.log(this)
   }

   foo()
   ```

3. 📌 Method Invocation

   - 객체의 property로서 함수를 저장하고 있을 때 object.key() 방식으로 그 함수를 호출하여 실행하게 되면 함수 property를 갖고있는 그 객체가 this가 된다.
   - `object.method()` 방식으로 호출하는 방법

   - case 1

   ```js
   const obj = {
     foo: function() {
       console.log(this)
     },
   }

   obj.foo()
   /// obj
   ```

   - case 2

   ```js
   function student(name, subject) {
     return {
       name: name,
       subject: subject,
       learn: function() {
         console.log(this.name + ' is studying ' + subject)
       },
       foo: function() {
         console.log(this)
       },
     }
   }

   let john = student('john', 'coding')
   john.learn() // john is studying coding
   john.foo() // {name:'john', subject:'coding', learn:fn, foo:fn} ==> john 자신 객체
   ```

4. 📌 `new` keyword를 이용한 constructor invocation

   - new 키워드를 통해 생성된 instance가 this로 설정된다.
   - Object Oriented Programming에서 주로 사용한다.

   ```js
   class Student {
     constructor(name) {
       this.name = name
     }

     learn() {
       console.log(this.name + ' is studying coding')
     }
   }

   let john = new Student('John')
   john.learn() // John is studying coding
   john.name // John
   ```

5. 📌 .call or .apply 와 같은 javascript built-in method를 이용하여 호출

   - 함수를 호출, 실행 할 때 this값을 force로 어떤 특정 객체로 지정하여 실행 할 때 사용
   - .call & .apply method 는 첫번째 인자로 this값을 받는다.
   - .apply는 두번재 인자로 Array Type의 인자를 받는다.
   - `fn.call(this, parameter1, parameter2, ..)`
   - `fn.apply(this, array parameter1, array parameter2, ..)`
   - JavaScript Built-in Prototype의 method를 차용하여 this를 지정하여 실행 할 때,

   ```js
   let phoneNumber = '010-1234-5678'
   phoneNumber.split('-')
   String.prototype.split.call(phoneNumber, '-')
   ''.split.call(phoneNumber, '-')
   // 위의 세가지 방법의 실행 결과는 같다
   ```

   - Array Type이 아닌 Array-like Type의 자료구조에 Array.prototype method를 차용하여 사용할 때,

   ```js
   let allDivs = document.querySelectorAll('div') // Node List 라는 유사배열이다
   Array.prototype.map.call(allDivs, function(el) {
     return el.className
   })
   ```

   - apply를 사용하여 array type에 method를 적용할 때

   ```js
   let arr = [1, 2, 3, 4]
   Math.max.apply(null, arr) // Math는 생성자가 아니므로 this를 설정할 필요가 없다.
   Math.max(...arr) // rest parameter를 이용하여 배열을 인자로서 사용할 수 있다.
   ```

   - Object Oriented Programming에서 많이 사용되는 예제

   ```js
   function PriceTag(name, price) {
     this.name = name
     this.price = price
   }

   function Food(name, price) {
     PriceTag.call(Food, name, price)
     this.catetory = food
   }

   let pizza = Food('peperoni', 15)
   //pizza 의 name은 'peperoni'이고 price는 15 이다
   ```

6. ## 📌 binding `this` by using .bind method

   - .bind method는 .call, .apply처럼 this 값을 bind하지만 함수를 바로 실행하는것이 아니라 this값만 binding한다.
   - `fn.bind(this, parameter1, parameter2, ..)`
   - Event Handler를 생성할 때 this를 bind할 때,

   ```js
   ;<button id="btn">click</button>
   let btn = document.querySelector('#btn')
   btn.onclick = handleClick

   let sayHello = {
     say: 'Hello, welcome!',
   }

   function handleClick() {
     console.log(this, this.say)
   }
   ```

   여기서 this는 btn이므로 button을 클릭하면 button HTML element 를 출력한다. 그럼 this값을 다른 객체로 bind해서 사용해보자.

   ```js
   btn.onclick = handleClick.bind(sayHello)

   function clickAlert() {
     alert(this, this.sayHi)
   }
   ```

   .bind method를 사용하여 this값을 `sayHello`로 지정하였다. button을 클릭하면 this는 sayHello 객체를 바라보고 있고, this.sayHi에 접근 가능하여 'Hello, welcome' 을 출력하는 것을 확인 할 수 있다.
   이처럼 함수를 바로 실행하지 않고 어떤 action이 있을 때 실행되야할 경우에 this값을 설정해줄 때 bind를 사용한다.

   - `setTimeout` 을 사용할 때 bind 사용

     - setTimout은 callback함수와 시간을 인자로 받고 인자로 받은 시간만큼 함수실행을 지연을 시켜서 callback함수를 비동기적으로 실행할 수 있는 Web APIs 중에 하나이다.
     - setTimeout 은 this를 항상 window 객체를 this값으로 binding 하는 특징이 있다.
     - setTimout 예제,

     ```js
     class Shape {
       constructor(width, height) {
         this.width = width
         this.height = height
       }

       printArea() {
         console.log(this.width * this.height)
       }

       printSync() {
         this.printArea()
       }

       printAsync() {
         setTimeout(this.printArea, 3000)
       }
     }
     ```

     class Shape을 생성하고 넓이를 계산해서 출력하는 함수, 그 함수를 동기적으로 실행하는 함수, setTimout을 이용하여 비동기적으로 실행하는 함수등의 method들을 생성

     ```js
     let rectangle = new Shape(10, 5)
     rectangle.printArea()
     rectangle.printSync()
     rectangle.printAsync()
     ```

     위와 같이 실행하면 printAsync()를 실행 했을 때 인자로 받은 시간후에 callback함수가 작동은 하지만 원하는값이 출력되지 않는것을 확인 할 수 있다. 이유는 setTimeout에서 this가 rectangle instance가 아닌 window 객체를 바라보고 있기 때문이다. 그럼 bind를 사용하여 setTimeout의 this를 instance로 binding해서 실행해보자

     ```js
     printAsync() {
       setTimeout(this.printArea.bind(this, 3000)
     }
     ```

     printAsync method 를 위와 같이 수정하면 원하던 대로 잘 작동하는 것을 확인 할 수 있다.
     **또 다른 solution으로는 Arrow Function 표현식으로 함수를 선언하는 것이다.**

     ```js
     printAsync() {
       setTimeout(() => this.printArea(), 3000)
     }
     ```

   * Arrow Function을 사용할 때 this를 따로 bind하지 않아도 잘 작동이 되는 이유는 일반적으로 this는 함수가 호출(function invocation) 될 때 그 함수의 호출 방식에 따라서 this 값이 설정되는데 Arrow Function은 호출 될 때 this값을 설정하지 않기 때문이다. 대신 Arrow Function을 둘러싸는 scope의 범위(lexical scope)의 this를 사용한다. 현재 범위에 this값이 존재하지 않을 때는 상위로 올라가면서 this값을 찾는다.  
     _다음의 MDN공식문서 발췌 참고_

   - 화살표 함수는 자신의 `this`가 없습니다. 대신 화살표 함수를 둘러싸는 렉시컬 범위(lexical scope)의 `this`가 사용됩니다. 화살표 함수는 일반 변수 조회 규칙(normal variable lookup rules)을 따릅니다. 때문에 현재 범위에서 존재하지 않는 `this`를 찾을 때, 화살표 함수는 바깥 범위에서 `this`를 찾는것으로 검색을 끝내게 됩니다.
     따라서 다음 코드에서 `setInterval`에 전달된 함수 내부의 `this`는 `setInterval`을 포함한 function의 `this`와 동일한 값을 갖습니다.

   ```js
   function Person() {
     this.age = 0

     setInterval(() => {
       this.age++ // this는 상위범위의 Person 객체를 참조
     }, 1000)
   }
   ```
