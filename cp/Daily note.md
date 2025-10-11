

# **11 October 2025** 
----
1. Garbage Value 
    1. https://unacademy.com/content/question-answer/gk/what-is-garbage-value/
2. - Basic Bitwise Operators
     1. https://www.geeksforgeeks.org/cpp/cpp-bitwise-operators/
3.  Overflows and Underflows
      1. https://www.geeksforgeeks.org/cpp/how-to-avoid-integer-overflows-and-underflows-in-cpp/
4. Infinite Loop
``` cpp

    for (;;) {
        // Code to be executed indefinitely
    }

        while (true) {
        // Code to be executed indefinitely
    }
    
    do {
        // Code to be executed indefinitely
    } while (true);
```
5. Occurrence
``` cpp
[[include]] <iostream>
[[include]] <vector>
[[include]] <algorithm> 

int main() {
    std::vector<int> numbers = {1, 2, 3, 2, 4, 2, 5};
    int target_value = 2;

    // Using std::count to find occurrences
    int count = std::count(numbers.begin(), numbers.end(), target_value);
    std==cout << "The value " << target_value << " appears " << count << " times." << std==endl;

    // Manually counting occurrences
    int manual_count = 0;
    for (int num : numbers) {
        if (num == target_value) {
            manual_count++;
        }
    }
    std==cout << "Manual count: The value " << target_value << " appears " << manual_count << " times." << std==endl;

    return 0;
}
```
6. 