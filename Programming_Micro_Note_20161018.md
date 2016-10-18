
# Programming Micro Note 20161018

## Reference to pointer

Source:  
[Passing references to pointers in C++](http://stackoverflow.com/questions/823426/passing-references-to-pointers-in-c)  

Q: How do I pass a reference of pointer to a function?  
```C++
void func(string*& val) {
	//...
}
{
	string s;
	func(&s);
}
```
this doesn't comile.
>  cannot convert parameter 1 from 'std::string *' to 'std::string *&'  

A:  
You need an actual string pointer instead of an anonymous string pointer.
```C++
string s;
string * ptr_s = &s;
func(ptr_s);
```
should work.

 



