# Flutter & Dart 문법
## 개요
- Dart 특징
- 객체지향
- Dart 기본 문법
- Null Safety
- Dart 기분 구문
- 그 외 특징들

## 0. 팁
아래의 예제들을 따라할 때 ```Android Studio``` 를 사용하거나 ```DartPad```(https://dartpad.dev)를 간편하게 사용할 수 있다.<br>
직접 예제를 변형하면서 테스트해보기를 권장한다.

## 1. Dart 특징
Flutter는  Dart 언어를 사용한다.<br/>
Dart는 구글에서 멀티플랫폼을 겨냥하여 내놓은 언어이다. <br/>
Dart는 동적 타입, 정접 타입 모두 이용가능하다.

### 동적 타입
컴파일 시 자료형을 정하는 것이 아닌 실행 시에 결정하는 자료형을 결정하는 것을 뜻한다.<br/>
타입을 지정하지 않고 변수만 선언하고 값을 지정해서 사용가능하다. <br/>
#### 장점
- 지켜야 할 문법이 적고 동적타입을 지원하는 대부분의 언어는 직관적이기에 러닝커브가 낮다.
- 유동적이며 빠른 개발이 가능하다.
#### 단점
- 타입 관련 에러가 나온다면 대부분 런타임 에러이기 때문에 디버깅이 어렵다. 
- 같은 이유로 유지보수 및 코드 리뷰가 어렵다.

<br/>

### 정적 타입
컴파일 시 변수의 자료형이 결정되는 것을 뜻한다. <br/>
변수 선언시 반드시 타입을 지정해주어야 한다.
#### 장점
- 타입 관련 런타임 에러가 발생할 확률이 적다.
- 다수와 협력하는 경우에 코드 리뷰가 편하며 유지보수가 용이하다.
#### 단점
- 개발 중 신경써야하는 것이 늘어나므로 번거롭고 개발 속도가 조금 느려질 수 있다.

Dart는 두 타입을 모두 지원하기 때문에 원하는 방식대로 선택하여 개발 가능하다.
하지만 규모가 큰 프로젝트일수록 정적 타입 사용을 추천한다.
<br><br>
Dart는 Flutter 기준 2.0 부터 Null Safety라는 문법이 추가되었다.(후술 예정)<br>
Dart는 객체지향을 지원하며 객체지향을 이용한 개발을 권장한다.

## 2. 객체지향
객체 지향 프로그래밍(Object-Oriented Programming, OOP)은 수많은 컴퓨터 프로그래밍의 패러다임 중 하나이다. 객체 지향 프로그래밍은 컴퓨터 프로그램을 명령어의 목록으로 보는 시각에서 벗어나 여러 개의 독립된 단위, 즉 "객체"들의 모임으로 파악하고자 하는 것이다. 각각의 객체는 서로 데이터를 주고 받고 데이터를 처리한다.<br>
간단히 말해 절차적으로 나열된 명령어가 아닌 서로 관계를 맺는 존재들을 설명하여 프로그램을 만드는 방식을 뜻한다.<br>
객체지향은 현실 세계의 방식과 매우 유사한데 이러한 개념을 컴퓨터에서 구현하기 위해서는 객체, 인스턴스, 클래스 등의 개념이 필요하다.

#### 객체
객체란 세상에 있는 물건, 대상, 생명체 등 온가지 것들을 일컫는 말이다. 현실 세계는 이러한 객체들 간의 행위, 관계에 의해 풀이된다. <br>
Ex) "뉴턴"은 "사과"를 떨어뜨렸다. "다람쥐"는 "도토리"를 먹는다. "버스"는 "의자", "바퀴", "핸들" 등으로 이루어져 있다.

#### 클래스(Class)
클래스란 프로그래밍 세계에서 객체를 구현하기 위해 존재하는 개념이다. 클래스는 객체, 인스턴스를 찍어내기 위한 설계도, 청사진이다. <br>
Ex) 아래 코드에서 Animal이라는 Class를 이용해 cat, dog와 같은 Animal 객체를 여러개 만들어 낼 수 있다.

```Dart
/* 클래스 */
class Animal {
  final String name; //프로퍼티 : 클래스를 만들 때 해당 객체의 정보를 포함하는 변수
  Animal({required this.name});

  //메소드 : 클래스가 가지는 프로퍼티 반환, 연산 등의 작용을 하는 함수
  void printName() {
    print("이 동물의 이름은 " + name);
  }
}

void main() {
  //cat : name 프로퍼티를 "냐옹이"로 가지는 Animal 인스턴스
  var cat = Animal(name: "냐옹이");
  var dog = Animal(name: "멍멍이");
  cat.printName();
  dog.printName();
}
/* 출력값 
이 동물의 이름은 냐옹이
이 동물의 이름은 멍멍이
*/

```

#### 인스턴스
인스턴스란 현실 세계의 객체를 프로그래밍 세계에서 클래스를 이용해 구현한 것. 위의 예제 코드 참고 바람.


## 3. Dart 기본 문법
대부분이 <프로그래밍과 문제해결>을 수강하였기 때문에 기본적인 문법에 대해서는 간략히 설명.

### 타입
#### 정적 타입
변수를 선언할 때 아래 예제에 있는 자료형을 미리 써주어야 한다. 예제 외에도 다양한 타입이 있다.
```Dart
void main() {
  // String : 문자 및 문자열을 저장하는 자료형
  String a = "Hello World!";
  print(a);
  // int : 정수를 저장하는 자료형
  int b = 100;
  print(b);
  // DateTime : 시간을 저장하는 타입
  DateTime c = DateTime.now();
  print(c);
  // double : 실수를 저장하는 자료형
  double d = 1 + 2.5;
  print(d);
  // bool : 참, 거짓을 표현하는 Boolean 자료형
  bool e = true;
  print(e)
}
/* 출력값
Hello World!
100
2022-04-02 21:06:39.188
3.5
true
*/
```


#### 동적 타입
```var```을 사용해서 변수를 선언하면 어떠한 값이든 집어넣을 수 있다. ```dynamic```을 이용해 List에 여러 타입이 들어갈 수 있게 할 수도 있고 함수의 반환하는 값의 자료형이 상황에 따라 다르게 할 수도 있다. 그렇기에 ```dynamic```은 ```var```와 함께 이용하는 경우가 많다.
```Dart
void main() {
  // var을 이용하여 String, int, double, DateTime 등 다양한 자료형의 값을 저장할 수 있다.
  var a = "Hello World!";
  print(a);
  var b = 100;
  print(b);
  var c = DateTime.now();
  print(c);
  var d = 1 + 2.5;
  print(d);
  print("----------------");
  // dynamic을 이용하여 한 리스트에 다양한 자료형의 값을 저장할 수 있다.
  List<dynamic> list = [1, "3", 2.5, DateTime.now()];
  //var로 dynamic List의 데이터를 받음으로서 자료형에 신경쓰기 않고 값을 받을 수 있다.
  for (var item in list) {
    print(item);
  }
}

/* 출력값
Hello World!
100
2022-04-02 20:55:19.871
3.5
----------------
1
3
2.5
2022-04-02 20:55:19.871
*/
```
<br>

#### 상수 final, const
```const```
```Dart
void main() {
  const int a = 100;
  // const로 선언하면 변수에 한 번 값을 대입하면 변경할 수 없다.
  a = 200;
}
/* 출력값 : 에러남.
Error: Can't assign to the const variable 'a'.
  a = 200;
  ^
*/
```
```final```
```Dart
void main() {
  final int a = 100;
  // const로 선언하면 변수에 한 번 값을 대입하면 변경할 수 없다.
  a = 200;
}
/* 출력값 : 에러남.
Error: Can't assign to the final variable 'a'.
  a = 200;
  ^
*/
```
```final``` vs ```const```<br>
```final```은 컴파일시에 값이 결정되는 것이 아닌 실행 중에 값이 결정된다.
```Dart
void main() {
  //아래 코드를 실행할 때 값이 결졍되어 저장된다.
  final DateTime dt = DateTime.now();
  print(dt);
}
/* 출력값
2022-04-02 21:26:18.035
*/
```
```const```는 컴파일 시 값이 결정된다.
```Dart
void main() {
  //DateTime.now()는 코드가 실행될 때에 따라 값이 달라진다. 즉 컴파일 단계에서는 해당 값이 무엇일지 알 수 없으므로 에러가 발생한다.
  final DateTime dt = DateTime.now();
  print(dt);
}
/* 출력값 : 에러남.
Error: Cannot invoke a non-'const' constructor where a const expression is expected.
  const DateTime dt = DateTime.now();
                               ^^^
*/
```
현실에 빗댄 예 : ```final```은 여행을 가기 전에 정하는게 아니라, 여행 중에 결정할 수 있다. 단 결정하고 나서는 변경 불가. 
```const```는 먹을 것을 여행을 가기 전에 미리 정한 것, 가서 딴거 먹을래라고 물어보면 안된다.
<br><br>

### 연산자

#### 산술 연산자

```Dart
void main() {
  //+,-,* 기본 연산
  print(1 + 2);
  print(1 - 0.5);
  print(2 * 3);
  // / : 나누기(double 타입 반환)
  print(3 / 2);
  // ~/ : 몫(int 타입 반환)
  print(9 ~/ 7);
  // % : 나머지 연산(int 타입 반환)
  print(9 % 5);
}
/* 출력값
3
0.5
6
1.5
1
4
*/
```
#### 증감 연산자
```Dart
void main() {
  int a = 0;
  //후위 연산, 출력하고 연산
  print(a++);
  a = 10;
  //전위 연산, 연산하고 출력
  print(++a);
}
/* 출력값
0
11
*/
```
#### 비교 연산자
```Dart
void main() {
  //같은가?
  print(1 == 1);
  //다른가?
  print(1 != 2);
  //앞이 뒤보다 큰가?
  print(1 > 2);
  //앞이 뒤보다 작거나 같은가?
  print(2 <= 3);
}
/* 출력값
true
true
false
true
*/
```
#### 논리 연산자
```Dart
void main() {
  //&& : 그리고
  print(true && false);
  print(true && true);
  print("");
  //|| : 또는
  print(true || false);
  print(false || false);
  print("");
  //== : 같다
  print(true == true);
  print(true == false);
  print("");
  //! : 부정(반대)
  print(!true);
  print(!false);
  print("");
  //!= : 다르다
  print(true != false);
}
/* 출력값
false
true

true
false

true
false

false
true

true
*/
```

### 함수
코드 묶음 단위이다. 이름과 반환형, 매개변수, 작동하는 코드를 구성 성분으로 가진다.<br>
이름 : 함수를 호출할 때 사용하는 문자열
반환형 : 해당 함수의 코드를 모두 수행하고 결과로 돌려주는 자료형

- void : 아무 것도 반환하지 않는다. 단순히 함수의 코드만을 수행할 뿐이다.
- String, int, double... : 지정한 타입의 값을 반드시 반환해주어야 한다.
- dynamic : 어떠한 자료형을 반환하든, 반환하지 않든 모두 가능하다.

매개변수 : 함수를 호출할 때 요구하는 변수<br>
코드 : 함수를 호출한 곳에서 매개변수로 받은 변수를 이용하여  해당 코드를 수행한다. 마지막에는 반드시 반환형에 해당하는 변수를 반환한다.<br>
기본적인 Dart 함수의 구조
```Dart
<반환형> <이름>(<매개변수>) {
    <코드...>
    return <반환형 자료형의 변수>;
}
```
예제1
```Dart
void main() {
  int a = 100;
  int b = 200;
  print(add(a, b));
}

int add(int a, int b) {
  var c = a + b;
  return c;
}

/* 출력값
300
*/
```
예제2
```Dart
void main() {
  var str = printAnyThing(DateTime.now());
  print(str);
  var str2 = printAnyThing(true);
  print(str2);
  var str3 = printAnyThing([1,3,"hihi",true]);
  print(str3);
}
// 어떤 타입을 매개변수로 받든, 어떤 형으로 반환하든 상관 없음.
dynamic printAnyThing(dynamic a) {
  print(a);
  return "당신이 입력한 값은 바로 "+a.toString();
}

/* 출력값
2022-04-03 00:37:38.585
당신이 입력한 값은 바로 2022-04-03 00:37:38.585
true
당신이 입력한 값은 바로 true
[1, 3, hihi, true]
당신이 입력한 값은 바로 [1, 3, hihi, true]
*/
```

### Class
Class는 상단의 객체지향 파트에서 설명한 Class와 동일하다.<br>
Class란 객체를 만들기 위한 설계도이다. 쉽게 생각하면 하나의 자료형으로 생각할 수 있으며 Class는 Class의 정보를 담는 property와 Class가 수행할 수 있는, 내부에서 수행되는 행동을 담은 method를 성분으로 가진다.<br>
#### 예제
```Dart
void main() {
  //인스턴스 생성
  Animal cat = Animal(name: "야옹이", isMale: true, age: 10);
  //메소드 호출
  cat.printInfo();
  Animal dog = Animal(name: "멍멍이", isMale: false, age: 100);
  dog.printInfo();
}

//클래스 선언
class Animal {
  final String name;
  final bool isMale;
  final int age;
  //생성자 : 처음에 Animal 인스턴스를 만들 때 필요한 정보 등을 명시한 함수
  //required인 프로퍼티를 넣어주지 않으면 에러가 발생한다.
  Animal({required this.name, required this.isMale, required this.age});

  //메소드
  void printInfo() {
    print("이 동물의 이름은 " + name + "이다.");
    if (isMale == true) {
      print("이 동물은 남자입니다.");
    } else {
      print("이 동물은 여자입니다.");
    }
    print("이 동물은 $age살입니다.");
  }
}
/* 출력값
이 동물의 이름은 야옹이이다.
이 동물은 남자입니다.
이 동물은 10살입니다.
이 동물의 이름은 멍멍이이다.
이 동물은 여자입니다.
이 동물은 100살입니다.
*/
```
#### 예제2
```Dart
void main() {
  //static으로 선언된 property는 해당 클래스의 인스턴스를 생성하지 않아도 사용할 수 있다. 또한 모든 인스턴스가 해당 클래스의 static 변수를 공유한다.
  print(Biology.korName);
  //Biology class 자체의 korName이 변경되는 것.
  Biology.korName = "컴퓨터공학";
  //static method는 앞선 메소드와 다르게 인스턴스.메소드이름으로 호출하지 않고 클래스이름.메소드로도 호출 할 수 있다. 즉 인스턴스를 필요로하지 않는다.
  Biology.printKorName();
}

class Biology{
  //static 변수
  static String korName = "생명과학";
  //static method
  static void printKorName(){
    print("이 학문의 한국어 이름은 "+korName+"이다.");
  }
}
/* 출력값
생명과학
이 학문의 한국어 이름은컴퓨터공학이다.
*/

```
static 변수 및 함수 모두 인스턴스에 의존하지 않으며 독립적이다. 오직 class 자체만을 필요로 한다.
<br><br>

## 4. Null Safety
말 그대로 Null에 대해 안전한가?라는 의미이며 Dart에 있는 독특한 문법이다. 동시에 Dart를 처음 접할 때 성가시다고 느낄 수 있는 문법이다. <br>
Dart는 변수를 선언할 때 해당 변수가 null을 가질 수 있는지 가질 수 없는지를 자료형에서 결정한다.<br>
Null Safety는 개발자가 nullable를 혼동하지 않게 하여 치명적 프로그래밍 실수를 방지한다. 개발자는 어떠한 언어를 사용하든 null 사용을 최대한 자제하여야 한다.<Br>
nullable를 런타임 중에 검사하지 않아도 되어서 처리속도가 증진된다.
### null safety 적용 이전(Flutter 2.0 이전)
```Dart
void main() {
  String str;
  print(str);
  
  str = "Hello World!";
  print(str);
}
/* 출력값
null
Hello World!
*/
```
### null safety 적용 이후
```Dart
void main() {
  String str;
  print(str);
  
  str = "Hello World!";
  print(str);
}
/* 출력값 : 에러남.
Error: Non-nullable variable 'str' must be assigned before it can be used.
  print(str);
        ^^^
*/
```
```str``` 변수가 ```Non-nullable``` 변수라고 에러를 낸다. <br>Dart는 기본적으로 자료형 뒤에 아무것도 붙이지 않으면 해당 자료형을 가진 변수는 ```null```을 가질 수 없다고 판단한다.
```Dart
void main() {
  String? str;
  print(str);
  
  str = "Hello World!";
  print(str);
}
/* 출력값 : 에러남.
null
Hello World!
*/
```
```str``` 변수의 자료형을 ```String?```으로 해줌으로서 ```null```이 들어갈 수 있도록 해주어 에러가 없어졌다.<br>
즉 타입 뒤에 ```?```를 붙여주면 해당 변수는 ```nullable```로 ```null``` 값을 가질 수 있다.<br>
그렇다면 모두 물음표를 붙여서 사용하면 되지 않느냐 하는 생각이 들 수 있다. 하지만 그렇게 한다면 다음 같은 문제가 생긴다.
- ```non-nullable```을 반환하거나 매개변수로 가지는 함수를 사용할 때 번거롭다.
- ```null```에 의한 에러에 시달리게 된다.
#### null safety 추가 설명 예제
```Dart
void main() {
  String str = printString("하하");
}

String? printString(String str){
  String temp = "It is "+ str;
  print(temp);
  return temp;
}
/* 출력값 : 에러남
Error: A value of type 'String?' can't be assigned to a variable of type 'String' because 'String?' is nullable and 'String' isn't.
  String str = printString("하하");
               ^
*/
```
```printString``` 함수는 반환값으로 ```String?```을 반환하지만 실제로는 이 값을 받는 ```str```는 ```String```형의 변수이기 때문에 해당 반환 값이 ```null```일 가능성을 가진다고 판단하여 에러를 내는 것이다.<Br> 이럴때는 해당 변수가 ```null```이 아니라고 명시하기 위해서는 변수 뒤에 ```!```를 붙이면 된다. 하지만 ```null```일 가능성이 있음에도 ```!```를 붙이게 된다면 나중에 에러를 만나게 될 수 있으니 신중히 사용하여야 한다.
```Dart
void main() {
  String str = printString("하하")!;
}

String? printString(String str){
  String temp = "It is "+ str;
  print(temp);
  return temp;
}
/* 출력값 : 에러 안남.
It is 하하
*/
```
## 6. 그 외 특징들

다음은 문법은 아니지만 권장되는 사항이다.(Coding Standard, Coding Convention 이라고 한다.)
- Dart는 소스파일, 디렉터리, 라이브러리, 패키지 이름 모두 ```lowercase_with_underscores```를 사용한다.
    - 띄어 쓰기 -> '_'
    - 모든 문자는 소문자로
    - Ex) ```main_page.dart```, ```import 'flutter_packages/flutter_screen_util'```
- Type의 경우 ```UpperCamelCase```를 사용한다.
    - 각 word의 첫자는 대문자로
    - Type에는 ```class```,```Enum``` 등을 모두 포함한 것이다.
    - Ex) ```class Animal{}```,  ```DateTime dt= DateTime();```,  ```Widget MainPageSliderMenu(){...}```
- 그 외 모든 식별자는 ```lowerCamelCase```를 사용한다.
    - 모든 word의 첫자를 대문자로 하되 가장 첫 글자는 소문자를 사용한다.
    - class의 property, 매개변수, 변수, 등 모든 것을 포함한다.
    - Ex) ```DateTime dateTime = DateTime.now();```,   ```bool isAllRight = true;```