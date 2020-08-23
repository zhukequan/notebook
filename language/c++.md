## C++构造不能被继承的类
1. 将自身的构造函数与析构函数放在private作用域
2. 将自身作为一个已存在类Base的友元类,Base只有私有构造函数,Sub再虚继承Base。因为Sub是虚继承Base，所以Sub的子类会直接调用Base的构造函数，但Base的构造函数为私有，且友元类不能被继承，所以Sub的子类无法被构造。如下：
```
template<typename T>
class Base
{
    friend T;  //定义友元，子类可以访问父类的私有成员对象
private:
    Base()
    {
        cout<<"Base()"<<endl;
    }
    ~Base()
    {
        cout<<"~Base()"<<endl;
    }
};
//虚继承
class Sub:virtual public Base<Sub>  
{
public:
    Sub()
    {
        cout<<"Sub()"<<endl;
    }
    ~Sub()
    {
        cout<<"~Sub()"<<endl;
    }
};
```
3. c++11新增了final.
