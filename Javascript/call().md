# call()
call(), apply() 메서드는 this 를 조작 하는 메서드로, 원하는 객체를 this 로 할당 하고 싶을 때 사용 한다.

## this 의 이해

메서드를 호출한 객체가 저장되는 this 에는 변수는 물론 함수, 브라우저의 window 객체 등이 될 수 있다.

this 는 일반적으로 메서드를 호출한 객체가 저장 된다.

1) 예제1

아래의 예제를 보면 버튼을 클릭시 click 이벤트가 실행되는데, 콜백함수에 있는 this 는 누구를 가르킬까?

이 경우에는 id='btn' 인 버튼 요소가 this 가 된다.

즉, 이벤트가 발생했을 때 이벤트를 발생 시킨 객체가 this 가 된다.

```javascript

<input type='button' id='btn'>

$('#btn').on('click', function(){
    console.log(this);
});

```

2) 예제2

아래의 예제를 보면 move() 함수에 있는 this 는 어떤 객체를 가르킬까?

move() 함수를 호출한 것은 car 객체 이므로, this 는 car 객체를 가르킨다.

```javascript

var car = {
    model : "test"
    , number : "1234"
    , move : function() {
        console.log(this);
    }
}

car.move();

```

## call() , apply()
call(), apply() 메서드의 차이는 아래와 같다.


```

fn.call('지정할 객체', '인자1', '인자2', .....);

fn.apply('지정할 객체', '배열');

```

### call() 활용
아래 예제를 보면 move() 메서드를 호출하기 위해서는 car 객체에서 호출해야 하므로 원래 this 는 car 객체 이다. 
그러나 call() 메서드를 호출할 때 window 객체를 전달 하므로 move() 함수의 this 는 window 객체 이다.

```javascript

var car = {
    model : "test"
    , number : "1234"
    , move : function(x, y) {
        console.log(x, y);
    }
}

car.move.call(window, 1, 2);

```