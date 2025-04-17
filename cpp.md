# (WIP) rajayonin's C++ cheatsheet

## C++
Why C++:
- Modern, but old language
- Strongly typed, safe, high-performance with zero-cost abstractions.
- Portability to WASM, Python Modules.

Useful stuff:
- [C++ reference](https://en.cppreference.com): C++ Bible
    - [Compiler support](https://en.cppreference.com/w/cpp/compiler_support): allows you to see which feature from each standard is implemented in which compiler. A godsend!

### Casting
- [`static_cast<target_type>(value)`](https://en.cppreference.com/w/cpp/language/static_cast)


### Functions

- **Specifiers:** Modify the function's properties
    - [`noexcept`](https://en.cppreference.com/w/cpp/language/noexcept_spec): The function doesn't lauch exception. If it does, **shit goes down**.
    - [`[[nodiscard]]`](https://en.cppreference.com/w/cpp/language/attributes/nodiscard): You have to assign to something whatever the function returns.
    - [`inline`](https://en.cppreference.com/w/cpp/language/inline): Signals the compiler that you prefer to not deal with the overhead of a function call. Don't use with recursive functions.
    - [`constexpr`](https://en.cppreference.com/w/cpp/language/constexpr): The function results can be evaluated at compile time. Use with simple functions, without try-catch blocks.
- **Parameter passing convention:** Types of parameter passing.
    - **By value -** `type p`: It makes a copy.
    - **By constant value -** `type const p`: It makes a copy, but it can't be modified.
    - **By reference -** `type & p`: Passes a reference to the object.
    - **By constant reference -** `type const & p`: Passes a reference to the object, but it can't be modified.
    - **By movement -** `type && p`: Passes the ownership of the object to the function.

### Classes
- **Constructor**: Get executed when the object is created. Methods, same name as the class.
    - Called with its arguments with `class{ p1, p2, ...}`.
    - Initialization list `class(...) : p1{...}, p2{...}, ...`: List of constructors to be run before this constructor. Add here the constructors of the class members.  
    **IMPORTANT:** Class members don't initialize in the order that they appear, they are initialized in the order they are declared in.
- **Accesibility:**
    - `public`: Everyone can access.
        - Default in `struct`.
    - `private` Only members can access.
        - Default in `class`.
    - `protected`: Only members and children can access.
- **Specifiers:**
    - `final`: To prevent further inheritance.

#### Member functions (methods)
- **Specifiers:** Modify the function's properties
    - [`static`](https://en.cppreference.com/w/cpp/language/static): Allow for it to be called outside the class.
    - `const` (after parenthesis): Use it if you don't modify any class member.
    - `friend`: As if you define the function outside the class, you must pass a parameter for the class object. It has acces to the private members of the class.

### Enums
- Use `enum class`.


### Typedef
Don't use it, use aliases: `using new_type = old_type`.

### #define
Don't use it, use [`constexpr`](https://en.cppreference.com/w/cpp/language/static).

### Namespaces


### Templates and concepts
This is C++'s implementation of generic programming, which allows you to use the same function for different parameter types/classes. This is **not** overloading, because that requires two function definitions.

You declare a template through `template <NAME>`, and that `NAME` will represent any type defined in the template. A template only applies to the next function definition.

In order to constraint the number of types, you can use concepts, which are specified before the template type name. If no concept is specified, _all_ types will be valid.  
C++20 comes with some predefined concepts in the `<concepts>` header.

E.g. the following function allows checking if any integer number is even, allowing for all integer types (`int`, `long`, etc.).
```cpp
#include <concepts>

template <std::integral INT_T>
bool is_even(INT_T n) {
    return n % 2 == 0;
}

int two = 2;
long two_long = 2;

is_even(two);
is_even(two_long);
```

### Concepts



### Containers (data structures)
- [`std::array<type, size>`](https://en.cppreference.com/w/cpp/container/array) (`<array>`): Classic arrays, but better
- [`std::vector<type>`](https://en.cppreference.com/w/cpp/container/vector) (`<vector>`): A non-fixed size array
    - Constructor: `{ value0, ... }`
    - To append a value, use `.push_back(value)`
- [`std::map<keyType, valueType>`](https://en.cppreference.com/w/cpp/container/vector) (`<map>`): Ordered key-value pairs. Keys must be constant.
    - Constructor: `{ {key0, value0}, ... }`
    - [`[]`](https://en.cppreference.com/w/cpp/container/map/operator_at) operator will create the element if it doesn't exist. Use [`.at()`](https://en.cppreference.com/w/cpp/container/map/at) to access the element.
    - [`.contains(key)`](https://en.cppreference.com/w/cpp/container/map/contains) checks if a key exists in the map
- [`std::unordered_map<keyType, valueType>`](https://en.cppreference.com/w/cpp/container/unordered_map) (`<unordered_map>`): Unordered [`std::map`](https://en.cppreference.com/w/cpp/container/map).
- [`std::set<type>`](https://en.cppreference.com/w/cpp/container/set) (`<set>`): A collection of homogeneous values.
    - [`.insert(element)`](https://en.cppreference.com/w/cpp/container/set/insert) inserts an element.
    - [`.contains(element)`](https://en.cppreference.com/w/cpp/container/set/contains) checks if an element is inside the set.
    - [`.extract(element)`](https://en.cppreference.com/w/cpp/container/set/extract) deletes an element and returns it.
  
Most of these structures share the following methods:
- `.clear()` clears the structure.
- `.size()` returns the number of elements.


### Other structures
- [`std::tuple<type0, ...>`](https://en.cppreference.com/w/cpp/utility/tuple) (`<tuple>`): A fixed-size collection of heterogeneous (multiple type) values.
    - Use [`std::make_tuple(value0, ...)`](https://en.cppreference.com/w/cpp/utility/tuple/make_tuple), or `{value0, ...}` to create one.
    - Extremely useful to return several data from a function, as it can be unpacked:
        ```cpp
        std::tuple<int, std::string> foo() {
            return {69, "nice"};
        }

        [n, msg] = foo();
        ```
- [`std::initializer_list<type>`](https://en.cppreference.com/w/cpp/utility/initializer_list) (`<initializer_list>`): Allows for a cleaner syntax for class constructors, with arbitrarily sized lists.  
  E.g.:
  ```cpp
  class Add {
    public:
        Add(std::initializer_list<int> l): count{}, numbers {l} {
            count = 0;
            for (auto & i : l) { count += i; }
        }

        int get() { return count; }

    private:
        int count;
        std::vector<int> numbers;
  };

  Add a {1, 2, 3, 4};
  a.get();  // 10
  ```
- [`std::function<rtype(arg0_type, ...)>`](https://en.cppreference.com/w/cpp/utility/functional/function) (`<functional>`): Wrapper for a function that can be passed as an argument. If it's a member function, the first argument must be the object: `std::function<rtype(Obj &, arg0_type, ...)>`, and it must be called with.  
    E.g.:
    ```cpp
    class Foo {
        Foo(int num) : num_(num) {}
        void print_add(int i) const { std::cout << num_ + i << '\n'; }
        int num_;
    };

    std::function<void(const Foo&, int)> f_add_display = &Foo::print_add;
    const Foo foo(69);
    f_add_display(foo, 1);
    ```


### [Ranged for loops](https://en.cppreference.com/w/cpp/language/range-for)

`for (type elem : iterable) {}`
- Remember you can use `auto` for the type (you still need to put your `const` and `&` if needed).
- You can use structured bindings in order to make your life easier: `for (type [memberA, memberB, ...] : iterable) {}`.  
  Specially useful with maps. E.g.:
  ``` cpp
  std::unordered_map<std::string, std::array<int>> my_map { 
      {"A", [0, 1, 2]},
      {"B", [3, 4, 5]}
  };

  for (const auto & [key, value] : my_map) {
      std::cout << key << ": " << value << std::endl;
  }
  ```

### [Lambda expressions](https://en.cppreference.com/w/cpp/language/lambda)
Nameless functions: `[captured_variable0, ...] (param_type param0, ...) -> return_type { <body> }`
- The return type is optional
- Captured variables are variables from the local scope to be passed to the lambda function
    - They are copied by default, use `&captured_variable` to reference it.
    - Use `[&]` to capture everything, `[=]` to copy everything.
  
E.g.:

``` cpp
int x = 69;
[&x] (int y) -> std::string { return std::to_string(y + x); }
```

- Useful to map keys to functions:
    ``` cpp
    int x = 69;
    std::string add_stuff(int y) {
        return std::to_string(y + x);
    }

    using myFunction = std::function<std::string (int)>;
    const std::unordered_map<std::string, myFunction> myMap {
        {
            "+",
            [&x] (int y) {return add_stuff(y);}
        }
    };

    int y = 420;
    myMap["+"](y)
    ```


### Exceptions
[Custom C++ Exceptions for Beginners](https://peterforgacs.github.io/2017/06/25/Custom-C-Exceptions-For-Beginners/)



### Libraries (Header / source files)
You can have header-only libraries, by simply having functions defined there, but it greatly increases compilation times and forces to recompile every time the code changes without the interface changing.

- Declare functions in header file (`.hpp`), and define them in the source files (`.cpp`).  
  If you want a function to be defined only in the header, it has to be `inline`. You can also have source file ("private") inline functions.  
- For non-constant variables, declare them using `extern` in the header and assign their values in the source file.
- Classes and its constructors are defined in the header, but the methods are only declared and must be defined in the source file, adding the class namespace (`type MyClass::my_method() {...}`). Attributes can be either declared or defined in the header.
- Macros have to be defined in the header.

For any type of library, use [guards](https://www.learncpp.com/cpp-tutorial/header-guards/) on the header files (`#ifndef LIB_HPP`, `#define LIB_HPP`) to prevent double declaration.

E.g:
```cpp
// lib.hpp

#ifndef LIB_HPP
#define LIB_HPP

inline say_hello() { std::cout << "hello\n"; }
int foo(int bar);

const baz = 69;
extern int myVar;

class MyClass() {
    public:
        MyClass(float y): _y {y} { }

        int get();

    private:
        int _x = 0;
        float _y;
};

#endif
```

```cpp
// lib.cpp

int foo(int bar) {
    return bar + myVar;
}

int myVar = 0;

MyClass::get() { return _x + _y; }
```

- [Classes and header files](https://www.learncpp.com/cpp-tutorial/classes-and-header-files/)


### Modules (C++ 20)

Couldn't get them to work, support is still shit.
