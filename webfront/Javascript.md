# Javascript

- ## **[개요](#개요)**

- ## **[데이터 입출력(IO)](##데이터-입출력(io))**

- ## **[배열(Array)](##배열)**

- ## **[함수(Function)](##-함수(function))**

  - [작성방법](##-작성방법)
  - [함수의 매개변수](##-함수의-매개변수(전달인자))

- ## **[객체(Object)](##-객체)**

  - [객체 선언 및 호출](###-객체-선언-및-호출)

- ## **[내장객체](##-내장-객체)**

- ## **[BOM(Browser Object Model)](##-BOM(Browser-Object-Model))**

- ## **[정규표현식(Regular Expression)](##-정규표현식(Regular-Expression))**

***

## 개요

### 스크립트 언어란?

기본 프로그램의 동작을 사용자의 요구에 맞게 수행되도록 해주는 용도로 사용.
매우 빠르게 배우고 짧은 소스코드 파일로 상호작용하도록 고안됨

그 중, *자바스크립트(Javascript)*는 웹 브라우저에서 많이 사용하는 인터프리터 방식의 객체지향 프로그래밍 언어로, ECMA 스크립트 표준을 따르는 대표적인 웹 기술이다.

### 자바스크립트 작성 방법

소스는 함수 단위로 작성하고, 이벤트 속성을 사용해서 구동되게 한다.
이벤트 속성은 태그마다 차이 있음.
`on이벤트명="실행할 함수명([전달값])"`

#### 인라인 방식(inline)

태그에 직접 간단소스코드를 작성해서 실행되게 하는 방법

```javascript
<button onclick="window.alert('경고창 Open!');">경고창 띄우기</button>
<button onclick="console.log('Console.log 출력!');">console 창에 출력</button>
<h4 onmouseover="this.style.backgroundColor='red'">마우스 오버</h4>
```

#### 내부실행 방식(internal)

script 태그 영역에 작성하여 실행하는 방법으로, *head태그, body태그*에 작성 가능

```javascript
<button onclick="testfn();">실행 확인버튼</button>
<script type="text/javascript"> // type="text/javascript" : 기본값
    // 자바스크립트 주석 타입 : "//"
    // 함수 작성시에는 함수명 앞에 반환자료형(return type)
    // -> 자바스크립트는 자료형이 없음
    function testfn(){
        alert('testfn() 실행 확인'); // 알림 팝업창 실행됨
    }
</script>
```

#### 외부실행 방식(external)

별도의 js파일로 작성해서 가져다 사용하는 방법

```javascript
<head>
...
<script src="js/sample.js"></script> // 헤드 영역에 해당되는 js파일 링크
</head>
```

## 데이터 입출력(IO)

### 출력(Output)

#### `document.write()` : HTML에 해당 내용으로 모두 반영됨

```javascript
<script type="text/javascript">
    // body 부분에 작성된 script 태그의 내용이
    // function으로 감싸져 있지 않으면 html 로딩과정에서 실행됨.
    document.write("document.write() 로 출력한 내용");
    alert("출력 문구를 실행하였습니다.");
</script>
// -> 별도의 function으로 감싸져 있지 않으므로 HTML 열면 바로 실행됨
<br>

<button onclick="writefn();">출력</button> // 버튼 클릭 시 document.write 내 내용으로 모두 변경
<script>
    function writefn(){ 
        document.write("HTML문서가 완전히 로드된 후 호출 시 " + "기존 HTML 내용을 모두 삭제");
    }
</script>
```

#### `innerHTML` 활용한 요소의 내용 변경

Javascript에서 Tag Element의 값을 읽거나, 변경할 때 innerHTML 속성 사용

```javascript
<div id="area1">Hello, World!</div> 
<button onclick="checkValue();">innerHTML 확인</button>
<script>
    function checkValue() {
        var divEl = document.getElementById("area1"); // 아이디를 기용하여 요소 선택 후 값 읽어오기

        alert(divEl.innerHTML); // 읽어온 요소값 경고창으로 출력('Hello, World!')

        divEl.innerHTML = "innerHTML 속성으로 값 변경";
    }
</script>
```

#### `console.log()` : 개발자 도구 Console화면에 출력

개발자 도구 콘솔화면에 출력할 때 사용하며, 내부적으로 정상적으로 구현하는지 확인하는 디버깅 등에 사용됨
(HTML 화면에 나오는 것이 아님!)

```javascript
<script>
    function printConsole(){
        console.log('콘솔 화면에 출력하기'); // 개발자 도구의 console에 해당 내용 확인가능
    }
</script>
```

### 입력(Input)

#### `window.confirm()` : 질문에 대한 예/아니오 결과를 얻을 때 사용(확인:true / 취소:false)

```javascript
<script>
    function checkHungry(){
        var result = confirm("If you feel Hungry, click OK or if not, click cancel");
        // 콘솔에서 리턴 값 확인
        console.log(result); // true or false

        var str = ""; // 문자열을 저장할 비어있는 변수 선언
        if(result){
            str = "Yes, I'm hungry";
        }else{
            str = "No, I'm OK!";
        } 
        console.log(str); // 입력받은 값을 if문을 통해 변수로 받을 수도 있다. 
    }
</script>
```

#### `window.prompt()` : 텍스트 필드와 확인/취소 버튼이 있는 대화상자를 출력하고, 입력한 메시지 내용을 리턴값 반환

```javascript
<script>
    function testPrompt() {
        var result = window.prompt("What's your name?"); // 프롬프트창에 입력한 값을 result로 받음
        console.log("Oh, you're " + result + "!"); // Oh, you're + 입력한 값 + !
    }
</script>
```

### HTML 태그 접근

#### 1. 아이디로 접근 `getElementById("id")`

```javascript
<div id="area1" class="area"></div>
<div id="area2" class="area"></div>
<script>
    function accessId() {
        var area1 = document.getElementById("area1"); // id="area1" 인 div 영역 변수 담기
        area1.style.backgroundColor = "yellow"; // id 영역 Style 변경
    }
    function accessId2() { // accessId2() 실행시마다 backgroundColor 변경 yellow <-> red
        var bgColor = area2.style.backgroundColor;

        if(bgColor == "red") {
            area2.style.backgroundColor = "yellow";
        }else{
            area2.style.backgroundColor = "red";
        }
    }
</script>
```

#### 2. 태그명으로 접근 `getElementsByTagName("태그명")`

```javascript
<ul>
    <li>list1</li>
    <li>list2</li>
    <li>list3</li>
    <li>list4</li>
    <li>list5</li>
</ul>
<button onclick="accessTagName();">태그명으로 접근</button>
<script>
    function accessTagName() {
        var list = document.getElementsByTagName("li"); // 문서 내의 모든 li 태그들의 정보들을 읽어와 배열 형식으로 저장
        console.log("전달받은 li 태그의 갯수 : " + list.length) // 5
        
        // 배경값을 rgb로 지정하며, b값을 50씩 변경하며 목록 list에 그라데이션 효과를 반영하기
        var changeColor = 50;
        for(var i = 0; i < list.length; i++) { 
            console.log(list[i]);
            list[i].style.backgroundColor = "rgb(130,220," + changeColor + ")";
            changeColor += 50;
        }
    }
</script>
```

#### name으로 접근 `getElementsByName("name")`

```javascript
// checkbox type의 form 작성(name='hobby')
<form>
    <fieldset>
        <legend>hobby</legend>
        <table>
            <tr>
                <td><input type="checkbox" name="hobby" value="game" id="game"><label for="game">Playing game</label></td>
                <td><input type="checkbox" name="hobby" value="music" id="music"><label for="music">Listen to Music</label></td>
                <td><input type="checkbox" name="hobby" value="movie" id="movie"><label for="movie">Watching Movies</label></td>
            </tr>
            <tr>
                <td><input type="checkbox" name="hobby" value="book" id="book"><label for="book">Reading books</label></td>
                <td><input type="checkbox" name="hobby" value="travel" id="travel"><label for="travel">Travel</label></td>
                <td><input type="checkbox" name="hobby" value="exercise" id="exercise"><label for="exercise">Exercise</label></td>
            </tr>
        </table>
    </fieldset>
</form>
<div id="area" class="area"></div>
<button onclick="accessName();">name으로 접근</button>
<script>
    function accessName() {
        var hobby = document.getElementsByName("hobby"); // 'hobby' name을 hobby 변수에 담음

        console.log("hobby의 길이 : " + hobby.length); // 6(모든 name='hobby'인 변수가 배열로 담김)

        // checkbox의 checked여부를 확인해서 checkItem에 담기 가능
        var checkItem = "";
        for(var i in hobby) { // aree
            if(hobby[i].checked == true) {
                checkItem += hobby[i].value + "selected <br>";
            }
        }
        console.log(checkItem); // 체크가 되어있는 hobby 값들에 대해 '... selected' 형태로 확인
    }
</script>
```

#### input type = "text"의 값 읽어오기(`value` 사용)

```javascript
<form>
    name : <input type="text" name="username" id="username">
    <br>
    <input type="button" onclick="readValue();" value="Check inputValue">
</form>
<script>
    function readValue(){
        var input = document.getElementById("username");
        if(input.value == "" || input.value.length == 0){ // 입력이 안된 경우
            alert("이름을 입력하세요");
            input.focus();
        }else{
            console.log(username.value); // 입력된 text를 가져오고 싶을 경우 '.value' 사용
        }
    }
</script>
```

### 변수 & 자료형

#### 전역변수와 지역변수

```javascript
<script>
    // 전역 변수의 선언
    str = '전역변수'; // 자동으로 window 객체의 필드가 됨

    // 함수 외부에 선언한 변수는 var를 붙여도 전역 변수
    var str2 = '전역변수';

    window.onload = function(){  // window.onload : 페이지가 로드 된 직후 실행하는 함수를 지정
        var str = '지역변수';  // 지역 변수 선언
        // -> 지역 변수 앞에는 var를 붙인다.

        var str3 = '새로운 지역변수';

        str4 = "새로운 전역변수";

        // 전역 변수를 호출할 때 this. 혹은 window.을 붙일 수 있다.
        console.log("str 호출");
        console.log(str); // 지역변수
        console.log(this.str); // 전역변수
        console.log(window.str); // 전역변수

        console.log("str2 호출");
        console.log(str2); // 전역변수
        console.log(this.str2); // 전역변수
        console.log(window.str2); // 전역변수

        // 지역변수에 this. 혹은 window.을 사용하지 못한다.
        console.log("str3 호출");
        console.log(str3); // 새로운 지역변수
        console.log(this.str3); // undefined
        console.log(window.str3); // undifined

        console.log("str4 호출");
        console.log(str4); // 새로운 전역변수
        console.log(this.str4); // 새로운 전역변수
        console.log(window.str4); // 새로운 전역변수

        // 함수 안에 작성되어도 var를 사용하지 않으면 전역 변수가 된다.
        showStr4();

    }

    function showStr4(){
        console.log("str4 전역변수 확인");
        console.log(str4); // 새로운 전역변수
        console.log(this.str4); // 새로운 전역변수
        console.log(window.str4); // 새로운 전역변수
    }
</script>
```

#### `window` 객체

웹 브라우저에서 제공하는 창(window) 자체를 나타내는 객체

```
<script>
    변수명; // 전역 변수(global)

    var 변수명; // 전역 변수(global)

    function 함수명(){
        변수명; // 전역 변수(global)

        var 변수명; // 지역 변수(local)
    }
</script>
```

#### 전역변수명과 지역변수명이 같을 때

함수 내부에서 변수명을 호출하면 **지역변수가 우선권**을 가짐.
전역 변수 사용 시 `this.변수명` 또는 `window.변수명`으로 사용하여 지역 변수와 구분.

#### 자료형

Javascript는 변수의 자료형을 별도로 지정하지 않음
> -> 변수에 저장되는 값(리터럴)에 의해 자료형이 결정됨.

```javascript
// javascript의 자료형
<ul>
    <li>String(문자열)</li>
    <li>Number(숫자열)</li>
    <li>Boolean(논리값)</li>
    <li>Object(객체)</li>
    <li>Function(함수)</li>
    <li>Undefined(초기값이 없는 변수)</li>
</ul>

<button onclick="typeTest();">자료형 테스트</button>
<br>
<script type="text/javascript">
    function typeTest(){
        // // typeof : 값의 자료형을 확인하는 연산자 를 통해 해당 변수의 타입 확인가능
        var name = '홍길동'; // String
        var age = 20; // Number
        var check = true; // Boolean
        var hobby = ['영화', '음악','낮잠']; // Object
        var user = { // Function
                        name : "홍길동",
                        age : 20,
                        id : 'user1'
                    }
        var testFuntion = function testFuntion(num1, num2){ // function
                                var sum = num1 + num2;
                                alert(sum);
                            };
        var noVal; // undefined

        // undefined와 null의 차이점
        // - undefined : 변수 생성 시 초기값이 없는 상태
        // - null : 의도적으로 변수가 참조하고 있는 값이 없다는 걸 알리는 상태
    }
</script>
```

### 문자열 / 숫자

#### 문자열(String)

" " 또는 ' ' 로 묶어 있는 리터럴. String이라는 자바스크립트 내장객체가 존재하며, 문자열과 관련된 기본적인 메소드(함수)를 제공함

* 문자열 관련 메소드

```javascript
<script>
function stringMethod() {
    var str = "Hello World";

    console.log(str.toUpperCase()); // HELLO WORLD
    console.log(str.toLowerCase()); // hello world
    console.log(str.length()); // 11
    console.log(str.indexOf("l")); // 2 (맨 처음 나온 l의 위치)
    console.log(str.lastIndexOf("l")); // 9 (맨 뒤에 나온 l의 위치) 
    for(var i = 0; i < str.length; i++) {
        console.log(i + "번째 인덱스 " : str.charAt(i)); // 0번째 인덱스 : H,,,,, 
    }
    console.log(str.substring(6, str.length)); // World

    var strForSplit = "Java, Jquery, React";
    var lang = strForSplit(", "); // ", " 기준으로 자르기
    console.log(lang); // length 3의 배열
}
</script>
```

#### 숫자(Number)

정수, 부동소수점, Infinity, NaN 리터럴.
Math라는 자바스크립트 내장 객체가 존재하며, 수학과 관련된 기본적인 메소드를 제공

* 숫자 처리 메소드

```
<script>
function showMathMethod(){
    var num = -123;

    console.log(Math.abs(num)); // 123
    console.log(Math.random()); // 0~1 사이의 임의의 랜덤값 발생
    console.log(Math.round(572.572)); // 573 --> 반올림
    console.log(Math.floor(572.572)); // 572 --> 내림
    console.log(Math.ceil(572.572)); // 573 --> 올림
    }
</script>
```

### 데이터 형변환

#### 문자열(String)과 숫자(Number)의 '+' 연산

> 문자열 + 숫자 = 문자열
> 숫자 + 숫자 + 문자열 = 숫자가 먼저 계산되고 뒤의 문자열과 합쳐짐

```javascript
<script>
    function testPlus() {
        console.log(7 + 7); // 14
        console.log(7 + "7"); // 77
        console.log("7" + 7); // 77
        console.log("7" + "7"); // 77
        console.log(7 + 7 + "7"); // 147
        console.log(7 + "7" + 7); // 777
        console.log("7" + 7 + 7); // 777
        console.log("7" + (7 + 7)); // 714
    }
</script>
```

#### 강제 형변환

자바스크립트에서는 문자열 -> 숫자형 변환 시 
`Number()` 내장객체 또는 `parseInt()`, `parseFloat()` 내장함수를 이용하여 강제형변환

```javascript
<script>
    function castingTest() {
        var iNum = 2;
        var sNum = "3"; // String
        var fNum = "1.234"; // String

        console.log(iNum + sNum); // 23 
        consolg.log(iNum + Number(sNum)); // 5
        consolg.log(iNum + parseInt(sNum)); // 5
        consolg.log(iNum + parseFloat(sNum)); // 5

        consolg.log(iNum + fNum); // 21.234
        consolg.log(iNum + Number(fNum)); // 3.234
        consolg.log(iNum + parseInt(fNum)); // 3
        consolg.log(iNum + parseFloat(fNum)); // 3.234
    }
</script>
```

### 연산자

- 동등 연산자(==, !=)
자료형에 **상관없이** 값이 일치하면 true, 아니면 false

- 일치 연산자(===, !==)
자료형과 값이 **모두** 일치하면 true, 아니면 false

```javascript

<script>
    function opTest1() {
        var num = 1;
        var str1 = "1";
        var boolT = true;
        var strT = 'true';

        var num0 = 0;
        var str0 = "0";
        var str = "";

        var nullVal = null;
        var unDef = undefined;

        // 동등 연산자 테스트
        console.log('1 == 1 : ' + (num == 1)); // true
        console.log('1 == "1" : ' + (num == str1)); // true
        console.log('1 == true : ' + (num == boolT)); // true(Boolean true의 값 = 1)
        console.log('1 == "true" : ' + (num == strT)); // false

        console.log('0 == "0" : ' + (num0 == str0)); // true
        console.log('0 == "" : ' + (num0 == str)); // true
        console.log('"0" == "" : ' + (str0 == str)); // false
        console.log('null == undefined : ' + (nullVal == unDef)); // true 

        // 일치 연산자 테스트
        console.log('1 === 1 : ' + (num === 1)); // true
        console.log('1 === "1" : ' + (num === str1)); // false
        console.log('1 === true : ' + (num === boolT)); // false
        console.log('1 === "true" : ' + (num === strT)); // false

        console.log('0 === "0" : ' + (num0 === str0)); // false
        console.log('0 === "" : ' + (num0 === str)); // false
        console.log('"0" === "" : ' + (str0 === str)); // false

        console.log('null === undefined : ' + (nullVal === unDef)); // false
    }
</script>
```

## 배열

### Javascript에서 배열이란?

자바스크립트에서는 별도의 자료형 지정이 없기 때문에 모든 자료형을 보관하는 변수의 모음을 배열로 처리함
`Java의 Collection`과 유사하다.

```javascript
<script>
    // 기본 배열 정의
    function arrayTest1(){
        var arr1 = ['홍길동', 20, true, [1, 2, 3, 4]]; // 배열 정의
        console.log(arr1); // Array(4) 형태의 배열
    }
</script>
```

### 배열의 선언

배열 선언 시 배열의 크기를 정하거나, 정하지 않고 선언할 수 있다.

```javascript
<script>
    function arrayTest2(){
        var arr1 = new Array(); // 크기를 지정하지 않은 선언
        var arr2 = new Array(3);

        console.log(arr1);
        console.log(arr2);

        // 배열에 값 대입
        arr1[0] = 'a';
        arr1[1] = 'b';
        arr1[2] = 'c';
        arr1[3] = 'd';
        console.log(arr1); // length: 4의 배열

        arr2[0] = "ㄱ";
        arr2[1] = "ㄴ";
        arr2[2] = "ㄷ";
        arr2[3] = "ㄹ";

        console.log(arr2); // length: 4의 배열 --> 선언한 크기보다 더 들어오면 그에 따라 크기 늘림

        // new 연산자를 활용한 초기화
        var arr3 = new Array('a', 'b', 'c');
        console.log(arr3); // length: 3의 배열

        var arr4 = ['java', 'oracle', 'html5', 'css', 'javascript'];
        console.log(arr4); // length: 5의 배열
    }
</script>
```

### 배열 객체의 메소드

배열도 하나의 객체이기 때문에 배열에서 활용할 수 있는 메소드가 있음
    
- `indexOf()` : 배열에서 요소가 위치한 인덱스를 리턴

```javascript
<script>
    function methodTest1() {
        var arr1 = ['사과', '딸기', '바나나', '복숭아', '키위', '파인애플', '토마토'];
        console.log(arr1.indexOf('바나나')); // 2
    }
</script>
```

- `concat(배열명)` : 두개 또는 세개의 배열을 결합

```javascript
<script>
    function methodTest2() {
        var arr1 = ['5', '7', '2'];
        var arr2 = ['4', '8', '6'];
        var arr3 = arr1.concat(arr2); console.log(arr3); // 5,7,2,4,8,6 --> arr1을 기준으로 arr2 합침
        console.log(arr2.concat(arr1)); // 4,8,6,5,7,2 --> arr2를 기준으로 arr1 합침
        var arr4 = arr2.concat(arr1, arr3); console.log(arr4); // 4,8,5,5,7,2,5,7,2,4,8,6 --> 전달인자가 하나더 있어도 됨
    }
</script>
```

- `toString()`, `join()` : 배열을 결합하여 문자열로 변환
`toString()`은 배열을 문자열로 합칠 때 요소 사이에 `,`(콤마)를 추가하여 합침
`join()`도 기본적으로 `toString()`과 같지만 매개변수로 구분자를 지정할 수 있음

```javascript
<script>
    function methodTest3() {
        var arr1 = ['bomin', 'eder', 'mota', 'minhyun'];
        var arr1toString = arr1.toString();
        var arr1Join = arr1.join("/");

        console.log("arr1 : " + arr1); // bomin,eder,mota,minhyun
        console.log("arr1의 자료형 : " + typeof(arr1)); // object
        console.log("arr1toString : " + arr1toString); // bomin,eder,mota,minhyun
        console.log("arr1toString의 자료형 : " + typeof(arr1toString)); // string
        console.log("arr1Join : " + arr1Join); // bomin/eder/mota/minhyun
        console.log("arr1Join의 자료형 : " + typeof(arr1Join)); // string
    }
</script>
```

- `sort()` : 배열을 오름차순으로 정렬
`reverse()` : 배열의 순서를 뒤집음

> `sort(), reverse()` 수행 시 원본 데이터의 순서 자체가 변함

```javascript
<script>
    function methodTest4() {
        var arr = new Array();

        for(var i = 0; i < 10; i++){ // 배열에 10개의 랜덤값(0 ~ 100 생성)
            arr[i] = Math.round(Math.random() * 100);
        }

        console.log("arr의 값 : " + arr);

        // 오름차순 정렬
        // 정렬 후 정렬 순서를 유지함
        console.log("arr.sort() 후 값 : " + arr.sort(function(left, right){
            return left - right;
        }));

        // 내림차순 정렬
        console.log("내림차순 정렬 : " + arr.sort(function(left, right) {
            return right - left;
        }));
        // reverse()를 이용한 내림차순 정렬
        console.log("내림차순 정렬 : " + arr.sort().reverse());
    }
</script>
```

- `push()` : 배열의 맨 뒤에 요소 추가
`pop()` : 배열의 맨 뒤 요소 제거

```javascript
<script>
    function methodTest5() {
        var arr = ['suwon', 'seongnam', 'incheon'];
        console.log(arr); // suwon, seongnam, incheon

        arr.push('hwaseong');
        console.log(arr); // suwon, seongnam, incheon, hwaseong

        arr.push('paju');
        console.log(arr); // suwon, seongnam, incheon, hwaseong, paju

        arr.sort();
        console.log(arr); // hwaseong, incheon, paju, seongnam, suwon

        console.log("arr에서 pop한 값 : " + arr.pop()); // suwon
        console.log(arr); // hwaseong, incheon, paju, seongnam

        console.log("arr에서 pop한 값 : " + arr.pop()); // seongnam
        console.log(arr); // hwaseong, incheon, paju
    }
</script>
```

- `shift()` : 배열의 맨 앞에 요소 제거
`unshift()` : 배열의 맨 앞에 요소 추가

```javascript
<script>
    function methodTest6() {
        var arr = ['suwon', 'seongnam', 'incheon'];
        console.log(arr); // suwon, seongnam, incheon

        arr.unshift('hwaseong');
        console.log(arr); // hwaseong, suwon, seongnam, incheon

        arr.unshift('paju');
        console.log(arr); // paju, hwaseong, suwon, seongnam, incheon

        arr.sort();
        console.log(arr); // hwaseong, incheon, paju, seongnam, suwon

        console.log("arr에서 shift한 값 : " + arr.shift()); // hwaseong
        console.log(arr); // incheon, paju, seongnam, suwon
    }
</script>
```

- `slice()` : 배열의 요소 선택 잘라내기
`splice()` : 배열의 index 위치의 요소 제거 및 추가

```javascript
<script>
    function methodTest7() {
        var arr = ['berlin', 'rio', 'galway', 'london'];
        console.log(arr); // berlin, rio, galway, london

        // slice(시작인덱스, 종료인덱스);
        // 원본 배열에 영향 끼치지 않음
        console.log("slice(2, 4) : " + arr.slice(2, 4)); // galway, london
        console.log(arr); // berlin, rio, galway, london

        // splice([index], 제거수, 추가값);
        // 원본 배열에 영향을 미침
        // 제거 완료 후 값이 추가 됨
        console.log("splice(2, 1, 'jsp') : " + arr.splice(2, 1, 'atacama')); // galway
        console.log(arr); // berlin, rio, atacama, london
    }
</script>
```

## 함수(Function)

### 작성방법

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

### 함수의 매개변수(전달인자)

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

### 함수의 return 처리

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

### 가변인자 함수 테스트

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