# 快速排序学习记录

## 简介

在数组中找一个标定点 p，把数组中小于 arr[p] 元素放到 arr[p] 的左边，把大于等于 arr[p] 的元素放到 arr[p] 的右边，即：

- 在区间 [0, p - 1] 内的元素小于 arr[p]；
- 在区间 [p + 1, count(arr) - 1] 内的元素大于 arr[p]。

再分别对 arr[0,...,p - 1]、arr[p + 1,...,count(arr) - 1] 进行递归排序。

如果用以上思路去排序一个完全无序的数组，时间复杂度会是 O(nlgn)，但是有两种特例会出现性能退化的现象，时间复杂度会变成 O(n^2)：

- 数组完全有序，例如 [1, 2, 3, 4]；
- 数组中的所有元素都相同，例如 [0, 0, 0]。

为了避免出现因为数组完全有序而导致算法性能退化的现象，使用了**随机化**的方法，即在区间 [l, r] 内随机选一个元素，与 arr[l] 交换，把交换后的 arr[l] 作为标定点，而不是直接把 arr[l] 作为标定点。

而数组中所有元素都相同导致性能退化的问题的解决方法则是使用双路快排：

三路快排则是对双路快排的进一步优化。

## 单路快速排序

```PHP
<?php

class OneWayQuickSort
{
    public function sort(&$arr)
    {
        $this->oneWaySort($arr, 0, count($arr) - 1);
    }

    protected function oneWaySort(&$arr, $l, $r)
    {
        if ($l >= $r) {
            return;
        }
        $p = $this->partition($arr, $l, $r);
        $this->oneWaySort($arr, $l, $p - 1);
        $this->oneWaySort($arr, $p + 1, $r);
    }

    protected function partition(&$arr, $l, $r)
    {
        // 原地分割
        // arr[l+1,...,j] < v; arr[j+1,...,i-1] >= v
        $j = $l;
        for ($i = $l + 1; $i <= $r; $i++) {
            if ($arr[$i] < $arr[$l]) {
                $j ++;
                $this->swap($arr, $i, $j);
            }
        }
        $this->swap($arr, $l, $j);
        return $j;
    }

    protected function swap(&$arr, $i, $j)
    {
        $temp = $arr[$i];
        $arr[$i] = $arr[$j];
        $arr[$j] = $temp;
    }

    public static function Main()
    {
        $arr = [1,3,5,7,2,4,6,8];
        (new OneWayQuickSort())->sort($arr);
        $result = '['.implode(', ', $arr).']';
        echo $result;
    }
}

OneWayQuickSort::Main();
// [1, 2, 3, 4, 5, 6, 7, 8]
```

## 双路快速排序

```PHP
<?php

class TwoWaysQuickSort
{
    public function sort(&$arr)
    {
        $this->twoWaysSort($arr, 0, count($arr) - 1);
    }

    protected function twoWaysSort(&$arr, $l, $r)
    {
        if ($l >= $r) {
            return;
        }
        $p = $this->partition($arr, $l, $r);
        $this->twoWaysSort($arr, $l, $p - 1);
        $this->twoWaysSort($arr, $p + 1, $r);
    }

    protected function partition(&$arr, $l, $r)
    {
        // 随机化，避免因有序数组出现性能退化的问题
        // 在区间[l, r]中取一个数k，交换arr[l]和arr[k]
        $k = mt_rand($l, $r);
        $this->swap($arr, $l, $k);
        // arr[l+1,...,i - 1] <= v; arr[j + 1,...,r] >= v
        $i = $l + 1;
        $j = $r;
        while (true) {
            while ($i <= $j && $arr[$i] < $arr[$l]) {
                $i ++;
            }
            while ($j >= $i && $arr[$j] > $arr[$l]) {
                $j --;
            }
            if ($i >= $j) {
                // 循环终止条件，但 i 和 j 相等时，循环终止。
                break;
            }
            $this->swap($arr, $i, $j);
            $i ++;
            $j --;
        }
        $this->swap($arr, $l, $j);
        return $j;
    }

    protected function swap(&$arr, $i, $j)
    {
        $temp = $arr[$i];
        $arr[$i] = $arr[$j];
        $arr[$j] = $temp;
    }

    public static function Main()
    {
        $arr = [1,3,5,7,2,4,6,8];
        (new TwoWaysQuickSort())->sort($arr);
        $result = '['.implode(', ', $arr).']';
        echo $result;
    }
}

TwoWaysQuickSort::Main();
// [1, 2, 3, 4, 5, 6, 7, 8]
```

- 循环不变量是什么？
  - arr[l + 1,...,i - 1] <= arr[l];
  - arr[j + 1,...,r] >= arr[l];
- 每个变量的定义是什么？
  - i：指针，从前往后找；
  - j：指针，从后往前找。
- 每个变量的初值该怎么取？
  - i = l - 1;
  - j = r + 1;
- 循环的终止条件是什么？
  - 当 i >= j 时终止循环。
- 在循环的过程中 i、j 该如何维护？
  1. i：从前往后找，遇到第一个小于等于标定点的元素就停止；
  2. j：从后往前找，遇到第一个大于大于标定点的元素就停止；
  3. 交换 arr[i]，arr[j] 的值；
  4. i ++，j--。

在循环结束之后，需要交换 arr[l] 和 arr[j] 的值。

注意：循环结束之后为什么不是交换 arr[l] 和 arr[i] 的值，而是交换 arr[l] 和 arr[j] 的值呢？

在最后一轮循环中，即在循环结束之前，从后往前，j 指向的是数组中第一个小于标定点 arr[l] 的值，而且 i >= j，**即 j 前面的元素都是小于等于标定点的，j 后面的值都是大于等于标定点的，故 arr[l] 是和 arr[j] 交换而非 arr[i] 交换**。

## 三路快速排序

```PHP
<?php

class ThreeWaysQuickSort
{
    public function sort(&$arr)
    {
        $this->threeWaysSort($arr, 0, count($arr) - 1);
    }

    protected function threeWaysSort(&$arr, $l, $r)
    {
        if ($l >= $r) {
            return;
        }
        $result = $this->partition($arr, $l, $r);
        $lt = $result['lt'];
        $gt = $result['gt'];
        $this->threeWaysSort($arr, $l, $lt);
        $this->threeWaysSort($arr, $gt, $r);
    }

    protected function partition(&$arr, $l, $r)
    {
        $k = mt_rand($l, $r);
        $this->swap($arr, $l, $k);
        // 定义循环不变量 arr[l,...,lt] < v; arr[lt + 1,...,gt - 1] = v; arr[gt,...,r] > v
        // 定义 lt、gt、i
        // lt 最后一个小于 v 的元素所在的位置；
        // gt 第一个大于 v 的元素所在的位置。
        $lt = $l;
        $gt = $r + 1;
        $i = $l + 1;
        $v = $arr[$l];
        while ($i < $gt) {
            if ($arr[$i] < $v) {
                $lt ++;
                $this->swap($arr, $i, $lt);
                $i++;
            } elseif ($arr[$i] > $v) {
                $gt --;
                $this->swap($arr, $i, $gt);
            } else {
                $i ++;
            }
        }
        // 循环结束后，因为需要将 arr[l] 与 arr[lt] 进行交换，
        $this->swap($arr, $l, $lt);
        // 故最终 arr[l,...,lt - 1] < v; arr[lt,...,gt - 1] = v; arr[gt,...,r] > v
        return [
            'lt' => $lt - 1,
            'gt' => $gt
        ];
    }

    protected function swap(&$arr, $i, $j)
    {
        $temp = $arr[$i];
        $arr[$i] = $arr[$j];
        $arr[$j] = $temp;
    }

    public static function Main()
    {
        $arr = [1,3,5,7,2,4,6,8];
        (new ThreeWaysQuickSort())->sort($arr);
        $result = '['.implode(', ', $arr).']';
        echo $result;
    }
}

ThreeWaysQuickSort::Main();
// [1, 2, 3, 4, 5, 6, 7, 8]
```

说实话三路快速排序的 partition 函数不是很好理解，一个循环涉及到了 lt、gt、i 三个变量，要做到正确地维护这些变量并不容易。

以后再写循环之前应该先问自己以下问题，回答清楚之后再动手写代码：

- 循环不变量是什么？
- 每个变量的定义是什么？
- 每个变量的初值该怎么取？
- 循环的终止条件是什么？
- 在循环的过程中 lt、gt、i 该如何维护？

三路快排的 partition 函数中的循环：

- 循环不变量？
  - arr[l,...,lt] < arr[l];
  - arr[lt+1,...,gt-1] = arr[l];
  - arr[gt,...,r] > arr[l]。
- 每个变量的含义是什么？
  - lt：arr[lt] 是最后一个小于 arr[l] 的元素；
  - gt：arr[gt] 是第一个大于 arr[l] 的元素；
  - i：用于遍历 arr[lt+1,...,r] 的工具人。
- 每个变量的初值该怎么取？
  - lt = l;
  - gt = r + 1;
  - i = l + 1。
- 循环的终止条件？
  - i >= gt 时循环终止。
- 在循环的过程中 lt、gt、i 该如何维护？
  - 当 arr[i] 小于 arr[l] 时，lt 先自增，再交换 arr[i] 和 arr[lt]，最后 i ++；
  - 当 arr[i] 大于 arr[l] 时，gt 先自减，再交换 arr[i] 和 arr[gt]；（注意这里并不需要 i ++，因为并不知道交换之前 arr[gt] 的值和 arr[l] 的值哪个大，需要等下轮循环进行判断）
  - 当 arr[i] 等于 arr[l] 时，自增 i 即可。

注意：循环结束之后，还需要交换 arr[l] 和 arr[lt] 的值，这样数组就有了这样的性质：

- arr[l,...,lt-1] < arr[l];
- arr[lt,...,gt-1] = arr[l];
- arr[gt,...,r] > arr[l]。

再对 arr[l,...,lt - 1]，arr[gt,...,r] 分别进行递归。

这里需要注意的是，因为在循环结束之后，交换了 arr[l] 和 arr [lt]，所以 arr[lt] 并不是最后一个小于 arr[l] 的元素了，**arr[lt - 1] 才是最后一个小于 arr[l] 的元素**，故是对 arr[l,...,lt - 1] 进行递归。

## 时间复杂度

为了避免因为数组完全有序导致算法性能退化，引入了随机化，所以即使是用同一个数组排序，虽然得到的结果相同，但处理的过程可能不同，换句话说，双路、三路快速排序算法都是随机算法。

随机算法的时间复杂度分析用的是期望。

对于双路还是三路快速排序算法，时间复杂度都是 O(nlgn)。

## 快速排序的应用

Select K 问题。

## 实践
【2024-03-28 22:48】partition 函数中，while true 循环中，第一个小循环找的是第一个大于等于arr\[l\] 的 i，第二个小循环找的是第一个小于等于 arr\[l\] 的 j，如果 i 大于等于 j，直接终止 while true 循环，否则就交换 i 和 j 的值，再维护 i 和 j 的值。 

while true 循环外面为什么是 l 和 j 的值交换，而不是 l 和 i 的值交换？之前提到 while true 循环中第一个循环终止时，i 就指向了第一个大于等于 arr\[l\] 的值，第二个循环终止时，j 就指向了第一个小于等于 arr\[l\] 的值，当 while true终止后，如果 l 和 i 交换并返回 i 的值，就不能保证标定点左侧的值全部小于等于标定点。

