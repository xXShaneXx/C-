# Modern C++ Features

This document explores key modern C++ features introduced in C++11, C++14, C++17, and C++20. These features aim to make C++ code safer, more expressive, and maintainable. Below is a summary of these features with code examples.

---

## **1. Auto Type Deduction**
Automatically deduces variable types, reducing verbosity and improving maintainability.

```cpp
auto value = 42;             // Compiler deduces int
auto it = container.begin(); // Deduces iterator type
const auto& ref = someValue; // Works with const and references

// Example with complex types:
std::map<int, std::string> myMap;
auto mapIterator = myMap.find(42); // Automatically deduces std::map<int, std::string>::iterator
```

### **Benefits:**
- Reduces typing errors.
- Simplifies handling complex or frequently changing types.

---

## **2. Uniform Initialization**
Provides consistent syntax for initializing variables and prevents narrowing conversions.

```cpp
std::vector<std::string> names1 = {"John", "Mary"}; // With assignment
std::vector<std::string> names2{"John", "Mary"};    // Direct initialization

// Example with narrowing prevention:
int valid{42};    // OK
// int invalid{3.14}; // Error: narrowing conversion
```

### **Benefits:**
- Clear and consistent initialization syntax.
- Prevents narrowing conversions.

---

## **3. Structured Bindings**
Simplifies working with tuples, pairs, or structured data.

```cpp
// Instead of:
auto pair = map.insert({key, value});
if (!pair.second) { ... }

// Use:
if (auto [iter, success] = map.insert({key, value}); !success) {
    const auto& [key, val] = *iter;
    // Work with key and val directly
}

// Example with std::tuple:
std::tuple<int, double, std::string> data = {42, 3.14, "Hello"};
auto [num, decimal, text] = data; // num=42, decimal=3.14, text="Hello"
```

### **Benefits:**
- Improves readability.
- Reduces errors when accessing tuple or pair members.

---

## **4. Scoped Enums**
Provides better type safety and scope control compared to traditional enums.

```cpp
enum class Status : uint8_t {  // Specify base type to control size
    OFF,
    ON
};

Status s = Status::ON; // Must use Status::ON

// Example with switch statement:
switch (s) {
    case Status::OFF:
        std::cout << "Status is OFF\n";
        break;
    case Status::ON:
        std::cout << "Status is ON\n";
        break;
}
```

### **Benefits:**
- Avoids implicit conversions to integers.
- Keeps enums scoped, reducing naming conflicts.

---

## **5. Lambda Functions**
Simplifies function declarations and usage.

```cpp
// Simple lambda
auto add = [](int a, int b) { return a + b; };

// Lambda capturing variables
int multiplier = 10;
auto multiply = [multiplier](int x) { return x * multiplier; };

// Example with std::sort:
std::vector<int> numbers = {3, 1, 4, 1, 5};
std::sort(numbers.begin(), numbers.end(), [](int a, int b) { return a < b; });
```

### **Benefits:**
- Ideal for short functions and callbacks.
- Can capture local variables for inline use.

---

## **6. Modern Error Handling**
Uses `std::expected` (C++23) or similar constructs for more explicit error handling.

```cpp
std::expected<Config, Error> getConfig(int index) {
    if (isValid(index))
        return Config{index};
    return std::unexpected{'invalid_index'};
}

if (auto config = getConfig(5)) {
    useConfig(*config);
} else {
    handleError(config.error());
}

// Example with std::optional:
std::optional<int> divide(int a, int b) {
    if (b == 0) return std::nullopt;
    return a / b;
}

if (auto result = divide(10, 2)) {
    std::cout << "Result: " << *result << "\n";
} else {
    std::cout << "Division by zero\n";
}
```

### **Benefits:**
- Avoids exceptions for expected errors.
- Provides explicit and efficient error handling.

---

## **7. Designated Initializers**
Makes struct initialization more readable and less error-prone.

```cpp
struct Point {
    double latitude, longitude;
};

// Clear initialization:
auto wroclaw = Point{
    .latitude = 51.1,
    .longitude = 17.03
};

// Example with partial initialization:
struct Rectangle {
    int width = 10;
    int height = 20;
};

Rectangle rect{
    .width = 15 // height remains 20
};
```

### **Benefits:**
- Ensures clarity about which value initializes which field.

---

## **8. Attributes**
Adds metadata to inform the compiler and developers about code intent.

```cpp
[[nodiscard]] int getValue();                // Warn if return value is unused
[[deprecated("Use newFunc instead")]] void oldFunc(); // Warn when used
[[fallthrough]];                            // Indicates intentional fallthrough

// Example with optimization hints:
[[likely]] if (condition) {
    // Optimized for likely true condition
}
[[unlikely]] else {
    // Optimized for unlikely condition
}
```

### **Benefits:**
- Improves code safety and clarity.
- Helps avoid unintended behavior.

---

## **9. Modern Output Formatting**
Provides a more readable and type-safe way to format output (C++20).

```cpp
// Old way:
std::cout << "Hello, " << name << " age: " << age << "\n";

// Modern way:
std::print("Hello, {} age: {}\n", name, age); // Cleaner syntax

// Example with positional arguments:
std::print("{1}, {0}, {1}\n", "first", "second"); // Outputs: second, first, second
```

### **Benefits:**
- Simplifies formatting.
- Improves readability and maintainability.

---

## **10. Constexpr for Compile-Time Computation**
Enables compile-time computation to improve runtime performance.

```cpp
constexpr int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}

constexpr int result = factorial(5); // Computed at compile time

// Example with constexpr variables:
constexpr int arraySize = 10;
std::array<int, arraySize> arr; // Compile-time array size
```

### **Benefits:**
- Reduces runtime computation overhead.
- Enables optimization through compile-time evaluation.

---

### **Summary**
Modern C++ features make code:
- **More type-safe**
- **Easier to read and maintain**
- **Less prone to runtime errors**
- **More efficient through compile-time optimizations**


