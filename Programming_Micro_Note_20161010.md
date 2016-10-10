#Programming Micro Note 20161010
##Compare C-style String
Remember to use `strcmp` to compare `char *`, otherwise it compares the address instead of the "string."  
Q:  
But it works find when I write
```C++
#include <iostream>
using namespace std;
int main(){
    const char* text1 = "CCW";
    const char* text2 = "CCW";
    if(text1 == text2)
        cout << "Equal" << endl;
    else
        cout << "Not Equal" << endl;
}
```
A:  
That's because compiler assigns the same address to avoid duplicate. When you get the string from other source, the story is different. Use compare function instead, or create a `string` object.
```C++
#include <iostream>
#include <cstring>
using namespace std;
int main(){
    const char* text1 = "CCW";
    const char* text2 = "CCW";
    if(strcmp(text1, text2) == 0)
        cout << "Equal" << endl;
    else
        cout << "Not Equal" << endl;
}
```