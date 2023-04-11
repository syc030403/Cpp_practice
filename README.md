# C++을 연습하기위해 작성한 코드를 올리는 연습장
---
**2023/04/03**
---
가수 맞추기
```
#include <iostream>
#include <string>
using namespace std;

int main() {
	string song("Falling in love with you");
	string elvis("Elvis Presley");
	string singer;

	cout << song + "를 부른 가수는";
	cout << "(힌트: 첫글자는" << elvis[0] << ")?";

	getline(cin, singer);
	if (singer == elvis) {
		cout << "맞았습니다.";
	}
	else {
		cout << "틀렸습니다." + elvis + "입니다." << endl;
	}
}
```
---
**2023/04/03**
---
클래스를 활용하여 도넛과 피자의 면적구하기
```
#include <iostream>
using namespace std;

class Circle {         //클래스 선언
public:
	int radius;
	double getArea();
};

double Circle::getArea() {     //클래스 구현
	return 3.14 * radius * radius;
}

int main() {
	Circle donut;   //객체 생성
	donut.radius = 1; // 객체에 멤버함수 접근
	double area = donut.getArea();  //객체의 멤버함수 호출
	cout << "donut 면적은" << area << endl;

	Circle pizza;
	pizza.radius = 30;
	area = pizza.getArea();
	cout << "pizza 면적은" << area << endl;
}
```
제문제: main함수가 작동하도록 width와 height를 가지고 면적 계산을 할 수 있는 Rectangle 클래스를 구현해라
```
#include <iostream>
#include <string>
using namespace std;

class Rectangle {
public:
	int width;
	int height;
	int getArea();
};

int Rectangle::getArea() {
	return width * height;
}

int main() {
	Rectangle rect;
	rect.width = 3;
	rect.height = 5;
	cout << "사각형의 면적은 " << rect.getArea() << endl;
}
```
2개의 생성자를 가진 Circle 클래스 를 활용하여 도넛과 피자의 면적 구하기
```
#include <iostream>
#include <string>
using namespace std;

class Circle {
public:
	int radius;
	Circle();
	Circle(int r);
	double getArea();
};

Circle::Circle() { //Circle() 자동호출
	radius = 1;
	cout << "반지름 " << radius << "인 원 생성" << endl;
}

Circle::Circle(int r) { //Circle(int r) 자동호출 (r = 30)
	radius = r;
	cout << "반지름 " << radius << "인 원 생성" << endl;
}

double Circle::getArea() {
	return 3.14 * radius * radius;
}

int main() {
	Circle donut;
	double area = donut.getArea();
	cout << "donut 면적은" << area << endl;

	Circle pizza(30);
	area = pizza.getArea();
	cout << "pizza 면적은" << area << endl;
}
```
위임 생성자를 활용한 도넛과 피자의 면적 구하기
```
#include <iostream>
#include <string>
using namespace std;

class Circle {
public:
	int radius;
	Circle();
	Circle(int r);
	double getArea();
};

Circle::Circle() : Circle(1){}

Circle::Circle(int r) {
	radius = r;
	cout << "반지름 " << radius << "의 원 생성" << endl;
}

double Circle::getArea() {
	return 3.14 * radius * radius;
}

int main() {
	Circle donut;
	double area = donut.getArea();
	cout << "donut 면적은" << area << endl;

	Circle pizza(30);
	area = pizza.getArea();
	cout << "pizza 면적은 " << area << endl;
}
```
---
**2023.04.11**
---
멤버변수의 초기화와 위임 생성자 활용
```
#include <iostream>
using namespace std;

class Point {
	int x, y;
public:
	Point();
	Point(int a, int b);
	void show() {
		cout << "(" << x << "," << y << ")" << endl;
	}
};

Point::Point() : Point(0, 0){} // 위임 생성자
Point::Point(int a, int b) // 타겟 생성자
	: x(a), y(b){}

int main() {
	Point origin;
	Point target(10, 20);
	origin.show();
	target.show();
}
```
---
다음 main() 함수가 잘 작동하도록 Rectangle 클래스를 작성하고 프로그램을 완성하라.
Rectangle 클래스는 width와 height의 두 멤버 변수와 3 개의 생성자, 그리고 isSquare() 함수를 가진다.
---
```
#include <iostream>
using namespace std;

class Rectangle {
public:
	int width;
	int height;
	Rectangle();								// 생성자 1
	Rectangle(int w, int h);					// 생성자 2
	Rectangle(int len);							// 생성자 3
	bool isSquare();							// 멤버함수
};

Rectangle::Rectangle() {						// 생성자 1 호출
	width = height = 1;
}

Rectangle::Rectangle(int w, int h) {			// 생성자 2 호출
	width = w;
	height = h;
}

Rectangle::Rectangle(int len) {					// 생성자 3 호출
	width = height = len;
}

bool Rectangle::isSquare() {					// 정사각형이면 true를 아니면 false를 반환하는 함수
	if (width == height) {
		return true;
	}
	else {
		return false;
	}
}

int main() {
	Rectangle rect1;
	Rectangle rect2(3, 5);
	Rectangle rect3(3);
	if (rect1.isSquare()) cout << "rect1은 정사각형이다." << endl;
	if (rect2.isSquare()) cout << "rect2는 정사각형이다." << endl;
	if (rect3.isSquare()) cout << "rect3는 정사각형이다." << endl;
}
```
