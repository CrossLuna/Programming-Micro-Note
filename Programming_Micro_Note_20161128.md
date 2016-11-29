
# Programming Micro Note 20161128

## Temporary objects

Source:  
[When do temporary parameter values go out of scope?](http://stackoverflow.com/questions/12323049/when-do-temporary-parameter-values-go-out-of-scope)  

Q:  
I have code 
```C++
int LegacyFunction(const char *s) {
    // do something with s, like print it to standard output
    // this function does NOT retain any pointer to s after it returns.
    return strlen(s);
}

std::string ModernFunction() {
    // do something that returns a string
    return "Hello";
}

LegacyFunction(ModernFunction().c_str());
``` 
Is it safe?  

A:    
Yes, the destruction of copy will be after evaluation of full expression.  
According to [n3337](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2012/n3337.pdf) 12.2/3

>  Temporary objects are destroyed as the last step in evaluating the full-expression (1.9) that (lexically) contains the point where they were created. 

