---
layout: post
title: 'double과 long double의 차이점'
date: 2023-10-09
categories: [Language, C++]
lang: ko
tags: [C++, 자료형, 데이터모델]
typora-root-url: ../
---

## 서론

doube로는 WA[^1], long double로는 AC[^2]가 나오는 [문제](https://www.acmicpc.net/problem/1072) [^3]를 풀었습니다.

long double은 double과 같은 8바이트라고  **잘못** 알고 있었기 때문에 차이점을 알아봤습니다.



## 본론

long double은 컴파일러에 따라 크기가 다르고,  다음 중 한가지 방식을 따릅니다. [^4]

* IEEE-754 binary128
* IEEE-754 binary64-extended
* non-IEEE-754 extended
* IEEE-754 binary64



### MSVC(MicroSoft C++ Compiler)

Visual Studio는 MSVC 컴파일러를 사용합니다. MSVC는 double과 long double이 동일한 형식(binary64)을 사용합니다. 따라서 Visual Studio에서 컴파일 시 long double의 size는 **8바이트** 입니다.



### G++(GNU C++ Compiler)

백준 C++17은 채점 시 g++ 컴파일러를 사용합니다.[^5] g++은 C++ 언어용 컴파일러입니다. g++ win64에서의 크기는 **16바이트**(binary128), g++ win32에선 **12 바이트**[^6]입니다.



###  x87 80-bit extended precision format

x86 32비트 시스템에서 윈도우,리눅스 모두 ILP32 모델을 사용하였습니다. **x87 80-bit extended precision format**은 x86, x86-64에서 많이 사용하는 방식입니다. IEEE-754 binary-extended 형식을 따릅니다. 



#### TEST

* 테스트 코드

```cpp
#include<iostream>
using namespace std;

int main()
{
    cout << "sizeof(long double) : " << sizeof(long double) << endl;
}
```

* 실행결과 (g++ win32)

![image-20231009170302704](/images/2023-10-03-double과-long-double의-차이점/image-20231009170302704.png)

* 실행결과 (visual studio - msvc)

![image-20231009165829978](\images\2023-10-03-double과-long-double의-차이점\image-20231009165829978.png)

## 결론

double은 8 byte, long double은 컴파일러에 따라 크기가 다릅니다. (8/12/16 byte)



## 참고사항

각 플랫폼별로 데이터 모델[^7]이 다르기 때문에 long double 뿐만이 아니라 int/long/pointer 또한 실행환경에 따라서 크기가 다릅니다.

---

[^1]: Wrong Answer
[^2]: Accepted
[^3]: [1072 게임 - 문제풀이](gyowoo1113.github.io/categories/problem-solving/)
[^4]: [Fundamental types - cppreference.com](https://en.cppreference.com/w/cpp/language/types) ↩- Standard floating-point types 항목
[^5]: [언어 정보 (acmicpc.net)](https://help.acmicpc.net/language/info)
[^6]: IEEE-754 binary-extended 형식을 사용하기 때문에 long double가 12바이트로 나온다고 추측됩니다.
[^7]: 각 타입에 따른 크기가 어떻게 결정되는지를 나타냄, 프로그래밍 원리(김화수 저) - 28p
