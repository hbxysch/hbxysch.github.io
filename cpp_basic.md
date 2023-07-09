# C++ basic knowledge
1. a two-dimensional array could be initialized by the following way:
``` 
vector<vector<int>> result(n, vector<int>(n,0));
``` 

2. differences between vector<char> and string
其实在基本操作上没有区别，但是string提供更多的字符串处理的相关接口，例如string重载了+，而vector却没有。所以如果想处理字符串还是会使用string。