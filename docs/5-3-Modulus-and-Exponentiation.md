---
title: 5.3 - 求模和指数运算
alias: 5.3 - 求模和指数运算
origin: /5-3-modulus-and-exponentiation/
origin_title: "5.3 — Modulus and Exponentiation"
time: 2022-4-7
type: translation
tags:
- operator
---


## 求模运算符

求模运算符（有时候也被叫做求余运算符）可以返回整数除法结果的余数。例如 7 / 4 = 1 余 3。因此 7 % 4 = 3。又比如，25 / 7 = 3 余 4，因此 25 % 7 = 4。求模运算只能用于整数操作数。

在需要判断一个数是否能被另外一个数整除（除法结果没有余数）时求模运算非常有：如果 `x%y`结果为0，说明 `x` 可以被 `y` 整除。

```cpp
#include <iostream>

int main()
{
	std::cout << "Enter an integer: ";
	int x{};
	std::cin >> x;

	std::cout << "Enter another integer: ";
	int y{};
	std::cin >> y;

	std::cout << "The remainder is: " << x % y << '\n';

	if ((x % y) == 0)
		std::cout << x << " is evenly divisible by " << y << '\n';
	else
		std::cout << x << " is not evenly divisible by " << y << '\n';

	return 0;
}
```

程序运行结果如下：

```
Enter an integer: 6
Enter another integer: 3
The remainder is: 0
6 is evenly divisible by 3
```

```
Enter an integer: 6
Enter another integer: 4
The remainder is: 2
6 is not evenly divisible by 4
```

接下来，我们实时如果第二个数比第一个数大会怎么样：

```
Enter an integer: 2
Enter another integer: 4
The remainder is: 2
2 is not evenly divisible by 4
```

余数是 2 ，乍一看原因可能不是很明显，但其实很简单：2 / 4 是 0 (整数除法) 余数为 2。任何时候只要第二个数大于第一个，则第一个数为余数。


## 负数求模

负数也可以求模。`x % y` 的结果总是和 x 的符号一样。

执行上述程序：

```
Enter an integer: -6
Enter another integer: 4
The remainder is: -2
-6 is not evenly divisible by 4
```

```
Enter an integer: 6
Enter another integer: -4
The remainder is: 2
6 is not evenly divisible by -4
```

在上面两种例子中可以看到余数的符号总是和第一个操作符一样。

## 指数运算符去哪了?

你可能已经注意到了 `^` 运算符(通常用于表示指数运算)在 C++ 中是异或运算符 (在[O.3 -- Bit manipulation with bitwise operators and bit masks](https://www.learncpp.com/cpp-tutorial/bit-manipulation-with-bitwise-operators-and-bit-masks/) 中介绍)。C++ 并没有指数运算符。

在 C++ 中进行指数运算需要 `#include` `<cmath>` 头文件，然后使用 pow() 函数：

```cpp
#include <cmath>

double x{ std::pow(3.0, 4.0) }; // 3 to the 4th power
```


注意，参数和返回值的类型都是 double。而由于浮点数存在[[rounding-error|舍入误差]]，所以`pow()`的结果可能并不精确（即使你传入的是整数）。

如果你想进行整数指数运算，你最好自己写一个函数。下面这个函数就实现了整型的指数运算（使用了不太直观的**平方求幂**算法以提高效率）：

```cpp
#include <iostream>
#include <cstdint> // for std::int64_t
#include <cassert> // for assert

// note: exp must be non-negative
std::int64_t powint(int base, int exp)
{
	assert(exp > 0 && "powint: exp parameter has negative value");

	std::int64_t result{ 1 };
	while (exp)
	{
		if (exp & 1)
			result *= base;
		exp >>= 1;
		base *= base;
	}

	return result;
}

int main()
{
	std::cout << powint(7, 12); // 7 to the 12th power

	return 0;
}
```

结果为：

```
13841287201
```

Don’t worry if you don’t understand how this function works -- you don’t need to understand it in order to call it.

!!! warning "注意"

	In the vast majority of cases, integer exponentiation will overflow the integral type. This is likely why such a function wasn’t included in the standard library in the first place.