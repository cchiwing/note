# Python
[TOC]


## IO

### Join dir and file to path

```python
import os
os.path.join("C:\\folder", "filename.txt") 
# Result: C:\\folder\\filename.txt 
```



## Data Type

### Array (list)

#### [`append`](https://docs.python.org/2/library/array.html?#array.array.append): Appends object at the end.

```py
x = [1, 2, 3]
x.append([4, 5])
print (x)
```

gives you: `[1, 2, 3, [4, 5]]`



#### [`extend`](https://docs.python.org/2/library/array.html?#array.array.extend): Extends list by appending elements from the iterable.

```py
x = [1, 2, 3]
x.extend([4, 5])
print (x)
```

gives you: `[1, 2, 3, 4, 5]`



#### `set`: Delete duplicated, 删除重复数据

```python
list(set(['燒排骨', '經典燒排骨','露比三合一拼盤', '燒排骨' ]))
# result: ['露比三合一拼盤', '經典燒排骨', '燒排骨']
```



