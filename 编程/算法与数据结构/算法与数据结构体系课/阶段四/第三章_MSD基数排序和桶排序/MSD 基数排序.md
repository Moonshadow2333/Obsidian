## 什么是MSD

MSD 是 **M**ost **S**ignificant **D**igit 单词的缩写。
 
MSD 基数排序是从前往后计数排序

与之相对应的有LSD，即**L**east **S**ignificant **D**igit，是从后往前排的计数排序，只适用于等长字符串。

而 MSD 则：**可用于不等长字符串的排序**。

## 思路

第 i 轮过后，第 i 列的字符是有序的，例如 AAABBBCCC，把第 i 列字符相同的字符串分成一组，对这一组字符串执行相同的操作。
