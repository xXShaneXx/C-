C++ Standard Template Library (STL) Summary
The Standard Template Library (STL) provides several important generic classes and algorithms that help developers create efficient and reusable software components. The STL consists of four primary components: containers, algorithms, iterators, and function objects.

1. Containers
Containers in STL are objects that hold collections of data. STL provides different types of containers, each with its own characteristics and use cases.

std::vector
A dynamic array that can grow or shrink in size. It supports random access and is efficient for adding/removing elements at the end of the container.

Code Example:

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

std::vector provides a dynamic array, meaning it can change its size as needed.
It's efficient for accessing elements via indices and appending new elements at the end using push_back.
std::deque
A double-ended queue that supports fast insertion and deletion at both ends (front and back). The internal structure of std::deque makes it a good choice when you need to add or remove elements at both ends frequently.

Code Example:

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

std::deque is ideal when there are frequent operations at both ends of the container (like inserting or removing elements).
Unlike std::vector, std::deque allows efficient operations at both the front and back of the container.
std::set and std::multiset
std::set: Stores unique elements in sorted order.
std::multiset: Allows duplicate elements but maintains them in sorted order.
Code Example (std::set):

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
Explanation:

std::set ensures that each element is unique, and the container automatically sorts the elements.
std::multiset is similar but allows duplicate elements to be stored.
Code Example (std::multiset):

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
std::map and std::multimap
std::map: An associative container that stores key-value pairs with unique keys.
std::multimap: Like std::map, but allows duplicate keys.
Code Example (std::map):

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

std::map stores key-value pairs where the keys are unique and automatically sorted.
The std::multimap allows multiple elements with the same key.
2. Algorithms
STL algorithms are template functions that perform various operations on containers, such as sorting, searching, modifying, and partitioning data.

Sum of Even Elements
This algorithm calculates the sum of all even elements in a container.

Code Example:

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

This algorithm uses std::accumulate to iterate through the container and sum only the even numbers.
The lambda function inside accumulate filters out the odd numbers and only adds the even ones to the sum.
Partitioning Data
This algorithm rearranges elements in a container based on a condition. It moves all elements satisfying a condition (e.g., "underage" persons) to the front of the container.

Code Example:

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

std::partition rearranges the container so that all elements that satisfy the condition (in this case, underage == true) come before the rest.
Sorting
Sorting algorithms are used to order elements in containers. You can sort data in ascending or descending order using std::sort.

Code Example:

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

std::sort sorts the elements in ascending order. You can provide a custom comparison function (in this case, sorting by name alphabetically).
Transforming Data
This algorithm applies a function to each element in the container, transforming it and storing the result in another container.

Code Example:

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

std::transform applies a function to each element of the input container (people) and stores the transformed result in the after_raise container.
3. Iterators
Iterators are used to traverse through containers. They provide a way to access and manipulate container elements without exposing the underlying data structure.

Types of Iterators:
Forward Iterator: Can only move forward through the container.
Bidirectional Iterator: Can move both forward and backward.
Random Access Iterator: Allows access to elements at any position (like a pointer), and supports operations like addition and subtraction.
Each type of iterator is associated with the container type. For example, std::vector and std::deque provide random access iterators, while std::list provides bidirectional iterators.

Conclusion
The C++ STL offers a comprehensive set of tools that enable efficient and clean programming. By understanding the different containers, algorithms, and iterators available, you can write more efficient and maintainable C++ code.
