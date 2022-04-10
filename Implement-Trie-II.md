## Implement Trie - II
##### Problem Link: https://www.codingninjas.com/codestudio/problems/implement-trie_1387095

```.cpp
class Trie{
	
	struct Node{
		Node* arr[26];
		bool flag;
		int count;
		
		Node(){
			for(int i=0;i<26;i++){
				arr[i] = NULL;
			}
			flag = false;
			count = 0;
		}
		
		Node* get(char ch){
			return arr[ch-'a'];
		}
		
		void put(char ch){
			arr[ch-'a'] = new Node();
		}
		
		void setEnd(){
			flag = true;
		}
		
		bool isEnd(){
			return flag;
		}
		
		void increment(){
			count++;
		}
		
		void decrement(){
			count--;
		}
		
		int getCount(){
			return count;
		}
	};

	Node* root;
	
    public:

    Trie(){
        // Write your code here.
		root = new Node();
    }

    void insert(string &word){
        // Write your code here.
		Node* node = root;
		for(int i=0;i<word.length();i++){
			if(node->get(word[i]) == NULL){
				node->put(word[i]);
			}
			node->get(word[i])->increment();
			node = node->get(word[i]);
		}
		node->setEnd();
    }

    int countWordsEqualTo(string &word){
        // Write your code here.
		Node* node = root;
		for(int i=0;i<word.length();i++){
			if(node->get(word[i]) == NULL){
				return 0;
			}
			node = node->get(word[i]);
		}
		if(node->isEnd()){
			return node->getCount();
		} else return 0;
    }

    int countWordsStartingWith(string &word){
        // Write your code here.
		Node* node = root;
		for(int i=0;i<word.length();i++){
			if(node->get(word[i]) == NULL){
				return 0;
			}
			node = node->get(word[i]);
		}
		
		return node->getCount();
    }

    void erase(string &word){
        // Write your code here.
		Node* node = root;
		for(int i=0;i<word.length();i++){
			if(node->get(word[i]) == NULL){
				return;
			}
			node = node->get(word[i]);
			node->decrement();
		}
    }
};

```
