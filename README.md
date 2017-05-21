# cpp-tips

## Priority Queue
```cpp
  priority_queue<int> maxHeap;
  for(int i = 0; i < 5; i++) {
    maxHeap.push(i); // 4 3 2 1 0
  }
  
  priority_queue<int, vector<int>, greater<int>> minHeap;
  for(int i = 0; i < 5; i++) {
    minHeap.push(i); // 0 1 2 3 4
  }
  
  class Comp {
  public:
    bool operator() (int a, int b) {
      return a < b;
    }
  };
  
  priority_queue<int, vector<int>, Comp> maxHeap;
  for(int i = 0; i < 5; i++) {
    maxHeap.push(i); // 4 3 2 1 0
  }
```

## Vector

```cpp
  vector<vector<int>> a(10, vector<int>(5, 0)); // 2d vector 
```

## Sort

```cpp
  vector<int> a;
  
  bool comp(int a, int b) {
    return a < b;
  }
  
  for(int i = 0; i < 5; i++) {
    a.push_back(i);
  }
  
  sort(a.begin(), a.end(), comp); // 0 1 2 3 4
```

## Function Pointer

```
typedef void (*func)();
map<string, func> key2func;

```
