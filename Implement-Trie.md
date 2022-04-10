## Implementation of Trie (Prefix Tree)
##### Problem Link: https://leetcode.com/problems/implement-trie-prefix-tree/
```.cpp
struct Node{
    Node* arr[26];
    bool flag;
    
    Node(){
        for(int i=0;i<26;i++){
            arr[i] = NULL;
        }
        flag = false;
    }
    
    bool containsWord(char c){
        return arr[c-'a'] != NULL;
    }
    
    Node* getNode(char ch){
        return arr[ch-'a'];
    }
    
    void setEnd(){
        flag = true;
    }
    
    bool isEnd(){
        return flag;
    }
    
};


class Trie {
    Node* root;
public:
    Trie() {
        root = new Node();
    }
    
    void insert(string word) {
        Node* node = root;
        for(int i=0;i<word.length();i++){
            if(!node->containsWord(word[i])){
                node->arr[word[i]-'a'] = new Node();
            }
            node = node->getNode(word[i]);
        }
        node->setEnd();
    }
    
    bool search(string word) {
        Node* node = root;
        for(int i=0;i<word.length();i++){
            if(!node->containsWord(word[i])){
                return false;
            }
            node = node->getNode(word[i]);
        }
        
        return node->isEnd();
    }
    
    bool startsWith(string prefix) {
        Node* node = root;
        for(int i=0;i<prefix.length();i++){
            if(!node->containsWord(prefix[i])){
                return false;
            }
            node = node->getNode(prefix[i]);
        }
        return true;
    }
};

```
