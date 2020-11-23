### leetcode_208_medium_实现Trie(前缀树)

![image-20201110202640358](leetcode_208_medium_实现Trie(前缀树).assets/image-20201110202640358.png)

同 文档 Trie树

```c++
class Trie {
public:
	/** Initialize your data structure here. */
	Trie() {
		m_child = vector<Trie*>(26);
		m_bIsEnd = false;
	}

	/** Inserts a word into the trie. */
	void insert(string word) {
		Trie* pCur = this;
		for (char& c : word)
		{
			if (pCur->m_child[c - 'a'] == nullptr)  //如果未找到对应子节点 则生成子节点
				pCur->m_child[c - 'a'] = new Trie();
			pCur = pCur->m_child[c - 'a'];
		}
		pCur->m_bIsEnd = true;  //将该节点标记为结束节点
	}

	/** Returns if the word is in the trie. */
	bool search(string word) {
		Trie* pCur = this;
		for (char c : word)
		{
			if (pCur->m_child[c - 'a'] == nullptr)  //如果未找到对应子节点 则单词不在树中
				return false;
			pCur = pCur->m_child[c - 'a'];
		}
		return pCur->m_bIsEnd;  //需检测该节点是否为结束节点
	}

	/** Returns if there is any word in the trie that starts with the given prefix. */
	bool startsWith(string prefix) {
		Trie* pCur = this;
		for (char c : prefix)
		{
			if (pCur->m_child[c - 'a'] == nullptr)  //若未找到对应子节点 则前缀不在数中
				return false;
			pCur = pCur->m_child[c - 'a'];
		}
		return true;
	}

private:
	bool m_bIsEnd;  //当前节点是否为一个单词的终点
	vector<Trie*> m_child;  //以长度为26的vector 表示26个子节点的26个字母
};

```

