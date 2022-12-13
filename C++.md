| 标准容器类 | 特点 | 类比 |
| --- | --- | --- |
| 顺序性容器 | 
| vector | 从后面快速的插入与删除，直接访问任何元素 | 单端数组 |
| deque | 从前面或后面快速的插入与删除，直接访问任何元素 | 双端数组 |
| queue | 先进先出 | 队列 |
| list | 双链表，从任何地方快速插入与删除 | 双向循环链表 |
| stack | 后进先出 | 栈 |
| 关联容器 |
| set | 基础为红黑树，不允许重复值,自动排序 | 集合 |
| multiset | 允许重复值 | 
| pair | 键值对 |
| map | 一对多映射，基于关键字快速查找，不允许重复值 | 所有元素为键值对 |
| multimap | 一对多映射，基于关键字快速查找，允许重复值 |

## vector容器
自动拓展的动态数组

### 创建
| 函数 | 说明 |
| --- | --- |
| vector() | 无参构造 |
| vector(int size) | 指定初始大小 |
| vector(int size, const t &t) | 指定初始大小和初始值 |
| vector(const vector &v) (operator=)| 复制(拷贝)构造,用等号赋值即可 |
| vector(begin, end) | 指定拷贝区间 |

### 赋值
| 函数 | 说明 |
| - | - |
| push_back() | 在数组尾端加入元素 |
| insert(iterator it, const T &t) | 指定位置添加元素 |
| assign(begin, end) | 将vector一部分赋值 |
| assign(n, m) | 给vector赋值n个m |

## set容器
### 特点
- 自动排序,如果是键值对,要求key=value.  
- 不允许重复值(「请」用multiset)
- 一般不能修改元素的值,「请」先删除,再添加。
- set定义于std命名空间<set>头文件中。

### 创建
1. 调用默认构造函数:  
`std::set<std::string> myset;`

2. 创建时进行初始化:  
`set<string> myset{"string1", "string2", "string3"};`  

3. 利用已有的set容器拷贝构造:  
`set<string> copyset(myset);`  
`set<string> copyset = myset;`

4. 取已有的set容器的部分元素初始化:  
`set<string> copyset(myset.begin(), myset.end());`

5. 

