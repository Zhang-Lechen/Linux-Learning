参考文章
[写给VS code用户的vim入坑指南](https://www.ahonn.me/blog/the-vim-guide-for-vs-code-users)

# 基础模式之间转化

<img src="https://user-images.githubusercontent.com/75344279/136719546-eb2a7410-79d5-425c-950a-5b4dd27f4cd6.png" alt=drawing width="600">

<img src="https://user-images.githubusercontent.com/75344279/136719608-0a48bee8-dda8-4a58-b9dd-e7fb2f4ec4fc.png" alt=drawing width="600">

<img src="https://user-images.githubusercontent.com/75344279/136719705-0882382c-7b75-4c3e-8328-792f17b56568.png" alt=drawing width="600">

# 常用快捷键

+ 光标移动

h👈，l👉，j👆，k👇
-------
+ w跳到一个单词的开头
+ b跳到本单词或上一个单词开头（如果光标已经在本单词开头，则跳到上一个单词的开头，否则跳到本单词的开头）
+ e跳到本单词或下一个单词结尾（同b的解释）
+ ge跳到上一个单词的结尾
------
+ 0跳到行首
+ ^跳到行首第一个非空字符
+ \$跳到行尾
+ gg跳到第一行
+ G跳到最后一行

-----
+ f{char}跳到下一个char所在的位置
+ F{char}跳到上一个char所在的位置
+ t{char}跳到下一个char之前的一个字符
+ T{char}跳到上一个char之后的一个字符
+ ;重复上一个字符查找的操作
+ ,反向上一个字符查找的操作

-----
<img src="https://user-images.githubusercontent.com/75344279/136721902-0c811f96-3b81-4502-8a09-18c9a54c1b96.png" alt=drawing width="600">

<img src="https://user-images.githubusercontent.com/75344279/136722221-08bf095f-b896-4827-926c-1fc8943258c8.png" alt=drawing width="600">

操作符
+ d(delete) 删除 dd能够删除一整行
+ c(change) 修改（删除并进入插入模式）
+ y(yank) 复制
+ v(visual) 选中并进入visual模式
+ p 粘贴
+ u 撤销动作和操作符
