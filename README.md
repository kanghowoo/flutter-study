## Flutter 학습 기록 레포지토리
- **Wallet** (Flutter basic UI study ) - [바로가기](https://github.com/kanghowoo/flutter-study/tree/master/wallet)

<br/>


---

## Dart for Flutter (간단한 정리)

* variables

변수를 만드는 방법 2가지

1. 명시적으로 변수 타입 지정 ex) String name = '홍길동';
2. var keyword
	- 컴파일러가 변수 타입을 추론한다.
	- 관습적으로 함수나 메서드 내부에 지역 변수를 선언할 때 사용.
	- 처음 받은 데이터와 같은 타입의 데이터로 업데이트 가능. 
		ex) String name = '홍길동'; 
			name = '길동이';
	
* dynamic
	- 어떠한 변수형도 받을 수 있다.
		- 타입 체크를 하지 않고 런타임에 객체의 타입을 결정하기 때문.
	- var와 다르게, 처음 받은 데이터와 다른 타입의 데이터로 업데이트 가능.
		ex) dynamic age = '7';
			age = 7;
	- Dart 언어의 기본형이다.
		ex) var name; (데이터 선언 안한 경우) -> Type : dynamic
	- 외부에서 받는 데이터의 타입을 모르는 경우에 사용한다던지 유연하게 사용 가능.
	- 런타임에 타입이 결정 되기 때문에 타입 안정성을 보장하지 않아 애플리케이션 구동 시 타입 오류를 일으킬 수 있어 필요한 경우가 아니면 사용이 권장되지 않음.
	
* null safety
	- Dart 2.12.0 (Flutter 2.0) 이후로 모든 자료형은 기본적으로 non-nullable
		- null은 중요한 데이터 자료형이기 때문에 Dart에서 null을 없앤 것이 아니라 nullable 자료형을 제공
	- nullable 변수형은 키워드 뒤에 '?' 를 붙이면 됨.
		ex) int? var = null;
		
* final
	- runtime시에 변수할당. (compile-time에는 확인할 수 없는 값을 받을 때 사용)
		ex) final now = DateTime.now();
			final apiData = ApiService.getText();
	- 한 번 정의된 변수를 수정할 수 없게 만들 수 있는 키워드. (상수 키워드)
		ex) final name = '홍길동'; (o) (final 키워드 만으로도 타입 추론)
			name = '길동이'; (error)

* late
	- final 혹은 var 앞에 사용.
	- 초기 데이터 없이 변수선언을 가능하게 해줌. (변수의 초기화를 지연시킨다.)
		- 기본적으로 모든 자료형은 non-nullable이므로 초기화를 안하면 불가능한데 이를 가능하게 함.
	- '?' 키워드를 사용하는 것과 같다고 생각할 수 있지만 null check가 없는 상황에서 late는 null로 인한 잠재적 버그를 발생 시키지 않음.
	- API를 통한 Data Fetching의 경우에 주로 사용.
	
* const
	- compile-time에 변수 선언 (final과의 차이점)
	- 선언된 객체는 컴파일 시점에 상수 메모리에 저장되고, 객체를 참조할 때 매번 같은 곳을 참조하기 때문에 리소스 낭비를 줄인다.
	- Flutter 앱에서 사용할 상수 값에 주로 사용해 불필요한 랜더링을 줄여 성능을 높여준다.
		ex) const SizeBox(height: 30);


Data Types
Dart는 모두 class로 이루어 져 있기 때문에 자료형 역시 class이다.

1. 숫자형 (Numbers)
* int
	- num class를 상속받은 클래스
	- 소수점이 없는 숫자. 플랫폼 별로 다르지만 Dart VM을 통해 실행한 경우는 -2^63 ~ 2^63 -1 범위의 값 표현.
* double
	- num class를 상속받은 클래스
	- 실수 데이터. IEEE 754의 64bit Double 처리 방식을 사용. 링크 - https://en.wikipedia.org/wiki/Double-precision_floating-point_format
	
2. 문자형 (Strings)
* String
	- 작은따옴표, 큰 따옴표를 사용해서 선언 (두 가지 모두 가능).
	- 문자열 중간에 ${} 표현을 사용해 값을 넣을 수 있다.
		ex) String s = "중간값";
			assert("여기는 $s 입니다." == "여기는 중간값 입니다.");  -> assert는 디버깅 함수로 참/거짓 결과를 던져줌.

3. 참/거짓 (Booleans)
* bool
	- true/false 만을 객체로 가진다.
	
4. 리스트 (Lists)
* list
	- 데이터의 순서가 지정된 객체의 그룹.
	- 크기를 지정할 수도, 안할 수도 있다. 
		ex) var names = <String>[]; or String names = []; or List<String> names;
		ex) var nums = List.filled(5,0); -> 고정의 경우, 크기 변경 불가능
		
5. Maps
* Map
	- key,value의 짝을 이루는 객체
	- key와 value는 어떤 데이터 타입이던 가능.
	- key는 유일한 값, value는 중복 가능.
	
6. Sets
* Set
	- 데이터의 순서가 지정되지 않은 객체의 그룹.
	- 중복되지 않은 요소들의 집합.
	
	
---
Functions
* named parameters
	- 함수호출 시, 매개변수의 위치가 아닌 이름을 통해 값을 넘긴다. -> 순서 상관 없이 가능하다는 뜻.
	- 함수 선언 시 파라미터를 중괄호로 묶는다.
	- 파라미터에 'required'를 붙이거나 기본값을 지정해야 한다. (null-safety때문에 컴파일이 안됨)
		ex)
```
String sayHello({
  required String name,
  required int age,
  required String country,
}) {
  return "Hello, My name is $name, i'm $age years old and i'm from $country.";
}

void main() {
  print(sayHello(
    age: 30,
    country: 'seoul',
    name: 'kanghowoo',
  ));
}
```
* Optinal Positional Parameters
	- nullable 함을 명시하고, 기본값을 설정해 매개변수로 값이 넘어오지 않아도 실행되게 함.
	- 넘겨받지 않아도 되는 파라미터를 자료형과 함께 대괄호로 감싸고, nullable 표시기호 '?'와 기본값을 설정한다.
		ex) String sayHello(String name, int age, [String? country = 'Korea']) {
			return "Hello, My name is $name, i'm $age years old and i'm from $country.";
		}
	
		void main() {
			print(sayHello('kanghowoo', 30);
		}

* QQ operator
	- value1 ?? value2 형식으로 사용되며 null 병합 연산자 라고도 불림.
	- value1이 null이면 value2를 반환, value1이 null이 아니면 value1을 반환.
		ex) String? name;
			String nickname = name ?? 'kanghowoo';
			print(nickname); //kanghowoo
			name = nickname ?? 'newbee';
			print(nickname); //kanghowoo
	
* QQ assignment operator (QQ equals)
	- 변수 ??= value 형식으로 사용.
	- 변수가 null이면 value값을 할당함.
		ex) String? name;
			name ??= 'kanghowoo';
			print(name); //kanghowoo
			name ??= 'noname';
			print(name); //kanghowoo
			
* Typedefs
	- typedef 키워드로 선언.
	- 자료형을 참조하는 방법으로 type alias 라고도 불림.
		ex) typedef IntList = List<int>;
			IntList il = [1, 2, 3];
	
	- Dart 2.13 이전에는 함수를 참조하는 방법으로'만' 쓰였음. (버전 업 이후로 자료형 참조가 가능)
	- 코드 가독성, 유지보수성, 재사용성 향상을 기대할 수 있다. 아래는 재사용성의 예시
		ex) typedef IntBinaryOperation = int Function(int a, int b);

			void performOperation(IntBinaryOperation operation, int a, int b) {
			  print(operation(a, b));
			}

			void main() {
			  performOperation((a, b) => a + b, 5, 3); // 8
			  performOperation((a, b) => a - b, 5, 3); // 2
			}
			
----
Classes

* Named Parameters in Constructors
	- 클래스의 생성자에 Named Parameters를 사용한 것.
	
* Named Constructors
	- 하나의 클래스에 여러 생성자를 정의할 수 있게 하는 방법.
	- 각각의 생성자에 유니크한 이름을 부여할 수 있어 코드 가독성을 높여줌.
	- 콜론 ':' 을 붙여 초기화 선언
	- JSON 데이터로부터 객체를 초기화 한다거나 여러 상황에 따라 생성자를 사용할 수 있음.
		ex)
		class Person {
		  String name;
		  int age;

		  // 기본 생성자
		  Person(this.name, this.age);

		  // Named Constructor: JSON으로부터 초기화
		  Person.fromJson(Map<String, dynamic> json)
			  : name = json['name'],
				age = json['age'];

		  // Named Constructor: 기본값을 사용하는 초기화
		  Person.defaultPerson()
			  : name = 'kanghowoo',
				age = 30;

		  @override
		  String toString() => 'Person(name: $name, age: $age)';
		}

		void main() {
		  var p1 = Person('flutter', 25);
		  var p2 = Person.fromJson({'name': 'newbee', 'age': 1});
		  var p3 = Person.defaultPerson();

		  print(p1); // Person(name: flutter, age: 25)
		  print(p2); // Person(name: newbee, age: 1)
		  print(p3); // Person(name: kanghowoo, age: 30)
		}

* Cascade Notation ('..')
	- double dot (점 두개)로 표현
	- 객체의 여러 메서드를 호출하거나 속성을 설정할 때 객체를 반복해서 명시(참조)안하고 연속적으로 호출할 수 있도록 해줌.
		ex)
		class Rectangle {
		  double width;
		  double height;

		  @override
		  String toString() => 'Rectangle(width: $width, height: $height)';
		}

		void main() {
		  var rect = Rectangle()
			..width = 10
			..height = 20;
			
		//위 코드는 아래와 같음 
		
		/* 
		  var rect = Rectangle();
		  rect.width = 10;
		  rect.height = 20;
		*/ 

		  print(rect); // Rectangle(width: 10.0, height: 20.0)
		}
			

* Enums - 상수 집합
* Inheritance - 상속

* Abstract Classes - 추상화 클래스

* Mixins
	- 'mixin'키워드를 사용하며 정의, 메서드와 필드를 포함할 수 있다.
		- 주의할 점은 생성자가 없어야 한다는 점.
		ex) mixin Logger {
				void log(String message) {
					print('Log : $message);
				}
			}
	- 클래스를 정의할 때 'with' 키워드를 사용하여 mixin을 적용한다.
		ex) class exampleClass with Logger {
				void example() {
					log('example'); // Log : example
				}
			}
			
	- 쉼표로 여러 mixin을 사용할 수 있다.
	- Flutter의 애니메이션이나, 공통으로 동작하는 기능을 추출해 mixin을 만들고 적용한다.
		-> 코드의 재사용성을 높여준다.
		
	- 더 자세한 내용은 공식문서 : https://dart.dev/language/mixins
