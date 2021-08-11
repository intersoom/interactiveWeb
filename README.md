# 1. CSS 변환과 애니메이션

### 1) Transform

- transform을 사용하면 기준점을 바꿀 수 있음 (기본이 중앙임)
- 기본적인 width/ height를 조정하면 오른쪽/ 아래로만 늘어나는데 transform을 이용하면 사방으로 모두 가능
- 하드웨어 가속을 이용(GPU를 이용함)해서 → 성능이 좋음 → 굉장히 부드러움
- CSS3를 지원하는 브라우저 기준임  → 최신 기술들을 이용

```css
.box:hover{
	transform: scale(2) rotate(15deg); /*마우스 올리면 2배 커지고 15도 회전*/
	transform: skewY(-30deg); /*수직방향으로 -30만큼 뒤틀기*/
	transform: translate(30px, 10px); /*30px, 10px만큼 이동*/
	transform: translateY(-30px); /*Y축만 -30px만큼 이동*/
	transform-origin: 0% 0%; /*transform 기준이 중앙 -> 왼쪽 위 (left top)으로*/
}
```

### 2) Transition

- transition-timing-function

    - 기본값: ease (이 외: linear,,,)

    - 크롬 개발자 도구 가서 그래프 모양 누르면 원하는 transition 속도 만들 수 있음

- transition-delay

    ```css
    transition: 1s 2s;
    ```

    → 이렇게 되면, 2초 delay가 있고 실행됨

- transition은 transform뿐만 아니라 ((수치로 표현된)) width, height, background 등등 모두 적용 가능
- ((수치로 표현된)) → auto 같은 것들은 적용 안됨

### 3) Animation

- Keyframe(키프레임): 변화가 있는 지점

    → EX> 오른쪽으로 이동하다가 아래로 이동하면 오른쪽 → 아래로 바뀌는 지점

- timeline(타임라인): 0%~100% 존재 (0%는 from으로, 100%는 to로 대체 가능, 0% 생략 가능)

    → 0% == 시작점, 100% == 종료지점

    @keframes를 이용해서 키프레임 지정 → 이에 이름을 부여해서 사용하고 싶은 클래스에 적용

```css
@keyframes sample-ani {
            0% {
                transform: translate(0, 0);
            }
            50% {
                background: red;
                transform: translate(300px, 0);
            }
            100% {
                transform: translate(400px, 500px);
            }
        }
        .box {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100px;
            height: 100px;
            border: 2px solid #000;
            background: #fff000;
            animation: sample-ani 2s linear forwards 3;
        }
				.box:hover{
						animation-play-state: paused;
				}
```

- animation-iteration-count: infinite로 하면 무한 반복, 숫자로도 지정 가능
- animation-direction: alternate 사용시, 정방향 → 역방향 왔다갔다 가능, 이 외에도 reverse, alternate-reverse도 존재
- animater-fill-mode: forwards 사용시, 이동이 완료된 자리에 멈춰 있음
- animation-play-state: 애니메이션을 재생할지 정지할지 정하는 것, running/paused

- 프레임 바이 프레임 애니메이션: 일명 노가다 애니메이션, 장면 장면 별로 하나하나 모두 그려서 표현하는 것

    → 옆으로 긴 이미지를 div태그에 보이는 정도를 조정해서 애니메이션처럼 보이게 함

    → 정해진 사이즈만큼 탁탁탁 넘어가면서 보여야함

- !!요즘은 원래 쓸 사이즈보다 2배를 크게 해서 고화질 디스플레이에도 대응할 수 있도록 함!!

```css
body {
            background: #222;
        }
        @keyframes spaceship-ani {
            to {
                background-position: -2550px 0;
            }
        }
        .spaceship {
            width: 150px;
            height: 150px;
            background: url('images/sprite_spaceship.png') no-repeat 0 0 / cover;
            animation: spaceship-ani 1s infinite steps(17);
        }
```

- steps(a): a 단계만큼으로 나눠서 움직임
- gif는 알파 채널(불투명도)가 지원이 안됨 → animation으로 사용하는 것이 좋음

++ 구글에서 기념일 같은거 할 때 쓰는 기능이 이것!

# 2. CSS 3D

### 1) CSS 3D 1

- CSS 3D를 활용하면 고급스럽고 독특한 효과를 낼 수 있음
- rotateY를 활용하면 카드를 돌린듯한 효과를 낼 수 있지만, element를 감싸고 있는 3차원 공간이 필요함
- (++) rem은 html 기준이고 em은 font-size 기준 → font-size를 rem으로, radius를 em으로 두면 상대적인 사이즈를 유지 할 수 있음
- (++) vw = viewport width, vh = viewport height → 100vw/100vh는 화면 크기를 꽉 채운 것을 의미
- 3D 효과를 내고 싶을 때는 perspective(원근감)라는 속성을 px 단위로 주면 됨
- perspective: 눈에서 사물의 거리, 눈에 가까이 있을 수록 3D 효과가 극적으로 보임
    1. 눈에서 보이는 것처럼 리얼하게 3D 효과를 주고 싶으면 perspective를 감싸고 있는 div 태그에 주면 됨
    2. 모든 사물에 같은 3D 효과를 주고 싶으면 돌아가는 element의 transform에 perspective를 주면 됨

```css
.world {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 60vw;
            height: 60vh;
            background: #fff000;
            perspective: 500px;
		}
		.card {
			display: flex;
			align-items: center;
			justify-content: center;
			width: 100px;
			height: 150px;
			border-radius: 0.5em;
			font-size: 1.5rem;
			background: red;
			transform: rotateY(45deg);
			/* transform: perspective(500px) rotateY(45deg); */
		}
```

### 2) CSS 3D 2

```css
.card {
            position: relative;
            width: 100px;
            height: 150px;
            margin: 1em;
            transform: rotateY(0deg);
            transition: 1s;
            transform-style: preserve-3d;
        }

.world:hover .card {
            transform: rotateY(180deg);
        }
```

→ .card에서 ```rotateY(0deg)```를 안 해도 괜찮지만 해주는게 좋다고 함, transform rotate로 움직일 준비를 해줌

```css
<body>
    <div class="world">
      <div class="card">A</div>
      <div class="card">B</div>
      <div class="card">C</div>
    </div>
</body>
```

→ 이렇게만 두면 카드 뒷면이 안 보여서 카드 뒷면을 만들어줌

```html
<div class="world">
        <div class="card">
            <div class="card-side card-side-front">F</div>
            <div class="card-side card-side-back">B</div>
        </div>
    </div>
```

- absolute를 이용해서 앞뒷면을 포개고 부모인 .card를 이용해서 기준점을 만들어줌

    → absolute의 기준점이 부모 태그이려면 부모 태그가 static이 아닌 값이면 됨 (보통 relative로 사용)

    ```css
    .card-side {
                display: flex;
                align-items: center;
                justify-content: center;
                position: absolute;
                left: 0;
                top: 0;
                **width: 100%;
                height: 100%;
                border-radius: 0.5em;
                font-size: 1.5rem;**
                backface-visibility: hidden;
            }
    ```

    → 주황색 부분을 활용해서 앞뒷면을 포갬

- B가 위로 옴 → ```z-index: 1``` 써서 F가 위로 오게 해줌
- 문제점: 앞 뒷면을 포개도 양 쪽이 같은 면을 보고 있기 때문에 카드를 뒤집어도 B가 보이는게 아니라 아무 것도 안 보임

    → 해결책: 뒷면을 rotateY를 활용해서 뒤집어줌

```html
<div class="world">
        <div class="card">
            <div class="card-side card-side-front">F</div>
            <div class="card-side card-side-back">B</div>
        </div>
    </div>
```

- 문제점: world 안에 card가 있고 그 안에 card-side가 있기 때문에 3D 속성(perspective)을 world에 줬기 때문에 card-side에 그 효과가 안 미침

    → 해결책: card에 ```transform-style: preserve-3d;```를 주면 됨

    ```css
    transform-style: preserve-3d;
    ```

- 3D에는 앞 뒷면이 모두 존재 → 뒷면이 안 보이게 해줘야함

    ```css
    backface-visibility: hidden;
    ```

- 회전축 변경 방법:

    ```css
    transform-origin: left;
    ```

    → 이를 활용해서 문 같은 것을 만들 수 있음

    → 문이 반대쪽으로 열렸으면 좋겠으면, 각도를 변경하면 됨

### 3) CSS 3D 3

- Chrome을 제외한 다른 브라우저에서 지원하지 않는 속성들에 대한 수정이 필요함
- Safari에서는 backface-visibility를 지원은 하지만 -webkit-을 붙여주지 않으면 안됨

    → -webkit-backface-visibility라고 쳐줘야함 (표준 속성과 함께 써주기)

- 표준으로 픽스되지 않은 새로 나온 스펙들이 있으면 각 브라우저 회사 별로 자신들만의 접두어를 정해놓음

    → webkit 기반인 Safari/Chrome은 -webkit-

    → mozila 계열은 -moz-

    → microsoft 계열은 -ms-

    → opera는 -o-

- 접두어들이 있는 속성 뒤에 접두어 없는 표준 속성을 써주는 것이 좋음
- IE는 preserve 3d를 지원을 안 함

    → .card를 없애버리기 (preserve 3d 지원을 안 하니까)

    ```html
    <div class="world">
            <div class="card-side card-side-front">F</div>
            <div class="card-side card-side-back">B</div>
    </div>
    ```

    ```css
    world {
                display: flex;
                align-items: center;
                justify-content: center;
                width: 60vw;
                height: 60vh;
                background: #fff000;
                perspective: 500px;
            }
            .card-side {
                display: flex;
                align-items: center;
                justify-content: center;
                position: absolute;
                left: 50%;
                top: 50%;
                width: 100px;
                height: 150px;
                margin: -75px 0 0 -50px;
                border-radius: 0.5em;
                font-size: 1.5rem;
                -webkit-backface-visibility: hidden;
                backface-visibility: hidden;
                transition: 1s;
            }
            .card-side-front {
                z-index: 1;
                background: white;
            }
            .card-side-back {
                background: red;
                transform: rotateY(180deg);
            }
            .world:hover .card-side-front {
                transform: rotateY(180deg);
            }
            .world:hover .card-side-back {
                transform: rotateY(360deg);
            }
    ```

# 3. CSS Flex

++ 유투브 스튜디오 밀 가면 grid&flex 사용 강의 볼 수 있음

### 1) Flex & Grid

- flex box 다음에 grid 나옴 → 두가지를 적절히 섞어서 사용하는 것이 제일 좋음
- 차이점:
    1. flex box: 가로 OR 세로 둘 중에 한 쪽으로 구성
    2. grid: 격자로 구성, 가로축/세로축으로 구성
- 전체적인 레이아웃을 grid로 잡고 안에 있는 요소들을 flex로 구성
- 아직 grid는 지원하는 브라우저가 많지는 않아서 실무에서는 잘 사용하지 않음
- 그래도 grid 관련 공부는 미리미리 해두기!

### 2) Flex

- 부모가 필요함
- display 속성임
- flex 사용 전에는 높이가 content만큼만 늘어나있는데, flex를 사용하면 부모만큼 커짐

<부모에 적용시키는 것>

- flex-direction: row(기본값), column, row-reverse, column-reverse
- justify-content: 메인 축 기준으로 정렬하는 것임 / flex-start(기본값), flex-end, center, space-between(양 쪽 끝이 끝에 붙고 여백을 균일하게 나눠 가짐), space-around(양 쪽 끝에도 여백이 존재, 양 끝에는 1만큼 사이에는 2만큼 여백이 존재함)
- align-items: 축의 수직 방향으로 정렬하는 것임 / flex-start(기본값), flex-end, center

<자식에 적용시키는 것>

- flex-grow: 아무 숫자를 넣으면 부모를 가득 채움 / 숫자가 유의미해지려면 각 자식마다 다른 숫자를 넣어주면 됨 (비율에 따라서 정렬됨)

    → flex-grow는 div 전체의 비율이 아니라 여백의 비율에 따라서 정렬되는 것임 (여백 = 컨텐츠를 제외한 너비)

- flex-basis: 원래 컨텐츠가 점유하는 영역이 얼만큼인가를 설정함 / 기본값 = auto, 0 (으로 해주면 flex-grow를 사용했을 때 콘텐츠를 포함한 너비에 대한 비율에 따라서 정렬됨)
- flex(축약형)을 사용하면 자동으로 flex-basis가 0%로 들어감

    → flex: 1;로만 사용 가능

- flex-shrink

이외에도 다양한 기능이 있지만 핵심 개념은 이 정도!

# 4. JS 시작하기

### 1) 변수 선언하기

- var 대신 const랑 let 사용
- const: 값이 변하지 않는 것 (값을 변화시키려고 하면 에러남)
- let: 값이 변하는 것
- var & const/let을 섞어쓰면 안됨
- 변수의 scope(유효범위):
    1. var은 함수 단위로 함 → 함수 내에서 선언한 변수는 함수 밖에서는 사용할 수 없음
    2. const/let은 {}을 단위로 함 → 함수 / if / for 등 안에서 선언한 변수는 밖에서 사용할 수 없음

### 2) DOM Script

- Document Object Model
- 기본으로 const를 사용하고 나중에 값이 변할 것만 let을 사용하면 됨
- querySelector: 공통된 클래스를 갖고 있는 값이 여러개 있어도 첫번째 것만 가져옴
- querySelectorAll: 공통된 클래스를 갖고 있는 값을 모두 가져옴 (배열과 비슷한 형태로 가져옴)

    → all 중에 하나 가져오는 방법

    ```jsx
    ilbuniGroup = document.querySelectorAll('.ilbuni')
    console.log(ilbuniGroup[2])
    ```

    → nth-child도 사용 가능!

- HTML element에 속성 값을 넣는 방법: setAttribute('data-XXX', XXX) 활용
- data-로 시작하는 표준 커스텀 속성, data-의 형식으로 시작하면 어떤 속성이든 필요에 따라서 임의로 추가 가능

    ```jsx
    const char = document.querySelector('.characters')
    char.setAttribute('data-id', 123)
    ```

- HTML element에 속성 값을 가져오는 방법: getAttribute('data-XXX') 활용

    ```jsx
    char.getAttribute('data-id')
    ```

- XXX.innerHTML: XXX 태그 사이에 HTML 태그나 글을 추가할 수 있음
- appendChild(XXX): XXX라는 자식을 추가하는 속성
- removeChild(XXX): XXX라는 자식을 삭제하는 속성
- XXX.classList.add('YYY'): XXX에 YYY라는 클래스를 추가하는 속성 (이게 훨씬 좋기 때문에 이거 사용)
- XXX.className = 'YYY': XXX의 클래스를 YYY 하나로 바꿔버림 (기존에 있던 클래스가 날라감)
- XXX.classList.remove('YYY'): XXX에 YYY라는 클래스를 삭제하는 속성
- XXX.classList.toggle('YYY'): XXX에 YYY라는 클래스를 추가/삭제하는 속성 (토글: on&off 개념)
