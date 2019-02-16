

# [2017 407 Understanding Undefined Behavior](https://developer.apple.com/videos/play/wwdc2017/407/)

## What Can the Compiler Do with Undefined Behavior?

* Diagnose using warnings or errors
* Act in a documented manner
* Produce unpredictable results

### Undefined Behavior Is About Tradeoffs

Performance over safety

Some Undefined Behavior Examples

Use of an uninitialized variable

```c
int uninitialized_variable(int arg) {
    int value;
    if (arg <= 0)
        value = 42;
    return arg + value;
}
```

Misaligned pointers

```c
char * serialize_misaligned(char * buffer, int a, int b) {
    *(int *)buffer = a;
    buffer += sizeof(a);
    *(int *)buffer = b;
    buffer += sizeof(b);
    return buffer;
}  
```
