# C++을 연습하기위해 작성한 코드를 올리는 연습장
---
**2023.04.11** 4장   
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
다음 main() 함수가 잘 작동하도록 Rectangle 클래스를 작성하고 프로그램을 완성하라
Rectangle 클래스는 width와 height의 두 멤버 변수와 3 개의 생성자, 그리고 isSquare() 함수를 가진다.
```
#include <iostream>
using namespace std;

class Rectangle {
public:
	int width;
	int height;
	Rectangle();					// 생성자 1
	Rectangle(int w, int h);			// 생성자 2
	Rectangle(int len);				// 생성자 3
	bool isSquare();				// 멤버함수
};

Rectangle::Rectangle() {				// 생성자 1 호출
	width = height = 1;
}

Rectangle::Rectangle(int w, int h) {			// 생성자 2 호출
	width = w;
	height = h;
}

Rectangle::Rectangle(int len) {				// 생성자 3 호출
	width = height = len;
}

bool Rectangle::isSquare() {				// 정사각형이면 true를 아니면 false를 반환하는 함수
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
---
Circle 클래스에 소멸자 작성 및 실행
```
#include <iostream>
using namespace std;

class Circle {
public:
	int radius;

	Circle();
	Circle(int r);
	~Circle();
	double getArea();
};

Circle::Circle() {
	radius = 1;
	cout << "반지름 " << radius << " 원 생성" << endl;
}

Circle::Circle(int r) {
	radius = r;
	cout << "반지름 " << radius << " 원 생성" << endl;
}

Circle::~Circle() {
	cout << "반지름 " << radius << " 원 소멸" << endl;
}

double Circle::getArea() {
	return 3.14 * radius * radius;
}

int main() {
	Circle dounut;
	Circle pizza(30);
}
```
---
지역 객체와 전역 객체의 생성과 소멸 과정
```
#include <iostream>
using namespace std;

class Circle {
public:
	int radius;
	Circle();
	Circle(int r);
	~Circle();
	double getArea();
};

Circle::Circle() {
	radius = 1;
	cout << "반지름 " << radius << " 원 생성" << endl;
}

Circle::Circle(int r) {
	radius = r;
	cout << "반지름 " << radius << " 원 생성" << endl;
}

Circle::~Circle() {
	cout << "반지름 " << radius << " 원 소멸" << endl;
}

double Circle::getArea() {
	return 3.14 * radius * radius;
}

Circle globalDonut(1000);
Circle globalPizza(2000);

void f() {
	Circle fDonut(100);
	Circle fPizza(200);
}

int main() {
	Circle mainDonut;
	Circle mainPizza(30);
	f();
}
/*
프로그램 로딩
1. globalDonut 객체 생성
2. globalPizza 객체 생성
main() 함수 시작 
3. mainDonut 객체 생성
4. mainPizza 객체 생성
f() 함수 실행
5. fDonut 객체 생성
6. fPizza 객체 생성
f() 함수 종료
-6. fPizza 객체 소멸
-5. fDonut 객체 소멸
main() 함수 종료
-4. mainPizza 객체 생성
-3. mainDonut 객체 생성
프로그램 종료
-2. globalPizza 객체 종료
-1. globalDonut 객체 종료
*/
```
---
Circle 클래스를 C++ 구조체를 이용하여 재작성
```
#include <iostream>
using namespace std;

struct StructCircle {
private:
	int radius;
public:
	StructCircle(int r) { 
		radius = r; 
	}
	double getArea();

};

double StructCircle::getArea() {
	return 3.14 * radius * radius;
}

int main() {
	StructCircle waffle(3);
	cout << "면적은 " << waffle.getArea();
}
```
---
