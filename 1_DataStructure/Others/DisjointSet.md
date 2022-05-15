## Disjoint Set
## 1. Motivation: 
- Solving Connectivity problem in Graph with almost constant time.

Union-Find| Constructor|Find|Union|IsConnect|
-|-|-|-|-|
TimeComplexity|O(N)|O(a(N))|O(a(N))|O(a(N))|
### Note:
- a(n) = Inverse Ackermann function
- In practice, we can regard 0(a(N)) as O(1), constant time on average.

### 1.1 Interface
1. *.find(x)*: 
    - finds the root node of a given vertex.
2. *.is_connected(x,y)*: 
    - finds if two vertices are connected.
3. *.union_set(x,y)*: 
    - unions two vertices and makes their root nodes the same.
4. *.get_count()*: 
    - returns the number of un-connected groups. 

## 2. Pros. & Cons.
- Pros: 
    - Constant time complexity for graph's connectivity.
- Cons:
    - Almost nope.
    - If we must to say, it requires O(n) for construction, two vector.
    
## 3. When to use:
- Check connectivity.
- Find the number of connected groups / un-counnected groups


## 4. Implementation
~~~c++
class Disjoint_set{
    vector<int> root;
    vector<int> rank;
    int count;
public:
    
    Disjoint_set(int n): root(n), rank(n), count(n){
        for(int i = 0;i<n;i++)
        {
            rank[i]=1;
            root[i]=i;
        }
    }
    
    int find(int x)
    {
        // Path compression by recurrence.
        if(x==root[x])
        {
            return x;
        }
        root[x]=find(root[x]);
        return root[x];
    }
    
    void union_set(int x, int y)
    {
        int rootX = find(x);
        int rootY = find(y);
        
        if(rootX!=rootY)
        {
            if(rank[rootX]>rank[rootY]) // union by rank
            {
                root[rootY]=rootX;
            }else if(rank[rootX]<rank[rootY])
            {
                root[rootX]=rootY;
            }else{
                root[rootX]=rootY;
                rank[rootY]++;
            }
            count--;
        }
    }
    
    bool is_connected(int x, int  y)
    {
        return find(x)==find(y);
    }
    
    int get_count(){
        return count;
    }
};
~~~

## 5. Alternative
- For connectivity problems, there is no algernative solution. Because it has been almost constant time complexity.

## 6. C++ Container
- No existing containers, we should implemented them.