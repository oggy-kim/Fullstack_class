# Javascript

- ## **[함수(Function)](#함수(Function))**

  - [작성방법](##작성방법)
  - [함수의 매개변수](##함수의&nbsp;매개변수(전달인자))
  - 

- ## **[객체(Object)](##객체)**

  - [객체 선언 및 호출](###객체&nbsp;선언&nbsp;및&nbsp;호출)

- ## **[내장객체](##내장&nbsp;객체)**

- ## **[BOM(Browser Object Model)](##BOM(Browser&nbsp;Object&nbsp;Model))**

- ## **[정규표현식(Regular Expression)](##정규표현식(Regular&nbsp;Expression))**

***

# 함수(Function)

## 작성방법

* `function name(){ source code } }` : 선언함수

```javascript
<button onclick="test();">Execute</button>
<p id="p1"></p>
<script>
    function test1(){
        document.getElementById("p1").innerHTML = "test() 함수 실행됨.";
    }
</script>
```

-> 버튼을 눌렀을 때 _p1_ 태그 안쪽에 test() 함수 실행됨 추가

* `var = function(){ source code }` : 익명함수(이벤트핸들러 작성시 주로 사용)

```javascript
<button onclick="test();">Execute</button>
<p id="p1"></p>
<script>
    test2 = function(){
        document.getElementById("p1").innerHTML = "test() 함수 실행 확인.";
    }
</script>
```

-> 버튼을 눌렀을 때 _p1_ 태그 안쪽에 test() 함수 실행됨 추가

* `(function(){})();` : 스스로 실행하는 함수

```javascript
<p id="p1"></p>
<script>
    // 문서 열고 바로 자동 실행됨
    (function(){
        document.getElementById("p1").innerHTML = "test() 함수 실행";
    })();
</script>
```

-> html 문서를 열면 바로 자동으로 실행됨

## 함수의 매개변수(전달인자)

```javascript
<button onclick="function();">Execute</button>
<p id="p1"></p>

<script>
function test(value){
    document.getElementById("p1").innerHTML += value + " ";
}

function(){
    // 정상 호출
    test(window.prompt("메세지를 입력하세요."));

    // 지정된 매개변수보다 많은 개수를 호출하는 것을 허용한다.
    // (단, 초과된 매개변수는 무시)
    test('안녕하세요', '반갑습니다');

    // 지정된 매개변수보다 적게 호출하는 것도 허용한다.
    // (단, 선언이 안된 매개변수는 undefined로 자동 설정된다.)
    test();
}
</script>
```

-> 'prompt에 입력한 value값', '안녕하세요', 'undefined' 실행

## 함수의 return 처리

```javascript
<button onclick="test();">Execute</button>
<p id="p1"></p>
<script>
    function returnFunction(){
        return Math.floor(Math.random() * 10) + 1; // 1~10 사이의 랜덤값 추출
    }
    function test(){
        document.getElementById("p1").innerHTML = returnFunction();
    }
</script>
```

-> test() 함수의 returnFunction()를 위해, 위의 returnFunction()을 실행한 return값 보여줌

## 가변인자 함수 테스트

가변인자 함수 : 매개변수의 개수가 변하는 함수.
함수 내부에 _arguments_ 라는 Object가 자동으로 생성
매개변수가 지정되지 않은 값이 넘어오면 _arguments_ 객체에 인덱스 부여해서 순서대로 저장

```javascript
<script>
    function sumAll(){
        p = document.getElementById("p");

        p.innerHTML = "";
        p.innerHTML += 'arguments의 타입 : ' + typeof(arguments) + "<br>"; // object
        p.innerHTML += 'arguments의 길이 : ' + arguments.length + "<br>"; // 10
        p.innerHTML += 'arguments : ' + arguments + "<br>"; // [object Arguments]
   }
    function test(){
        sumAll(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    }
</script>
```

## 매개변수로 함수 전달

> 함수 또한 하나의 자료형이기 때문에 매개변수로 전달 가능! 

### 선언적 함수를 매개변수로 전달

```javascript
<script>
    function callFunction(otherFunction) {  // 선언적 함수를 매개변수로 받는 함수
        for(var i = 0; i < 10; i++) {
            otherFunction(i + 1);
        }
        alert('10번 클릭하셨습니다. 끝!');
    }

    function justFunction(i) { // 매개변수로 들어갈 선언적 함수
        alert(i + '번 클릭하셨습니다.'); // 1~10번 클릭하셨습니다 창 띄워줌
    }
</script>
```

### 익명 함수를 매개변수로 전달

```javascript
<script>
    function callFunction(otherFunction) { // 함수를 매개변수로 받는 함수
        for(var i = 0; i < 10; i++) {
            otherFunction(i);
            }
        }  
    callFunction(function(i) {
        document.getElementById("area1").innerHTML += (i + 1) + '번째 함수 호출!<br>';
        });
</script>
```

### 익명 함수를 리턴하는 함수

> `함수명()();` 형태로 호출

```javascript
<input type="text" id="text1">
<button onclick="returnFunction()();">Execute</button>
<!-- 첫번째 () : 함수 호출 / 두번째 () : 리턴된 함수 호출 -->
<script>
    function returnFunction() {
        var text1 = document.getElementById("text1");
        return function(){
            text1.disabled = true; // 비활성화
            alert("비활성화 되어도 접근 가능! : " + text1.value);
        }
    }
</script>
```

## 클로저(Closure)

```
클로저는 독립적인 (자유) 변수를 가리키는 함수이다. 또는, 클로저 안에 정의된 함수는 만들어진 환경을 ‘기억한다’.
지역변수의 scope(범위)는 선언된 함수 내부로 함수가 실행될 때 생성되고 함수가 종료될 때 사라지지만,
함수를 리턴하는 함수(클로저)를 이용하면 규칙을 위반하고 사라진 지역변수에 접근이 가능해짐
```

```javascipt
<script>
    <button onclick="test1('Eder')();">Execute</button>
    function test1(name) {
        var output = "Hello, " + name + ":)";

        function innerFn() {
            alert(output);
        }
        return innerFn; // Hello, Eder:)
    }
</script>
```

## Javascript 내장함수

### 인코딩과 디코딩 관련 내장함수

> 웹 통신 시 유니코드 문자는 오작동을 일으킬 문제가 있어, **인코딩**이 필요하다.

```
escape : 영문 알파벳, 숫자, 일부 특수문자(@, *, -, _, ., /)를 제외한 모든 문자를 인코딩
encodeURI : escape에서 인터넷주소에 사용되는 일부 특수문자(:, ;, /, =, ?, &)는 변환하지 않음
encodeURIComponent : 알파벳과 숫자를 제외한 모든 문자를 인코딩(UTF-8방식)
unescape : escape로 인코딩된 문자를 디코딩
decodeURI : endodeURI로 인코딩된 문자를 디코딩
decodeURIComponent : encodeURIComponent로 인코딩된 문자를 디코딩
```

```javascript
<script>
    function test() {
        var URI = "http://search.daum.net/search?w=tot&q=안녕";
        var esURI = escape(URI);
        var enURI = encodeURI(URI);
        var enURIC = encodeURIComponent(URI);

        console.log(esURI);
        console.log(enURI);
        console.log(enURIC);

        console.log(unescape(esURI));
        console.log(decodeURI(enURI));
        console.log(decodeURIComponent(enURIC));
        // 인코딩 한것과 매칭되지 않는 함수로 디코딩 시 원본 URI 내용 확인불가
    }
<script>
```

### eval() 함수

> 문자열을 자바스크립트 코드로 변환해 실행하는 함수

```javascript
<button onclick="test();">Execute</button>
<script>
    function test() {
        var testEval = "";

        testEval += "var number1 = parseInt('2');";
        testEval += "var number2 = parseInt('3');";
        testEval += "var sum = 0;";
        testEval += "sum = number1 + number2;";
        testEval += "console.log(number1 + '과' + number2 + '의 합은 : ' + sum + '입니다.');";
        eval(testEval); // testEval을 코드로 변환함
    }
</script>
```

## 객체

### 객체 선언 및 호출

> 객체는 키 값을 사용하여 속성을 식별
> 중괄호를 사용하여 객체를 생성하며, 속성에는 모든 자료형이 올 수 있다.

```javascript
<script>
    function test(){
        var product = {
                pName:'Strawberry Juice',
                type:'Fruit',
                ingredient:['strawberry', 'sugar'],
                origin:'Korea'
        }

        // 객체명.속성명으로 접근하기
        console.log(product.pName); // Strawberry Juice
        console.log(product.type); // Fruit
        console.log(product.ingredient[0]); // strawberry
        console.log(product.ingredient[1]); // sugar
        console.log(product.origin); // Korea

        // 객체명['속성명']으로 접근하기(위와 동일한 결과)
        console.log(product['pName']);
        console.log(product['type']);
        console.log(product['ingredient'][0]);
        console.log(product['origin']);
</script>
```

### 객체의 키 식별자 테스트

> 객체의 키는 *모든 문자열* 사용 가능.
> 단, 식별자로 사용할 수 없는 단어를 사용한 경우에는 무조건 `[]` *대괄호*를 사용해야 접근가능

```javascript
<script>
    function test() {
        var objTest = {
            'hello World':'Hello World!!',
            '!@#$%^&*()': 1234567890
        }

        // console.log(objTest.'hello world');
        // console.log(objTest.'!@#$%^&*()');
        // -> 식별자로 사용할 수 없는 단어를 사용했기에, 접근 불가능.

        // 대괄호를 사용하여 접근 가능
        console.log(objTest['hello World']);
        console.log(objTest['!@#$%^&*()']);
    }
</script>
```

### 객체의 메소드 속성

> 객체의 속성 중 함수 자료형인 속성을 메소드라고 부름

```javascript
<script>
    function test() {
        var name = "이재성";
        var player = {
            name:'서보민',
            play:function(role){
                // 객체 내에서 자신의 속성을 호출할 때에는 반드시 this 사용
                console.log(this.name + '이 ' + role + '을 합니다.');

                console.log('name : ' + name); // 이재성
                console.log('this.name : ' + this.name); // 서보민
            }
        }
        console.log(player.play('연습')); // 서보민이 연습을 합니다.
    }
</script>
```

### 반복문

> 객체의 속성을 살펴볼 때에는 단순 for문으로는 사용 불가능, `for in` 문을 사용해야 함

```
for in문 : 객체의 속성에 순차적으로 접근
```

```javascript
<script>
    function test() { 
        var game = {
            title: 'FM2020',
            price: '$35.2',
            language : 'Supports Korean',
            supportOS : 'windows x64, x86',
            service: true
        }

        for(var key in game) {
            console.log(key + " : " + game[key]);
            // title : FM2020
            // price : $35.2
            // language : Supports Korean
            // supportOS : windows x64, x86
            // service : true
        }
    }
</script>
```

### in / with

*in* : 객체 _내부_ 에 해당 속성이 있는지 확인하는 키워드

*with* : 코드를 줄여주는 키워드. 호출 시 객체명 생략 가능

```javascript

<script>
    function test() {
        var name = '현정';
        var kor = 100;
        var eng = 80;
        var math = 90;

        // 객체 생성
        var student = {
            name: name,
            kor: kor,
            eng: eng,
            math: math
        }

        // in 사용하여 객체에 속성 존재여부 확인
        console.log('name' in student); // true
        console.log('kor' in student); // true
        console.log('eng' in student); // true
        console.log('math' in student); // true
        console.log('sum' in student); // false

        // with 키워드 사용하여 접근
        with(student) { // -> with를 사용해 student라는 객체명을 여러번 사용하지 않아도 됨
            console.log(name); // 현정
            console.log(kor); // 100
            console.log(eng); // 80
            console.log(math); // 90
            console.log(kor + eng + math); // 270 (객체 내 속성간의 sum)
        }
</script>
```

### 속성 추가/제거

> 처음 객체생성한 이후 속성의 추가/제거를 동적으로 처리 가능

```javascript
<script>
    function test() {
        // 빈 객체 선언
        var player = {}

        // 객체에 속성을 추가
        player.name = "Eder";
        player.hobby = "Football";
        player.dream = "Kleague champ";

        console.log(player);

        // 객체에서 속성 제거
        delete(player.dream); 

        console.log(player); // dream : "Kleague champ"이 삭제됨
    }
</script>
```

### 객체 배열

객체와 배열을 활용한 데이터 관리

```javascript
<script>
    function test() {
        // 임의의 객체 생성
        var student0 = {name:'보민', java:100, oracle: 90, html5: 80, CSS3: 70, javascript: 60}
        var student1 = {name:'고민', java:100, oracle: 90, html5: 80, CSS3: 70, javascript: 60}
        var student2 = {name:'노민', java:100, oracle: 90, html5: 80, CSS3: 70, javascript: 60}
        var student3 = {name:'도민', java:100, oracle: 90, html5: 80, CSS3: 70, javascript: 60}

        // 배열 선언
        var students = [];
        // 배열에 객체 추가
        students.push(student0);
        students.push(student1);
        students.push(student2);
        students.push(student3);

        // 각 개체별 메소드 추가
        for(var i in students) {
            students[i].getSum = function(){
                return this.java + this.oracle + this.html5 + this.CSS3 + this.javascript;
            }
            students[i].getAvg = function(){
                return this.getSum() / 5;
            }
        }

        // 모든 객체의 정보가 담긴 배열의 메소드를 통해 총점과 평균 출력
        for(var i in students) {
            with(students[i]) {
                console.log("이름 : " + name + ", 총점 : " + getSum() + ", 평균 : " + getAvg());
                // 이름 : 보민, 총점 : 400, 평균 : 80
                // 이름 : 고민, 총점 : 400, 평균 : 80
                // 이름 : 노민, 총점 : 400, 평균 : 80
                // 이름 : 도민, 총점 : 400, 평균 : 80
            }
        } 
    }
</script>
```

### 객체 관련 키워드

1. instanceof 키워드

> 해당 객체가 어떤 생성자함수로 생성이 되었는지 검사

```javascript
<script>
    function Laptop(pName, price) { // 객체 정의
        this.pName = pName;
        this.price = price;
    }

    function test() {
        var myLaptop = new Laptop("Dell XPS15 9570", 2500000); // 생성자를 통한 객체 생성
        console.log(myLaptop instanceof Laptop); // true
        console.log(myLaptop instanceof Student); // false
        }
</script>
```

## 캡슐화(Encapsulation) & 상속(Inherit)

### 캡슐화

```
생성자 함수에서 속성 선언시, this 키워드를 사용하지 않고 지역변수로 선언하게 되면
캡슐화된 객체의 속성은 직접 접근이 불가능
    -> 간접 접근할 수 있도록 this 키워드를 사용하여 getter/setter 메소드 작성
```

```javascript
<script>
    function FootballLeague(ln, tc, t){ // 객체 정의
        var leagueName = ln; // 지역변수로 선언
        var teamCount = tc;
        var teams = t;

        // getter
        this.getLeagueName = function() {
            return leagueName;
        }

        this.getTeamCount = function(){
            return teamCount;
        }

        this.getTeams = function(){
            return teams;
        }

        // setter
        this.setLeagueName = function(ln){
            leagueName = ln;
        }

        this.setTeamCount = function(t){
            teamCount = tc;
        }

        this.setTeams = function(t){
            teams = t;
        }
    }
    function test() {
        var ln = 'K League';
        var tc = 4;
        var t = ['SeongnamFC', 'Jeonbuk Hyundai', 'SuwonFC', 'Busan IPark'];  
        // 생성자 함수를 이용하여 객체 생성
        var kleague = new FootballLeague(ln, tc, t);

        console.log(kleague); // K League
        console.log(kleague.teams); // undefined : 직접 접근 불가

        console.log(kleague.getTeamCount()); // 4 : 간접 접근

        // 객체에 간접 접근해서 탈퇴멤버 삭제
        kleague.getTeams().splice(kleague.getTeams().indexOf('SuwonFC'),1);
        kleague.setTeamCount(3);

        console.log(kleague.getTeamCount()); // 3 : 간접 접근
        console.log(kelague.getTeams()); // SeongnamFC, Jeonbuk Hyundai, Busan IPark
    }
</script>
```

### 상속

Javascript에는 Class가 존재하지 않아 Java와 같은 상속을 할 수 없음
대신 *prototype*이라는 것을 이용하여 상속과 비슷한 효과를 낼 수 있음

### 프로토타입(Prototype)

Javascript에서 객체와 객체를 연결하여 속성, 메소드를 공유함
(단, 공유한 정보는 한쪽 방향으로만 공유됨)

* 프로토타입의 종류

    * `__proto__` (Prototype Link) : 상위 객체로부터 물려받은 프로토타입 정보
    * `prototype`(Prototype Object) : 하위 객체로 물려줄 프로토타입 정보(현재 객체 정보)
    * -> `console.log(객체);` 호출 시 개발자 도구에서 확인 가능

```javascript
<script>
    function Book(t, p, dr){ // 캡슐화 된 Book 생성자 함수
        var title = t;
        var price = p;
        var discountRate = dr;

        // getter
        this.getTitle = function(){
            return title;
        }

        this.getPrice = function(){
            return price;
        }

        this.getDiscountRate = function(){
            return discountRate;
        }
        
        // setter
        this.setTitle = function(t){
            title = t;
        }

        this.setPrice = function(p){
            if(p < 0){
                throw '가격은 음수값을 가질 수 없습니다.';
            }else{
                price = p;
            }
        }

        this.setDiscountRate = function(dr){
            if(dr < 0){
                throw '할인율은 음수값을 가질 수 없습니다.';
            }else{
                discountRate = dr;
            }
        }
        // this.getSellPrice = function(){
        //     return this.getPrice() * (1 - this.getDiscountRate());
        // }
        // -> Book 객체 내에 직접 메소드 구현
    }
    
    // Book 객체 정보를 나타내는 prototype에 함수 속성 추가
    // 바로 위 주석 처리 된 this.getSellPrice와 같은 기능을 함
    Book.prototype.getSellPrice = function(){
        return this.getPrice() * (1 - this.getDiscountRate());
    }

    function test(){
        var book1 = new Book("Do it! Javascript", 20000, 0.1); // Book 객체 생성
        console.log(book1.getTitle() + book1.getSellPrice()); // Do it! Javascript18000
    }
</script>
```

상속 확인

```javascript
<script>
    function Novel(t, p, dr, tp){ // Book 생성자 함수를 가져와 지역 변수에 담음
        this.base = Book;

        this.base(t, p, dr); // 가져온 Book 생성자 함수를 호출하여 객체 생성

        var type = tp; // 접근 제한 된 속성 선언

        // 간접 접근을 위한 getter/setter 생성
        this.getType = function(){ 
            return type;
        }

        this.setType= function(tp){
            type = tp;
        }
    }

    console.log(Book.prototype); // -> Book.prototype에는 Book 생성자와 getSellPrice()가 존재
    Novel.prototype = new Book();
    console.log(Novel.prototype); // -> Book 생성자에 존재하는 function들과 Book.prototype이 담김

    function test(){ // tp 속성을 추가한 Novel 객체로 생성, 기존 Book 객체의 속성을 그대로 상속함
        var novel1 = new Novel('나무', 30000, 0.2, '소설');

        console.log(novel1.getTitle()); // 나무
        console.log(novel1.getSellPrice()); // 24000
    }
</script>
```

## 내장 객체

### Object 객체

> Javascript의 가장 기본적인 내장객체로, Object 생성자 함수를 통해 만들어진 인스턴스

* 생성 방법

```javascript
<script>
    function test1(){
        // Object를 생성하는 방법
        var obj1 = {};
        var obj2 = new Object();

        console.log(obj1); // Object
        console.log(obj2); // Object
    }
</script>
```

* Object 객체 기본메소드 : hasOwnProperty() / propertyIsEnumerable()

  * hasOwnProperty() : 속성을 가지고 있는지 확인하는 메소드로 true와 false를 리턴
  * propertyIsEnumerable() : 열거할 수 있는 프로퍼티란 내부적으로 enumerable 플래그가 true로 설정된 Property -> for / in 문으로 접근할 수 있다.

```javascript
<script>
    function test(){
        var object = { // name, age를 가진 객체 생성
            name: "asd",
            age: 20
        } 

        console.log(object.hasOwnProperty('name')); // true
        console.log(object.hasOwnProperty('age')); // true
        console.log(object.hasOwnProperty('score')); // false

        console.log(object.propertyIsEnumerable('name')); // true
        console.log(object.propertyIsEnumerable('age')); // true
    }
</script>
```

* constructor() 메소드

  * Object가 가지는 객체의 생성자 메소드로, 자료형을 검사할 때 유용하게 사용할 수 있음

```javascript
<script>
    function test(){
        var num1 = 120;
        var num2 = new Number(120);

        console.log(typeof(num1)); // number
        console.log(typeof(num2)); // object
        console.log(num1 + num2); // 240(형태가 다르지만 계산은 가능)

        // 두 대상을 같은 자료형으로 취급하고 싶을 때 constructor 메소드로 사용
        console.log(num1.constructor == Number); // true
        console.log(num2.constructor == Number); // true
        }
</script>
```

### Number 객체

* toFixed() : 숫자를 고정 소수점 자리로 나타낸 문자열을 만든다.

```javascript
<script>
    function test(){
        var num1 = 123.456789;
        var num2 = 123;

        console.log(num1); // 123.456789
        console.log(num2); // 123
        console.log(num1.toFixed(1)); // 123.5 : 반올림
        console.log(num1.toFixed(4)); // 123.4568 
        console.log(num2.toFixed(4)); // 123.0000
        console.log(typeof(num1.toFixed(1))); // String
    }
</script>
```

### String 객체의 HTML 관련 메소드

* String 객체의 메소드는 크게 기본 메소드 & HTML 관련 메소드로 구분

```javascript
<script>
    function test(){
        var str = "Javascript";

        // 각 메소드에 따라 HTML에 표시되는 내용이 변경됨
        console.log(str);
        console.log(str.big());
        console.log(str.bold());
        console.log(str.fontcolor('red'));
        console.log(str.fontsize(20));
        console.log(str.italics());
        console.log(str.link("http://www.google.com"));
        console.log(str.strike());
        console.log(str.sub());
        console.log(str.sup());
    }
</script>
```

### Date 객체

* Date 객체 입력값에 따른 출력 확인

```javascript
<script>
    function test(){
        // GMT 시간
        var date1 = new Date();
        var date2 = new Date('June 18'); // Jun 등으로 작성도 가능
        var date3 = new Date('June 18, 2019');
        var date4 = new Date('June 18, 2019 09:00:00');

        console.log(date1); // Mon Sep 09 2019 14:52:49 GMT+0900 (한국 표준시)
        console.log(date2); // Mon Jun 18 2001 00:00:00 GMT+0900 (한국 표준시)
        console.log(date3); // Tue Jun 18 2019 00:00:00 GMT+0900 (한국 표준시)
        console.log(date4); // Tue Jun 18 2019 09:00:00 GMT+0900 (한국 표준시)

        
        // UTC 시간
        var date5 = new Date(2019, 6-1, 18);
        var date6 = new Date(2019, 6-1, 18, 9, 0, 0);

        console.log(date5); // Tue Jun 18 2019 00:00:00 GMT+0900 (한국 표준시)
        console.log(date6); // Tue Jun 18 2019 09:00:00 GMT+0900 (한국 표준시)
    }
</script>
```

### Date 객체 메소드

```javascript
<script>
    function test(){
        var date = new Date();

        console.log(date.get)


        console.log(date.getFullYear()); // 2019
        console.log(date.getMonth()); // 8(실제는 9월이나, 월은 0부터 count)
        console.log(date.getHours()); // 14
        console.log(date.getMinutes()); // 55
        console.log(date.getMilliseconds()); // 656
        // UTC(협정세계시)와 시스템이 속해 있는 지역의 시간의 차이 리턴
        console.log(date.getTimezoneOffset()); // -540
        console.log(date.getTime()); // 1568008547656

        // 1970년 1월 1일 자정 기준 밀리세컨 단위로 객체 생성
        var date2 = new Date(new Date(2019, 5, 18, 9, 0, 0, 0).getTime());
        console.log(date2); // Tue Jun 18 2019 09:00:00 GMT+0900 (한국 표준시)

        // 날짜 사이의 간격 구하기
        var now = new Date(); // 현재 날짜
        var start = new Date('June 18, 2019'); // 시작 시점
        
        var interval = now.getTime() - start.getTime();
        interval = Math.floor(interval / (1000*60*60*24)); // Milliseconds를 일자 단위로 변환
        alert('It's ' + interval + 'days since I studied coding.... ');
    }
</script>
```

## BOM(Browser Object Model)

### Window 객체는 Javascript의 최상위 객체로, BOM과 DOM으로 나뉨

> BOM(Browser Object Model) : location 객체, navigator 객체, history 객체, screen 객체
> DOM(Document Object Model) : document 객체

* open() 메소드
```javascript
<button onclick="test1();">Javascript</button>
<button onclick="test2();">Google</button>
<script>
    function test1() {
        // window.open();

        // window.open('주소'), '이름 또는 open방식,', '형태'); 로 작성
        window.open("Javascript.md", 'popup1', 'width=300, height=360'); // 클릭시 새 팝업창으로 Javascript.md 파일 오픈
    }
    function test2() {
        window.open("http://www.google.com", "_self"); // 클릭시 기존 창에 google 사이트 오픈
    }
</script>
```

### timer() 메소드

* setTimeout() : 정해진 시간 이후 실행하는 메소드

```javascript
<script>
    function test3() {
        var myWindow = window.open(); // 새 윈도우창 열림
        myWindow.alert("3초 후에 이 페이지는 종료됩니다."); // 팝업창
        window.setTimeout(function() { // 3000Miliseconds(3초) 후 myWindow.close() Function 수행
            myWindow.close();
        }, 3000);
    }
</script>
```

* setInterval() : 정해진 시간마다 반복적으로 메소드를 실행

```javascript
<script>
    // 시계 구현하는 function
    function clock() {
        window.setInterval(function(){ // area의 innerHTML에 1초에 한번씩 시간을 업데이트해줌
            var date = new Date();
            area.innerHTML =
            date.getHours() + " : " + date.getMinutes() + " : " + date.getSeconds();
        },1000); 
    }
</script>
```

* clearInterval() : 반복되는 인터벌 설정을 해제하는 메소드

```javascript
// 버튼을 누름에 따라 스톱워치처럼 구현하는 메소드

<button onclick="test1();">GO!</button>
<button onclick="test1_2();">STOP!</button>
<button onclick="test1_3();">RESET!</button>
<div id="area"></div>
<script>
    var stop = false;
    var timer;
    var count = 0;

    function test1() {
        var area2 = document.getElementById("area");

            timer = window.setInterval(function(){
                area2.innerHTML = parseInt(count/100/60%60) + " : " + // 분
                                    parseInt(count/100%60) + " : " + // 초
                                    parseInt(count%100);             // 1/100초
                count++;
            }, 10); // 0.01초마다 update
    }

    function test1_2() {
        clearInterval(timer); // test1()에서 실행중인 timer의 setInterval 메소드를 중지
    }

    function test1_3() {
        clearInterval(timer);
        count = 0; // 다시 숫자를 0으로 변경
        area2.innerHTML = parseInt(count/100/60%60) + " : " +
                                    parseInt(count/100%60) + " : " +
                                    parseInt(count%100);
    }
</script>
```

### screen 객체

> 웹 브라우저 화면이 아닌 운영체제 화면의 속성을 가지는 객체

```javascript
<script>
    function test() {
        var width = screen.width;
        var height = screen.height;

        child = window.open("","", "width=800, height=500"); // 정해진 크기의 빈 창 열기

        child.resizeTo(width, height);

        setInterval(function() {
            child.resizeBy(-20, -20); // 20씩 width, height를 감소
            child.moveBy(10, 10); // 10씩 이동
        }, 500); // 500Milliseconds마다(0.5초)

        console.log(screen.height); // 화면높이
        console.log(screen.width); // 화면너비
        console.log(screen.availWidth); // 실제 화면에서 사용 가능한 너비
        console.log(screen.availHeight); // 실제 화면에서 사용 가능한 높이
        console.log(screen.colorDepth); // 사용 가능한 색상 수
        console.log(screen.pixelDepth); // 한 픽셀 당 비트 수
    }
</script>
```

### location 객체

* 브라우저의 주소 표시줄과 관련된 객체

  * Location 객체의 속성 확인

```javascript
<script>
    function test(){
        for(var key in location) {
            console.log(key + " : " + location[key]);
        }
    }
</script>
```

  * location 객체를 통한 사이트 이동

```javascript
<button onclick="location = 'http://www.google.com'">구글로 이동</button>
<button onclick="location.href = 'http://www.google.com'">구글로 이동</button>
<br>

<button onclick="location = location">새로고침</button>
<button onclick="location.href = location.href">새로고침</button>
<!-- reload()는 현재 위치에서 새로고침 -->
<button onclick="location.reload()">새로고침(현 위치 유지)</button>
<br>

<button onclick="location.assign('http://google.com')">구글로 이동</button>
<!-- replace는 뒤로가기 사용 불가 -->
<button onclick="location.replace('http://google.com')">구글로 이동</button>
```

### navigator 객체

* 웹페이지를 실행하고 있는 브라우저에 대한 정보를 가지고 있는 객체

```javascript
<script>
    function test() {
        for(var key in navigator) {
            str += (key + " : " + navigator[key] + "\n");
        }
        alert(str); // 알림창으로 navigator 객체의 속성 확인

        // navigator 객체의 주요속성
        console.log("브라우저의 코드명 : " + navigator.appCodeName);
        console.log("브라우저의 이름 : " + navigator.appName);
        console.log("브라우저 전체정보 : " + navigator.userAgent);
        console.log("브라우저 언어 : " + navigator.language);
        console.log("사용중인 운영체제 : " + navigator.platform);
    }
</script>
```

### History 객체

* 페이지에서 활동한 이력 등을 확인 가능함

```javascript
<script>
    function test() {

        console.log(history.length); /* 뒤로가기 할 수 있는 페이지 수 */

        history.back(); // 현재 페이지의 한단계 이전페이지로 이동
        history.go(-1); // 이전 또는 이후 페이지의 이동이 가능(인자 -1 : 이전, 1 : 이후)
        history.forward(); //  이후 페이지인 다음 페이지로 이동(history.go(1) 과 동일)
    }
</script>
```

***

## DOM(Document Object Model)

HTML에 있는 태그들을 구조화(트리)하였을 때, 각각의 태그를 **노드(Node)**라고 한다.

### 텍스트노드(TextNode)가 있는 노드 생성

```javascript
<div id="area"></div> // area div 영역에 생성
<script>
    function test() {
        // element 생성
        var title = document.createElement("h3"); // <h3></h3> 태그를 의미

        // textnode 생성
        var textNode = document.createTextNode('Hello, World!'); // hn, p 태그 등에 들어가는 text를 의미

        // 노드를 연결
        title.appendChild(textNode); // title이라는 <h3> 태그에 textNode의 text 연결 --> <h3>Hello, World!</h3>

        // area1에 출력
        document.getElementById("area").appendChild(title); // area1(div 요소)에 title이라는 요소 노드를 연결
        console.log(title); // Hello, World!
    }
</script>
```

### 텍스트노드(TextNode)가 없는 노드 생성

```javascript
<button onclick="testAdd();">이미지 추가</button> // 버튼 클릭하면 노드 생성하여 추가
<div id="area"></div> // area div 영역에 생성
<script>
    function testAdd() {
        var imgTest = document.createElement('img'); // img 태그 생성

        // 속성 지정
        imgTest.src = "https://upload.wikimedia.org/wikipedia/commons/thumb/0/02/Berlin_Skyline_Fernsehturm_02.jpg/1600px-Berlin_Skyline_Fernsehturm_02.jpg";
        imgTest.width = "200";
        imgTest.height = "150";
        imgTest.myProperty = "123"; // 없는 속성은 줄 수 없으므로
        imgTest.setAttribute('myProperty', "123"); // 없는 속성을 주기 위해서는 setAttribute() 사용

        document.getElementById("area").appendChild(imgTest); // area div에 이미지 출력
    }
</script>
```

### 노드 삭제

```javascript
// 위 이미지 추가와 연계하여 확인
<button onclick="testDelete();">이미지 삭제</button>
<script>
    function testDelete() {
        var img = document.getElementsByTagName('img'); // 삭제할 노드 찾기
        var area = document.getElementById("area"); // 삭제할 노드의 부모 찾기

        // 찾은 부모에 대한 노드 삭제(3가지 방법)
        area.removeChild(img[0]);
        area.firstChild.remove(); // 첫번째 노드 삭제
        area.lastChild.remove(); // 마지막 노드 삭제
    }
</script>
```

### 노드의 스타일 지정

```javascript
<div id="area"></div> // 'area' div 영역에 생성
<script>
    function test() {
        var area = document.getElementById("area"); // 스타일 지정할 노드 찾기

        // 해당 노드의 스타일 지정
        area.style.backgroundColor = "orangered";
        area.style.borderRadius = "50px";
        area.style.transition = "all 2s";
    }
</script>
```

***

## 이벤트(Event)

### 고전 이벤트 모델

```
요소 객체가 갖고 있는 이벤트 속성에 이벤트 핸들러를 연결하는 방법으로,
이벤트 객체를 제거할 때는 속성값에 null을 넣어주면 된다.
```

```javascript
<button id="test1">test1() 실행확인</button>
<button id="test2">test2() 실행확인</button>
<script>
    test1.onclick = function() {
         alert("!");
    }
    test1.onclick = function() { // 하나의 이벤트밖에 연결하지 못함(alert가 포함된 이벤트는 실행불가)
        console.log("test1()이 실행되었습니다. ");
    }

    test2.onclick = function() {
        console.log("test2()이 실행되면서 test1() 이벤트 제거");
        test1.onclick = null; // test1의 이벤트 제거(test1() 실행불가)
    }
</script>
```

### 이벤트 발생 객체

```
이벤트 발생 객체는 매개변수(e, window.event)로 이벤트 정보를 전달함
핸들러 내부에서 e.target 또는 this로 이벤트가 발생된 요소 선택 가능
```

```javascript
<button id="test">실행확인</button>
<div id="area"></div>
<script>
    var test = document.getElementById("test"); // 이벤트가 발생할 var 선언
    test.onclick = function(e) {
        // e : 이벤트가 발생한 객체
        // window.event : ie8 이전 버전의 e
        var event = e || window.event;

        console.log(event.target); // <button id="test">실행확인</button>
        console.log(this); // <button id="test">실행확인</button>
    }
</script>
```

### 인라인 이벤트 모델

```
요소 내부에 이벤트를 작성하는 방식
script 태그에 정의된 함수를 호출하는 방식을 사용
(권장하지 않음 / 소스 관리의 불편함)
```

```javascript
<button onclick="test();">Execute</button> // button 요소 내부에 onclick 통해 이벤트 작성
<script>
    function test() {
        console.log("test()가 실행되었습니다.");
    }
</script>
```

### 기본 이벤트 제거

```
태그에 기본적으로 설정되어 있는 이벤트 제거
    -> 이벤트 핸들러의 return값을 false로 설정
```

* 기본 태그에 이벤트가 설정되어 있는 태그

  1. `a` : 클릭하면 다른 페이지로 이동
  2. `submit` : form 입력양식 제출 후 페이지 새로고침

* submit 기본 이벤트 제거를 통한 패스워드 - 확인 패스워드 입력값 검증 방법

```javascript

<form id="join"> // form 선언
    <label>비밀번호 : </label><input type="password" name="password" id="password"><br>
    <label>비밀번호 확인 : </label><input type="password" name="password1" id="password1">
    <input type="submit" value="제출" onclick="return test();"> // submit의 기본값은 return이므로, 잘못된 값 입력 시 false 값으로 기본 이벤트 제거
</form>
<script>
    function test(){
        var password = document.getElementById("password").value; // password 입력값
        var password1 = document.getElementById("password1").value; // password 확인 입력값

        // console log 확인
        console.log("password : " + password); 
        console.log("password1 : " + password1);

        // 비밀번호가 같은지 확인
        if(password == password1) {
            alert('비밀번호가 일치합니다.');
        } else {
            alert('비밀번호가 틀립니다.');
            document.getElementById("password1").select(); 
            return false; // submit의 기본 이벤트 제거를 위해 false 리턴
        }
    }
</script>
```

## 표준 이벤트 모델(addEventListener)

```
w3에서 공식적으로 지정한 이벤트 모델로, 한번에 여러개의 이벤트 핸들러 설정 가능
(IE는 9버전부터 지원)
```

(참고) HTML DOM 이벤트 종류 [(링크)](https://www.w3schools.com/jsref/dom_obj_event.asp)
표준 이벤트 모델 작성방법

```javascript
<button id="btn">Execute</button>
<script>
    window.onload = function() {
        var btn = document.getElementById("btn");

        btn.addEventListener('click', function(){ // addEventListener 사용
            alert('표준 이벤트 모델 테스트');
        });

        btn.addEventListener('click', function(){
            btn.style.background = 'red';
        });
    }
</script>
```

### 이벤트 전달

### 이벤트 버블링

* 자식 노드에서 부모 노드로 이벤트가 전달

```javascript
<style> // div를 겹칠 수 있도록 style 추가
    .div-test {
        border: 1px solid black;
        padding: 20px;
    }
    .div1 {
        background: red;
    }
    .div2 {
        background: orange;
    }
    .div3 {
        background: yellow;
    }
    .div4 {
        background: green;
    }
</style>

/* 이벤트 버블링 */
<div onclick="test1('1번 div');" class="div-test div1">
    <div onclick="test1('2번 div');" class="div-test div2">
        <div onclick="test1('3번 div');" class="div-test div3">
            <div onclick="test1('4번 div');" class="div-test div4"></div>
        </div>
    </div>
</div>
<script>
    // 가운데 있는 4번 div를 클릭하면 4번 div, 3번 div, 2번 div, 1번 div까지 총 4번의 alert 실행됨
    function test1(msg) {
        alert(msg);
    }
</script>

<hr>

/* 이벤트 버블링 막기 */
<div onclick="test2(event, '1번 div');" class="div-test div1">
        <div onclick="test2(event, '2번 div');" class="div-test div2">
            <div onclick="test2(event, '3번 div');" class="div-test div3">
                <div onclick="test2(event, '4번 div');" class="div-test div4"></div>
            </div>
        </div>
    </div>
<script>
    function test2(e, msg) {
        var event = e || window.event;

        alert(msg);

        // 이벤트 버블링을 막음
        // ie 제외
        event.stopPropagation();

        // ie8 전용(9 이전)
        event.cancelBubble = true;
    }
</script>
```

## 정규표현식(Regular Expression)

특정한 규칙을 가진 문자열의 집합을 표현하는 데에 사용하는 형식 언어.
정규표현식을 이용하면 입력된 문자열에 대하여 특정 조건검색, 치환 시 복잡한 조건문 대신 간단하게 처리 가능
ex) 회원가입 시 입력 유효성 확인 등

### 정규표현식의 객체 생성

* 주요 메소드

```
test() : 문자열에서 정규식 변수의 값과 일치하는 값이 있으면 true / 없으면 false
exec() : 문자열에서 정규식 변수의 값과 일치하는 값이 있으면 처음으로 매치된 문자열 반환
match() : 문자열에서 정규식 변수의 값과 일치하는 모든 값 반환
replace() : 문자열에서 정규식 변수의 값과 일치하는 부분을 새로운 값으로 변경
search() : 일치하는 부분의 시작 인덱스 반환
split() : 정규식 변수에 지정된 값을 구분자로 하여 배열 생성
```

```javascript
<script>
    function test() {
        // 정규식 변수를 선언(검색 조건으로 삼을 문자열 선언)방법 2가지
        // 1. var regExp = new RegExp('script');
        var regExp = /script/; // 정규식 리터럴 양쪽에 '/' 붙이기

        var str = 'javascript jquery ajax';

        console.log(regExp.test(str)); // true
        console.log(regExp.exec(str)); // script

        // 정규 표현식의 메소드를 직접 사용하기보다 string 메소드를 사용하는 것이 일반적
        console.log(str.match(regExp)); // script
        console.log(str.replace(regExp, '스크립트')); // java스크립트 jquery ajax
        console.log(str.search(regExp)); // 4
        console.log(str.split(regExp)); // java, jquery ajax
    }
</script>
```

* 메타 문자를 이용한 문자 검색/치환

특정 메타문자를 사용하여 문자열에 정규식이 존재하는지
`test()`를 이용해 검사하거나, `replace()`를 이용하여 치환

```javascript
<script>
    function test2() {
        var str = "javascript jquery ajax";

        var regExp = /a/; // 메타문자 없음 : 일치하는 값 의미
        // 문자열에서 정규식과 일치하는 값이 있는지 검사
        console.log("/a/ : " + regExp.test(str)); // true
        // 문자열에서 정규식과 일치하는 값들 중 첫번째 값 대체
        console.log("/a/ : " + str.replace(regExp, '(*)')); // j(*)vascript jquery ajax

        regExp = /^j/; // ^ : 시작을 의미 -> j로 시작하는
        console.log("/^j/ : " + regExp.test(str)); // true
        console.log("/^j/ : " + str.replace(regExp, '(*)')); // (*)avascript jquery ajax

        regExp = /[ab]/; // [] : [] 내의 문자 중 하나라도 존재할 경우
        console.log("/[ab]/ : " + regExp.test(str)); // true
        // a 또는 b가 문자열에 있을 경우 첫번째 값 대체
        console.log("/[ab]/ : " + str.replace(regExp, '(*)')); // j(*)vascript jquery ajax

        regExp = /^[js]/; // 시작이 j 또는 s일때
        console.log("/^[js]/ : " + str.replace(regExp, '(*)')); // (*)avascript jquery ajax

        regExp = /x$/; // $ : 끝을 의미 -> 끝이 x로 끝날 때
        console.log("/x$/ : " + str.replace(regExp, '(*)')); // javascript jquery aja(***)

        // . : 개행문자를 제외한 모든 문자
        // + : 한 글자 이상
        regExp = /^j.+x$/; // j로 시작하고 x로 끝나면 문자열 전체 대체(중간 글자수 제한x)
        console.log("/^j.+x$/ : " + str.replace(regExp, '(*)')); // (*)

        regExp = /^[0-9]+$/; // 숫자만 입력한 경우 대체
        // 시작(^)부터 1글자 이상(+) 끝까지 [0~9]일 때를 의미
        console.log("/^[0-9]+$/ : " + ("12345").replace(regExp, '(*)')); // (*)

        regExp = /^[a-zA-Z]+$/; // 영어 대/소문자만 입력한 경우 대체
        // 시작(^)부터 a-z 또는 A-Z인지 끝($)까지 검사
        console.log("/^[a-zA-Z]+$/ : " + "Javascript".replace(regExp, '(*)')); // (*)

        regExp = /^[a-zA-Z0-9]+$/; // 영어 대/소문자 + 숫자만 입력하면 대체
        // 시작(^)부터 a-z 또는 A-Z 또는 0-9인지 끝($)까지 검사
        console.log("/^[a-zA-Z0-9]+$/ : " + "Javascript123".replace(regExp, '(*)')); // (*)

        regExp = /^[ㄱ-ㅎㅏ-ㅣ가-힣]+$/; // 한글만 입력하면 대체
        console.log("/^[ㄱ-ㅎㅏ-ㅣ가-힣]+$/ : " + "안녕".replace(regExp, '(*)')); // (*)

        regExp = /^[ㄱ-ㅎㅏ-ㅣ가-힣0-9]+$/; // 한글 또는 숫자만 입력하면 대체
        console.log("/^[ㄱ-ㅎㅏ-ㅣ가-힣0-9]+$/ : " + "안녕572".replace(regExp, '(*)')); // (*)
    }
</script>
```

### 플래그 문자

* g : 전역비교를 수행
* i : 대소문자를 가리지 않고 비교
* m : 여러 줄의 검사를 수행

```javascript
<script>
    function test1() {
        var regExp = /a/ig; // a라는 문자를, 대소문자 가리지 않고 전체에 대해 해당하는 값 의미
        var str = "Javascript Jquery Ajax";

        // $& : 대체 문자열에 일치하는 전체 문자열의 복사본을 포함  
        console.log(str.replace(regExp, '($&)')); // J(a)v(a)script Jquery (A)j(a)x
    }

    function test2() {
        var regExp = /^j/gi; // j라는 문자로 시작하는 문자를 대소문자 가리지 않고 전체에서 해당하는 값
        var regExp2 = /ipt$/gim; // ipt로 끝나는 문자를 대소문자 가리지 않고 모두 찾으며, 모든 줄을 검색하는 값

        var str = "Javascript\nJquery\nAjax"; // \n으로 띄어쓰기 포함
        var str2 = "Javascript\nJquery\nAjax";

        console.log("/^j/gi : " + str.replace(regExp, "($&)")); // /^j/gi : (J)avascript \n Jquery \n Ajax

        console.log("/ipt$/gim : " + str2.replace(regExp2, "($&)")); // /ipt$/gim : Javascr(ipt) \n Jquery \n Ajax
    }
</script>
```

* 추가 메타 문자
  * \d : 숫자
  * \w : 아무 단어(숫자 포함)
  * \s : 공백 문자(탭, 띄어쓰기, 줄바꿈)
  * \D : 숫자 아님
  * \W : 아무 단어 아님
  * \S : 공백 문자 아님

* 수량 문자
  * a+ : a가 적어도 1개 이상
  * a* : a가 0개 또는 여러개
  * a? : a가 0개 또는 1개
  * a{5} : a가 5개
  * a{2,5} : a가 2~5개
  * a{2, } : a가 2개 이상
  * a{ ,2} : a가 2개 이하

```javascript
<script>
    <input type="text" id="pnoVal"></input>
    <button type="submit" onclick="test();">ValCheck</button>
    function test(){
        var regExp = /^\d{2}(0[1-9]|1[0-2])(0[1-9]|[1-2][0-9]|3[0-1])-[1234]\d{6}$/;
        // 1,2번자리(출생년도) : \d{2} : 숫자 2개가 들어가고
        // 3,4번자리(월) : (0[1-9]|1[0-2]) : 3번째 자리에 0이 들어가면 4번째는 1-9 / 1이 들어가면 4번째는 0-2
        // 5,6번자리(일) : (0[1-9]|[1-2][0-9]|3[0-1]) : 최대 31까지만 입력을 받도록
        // 7번자리 - 
        // 8번자리(남녀) : [1234] : 1,2,3,4만 받을 수 있도록
        // 9~15번자리 : \d{6}$ : 숫자 6자리가 오고 끝나도록
        var pNo = document.getElementById("pnoVal").value;

        if(regExp.test(pNo)) {
            alert('맞는 주민번호입니다.');
        } else {
            alert('틀린 주민번호입니다.');
        }
    }
</script>
```

### 유효성 검사

정규 표현식을 활용하여 입력받은 value의 유효성 검사에 활용할 수 있다.

- text로 받은 두 숫자의 합을 구하는 검사

```javascript
<input type="button" value="계산하기" onclick="execute();">
<input type="text" id="a"> +
<input type="text" id="b"> =
<span id="result"></span>
<script>
    function execute(){
        /// a와 b의 결과를 합쳐서 result에 보여주기
        var a = document.getElementById('a');
        var b = document.getElementById('b');

        var re = /^[0-9]+$/; // 정규식을 이용한 숫자 입력여부 검사
        if(!re.test(a.value)){ // 입력받은 value가 정규식을 통과하지 못할 경우
            alert('숫자만 넣으셔야 합니다.'); 
            a.value = "";
            a.focus();
            return;
        }
        var result = Number(a.value) + Number(b.value);

        if(isNaN(result)){ // 결과값이 NaN인 경우(a는 유효성 검사가 끝났으므로, b가 Number가 아닌경우)
            result = "숫자를 넣어주세요.";
        }
        document.getElementById("result").innerHTML = result;
        console.log(result); // 
</script>
```

- 회원가입 폼을 작성하여, 각각 입력되는 value에 대하여 기준을 가지고 유효성 검사

```javascript
<script>
function validate() {
            var id = document.getElementById("userid");
            var pass = document.getElementById("pass");
            var pass1 = document.getElementById("pass1");
            var name = document.getElementById("name");
            var email = document.getElementById("email");
            var tel1 = document.getElementById("tel1");
            var tel2 = document.getElementById("tel2");
            var tel3 = document.getElementById("tel3");

        // 아이디 검사
        // 첫글자는 영문 소문자로 시작, 숫자가 반드시 하나 이상 포함된(영문 소문자와 숫자로만 이루어짐) 4~12자 사이
        if(!chk(/^[a-z][a-z\d]{3,11}$/, id, "첫글자는 영문 소문자, 4~12자 사이로 입력"))    
            return false;
        if(!chk(/[0-9]/, id, "숫자 하나 이상 포함"))
            return false;

        // 비밀번호 유효성 검사
        // 대소문자 하나 이상씩, 숫자도 하나 이상, 특수문자 하나 이상 길이 8 이상
        if(!chk(/(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[^a-zA-Z0-9가-힣]).{8,}/, pass, "영문 대소문자, 숫자, 특수문자 1개 이상 포함"))
            return false;

        // 비밀번호 확인 일치여부
        if(pass.value != pass1.value) {
            alert("비밀번호 확인내용이 같지 않습니다.");
            return false;
        } 

        // 이름 검사
        // 2글자 이상, 한글만
        if(!chk(/^[가-힣]{2,}$/, name, "한글로 2글자 이상 입력해주세요"))
            return false;

        // 이메일 검사
        // 4글자 이상 @ 1글자 이상 . 글자1~3글자

        if(!chk(/^[\w]{4,}@[\w]+\.[\w]+{1,3}$/, email, "이메일을 알맞게 입력해주세요"))
            return false;

        // 전화번호 검사(휴대폰 번호)
        // 앞자리 3자리(휴대폰에서 가능한 앞자리)
        // 두번째 자리 3-4자리
        // 마지막 자리 4자리

        if(!chk(/^01[016789]$/, tel1, "전화번호를 다시 입력하세요."))
            return false;

        if(!chk(/^[1-9]\d{2,}$/, tel2, "전화번호를 다시 입력하세요."))
            return false;

        if(!chk(/^\d{4}$/, tel3, "전화번호를 다시 입력하세요."))
            return false;

        }
        // 입력받은 값을 확인하는 function으로,
        // 유효성 검사에 통과하지 못한 경우 위 if절에서 입력한 문구를 alert 형태로 출력하며,
        // 동시에 form 태그의 submit을 막도록 함
        function chk(re, e, msg) { 
            if(re.test(e.value)) {
                return true;
            } 
            alert(msg);
            e.value = "";
            e.focus();
            return false;
        }
</script>
```