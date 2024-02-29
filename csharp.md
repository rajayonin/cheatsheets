# rajayonin's C# cheatsheet

## General notions
- Compiled
- Case-senstitive (`stuff` != `Stuff`)
- Whitespace is ignored (except special cases)
- End instructions with `;`
- Code blocks with `{}` (for one-line code blocks it's not needed).



## Variables
```csharp
type variable = <literal>;
```

- Can be declared and not initialized (must be initialized to be used).
- Can't be re-declared.
- A variable's scope is the code block of its declaration.
- Use `var` instead of the type for implicit initialization:
    ```csharp
    var variable = <literal>;
    ```
- Can declare several variables of the same type in one line: `type var1, var2;`
- Must begin with letter, can only contain alphanumeric characters and the underscore character.
- Can't be C# keywords.
- Make a variable a constant with `const`.



## Types
Check the type of an object with `.GetType()`.

### Value types
Reference directly to their data, stored in the stack.  
Disposed of immediately after a .NET program completes and closes.

- **Integral types:**
    - `sbyte`: Signed 8-bit integer.
    - `byte`: Unsigned 8-bit integer.
    - `short`: Signed 16-bit integer.
    - `ushort`: Unsigned 16-bit integer.
    - `int`: Signed 32-bit integer.
    - `uint`: Unsigned 32-bit integer.
    - `long`: Signed 64-bit integer.
    - `ulong`: Unsigned 64-bit integer.
- **Floating-point types:**
    - `float`: IEEE 754 Single precision (32-bit).
    - `double`: IEEE 754 Double precision (64-bit).
    - `decimal`: (Preffered type) IEEE 754 Quadruple precision (128-bit).
- **Chars -** `char`: Unicode chars.
- **Boolean -** `bool`: Good ol' booleans.

### Reference types
Store a reference to their data, which is stored in the heap.  
New instances are created using the `new` operator.
- Strings - `string` (see [Strings](#strings))
- Arrays - `array` (see [Arrays](#arrays))
- Classes - `class` (see [Classes](#classes))



## Literals
- `int`: `69`
- `string`: `"caca"`
- `char`: `'a'`
- `float`: `4.20f`
- `double`: `4.20`
- `decimal`: `4.20m` (can avoid the leading `0`)
- `bool`: `true` / `false`



## Data conversions
- Allows "safe" implicit conversions, e.g. `decimal` to `int` and viceversa.
- **Casting -** `(type)`: Truncates (narrows). Can't be used with strings.
- **Parsing -** `<type>.Parse(<value>)` (if `null` throws `ArgumentNullException`)
    - `TryParse(value, out result)` returns `bool` instead of raising an exception.
- **Converting -** `Convert.To<type>(<value>)`: If `null` sets to default, rounds.
    - `Convert.ToInt32()`
    - `Convert.ToDecimal()`
    - `Convert.ToBoolean()`
- **Converting to string -** `.ToString()`

### Overflow checking
When performing calculations that assign the value of one integral type to another integral type, the result depends on the overflow-checking context.
- In a checked context (inside `checked` block) the conversion succeeds if the source value is within the range of the destination type.
    - Otherwise, an `OverflowException` is thrown.
    ```csharp
    checked {
        <integral_operations>
    }
    ```
- In an unchecked context, the conversion always succeeds, and proceeds as follows:
    - If the source type is larger than the destination type, the source value is truncated by discarding its most significant bits.
    - If the source type is smaller than the destination type, then the source value is either sign-extended (if source type is signed) or zero-extended (if source type is signed).


## Operators
- **Addition -** `+` (numerical types)
- **Subtraction -** `-` (numerical types)
- **String concatenation -** `+` (casts other types into `string`)
- **Product -** `*` (numerical types)
- **Quotient -** `/` (numerical types): Integer by default, except at least one of the operands (and target variable) is floating point.
- **Remainder -** `%` (numerical types)
- **Exponent -** `**` (numerical types)
- **Increment/Decrement -** `++` / `--` (both post and pre)
- **Assignment -** `=`
- **Compound assignment -** `+=` / `-=` / `*=` / `/=`
- **Logical operations -** `==` / `!=` / `>` / `<` / `>=` / `<=` / `&&` / `||` / `!` (return `bool`)
    - It also supports `|` and `&`, which forces to check both sides, unlike their "doubled up" counterparts, which only check the rhs condition if necessary.
- **Tertiary operator -** `<expression> ? <true> : <false>;` (returns whatever type applies)
- **Bitwise operatos -** `~` (NOT) / `<<` (lshift) / `>>` (rshift) / `>>>` (unsigned rshift) / `&` (AND) / `|` (OR) / `^` (XOR) (integer types and `char`)

### Order of operations
1. **P**arentheses (whatever is inside the parenthesis is performed first)
2. **E**xponents
3. **M**ultiplication and **D**ivision (from left to right)
4. **A**ddition and **S**ubtraction (from left to right)



## Strings
- Inmutable (can only be altered (overwritten) with a new value).
- Array of `char`s.

### String methods

- `.Contains(substring)`: Check if the substring exists.
- `.StartsWith(char)`: Check if the string starts with that character.
- `.EndsWith(char)`: Check if the string ends with that character.
- `.ToUpper()`: Converts characters to uppercase.
- `.ToLower()`: Converts characters to lowercase.
- `.Trim()`: Eliminates leading and trailing whitespace.
- `.ToCharArray()`: Transforms the string into a char array
    - The best way to reverse a string is to convert it into a `char` array, reverse it, and convert it back to string:
        ```csharp
        char[] valueArray = value.ToCharArray();
        Array.Reverse(valueArray);
        value = new string(valueArray);
        ```
- `.Split(delimeter)`: Splits the string into a string array by using the `char` delimiter.
- `.IndexOf(char)`: Returns the index of the first instance of the character.
    - Use `.IndexOf(char, start)` to start searching at `start`.
- `.LastIndexOf(char)`: Returns the index of the last instance of the character.
    - Use `.LastIndexOf(char, start)` to start searching at `start`.
- `.IndexOfAny(char_array)`: Returns the index of the first instance of any of the characters in the `char` array.
    - Use `.IndexOfAny(char, start)` to start searching at `start`.
- `.Substring(start, length)`: Returns a substring starting at `start` of length `length`.
- `.Insert()`
- `.Remove(start, count)`: Returns a substring removing `count` characters starting from `start`.
- `.Replace(string, replace_string)`: Returns a substring replacing all ocurrences of `string` with `replace_string`.

### String functions

- `String.Join(delimiter, array)`: Joins the elements of a string array into a `string`, including the `string` delimeter in between elements.



## Arrays

- Homogeneous (all elements must be from the same type).
- Static (fixed size).
- Ordered, start at index `0`.
- **Declaration:** 
    ```csharp
    type[] array = new type[<size>];
    ```
- **One-line declaration & initialization:** 
    ```csharp
    type[] array = {<value0>, <...>};
    ```
- **Indexation and assignation of values:**
    ```csharp
    array[<index>] = <stuff>;
    ```
- **Multidimensional arrays -** `type[, ...]` (one `,` per extra dimension)
    - Address them with `array[index0, index1, ...]`.

#### Array methods
- `.Length`: Returns the size of the array.
- `.Sort()`: Sorts the array.
- `.Reverse()`: Reverses the array.

#### Array functions
- `Array.Clear(array, start, end)`: Removes elements from the array in the range $[\texttt{start}, \texttt{end})$, and replaces them by `null`.
- `Array.Resize(ref array, size)`: Resizes the array to the specified size. 
    - New elements are added at the end of array, and are set to `null`.
    - Removes elements from the end of the array.



## Flow control

- **Conditional branching -** `if`-`else if`-`else`
    ```csharp
    if (expression) {
        <if block>
    }
    else if (expression) {
        <else if block>
    }
    else {
        <else block>
    }
    ```
- **Matching -** `switch`-`case`
    ```csharp
    switch (variable) {
        case <match>:
            <code>
            break;  // to stop evaluating other cases
        <...>
        default:
            <code>
            break;
    }
    ```
- **Unconditional branching -** `goto`
    ```csharp
    goto Label;
    ```

    ```csharp
    Label:
        <...>
    ```



## Loops

- **Conditional (evaluate before execution)-** `while`
    ```csharp
    while (<condition>) {
        <stuff>
    }
    ```
- **Conditional (evaluate after execution)-** `do`-`while`
    ```csharp
    do {
        <stuff>
    } while (<condition>);
    ```
- **Structured -** `for`
    ```csharp
    for (<initialization>; <condition>; <update>) {
        <stuff>
    }
    ```
- **Iterative -** `foreach`
    ```csharp
    foreach (type iterator in iterable) {
        <stuff>
    }
    ```

### Interruptions
- `break;`: Exits the loop.
- `continue;`: Ends the current iteration and starts the next one.



## Functions
- Can be declared without defining the code block.
- Can be overloaded.
- **Declaration & definition:**
    ```csharp
    return_type function_name([param_type param,...]) {
        <...>

        return value;
    }
    ```
- **Use:** `return_type return_value = function_name(<arguments>);`

Remember that the return type can be `void` (no return argument).

### Parameters
- **Pass by value:** Containe the value.
- **Pass by reference:** Contain the address of the value.
    - `ref <param>` forces to pass the reference.
    - `out <param>` forces changes in the variable affect outside the function.
- **Optional parameters -** `param_type param = value`: Parameters with default values.
    - Must appear after all required parameters.
    - When passing arguments, you can choose to specify them by naming: `function_name(param: value);`



## Exceptions
- Objects of the `System.Exception` class.
    - `.Message`: Message of the exception.
    - `.StackTrace`: Stack trace of the exception (execution path until exception).
- Throw exceptions with:
    ```csharp
    throw new ExceptionType();
    ```
    - In order to customize the exception message, use `ExceptionType(msg)`.


### Compiler-generated exceptions
`Exception` subclasses.

- `ArrayTypeMismatchException`: Thrown when an array can't store a given element because the actual type of the element is incompatible with the actual type of the array.
- `DivideByZeroException`: Thrown when an attempt is made to divide an integral value by zero.
- `FormatException`: Thrown when the format of an argument is invalid.
- `IndexOutOfRangeException`: Thrown when an attempt is made to index an array when the index is less than zero or outside the bounds of the array.
- `InvalidCastException`: Thrown when an explicit conversion from a base type to an interface or to a derived type fails at runtime.
- `NullReferenceException`: Thrown when an attempt is made to reference an object whose value is null.
- `OverflowException`: Thrown when an arithmetic operation in a checked context overflows.

### Exception handling
```csharp
try {
    <try_block>
}
catch {
    <exception_handling>
}
finally {
    <final_block>
}
```
- After a `try` block you must write either a `catch` or a `finally` block (but both are not strictly needed at the same time).
- When an exception is raised inside a `try` block, the `catch` clauses associated with the `try` statement are considered in order. If the `catch` clauses are unable to handle the exception, the method that called the current method is searched.
- You can choose to catch an specific exception and store it in a variable with `catch (<exception_type> <variable>)`.
- In order to handle multiple exceptions, use several `catch` blocks.
- Re-throw the same exception with `throw;`.


## Classes

- Create an instance of a class:
    ```csharp
    Class instance = new Class();
    ```
- 

### Methods
- Can be overloaded.



## I/O

### Print to console
- Two different versions:
    - `Console.Write(msg)`: No newline appended.
    - `Console.WriteLine(msg)`: Newline appended.

    Being `msg` a `string` (other types are automatically casted into `string`).

- You can use the usual escape sequences (`\n`, `\t`, etc.).  
  Escape them with `\`, e.g.: `\"` to output `"`, `\\` to output `\`.  
  Also allows unicode escape characters (`\u1234`).
- **Verbatim literals** (`@""`) allow to output the text as is, with no escape sequences, and keeping whitespaces and newlines. E.g.:
    ```csharp
    @"    c:\source\repos    
        (this is where your code goes)"
    ```
    Escape double-quotes with other double-quotes: `@" "" "`.
- **String interpolation** allows to format strings:  `$"whatever {variable}"`.
    <!--
    - You can format the strings to better display the information with `{<value>:<format>}`. The specific formatting depends on Windows country configuration
        - Currency - `:C`
        - Numbers - `:N` 
        - Percentages - `:P`
        - Use `:<format><precision>` to specify the number of precision digits.
    - Also padding: https://learn.microsoft.com/en-us/training/modules/csharp-format-strings/4-exercise-string-methods-padding
    -->

### Read from console
```csharp
Console.ReadLine();
```
- Always returns a string.
- Waits for a newline character to stop reading.



## Comments
- **Single-line:**
    ```csharp
    // my comment
    ```
- **Multi-line:**
    ```csharp
    /* 
    my long
    comment
    */
    ```



## Compilation and execution

- C# project creation (current directory, console application):
    ```powershell
    dotnet new console
    ```
- Compilation:
    ```powershell
    dotnet build
    ```
- Execution:
    ```powershell
    dotnet run
    ```



## More information
- These are my personal notes from [Microsoft's Learn C# Official Collection](https://learn.microsoft.com/en-us/users/dotnet/collections/yz26f8y64n7k07?WT.mc_id=dotnet-35129-website)
- [C# Documentation](https://docs.microsoft.com)


