# Javascript

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