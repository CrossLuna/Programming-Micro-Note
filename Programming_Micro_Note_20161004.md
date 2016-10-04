#Programming Micro Note 20161004

##Purpose of void
Source
[Why is (void) 0 a no operation in C and C++?](http://stackoverflow.com/questions/2198950/why-is-void-0-a-no-operation-in-c-and-c)
[What is the purpose of the statement “(void)c;”?](http://stackoverflow.com/questions/6145548/what-is-the-purpose-of-the-statement-voidc?noredirect=1&lq=1)

Q: Why  no operation is defined as ?
```C
#define noop ((void) 0)
``` 
A: To avoid a psychopath doing something like
```C
int x = noop;
```
compiler complains. 
GCC `error: void value not ignored as it ought to be`
Visucal C++ `'void' illegal with all types`
*******
Q: What is the purpose of the last line?
```C++
op_queue<operation> completed_ops;
task_cleanup c = { this, &lock, &completed_ops };
(void)c;  // EH?
```
A: Maybe to avoid an unused variable warning of `c`.  
******
## Operator overloading
Source:
[What is the difference between defining an overloaded operator outside the class and defining it inside the class?](https://www.quora.com/What-is-the-difference-between-defining-an-overloaded-operator-outside-the-class-and-defining-it-inside-the-class)
[c++ two versions of overloading subscript operator](http://stackoverflow.com/questions/15413831/c-two-versions-of-overloading-subscript-operator)
Q: Difference between defining overloaded operators outside and inside the class?  
A: Here are the reasons:  
1. LHS and RHS are symmetric. If we do it inside, `Complex + double` can compile but `double + Complex` cannot.
2. Hide class implementation details.
3. Generally speaking, prefer non-member functions in C++

Q: Why `const` version of e.g. subscript `operator[]`, `begin()`, `end()` ? Any difference between
```C++
const T& operator[](size_t idx) const;
```
and
```C++
T& operator[](size_t idx);
```

A: They are for `const` version of object. For example,
```C++
const Vector<int> v = /*Initialization*/;
v[0] = 3;      // Wrong!
int n = v[0];  // Even reading is not allowed!
```
if there is no `const` version of `operator[]`, subscipt operator on `const` object is not allowed at all (compilation error.) BTW, the two versions are overloaded by constness of function, not by the constness of return type. Funcion cannot be overloaded just by different return types.