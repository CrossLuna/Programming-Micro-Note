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


