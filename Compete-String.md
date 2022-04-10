## Complete String/ Longest String With All prefixes
#### Problem Link: https://www.codingninjas.com/codestudio/problems/complete-string_2687860

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
    
    void setEnd(){
        flag = true;
    }
    
    bool isEnd(){
        return flag;
    }
    
    void insert(char ch){
        arr[ch-'a'] = new Node();
    }
    
    Node* get(char ch){
        return arr[ch-'a'];
    }
};

class Trie{
    Node* root;
    
    public:
      Trie(){
          root = new Node();
      }
      
      void insert(string word){
          Node* node = root;
          for(int i=0;i<word.length();i++){
              if(node->get(word[i]) == NULL){
                  node->insert(word[i]);
              }
              node = node->get(word[i]);
          }
          
          node->setEnd();
      }
    
    bool search(string prefix){
        Node* node = root;
        for(int i=0;i<prefix.length();i++){
            if(node->get(prefix[i]) != NULL){
                node = node->get(prefix[i]);
            } else return false;
        }
        return node->isEnd();
    }
};


string completeString(int n, vector<string> &a){
    // Write your code here.
   	Trie tr;
    for(int i=0;i<a.size();i++){
        tr.insert(a[i]);
    }
    sort(a.begin(), a.end()); // sort lexographically
    int maxi = 0;
    string ans = "";
    
    for(int i=0;i<a.size();i++){
        string prefix = "";
        int count = 0;
        for(int j=0;j<a[i].length();j++){
            prefix += a[i][j];
            if(tr.search(prefix) == true){
                count++;
            } else break;
        }
        
        if(count == a[i].length() && maxi < a[i].length()){
            maxi = a[i].length();
            ans = a[i];
        }
    }
    
    if(ans == "") return "None";
    return ans;
}
```
