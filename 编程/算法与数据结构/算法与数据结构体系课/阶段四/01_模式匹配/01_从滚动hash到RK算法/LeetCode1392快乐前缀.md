
## 暴力解法

```PHP
<?php

  

class LongestPreFix {

    public function solve ($s) {

        // s[0,...,len - 1] ~ s[s.length - len,...,s.length - 1]

        for ($len = strlen($s) - 1; $len >= 1; $len --) {

            if ($this->isEqual($s, 0, $len, strlen($s) - $len, strlen($s) - 1)) {

                return substr($s, 0, $len);

            }

        }

        return "";

    }

  

    protected function isEqual ($s, $l1, $r1, $l2, $r2) {

        for ($i = $l1, $j = $l2; $i <= $r1 && $j <= $r2; $i++, $j++) {

            if ($s[$i] != $s[$j]) {

                return false;

            }

        }

        return true;

    }

  

    public static function Main () {

        $obj = new LongestPreFix();

        $s = 'level';

        $res = $obj->solve($s);

        var_dump($res);

    }

}

  

LongestPreFix::Main();
```

## hash

除法
预处理，从短字符串的哈希计算到长字符串的哈希，把中间的计算结果存储起来

```PHP
<?php

  

class LongestPreFix {

    protected $MOD = 10^9 + 7;

    protected $pow26 = [];

    // 从短字符串的哈希计算到长字符串的哈希，把中间的计算结果存储起来

    public function solve ($s) {

        $this->pow26[0] = 1;

        for ($i = 1; $i < strlen($s); $i ++) {

            $this->pow26[$i] = $this->pow26[$i - 1] * 26 % $this->MOD;

        }

        $preHash = [];

        $preHash[0] = ord($s[0]);

        for ($i = 1; $i < strlen($s); $i ++) {

            $preHash[$i] = ($preHash[$i - 1] * 26 + ord($s[$i])) % $this->MOD;

        }

        $postHash = [];

        $postHash[strlen($s) - 1] = ord($s[strlen($s) - 1]);

        for ($j = strlen($s) - 2; $j >= 1; $j --) {

            $postHash[$j] = (ord($s[$j]) * $this->pow26[strlen($s) - $j - 1] + $postHash[$j + 1]) % $this->MOD;

        }

        // s[0,...,len - 1] ~ s[s.length - len,...,s.length - 1]

        for ($len = strlen($s) - 1; $len >= 1; $len --) {

            if ($preHash[$len - 1] == $postHash[strlen($s) - $len] && $this->isEqual($s, 0, $len, strlen($s) - $len, strlen($s) - 1)) {

                return substr($s, 0, $len);

            }

        }

        return "";

    }

  

    protected function isEqual ($s, $l1, $r1, $l2, $r2) {

        for ($i = $l1, $j = $l2; $i <= $r1 && $j <= $r2; $i++, $j++) {

            if ($s[$i] != $s[$j]) {

                return false;

            }

        }

        return true;

    }

  

    public static function Main () {

        $obj = new LongestPreFix();

        $s = 'level';

        $res = $obj->solve($s);

        var_dump($res);

    }

}

  

LongestPreFix::Main();
```