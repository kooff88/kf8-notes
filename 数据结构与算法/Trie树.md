## Trie 树

Trie 树，也叫“字典树”。它是一种专门处理字符串匹配的数据结构，用来解决在一组字符串集合中快速查找某个字符串的问题。

Trie 树的本质，就是利用字符串之间的公共前缀，将重复的前缀合并在一起。

Trie 树主要有两个操作：

```
一个是将字符串集合构造成 Trie 树,是一个将字符串插入到 Trie 树的过程。
另一个是在 Trie 树中查询一个字符串。

```

```java

public class Trie {
  private TrieNode root = new TrieNode('/'); // 存储无意义字符

  // 往Trie树中插入一个字符串
  public void insert(char[] text) {
    TrieNode p = root;
    for (int i = 0; i < text.length; ++i) {
      int index = text[i] - 'a';
      if (p.children[index] == null) {
        TrieNode newNode = new TrieNode(text[i]);
        p.children[index] = newNode;
      }
      p = p.children[index];
    }
    p.isEndingChar = true;
  }

  // 在Trie树中查找一个字符串
  public boolean find(char[] pattern) {
    TrieNode p = root;
    for (int i = 0; i < pattern.length; ++i) {
      int index = pattern[i] - 'a';
      if (p.children[index] == null) {
        return false; // 不存在pattern
      }
      p = p.children[index];
    }
    if (p.isEndingChar == false) return false; // 不能完全匹配，只是前缀
    else return true; // 找到pattern
  }

  public class TrieNode {
    public char data;
    public TrieNode[] children = new TrieNode[26];
    public boolean isEndingChar = false;
    public TrieNode(char data) {
      this.data = data;
    }
  }
}

```

### Trie 树与散列表、红黑树的比较

Trie 对要处理的字符串有及其严苛的要求。

```
第一，字符串中包含的字符集不能太大。我们前面讲到，如果字符集太大，那存储空间可能就会浪费很多。
     即便可以优化，但也要付出牺牲查询、插入效率的代价。
第二，要求字符串的前缀重合比较多，不然空间消耗会变大很多。
第三，如果要用 Trie 树解决问题，那我们就要自己从零开始实现一个 Trie 树，还要保证没有 bug，
    这个在工程上是将简单问题复杂化，除非必须，一般不建议这样做。
第四，我们知道，通过指针串起来的数据块是不连续的，而 Trie 树中用到了指针，所以，对缓存并不友好，性能上会打个折扣。
```

针对在一组字符串中查找字符串的问题，我们在工程中，更倾向于用散列表或者红黑树

Trie 树比较适合的是查找前缀匹配的字符串 Trie 树只是不适合精确匹配查找
