
# Programming Micro Note 20161017

## Negative number assigned to `unsigned`
Source:  
[What happens if I assign a negative value to an unsigned variable?](http://stackoverflow.com/questions/2711522/what-happens-if-i-assign-a-negative-value-to-an-unsigned-variable)
Q:  
What happes if I do
```C++
unsigned int n = -1;
```

A:
>  Section 4.7
>  If the destination type is unsigned, the resulting value is the least unsigned integer congruent to the source integer (modulo 2^n where n is the number of bits used to represent the unsigned type). [ Note: In a two’s complement representation, this conversion is conceptual and there is no change in the bit pattern (if there is no truncation)

so it's `0xFFFFFFFF` (on a machine defining `unsigned` as 32 bits);