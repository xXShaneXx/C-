C++ Standard Template Library (STL) Overview
The C++ Standard Template Library (STL) provides a collection of template classes and functions designed to make your code more efficient and reusable. The STL consists of four major components:

Containers – Data structures to hold collections of data.
Algorithms – Functions to manipulate data stored in containers.
Iterators – Objects used to traverse through containers.
Function Objects – Callable objects used by algorithms.
This README provides a summary and usage examples for the most commonly used components of STL.

Containers
Containers are objects that store data in different forms and provide various methods to interact with that data. Here are the most frequently used container types in STL.

1. std::vector
std::vector is a dynamic array that allows efficient resizing. It supports random access and is optimized for appending elements at the end.

Example:
cpp
Copy code
#include <vector>
#include <iostream>

std::vector<int> numbers{1, 2, 3, 4, 5};

for (auto n : numbers) {
    std::cout << n << std::endl;
}
Output:

Copy code
1
2
3
4
5
Explanation:
Characteristics: Dynamic size, fast access, and efficient at appending elements at the end.
Usage: Ideal when you need a resizable array with fast access.
2. std::deque
std::deque (double-ended queue) allows fast insertion and removal of elements at both the front and back.

Example:
cpp
Copy code
#include <deque>
#include <iostream>

std::deque<int> numbers{1, 2, 3, 4, 5};
numbers.push_front(0);

for (auto n : numbers) {
    std::cout << n << std::endl;
}
Output:

Copy code
0
1
2
3
4
5
Explanation:
Characteristics: Fast insertion and deletion from both ends.
Usage: Suitable when you need efficient insertions or deletions from both ends.
3. std::set and std::multiset
Both std::set and std::multiset are associative containers that store elements in sorted order. A set does not allow duplicate elements, while a multiset allows duplicates.

Example (std::set):
cpp
Copy code
#include <set>
#include <iostream>

std::set<int> numbers{1, 2, 3, 4, 5};
numbers.emplace(6);

for (auto n : numbers) {
    std::cout << n << std::endl;
}
Output:

Copy code
1
2
3
4
5
6
Example (std::multiset):
cpp
Copy code
#include <set>
#include <iostream>

std::multiset<int> numbers{1, 2, 3, 4, 5};
numbers.emplace(5);

for (auto n : numbers) {
    std::cout << n << std::endl;
}
Output:

Copy code
1
2
3
4
5
5
Explanation:
std::set: Ensures all elements are unique and sorted.
std::multiset: Allows duplicate elements but maintains the order.
Usage: Use std::set when uniqueness is needed, and std::multiset when duplicates are allowed.
4. std::map and std::multimap
Both std::map and std::multimap are associative containers that store key-value pairs. A map ensures unique keys, while a multimap allows duplicate keys.

Example (std::map):
cpp
Copy code
#include <map>
#include <iostream>

std::map<int, std::string> numbers{{1, "one"}, {2, "two"}, {3, "three"}};
numbers.emplace(4, "four");

for (auto [key, value] : numbers) {
    std::cout << key << "=" << value << std::endl;
}
Output:

sql
Copy code
1=one
2=two
3=three
4=four
Explanation:
std::map: Stores key-value pairs with unique keys, automatically sorted by key.
std::multimap: Similar to std::map but allows duplicate keys.
Usage: Use std::map when you need to associate a unique key with each value.
Algorithms
STL algorithms are generic functions that operate on containers. Here are a few useful examples.

1. Sum of Even Elements
This algorithm sums only the even elements of a container.

Example:
cpp
Copy code
#include <vector>
#include <numeric>
#include <iostream>

int sum_of_even_elements(const std::vector<int>& numbers) {
    return std::accumulate(numbers.begin(), numbers.end(), 0, [](int sum, int current) {
        return (current % 2 == 0) ? sum + current : sum;
    });
}

std::vector<int> numbers{1, 2, 3, 4, 5};
std::cout << sum_of_even_elements(numbers) << std::endl;
Output:

Copy code
6
Explanation:
std::accumulate iterates over the container and sums only the even numbers using a lambda function.
2. Partitioning Data
This algorithm rearranges the elements in a container such that all elements satisfying a given condition come before others.

Example:
cpp
Copy code
#include <vector>
#include <algorithm>
#include <iostream>

struct Person { std::string name; bool underage; };
using People = std::vector<Person>;

People underage_first(People people) {
    std::partition(people.begin(), people.end(), [](const Person& p) {
        return p.underage;
    });
    return people;
}

int main() {
    People people{{"Alice", true}, {"Bob", false}, {"Charlie", true}};
    people = underage_first(people);
    
    for (const auto& p : people) {
        std::cout << p.name << " (" << (p.underage ? "Underage" : "Adult") << ")\n";
    }
}
Explanation:
std::partition rearranges the container, placing elements that satisfy the condition at the front.
3. Sorting
Sorting allows you to arrange elements in a container according to a specified criterion.

Example:
cpp
Copy code
#include <vector>
#include <algorithm>
#include <iostream>

struct Person { std::string name; bool underage; };
using People = std::vector<Person>;

People alphabetical_names(People people) {
    std::sort(people.begin(), people.end(), [](const Person& a, const Person& b) {
        return a.name < b.name;
    });
    return people;
}

int main() {
    People people{{"Charlie", false}, {"Alice", true}, {"Bob", false}};
    people = alphabetical_names(people);
    
    for (const auto& p : people) {
        std::cout << p.name << "\n";
    }
}
Explanation:
std::sort sorts the container based on the provided comparison function. In this case, it sorts by name alphabetically.
4. Transforming Data
This algorithm applies a transformation function to each element of a container.

Example:
cpp
Copy code
#include <vector>
#include <algorithm>
#include <iostream>

struct Person { std::string name; int salary; };
using People = std::vector<Person>;

People give_a_raise(const People& people) {
    People after_raise{};
    std::transform(people.begin(), people.end(), std::back_inserter(after_raise), [](Person p) {
        p.salary *= 1.1; // 10% raise
        return p;
    });
    return after_raise;
}

int main() {
    People people{{"Alice", 30000}, {"Bob", 40000}};
    People after_raise = give_a_raise(people);

    for (const auto& p : after_raise) {
        std::cout << p.name << ": " << p.salary << std::endl;
    }
}
Explanation:
std::transform applies the transformation (raising salary by 10%) to each element and stores the result in a new container.
Iterators
Iterators are used to traverse containers. They provide a uniform interface for accessing elements regardless of the underlying container type. The three main types of iterators are:

Forward Iterator: Can move forward through a container.
Bidirectional Iterator: Can move forward and backward.
Random Access Iterator: Allows direct access to elements via index-like operations.
Conclusion
The C++ STL provides powerful and efficient tools that help streamline the development process. By using containers, algorithms, and iterators, you can write clean, reusable, and efficient C++ code.
