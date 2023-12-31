## 什么是MSD

MSD 是 **M**ost **S**ignificant **D**igit 单词的缩写。
 
MSD 基数排序是从前往后计数排序

与之相对应的有LSD，即**L**east **S**ignificant **D**igit，是从后往前排的计数排序，只适用于等长字符串。

而 MSD 则：**可用于不等长字符串的排序**。

## 思路

在 [[01_LSD 基数排序|LSD 基数排序]]的学习中我们知道字符的[[ASCII]]值有 256 种，即 R = 256。如果用于排序等长字符串，R 为 256 完全够用，但是 MSD 可以排序不等长的字符串，即会出现 r 指向”空“的情况，这里的”空“指的不是空字符串，而是出界。例如排序 AC，ABC 这两个字符串，当 r 为 2 时，第一个字符就出界了（字符串的索引也是从 0 开始的），第二个字符串指向的是 C。

在 ASCII 的 256 个值中，没有一个表示出界的情况，所以我们就人为规定 0 表示出界的情况，并且其他字符的 ASCII 值整体往后挪一个位置，例如原来字符的 ASCII 值为 65，现在因为往后挪了一个位置，所以现在的 ASCII 值为 66。

因为新规定了 0 为字符出界，所以 ASCII 的值就多了一个，即 R = 256 + 1 = 257。故 cnt 数组要开辟 257 个空间。而 index 数组的空间要比 cnt 数组的多一个，即 index 的空间为 257 + 1 = 258。cnt 数组用于统计字符出现的频数，而 index 数组则用于计算字符的起始索引。

基本步骤

1. 统计频率；
2. 计算字符起始索引；
3. 在临时数组中排序；
4. 扔回原数组。

例子

以排序 BCA，CBAA，AC，BADFE，ABC，CBA 为例

| 0   | 1   | 2   | 3   | 4   |
| --- | --- | --- | --- | --- |
| B   | C   | A   |     |     |
| C   | B   | A   | A   |     |
| A   | C   |     |     |     |
| B   | A   | D   | F   | E   |
| A   | B   | C   |     |     |
| C   | B   | A   |     |     |

### 统计频数

当 r = 0 时，B C A B A C  
统计频数，A 2 B 2 C 2 即 cnt\[66\] = 2 cnt\[67\] = 2 cnt\[68\] = 2

```PHP
for ($i = $left; $i <= $right; $i ++) {

    // r 是否大于等于当前字符串的长度，          

    $ascii = $r >= strlen($arr[$i]) ? 0 : (self::letter2num($arr[$i][$r]) + 1); // TODO 这里为什么要加一？

    $cnt[$ascii] += 1;

}
```

### 计算每个字符起始索引

```PHP
for ($j = 0; $j < $R + 1 ; $j ++) { // index [0,...,257] 即 j + 1 < R + 2 故 j < R + 1

    $index[$j + 1] = $index[$j] + $cnt[$j];

}
```

index[1] = index[0] + cnt[0] = 0
index[2] = index[1] + cnt[1] = 0
...
index[66] = index[65] + cnt[65] = 0
index[67] = index[66] + cnt[66] = 2
index[68] = index[67] + cnt[67] = 4
index[69] = index[68] + cnt[68] = 6
index[70] = index[69] + cnt[69] = 6
...
index[257] = index[256] + cnt[256] = 6

index 数组如下：

[0 => 0, 1 => 0, ... , 65 => 0, 66 => 0, 67 => 2, 68 => 4, 69 => 6, 70 => 6, 71 => 6, ..., 257 => 6]

### 在临时数组中进行排序

- 遍历 arr[left] 到 arr[right] 这里的 left = 0，right = count(arr) - 1 = 5；
- 计算 arr[i][r] 的 ASCII 值，如果 r 出界，即 r 的值大于 arr[i] 字符串的长度，就为 0，否则的话就等于字符原本ASCII 值加一后的值。

```PHP
for ($i = $left; $i <= $right; $i ++) {

    $p = $r >= strlen($arr[$i]) ? 0 : (self::letter2num($arr[$i][$r]) + 1);

    $temp[$index[$p]] = $arr[$i];

    $index[$p] ++;

}
```

| temp[index[p]] = arr[i]           | index[p]++    |
| --------------------------------- | ------------- |
| temp[index[67]] = temp[2] = BCA   | index[67] = 3 |
| temp[index[68]] = temp[4] = CBAA  | index[68] = 5 |
| temp[index[66]] = temp[0] = AC    | index[66] = 1 |
| temp[index[67]] = temp[3] = BADFE | index[67] = 4 |
| temp[index[66]] = temp[1] = ABC   | index[66] = 2 |
| temp[index[68]] = temp[5] = CBA   | index[68] = 6 | 

临时数组 temp [0 => AC, 1 => ABC, 2 => BCA, 3 => BADFE, 4 => CBAA, 5 => CBA]

index 数组的更新如下：

[0 => 0, 1 => 0, ... , 65 => 0, **66 => 2, 67 => 4, 68 => 6**, 69 => 6, 70 => 6, 71 => 6, ..., 257 => 6]

### 扔回原数组中

```PHP
for ($k = $left; $k <= $right; $k ++) {

    $arr[$k] = $temp[$k - $left]; // 偏移量

}
```

arr 就变为 [0 => AC, 1 => ABC, 2 => BCA, 3 => BADFE, 4 => CBAA, 5 => CBA]

经过一轮排序之后：

| 0   | 1   | 2   | 3   | 4   |
| --- | --- | --- | --- | --- |
| A   | C   |     |     |     |
| A   | B   | C   |     |     |
| B   | C   | A   |     |     |
| B   | A   | D   | F   | E   |
| C   | A   | A   | A   |     |
| C   | B   | A   |     |     |

### 递归下去

通过上面表格我们知道，第零列已经是有序了，现在该怎么把剩下的列变得有序呢？

排序第一列，但是排序的范围不再是整个数组，而是第零列相同的字符串，以此类推，即

- 排序第二列，排序的范围是第一列相同的字符串；
- 排序第三列，排序的范围是第二列相同的字符串；
- 排序第四列，排序的范围是第三列相同的字符串。

这里有个问题，该如何确定排序的范围，换句话说，当排序第 r 列的时候，我怎么知道第 r - 1 相同字符串的范围呢？答案是利用 index 数组。

前面提到了，index 数组用于记录字符起始的位置，例如 A 字符一开始应该放在 temp 数组中索引为 0 的位置，维护一下字符 A 的索引，当下一次再遇到字符 A 时，就知道把字符 A 放到 temp 数组中的哪个位置，当循环结束时，index[ascii[A]] 的值就是下一个字符开始的位置。

- 第零列未排序前的 index 数组： [0 => 0, 1 => 0, ... , 65 => 0, 66 => 0, 67 => 2, 68 => 4, 69 => 6, 70 => 6, 71 => 6, ..., 257 => 6]

- 第零列排序后的 index 数组：[0 => 0, 1 => 0, ... , 65 => 0, **66 => 2, 67 => 4, 68 => 6**, 69 => 6, 70 => 6, 71 => 6, ..., 257 => 6]

A [0, 2- 1]
B [2, 4 - 1]
C [4, 6 -1]

我可能知道是什么回事，但是真的不好描述，先记住吧。

```PHP
for ($i = 0; $i < $R; $i ++) {

    $this->implementsort($arr, $left + $index[$i], $left + $index[$i + 1] - 1, $r + 1);

}
```


需要注意的是有偏移量。

创建了一个临时的数组 #算法-非原地排序
#算法-偏移

 ## 时间复杂度
O(w * n) w是最长的字符串长度