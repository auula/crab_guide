## `tuple`元组

`tuple`是`复合类型`可以存储多个不同类型的数据，`复合类型`就像我们的菜篮子，里面可以放各种类型的菜。

- `tuple`长度是固定的，而且一旦定义了，就不能再次更改。
- `tuple`是下标从`0`开始。

## `tuple`元组的定义

在定义的时候可以指定存储的数据类型：

```rust linenums='1'
let tuple_name:(data_type1,data_type2,data_type3) = (value1,value2,value3);
```

`Rust` 中元组的定义很简单，就是使用一对小括号 `()` 把所有元素放在一起，元素之间使用逗号 `,` 分隔，当然也可以忽略类型声明。

```rust linenums='1'
let tuple_name = (v1,v2,v3)
```


## `tuple`元组的使用

- 下标访问
- 解构赋值

我们可以使用 `元组名.索引数字` 来访问元组中相应索引位置的元素。索引从 `0` 开始。

如果要输出元组中的所有元素，必须使用 `{:?}` 格式化符：

```rust linenums='1'
fn main() {
    let tuples: (&'static str, i8, f64) = ("🦀", 22, 3.1415927);
    println!("{:?}", tuples);
    // 声明一个可变的tuple
    let mut people = ("tom", "robin", "jarvib");
    // 通过下标访问
    println!("{},{},{}", people.0, people.1, people.2);
    // 修改下标为2的值
    people.2 = "Jarvib Ding";
    // 通过 解构赋值 (destructing)
    let (v1, v2, v3) = people;
    println!("{},{},{}", v1, v2, v3);
}
```
output:
```rust linenums='1'
("🦀", 22, 3.1415927)
tom,robin,jarvib
tom,robin,Jarvib Ding
```

`tuple`即`元组`，元组类型是由多个不同类型的元素组成的复合类型，通过`()`小括号把元素组织在一起成一个新的数据类型。元组的长度在定义的时候就已经是固定的了，不能修改，如果指定了元素的数据类型，那么你的元素就要对号入座！！！否则编译器会教训你！

```rust linenums='1'
fn main() {
    // 指定数据类型
    let tup_type:(i8,i32,bool) = (21,-1024,true);
    // 解构元素
    let (one,two,three) = tup_type;
    // 二维的元组
    let tup_2d:(f64,(i8,i32,bool)) = (3.1415927,(one,two,three));
    println!("tup_2d = {:?}",tup_2d);
    // 索引
    println!("π = {:?}",tup_2d.0);
}
```

元组的访问方式有好几种，通过下标去访问，也可以使用解构赋值给新的变量去访问，但是不支持迭代器去访问。

```rust
for v in tup_2d.1.iter() {
        println!("{}",v)
}
```

```bash
   Compiling playground v0.0.1 (/playground)
error[E0599]: no method named `iter` found for tuple `(i8, i32, bool)` in the current scope
  --> src/main.rs:10:23
   |
10 |     for v in tup_type.iter() {
   |                       ^^^^ method not found in `(i8, i32, bool)`

error: aborting due to previous error

For more information about this error, try `rustc --explain E0599`.
error: could not compile `playground`

To learn more, run the command again with --verbose.
```

`元组`的每个元素的类型可以不同，因此您无法对其进行迭代。元组甚至不能保证以与类型定义相同的顺序存储数据，因此即使您自己为它们实现`Iterator`，它们也不适合进行有效的迭代。

但是如果元素是支持实现了`Iterator`就可以通过`.iter()`进行迭代访问。

```rust
    let mut arrays:[usize;5] = [0;5];
    
    for i in 0..5 {
        arrays[i] = i+1;
    }
    
    println!("{:?}",arrays);
    
    let tup_arr:(&str,[usize;5]) = ("tup_arr",arrays);
    
    println!("{:?}",tup_arr);
    
    for v in tup_arr.1.iter() {
        println!("{}",v)
    }
```
例如上的元素是一个`array`，`Rust`中的数组和其他语言一样，一组类型相同的元素组成的复合类型，数组在底层存储是一块连续的内存空间。

[点击查看元组代码案例](https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=195d35086371375f182fc67922d81b44)