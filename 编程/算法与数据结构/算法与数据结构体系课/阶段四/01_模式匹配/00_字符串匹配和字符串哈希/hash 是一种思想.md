暴力匹配：每次匹配，最差的情况下，重新扫描一遍匹配字符串 t；

改进：比较两个字符串是否相等的时间复杂度是 O(n)；比较两个整数是否相等的时间复杂度是 O(1)；

把字符串是否匹配转换成整数的值是否匹配的思想就是哈希的思想；

之前的哈希表的课程就介绍过，只要哈希函数设计的合理，任何的对象，数据集合都可以转换成整数。

但是还是存在哈希冲突的可能，但是如果只在哈希冲突的时候才去进行匹配，就能大大地减少运算的次数。


## LeetCode 1147 号问题

双指针

把字符串转换为哈希值，每次比较哈希值

每添加一个字符，新的哈希值计算：

| 方向 | 计算方式                           | 例子                         |
| ---- | ---------------------------------- | ---------------------------- |
| 前面 | hashcode \* B + newchar            | 123->1234 123 \* 10 + 4      |
| 后面 | newchar \* B\^(len - 1) + hashcode | 123->4123 4 \* (10\^3) + 123 |

递归解决
字符串比较
```PHP
<?php

  

class LongestDeComposition {

    public function longestDeComposition ($text) {

        return $this->solve($text, 0, strlen($text) - 1);

    }

  

    // s[left, right]

    public function solve ($s, $left, $right) {

        if ($left > $right) {

            return 0;

        }

  

        for ($i = $left, $j = $right; $i < $j; $i ++, $j --) {

            // s[left, i] == s[j, right]

            if ($this->isEqual($s, $left, $i, $j, $right)) {

                return 2 + $this->solve($s, $i + 1, $j - 1);

            }

        }

  

        return 1;

    }

  

    // s[l1, r1] == s[l2, r2]; ?

    protected function isEqual ($s, $l1, $r1, $l2, $r2) {

        for ($i = $l1, $j = $l2; $i <= $r1 && $j <= $r2; $i++, $j++) {

            if ($s[$i] != $s[$j]) {

                return false;

            }

        }

        return true;

    }

}
```

哈希比较

```PHP
<?php

  

class LongestDeComposition {

    protected $MOD = 10^9 + 7;

    protected $pow26 = [];

    public function longestDeComposition ($text) {

        $this->pow26[0] = 1;

        for ($i = 1; $i < strlen($text); $i ++) {

            $this->pow26[$i] = $this->pow26[$i - 1] * 26 % $this->MOD;

        }

        return $this->solve($text, 0, strlen($text) - 1);

    }

    // s[left, right]

    public function solve ($s, $left, $right) {

        if ($left > $right) {

            return 0;

        }

  

        $preHash = $postHash = 0;

        for ($i = $left, $j = $right; $i < $j; $i ++, $j --) {

            // s[left, i] == s[j, right]

            $preHash = ($preHash * 26 + ord($s[$i])) % $this->MOD;

            $postHash = (ord($s[$j]) * $this->pow26[$right - $j] + $postHash) % $this->MOD;

            if ($preHash == $postHash && $this->isEqual($s, $left, $i, $j, $right)) {

                return 2 + $this->solve($s, $i + 1, $j - 1);

            }

        }

  

        return 1;

    }

  

    // s[l1, r1] == s[l2, r2]; ?

    protected function isEqual ($s, $l1, $r1, $l2, $r2) {

        for ($i = $l1, $j = $l2; $i <= $r1 && $j <= $r2; $i++, $j++) {

            if ($s[$i] != $s[$j]) {

                return false;

            }

        }

        return true;

    }

}
```