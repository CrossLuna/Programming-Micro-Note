
# Programming Micro Note 20161019

## Container - constness issue

Source:  
[Cppreference - vector](http://en.cppreference.com/w/cpp/container/vector/begin)  

Q:  
I have constness issue when using self-defined container in the case of calling $begin()$ and $end()$  

A:  
Remember to define all 3 versions of `begin()`  

```C++
iterator begin();
const_iterator begin() const;
const_iterator cbegin() const;  // Since C++11
```

