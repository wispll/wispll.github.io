---
title: bash笔记
date: 2022-06-21 18:10:41
tags: bash
categories: bash
---

```bash

#声明数组
array=(value1 value2 value3)

#声明键值对
declare -A dict
dict=(
    [key1]=value1       
    [key2]=value2
)

#数组
for index in ${!array[@]}
do
    printf "index:%s\n value:%s\n" "$index" "${array[$index]}"
done

for value in ${array[@]}
do
    .....
done

printf “length:%s\n” "${#array[@]}"

#其他
bash不能直接进行浮点数运算。可以通过bc或awk间接运算

修改的文件数据，不能再通过重定向写回文件。可通过sponge解决
grep '...' file > file  #error
grep '...' file | sponge file

```
