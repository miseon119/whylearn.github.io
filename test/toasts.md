---
sort: 2
---

# Modern C++ Notes

## Pass Arguments to Threads

- Pass Simple Arguments
- Pass References
- Pass Class Member Function

### Passing simple arguments to thread

```cpp
#include <iostream>
#include <string>
#include <thread>

void threadFunc(int x, std::string str)
{
    std::cout<< x <<std::endl;
    std::cout<< str <<std::endl;
}
int main()  
{
    int x = 5;
    std::string str = "abc";
    std::thread threadObj(threadFunc, x, str);
    threadObj.join();
    return 0;
}
```

### Passing References

> We use std::ref() to pass a reference

```cpp
#include <iostream>
#include <thread>
void threadFunc(int const & x)
{
    std::cout<<" x = "<<x<<std::endl;
}
int main()
{
    int x = 5;
    std::thread threadObj(threadFunc,std::ref(x));
    threadObj.join();
    return 0;
}
```
### Passing  Member Function

> Create a thread using Class member function.

```cpp
#include <iostream>
#include <thread>
class Drone {
public:
    Drone(){}
    Drone(const Drone & obj){}
    void MissionStart(int x)
    {
        While(1)
        {
            x++;
            // do something
        }
    }
};
int main() {
 
    Drone dummyDrone;
    int x = 0;
    std::thread threadObj(&Drone::MissionStart,&dummyDrone, x);
    threadObj.join();
    return 0;
}
```

## map vs. unordered_map

|          | map             | unordered_map  |
| -------- | --------------- | -------------- |
| Times    | log(n)          | O(n)           |
| Ordering | True            | False          |


### Unordered_map Usage

Check an element:
```cpp
unordered_map <int, int> mp;

mp.find(x)!=mp.end() //  method 1
mp.count(x)!=0       //  method 2
```
[Reference](https://www.geeksforgeeks.org/map-vs-unordered_map-c/)
