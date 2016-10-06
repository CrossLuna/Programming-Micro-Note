#Programming Micro Note 20161006

## extern and static
Q:  
What do they mean?  
A:  
`extern`  
for function: means it's a declaration, not necassarily needed.  
for variable: means it's a declaration, definition may be in other file.  

`static`  
for function: means the funtions is visible only in this file.  
for variable: means this variable lives during the whole running time of the program.  
Q: Why not Global Variable?  A: Scope(where the variable is visible,) global variable pollutes too much.  


## Forward-declare with namespace
Source:  
[Why can't I forward-declare a class in a namespace like this?](http://stackoverflow.com/questions/2059665/why-cant-i-forward-declare-a-class-in-a-namespace-like-this)

Q:  
I have compilation error with forward-declare.
```C++
// for a class "Car" in namespace "myspace"
class myspace::Car;
```
Visual C++: error C2653  

A:  
Do this way
```C++
namespace myspace{
    class Car;
}
```
C++ allows you to do so only when the class is declared already. Some people say it should be legal.
## wchar_t
Q: What do you think of `wchar_t` ?
A: **NEVER USE IT** whenever possible, unless some stupid APIs do it that way. `wchat_t` is implemented environment-dependently.