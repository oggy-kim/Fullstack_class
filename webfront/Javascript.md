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