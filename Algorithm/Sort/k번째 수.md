## 문제
~~~
배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면

array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
2에서 나온 배열의 3번째 숫자는 5입니다.
배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, 
commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.
~~~

## 제한 사항
~~~
array의 길이는 1 이상 100 이하입니다.
array의 각 원소는 1 이상 100 이하입니다.
commands의 길이는 1 이상 50 이하입니다.
commands의 각 원소는 길이가 3입니다.
~~~

## 변경전
```javascript
function solution(array, commands) {
    var answer = [];

    commands.forEach(function(value, index){
            var start = value[0]
            , end = value[1]
            , select = value[2]
            , returnArray = array.slice(0);
            
            returnArray = returnArray.slice(start - 1, end)
                                     .sort(function(a, b){
                                         return a - b;
                                     });

            answer[index] = returnArray[select-1];
    });

    return answer;
}
```
## 변경후
```javascript
function solution(array, commands) {
    var answer = [];

    commands.forEach(function(item, index){
        var temp = array.slice(item[0] - 1, item[1])
                        .sort(function(a, b){
                            return a - b;
                        });
        answer[index] = temp[item[2] - 1];
    });

    return answer;
}
```

## 2번째 케이스에서 실패 했던 이유
~~~
sort 함수는 ASCII 순서로 정렬이 됩니다. [2,3,1,10,20]이 있으면 [1,10,2,20,3] 이렇게 정렬이 되는 식입니다. 
때문에 오름차순으로 sort의 callback 함수를 작성해주어야 제대로 동작할 듯 합니당
출처) 풀이

기본 정렬 순서는 문자열의 유니코드 코드 포인트를 따릅니다
출퍼) MDN
~~~

## 유니코드(Unicode)란?
기본적으로 컴퓨터는 숫자만 처리 한다. 그래서 글자나 다른 문자에 숫자를 지정하여 저장한다.

1. 컴퓨터의 기본 저장 단위는 바이트(byte)이다.

2. 1바이트(byte)는 8비트(bit)이다.

3. 1byte에는 2의 8승에 해당하는 256개의 고유한 값을 저장할 수 있다.

4. 문자나 기호들의 집합을 컴퓨터에서 저장하거나, 통신 목적으로 사용할 경우에는 부호로 바꾸어야 한다.

이를 '문자 인코딩(encoding)' 또는 '부호화'라고 하며 부호화된 문자를 복원하는 것을 '복호화'라고 한다.

5. 모스부호도 일종의 문자 인코딩이다.

### 아스키코드(ASCII)
미국에서 정의한 표준화 부호체계 이다.

여러 가지 이유로 아스키코드는 7비트 즉, 128개의 고유한 값만 사용한다.

왜 아스키 코드는 7비트만 활용할까? 그 이유는 1비트를 통신 에러 검출을 위해 사용하기 때문이다.

통신 에러 검출을 위한 비트를 Parity Bit라고 한다.

아스키코드를 이용해 다른 언어를 표현하기에는 7비트로는 부족했다. 

그래서 8비트로 확장한 아스키 코드가 나왔다.

사람들은 이 코드를 ANSI 코드라고 부르기 시작했다.

7비트에서 8비트로 확장되었으니 사람들이 활용할 수 있는 문자는 몇 개가 더 늘어났을까?

1비트 늘어났으니 2개 더 늘어났다고 생각하면 안된다. 

~~~
2의 7승 = 128 -> 2의 8승 = 256
~~~

이렇게 되었으니 128개나 더 쓸 수 있게 되었다.

그러나, 비유럽 국가 특히 한국, 중국, 일본과 같은 문자가 많은 국가에서는 여전히 제한적이다.

(※ 우리나라의 경우 KSC5601 표준이라는 고유한 인코딩 방법으로 문자를 표현했다)

그래서 유니코드(Unicode)라는 전 세계 언어의 문자를 정의하기 위한 국제 표준 코드가 등장하게 되었다.
