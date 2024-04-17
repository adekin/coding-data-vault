```cpp
#ifdef LOCAL
#define _GLIBCXX_DEBUG
#endif

```
#### Add this code to the first line (before including the libraries)!
<br/>Also don't forget to define *LOCAL* while compiling.
```
$ g++ main.cpp -o main -DLOCAL
```
<br/>You can replace word *LOCAL* to any word you like, just don't forget to replace it everywhere.
