# WEB API

## 1. Bootstrap

트위터에서 개발한 UI 라이브러리로, 웹 사이트 디자인 개발 시간을 줄이며 반응형 웹 사이트 개발을 위해 만듬
[부트스트랩 공식 사이트](http://www.getbootstrap.com)

### 부트스트랩 로딩 방법

```html
// CDN으로 불러오기
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

// Download 받은 뒤 링크로 연결하기
<link rel='stylesheet' href='../css/bootstrap.css'>
<script type='text/javascript' href="../js/bootstrap.js">
```

일부 샘플은 무료로 사용할 수 있고, 일부 샘플을 유료 결제를 해야만 사용할 수 있음.


## 2. Geolocation

위치 정보 API를 사용하기 위해 `navigator.geolocation` 내장 객체를 이용해야 함

* GeoLocation 지원여부 확인

```html
<button id="btn1">GeoLocation navigator</button>
<script>
    $(function(){
        $('#btn1').on('click', supportGeolocation);
    });

    function supportGeolocation() { // 지원 여부 확인
        if(window.navigator.geolocation){
            console.log('geolocation을 지원합니다.');
        }else{
            console.log('geolocation을 지원하지 않습니다.');
        }
    }
</script>
```

* 위도/경도 확인

```html
<script>
    $(function(){
        $("#btn2").on('click', getGeolocation);
    });


    function getGeolocation(){ // 위치정보 획득
        if(window.navigator.geolocation){
            //navigator.geolocation.getCurrentPosition(successCallback, [errorCallback, [options]])
            // : 현재 위치 정보 반환
            navigator.geolocation.getCurrentPosition(showPosition, handleError);
        }else {  
            $("#comment").html('Geolocation을 지원하지 않는 브라우저입니다.');
        }

        function showPosition(position){ // successCallback
            $("#comment").append('위도 : ' + position.coords.latitude + "<br>경도"
                                + position.coords.longitude + "<br>");
            console.log(new Date(position.timestamp)); // timestamp : 위치 정보를 가져온 시각
        }


        function handleError(error){ // errorCallback
            // code 1 : 사용자가 위치 정보에 대한 접근을 막은 경우
            if(error.code == error.PERMISSION_DENIED){
                alert('사용자가 위치정보에 대한 접근을 막은 경우');
            }
            // code 2 : 네트워크 또는 GPS에 연결할 수 없는 경우
            else if(error.code == error.POSITION_UNAVAILABLE){
                alert('네트워크 또는 GPS에 연결할 수 없는 경우');
            }
            // code 3 : 사용자의 위치정보를 계산하는데 시간이 초과한 경우
            else if(error.code == error.TIMEOUT){
                alert('사용자의 위치정보를 계산하는데 시간이 초과한 경우');
            }
            // code 4 : 그 외 알 수 없는 문제가 생긴 경우
            else if(error.code == error.UNKNOWN_ERROR){
                alert('그 외 알 수 없는 문제가 생긴 경우');
            }
        }
    }
</script>
```

## 3. Drag and Drop

마우스를 이용하여 파일이나 데이터를 애플리케이션 간에 전달하는 기능
특히 웹 애플리케이션에서는 화면 상에 나타나는 요소를 옮기거나, 웹 브라우저와 다른 웹 브라우저 간의 자료를 전달하기 위해 사용됨

끌기 할 요소에 `draggable` 속성과 끌기 관련 이벤트인 `dragstart, dragend, drag이벤트 처리`
놓기 영역 요소에는 `dragenter, dragover, dragleave`이벤트 처리
(놓기 영역에 요소를 끌어다 놓을 경우 drop 이벤트 발생)

### 끌기 이벤트

```
- dragstart : 요소를 끌기 시작했을 때 발생
- drag : 요소를 끌기 도중에 발생
- dragend : 요소를 끌기 끝났을 때 발생
```

```html
<div id="imgs">
    <img id="img1" class="image" src='../images/tour1.jpg' draggable='false'> // draggable 'false'이면 드래그 불가
    <img id="img2" class="image" src='../images/tour2.jpg' draggable='true'>
</div>

<div id='div1' class='div'></div>
<script>
    var src = document.getElementById('imgs');

    var isDragging;
    var srcId;

    src.ondragstart = function(e){
        srcId = e.target.id;
        $("#div1").append('srcId : ' + srcId + '<br>'); // srcId : img2
        $("#div1").append('dragstart : ' + srcId + '<br>'); // dragstart : img2
        isDragging = false;
        console.log(srcId);
    }

    src.ondrag = function(e){
        if(!isDragging){
            $("#div1").append('drag : ' + srcId + '<br>'); // drag : img2
            isDragging = true;
        }
    }
    /* isDragging의 역할은 drag를 하고 있으면 계속 drag 이벤트가 호출됨
        이를 막기 위해서 한 번만 호출 되게 처리하는 용도 */
    src.ondragend = function(e){
        $("#div1").append('dragend : ' + srcId + "<br>"); // dragend : img2
    }
</script>
```

### 놓기 이벤트

```
- dragenter : 끌기한 요소가 놓기 영역으로 들어왔을 때 발생
- dragover : 끌기한 요소가 놓기 영역에 있을 때 발생
- dragleave : 끌기한 요소가 놓기 영역을 떠날 때 발생
- drop : 끌기한 요소를 놓기할 때 발생
```

```html
<img id='img3' class='image' src='1.jpg' draggable='true'> // 1.jpg 이미지
<div id='area' class='div'></div>
<div id='div2' class='div'></div>
<script>
    var src = document.getElementById('img3');
    var target = document.getElementById('area');
    var isDraggingOver;
    var srcId, targetId;

    target.ondragenter = function(e){
        targetId = e.target.id;
        $("#div2").append('dragenter : ' + targetId + "<br>");
        isDraggingOver = false;
    }

    target.ondragover = function(e){
        // HTML 요소들의 기본 값은 드롭을 받아들이지 X
        // 이벤트의 preventDefault() 함수로 기본값 취소
        e.preventDefault();
        // -> 이 코드가 없으면 객체를 놓았을 때 drop 대신 leave 동작

        if(!isDraggingOver){
            $("#div2").append('dragover : ' + targetId + '<br>'); // dragover : img3
            isDraggingOver = true;
        }
        /* dragenter의 경우 한 번만 일어나는데 dragover는 그 영역에
            있으면 계속 일어나므로 방지하기 위해 isDraggingOver 사용*/
    }

    target.ondragleave = function(e){
        $("#div2").append('dragleave : ' + targetId + "<br>"); // dragleave : img3
    }

    target.ondrop = function(e){
        $("#div2").append('drop : ' + targetId + "<br>"); // drop : img3
    }

</script>
```

## 4. localStorage

웹 스토리지가 나오기 전에는 쿠키를 사용했으나 저장 용량이 적고 보안이 취약하여, 웹 브라우저에 저장하는 방법인 웹 스토리지를 선택

```html
<button id="removeItem">데이터 삭제</button>
<button id="clearItem">전체 데이터 삭제</button>
<script>
    if(window.localStorage){
        console.log('localStorage가 지원되는 브라우저입니다.');
        // localStorage setItem
        localStorage.team = 'seongnamFC';
        localStorage['league'] = 'KLeague';
        localStorage.setItem('player', 'Bomin');
        // localStorage getItem
        console.log('localStorage team : ' + localStorage.academy);
        console.log('localStorage league : ' + localStorage['league']);
        console.log('localStorage player : ' + localStorage.getItem('player'));
        // sessionStorage setItem
        sessionStorage.LoginUser = 'eder';
        sessionStorage['userId'] = 'ederr';
        sessionStorage.setItem('loginDate', new Date());
        // sessionStorage getItem
        console.log('sessionStorage LoginUser : ' + sessionStorage.LoginUser);
        console.log('sessionStorage userId : ' + sessionStorage['userId']);
        console.log('sessionStorage loginDate : ' + sessionStorage.getItem('loginDate'));
        /*
            storage 확인하는 방법
            F12 - Application 탭 - storage에서 확인
            창이나 탭을 닫으면 sessionStroage는 사라지고 
            사용자가 지우지 않는 이상 localStorage는 남아있음
        */
    }else{
        console.log('localStorage가 지원되지 않는 브라우저입니다.');
    }

    $("#removeItem").on('click', function(){
        // 반 데이터 삭제
        // localStorage.removeItem('class');

        // 세션 스토리지의 userId 삭제
        sessionStorage.removeItem('userId');
    });

    $("#clearItem").on('click', function(){
        // 전체 데이터 삭제
        // localStorage.clear();

        // 세션 스토리지 전체 데이터 삭제
        sessionStorage.clear();
    });
</script>
```

