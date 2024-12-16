
# C++ Standard Template Library (STL) Complete Guide

This guide serves as a comprehensive reference to the C++ Standard Template Library (STL). It covers basic containers, associative containers, container adapters, algorithms, iterators, and best practices, aimed to help you use STL effectively in your C++ projects.

## Table of Contents
- [Basic Containers](#basic-containers)
  - [std::vector](#stdvector)
  - [std::array](#stdarray)
  - [std::list](#stdlist)
- [Associative Containers](#associative-containers)
  - [std::set and std::multiset](#stdset-and-stdmultiset)
  - [std::map and std::multimap](#stdmap-and-stdmultimap)
- [Algorithms](#algorithms)
  - [Finding and Counting](#finding-and-counting)
  - [Sorting and Partitioning](#sorting-and-partitioning)
  - [Transforming Data](#transforming-data)
  - [Numeric Operations](#numeric-operations)
  - [Modifying Sequences](#modifying-sequences)
- [Iterators](#iterators)
  - [Iterator Categories](#iterator-categories)
  - [Common Iterator Operations](#common-iterator-operations)
- [Best Practices](#best-practices)
  - [Container Selection](#container-selection)
  - [Performance Optimization](#performance-optimization)
  - [Memory Management](#memory-management)
  - [Algorithm Usage](#algorithm-usage)
  - [Iterator Safety](#iterator-safety)
- [Common Pitfalls to Avoid](#common-pitfalls-to-avoid)
- [Additional Resources](#additional-resources)

---

## Basic Containers

### std::vector
```cpp
#include <vector>

std::vector<int> numbers{1, 2, 3, 4, 5};
numbers.push_back(6);    // Add element
numbers.pop_back();      // Remove last element
std::cout << numbers[0]; // Access element
```

**Use when:** You need a dynamic array with fast random access.

---

### std::array
```cpp
#include <array>

std::array<int, 5> numbers{1, 2, 3, 4, 5};
numbers[0] = 10;         // Modify element
auto size = numbers.size();
```

**Use when:** You need a fixed-size array with bounds checking.

---

### std::list
```cpp
#include <list>

std::list<int> numbers{1, 2, 3, 4, 5};
numbers.push_front(0);   // Add to front
numbers.pop_front();     // Remove from front
```

**Use when:** You need frequent insertions/deletions at both ends.

---

## Associative Containers

### std::set and std::multiset
```cpp
#include <set>

std::set<int> numbers{1, 2, 3, 4, 5};
numbers.emplace(6);      // Insert element
auto it = numbers.find(3); // Find element
```

**Use when:** You need ordered unique elements (`std::set`) or ordered elements with duplicates (`std::multiset`).

---

### std::map and std::multimap
```cpp
#include <map>

std::map<std::string, int> prices{};
prices.emplace("bread", 20);
std::cout << prices["bread"];  // Access value
```

**Warning:** Using `operator[]` creates an element if the key doesn't exist.

**Use when:** You need key-value pairs. Use `std::map` for unique keys and `std::multimap` for multiple occurrences of the same key.

---

## Algorithms

### Finding and Counting
```cpp
// Finding elements
auto it = std::find(vec.begin(), vec.end(), value);

// Counting elements
int count = std::count(vec.begin(), vec.end(), value);
```

### Sorting and Partitioning
```cpp
// Sorting
std::sort(vec.begin(), vec.end());           // Ascending
std::sort(vec.begin(), vec.end(), std::greater<>()); // Descending

// Partitioning
std::partition(vec.begin(), vec.end(), [](int x) { return x < 5; });
```

### Transforming Data
```cpp
// Transform elements
std::transform(input.begin(), input.end(), output.begin(), [](int x) { return x * 2; });
```

### Numeric Operations
```cpp
#include <numeric>

// Sum of elements
int sum = std::accumulate(vec.begin(), vec.end(), 0);

// Custom accumulation
int sum_even = std::accumulate(vec.begin(), vec.end(), 0, [](int sum, int val) {
    return val % 2 == 0 ? sum + val : sum;
});
```

### Modifying Sequences
```cpp
// Replace elements
std::replace(vec.begin(), vec.end(), old_value, new_value);

// Remove elements
vec.erase(std::remove(vec.begin(), vec.end(), value), vec.end());
```

---

## Iterators

### Iterator Categories

- **Input Iterator:** Read forward.
- **Output Iterator:** Write forward.
- **Forward Iterator:** Read/write forward.
- **Bidirectional Iterator:** Read/write forward and backward.
- **Random Access Iterator:** Read/write with random access.

### Common Iterator Operations
```cpp
// Basic iteration
for (auto it = container.begin(); it != container.end(); ++it) {
    // Use *it to access element
}

// Reverse iteration
for (auto it = container.rbegin(); it != container.rend(); ++it) {
    // Use *it to access element
}

// Range-based for loop (preferred when possible)
for (const auto& element : container) {
    // Use element directly
}
```

---

## Best Practices

### Container Selection

- Use `std::vector` as the default container.
- Use `std::list` when frequent insertions/deletions in the middle are needed.
- Use associative containers like `std::map` and `std::set` for key-value pairs or unique elements.

### Performance Optimization
```cpp
// Reserve vector capacity
std::vector<int> vec;
vec.reserve(1000);  // Prevents multiple reallocations

// Use emplace instead of push_back
vec.emplace_back(args...);  // Constructs in-place

// Use references to avoid copies
for (const auto& element : container) {
    // Process element
}
```

### Memory Management
```cpp
// Clear and shrink
vector.clear();
vector.shrink_to_fit();

// Swap trick to free memory
std::vector<int>().swap(vector);
```

### Algorithm Usage

- Prefer STL algorithms over manual loops.
- Use the appropriate algorithm for the task.
- Consider algorithm complexity.
- Use lambda expressions for custom behavior.

### Iterator Safety
```cpp
// Check iterator validity
auto it = container.begin();
if (it != container.end()) {
    // Safe to use iterator
}

// Be careful with iterator invalidation
// After modifying the container, previously obtained iterators
// might become invalid
```

---

## Common Pitfalls to Avoid

- Using `operator[]` with `std::map` without checking for existence.
- Forgetting to check iterator validity.
- Ignoring iterator invalidation after modifying the container.
- Using the wrong container for the task.
- Writing manual loops when STL algorithms would be better.

---

## Additional Resources

- [C++ Reference](https://en.cppreference.com/w/)
- [STL Algorithms Complexity](https://en.cppreference.com/w/cpp/algorithm)
- [C++ Core Guidelines](https://isocpp.github.io/)

---

### Compilation Instructions

To compile your code with modern C++ standards (C++11 or later), use the following command:

```bash
g++ -std=c++17 your_file.cpp -o your_program
```

---

This guide combines both basic and advanced concepts of the C++ STL to help you improve your coding efficiency and write more efficient, cleaner, and safer C++ code. Happy coding!
