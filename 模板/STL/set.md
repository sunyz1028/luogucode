## **set中常用的方法**

**begin()   　　 ,返回set容器的第一个元素**

**end() 　　　　 ,返回set容器的最后一个元素**

**clear()  　　   ,删除set容器中的所有的元素**

**empty() 　　　,判断set容器是否为空**

**max_size() 　 ,返回set容器可能包含的元素最大个数**

**size() 　　　　 ,返回当前set容器中的元素个数**

**rbegin　　　　 ,返回的值和end()相同**

**rend()　　　　 ,返回的值和begin()相同**

**count()** 用来查找set中某个某个键值出现的次数。这个函数在set并不是很实用，因为一个键值在set只可能出现0或1次，这样就变成了判断某一键值是否在set出现过了。

**equal_range()** ，返回一对定位器，分别表示第一个大于或等于给定关键值的元素和 第一个大于给定关键值的元素，这个返回值是一个pair类型，如果这一对定位器中哪个返回失败，就会等于end()的值。

**erase(iterator) ,删除定位器iterator指向的值**

**erase(first,second),删除定位器first和second之间的值**

**erase(key_value),删除键值key_value的值**

**find()** ，返回给定值值得定位器，如果没找到则返回end()。

**insert(key_value);** 将key_value插入到set中 ，返回值是pair<set<int>::iterator,bool>，bool标志着插入是否成功，而iterator代表插入的位置，若key_value已经在set中，则iterator表示的key_value在set中的位置。

**inset(first,second);**将定位器first到second之间的元素插入到set中，返回值是void.

**lower_bound(key_value)** ，返回第一个大于等于key_value的定位器

**upper_bound(key_value)，**返回最后一个大于等于key_value的定位器

**自定义比较函数**
   (1)元素不是结构体：
     例：
     //自定义比较函数myComp,重载“（）”操作符

```cpp
        struct myComp {



            bool operator()(const your_type &a,const your_type &b)



            [



                return a.data-b.data>0;



            }



        }



        set<int,myComp>s;



        ......



        set<int,myComp>::iterator it;
```

   (2)如果元素是结构体，可以直接将比较函数写在结构体内。
     例：

```cpp
        struct Info



        {



            string name;



            float score;



            //重载“<”操作符，自定义排序规则



            bool operator < (const Info &a) const



            {



                //按score从大到小排列



                return a.score<score;



            }



        }



        set<Info> s;



        ......



        set<Info>::iterator it;
```