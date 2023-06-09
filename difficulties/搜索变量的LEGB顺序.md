## 搜索变量的LEGB顺序

LEGB是Python中的作用域解析规则，用于确定在一个作用域中使用哪个变量名。

- L： Local（局部作用域），函数内部定义的名字。
- E： Enclosed（闭包函数外的函数中），闭包函数外面的函数中定义的名字。
- G： Global（全局作用域），模块中定义的名字。
- B： Built-in（内置作用域），Python内置的名字。

当我们使用一个变量名时，Python会按照LEGB的顺序依次查找这个变量名对应的值。例如，如果在函数内部使用了一个变量名，Python会先在该函数内部的局部作用域中查找该变量，找到则使用该值；如果没有找到，则在包含该函数的外部函数中查找该变量；如果还是没有找到，则在全局作用域中查找该变量；如果最终还是找不到，则报错。

举个例子：
```python
x = 42 # x在全局作用域中定义

def test():
    x = 2  # x在局部作用域中定义
    def inner():
        nonlocal x  # 引用上一级函数（即test函数）中的x
        x += 1
        print(x)
    inner()

test()
print(x)
```
运行上面的代码，输出结果为：
```
3
42 
```
在`test()`函数内部，我们定义了一个局部变量`x`，并在`inner()`函数内部引用了上一级函数`test()`中的`x`。`inner()`函数内部对`x`进行自增操作，最终输出3。

在`test()`函数内部增加`print(x)`的语句会输出2。这证明了在内部函数内部修改了上级函数中的变量。最后输出`x`的值，结果为全局作用域中的42。

因此，在使用变量名时，理解LEGB规则可以避免命名冲突和错误使用变量名的问题。

## 闭包函数

闭包函数指的是在函数内部定义函数，并且内部函数可以访问外部函数的变量，即使外部函数已经执行完毕，也能够记住并继续访问这些变量的函数。简单来说，闭包函数是指一个函数，它有一个返回值是一个函数。例如： 

```python
def outer_func(x):
    def inner_func(y):
        return x + y
    return inner_func

closure = outer_func(5)    # closure 现在 == inner_func，并且已经捕获了 x = 5
result = closure(3)        # 计算 result == 8
```

在上面的例子中，`outer_func` 是一个以 x 作为参数的函数，其返回一个内部函数` inner_func`。`inner_func` 以 y 作为参数，返回 x + y 的值。当调用 `outer_func(5)` 时，返回 `inner_func`，此时 x 已经被捕获为 5。当我们执行 `closure(3)` 时，实际上在调用 `inner_func(3)`，得到 5 + 3 = 8 的结果。值得注意的是，`closure(3)` 中并没有传递 x 的值，但是因为 `inner_func` 能够访问外部函数 `outer_func` 的变量，所以 x 的值仍然被记住并且被使用了。