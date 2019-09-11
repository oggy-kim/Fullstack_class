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

```jQuery
$(document).ready(function(){
    $("*").css("color","red"); // css() 메소드 : 스타일과 관련된 기능 수행
});
```

### 태그 선택자

* `$("태그이름")`

```jQuery
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

```jQuery
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

```jQuery
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

```jQuery
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

```jQuery
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

```jQuery
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
