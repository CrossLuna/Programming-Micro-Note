#Programming Micro Note 2016100

## Multiple definition
Source:  
[error LNK2005, already defined?](http://stackoverflow.com/questions/10046485/error-lnk2005-already-defined)
Q:   
I have compilation errer with 
```C++
//plus.h
int plus(int n){
    return n + 1;
}
```
```C++
//plus.cpp
#include "plus.h"
/*bla bla bla*/
```
```C++
//main.cpp
#include "plus.h"
int main(){
    plus(3);
}
```

A:  
You violated One Definition Rule. Tracing like a compiler, you find that when compiling the `plus.cpp` translation unit, `plus(int n)` is defined twice since header file is copied by preprocessor. The solution is either to leave only declaration in header files and to put all implementation in `cpp` file or to announce the function as `inline`.

```C++
//plus.h
inline int plus(int n){
    return n + 1;
}
```

***

## Dynamic allocation with size 0
Source:  
[C++ new int[0] — will it allocate memory?](http://stackoverflow.com/questions/1087042/c-new-int0-will-it-allocate-memory)  
Effective C++ 3/e - Item 51: Adhere to convention when writing new and delete

Q:  
If a psycopath writes something like 
```C++
int *pt = new int[0];
```
what happens?

A:
It allocates an array with NO elements and return a legal pointer. Dereference the pointer is undefined behavior. You can do that but not legal. BTW, `delete[]` it is legal.

***
## typename 
Q:  
I have a class looking like
```C++
template <typename T> 
class mw2dPoint : public mw2dGeometry<T> {
public:
    /*bla bla bla*/
    typedef typename misc::mwAutoPointer<mw2dPoint<T>> Ptr;
    /*bla bla bla*/
};
```
and when I write 
```C++
template <typename T>
cadcam::mw2dPoint<T>::Ptr to_mwpoint(const contour_data<T>& contour){
    return new cadcam::mw2dPoint<T>(contour._pos[0], contour._pos[1]);
}
```
it doesn't compile!

A:  
In compile time, the compiler doesn't know `cadcam::mw2dPoint<T>::Ptr` is a type (depending on `T`). Therefore, use
```C++
template <typename T>
typename cadcam::mw2dPoint<T>::Ptr to_mwpoint(const contour_data<T>& contour){
    return new cadcam::mw2dPoint<T>(contour._pos[0], contour._pos[1]);
}
``` 