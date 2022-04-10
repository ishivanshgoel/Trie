## Longest-Common-Prefix
##### Problem Link: https://www.codingninjas.com/codestudio/problems/count-distinct-substrings_985292

```.cpp
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
    
    void increment(char ch){
        arr[ch-'a']->count++;
    }
    
    void setEnd(){
        flag = true;
    }
};

class Trie {
private:
    Node* root;
public:
    Trie(){
        root = new Node();
    }
    
    void insert(string word){
        Node* node = root;
        
        for(int i=0;i<word.length();i++){
            if(node->get(word[i]) == NULL){
                node->put(word[i]);
            }
            node->increment(word[i]);
            node = node->get(word[i]);
        }
        node->setEnd();
        
    }
    
    string lcp(string first, int c){
        Node* node = root;
        string ans = "";
        for(int i=0;i<first.length();i++){
            char ch = first[i];
            if(node->get(first[i])->count == c){
                ans += ch;
                node = node->get(first[i]);
            } else {
                break;
            }
        }
        return ans;
    }
    
};

class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.size() == 0) return "";
        Trie tr; 
        for(int i=0;i<strs.size();i++){
            tr.insert(strs[i]);
        }
        return tr.lcp(strs[0], strs.size());
    }
};
```
