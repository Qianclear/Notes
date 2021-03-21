# 5-27

操作符noskipws会令输入运算符读取空白符，而不是跳过它们。为了恢复默认行为，可以使用skipws操作符。

```
cin>>noskipws;//设置cin读取空白符
while(cin>>ch)
cout<<ch;
cin>>skipws;//将cin恢复到默认状态，从而丢弃空白符
```

