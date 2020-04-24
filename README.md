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

```cpp
typedef void (*func)();

map<string, func> key2func;

void functionA(func func1);
void functionB(void (*func)());

```

## [Socket Programming](http://www.geeksforgeeks.org/socket-programming-cc/)

```cpp
#define PORT 8080

struct sockaddr_in address;
int sock = 0, valread;
struct sockaddr_in serv_addr;
char *hello = "Hello from client";
char buffer[1024] = {0};
if ((sock = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
  printf("\n Socket creation error \n");
  return -1;
}

memset(&serv_addr, '0', sizeof(serv_addr));

serv_addr.sin_family = AF_INET;
serv_addr.sin_port = htons(PORT);

// Convert IPv4 and IPv6 addresses from text to binary form
if(inet_pton(AF_INET, "127.0.0.1", &serv_addr.sin_addr)<=0) {
  printf("\nInvalid address/ Address not supported \n");
  return -1;
}

if (connect(sock, (struct sockaddr *)&serv_addr, sizeof(serv_addr)) < 0) {
  printf("\nConnection Failed \n");
  return -1;
}

send(sock , hello , strlen(hello) , 0 );
printf("Hello message sent\n");
valread = read( sock , buffer, 1024);
printf("%s\n",buffer );
```

## Exception and Assert

```cpp
assert(a > 0)

throw runtime_error("There is an error");
```

## Set, Compare, Insert

```cpp
struct Node {
	int x;
	RectNode rect;
	bool end;
	int index;
	
	Node& operator=(Node const& copy)
	{
		this->x = copy.x;
		this->rect = copy.rect;
		this->end = copy.end;
		this->index = copy.index;
		return *this;
	}
	
	Node(Node const &copy) {
		x = copy.x;
		rect = copy.rect;
		end = copy.end;
		index = copy.index;
	}
	
	Node(int x, RectNode &rect, bool end, int index) {
		this->x = x;
		this->rect = RectNode(rect.topLeft, rect.topRight, rect.bottomLeft, rect.bottomRight);
		this->end = end;
		this->index = index;
	}
	
	bool operator==(const Node& other) const
	{
		return this->index == other.index;
	}
	
	bool operator<(const Node& other) const
	{
		if (this->x < other.x) {
			return true;
		}
		
		if (this->x > other.x) {
			return false;
		}
		
		return this->end;
	}
};

struct NodeComp {
	bool operator()(const Node& lhs, const Node& rhs) const { 
		return lhs.index < rhs.index;
	}
};

set<Node, NodeComp> s;
```
