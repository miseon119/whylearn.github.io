# Multi-threading Note

## Three Ways to Create Threads

```cpp
#include <thread>
```

- Function Pointer
- Function Objects
- Lambda

## Function Pointer

```cpp
#include <iostream>
#include <thread>

void thread_A()
{
    for(int i = 0; i < 10000; i++);
        std::cout<<"I'm thread A! "<<std::endl;
}

int main()  
{
    std::thread threadObj(thread_A);
    sleep(5);
    threadObj.join();
    return 0;
}
```

## Function Objects

