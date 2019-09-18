# jQuery

## jQuery 개요

### jQuery의 정의

기존 복잡했던 클라이언트 측 HTML 스크립팅을 간소화 하기 위해 고안된 Javascript 라이브러리로,
적은 양의 코드로 빠르고, 풍부한 기능을 제공함.

  ※ library : 프로그램 개발 시 필요한 기능
  
  ※ framework : 프로그램을 만들 때 사용하는 틀, 뼈대

### jQuery 연결 방법

```
- head 태그 내부에 script 태그 선언
<script type="text/javascript" src="js파일 경로.js"></script>

오프라인/ 온라인 상태에 따라 파일 경로 지정

- jQuery 공식 사이트 : https://jquery.com/
- jQuery 라이브러리 제공 페이지 : https://code.jquery.com/

    1. jQuery 라이브러리 다운로드를 통한 연결
        - js 파일을 다운로드하여 파일 경로 지정

    2. CDN(Content Delivery Network)을 통한 연결
        - 제공하는 주소를 이용하여 파일 경로 지정
```

### jQuery 시작하기

* jQuery 시작하기
  * jQuery의 명령은 문서가 로드된 후에 실행되어야 함
    javascript의 `window.onload = function(){}` 과 같지만
    **onload 이벤트는 1회만 가능하고, jQuery는 제한없음**

* jQuery에서 onload를 의미하는 함수는 3가지 방법이 존재
  1. `jQuery(document).ready(function(){});`
        ($ == jQuery를 의미)
  2. `$(document).ready(function(){});` // <-- 가장 일반적으로 쓰임
  3. `$(function(){});`

* jQuery 기본형태
    `$('선택자').메소드명('속성','속성값');`

## 기본 선택자

### 전체 선택자 : (*)

```javascript
$(document).ready(function(){
    $("*").css("color","red"); // css() 메소드 : 스타일과 관련된 기능 수행
});
```

### 태그 선택자

* `$("태그이름")`

```javascript
<script>
    //  한종류의 태그를 선택하고 싶을 경우
    $(document).ready(function(){
        $("h5").css("color", "blue");
    });

    $(document).ready(function() {
        $("p").css("color", "red");
    });

    // 여러 종류의 태그 선택자를 동시에 사용하고 싶은 경우
    $(document).ready(function(){
        $("h5, p").css("backgroundColor", "yellow");
    });
</script>
```

### 클래스 선택자

* 특정한 클래스 속성을 가진 문서 객체를 선택하는 선택자`$(".클래스이름")`

```javascript
<script>
    jQuery(document).ready(function(){
        $(".item").css("color", "orange");
    });
    $(document).ready(function(){
        $(".item.select").css("backgroundColor", "yellow");
    });
</script>
```

### 아이디 선택자

* 특정한 아이디 속성을 가진 객체를 선택하는 선택자`$("#아이디이름")`

```javascript
<script>
    jQuery(document).ready(function() {
        $("#id1").css("color", "brown");
    });

    $(document).ready(function() {
        $("#id2").css("color", "pink");
    })
</script>
```

### 자식 선택자 / 후손 선택자

* 기본 선택자의 앞에 붙여 사용하며, 기본 선택자의 범위를 제한

```javascript
<script>
    $(document).ready(function(){
        $("div > h3").css("color", "violet"); // 자식 선택자 : '부모 > 자식'
        $("ul > .ch").css("backgroundColor", "red");
    });
    $(document).ready(function(){
        $("div h3").css("backgroundColor", "lightblue"); // 후손 선택자 : '부모 자식'
    });
</script>
```

### 속성 선택자

* 기본 선택자 뒤에 붙여 사용

```
요소[속성] : 특정 속성을 가지고 있는 객체 선택
요소[속성 = 값] : 속성 안의 값이 특정값과 같은 객체 선택
요소[속성 ~= 값] : 속성 안의 값이 특정값을 단어로써 포함하는 객체 선택
요소[속성 ^= 값] : 속성 안의 값이 특정값으로 시작하는 객체 선택
요소[속성 $= 값] : 속성 안의 값이 특정값으로 끝나는 객체 선택
요소[속성 *= 값] : 속성 안의 값이 특정값을 포함하는 객체 선택
```

```javascript
<input type="text">
<input type="number" class="test test1">
<input type="radio">
<input type="checkbox">
<input type="button" class="test2" value="button">
<script>
    $(document).ready(function(){
        // val() : value와 관련된 기능 수행
        // attr() : 속성과 관련된 기능 수행
        $("input[type = text]").val("change value");
        $("input[class ~= test]").val("123456");
        $("input[type ^= ra]").attr("checked", true);
        $("input[type $= box]").attr("checked", true);
        // $("input[class *= st2").css("width", "100px").css("height", "100px");
        $("input[class *= st2").css({"width":"100px", "height":"100px"});
    });
</script>
```

### 입력양식 필터 선택자

* input 태그의 type 속성에 따른 문서 객체 선택

```javascript
<script>
    $(document).ready(function() {
        $("input:text").css("background", "red"); 
        $("input:button").attr("value", "버튼").css({"width":"200px", "height":"200px"})
        $("input:checkbox").attr("checked", true).css({"width":"50px", "height":"50px"})
        $("input:file").css("background", "yellowgreen");
        $("input:image").mouseenter(function(){ // mouseenter() : 마우스가 요소 경계 내부로 들어 왔을 때 이벤트 발생
            $(this).attr("src", "https://berlinsbi.com/media/1077/studing-in-berlin-400-x-300-copy.jpg");
        });
        $("input:image").mouseleave(function(){
            $(this).attr("src", "https://res.cloudinary.com/prestige-property-group/image/upload/w_400,h_300/PropertyImages/209835.jpg");
        });
        $("input:password").css("background", "yellow");
        $("input:radio").attr("checked", true);
        $("input:reset").css({"background":"blue", "color":"white"});
        $("input:submit").css({"background":"purple", "color":"white"});
    });
</script>
```

* checkbox의 상태에 대한 선택자

```javascript
<label>취미 : </label>
<input type="checkbox" name="hobby" value="game" id="game">
<label for="game">게임</label> 
<input type="checkbox" name="hobby" value="movie" id="movie">
<label for="movie">영화</label> 
<input type="checkbox" name="hobby" value="music" id="music">
<label for="music">음악</label>

<script>
    // input 태그 중 checkbox의 값에 변화가 있을 경우 function checkedChange() 실행
    $("input:checkbox").change(checkedChange);

    function checkedChange(){
        console.log($(this).prop("checked")); // prop() : 선택한 요소의 속성 값을 반환하거나 설정

        if($(this).prop("checked")){ // 선택한 요소의 값이 'checked'일 경우
            $(this).css({"width":"50px","height":"50px"});
        }else{
            $(this).css({"width":"10px","height":"10px"});
        }
    }
</script>
```

* select > option 태그의 상태에 대한 선택자

```javascript
<select id="national">
    <option value="한국" selected>한국</option>
    <option value="미국">미국</option>
    <option value="일본">일본</option>
    <option value="중국">중국</option>
</select>

<label>Selected : </label><input type="text" id="result">

<script>
    $(selectChange); // 초기 select 값 출력

    $("#national").change(selectChange); // national option이 변경하면 그에 대한 function 실행

    function selectChange(){
        var value = $("option:selected").val(); // select 태그의 option 태그 중 선택 된 객체 선택

        console.log(value);
        $("#result").val(value);
    }
</script>
```

* input 상태에 대한 선택자

```javascript
<label>활성화 텍스트상자 : </label><input type="text"><br>
<label>비 활성화 텍스트상자 : </label><input type="text" disabled><br>
<label>활성화 버튼 : </label><input type="button" value="활성화"><br>
<label>비 활성화 버튼 : </label><input type="button" value="비활성화" disabled><br>

<script>
    $("input:enabled").css("background", "yellow");
    $("input:disabled").css("background", "red");
</script>
```

* 순서에 따른 필터 선택자

```javascript
<table border="1">
    <tr><th>name</th><th>blood type</th><th>region</th></tr>
    <tr><td>bomin</td><td>B</td><td>seoul</td></tr>
    <tr><td>eder</td><td>A</td><td>incheon</td></tr>
    <tr><td>hyunsung</td><td>O</td><td>hwaseong</td></tr>
    <tr><td>minhyun</td><td>AB</td><td>yongin</td></tr>
    <tr><td>mathias</td><td>O</td><td>gwangju</td></tr>
    <tr><td colspan="2">total</td><td>5</td></tr>
</table>
<script>
    // 요소:odd -> 홀수번째 인덱스 객체 선택
    // 요소:even -> 짝수번째 인덱스 객체 선택
    // 요소:first -> 첫번째 위치한 객체 선택
    // 요소:last -> 마지막에 위치한 객체 선택

    $(document).ready(function(){
        $("tr:first").css("backgroundColor", "black").css("color","white"); // 첫번째 tr
        $("tr:last").css("backgroundColor", "red").css("color", "white"); // 마지막 tr
        $("tr:odd").css("backgroundColor", "yellow"); // 홀수번째 tr
        $("tr:even").css("backgroundColor", "lightgray"); // 짝수번째 tr
    });
</script>
```

## 필터링 메소드

선택자로 지정한 객체(요소)를 기준으로 객체 그룹에서 위치를 가지고 객체를 선택하는 메소드

### 필터링 메소드 사용법

* 필터 메소드를 사용해 문서 객체를 선택할 수 있음

```javascript
// 테스트할 html 태그
<h3 class="test">1</h3>
<h3 class="test">2</h3>
<h3 class="test">3</h3>
<h3 class="test">4</h3>
<h3>5</h4>
<h3 class="test">6</h3>

<script>
    $(document).ready(function(){
        $("h3:odd").css("background", "black").css("color", "white"); // 2, 4, 6

        // filter() 메소드 사용
        // filter() 메소드는 특정 기준과 일치하는 요소 반환

        // test 클래스 요소 중 짝수 인덱스의 css 변경
        $(".test").filter(":even").css({"background":"tomato", "color":"white"}); // 1, 3, 6

        // 함수를 매개변수로 하는 filter() 메소드 사용
        // 매개변수로 index 작성 시 필터링 되기 전의 인덱스 값을 전달 받는다
        $(".test").filter(function(index){
            // test 클래스 요소 중 홀수 인덱스의 css를 바꿈
            return index % 2 == 1; // 리턴 결과가 true인 요소만 걸러냄
        }).css({"background":"blue", "color":"white"}); // 2, 4

        // 선택 된 요소 중 제일 처음에 있는 요소
        $("h3").first().css("font-size","1.5em"); // 1

        // 선택된 요소 중 제일 마지막에 있는 요소 리턴
        $("h3").last().text($("h3").last().text() + " : Last"); // 6 : Last

        // 인덱스 번호와 일치하는 요소만 리턴
        $("h3").eq(3).text($("h3").eq(3).text() + " : eq() method filtered"); // 4 : eq() method filtered

        // 인자값과 일치하지 않는 요소만 리턴
        $("h4").not(".test").css({"background":"yellow", "color":"black"}); // 5
    });
</script>
```

## 순회(탐색) 메소드

### Ancestors(조상) 메소드 : 선택된 요소의 상위 요소들을 선택할 수 있는 메소드

`$('요소명').parent()` : 선택 된 요소의 바로 위 상위 요소

`$('요소명').parents([매개변수])` : 선택 된 요소의 모든 상위 요소 리턴

매개변수가 있으면 매개변수와 일치하는 부모만 리턴

`$('요소명').parentsUntil(매개변수)` : 선택 된 요소부터 매개변수 요소까지 범위의 요소 리턴

```javascript
// 확인할 div 생성
<div class="wrap">
    <div class="type">div (great-grandparent)
        <ul>ul (grand parent)
            <li>li (direct parent)
                <span>span</span>
            </li>
        </ul>
    </div>
    <div class="type">div (grand parent)
        <p>p (direct parent)
            <span>span</span>
        </p>
    </div>
</div>
<script>
    $(document).ready(function(){
        // parent() : 선택 된 요소의 바로 위 상위 요소만 리턴
        // span 태그의 부모 요소 스타일 지정
        $("span").parent().css({"color":"red", "border":"2px solid red"});

        // parents() : 선택 된 요소의 모든 상위 요소 리턴
        // li 태그의 모든 상위 요소 스타일 지정
        $("li").parents().css("color","blue");

        // li 태그의 상위 요소 중 div만 스타일 지정
        $("li").parents("div").css("border", "2px dashed magenta");

        // parentsUntil() : 선택된 요소부터 매개변수 요소까지 리턴
        // span태그부터 div 태그 이전까지 스타일 지정
        $("span").parentsUntil("div").css("backgroundColor", "black");
    });
</script>
```

### descendants(자손, 후손) 메소드 : 선택 된 요소의 하위 요소들을 선택 할 수 있는 메소드

`$('요소명').children([매개변수])` : 선택 된 요소의 모든 자식 객체 리턴
매개변수가 있으면 매개변수와 일치하는 자식 객체만 리턴

`$('요소명').find(매개변수)` : 선택 된 요소의 인자와 일치하는 모든 후손 객체 리턴

```javascript
<div class="wrap">
    <div class="type">div (great-grandparent)
        <ul>ul (grand parent)
            <li>li (direct parent)
                <span>span</span>
            </li>
        </ul>
    </div>

    <div class="type">div (grand parent)
        <p>p (direct parent)
            <span>span</span>
        </p>
    </div>
</div>

<script>
    var style1 = {"color":"red", "border":"2px solid red"};
    var style2 = {"color":"blue", "border": "2px solid blue"};
    var style3 = {"color":"green", "border": "2px solid green"};
    var style4 = {"color":"orange", "border": "2px solid orange"};

    // children()
    // 클래스명이 wrap인 태그의 자손의 스타일 지정
    $(".wrap").children().css(style1);

    // 클래스명이 wrap인 태그의 자손의 자손의 스타일 지정
    $(".wrap").children().children().css(style2);

    // 클래스명이 wrap인 태그의 자손의 자손 중 ul 태그의 스타일 지정
    $(".wrap").children().children("ul").css(style3);

    // li의 스타일 style4로 변경
    //$(".wrap").find("li").css(style4);
    $(".wrap").children().children("ul").children("li").css(style4);

    // find()
    // 클래스명이 wrap인 모든 후손 중 span의 스타일 지정
    $(".wrap").find("span").css({"color":"purple", "border":"2px solid purple"});

</script>
```

### sideways 메소드 : 같은 레벨에 있는 요소(형제)를 선택할 수 있는 메소드

`$('요소명').siblings([매개변수])` : 선택 된 요소와 같은 레벨(형제)에 있는 모든 요소 리턴

매개변수가 있으면 같은 레벨에 있는 요소 중 매개변수와 일치하는 모든 요소 리턴

`$('요소명').next()` : 선택 된 요소의 같은 레벨 중 선택 된 요소 다음 한 개 요소 리턴

`$('요소명').nextAll()` : 선택 된 요소의 같은 레벨 중 선택 된 요소 다음의 모든 요소 리턴

`$('요소명').nextUntil(매개변수)` : 선택 된 요소의 같은 레벨 중 매개변수 이전까지의 모든 요소 리턴

 `$('요소명').prev()` : 선택 된 요소의 같은 레벨 중 선택 된 요소 이전 한 개 요소 리턴

`$('요소명').prevAll()` : 선택 된 요소의 같은 레벨 중 선택 된 요소 이전의 모든 요소 리턴

`$('요소명').prevUntil(매개변수)` : 선택 된 요소의 같은 레벨 중 매개변수 이전까지의 모든 요소 리턴

```javascript
<div class="wrap">div (parent)
    <p>p</p>
    <span>span</span>
    <h2>h2</h2>
    <h3>h3</h3>
    <p>p</p>
</div>

<script>
    var style1 = {"color":"red", "border":"2px solid red"};
    var style2 = {"color":"blue", "border":"2px solid blue"};
    var style3 = {"color":"yellow", "border":"2px solid yellow"};
    var style4 = {"background":"aqua", "color":"red"};

    // siblings([매개변수])
    // h2 태그의 형제 객체 스타일 지정
    $("h2").siblings().css(style1);

    // h2 태그의 형제 객체 중 p 태그의 스타일 지정
    $("h2").siblings("p").css(style2);

    // next()
    // h2 태그의 바로 다음 형제 요소의 스타일 지정
    $("h2").next().css(style3);

    // nextAll()
    // h2 태그의 다음에 오는 모든 형제 요소의 스타일 지정
    $("h2").nextAll().css(style4);

    // nextUntil(매개변수)
    // h2 태그부터 p 태그 이전의 모든 형제 요소의 스타일 지정
    $("h2").nextUntil("p").css("font-size","3em").css("border","dashed");

    // prev()
    // h2 태그 바로 이전 형제 요소에 스타일 지정
    $("h2").prev().css("backgroundColor", "pink"); 

    // prevAll()
    // h2 태그 이전 모든 형제 요소에 스타일 지정
    $("h2").prevAll().css(style4);

    // prevUntil(매개변수)
    // h2 태그부터 p태그 이전의 모든 형제 요소의 스타일 설정
    $("h2").prevUntil("p").css("border","dotted");   

    // is([인자]) : 요소가 있는지 찾는 메소드
    // 선택자로 지정된 범위에 특정한 요소가 존재하는지 찾을 때 사용
    // 있으면 true, 없으면 false

    // h2 태그 다음에 오는 모든 형제 요소들 중 p 태그가 있는지 검사
    console.log($("h2").nextAll().is("p"));
</script>
```
------------------------------------------------------------------------

## content 관련 메소드

### html() 메소드

선택된 요소의 content 영역을 리턴하거나 설정하는 메소드이다.
getter로 사용 시 해당 요소를 태그까지 포함하여 얻어오고
setter로 사용 시 작성 된 html 태그를 실제 태그로 인식시킨다.

```javascript
<h1 id="test1"><a>Link to Daum</a></h1>
<h1 id="test2"></h1>

<script>
    // getter
    $(document).ready(function(){
        var tmp = $("#test1").html();
        console.log("html 메소드 리턴 값 : " + tmp); // <a>Link to Daum</a>

        $("#test2").html(tmp); // test2의 innerHTML에 <a>Link to Daum</a> 추가
        $("#test2").children("a").attr("href", "https://www.daum.ent"); // test2의 a태그에 링크속성 추가
    });
</script>

<div class="testClass1">1</div>
<div class="testClass1">2</div>
<div class="testClass1">3</div>
<script>
    $(document).ready(function(){
        // jQuery 메소드 :  text(), html() 및 val() 에는 콜백 함수도 함께 제공 됨
        // 콜백 함수에는 선택 된 요소 목록의 현재 요소 인덱스와 원래(이전) 값의 두 매개변수가 있음
        $(".testClass1").html(function(index, html){
            // 이전 값 : 1, index : 0
            // 이전 값 : 2, index : 1
            // 이전 값 : 3, index : 2

            return "<h1>이전 값 : " + html + ", index : " + index + "</h1>"; 
        });
    });
</script>
```

### text() 메소드

선택 된 요소의 content 영역을 리턴하거나 설정하는 메소드이다.
getter로 사용 시 태그는 *무시*하고,
setter로 사용 시 *html 태그를 문자 자체로 인식*한다.

```javascript
<h1 id="test3">Link to Google</h1>
<h1 id="test4"></h1>

<script>
    //setter
    $(document).ready(function(){
        var tmp = $('#test3').text();
        console.log("text() 리턴 값 : " + tmp); // Link to Google

        $("#test4").text(tmp); // Link to Google
    });
</script>

<div class="testClass2">1</div>
<div class="testClass2">2</div>
<div class="testClass2">3</div>

<script>
    $(document).ready(function(){
        $(".testClass2").text(function(index, text){
            // <h1>이전 값 : 1, index : 0</h1> --> h1 태그를 html 태그가 아닌 text로 인식
            // <h1>이전 값 : 2, index : 1</h1>
            // <h1>이전 값 : 3, index : 2</h1>
            return "<h1>이전 값 : " + text + ", index : " + index + "</h1>";
        });
    });
</script>
```

## 객체 생성 및 제거

### 객체 생성

```javascript
<script>
    $(document).ready(function(){
        var txt1 = "<p>Create text with HTML</p>"; // html 

        var txt2 = document.createElement("p");
        txt2.innerHTML = " Create text with DOM"; // DOM

        var txt3 = $("<p></p>").text("Create text with jQuery"); // jQuery

        $("#area1").append(txt1, txt2, txt3); 
    });
</script>
```

### 삽입 메소드(A 기준)

선택자 요소를 기준으로 매개변수에 작성 된 생성 된 요소 또는 함수의 리턴값을 추가

`$(A).append(B)` : A 요소 내 뒷부분에 B를 추가(자식)
`$(A).prepend(B)` : A 요소 내 앞부분에 B를 추가(자식)
`$(A).after(B)` : A 요소 뒷부분에 B를 추가(형제)
`$(A).before(B)` : A 요소 앞부분에 B를 추가(형제)

```javascript
<h1 id="test1"><span>A</span></h1>
<h1 id="test2"><span>A</span></h1>
<h1 id="test3"><span>A</span></h1>
<h1 id="test4"><span>A</span></h1>

<script>
    $(document).ready(function(){
        $("#test1").append("<span class='added'>B</span>"); // AB
        $("#test2").prepend("<span class='added'>B</span>"); // BA
        $("#test3").after("<span class='added'>B</span>"); // A \n B
        $("#test4").before("<span class='added'>B</span>"); // B \n A
    });
</script>
```

### 삽입 메소드(B 기준)

생성 된 요소를 매개변수로 지정한 선택자 요소에 추가(part1의 메소드와 선택자, 생성구문의 순서가 반대)

`$(B).appendTo(A)` : B를 A의 요소 내 뒷부분에 추가(자식)
`$(B).prependTo(A)` : B를 A의 요소 내 앞부분에 추가(자식)
`$(B).insertAfter(A)` : B를 A의 요소 뒤에 추가(형제)
`$(B).insertBefore(A)` : B를 A의 요소 앞에 추가(형제)

```javascript
<h1 id="test5"><span>A</span></h1>
<h1 id="test6"><span>A</span></h1>
<h1 id="test7"><span>A</span></h1>
<h1 id="test8"><span>A</span></h1>

<script>
    // setInterval을 이용하여 1초마다 객체 추가
    $(document).ready(function(){ // 위의 test1~4와 결과 동일
        $("<span class='added'>B</span>").appendTo("#test5");
        $("<span class='added'>B</span>").prependTo("#test6");
        $("<span class='added'>B</span>").insertAfter("#test7");
        $("<span class='added'>B</span>").insertBefore("#test8");
    });
</script>
```

### 객체 복제 메소드

`clone([true|false])` : html 요소를 복사하는 메소드. 매개변수로 이벤트 복사 여부를 지정(기본 값 : false)

```javascript
<button id="clone">clone</button>
<div id="clone-test">
    <div id="item1" class="item"><span>Hello!</span></div>
</div>
<br>

<script>
    $(function(){
        $("#item1").hover(function(){ // 마우스 오버 이벤트 추가
            $(this).addClass("lime");
        }, function(){
            $(this).removeClass("lime");
        });
        $("#clone").click(function(){ // 버튼 클릭 이벤트 핸들러
            $("#item1").clone(true).appendTo("#clone-test"); // 이벤트 복사 속성 값 true 추가
        });
    });
</script>
```

### 객체 제거 메소드

`empty()` : 모든 자식 요소를 제거
`remove()` : DOM 요소 잘라내기(연관된 이벤트도 모두 삭제)
`detach()` : DOM 요소 잘라내기(관련된 이벤트 모두 보관함)

```javascript
<button id="empty">empty</button>&nbsp;
<button id="remove">remove</button>&nbsp;
<button id="detach">detach</button><br>

<div id="remove-test" class="box">
    <div id="item2" class="item"><span>Hello</span></div>
</div>
<div id="result" class="box"></div>

<script>
    $(function(){
        $("#item2").hover(function(){ // 이벤트 추가
            $(this).addClass("lime");
        }, function(){
            $(this).removeClass("lime");
        });

        $("#empty").click(function(){ // empty 테스트
            $("#remove-test").empty();
        });

        $("#remove").click(function(){ // remove 테스트
            var el = $("#item2").remove();
            $("#result").html(el);
        });

        $("#detach").click(function(){ // detach 테스트
            var el = $("#item2").detach();
            $("#result").html(el);
        });

    });
</script>
```

### each() 메소드

객체나 배열을 관리하는 `for in`문과 비슷한 메소드로 객체나 배열의 요소를 검사

* 작성방법
  1. `$.each(object, function(index, item){})` 의 형식으로 사용
  * index : 배열의 인덱스 또는 객체의 키를 의미한다.
  * item : 해당 인덱스나 키가 가진 값을 의미한다.

  2. `$('선택자').each(function(index, item){})`

```javascript
<div id="area1"></div>
<script>
    $(document).ready(function(){ // 객체 배열 생성
        var arr = [ {name : "Github", link : "http://www.github.com"},
                    {name : "Google", link : "http://www.google.com"},
                    {name : "w3c", link : "http://www.w3c.com"},
                    {name : "w3school", link : "http://www.w3schools.com"}];
        var output = "";
        $.each(arr, function(index, item){ // arr에 하이퍼링크 추가
            output += "<h2><a href=" + item.link + ">" + item.name + "</a></h2>";
        });

        $("#area1").html($("#area1").html() + output); // area1 div에 기존 내용에 덧붙여 html 추가
    });
</script>
<hr>

// each()를 통해서 style 추가
<style> // 추가할 스타일
    .highlight_0{background:red;}
    .highlight_1{background:orange;}
    .highlight_2{background:yellow;}
    .highlight_3{background:green;}
    .highlight_4{background:blue;}
</style>

<div id="wrap"> // 스타일이 추가될 html
    <h1>item-0</h1>
    <h1>item-1</h1>
    <h1>item-2</h1>
    <h1>item-3</h1>
    <h1>item-4</h1>
</div>
<script>
    $(document).ready(function(){
        $("#wrap").children().each(function(index, item){ // wrap ID의 자식 태그들에게 each() 통해 index 순서로 class 추가하여 스타일과 연결
            $(this).addClass("highlight_"+index);
        });
    });
</script>
```

### `is()` : 문서 객체의 특징 판별

매개변수로 선택자를 입력하고, 선택한 객체가 선택자와 일치하는지 판단하여 boolean 리턴

```javascript
<h3 class="test">test1</h3>
<h3>test2</h3>
<h3 class="test">test3</h3>
<h3 class="test">test4</h3>
<h3>test5</h3>
<h3 class="test">test6</h3>
<script>
    $(function(){ // h3 태그에 차례대로 접근하여 class 속성이 "test"일 경우 스타일 변경
        $("h3").each(function(){
            if($(this).is(".test")){ // 1, 3, 4, 6에 css 적용됨
                $(this).css({"background":"orangered", "color":"white"}); 
            }
        });
    });
</script>
```

### `$.extend()` 메소드 : 여러 개의 객체를 하나로 합칠 때 사용

```javascript
<script>
    $(document).ready(function(){
        var obj1 = {name:"Mota", age:40};
        $.extend(obj1, {job:"player"});
        console.log(obj1); // {name: "Mota", age: 40, job: "player"}

        var obj2 = {name:"Molina", Strength:["Dribble", "Freekick"]};

        // 두 객체를 하나로 합칠 때도 사용할 수 있으며, 중복되는 속성의 경우 덮어쓰기
        $.extend(obj1, obj2);
        console.log(obj1); // {name: "Molina", age: 40, job: "player", Strength: Array(2)}
    });
</script>
```

### '$.noConflict()` 메소드

많은 자바스크립트 라이브러리가 `$` 기호를 함수, 변수로 사용하고 있기 때문에 jQuery 라이브러리와 충돌 가능성이 있음.
이를 방지하기 위해 `noConflict()` 메소드를 통해 `$` 대신 새로운 alias 부여

```javascript
<h1 id="ncTest">Hello</h1>
<script>
    $(document).ready(function(){
        $("#ncTest").css("color","red");
    });

    var jq = $.noConflict(); // jQuery에서 사용하는 별칭 : '$' --> 'jq'

    jq(function(){ // 기존 $(function(){}) 형태로는 사용 불가
         jq("#ncTest").css("color", "red");
    });
</script>
```

## 이벤트

### 이벤트 관련 속성

이벤트 핸들러의 매개변수로 event 객체를 전달한다.
인라인 방식으로 이벤트 설정 시 매개변수 키워드는 event로 고정

```javascript
<button onclick="test(event);">실행확인</button>
<script>
    function test(e){
        console.log(e); // MouseEvent 생김
        console.log(e.target); // 이벤트가 발생한 객체 리턴 : <button onclick="test(event);">실행확인</button>
    }
</script>
```

### 이벤트 연결 종류

요소 객체에 이벤트 발생 시 연결될 이벤트 핸들러를 지정하는 메소드

_`$('선택자').bind()` : 현재 존재하는 문서 객체만 이벤트 연결_

_`$('선택자').unbind()` : bind()로 연결 된 이벤트 제거_


`bind(), unbind()` 메소드는 jquery3.0부터 deprecated로 설정

> `on(), off()` 메소드 사용

`$('선택자').on("이벤트명", "이벤트 핸들러")`, `$('선택자').off()`

* `on()` 메소드의 기본 사용법

```javascript
<h1 id="test1">Your Mouse, here!</h1>

<script>
    // on() 메소드 기본적인 사용법
    $("#test1").on('click', function(){
        console.log(event.target); // <h1 id="test1">Your Mouse, here!</h1>
        console.log($(this).text()); // Your Mouse, here!
    });

    // on() 안에 객체 타입으로 여러 이벤트를 작성 가능
    $("#test1").on({'mouseenter':function(){
        $(this).css("background", "yellowgreen").text("Your Mouse is here!");
    }, 'mouseleave':function(){
        $(this).css("background", "yellow").text("Your Muose is gone away..");
    }, 'click':function(){ // off()를 통해 mouseenter, mouseleave 이벤트 제거
        $(this).off('mouseenter').off('mouseleave').css("background", "orangered").text("Mouse Event Deleted.");
    }});
</script>
```

* `$('선택자').on(event, selector, handler)`

선택자를 기준으로 매개변수로 전달된 selector에 지정한 event 발생 시 해당 handler를 동적 적용시켜 이벤트 처리 가능

```javascript
<div id="wrap">
    <h2>Add new h2 Tag</h2>
</div>
<script>
    $(document).on('click', 'h2', add); // h2 태그를 클릭하면, 새로운 h2 태그를 생성함

    function add(e){
        console.log(e.target); // <h2>Add new h2 Tag</h2>
        $("#wrap").append("<h2>h2 Tag added!</h2>");
    }
</script>
```

* `one()` 메소드 : 이벤트를 한 번만 연결할 때 사용

```javascript
<h1 id="test">Click!</h1>
<script>
    $(function(){
        $("#test").one('click', function(){
            console.log("It's Only one log!"); // 한번만 콘솔창에 로그가 남음
        });
    });
</script>
```

### 이벤트 연결 메소드

#### 마우스 관련 메소드
 
```javascript
<div class="outer o1" width="300px" height="300px" padding="50px">
    <div class="inner" width="200px" height="200px"></div>
</div>
<p id="output"></p>
<div class="outer o2" width="300px" height="300px" padding="50px>
    <div class="inner" width="200px" height="200px"></div>
</div>
<p id="output2"></p>

<script>
    $(document).ready(function(){
        // mouseover, mouseout -> 자식 요소 접근 시에도 이벤트 발생

        // mouseover() : 마우스가 요소에 있을 경우
        $(".o1").mouseover(function(){ // 부모 클래스에서 이벤트 지정 시
            $("#output").text($("#output").text() + 'OVER!'); // 자식 클래스에서도 이벤트 발생
        });

        // mouseout() : 마우스가 요소에서 나갈 때
        $(".o1").mouseout(function(){
            $("#output").text($("#output").text() + 'OUT!');
        });

        // mouseenter(), mouseleave()
        // -> 자식 요소 접근 시에는 이벤트가 발생하지 않음

        // mouseenter() : 마우스가 요소에 들어올 때
        $(".o2").mouseenter(function(){ // 부모 클래스에서 이벤트 지정 시
            $("#output2").text($("#output2").text() + 'ENTER!'); // 자식 클래스에서는 이벤트 미발생
        });

        // mouseleave() : 마우스가 요소에서 나갈 때
        $(".o2").mouseleave(function(){
            $("#output2").text($("#output2").text() + 'LEAVE');
        });
    });
</script>
```

#### 키보드 이벤트

keydown : 키보드가 눌려질 때.
keypress : 글자가 입력 될 때. Fn 키, 기능 키 사용 못함.
keyup : 키보드가 떼어질 때.

```javascript
<input type="text" id="test">
<script>
    $(document).ready(function(){
        $("#test").keydown(function(e){
            console.log("keydown : " + e.key); // 누르면 계속 로그 생성
        });

        $("#test").keypress(function(e){
            console.log("keypress : "+ e.key); // Ctrl, Shift 등 Fn키는 로그 생성하지 않음
        });

        $("#test").keyup(function(e){
            console.log("keyup : " + e.key); // 키보드에서 손을 떼야 로그 생성
        });
    });
</script>
```

#### 동적으로 글자수 세기

```javascript
// 글자수를 셀 textarea 생성
<div>
    <p><span id="counter">0</span>/150</p>
    <textarea cols="70" rows="5"></textarea>
</div>
<script>
    $(document).ready(function(){
        $("textarea").keyup(function(){ // textarea에서 keyup 이벤트가 발생했을 경우
            var inputLength = $(this).val().length; // 현재 요소(textarea)의 값의 길이를 저장
            $("#counter").html(inputLength);

            var remain = 150 - inputLength;

            if(remain >= 0){
                $("#counter").css("color", "black"); // 기본값
            }else {
                $("#counter").css("color", "red"); // 색상 변경
            }
        });
    });
</script>
```

#### 동적으로 아이디 조건 확인

```javascript
/*
    - 첫 글자는 반드시 영문 소문자
    - 영문 소문자와 숫자로만 이루어짐
    - 총 4~12자 */

// 아이디 조건 입력받을 input 생성
<label for="memberId">ID : </label>
<input type="text" name="memberId" id="memberId">
<span id="idCheck"></span>

<script>
    var regExp = /^[a-z][a-z\d]{3,11}$/; // 아이디 검사 정규표현식

    $(document).ready(function(){
        $("#memberId").keyup(function(){
            if(regExp.test($(this).val())){ // 정규식을 통과하면
                $("#idCheck").css({'color':'green', 'font-weight':'bolder'}).html("사용 가능한 아이디 형식입니다.");
            }else{ // 통과하지 못할 경우
                $("#idCheck").css({'color':'red', 'font-weight':'bolder'}).html("사용할 수 없는 아이디 형식입니다.");
            }
        });
    });
</script>
```

#### `trigger()` 메소드

특정 이벤트나 기본 이벤트를 강제로 발생 시키는 메소드로, 사용자 정의 이벤트 발생 시 사용하며 이벤트 발생 시 인자 값 전달 가능

```javascript
<div class="trg" id="trg">
    click Num : <span>0</span>
</div>
<div class="increment" id="increment">click me!</div>
<script>
    var ctn = 0;
    $(function(){
        $("#trg").on('click', function(){
            ctn++;
            $("span").text(ctn);
        });

        $("#increment").click(function(){ // click 이벤트 핸들러를 요청함
            $("#trg").trigger('click');
        });
    });
</script>

/*
    trigger 메소드는 실제 클릭이 일어나는 것이 아닌 click 이벤트 핸들러를 호출함.
    그래서 아래 경우에 링크로 실제 이동하지 않음.
*/

<a href="https://www.google.com" id="goGoogle" onclick="justClicked();">Go to Google</a>
<button id="btnTrg">trigger를 통한 a 태그 클릭</button>
<script>
    jQuery(function(){
        $("#btnTrg").click(function(){
            $("#goGoogle").trigger('click');
        });
    });

    function justClicked(){
        console.log("justClicked!!"); // button을 통한 trigger 메소드는 실제 링크로 이동할 수 없다.
    }
</script>
```

### display 속성 메소드

#### 시각적 효과

* Effect 메소드 : 페이지에 애니메이션 효과를 만들기 위한 메소드 집합

```
1. $('s').메소드명();
2. $('s').메소드명([speed],);
3. $('s').메소드명([speed], [easing], [callback]);
speed : 실행속도(밀리세컨초) / 숫자 or slow, fast
easing : 변경되는 지점별 속도 / linear, swing 가능
callback : 메소드 실행 후 실행할 함수
```

`show()`, `hide()` : 문서 객체를 크게 하며 보여주거나 작게 하며 사라지게 한다

  - 사용법 : `$(selector).show(speed, easing, callback);`

```javascript
<button id="show">Show</button>
<button id="hide">Hide</button><br>
<img id="berlin" src="https://www.thelocal.de/userdata/images/article/cb964e6f592a0abb65c7cc19f14d59a96ca0af995d2ec371812dd6c41b202d34.jpg">
<script>
    $(function(){
        $("#show").click(function(){
            $("#berlin").show(1000); // 1000밀리세컨드(1초)의 시간동안 width, height가 커짐
        });

        $("#hide").click(function(){
            $("#berlin").hide(1000); // 1000밀리세컨드(1초)의 시간동안 width, height가 작아짐
        });
    });
</script>

<button id="toggle">Toggle</button>
<br>
<img id="london" src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/87/Palace_of_Westminster_from_the_dome_on_Methodist_Central_Hall.jpg/1000px-Palace_of_Westminster_from_the_dome_on_Methodist_Central_Hall.jpg">
<script>
    $("#toggle").click(function(){
        console.log($("#london").css('display')); // display가 보일 때 : inline, 안보일때 : none
        if($("#london").css('display') == 'none') { // 버튼을 누르면 현재 display 상태에 따라 show(), hide()됨
            $("#london").show(1000);
        } else {
            $("#london").hide(1000);
        }
    });
</script>
```

* slide 메소드

`slideDown()`과 `slideUp()`

  - 사용법 : `$(selector).slideUp(speed, easing, callback)`

```javascript
// div 및 contents 영역의 크기 style 지정
<style>
div {
    width:300px;
    height:30px;
    background:yellowgreen;
    color:orangered;
    border-radius:10px;
    text-align:center;
    border:1px solid green;
    cursor:pointer;
}
p.contents{
    border:1px solid lightgray;
    width:300px;
    height:200px;
    display: none;
}
</style>
// div, contents html
<div>No.1</div>
<p class="contents">1</p>
<div>No.2</div>
<p class="contents">2</p>
<div>No.3</div>
<p class="contents">3</p>
<div>No.4</div>
<p class="contents">4</p>
<div>No.5</div>
<p class="contents">5</p>

<script>
    $(function(){
        $('div').click(function() {
            if($(this).next("p").css("display") == "none") { // div의 p 태그 display가 닫혀있을 때
                $(this).siblings("p.contents").slideUp(); // 모든 다른 contents의 영역을 닫고
                $(this).next().slideDown(); // 클릭한 div의 p태그를 연다.
            } else { // 만약 div의 p태그 display가 열려있을 때
                $(this).next().slideUp(); // 클릭한 div의 p태그를 닫는다.
            }
        })
    })
</script>
```

* `fade()` 메소드

  * `fadeIn` : 점점 진하게 변하면서 보여지는 효과

  * `fadeOut` : 점점 희미하게 변하면서 사라지는 효과

  * `fadeTo` : 설정한 값까지 희미해지는 효과 -> opacity 값으로 투명도 설정

  * `fadeToggle` : fadeIn과 fadeOut을 동시에 적용하는 메소드

  * 사용법 : `$('s').fideIn/Out/Toggle([속도],[구간별속도],[callback]);`, `$('s').fadeTo([시간],[투명도],[구간별속도],[callback]);`

```javascript
<button id="fadein">fadeIn()</button>
<button id="fadeout">fadeOut()</button><br>

<!-- fadeIn(), fadeOut() -->
<img id="moscow" src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/62/Panoramic_view_of_Moscow1.jpg/600px-Panoramic_view_of_Moscow1.jpg">

<script>
    $(function(){
        $("#fadein").click(function(){ // fadeIn()을 클릭하면 img가 서서히 나온다.(1초)
            $("img").fadeIn(1000);
        });
        $("#fadeout").click(function(){ // fadeOut()을 클릭하면 img가 서서히 사라진다.(1초)
            $("img").fadeOut(1000);
        });
    });
</script>

<!-- fadeToggle() -->
<button id="toggle">fadeToggle()</button>
<img id="saint" src="https://media.tacdn.com/media/attractions-splice-spp-674x446/06/70/64/98.jpg">
<script>
    $(function(){
        $("#toggle").click(function(){ // fadeToggle()을 클릭하면, 상태에 따라 img가 나오거나 사라진다.
            $("#saint").fadeToggle(1000, function(){
                alert("Toggle Complete!"); // fadeIn() or fadeOut() 완료시 alert창 나옴.
            });
        });
    });
</script>

<!-- fadeTo() -->
<img id="moscow1" src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/62/Panoramic_view_of_Moscow1.jpg/600px-Panoramic_view_of_Moscow1.jpg">

<script>
    $(function(){ 
        $("#moscow1").hover(function(){
            $(this).fadeTo(700, 1); // 마우스를 올리면 0.7초동안 투명도 1(불투명)으로 변경
        }, function(){
            $(this).fadeTo(700, 0.4); // 마우스를 떼면 0.7초동안 투명도 0.4(약간 투명)으로 변경
        });
    });
</script>
```

### 애니메이션

애니메이션 효과를 만들기 위한 메소드 집합

#### 'animate() 메소드

```
<code>.animate(properties [, duration] [, easing] [, complete])</code>
properties : 변경할 css 속성을 객체로 전달
duration : 기본 값은 400, millisec|slow|fast
easing : 속도 옵션. swing | linear 기본값은 swing
         더 많은 easing function은 jqueryUI 또는 별도의 plugin을 사용해야 함
complete : 애니메이션이 완료 되었을 때 호출 될 콜백함수 작성
```

```javascript
<script>
    // w3schools에서 기본 지원되는 속성 확인(https://www.w3schools.com/jquery/eff_animate.asp)
    // color 같은 경우 기본적으로 지원하지 않으므로, jquery-ui의 color 플러그인을 import 해서 사용(https://api.jqueryui.com/color-animation/)

    $(function(){
        $("#btn1").click(function(){
            $("#test1").animate({width:"500px", backgroundColor:"blue"}, 1000, function(){
                alert("Animate Complete!"); // 1초에 걸쳐 test1 id 영역이 width 500px로 size 변경 후 alert창 뜸
            });
        });
    });
</script>

<img src="https://techcrunch.com/wp-content/uploads/2015/08/safe_image.gif" width="150px" heihgt="100px" class="image">
<script>
    $(document).ready(function(){
        $(".image").click(function(event){ // image class를 가진 img를 클릭할 경우
            $(this).animate({'left':'-160px'}, 'slow'); // 해당 img가 왼쪽으로 160px 이동(웹브라우저에서 보이지 않게 됨)
        });
    });
</script>

<p>가운데 위치한 div 컨테이너 안에서 img를 우측으로 보내서 감추어 보기. div 컨테이너의 css 속성 width, overflow 등을 설정
<div id="scroller">
    <img src="https://techcrunch.com/wp-content/uploads/2015/08/safe_image.gif" width="150px" height="100px" class="image2">
</div>
<script>
    $(document).ready(function(){
        $(".image2").click(function(){ // img를 우측으로 160px 이동
            $(this).animate({'left':'160px'}, 1000);
        });
    });
</script>
```

#### 상대적 애니메이션

```javascript
// div의 스타일 지정
<style>
    div{
        width:50px;
        height:50px;
        position:relative;
    }
</style>

// div html 지정
<div></div>
<div></div>
<div></div>
<div></div>
<div></div>
<div></div>
<div></div>

<script>
    $(function(){
        $("div").click(function(){
            var w = $(this).width();
            var h = $(this).height();

            console.log(w);
            console.log(h);

            $(this).animate({width:w+50,height:h+50}, "slow");

        });

        $("div").each(function(index){ // 위에서부터 아래로 상자 색깔이 변경된 상태로 
            $(this).css("backgroundColor", "rgb(255,220," + (index*30) + ")");
            $(this).delay(index * 50).animate({left:200}, 'slow'); // 조금씩 딜레이되어 animation이 실행됨
        });
    });
</script>
```