# yaml_syntax
yaml syntax

yaml: 기존에 주로 사용되던 포맷인 JSON의 불편함을 해소하기 위해 만들어진 superset이다.  
.yaml과 .yml 둘 다 사용 가능한 확장자이다.

website: [yaml.org](https://yaml.org/)
References: [namu.wiki/yaml](https://namu.wiki/w/YAML#toc)


```yaml
#!syntax yaml
# yaml은 주석을 지원한다!

propA: lorem ipsum # 문자열에 따옴표는 선택사항이다.

# 프로퍼티 이름에 공백이 들어가도 상관없다.
my name is: 'namu\nwiki' # 작은따옴표(')와 큰따옴표(")를 모두 지원하며, 따옴표로 문자열을 감쌀 시 \n등의 이스케이프 문자를 사용할 수 있다.
without quotes: namu\nwiki # 따옴표가 없다면 일반 문자로 취급된다. 즉 json에서는 "namu\\nwiki" 처럼 변환된다.
#colon: string:
# 주석처리한 위 예제는 파싱에러가 발생한다.
colon: "string:" # : 등의 yaml에서 사용하는 기호를 사용하려고 할 때도 따옴표가 필요하다.

# 긴 문장(개행을 포함한 문장)을 표현할 때는 >, | 를 사용한다.
# > 를 사용하면 개행, 빈줄 없이 한 문장으로 인식한다. (끝에 공백 포함)
lorem ipsum1: >
    Lorem ipsum dolor sit amet, consectetur adipiscing elit.
    Quisque dictum lorem a tempor feugiat. Cras sit amet semper mi.

    Phasellus dignissim lobortis nisl, id varius metus.
# 개행(\n)과 빈 줄(\n\n)을 모두 인식한다.
lorem ipsum2: |
    Lorem ipsum dolor sit amet, consectetur adipiscing elit.
    Quisque dictum lorem a tempor feugiat. Cras sit amet semper mi.

    Phasellus dignissim lobortis nisl, id varius metus.
# >와 |의 끝에는 +또는 -를 사용할 수 있다.
# 다만 >와 |는 각각 >+와 |+의 단축 표현이기 때문에 명시적으로 +를 쓰는 경우는 거의 없다.
# >, |의 끝에 -를 사용하면 마지막에 개행(\n)을 포함하지 않는다.
# 위 예제를 각각 >- 와 |- 로 시험해 보자.

한글: 나무위키 # 유니코드 문자를 지원한다.

number: 3 # 숫자로 변환 가능한 문자라면 숫자로 인식한다.
PI: 3.141592653 # 소수를 지원한다.
float: 123.45678e+05 # 부동소수점을 지원한다.
not number: "3" # 따옴표로 감싼다면 무조건 문자열로 인식한다.

# .을 사용해 특수한 숫자를 표현할 수 있다.
# 이 숫자들의 경우 json으로 변환시 보통 null로 변환된다.
positive infinity: .inf # INF, Inf등의 일반적인 대소문자 표현을 모두 인식한다.
negative infinity: -.inf # -를 붙이면 음의 무한대를 표현할 수 있다.
not a number: .NaN # NaN, nan, NAN등을 모두 인식한다.
quarter: .25 # 문자가 아닌 숫자가 오면 소수점으로 인식한다. 이 경우는 0.25로 평가된다.

bool: true # true, false의 json식 불리언 값을 사용 가능하다.
yet another bool: yes # 추가로 yes, no등도 사용 가능하다. YAML 1.2부터는 지원하지 않는다.
light: Off # on, off등도 사용 가능하다. YAML 1.2부터는 지원하지 않는다.
python style bool: False # True, TRUE, False, FALSE 등의 일반적인 대소문자 표현을 인식한다.
not yet bool: TruE # "TruE" 로 평가된다.

null value: null # null을 사용 가능하다.
null shorthand: ~ # ~기호는 null의 단축 표현이다.

date: 2005-12-12 # ISO시간 포맷을 사용할 수 있다.
date2: 1234-56-78T12:34:56
date3: 12:34:56 # 시각은 초로 평가된다.

# 배열의 아이템은 -(하이픈)으로 구분한다.
array:
    - apple
    - banana
    - 12345
    - a: b # array의 a라는 속성에 b가 담긴 것이 아니라, array의 아이템 중 { "a": "b" }라는 객체가 있다는 뜻이다.
json style array: ["apple", banana, 12345, a: b] # 한줄로 쓸 때는 []를 사용한다.
json style array2: [
    apple,
    banana,
    12345,
    a: b, # 마지막의 ,(trailing comma)는 선택사항이다. 단, 모든 아이템은 ,로 구분되어야 한다.
]

# 객체는 들여쓰기와 :으로 구분한다.
object:
    name: namu wiki
    type: dictionary
    primary color: # json과 마찬가지로 중첩이 가능하다.
        gradient:
            start: 0x00A495 # hex 숫자를 사용 가능하다.
            end: 0x13AD65
        wordmark: 0x614D42
        header: 0x008275
# json스타일도 사용 가능하다.
json style object: {
    name: namu wiki, # json스타일로 쓸 경우 ,가 필요하다.
    "type": "dictionary" # 마지막의 ,(trailing comma)는 선택사항이다.
}

"quoted property name": value # 키에 따옴표를 사용해도 문제는 없다. 주로 :등의 문자가 있을 때 사용한다.

a1: b # 가능하다.
a2 : b # 가능하다.
#a3:b # 불가능하다. 콜론(:)과 값 사이는 띄어쓰기가 존재해야 한다.
# 단, json과의 호환성을 위해 존재하는 json식 표기에서는 키가 따옴표로 감싸져 있다는 조건 하에 붙혀서 쓸 수 있다.
#"a4":b # 불가능하다.
json style: {"a5":b} # 가능하다.

# key1을 가진 객체, key2를 가진 객체... 각각이 배열에 하나씩 담긴 것으로 평가된다.
arr:
    - key1: value
    - key2: value
    - key3: value
    - key4: value

# key1, key2를 가진 객체와 key3, key4를 가진 객체가 각각 배열에 담긴 것으로 평가된다.
arr2:
    - key1: value
      key2: value
    - key3: value
      key4: value
    
a6: # 가능하다. 이 경우 값에는 암묵적으로 null이 들어간다.

# 위 예제에 모두 null이 들어간다면 다음과 같이 쓸 수 있다.
arr3:
    - key1:
      key2:
    - key3:
      key4:
          
# 또한 '배열 안의 객체'는 주로 다음처럼도 표기한다 (완전히 동일한 표현이지만 포맷터 설정에 따라 다르게 나올 수 있다.)
arr4:
    -
        key1:
        key2:
    - 
        key3:
        key4:

# ?로 키를 표현할 수 있다.
? key # key라는 이름의 키를 선언한다. 값은 암묵적으로 null이 들어간다.

? another key
: value # value라는 값을 할당한다. 즉 "another key": "value" 처럼 평가된다.

# 즉 위의 예제는 다음처럼 쓸 수도 있다.
arr5:
    -
        ? key1
        ? key2
    - 
        ? key3
        ? key4

deep array:
    - - - - - value # 배열은 한번에 여러번 중첩 할 수도 있다.

# yaml은 반복적인 작성을 피하기 위한 anchor라는 문법을 지원한다.
long long string: &anchor Lorem ipsum dolor sit amet, consectetur adipiscing elit.
reuse anchor: *anchor # Lorem ipsum dolor... 로 평가된다. 즉, 값을 재사용할 수 있다.

# 객체에도 사용할 수 있다.
some object: &object-anc
    key: value
    another key: another value

duplicate object: *object-anc # some object와 똑같은 내용이 들어간다.
extended object:
    <<: *object-anc # some object의 내용을 기반으로 새 오브젝트를 만든다.
    another key: updated value # 새 내용으로 덮어씌운다.
    new key: new value # 새 필드를 작성한다.
# extended object는 최종적으로 { "key": "value", "another key": "updated value", "new key": "new value" } 로 평가된다.
# 이 동작은 자바스크립트의 스프레드 문법 { ...obj, key: value } 와 유사하다.

# 배열에서도 사용할 수 있다.
original array: &arr
    - 1
    - 2

copied array: *arr # array merge(<<:)는 지원하지 않는다.

# yaml은 한 파일에 여러 문서를 작성할 수 있다.
# -(대시)문자 3개로 새로운 스트림을 시작한다.
---
a: b # 기존과 다른 문서이기 때문에 키값이 겹쳐도 상관없다.
... # .(마침표)문자 3개로 스트림을 종료한다. (선택사항이며, 대부분 ...가 없어도 문제없이 인식한다)

# 보통 한 파일에 한 문서를 넣는 경우가 많아 ---로 시작하고 ...로 끝내는 것이 가장 이상적인 방법이지만, 대부분의 경우 둘을 생략할 수 있다.

# %로 시작하는 특수한 지시자로 문서에 설명을 추가할 수 있다.
%YAML 1.2 # %YAML은 현재 문서의 yaml버전을 명시한다.
%TAG !org! tag:yaml.org,2002: # %TAG는 외부에서 가져올 태그의 prefix를 명시한다.
---
must be string: !org!str 1234 # "1234"로 평가된다.
# !!는 !<tag:yaml.org,2002:(tagname)>: 의 단축 표기이기 대문에 다음과 같이 표현도 가능하다.
also string: !!str true # "true"로 평가된다.
empty object: !<tag:yaml.org,2002:map> # 태그 선언과 단축 표기법 둘다 사용하지 않을 수 있다.
    key: value

# 태그로 문서의 자료형을 정의할 수 있다.
--- !!seq
- XML: Extensible Markup Language
- JSON: JavaScript Object Notation
- YAML: Yet Another Markup Language

# json의 superset이기 때문에, 일반적인 json표현을 그대로 사용할 수도 있다.
---
{
    "key": "value",
    "array": [
        [1, 2, 3],
        ["apple", "banana", "orange"]
    ]
}
...
# yaml식 표현과 함께 사용할 수 있다.
---
- [name, avg: 547.2]
- [&bm {? namu : wiki, empty: }]
- [~, "this is string", *bm]
- { <<: *bm, empty: !!seq [] }
...
```
​
