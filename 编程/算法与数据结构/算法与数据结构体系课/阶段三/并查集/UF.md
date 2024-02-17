# 并查集

并查集主要解决连接问题：

- 网络中节点的连接状态；
- 数学中集合的实现。

在学习并查集的时候，学习的是不断优化的过程。

1. 数组；
2. 子指父（孩子指向父亲）；
3. 加权；
4. rank；
5. 路径压缩一；
6. 路径压缩二。

## 各个版本的 UnionFind

### UnionFind 接口

```PHP
<?php

namespace Algorithm\UnionFind;

interface UF
{
    public function getSize(): int;
    public function isConected(int $p, int $q): bool;
    public function unionElements(int $p, int $q): void;
}
```

### 数组（quick-find）

```PHP
<?php

namespace Algorithm\UnionFind;

use Exception;

class UnionFind1 implements UF
{
    private array $id;
    public function __construct(int $size)
    {
        $this->id = range(0, $size - 1);
    }
    public function getSize(): int
    {
        return count($this->id);
    }

    // 查找元素 P 所对应的集合编号
    public function find(int $p)
    {
        if ($p < 0 || $p >= count($this->id)) {
            throw new Exception('p is out of bound');
        }
        return $this->id[$p];
    }

    // 查看元素 p 和 元素 q 是否所属一个集合
    public function isConected(int $p, int $q): bool
    {
        return $this->find($p) == $this->find($q);
    }

    // 合并元素 p 和 元素 q 所属的结合
    public function unionElements(int $p, int $q): void
    {
        $pId = $this->find($p);
        $qId = $this->find($q);
        if ($pId == $qId) {
            return;
        }

        for ($i = 0; $i < count($this->id); $i ++) {
            if ($this->id[$i] == $pId) {
                $this->id[$i] = $qId;
            }
        }
    }
}
```

### 子指父

```PHP
<?php

namespace Algorithm\UnionFind;
use Algorithm\UnionFind\UF;

class UnionFind2 implements UF
{
    private $parent;
    public function __construct(int $size)
    {
        $this->parent = range(0, $size - 1);
    }

    public function getSize(): int
    {
        return count($this->parent);
    }

    private function find($p)
    {
        if ($p < 0 || $p >= $this->getSize()) {
            throw new \Exception('p is illegal index');
        }

        // 父节点指向孩子节点，根节点指向自己
        while ($p != $this->parent[$p]) {
            $p = $this->parent[$p];
        }
        return $p;
    }
    public function isConected(int $p, int $q): bool
    {
        return $this->find($p) == $this->find($q);
    }

    // 合并元素p和元素q所属的集合
    public function unionElements(int $p, int $q): void
    {
        $pRoot = $this->find($p);
        $qRoot = $this->find($q);
        if ($qRoot == $pRoot) {
            return ;
        }
        $this->parent[$pRoot] = $qRoot;
    }
}
```

### 加权

```PHP
<?php

namespace Algorithm\UnionFind;
use Algorithm\UnionFind\UF;

class UnionFind3 implements UF
{
    private $parent;
    private $sz;
    public function __construct(int $size)
    {
        $this->parent = range(0, $size - 1);
        $this->sz = array_fill(0, $size - 1, 1);
    }

    public function getSize(): int
    {
        return count($this->parent);
    }

    private function find($p)
    {
        if ($p < 0 || $p >= $this->getSize()) {
            throw new \Exception('p is illegal index');
        }
        
        // 父节点指向孩子节点，根节点指向自己
        while ($p != $this->parent[$p]) {
            $p = $this->parent[$p];
        }
        return $p;
    }
    public function isConected(int $p, int $q): bool
    {
        return $this->find($p) == $this->find($q);
    }

    // 合并元素p和元素q所属的集合
    public function unionElements(int $p, int $q): void
    {
        $pRoot = $this->find($p);
        $qRoot = $this->find($q);
        if ($qRoot == $pRoot) {
            return ;
        }

        if ($this->sz[$pRoot] < $this->sz[$qRoot]) {
            $this->parent[$pRoot] = $qRoot;
            $this->sz[$qRoot] += $this->sz[$pRoot];
        } else {
            $this->parent[$qRoot] = $pRoot;
            $this->sz[$pRoot] += $this->sz[$qRoot];
        }
    }
}
```

### 路径压缩一

```PHP
<?php

namespace Algorithm\UnionFind;

use Algorithm\UnionFind\UF;

class UnionFind5 implements UF
{
    private $parent;
    private $rank;
    public function __construct(int $size)
    {
        $this->parent = range(0, $size - 1);
        $this->rank = array_fill(0, $size - 1, 1);
    }

    public function getSize(): int
    {
        return count($this->parent);
    }

    private function find($p)
    {
        if ($p < 0 || $p >= $this->getSize()) {
            throw new \Exception('p is illegal index');
        }

        // 父节点指向孩子节点，根节点指向自己
        while ($p != $this->parent[$p]) {
            $this->parent[$p] = $this->parent[$this->parent[$p]];
            $p = $this->parent[$p];
        }
        return $p;
    }
    public function isConected(int $p, int $q): bool
    {
        return $this->find($p) == $this->find($q);
    }

    // 合并元素p和元素q所属的集合
    public function unionElements(int $p, int $q): void
    {
        $pRoot = $this->find($p);
        $qRoot = $this->find($q);
        if ($qRoot == $pRoot) {
            return ;
        }

        if ($this->rank[$pRoot] < $this->rank[$qRoot]) {
            $this->parent[$pRoot] = $qRoot;
        } elseif ($this->rank[$pRoot] > $this->rank[$qRoot]) {
            $this->parent[$qRoot] = $pRoot;
        } elseif ($this->rank[$pRoot] == $this->rank[$qRoot]) {
            $this->parent[$qRoot] = $pRoot;
            $this->rank[$pRoot] += 1;
        }
    }
}
```

### 路径压缩二

```PHP
<?php

namespace Algorithm\UnionFind;

use Algorithm\UnionFind\UF;

class UnionFind6 implements UF
{
    private $parent;
    private $rank;
    public function __construct(int $size)
    {
        $this->parent = range(0, $size - 1);
        $this->rank = array_fill(0, $size - 1, 1);
    }

    public function getSize(): int
    {
        return count($this->parent);
    }

    private function find($p)
    {
        if ($p < 0 || $p >= $this->getSize()) {
            throw new \Exception('p is illegal index');
        }

        // 父节点指向孩子节点，根节点指向自己
        if ($p != $this->parent[$p]) {
            $this->parent[$p] = $this->find($this->parent[$p]);
        }
        return $this->parent[$p];
    }
    public function isConected(int $p, int $q): bool
    {
        return $this->find($p) == $this->find($q);
    }

    // 合并元素p和元素q所属的集合
    public function unionElements(int $p, int $q): void
    {
        $pRoot = $this->find($p);
        $qRoot = $this->find($q);
        if ($qRoot == $pRoot) {
            return ;
        }

        if ($this->rank[$pRoot] < $this->rank[$qRoot]) {
            $this->parent[$pRoot] = $qRoot;
        } elseif ($this->rank[$pRoot] > $this->rank[$qRoot]) {
            $this->parent[$qRoot] = $pRoot;
        } elseif ($this->rank[$pRoot] == $this->rank[$qRoot]) {
            $this->parent[$qRoot] = $pRoot;
            $this->rank[$pRoot] += 1;
        }
    }
}
```


## 参考

1. [Quick-Find Algorithm - Edusera Quick-Find Algorithm - Algorithms](https://edusera.org/quick-find-algorithm/)
2. [01UnionFind.key (princeton.edu)](https://www.cs.princeton.edu/courses/archive/spr08/cos226/lectures/01UnionFind.pdf)