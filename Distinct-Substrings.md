## Distinct-Substrings
#### Problem Link: https://www.codingninjas.com/codestudio/problems/count-distinct-substrings_985292
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
    
    Node* get(char ch){
        return arr[ch-'a'];
    }
    
    void set(char ch){
        arr[ch-'a'] = new Node();
    }
    
   	void setEnd(){
        flag = true;
    }
};

class Trie{
    Node* root;
    int cnt;
    public:
    	Trie(){
            root = new Node();
            cnt = 0;
        }
    
    	void insert(string word){
            for(int i=0;i<word.length();i++){
                Node* node = root;
                for(int j=i;j<word.length();j++){
                    if(node->get(word[j]) == NULL){
                        cnt++;
                        node->set(word[j]);
                    }
                    node = node->get(word[j]);
                }
            }
        }
    
    	int getCount(){
            return cnt+1;
        }
};

int countDistinctSubstrings(string &s){
    //    Write your code here.
    Trie t;
    t.insert(s);
    return t.getCount();
}
```
