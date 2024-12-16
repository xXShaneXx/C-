C++ Standard Template Library (STL) Complete Guide
Table of Contents
Basic Containers
Associative Containers
Container Adapters
Algorithms
Iterators
Best Practices
Basic Containers
std::vector
#include <vector>

std::vector numbers{1, 2, 3, 4, 5};
numbers.push_back(6);    // Add element
numbers.pop_back();      // Remove last element
numbers[0];              // Access element

Use when: You need dynamic array with fast random accesss
std::array
#include <array>

std::array<int, 5> numbers{1, 2, 3, 4, 5};
numbers[0] = 10;         // Modify element
auto size = numbers.size();

Use when: You need fixed-size array with bounds checkings
std::list
#include <list>

std::list numbers{1, 2, 3, 4, 5};
numbers.push_front(0);   // Add to front
numbers.pop_front();     // Remove from front

Use when: You need frequent insertions/deletions at both endss
Associative Containers
std::set and std::multiset
#include <set>

std::set<int> numbers{1, 2, 3, 4, 5};
numbers.emplace(6);      // Insert element
numbers.find(3);         // Find element

Use when: You need ordered unique elements (set) or ordered elements with duplicates (multiset)s
std::map and std::multimap
#include <map>

std::map<std::string, int> prices{};
prices.emplace("bread", 20);
std::cout << prices["bread"];  // Access value

Warning: Using operator[] creates element if key doesn't exists
Algorithms
Finding and Counting
// Finding elements
auto it = std::find(vec.begin(), vec.end(), value);
auto it = std::find_if(vec.begin(), vec.end(), 
    [](int x) { return x > 3; });

// Counting elements
int count = std::count(vec.begin(), vec.end(), value);
int count = std::count_if(vec.begin(), vec.end(),
    [](int x) { return x % 2 == 0; });

Sorting and Partitioning
// Sorting
std::sort(vec.begin(), vec.end());
std::sort(vec.begin(), vec.end(), std::greater<>());

// Partitioning
std::partition(vec.begin(), vec.end(),
    [](const auto& x) { return x.underage; });

Transforming Data
// Transform elements
std::transform(input.begin(), input.end(),
    output.begin(),
    [](int x) { return x * 2; });

// Give raise example
People give_a_raise(const People& people) {
    People after_raise{};
    std::transform(
        people.begin(),
        people.end(),
        std::back_inserter(after_raise),
        [](auto p) { 
            p.salary *= 1.1; 
            return p; 
        });
    return after_raise;
}

s
Numeric Operations
#include <numeric>

// Sum of elements
int sum = std::accumulate(vec.begin(), vec.end(), 0);

// Product
int product = std::accumulate(vec.begin(), vec.end(), 1,
    std::multiplies<>());

// Custom accumulation
int sum_even = std::accumulate(vec.begin(), vec.end(), 0,
    [](int sum, int val) {
        return val % 2 == 0 ? sum + val : sum;
    });

Modifying Sequences
// Replace elements
std::replace(vec.begin(), vec.end(), old_value, new_value);

// Remove elements
vec.erase(std::remove(vec.begin(), vec.end(), value), vec.end());

// Remove_if
vec.erase(std::remove_if(vec.begin(), vec.end(),
    [](int x) { return x < 0; }), vec.end());

Iterators
Iterator Categories
Input Iterator: Read forward
Output Iterator: Write forward
Forward Iterator: Read/write forward
Bidirectional Iterator: Read/write forward/backward
Random Access Iterator: Read/write with random access s
Common Iterator Operations
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

Best Practices
1. Container Selection
Use vector as default container
Use list when frequent insertion/deletion in middle is needed
Use associative containers when key-value pairs or unique elements are needed
2. Performance Optimization
// Reserve vector capacity
std::vector<int> vec;
vec.reserve(1000);  // Prevents multiple reallocations

// Use emplace instead of push_back
vec.emplace_back(args...);  // Constructs in-place

// Use references to avoid copies
for (const auto& element : container) {
    // Process element
}

3. Memory Management
// Clear and shrink
vector.clear();
vector.shrink_to_fit();

// Swap trick to free memory
std::vector<int>().swap(vector);

4. Algorithm Usage
Prefer STL algorithms over manual loops
Use appropriate algorithm for the task
Consider algorithm complexity
Use lambda expressions for custom behavior
5. Iterator Safety
// Check iterator validity
auto it = container.begin();
if (it != container.end()) {
    // Safe to use iterator
}

// Be careful with iterator invalidation
// After modifying container, previously obtained iterators
// might become invalid

Common Pitfalls to Avoid
Using operator[] with map when checking for existence
Forgetting to check iterator validity
Not considering iterator invalidation
Using wrong container for the use case
Manual loops where STL algorithms would be better
Additional Resources
C++ Reference
STL Algorithms Complexity
C++ Core Guidelines
This comprehensive guide combines both the original contentsss and additional important STL features commonly used in professional C++ development. Use this as a reference while working with the C++ Standard Template Library. Remember to compile with modern C++ standards (C++11 or later) to access all features:
g++ -std=c++17 your_file.cpp -o your_program
