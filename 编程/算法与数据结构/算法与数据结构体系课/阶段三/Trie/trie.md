# trie

Trie 被称为字典树或者前缀树，专门为处理字符串而设计的。

查询每个条目的时间复杂度和字典中一共有多少条目无关！

时间复杂度为 O(w)，w 为 查询的长度；

## 结构



## 接口

|序号|返回值类型|名称|描述|
|----|----|----|----|
|1|int|getSize()|获得 trie 中存储的单词数量|
|2|void|add(\$word)|在字典树中添加单词|
|3|bool|contains(\$word)|trie 中是否有 word|
|4|bool|isPrefix(\$prefix)|查询是否在 trie 中有单词以 prefix 为前缀|

## 参考代码

```PHP
<?php

class Trie
{
    private $root;
    private $size;

    public function __construct()
    {
        $this->root = new Node();
        $this->size = 0;
    }

    // 获得 trie 中存储的单词数量
    public function getSize()
    {
        return $this->size;
    }

    public function add($word)
    {
        $cur = $this->root;
        for ($i = 0; $i < strlen($word); $i++) {
            $char = $word[$i];
            if (empty($cur->next[$char])) {
                $cur->next[$char] = new Node();
            } 
            $cur = $cur->next[$char];
        }

        if (!$cur->isWord) {
            $cur->isWord = true;
            $this->size++;
        }
    }

    // trie 中是否有 word
    public function contains($word)
    {
        $cur = $this->root;
        for ($i = 0; $i < strlen($word); $i ++) {
            $char = $word[$i];
            if (empty($cur->next[$char])) {
                return false;
            }
            $cur = $cur->next[$char];
        }
        return $cur->isWord;
    }

    // 查询是否在 trie 中有单词以 prefix 为前缀
    public function isPrefix($prefix)
    {
        $cur = $this->root;
        for ($i = 0; $i < strlen($prefix); $i ++) {
            $char = $prefix[$i];
            if (empty($cur->next[$char])) {
                return false;
            }
            $cur = $cur->next[$char];
        }
        return true;
    }

    public static function main()
    {
        $word = 'hello';
        $word1 = 'hi';
        $word2 = 'help';
        $trie = (new Trie());
        $trie->add($word);
        $trie->add($word1);
        echo $trie->getSize().PHP_EOL;
        // var_dump($trie->root);
        var_dump($trie->contains('hii'));
        var_dump($trie->isPrefix('hel'));
    }
}

class Node
{
    public $isWord;
    public $next;

    public function __construct($isWord = false)
    {
        $this->isWord = $isWord;
        $this->next = [];
    }
}
```

## 相关问题

1. [MapSum](https://leetcode.cn/problems/z1R5dt/)
2. [WordDictionary](https://leetcode.cn/problems/design-add-and-search-words-data-structure/)
