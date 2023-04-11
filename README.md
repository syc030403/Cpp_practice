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
