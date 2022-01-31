---
sort: 6
---
# Data Pipeline Design Patterns

## Data Lake vs Data Warehouse vs Data Mart

![datatype](https://chartio.com/images/articles/automatic-cloud-data-stack/data-storage-table.png)

## Design Pattern 

### ETL Pattern

![etl](./images/IMG_0185.jpg)

### ELT Pattern

![elt](./images/IMG_0186.jpg)

### CDC Pattern

![cdc](./images/IMG_0187.jpg)

### ETLT Pattern

![etlt](./images/IMG_0188.jpg)

## C++

### CMake

**Include header**

```cmake
include_directories(${YOUR_DIRECTORY})
```

**Set source files**
```cmake
set(SOURCES file.cpp file2.cpp ${YOUR_DIRECTORY}/file1.h ${YOUR_DIRECTORY}/file2.h)
add_executable(test ${SOURCES})
```

**Set Variable**
```cmake
SET()
```



**OpenCV Sample CMakeLists**

```cmake
cmake_minimum_required(VERSION 2.8)
project( DisplayImage )
find_package( OpenCV REQUIRED )
add_executable( DisplayImage DisplayImage.cpp )
target_link_libraries( DisplayImage ${OpenCV_LIBS} )
```

**Check Module List** 

```console
$ cmake --help-module-list
```

**Check pkg-config list**

```console
$ pkg-config --list-all
```

**Set CMAKE_PREFIX_PATH**

```console
$ cmake -DCMAKE_PREFIX_PATH=/home/rip/Qt/5.12.1/gcc_64/lib/cmake
```
or in CMakeLists:
```cmake
set(CMAKE_PREFIX_PATH "/home/rip/Qt/5.12.1/gcc_64/lib/cmake")
```

### Modern C++ Notes

#### Pass Arguments to Threads

- Pass Simple Arguments
- Pass References
- Pass Class Member Function

##### Passing simple arguments to thread

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

##### Passing References

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
##### Passing  Member Function

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

#### map vs. unordered_map

|          | map             | unordered_map  |
| -------- | --------------- | -------------- |
| Times    | log(n)          | O(n)           |
| Ordering | True            | False          |


##### Unordered_map Usage

Check an element:
```cpp
unordered_map <int, int> mp;

mp.find(x)!=mp.end() //  method 1
mp.count(x)!=0       //  method 2
```
[Reference](https://www.geeksforgeeks.org/map-vs-unordered_map-c/)

