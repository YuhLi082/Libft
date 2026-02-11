# Libft - Your Very First Own Library / 你的第一个自有函数库

**EN**  
Libft involves recoding a collection of standard C library functions, along with additional utility functions and linked list manipulation tools. The goal is to build a personal library of frequently used functions.

**CN**  
Libft 旨在重新实现一套标准C库函数，并在此基础上扩展实用工具函数和链表操作函数。目标是构建一个可复用的个人函数库。

---

## 🛠️ Instructions / 编译与使用

### Compilation / 编译

```bash
make        # Generate libft.a / 生成静态库
make bonus  # Include bonus functions (linked list) / 包含链表函数
```

### Makefile Rules / 规则说明

| Rule / 规则 | Description / 作用 |
|-------------|-------------------|
| `all`       | Compile library / 编译库 |
| `clean`     | Remove object files / 删除目标文件 |
| `fclean`    | Remove object files and library / 删除目标文件和库 |
| `re`        | fclean + all / 重新编译 |
| `bonus`     | Compile with linked list functions / 编译包含链表函数 |

### Usage / 使用

```c
#include "libft.h"

// Compile with / 编译时链接:
// cc -Wall -Wextra -Werror your_program.c -L. -lft
```

---

## 📚 Function Documentation / 函数详解

---

## 🔤 Character Classification & Conversion / 字符判断与转换

---

### `int ft_isalpha(int c)`

**EN**  
Checks if a character is an alphabetic letter (a-z or A-Z).  
**Implementation**: Simple range checks using ASCII values.

**CN**  
判断字符是否为英文字母（a-z 或 A-Z）。  
**实现**：直接比较ASCII范围。

```c
if ((c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z'))
    return (1);
return (0);
```

---

### `int ft_isdigit(int c)`

**EN**  
Checks if a character is a digit (0-9).  
**Implementation**: Returns 1 if c is between '0' and '9'.

**CN**  
判断字符是否为数字（0-9）。  
**实现**：若c在'0'~'9'之间返回1。

---

### `int ft_isalnum(int c)`

**EN**  
Checks if a character is alphanumeric (letter or digit).  
**Implementation**: Combines `ft_isalpha` and `ft_isdigit` logic.

**CN**  
判断字符是否为字母或数字。  
**实现**：合并`ft_isalpha`和`ft_isdigit`的判断条件。

---

### `int ft_isascii(int c)`

**EN**  
Checks if a character is within the ASCII table (0-127).  
**Implementation**: Returns 1 if c ≥ 0 and c ≤ 127.

**CN**  
判断字符是否属于ASCII表（0-127）。  
**实现**：若c ≥ 0 且 c ≤ 127 返回1。

---

### `int ft_isprint(int c)`

**EN**  
Checks if a character is printable (including space).  
**Implementation**: Returns 1 if c ≥ 32 and c < 127.

**CN**  
判断字符是否为可打印字符（含空格）。  
**实现**：若c ≥ 32 且 c < 127 返回1。

---

### `int ft_toupper(int c)`

**EN**  
Converts a lowercase letter to uppercase.  
**Implementation**: If c is between 'a' and 'z', subtracts 32.

**CN**  
将小写字母转换为大写。  
**实现**：若c在'a'~'z'之间，减去32。

---

### `int ft_tolower(int c)`

**EN**  
Converts an uppercase letter to lowercase.  
**Implementation**: If c is between 'A' and 'Z', adds 32.

**CN**  
将大写字母转换为小写。  
**实现**：若c在'A'~'Z'之间，加上32。

---

## 📝 String Manipulation / 字符串处理

---

### `size_t ft_strlen(const char *s)`

**EN**  
Calculates the length of a string.  
**Implementation**: Iterates through the string until null terminator, returns pointer difference.

**CN**  
计算字符串长度。  
**实现**：用指针遍历至'\0'，返回指针差值。

```c
const char *p = s;
while (*p)
    p++;
return (p - s);
```

---

### `size_t ft_strlcpy(char *dst, const char *src, size_t dstsize)`

**EN**  
Safer string copy with size limitation.  
**Implementation**: Copies up to dstsize-1 chars, always null-terminates. Returns length of src.

**CN**  
带长度限制的安全字符串复制。  
**实现**：最多复制dstsize-1个字符，始终以'\0'结尾。返回src的长度。

**Edge Cases / 边界处理**:
- If dstsize = 0 → nothing copied, return src length / dstsize为0则不复制
- If src longer than dstsize-1 → truncation / 源串过长则截断

---

### `size_t ft_strlcat(char *dst, const char *src, size_t size)`

**EN**  
Safer string concatenation with size limitation.  
**Implementation**: Appends src to dst, ensures total length ≤ size. Returns total length attempted.

**CN**  
带长度限制的安全字符串拼接。  
**实现**：将src追加到dst末尾，确保总长度不超过size。返回尝试创建的总长度。

**Note / 注意**:  
This function has tricky edge cases when size = 0 or dst is not null-terminated.  
当size = 0或dst不以'\0'结尾时，行为需要特别处理。

---

### `char *ft_strchr(const char *s, int c)`

**EN**  
Locates first occurrence of a character in a string.  
**Implementation**: Iterates through string, returns pointer to first match. Special handling for '\0'.

**CN**  
在字符串中查找首个匹配字符。  
**实现**：遍历字符串，返回首个匹配字符的指针。单独处理查找'\0'的情况。

```c
while (*s)
{
    if (*s == (char)c)
        return ((char *)s);
    s++;
}
if ((char)c == '\0')
    return ((char *)s);
return (NULL);
```

---

### `char *ft_strrchr(const char *s, int c)`

**EN**  
Locates last occurrence of a character in a string.  
**Implementation**: Uses ft_strlen to find the end, then searches backwards.

**CN**  
在字符串中查找最后一个匹配字符。  
**实现**：先用`ft_strlen`定位到末尾，再从后向前遍历查找。

---

### `int ft_strncmp(const char *s1, const char *s2, size_t n)`

**EN**  
Compares two strings up to n characters.  
**Implementation**: Compares char by char, returns ASCII difference of first differing chars.

**CN**  
比较两个字符串的前n个字符。  
**实现**：逐字符比较，返回第一个不同字符的ASCII差值。

---

### `char *ft_strdup(const char *s1)`

**EN**  
Creates a duplicate of a string (dynamic allocation).  
**Implementation**: Allocates memory with malloc, copies string char by char.

**CN**  
复制字符串（动态分配内存）。  
**实现**：`malloc`分配空间，逐字符复制，以'\0'结尾。

**Memory / 内存**:  
Caller must free() the returned pointer.  
调用者必须free()返回的指针。

---

### `char *ft_substr(char const *s, unsigned int start, size_t len)`

**EN**  
Extracts a substring from a string.  
**Implementation**: If start beyond string length → empty string. Adjusts len if too long. Allocates and copies.

**CN**  
提取子字符串。  
**实现**：若起始位置超出原串长度 → 返回空串；若len超出可用长度 → 截断。分配内存并复制。

```c
if (start >= s_len)
    return (ft_strdup(""));
if (len > s_len - start)
    len = s_len - start;
// allocate and copy
```

---

### `char *ft_strjoin(char const *s1, char const *s2)`

**EN**  
Concatenates two strings into a new allocation.  
**Implementation**: Calculates total length, allocates memory, copies s1 then s2.

**CN**  
拼接两个字符串（新分配内存）。  
**实现**：计算总长度，分配内存，依次复制s1和s2。

---

### `char *ft_strtrim(char const *s1, char const *set)`

**EN**  
Removes specified characters from beginning and end of string.  
**Implementation**: Helper `ft_in_set` checks if char in set. Finds first and last non-set chars, creates substring.

**CN**  
移除字符串首尾指定字符集。  
**实现**：辅助函数`ft_in_set`判断字符是否在集合中。从首尾分别找到第一个不在集合中的字符位置，截取中间部分。

---

### `char *ft_itoa(int n)`

**EN**  
Converts an integer to a string.  
**Implementation**: Handles negatives and zero. Static helper `ft_count` calculates needed length. Fills string from the end.

**CN**  
整数转字符串。  
**实现**：处理负数与零。静态辅助函数`ft_count`计算所需长度。从末尾向前填充数字（取模10）。

```c
// Example: n = -123
// 1. Count len = 4 ('-','1','2','3')
// 2. Allocate 5 bytes (len + 1)
// 3. Fill from end: '3' -> '2' -> '1' -> '-'
```

---

### `char *ft_strmapi(char const *s, char (*f)(unsigned int, char))`

**EN**  
Creates new string by applying function f to each character with its index.  
**Implementation**: Allocates new string, iterates through original, calls f(index, char).

**CN**  
对字符串每个字符应用函数，生成新串。  
**实现**：分配新字符串，遍历原串，对每个位置调用`f(index, char)`。

---

### `void ft_striteri(char *s, void (*f)(unsigned int, char*))`

**EN**  
Applies function f to each character of a string (modifies in place).  
**Implementation**: Passes address of each character to f, allowing direct modification.

**CN**  
对字符串每个字符应用函数（原地修改）。  
**实现**：遍历字符串，将每个字符的地址传给f，直接修改原串。

---

### `char **ft_split(char const *s, char c)`

**EN**  
Splits a string into an array of strings using a delimiter.  
**Implementation**:  
- `ft_count`: Counts words  
- `ft_empty`: Handles zero words case  
- `ft_fill`: Creates substrings with ft_substr  
- `ft_free_split`: Frees all allocations if any step fails

**CN**  
按分隔符分割字符串为字符串数组。  
**实现**：  
- `ft_count`：统计单词数量  
- `ft_empty`：处理0个单词的情况  
- `ft_fill`：用`ft_substr`逐个提取单词  
- `ft_free_split`：分配失败时释放已分配内存

**Memory Pattern / 内存模式**:
```
Returned array: [ptr1][ptr2][ptr3][NULL]
                    ↓     ↓     ↓
                 "word1" "word2" "word3"
```

---

### `char *ft_strnstr(const char *haystack, const char *needle, size_t len)`

**EN**  
Locates a substring in a string, limited to len characters.  
**Implementation**: Empty needle → return haystack. Nested loops to compare within len bound.

**CN**  
在字符串中查找子串（长度限制）。  
**实现**：空needle直接返回haystack。双层循环，在len范围内逐位比较。

---

## 🧠 Memory Functions / 内存操作

---

### `void *ft_memset(void *b, int c, size_t len)`

**EN**  
Fills memory with a constant byte.  
**Implementation**: Casts to unsigned char*, sets each byte to (unsigned char)c.

**CN**  
将内存区域填充为指定字节。  
**实现**：强转为`unsigned char*`，逐字节赋值为`(unsigned char)c`。

---

### `void ft_bzero(void *s, size_t n)`

**EN**  
Zeroes out memory.  
**Implementation**: Casts to unsigned char*, sets each byte to 0.

**CN**  
将内存区域清零。  
**实现**：强转为`unsigned char*`，逐字节赋0。

---

### `void *ft_memcpy(void *dst, const void *src, size_t n)`

**EN**  
Copies memory from source to destination (no overlap handling).  
**Implementation**: Casts both to unsigned char*, copies byte by byte.

**CN**  
内存拷贝（不考虑重叠）。  
**实现**：强转为`unsigned char*`，逐字节复制。

**Warning / 警告**:  
Undefined behavior if src and dst overlap.  
src和dst重叠时行为未定义。

---

### `void *ft_memmove(void *dst, const void *src, size_t len)`

**EN**  
Copies memory handling overlapping regions.  
**Implementation**: If dst > src (possible overlap), copy from end backwards; otherwise use ft_memcpy.

**CN**  
内存拷贝（处理重叠区域）。  
**实现**：若dst > src（可能存在重叠），从末尾向前复制；否则使用`ft_memcpy`。

```c
if (d > s)
    while (len--)
        d[len] = s[len];
else
    ft_memcpy(d, s, len);
```

---

### `void *ft_memchr(const void *s, int c, size_t n)`

**EN**  
Locates first occurrence of a byte in memory.  
**Implementation**: Casts to unsigned char*, iterates through n bytes, returns pointer to first match.

**CN**  
在内存中查找指定字节。  
**实现**：强转为`unsigned char*`，遍历n个字节，返回首个匹配位置的指针。

---

### `int ft_memcmp(const void *s1, const void *s2, size_t n)`

**EN**  
Compares two memory regions.  
**Implementation**: Casts to unsigned char*, compares byte by byte, returns difference of first differing byte.

**CN**  
比较两块内存区域。  
**实现**：强转为`unsigned char*`，逐字节比较，返回首个不同字节的差值。

---

### `void *ft_calloc(size_t count, size_t size)`

**EN**  
Allocates memory for an array and zeroes it.  
**Implementation**: Allocates count × size bytes, sets each byte to 0.

**CN**  
分配并清零内存。  
**实现**：分配`count × size`字节，逐字节赋0，返回指针。

**Special Rule / 特殊规则**:  
If count or size is 0, returns a unique pointer that can be passed to free().  
若count或size为0，返回一个可被free()的唯一指针。

---

## 📤 File Descriptor Output / 文件描述符输出

---

### `void ft_putchar_fd(char c, int fd)`

**EN**  
Writes a character to a file descriptor.  
**Implementation**: Wrapper for `write(fd, &c, 1)`.

**CN**  
向指定文件描述符输出字符。  
**实现**：封装`write(fd, &c, 1)`。

---

### `void ft_putstr_fd(char *s, int fd)`

**EN**  
Writes a string to a file descriptor.  
**Implementation**: Iterates through string, writing each char with write.

**CN**  
向指定文件描述符输出字符串。  
**实现**：遍历字符串，逐个字符`write`。

---

### `void ft_putendl_fd(char *s, int fd)`

**EN**  
Writes a string followed by a newline to a file descriptor.  
**Implementation**: ft_putstr_fd + write newline.

**CN**  
输出字符串并换行。  
**实现**：`ft_putstr_fd`输出字符串，再`write`一个换行符。

---

### `void ft_putnbr_fd(int n, int fd)`

**EN**  
Writes an integer to a file descriptor.  
**Implementation**: Handles negatives, recursive function: writes higher digits first, then last digit.

**CN**  
输出整数。  
**实现**：负数先输出'-'并取正。递归函数：先递归输出高位，最后输出个位数字。

```c
if (num < 0)
{
    write(fd, "-", 1);
    num = -num;
}
if (num >= 10)
    ft_putnbr_fd(num / 10, fd);
ft_putchar_fd((num % 10) + '0', fd);
```

---

## 🔄 Conversion Functions / 类型转换

---

### `int ft_atoi(const char *str)`

**EN**  
Converts a string to an integer.  
**Implementation**:  
1. Skip whitespace (space, tab, newline, etc.)  
2. Handle optional '+' or '-' signs, reject multiple signs  
3. Convert consecutive digits: `result = result × 10 + (*str - '0')`  
4. Apply sign and return

**CN**  
字符串转整数。  
**实现**：  
1. 跳过空白字符（空格、制表、换页等）  
2. 处理可选的正负号，禁止多个符号  
3. 连续转换数字字符  
4. 应用符号位后返回

```c
while (*str == ' ' || (*str >= 9 && *str <= 13))
    str++;
// handle signs...
while ('0' <= *str && *str <= '9')
    result = result * 10 + (*str++ - '0');
return (sign * result);
```

---

## 🔗 Linked List Functions / 链表操作

---

### Structure Definition / 结构定义

```c
typedef struct s_list
{
    void            *content;  // Data stored in node / 节点存储的数据
    struct s_list   *next;     // Pointer to next node / 指向下一个节点
}                   t_list;
```

---

### `t_list *ft_lstnew(void *content)`

**EN**  
Creates a new list node.  
**Implementation**: Allocates memory for t_list, sets content pointer, initializes next to NULL.

**CN**  
创建新链表节点。  
**实现**：为`t_list`分配内存，content指向传入数据，next初始化为NULL。

---

### `void ft_lstadd_front(t_list **lst, t_list *new)`

**EN**  
Adds a node at the beginning of the list.  
**Implementation**: new→next points to current head, update head pointer to new.

**CN**  
将节点插入链表头部。  
**实现**：new->next指向原头节点，更新头指针为new。

---

### `int ft_lstsize(t_list *lst)`

**EN**  
Counts the number of nodes in the list.  
**Implementation**: Iterates through the list until NULL, increments counter.

**CN**  
统计链表节点数量。  
**实现**：遍历链表至NULL，计数累加。

---

### `t_list *ft_lstlast(t_list *lst)`

**EN**  
Returns the last node of the list.  
**Implementation**: Iterates until next is NULL.

**CN**  
返回链表最后一个节点。  
**实现**：遍历至next为NULL的节点。

---

### `void ft_lstadd_back(t_list **lst, t_list *new)`

**EN**  
Adds a node at the end of the list.  
**Implementation**: If list empty → set head to new. Otherwise find last node and set its next to new.

**CN**  
将节点追加至链表尾部。  
**实现**：若链表为空则直接设为头节点；否则找到尾节点，将其next指向new。

---

### `void ft_lstdelone(t_list *lst, void (*del)(void*))`

**EN**  
Deletes a single node.  
**Implementation**: Calls del on node's content, then frees the node itself.

**CN**  
删除单个节点。  
**实现**：调用del函数释放节点存储的数据，然后释放节点本身。

**Note / 注意**:  
Does NOT free the next node.  
不释放下一个节点。

---

### `void ft_lstclear(t_list **lst, void (*del)(void*))`

**EN**  
Deletes an entire list and sets head to NULL.  
**Implementation**: Iterates through list: store next, delete current, move to next. Finally set *lst = NULL.

**CN**  
删除整个链表。  
**实现**：遍历链表，先用临时指针保存next，再删除当前节点，最后将头指针置NULL。

---

### `void ft_lstiter(t_list *lst, void (*f)(void *))`

**EN**  
Iterates through the list and applies function f to each node's content.  
**Implementation**: While loop, call f on each node's content.

**CN**  
遍历链表并对每个节点的内容应用函数。  
**实现**：循环遍历，对每个节点的content调用f。

---

### `t_list *ft_lstmap(t_list *lst, void *(*f)(void *), void (*del)(void *))`

**EN**  
Creates a new list by applying function f to each node's content.  
**Implementation**:  
1. Create empty new list  
2. For each node: apply f to content, create new node with result  
3. If allocation fails, clear new list using del  
4. Return head of new list

**CN**  
对链表每个节点应用函数，生成新链表。  
**实现**：  
1. 创建空链表  
2. 遍历原链表，对每个节点的content应用f，用返回值创建新节点  
3. 若任意节点分配失败，用del清除已创建的新链表并返回NULL  
4. 返回新链表头指针

**Memory Safety / 内存安全**:  
If any node allocation fails, already created nodes are properly freed.  
若任一节点分配失败，已创建的节点会被正确释放。

---

## ⚠️ Edge Cases & Defensive Programming / 边界处理与防御性编程

| Scenario / 场景 | Handling / 处理方式 |
|-----------------|---------------------|
| **NULL pointers / 空指针** | String functions return 0 or NULL; list functions return/exit early / 字符串函数返回0或NULL；链表函数提前返回 |
| **Zero allocation / 零长度分配** | ft_calloc returns pointer that can be freed / 返回可被free的有效指针 |
| **Allocation failure / 分配失败** | Return NULL, clean up already allocated memory / 返回NULL，清理已分配内存 |
| **Empty string / 空字符串** | ft_split returns array with NULL; ft_strtrim returns empty string / ft_split返回含NULL的数组；ft_strtrim返回空串 |
| **Integer overflow / 整数溢出** | ft_atoi follows standard C behavior (truncation) / 遵循标准C行为（截断） |
| **Memory overlap / 内存重叠** | ft_memmove专门处理；ft_memcpy不考虑 |
