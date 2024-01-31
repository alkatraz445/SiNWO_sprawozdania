# Ćwiczenie 3

Repozytorium z kodem źródłowym znajduje się pod adresem: [link](https://github.com/alkatraz445/SiNWO_3)

## `gcd.cpp`

```cpp
#include <iostream>

int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int main() {
    int a, b;
    std::cout << "Enter two numbers: ";
    std::cin >> a >> b;
    std::cout << "The GCD of " << a << " and " << b << " is " << gcd(a, b) << std::endl;
    return 0;
}
```

## `CMakeLists.txt`

```
cmake_minimum_required(VERSION 3.10)
project(GCD)

set(CMAKE_CXX_STANDARD 20)
set(SOURCE_FILES gcd.cpp)

add_executable(GCD ${SOURCE_FILES})
```
