
# Programming Micro Note 20161010

## Returning array from pure C funcion
Source:  
[How to make an array return type from C function?](http://stackoverflow.com/questions/14297169/how-to-make-an-array-return-type-from-c-function)

Q:  
How do I return an array form pure C function?  
```C
char *makeArray(char array []) {
    char returned [10];
    //handling the array
    return &(returned[0]); //is this correct?
} 
```
like this perhaps?  

A:  
Not in that way. The array disappers after leaving the scope. You can use either the static variable or dynamically allocate them.  Another way is to pass a pointer which points to an allocated memory to the function as a parameter.  

Option 1:
```C
char *makeArray(int count) {
    char *ret = malloc(count);
    if(!ret)
        return NULL;

    for(int i = 0; i < count; ++i) 
        ret[i] = i;

    return ret;
}
```
Option 2:
```C
void makeArray(char *buf, int count) {
    for(int i = 0; i < count; ++i)
        buf[i] = i;
}
```

***

## Dereference NULL pointer
Source:  
[Why dereferencing a null pointer is undefined behaviour?](http://stackoverflow.com/questions/6793262/why-dereferencing-a-null-pointer-is-undefined-behaviour)
[I do not know C](http://kukuruku.co/hub/programming/i-do-not-know-c)  

Q: What happens if I dereference a `NULL` pointer?  
A: Undefined Behavior!  
Q: But why UB instead of...?    
A: Otherwise compiler needs to check if the pointer is `NULL` and take corresponding action. It may limit potential optimizations.
See question 2 in *I do not know C*
