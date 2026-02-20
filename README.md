# Tech_Note
A personal space to document new technical insights and learnings from my work.

## I just need consistency to level up my coding and my life

**20260220** upgrade my jsp

-float-left → d-flex 

# 📘 JSP Frontend Tech Note
> 비전공자를 위한 JSP + jQuery + Bootstrap 정리노트

---

## 📌 목차
1. [jQuery 기초 (`$`)](#1-jquery-기초-)
2. [function 이란?](#2-function-이란)
3. [$.ajax 란?](#3-ajax-란)
4. [document.ready 란?](#4-documentready-란)
5. [전체 흐름 요약](#5-전체-흐름-요약)
6. [HTML div 구조 이해](#6-html-div-구조-이해)
7. [자주 쓰는 Bootstrap class](#7-자주-쓰는-bootstrap-class)
8. [float → d-flex 전환 (최신 방식)](#8-float--d-flex-전환-최신-방식)
9. [실전 예제 - card-header 개선](#9-실전-예제---card-header-개선)
10. [이모티콘 경고 문구 추가](#10-이모티콘-경고-문구-추가)

---

## 1. jQuery 기초 (`$`)

`$` 는 **jQuery** 라이브러리의 별명이에요.
HTML 요소를 쉽게 찾고 조작하려고 쓰는 도구예요.

```javascript
$('#lookupBtn')               // id="lookupBtn" 인 요소 찾기
$('.btn')                     // class="btn" 인 요소 찾기
$('#LookupZone2').html(data)  // LookupZone2 내용을 data로 교체
```

> 💡 `#` = id 선택 / `.` = class 선택

---

## 2. `function` 이란?

재사용할 수 있는 **명령 묶음**이에요.
같은 코드를 여러번 쓰기 싫을 때 이름 붙여서 저장해두는 것.

```javascript
// 저장
function do_refresh() {
    // 버튼 누르면 할 일들...
}

// 나중에 필요할 때 실행
do_refresh();
```

---

## 3. `$.ajax` 란?

**페이지 새로고침 없이** 서버에 데이터를 요청하는 방법이에요.

```javascript
$.ajax({
    url: '/서버주소',           // 어디에 요청할지
    data: $('#폼').serialize(), // 뭘 보낼지 (날짜, 모델명 등)
    type: 'POST',
    dataType: 'json',
    success: function(data) {
        $('#LookupZone2').html(data.report); // 성공하면 여기에 결과 넣기
    }
});
```

> 💡 서버 → 데이터 받기 → 화면 일부만 업데이트!

---

## 4. `document.ready` 란?

```javascript
$(document).ready(function() {
    // 페이지 다 로딩되면 이걸 실행해줘
});
```

HTML이 다 그려진 다음에 JS가 실행되도록 **순서를 잡아주는 것**이에요.
없으면 HTML보다 JS가 먼저 실행돼서 요소를 못 찾는 경우가 생겨요.

---

## 5. 전체 흐름 요약

```
페이지 열림
    └── document.ready 실행
            ├── 버튼에 클릭 이벤트 등록
            ├── Select2 초기화
            └── DatePicker 초기화

버튼 클릭
    └── do_refresh() 실행
            └── 여러 $.ajax 로 서버에 요청
                    └── 결과를 각 LookupZone에 넣음
```

---

## 6. HTML div 구조 이해

`div` 는 **박스**예요. 박스 안에 박스가 계속 들어가는 구조!

```
container-fluid         (전체 페이지 박스)
└── card                (카드 박스)
    ├── card-header     (카드 윗부분 - 필터 영역)
    │   ├── 제목
    │   └── 필터들 + 버튼
    │
    └── card-block      (카드 아랫부분 - 탭 + 내용)
        ├── nav-tabs    (탭 메뉴)
        └── tab-content (탭 내용)
            ├── Tab1 → LookupZone_1
            ├── Tab2 → LookupZone_2
            └── Tab3 → LookupZone_3
```

> 💡 핵심 3가지
> - `div` = 박스
> - `class` = 박스 스타일/역할 이름
> - `id` = 박스 고유 이름 (JS에서 `#`으로 찾음)

---

## 7. 자주 쓰는 Bootstrap class

| class | 뜻 |
|---|---|
| `container-fluid` | 화면 꽉 채우는 전체 틀 |
| `card` | 테두리 있는 카드 박스 |
| `card-header` | 카드 상단 (보통 필터/제목) |
| `card-block` | 카드 하단 (내용) |
| `d-flex` | 요소들을 가로로 나란히 배치 |
| `justify-content-between` | 양 끝으로 분리 |
| `align-items-center` | 세로 가운데 정렬 |
| `gap-2` | 요소 사이 간격 |
| `input-group` | input + 라벨 묶음 |
| `tab-pane` | 탭 클릭시 보이는 내용 영역 |
| `btn btn-success btn-sm` | 초록색 작은 버튼 |

---

## 8. `float` → `d-flex` 전환 (최신 방식)

`float` 은 원래 이미지 옆에 텍스트 배치용이었는데 레이아웃에 막 쓰다보니 문제가 많아서 `d-flex` 로 넘어갔어요.

### justify-content 옵션

| 옵션 | 뜻 |
|---|---|
| `justify-content-between` | 양 끝으로 분리 ← float-left/right 대체 |
| `justify-content-start` | 왼쪽 정렬 |
| `justify-content-end` | 오른쪽 정렬 |
| `justify-content-center` | 가운데 정렬 |
| `align-items-center` | 세로 가운데 정렬 |

```html
<!-- ❌ 기존 (float 방식) -->
<div class="container-fluid">
    <div class="float-left">제목</div>
    <div class="float-right">버튼들</div>
</div>

<!-- ✅ 개선 (d-flex 방식) -->
<div class="d-flex justify-content-between align-items-center">
    <div>제목</div>
    <div class="d-flex align-items-center gap-2">버튼들</div>
</div>
```

---

## 9. 실전 예제 - card-header 개선

```html
<!-- ✅ 개선된 card-header -->
<div class="d-flex justify-content-between align-items-center">

    <!-- 왼쪽: 제목 -->
    <div class="card-title mb-0">
        <h2><i class="bi bi-balloon-fill text-warning"></i>WAREHOUSE IN-N-OUT</h2>
    </div>

    <!-- 오른쪽: 필터 폼 -->
    <div>
        <form id="lookupForm" method="post">
            <input type="hidden" id="lookupModel" name="model" value="" />
            <input type="hidden" id="lookupDefect" name="defect" value="" />
            <input type="hidden" id="lookupKeyword" name="keyword" value="" />
            <input type="hidden" id="lookupFrom" name="from" value="" />

            <div class="d-flex align-items-center gap-2">

                <div class="input-group input-group-sm">
                    <span class="input-group-text">Pdesc</span>
                    <select name="pdesc" multiple class="js-pdesc-select form-select form-select-sm" style="width:300px;">
                        <!-- options -->
                    </select>
                </div>

                <div class="input-group input-group-sm">
                    <span class="input-group-text">Next Month</span>
                    <select name="Next_Month" class="form-select form-select-sm">
                        <!-- options -->
                    </select>
                </div>

                <div class="input-group input-group-sm">
                    <span class="input-group-text">Upcoming DO</span>
                    <select name="upcomingDO" class="form-select form-select-sm">
                        <!-- options -->
                    </select>
                </div>

                <div class="input-group input-group-sm">
                    <span class="input-group-text">Additional PO</span>
                    <select name="addPO" class="form-select form-select-sm">
                        <!-- options -->
                    </select>
                </div>

                <input id="lookupBtn" type="button" class="btn btn-success btn-sm"
                       style="width:100px;" value="Get" />
            </div>
        </form>
    </div>
</div>
```

### 변경 포인트 요약

| 기존 | 변경 | 이유 |
|---|---|---|
| `float-left` + `float-right` | `justify-content-between` | 양끝 배치 |
| `float-left ml-2 mt-2` 반복 | `d-flex gap-2` | 간격을 gap 하나로 |
| `container-fluid` 중첩 | 제거 | 불필요한 박스 정리 |
| `mt-1` on h2 | `mb-0` | 세로 정렬 맞추기 |

---

## 10. 이모티콘 경고 문구 추가

날짜 입력 옆에 참고/경고 문구가 필요할 때 사용해요.

```html
<div style="background-color:#fff3cd; 
            border:1px solid #ffc107; 
            border-radius:4px; 
            padding:5px 10px; 
            font-size:11px; 
            line-height:1.4; 
            max-width:300px;">
    ⚠️ Date prior to 10/14/2022 may be inaccurate. 
    Please refer to data from <strong>10/14/2022</strong> onward.
</div>
```

> 💡 `max-width` 값을 조절하면 줄바꿈 위치가 달라져요!
> - 좁게 → 줄 많아짐
> - 넓게 → 한줄에 길게

---

## ✅ 자주하는 실수 체크리스트

- [ ] `id` 중복 사용 안했는지 (페이지에 같은 id 두개 쓰면 JS가 첫번째만 인식)
- [ ] `LookupZone` 번호 순서 맞는지 (빠진 번호 없는지)
- [ ] 안쓰는 주석처리 코드 정리했는지
- [ ] `float` 대신 `d-flex` 사용했는지

---

*last updated: 2026-02*

