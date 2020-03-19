# 기본 연산자

C의 기본적인 연산자에 대해 배웁니다.

## 연산자

컴퓨터(computer)라는 단어는 사실 계산(compute)하는 기계라는 말입니다. [2장](../2-structure-of-computers)에서 말씀드렸듯이, 컴퓨터는 메모리와 **연산장치**로 이루어져있습니다. 이번 장에선 그 **연산장치**가 어떤 기본 연산을 할 수 있는지 소개하고자 합니다.
연산자는 연산장치에게 수학에서 연산자를 쓰는 것과 비슷한 방법으로 연산에 관련된 명령을 할 수 있는 방법입니다. 

## 대입 연산자(assignment operator)

대입 연산자는 메모리에 값을 저장하는 연산자입니다. 2장의 가짜 코드를 다시 상기해보도록 합시다.
```
load 2
load 3
add
store 1
```
여기서 `store`의 역할을 하는 것이 바로 대입 연산자입니다. 실제 C 코드를 통해 알아보도록 합시다.
```c
int main()
{
    int result;
    result = 6;
    result = 5;
}
```
이 코드가 어떤 일을 하는지 감이 오시나요? `int`는 4바이트를 차지하는 자료형이니, `result`가 메모리 공간 20번부터 23번을 차지하고 있다고 해봅시다. 초기식이 없기 때문에, `int result;` 까지는 20\~23번에 무엇이 들어있는지 알 수 없습니다. 그 다음 줄 `result = 6;`이 지나면 20\~23번엔 6이 들어있게 됩니다. 그 다음 줄 `result = 5;`가 지나면 20\~23번엔 5가 들어있게 됩니다. 그러니까 이 코드를 사람들이 사용하는 말에 가깝게 쓰면
```
프로그램이 시작했을 때,
    적당한 공간을 result라고 이름 짓습니다.
    result라는 이름의 공간에 6을 넣습니다.
    result라는 이름의 공간에 5를 넣습니다.
```
가 되는거죠. 20,21,22,23번 각각에 6이나 5가 들어가는 것이 아니라는 것에 주의해주세요. [4장](../4-types-and-variables)에서 설명했듯, int라는 자료형은 더 큰 숫자를 표현하기 위해, 4바이트의 공간을 묶어서 최대 32자리 2진수를 표현하기 위해 사용하는 자료형입니다. 즉, 20\~23번엔 00000006(16)(2진수로 32자리)이 들어있기 때문에, 네 공간 중 세 공간엔 0만 들어있고, 나머지 한 공간에 6이 들어있게 됩니다. 여러 공간을 묶어 한 숫자를 표현하는 방식에 대해서도 나중에 자세히 다룰 것입니다. 지금은 어떤 자료형은 여러 공간이 하나의 숫자를 표현하도록 한다는 사실만 기억해주세요.

앞으로 "변수가 가리키는 메모리 공간에 무엇을 대입한다"는 말을 줄여서 "변수에 무엇을 대입한다"라고 설명하겠습니다. 실제로 프로그래머들이 사용하는 표현도 "변수에 무엇을 대입하다"입니다. 변수와 메모리 공간이라는 단어를 함께 쓰는 건 제가 여러분들이 메모리라는 개념을 이해할 수 있도록 만들어낸 표현입니다.

다시 연산자로 돌아옵시다. 수학에서 `=` 라는 기호는 좌항과 우항의 값이 같다라는 것을 표현하는 기호였습니다. 하지만 C에선 우항의 `표현식(expression)`의 값을 좌항의 변수가 가리키고 있는 메모리의 공간에 저장한다는 의미입니다. 이 `=`라는 기호를 `대입 연산자`라고 부릅니다.

## 산술 연산자(arithmetic operator)

산술 연산자는 쉽게 말해 사칙연산을 수행하는 연산자입니다. C에선 다섯가지 산술 연산자를 지원하는데요, 덧셈 연산자(`+`), 뺄셈 연산자(`-`), 곱셈 연산자(`*`), 나머지 연산자(`/`), 나머지를 구하는 연산자(`%`) 다섯가지입니다. `/`가 단순히 나눗셈을 수행하는 것이 아니라, 몫을 구하는 연산자임에 주의할 필요가 있습니다. 예시를 보도록 합시다.
```c
#include <stdio.h>

int main()
{
    int a = 17, b = 6;
    int c;
    c = a + b;
    printf("a + b = %d    ", c);
    printf("a - b = %d    ", a - b);
    int d = a * b;
    printf("a * b = %d    ", d);
    printf("a / b = %d    ", a / b);
    printf("a % b = %d    ", a % b);
    int e = a * 2;
    printf("a * 2 = %d", e);
}
```
```
a + b = 23    a - b = 11    a * b = 102    a / b = 2    a % b = 5    a * 2 = 12
```
이 예제는 많은 것을 보여주는데요, 여기서 알 수 있는 것을 정리하면,

* C에서 사칙연산을 수행하는 방법에 대해 알 수 있습니다.
* `c = a + b`를 통해 대입 연산자의 우항에 단순한 값이 아니라 식을 넣을 수 있다는 것을 알 수 있습니다. 제가 지금까지 우항에 들어올 수 있는 것을 값(value)이 아니라 표현식이라고 했는데요, 바로 이런 특징을 고려한 것이었습니다.
* `int d = a * b`를 통해 변수를 선언할 때도 초기식에 값이 아니라 식을 넣을 수 있다는 것을 알 수 있습니다.
* `printf("a - b = %d", a - b)`를 통해 `printf`에도 식을 넣을 수 있다는 것을 알 수 있습니다. 이렇게 C를 비롯한 다양한 프로그래밍 언어에선 값이 들어갈 자리에 식도 집어넣을 수 있습니다.
* 자료형이라는 건 변수 뿐만 아니라 값이나 식에도 있다는 것을 알 수 있습니다.
* `int`를 사칙연산한 결과는 항상 `int`임을 알 수 있습니다.
* `int e = a * 2`를 통해 반대로 변수가 들어갈 자리에 숫자를 사용할 수 있는 경우가 있다는 것을 알 수 있습니다.

위 예제는 정수 자료형에 대해 산술 연산자를 사용한 것이었는데요, 부동소수점 자료형(`float`, `double`)에 대해선 나눗셈 연산자의 행동이 달라집니다.
```c
#include <stdio.h>

int main()
{
    double a = 17, b = 6;
    printf("a / b = %lf", a / b);
}
```
```
a / b = 2.833333
```
이렇게 몫을 구하는 것이 아니라 우리가 일반적으로 생각하는 나눗셈을 수행하는 것을 알 수 있습니다. `17/6`은 무한소수로 표현되기 때문에, `17/6`에 가까운 소수를 사용한 것도 알 수 있습니다. 그럼 나머지 연산자는 어떨까요? 다음 예제를 Visual Studio에 입력해보세요.
```c
#include <stdio.h>

int main()
{
    double a = 17, b = 6;
    printf("a % b = %lf", a % b);
}
```
`printf`안의 `a`와 `b`에 빨간 줄이 뜨는 것을 알 수 있습니다. 거기에 마우스 포인터를 올리면,
![Your first error](img/1.png "Your first error")
이렇게 "expression must have integral type", 즉 "표현식의 자료형이 정수형이어야 합니다"라는 오류 메시지를 보여줍니다. 이렇게 문법적으로 맞지 않은 C 코드를 사용하면 **에디터가** 에러 메시지와 함께 빨간 줄을 표시해주는 것을 알 수 있습니다. 주체가 에디터인 것에 주목해주세요. 여기서 Ctrl + F5를 누르면 어떻게 될까요?
![Error output](img/2.png "Error output")
이렇게 **컴파일러도** 에러 메시지와 함께 소스 코드의 어디가 문제인지 알려주는 것을 알 수 있습니다. 이번엔 주체가 컴파일러인 것에 주목해주세요. 여기서 밑에 "Error List"를 누르시면 이렇게 **에디터가** *컴파일러의* 메시지를 잘 정리해서 표시해주는 것을 알 수 있습니다.
![Message adapter result](img/3.png "Message adapter result")

여기서 컴파일러와 에디터를 철저하게 구분하는 이유가 있는데요, 소스 코드를 컴파일하는 것은 의외로 시간이 많이 걸리는 작업입니다. 소스 코드의 오류를 찾아내기 위해선 컴파일을 일부 수행해야하기 때문에, 소스 코드를 입력하고 나서 **에디터가** 오류를 표시해 줄 때까지 시간이 많이 걸릴 수 있습니다. 중간에 에디터에서 오류가 발생하게 되면 에디터가 오류를 표시해주지 않을 수도 있습니다. 프로그래밍을 배우기 시작하는 많은 분들이 "빨간 줄은 안 뜨는데 왜 오류가 나요?"라는 질문을 하시는데, 빨간 줄을 표시해주는 주체와 실제 오류인지 아닌지 확인해줄 수 있는 주체가 다르다는 것을 항상 기억해주시길 바랍니다. 빨간 줄이 없어도 컴파일러에서 오류가 나면 소스 코드에 오류가 있는 것이고, 빨간 줄이 있어도 컴파일러에서 오류가 안 나면 소스 코드에 문제가 없는 것입니다.

컴파일러의 역할을 자세히 알고 계시는 분을 위해 부가 설명을 하자면, 컴파일까지는 괜찮은데 링크 과정에서 오류가 발생하는 경우도 있습니다. 컴파일러와 링커 구분은 함수를 다루고 나서야 할 예정입니다.

## 연산자 우선순위(operator precedence)

수학에서 한 식에 여러 연산자를 섞어쓸 수 있듯이, C에서도 한 식에 여러 연산자를 사용할 수 있습니다.
```c
#include <stdio.h>

int main()
{
    printf("%d", 1 + 3 * 5);
}
```
```
16
```
수학에서 그런 것처럼, C에서도 연산자 우선순위가 적용됩니다. `*`와 `/`, `%`가 `+`나 `-` 보다 우선순위가 높습니다. 그래서 `1 + 3 * 5`는 실제로 `1 + (3 * 5)`로 번역됩니다. 우선순위에 따르지 않고 싶으면 수학에서 하는 것처럼 괄호를 사용하면 됩니다.
```c
#include <stdio.h>

int main()
{
    printf("%d", (1 + 3) * 5);
}
```
```
20
```
수학에서와 다르게, C에선 연산의 우선순위를 정하기 위해 괄호를 여러 개 사용하더라도 항상 소괄호`( )`만을 사용하여야 합니다. 예를 들면 원래 수학에서
```
7 / {(1 + 2) * 5}
```
로 표기하던 것도 `7 / ((1 + 2) * 5)` 로 써야 합니다.

## 리터럴(literal)

위에서 변수 대신에 값을 사용해도 된다는 것을 배웠습니다. 아까 부동소수점 자료형 변수 두 개와 나눗셈을 하는 예제를 봅시다.
```c
#include <stdio.h>

int main()
{
    double a = 17, b = 6;
    printf("a / b = %lf", a / b);
}
```
그럼 a / b 대신에 17 / 6을 사용해도 같은 결과가 나오겠네요.
```c
#include <stdio.h>

int main()
{
    printf("a / b = %lf", 17 / 6);
}
```
하지만 이 예제를 실제로 실행하면 같은 결과가 나오지 않습니다. 왜 그럴까요? 17과 6 위에 마우스 포인터를 올려놓아주세요.
![int literal](img/4.png "int literal")
이렇게 `17`과 `6`의 자료형이 `int`인 것을 알려주고 있습니다. 즉, 여기서 `17 / 6`은 `int`끼리의 나눗셈을 했기 때문에, 결과도 `int`가 되어, 잘못된 형식 지정자를 사용하게 된 것이 됩니다. 4장에서 변수에 대해 다룰 때 초기식이 없으면 변수에 어떤 값이 들어있는지 알 수 없다는 이야기를 한 적이 있는데요, 마찬가지로 이 경우에도 무엇이 출력될지 알 수 없습니다. 이건 C 표준에서, 잘못된 형식 지정자를 사용할 경우, printf가 어떻게 작동해야하는지 정해놓지 않았기 때문에, 컴파일러에 따라 잘 작동할 수도 있고, 그렇지 않을 수도 있기 때문입니다. 이렇게 특정 경우에 어떤 기능이 어떻게 돌아갈지 정해놓지 않은 것을 `정의되지 않은 행동(undefined behavior)` 라고 합니다. 초기식을 넣지 않았거나 값을 대입하지 않은 변수의 값을 출력하는 것도 undefined behavior의 일종입니다.

그래서 자료형이 `int`가 아니라 `double`인 숫자를 적기 위해선 소수점을 함께 적어야 합니다.
```c
#include <stdio.h>

int main()
{
    printf("a / b = %lf", 17.0 / 6.0);
}
```
```
a / b = 2.833333
```
아까 했던 것 처럼 `17.0`과 `6.0` 위에 마우스를 올리면 자료형이 `double`이 되는 것을 알 수 있습니다.

이렇게 `int`나 `double` 뿐만 아니라 다른 자료형을 가진 숫자도 만들 수 있습니다.

| 자료형 | 예시 | 설명 |
| --- | --- | --- |
| `float` | `1.0f` | 소수 뒤에 f를 붙입니다. |
| `long` | `17l` | 정수 뒤에 l을 붙입니다. |
| `long long` | `23ll` | 정수 뒤에 ll을 붙입니다. |
| `unsigned` | `39u` | 정수 뒤에 u를 붙입니다. |
| `unsigned long` | `28ul` | 정수 뒤에 ul을 붙입니다. |
| `unsigned long long` | `28ull` | 정수 뒤에 ull을 붙입니다. |

```c
#include <stdio.h>

int main()
{
    printf("%d %f %llu %lf", 20, 1.0f, 28ull, 2.5);
}
```
```
20 1.000000 28 2.500000
```

이렇게 변수에 저장되지는 않았지만 식이 들어가는 자리에 바로 넣은 값을 `리터럴`이라고 부릅니다. 지금은 숫자의 리터럴만을 다뤘지만, 나중에 다른 종류의 리터럴도 나올 예정입니다.

## 형변환 연산자(casting operator)

아까 `17`과 `6` 위에 마우스를 올렸을 때, `(int)17` 이라고 뜬 것을 보실 수 있었을 겁니다. 이 `(int)`라는 표시는 단순히 에디터에서 보여주는 것이 아니라, 유효한 C의 연산자 중 하나입니다. 형변환(型變換) 연산자라는 이름에서 알아차린 분도 계시겠지만, 형변환 연산자는 어떤 식의 자료형을 다른 자료형으로 바꿔주는 기능을 합니다. 형변환 연산자를 사용하는 방법은 어렵지 않습니다.
```
(<자료형>)<식>
```

사용 예시는 다음과 같습니다.
```c
#include <stdio.h>

int main()
{
    printf("%lf, %d", (double)17, (int)(17.0 + 8.0));
}
```
```
17.000000, 25
```
이렇게 결과가 `int`인 식은 `double`로, `double`인 식은 `int`로 변환할 수 있습니다.