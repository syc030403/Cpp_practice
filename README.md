# C++을 연습하기위해 작성한 코드를 올리는 연습장
---
**2023/04/03**
2장~3
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
**2023.04.14**
---
4-1 객체 포인터 선언 및 활용
```
#include <iostream>
using namespace std;

class Circle {
	int radius;
public:
	Circle() {
		radius = 1;
	}
	Circle(int r) {
		radius = r;
	}
	double getArea();
};


double Circle::getArea() {
	return 3.14 * radius * radius;
}

int main() {
	Circle donut;
	Circle pizza(30);

	cout << donut.getArea() << endl;

	Circle* p;
	p = &donut;

	cout << p->getArea() << endl;
	cout << (*p).getArea() << endl;

	p = &pizza;
	cout << p->getArea() << endl;
	cout << (*p).getArea() << endl;
}
```
---
4 - 2 Circle 클래스의 배열 선언 및 활용   
```
#include <iostream>
using namespace std;

class Circle {
	int radius;
public:
	Circle() {
		radius = 1;
	}
	Circle(int r) {
		radius = r;
	}
	void setRadius(int r) {
		radius = r;
	}
	double getArea();
};

double Circle::getArea() {
	return 3.14 * radius * radius;
}

int main() {
	Circle circleArray[3];

	// 배열의 각 원소 객체의 멤버 접근
	circleArray[0].setRadius(10);
	circleArray[1].setRadius(20);
	circleArray[2].setRadius(30);

	for (int i = 0; i < 3; i++) {
		cout << "Circle" << i << "의 면적은" << circleArray[i].getArea() << endl;
	}

	Circle* p;				// 객체 포인터로 배열 접근  
	p = circleArray;
	for (int i = 0; i < 3; i++) {
		cout << "Circle" << i << "의 면적은" << p->getArea() << endl;
	}
}
```
---
4 - 3 객체 배열 초기화
```
#include <iostream>
using namespace std;

class Circle {
	int radius;
public:
	Circle() {
		radius = 1;
	}
	Circle(int r) {
		radius = r;
	}
	void setRadius(int r) {
		radius = 4;
	}
	double getArea();

};

double Circle::getArea() {
	return 3.14 * radius * radius;
}

int main() {
	Circle circleArray[3] = {			// Circle 객체 배열 초기화 
		Circle(10), Circle(20), Circle()	// circleArray[0] 객체가 생성될 때, 생성자 Circle(10)
							// circleArray[1] 객체가 생성될 때, 생성자 Circle(20)
							// circleArray[2] 객체가 생성될 때, 생성자 Circle()
	};
	for (int i = 0; i < 3; i++) {
		cout << "Circle " << i << "의 면적은 " << circleArray[i].getArea() << endl;
	}
}
```
---
4 - 4 Circle 클래스의 2차원 배열 선언 및 활용
```
#include <iostream>
using namespace std;

class Circle {
	int radius;
public:
	Circle() {
		radius = 1;
	}
	Circle(int r) {
		radius = r;
	}
	void setRadius(int r) {
		radius = r;
	}
	double getArea();
};

double Circle::getArea() {
	return 3.14 * radius * radius;
}

int main() {
	Circle circles[2][3];

	circles[0][0].setRadius(1);
	circles[0][1].setRadius(2);
	circles[0][2].setRadius(3);
	circles[1][0].setRadius(4);
	circles[1][1].setRadius(5);
	circles[1][2].setRadius(6);

	/*
	Circle circles[2][3] = {{ Circle(1), Circle(2), Circle(3)},{ Circle(4), Circle(5), Circle(6) }}
	*/
	for (int i = 0; i < 2; i++) {
		for (int j = 0; j < 3; j++) {
			cout << "Circle [" << i << "," << j << "]의 면적은";
			cout << circles[i][j].getArea() << endl;
		}
	}
}
```
---
4 - 5 정수형 공간의 동적 할당 및 반환 예
```
#include <iostream>
using namespace std;

int main() {
	int* p;

	p = new int;						// int 타입 1개 할당

	if (!p) {						// p가 NULL이면, 메모리 할당 실패
		cout << "메모리를 할당할 수 없습니다.";
		return 0;
	}

	*p = 5;							// 할당 받은 정수 공간에 5 삽입
	int n = *p;
	cout << "*p = " << *p << '\n';
	cout << "n = " << n << '\n';

	delete p;						// 할당 받은 메모리 반환

}
```
---
4 - 6 정수형 배열의 동정 할당 및 반환
```
#include <iostream>
using namespace std;

int main() {
	cout << "입력할 정수의 개수는?";
	int n;
	cin >> n;
	if (n <= 0) {
		return 0;
	}
	int* p = new int[n];					// n 개의 정수 배열 동적 할당
	if (!p) {
		cout << "메모리를 할당할 수 없습니다.";
		return 0;
	}

	for (int i = 0; i < n; i++) {
		cout << i + 1 << "번째 정수: ";
		cin >> p[i];
	}

	int sum = 0;
	for (int i = 0; i < n; i++) {
		sum += p[i];
	}
	cout << "평균 = " << sum / n << endl;

	delete[] p;
}
```
---
4 - 8 Circle 객체의 동적 생성 및 반환
```
#include<iostream>
using namespace std;

class Circle {
	int radius;
public:
	Circle();
	Circle(int r);
	~Circle();
	void setRadius(int r) {
		radius = r;
	}
	double getArea() {
		return 3.14 * radius * radius;
	}
};

Circle::Circle() {
	radius = 1;
	cout << "생성자 실행 radius = " << radius << endl;
}

Circle::Circle(int r) {
	radius = r;
	cout << "생성자 실행 radius = " << radius << endl;
}

Circle::~Circle() {
	cout << "소멸자 실행 radius = " << radius << endl;
}

int main() {
	Circle* p, * q;
	p = new Circle;
	q = new Circle(30);
	cout << p->getArea() << endl << q->getArea() << endl;
	delete p;
	delete q;
}
```
---
4-9 Circle 배열의 동적 생성 및 반환
```
#include <iostream>
using namespace std;

class Circle {
	int radius;
public:
	Circle();
	Circle(int r);
	~Circle();
	void setRadius(int r) {
		radius = r;
	}
	double getArea() {
		return 3.14 * radius * radius;
	}
};

Circle::Circle() {
	radius = 1;
	cout << "생성자 실행 radius = " << radius << endl;
}

Circle::Circle(int r) {
	radius = r;
	cout << "생성자 실행 raidus = " << radius << endl;
}

Circle::~Circle() {
	cout << "소멸자 실행 radius = " << radius << endl;
}

int main() {
	Circle *pArray = new Circle[3];

	pArray[0].setRadius(10);
	pArray[1].setRadius(20);
	pArray[2].setRadius(30);

	for (int i = 0; i < 3; i++) {
		cout << pArray[i].getArea() << '\n';
	}
	Circle* p = pArray;
	for (int i = 0; i < 3; i++) {
		cout << p->getArea() << '\n';
		p++;
	}
	delete[] pArray;
}
```




