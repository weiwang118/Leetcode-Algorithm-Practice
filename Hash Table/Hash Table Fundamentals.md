### Hash Table Fundamentals
The access time of an element is on average O(1), therefore lookup could be performed very fast. 

#### Definition
Hash Table is a data structure which stores data in an associative manner. In a hash table, data is stored in an array format, where each data value has its own unique index value. Access of data becomes very fast if we know the index of the desired data.  

Thus, it becomes a data structure in which insertion and search operations are very fast irrespective of the size of the data. Hash Table uses an array as a storage medium and uses hash technique to generate an index where an element is to be inserted or is to be located from.  

数据检索是计算机技术中最基本也是最常用的操作，面对大规模的数据存储，快速的查询操作是被需要的，那么如何可以以最快的速度进行数据的查找呢？考虑计算机中数据存储和使用方式，可以得知：**如果数据项连续存储，而关键码就是存储数据的地址（下标）！**就可以以O(1)的时间得到所需要的数据。  

但是，实际上，关键码不可能总是整数，即使是整数也不太可能有大规模的连续存储空间供一个量使用。于是，人们想出了一个方法，也就是哈希（hash，也有翻译成散列）表，其基本思想是：如果一种关键码不能或者不适合作为数据存储的下标，可以考虑通过一个变换把它们映射到另一种下标，这样子就可以把基于关键码的检索转换为基于整数下标的直接元素访问。
以字典为例，用哈希表的思想实现，具体方法是：  
1）选定一个整数的下标范围（通常以0或者1开始），建立一个包括相应元素位置范围的顺序表  
2）选定一个从实际关键码集合到上述下标范围的映射h：  
^^在需要存入关键码为key的数据时，将其存入表中第h（key）个位置。  
^^遇到以key为关键码检索数据时，直接去找表中第 h（key）个位置的元素  
**这个h称为哈希函数，或者散列函数，它就是从可能的关键码集合到一个整数区间的映射  

#### Data Structure for Hast Table
在C++中，set 和 map 分别提供以下三种数据结构，其底层实现以及优劣如下表所示：

|集合 |底层实现 | 是否有序 |数值是否可以重复 | 能否更改数值|查询效率 |增删效率|
|---|---| --- |---| --- | --- | ---|
|std::set |红黑树 |有序 |否 |否 | $O(\log n)$|$O(\log n)$ |
|std::multiset | 红黑树|有序 |是 | 否| $O(\log n)$ |$O(\log n)$ |
|std::unordered_set |哈希表 |无序 |否 |否 |$O(1)$ | $O(1)$|

std::unordered_set底层实现为哈希表，std::set 和std::multiset 的底层实现是红黑树，红黑树是一种平衡二叉搜索树，所以key值是有序的，但key不可以修改，改动key值会导致整棵树的错乱，所以只能删除和增加。

|映射 |底层实现 | 是否有序 |数值是否可以重复 | 能否更改数值|查询效率 |增删效率|
|---|---| --- |---| --- | --- | ---|
|std::map |红黑树 |key有序 |key不可重复 |key不可修改 | $O(\log n)$|$O(\log n)$ |
|std::multimap | 红黑树|key有序 | key可重复 | key不可修改|$O(\log n)$ |$O(\log n)$ |
|std::unordered_map |哈希表 | key无序 |key不可重复 |key不可修改 |$O(1)$ | $O(1)$|

std::unordered_map 底层实现为哈希表，std::map 和std::multimap 的底层实现是红黑树。同理，std::map 和std::multimap 的key也是有序的（这个问题也经常作为面试题，考察对语言容器底层的理解）。

当我们要使用集合来解决哈希问题的时候，优先使用unordered_set，因为它的查询和增删效率是最优的，如果需要集合是有序的，那么就用set，如果要求不仅有序还要有重复数据的话，那么就用multiset。

#### Set
set作为一个容器也是用来存储同一数据类型的数据类型，并且能从一个数据集合中取出数据，在set中每个元素的值都唯一，而且系统能根据元素的值自动进行排序，set的元素不像map那样可以同时拥有实值(value)和键值(key),set元素的键值就是实值。set不允许两个元素有相同的键值。C++的标准库中的集合支持高效的插入、删除和查询操作，这三个操作的时间复杂度都是 O(lgn)，其中n是当前集合中元素的个数。如果用数组，虽然插入的时间复杂度是 O(1)，但是删除合查询都是 O(n)，此时效率太低。在C++中我们常用的集合是set。std::set 是基于hash表的，因此并不是顺序存储。

我们构造set集合的目的是为了快速的检索，不可直接去修改键值。可以先删后插。  

1、构造一个集合  
```
set<T> s;
```
这样我们定义了一个名为s的、储存T类型数据的集合，其中T是集合要储存的数据类型。初始的时候s是空集合。  

2、插入元素  
用 insert( ) 方法向集合中插入一个新的元素。注意如果集合中已经存在了某个元素，再次插入不会产生任何效果，集合中是不会出现重复元素的。  
```
set<string> country;  // {}
country.insert("China"); // {"China"}
country.insert("America"); // {"China", "America"}
```
3、删除元素   
```
country.erase("America"); // {"China"}
```
4、查找元素  
想知道某个元素是否在集合中出现，你可以直接用 count( ) 方法--返回某个值元素的个数，如果集合中存在我们要查找的元素，返回 1 ，否则返回 0 。  
另一种方法是：find()--返回一个指向被查找到元素的迭代器  
```
set<int> set;
        for (int i=0; i<list.size(); i++){
            set.insert(list[i]);
        }
        for (auto i = set.begin(); i != set.end(); i++) {
            cout << *i << endl;
        }
```
输出：5 14 22 34 39
```
cout << set.count(5) << endl;
if(set.find(5) != set.end()) 
    cout << *set.find(5) << endl; 
```
输出：1  5  
5、遍历集合  
```
 for (set<string>::iterator it = country.begin(); it != country.end(); ++it) 
        cout << (*it) << endl;
```
[set function](https://www.cnblogs.com/omelet/p/6627667.html)  

#### Unordered_Set
```
unordered_set<int> set;
        for (int i=0; i<list.size(); i++){
            set.insert(list[i]);
        }
        for (unordered_set<int>::iterator i = set.begin(); i != set.end(); i++) {
            cout << *i << endl;
        }
        cout << " find 39: " << *set.find(39) << endl;
        cout << "count 14:" << set.count(14) << endl;
```
输出：  
22  
39  
34  
14  
5  
find 39: 39  
count 14: 1  

#### Map
        
    映射是指两个集合之间的元素的相互对应关系。通俗地说，就是一个元素对应另外一个元素。比如一个姓名的集合 {“Tom”, “Jone”, “Marry”}，班级集合{1, 2}。姓名与班级之间可以有如下的映射关系： class(“Tom”) = 1 , class(“Jone”) = 2 , class(“Marry”) = 1; 我们称其中的姓名集合为 关键字集合(key) , 班级集合为值集合(value) 。 在 C++ 中我们常用的映射是 map。  
map的特点是增加和删除节点对迭代器的影响很小。对于迭代器来说，可以修改实值，而不能修改key。  
1、构造一个映射  
在C++中，我们构造一个 map 的语句为：  
```
map<T1,T2> m;
```
这样我们定义了一个名为 m 的从 T1 类型到 T2 类型的映射。初始的时候 m 是空映射。  

2、插入映射  
插入有三种方法：  
采用创建pair的形式插入pair<string, string>("string", "字符串")  
采用make_pair的形式进行插入make_pair("apple", "苹果")  
采用大括号的形式进行插入{ "left", "左边" }  
通过 insert( ) 方法向集合中插入一个新的映射，参数是一个 pair 类型的结构。这里需要用到另外一个 STL 模板 -元组(pair)。  
```
map<string, int> dict;  // {}
dict.insert(pair<string, int>("Tom", 1)); // {"Tom"->1}
dict.insert(pair<string, int>("Jone", 2)); // {"Tom"->1, "Jone"->2}
 
dict.insert(pair<string, string>("string", "字符串"));//模板类型pair：构造了一个匿名对象插入到map
dict.insert(make_pair("apple", "苹果"));//模板函数make_pair：偷懒了，实际调的是pair
dict.insert({ "left", "左边" });
dict.insert({ "left", "剩余" });//插入不进去了，因为key值已经有了
```

3、访问映射  

   访问映射合，直接用 [] 就能访问。比如 dict[“Tom”] 就可以获取 “Tom” 的班级了。而这里有一个比较神奇的地方，如果没有对 “Tom” 做过映射的话，此时你访问 dict[“Tom”] ，系统将会自动为 “Tom” 生成一个映射，其 value 为对应类型的默认值。并且我们可以之后再给映射赋予新的值，比如 dict[“Tom”] = 3 ，这样为我们提供了另一种方便的插入手段。  
```
    map<string, int> dict;  // {}
    dict["Tom"] = 1; // {"Tom"->1}
    dict["Mary"] = 1; // {"Tom"->1, "Mary"->1}
    printf("Mary is in class %d\n", dict["Mary"]);
```

4、查找关键字  

count( ) :  

     在 C++ 中，如果你想知道某个关键字是否被映射过，你可以直接用 count( ) 方法。使用count，返回的是被查找元素的个数。如果有，返回1；否则，返回0。注意，map中不存在相同元素(Tom,Mary)，所以返回值只能是1或0。  

find()函数：

     find函数，返回的是被查找元素的位置，没有则返回map.end()。注意：map.end()不指向最后一个元素，而指向最后一个元素再+1，当find不到输入的元素时候，返回迭代器就指向这个end() 。  
```
int main(){
    map<string,int> test;
    test.insert(make_pair("test1",1));   //test["test1"]=1
    test.insert(make_pair("test2",2));   //test["test2"]=2
    map<string,int>::iterator it=test.find("test0");
    
    if(it==test.end())
        cout<<"test0 not found"<<endl;
    else
        cout<<it->second<<endl;
   
    cout<<test.count("test1")<<endl;
 
    it=test.find("test1");
    if(it==test.end())
        cout<<"test1 not found"<<endl;
    else
        cout<<it->second<<endl;
//输出： test0 not found    1    1
```
5、遍历映射  

通过迭代器可以访问映射中的每个映射，每个迭代器的 first 值对应key，second值对应value。  
```
for (map<string, int>::iterator it = dict.begin(); it != dict.end(); ++it) 
    cout << it->first << " is in class " << it->second << endl;
```

#### Unordered Map
```
 unordered_map<int, int> map;
        for (int i=0; i<list.size(); i++){
            map[i] = list[i];
        }
        cout << map[0] << endl;
        for (unordered_map<int, int>::iterator i = map.begin(); i != map.end(); i++){
            cout << i->first << ' ' << i->second << endl;
        }
        if (map.find(3) != map.end()) {
            cout << "find key=" << map.find(3)->first << ", value=" << map.find(3)->second << endl;
        }
        if (map.count(5) > 0) {
            cout << "find 5: " << map.count(5) << endl;
        }
```

#### Difference between set and map
set：  
所得元素的只有key没有value，value就是key  
不允许出现键值重复  
所有的元素都会被自动排序  
不能通过迭代器来改变set的值，因为set的值就是键  
map：  
map的值不作为键，键和值是分开的，所有元素都是键+值存在  
不允许键重复  
所有元素是通过键进行自动排序的  
map的键是不能修改的，但是其键对应的值是可以修改的  

