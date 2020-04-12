```c++
结构体：
struct Box{
	ll x;
	ll y;
}box;
```

如果想 map<Box,int> mp;

直接用会报错，于是需要重载比较运算符。

```c++
struct Box{
	ll x;
	ll y;
	bool operator < (const Box &o) const
	{
		return x < o.x || y < o.y;
	}

}box;

map<Box,int> mp;
```

