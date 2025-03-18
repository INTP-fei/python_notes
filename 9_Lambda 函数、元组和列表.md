# Lambda 函数、元组和列表
## Lambda 函数和匿名函数
- `"Lambda 函数是在 Python 中创建匿名函数的一种方式，用于简单任务而不需要给它们命名。"`
#### Lambda 函数的定义
- lambda 函数是使用 <mark>lambda</mark> 关键字定义的，可以接受任意数量的参数，但只有一个表达式。语法如下：
**lambda 参数: 表达式**
    - **Lambda 关键字**：表示匿名函数的开始。
    - **参数**：函数将接受的变量。
    - **表达式**：当函数被调用时执行的计算。该表达式的结果会被返回，而**无需使用 return 关键字**。
#### Lambda 函数示例
  - 考虑一个检查数字是否为偶数的 lambda 函数：
```python
    def is_even(x):
    return x%2==0
    
    is_even(8)
    # 可以等效的使用 lambda 函数：             
    (lambda x: x%2==0)(8)  # 后接()立即调用的函数表达式
```
#### Lambda 函数的优点
1. **简洁性：**适合短小的单次使用函数。
2. **无需命名：**对仅需临时使用的函数非常有用。
```python
   def do_twice(n, fn):
    # 调用传入的函数fn两次，第一次将n作为参数传入，第二次将第一次的结果作为参数传入
    return fn(fn(n))
   # 调用do_twice函数，传入3和一个lambda函数，该lambda函数将输入的值平方
   print(do_twice(3, lambda x: x**2))  # 输出: 81
```
## 元组和列表简介
   - 已经见过的标量类型：int（整数）、float（浮点数）、bool（布尔值）
   - 已经见过的一个复合类型：string（字符串视为序列）
   - 想要介绍更一般的复合数据类型
     - 元素的索引序列，这些元素本身可以是复合结构
     - 元组（Tuples）——不可变的
     - 列表（Lists）——可变的
   - 下一节课，将探讨以下概念：
     - 可变性（Mutability）
     - 别名（Aliasing）
     - 克隆（Cloning）
### 元组
  `"元组是可索引的有序对象序列。"`
3. 元组的特征
   - 序列：元组可以包含任何类型的对象，而不仅仅是字符。
   - 顺序：元素具有定义的顺序。
   - 可索引：可以使用索引访问元素。
#### 创建元组
  - **空元组**：用 `() `创建。
  - **单元素元组**：需要一个逗号，例如 `(4,)`。
  - **多个元素**：用逗号分隔元素创建，例如 `(2, "mit", 3)`。
#### 元组的操作
  - 索引：使用方括号访问元素，例如 tuple[0]。
  - 连接：使用 + 运算符连接元组。
  - 长度：使用 len(tuple) 查找元素数量。
  - 最大/最小/总和：使用内置函数检索最大/最小值或求和元素。
  - **元组的不可变性**
```python
# 创建了一个包含多个元素的元组
t = (2, "mit", 3) 
# 表示访问元组 t 的第一个元素，结果为2（索引从0开始）
t[0] 
# 表示两个元组的拼接，结果为一个新的元组 (2, "mit", 3, 5, 6)
(2, "mit", 3) + (5, 6) 
#表示对元组 t 进行切片操作，结果为 ("mit",)
t[1:2] 
#表示对元组 t 进行切片操作，结果为 ("mit", 3)
t[1:3] 
#表示计算元组 t 的长度，结果为3
len(t)
# 表示找出元组 (3, 5, 0) 中的最大值，结果为5（其他函数也可以在元组上工作，例如 sum）
max((3, 5, 0))
#尝试修改元组 t 的第二个元素，这将导致错误，因为元组是不可变的，不能修改对象
t[1] = 4 
``` 
**变量t和它所绑定的对象是不同的东西。t等于其他值，它所绑定的对象仍将驻留在内存中，只是t失去了对它的绑定，t指向新对象。**
#### 遍历元组
   - 你可以直接遍历元组的元素，类似于遍历字符串。
```python
for e in seq:
print(e)
```
  - 这将打印 seq 的每个元素：2，a，4，(1, 2)。
#### 元组的交换变量
  - <mark> 元组允许优雅地交换值，而无需临时变量。</mark>
```python
x = 1  
y = 2  
# 使用元组解包来交换 x 和 y 的值
(x, y) = (y, x)  # 创建一个元组 (y, x)，即 (2, 1)，然后将其解包到 (x, y)
# 现在 x 的值变为 2，y 的值变为 1
```
#### 元组的返回值
   - 元组允许你从函数返回多个值。
```python
def quotient_and_remainder(x, y):
q = x // y  # q 是 x 除以 y 的商
r = x % y   # r 是 x 除以 y 的余数
# 返回商和余数作为一个元组
return (q, r)
# 调用函数，计算 10 除以 3 的商和余数
result = quotient_and_remainder(10, 3)
# 打印结果，result 是一个元组，包含商和余数
print(result)  # 输出: (3, 1)
# 调用函数，计算 5 除以 2 的商和余数，并将返回的元组解包
(quot, rem) = quotient_and_remainder(5, 2)
# 打印商和余数
print('quotient is:', quot)  # 输出: quotient is: 2
print('remainder is:', rem)   # 输出: remainder is: 1
```
##### 实践练习：计数字符
   - 编写一个函数 char_counts(s)，返回一个元组，包含字符串中的元音和辅音的数量。
```python
def char_counts(s):
    vowels = 'aeiou'
    v, c = 0, 0
    for char in s:
        if char in vowels:
            v += 1
        else:
            c += 1
    return (v, c)
```
#### 函数中的可变参数数量
**使用星号表示法处理可变参数**
`"一旦你创建了一个函数，其参数是星号和输入的名称，Python 基本上会将该输入分配给一个元组。"`
   - **星号表示法（*）**允许函数接受可变数量的参数。
   - 该参数将所有额外的位置参数收集到一个元组中。
  - 例如，创建一个计算可变数量输入均值的函数 mean
```python
  def mean(*args):
  tot = 0
  for a in args:
     tot += a
  return tot/len(args)
```
  - mean 函数可以接受多个数字：
  - mean(1, 2, 3, 4, 5, 6) 返回六个参数的均值。
  - mean(6, 0, 9) 返回三个参数的均值。
### 列表
#### 列表的定义和创建
`"要定义一个列表，我们使用开闭方括号。"`
  - 列表使用 方括号 [] 定义。
  - 创建列表的示例：
    - 一个空列表：my_list = []
    - 一个包含一个元素的列表：single_element_list = [42]（不需要额外的逗号）。
#### 迭代列表
  - 计算列表中元素的总和
  - 常见模式：
```python
    total = 0
    for i in range(len(L)):
    total += L[i] # 通过 L[i] 访问列表元素，并将它们加到 total 上
    print (total)
```
   - 迭代列表
    - 自然地在函数内部捕获对列表的迭代
```python
    total = 0
    for i in L: 
     total += i
    print total
  ```
  - 因为列表是元素的有序序列，它们自然地与迭代函数接口。 
```python
    def list_sum(L):
    total = 0
    for i in L:
     total += i
    return total
list_sum([8,3,5])
```
##### 添加列表中的元素
```python
def list_sum(L):
    total = 0 
    for e in L: 
        total += e 
    return(total)
print(list_sum([1,3,5]))
```
##### 添加列表中元素的长度
```python
# 定义一个函数，计算列表中每个字符串的长度之和
def len_sum(L):
    total = 0  # 初始化总长度为 0
    # 遍历列表 L 中的每个字符串 s
    for s in L: 
        total += len(s)  # 将字符串 s 的长度加到 total 中
    return total  # 返回总长度
# 调用 len_sum 函数，传入一个包含字符串的列表
print(len_sum(['ab', 'def', 'g']))  # 输出: 6
```
```python
def sum_and_prod(L):
    """ L 是一个数字列表
    返回一个元组，第一个值是 L 中所有元素的和，
    第二个值是 L 中所有元素的积
    """
    s,p = 0,1
    for i in L:
        s +=i
        p *=i
    return (s,p)

print(sum_and_prod([4,6,2,5]))   # prints (17, 240)
```
# 课后
1. **课后作业**
```python
# 跟踪此代码：
# 找出它返回的内容，然后运行它来自己检查。
def always_sunny(t1, t2):
""" t1, t2 非空 """
    sun = ("sunny", "sun")
    first = t1[0] + t2[0]
    return (sun[0], first)
# always_sunny(('cloudy' ), ('cold',)) # 返回什么？
# 输出('sunny', 'ccold')
#解析:t1 是 ('cloudy')，但缺少逗号，实际被解析为字符串 'cloudy'。
#     t2 是 ('cold',)，是一个元组，其第一个元素是字符串 'cold'。
```
```python
def max_of_both(n, f1, f2):
""" n 是 int
f1 和 f2 是接受 int 并返回浮点数的函数
将 f1 和 f2 应用于 0 到 n（含）之间的所有数字。
返回所有这些结果的最大值。
"""
# 我的想法用元组来做，最后通过max函数比较大小
    results = ()
    for i in range(n+1):
        results += (f1(i),f2(i))
    return max(results)
print(max_of_both(2, lambda x:x-1, lambda x:x+1))   # prints 3
print(max_of_both(10, lambda x:x*2, lambda x:x/2))  # prints 20
##老师的方法
  maxval = f1(0)  # 初始化 maxval 为 f1(0) 的值，调用函数 f1，并传入参数 0
  for i in range(n+1):  # 遍历 0 到 n
      if f1(i) > maxval:  # 如果 f1(i) 大于当前最大值
          maxval = f1(i)  # 更新 maxval
      if f2(i) > maxval:  # 如果 f2(i) 大于当前最大值
          maxval = f2(i)  # 更新 maxval
  return maxval  # 返回最终的最大值
```
```python
def sublist_sum(L):
    """ L 是一个列表，其元素为 int 元素的列表
返回所有 int 元素的总和。"""
    # your code here
#print(sublist_sum([[1,2], [4,5,6]])) # prints 18
#我的想法 
# wrong  
  sum = 0
  for i in L:
      sum += i
  return sum
# 因为L 是一个嵌套列表（列表的列表）而你直接对 L 中的元素（即子列表）进行累加，导致 TypeError，因为子列表不能直接与整数相加。
#修改方法 需要遍历每个子列表，再遍历子列表中的每个整数，将它们累加到总和中。
def sublist_sum(L):
    total = 0
    for sublist in L:  # 遍历每个子列表
        for num in sublist:  # 遍历子列表中的每个整数
            total += num
    return total
#老师的方法
## One way by using the sum function over the sublist
# sum() 是 Python 内置函数，用于计算可迭代对象（如列表、元组等）中所有元素的和。
    tot = 0
    for subL in L:
        tot += sum(subL)
    return tot
## Alternate way by nesting a for loop that 
## iterates over the sublist's int elements
    tot = 0
    for subL in L:
        for e in subL:
            tot += e
    return tot
```
2. **手指练习**
```python
def dot_product(tA,tB):
"""
tA：一个数字元组
tB：一个与 tA 长度相同的数字元组
假设 tA 和 tB 长度相同。
返回一个元组，其中：
* 第一个元素是其中一个元组的长度
* 第二个元素是tA和tB成对乘积的总和
"""
# 示例：
tA = (1, 2, 3)
tB = (4, 5, 6) 
print(dot_product(tA, tB)) # 打印 (3,32)
#我的做法
tA = (1, 2, 3)
tB = (4, 5, 6) 
def dot_product(tA,tB):
  total = 0
  l=len(tA)
  for i in range(l):
    total += tA[i]*tB[i]
  return (l,total)

print(dot_product(tA, tB))
#老师的方法
def dot_product(tA, tB): 
  tot = 0
  for i in range(len(tA)):
    tot += tA[i]*tB[i]
  return (len(tA), tot)
```
    