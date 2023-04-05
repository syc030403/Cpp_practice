# C++을 연습하기위해 작성한 코드를 올리는 연습장

2023/04/03
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
2023/04/03
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
