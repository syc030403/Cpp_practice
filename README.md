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
