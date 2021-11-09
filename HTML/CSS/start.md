# HTML/CSS 

## 웹 앱 화면 설계
+ id: 고유한 이름을 붙일 때
    + <div id = "writing-section"> -> div#writing-seciton
+ class: 반복되는 영역을 유형별로 분류할 때
    + <li class="comment"> -> li.comment

## flex: grow, shrink, basis
    + grow(늘린다): 아이템들의 basis를 제외한 여백 부분을 grow에 지정된 숫자의 비율로 나누어 가진다.
    + shrink(줄인다): grow의 반대라고 생각하면 쉽다. basis 값보다 작아질 수 있는지.(0으로 세팅하면 basis보다 작아지지 않아 고정폭을 쉽게 만들 수 있다.)
    + basis(기본 크기): 아이템의 기본 크기

## 정렬
    + 수직 정렬: align-items
    + 수평 정렬: justify-content

## id와 Class를 어느 떄에 사용 해야 되는지?
    + Id: 고유한 이름을 붙일 때
    + Class: 반복되는 영역을 유형별로 분류할 때