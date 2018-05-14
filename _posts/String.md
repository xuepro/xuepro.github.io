# 模仿C++的string实现一个字符串String类

## 1. C++string 类的例子

```cpp
#include <iostream>
#include <string>
using std::string;
using std::endl;
using std::cout;

int main(){
	string str,str2("hello"),str3 = "world";
	cout<<str<<endl
	    <<str2<<endl
	    <<str3<<endl;
    
	string str4(str2);
	cout  <<str4<<endl;	
    
	str2+=str3;
	cout<<str2<<endl;
    
	str = str2+"---**=== "+str3;
	cout  <<str<<endl;	

	str[0] = 'H';
	cout<<str<<'\t'<<str[2]<<endl;
    
	str.append("jjjjj");
	cout<<str<<endl;
	str.push_back('P');
	cout<<str<<endl;

	str+=str2;
	cout<<str<<endl;
	str+="Student";
	cout<<str<<endl;
	int pos = str.find('o');
	cout<<pos<<endl;
	pos = str.find('o',pos+1);
	cout<<pos<<endl;

	string str4 = str.substr(2,5);
	cout<<str4<<endl;
	str.insert(3,"-taihu-");
	cout<<str<<endl;
	str.insert(2,"-xueyuan-",3,2);
	cout<<str<<endl;
	str.erase(str.begin()+2,str.end());
	cout<<str<<endl;

	return 0;
}
```

## 2. 实现自己的字符串String类

将string例子程序中的字符串类型换成自己的String就可以写一个String的测试程序，例如

```cpp
#include <iostream>
//#include <string>
//using std::string;
#include "String.h"

using std::endl;
using std::cout;

int main(){
	String str,str2("hello"),str3 = "world";
	cout<<str<<endl
	    <<str2<<endl
	    <<str3<<endl;
	String str4(str2);
	cout  <<str4<<endl;	
	str2+=str3;
	cout<<str2<<endl;
	str = str2+"---**=== "+str3;
	cout  <<str<<endl;	

	str[0] = 'H';
	cout<<str<<'\t'<<str[2]<<endl;
#if 0
	str.append("jjjjj");
	cout<<str<<endl;
	str.push_back('P');
	cout<<str<<endl;

	str+=str2;
	cout<<str<<endl;
	str+="Student";
	cout<<str<<endl;
	int pos = str.find('o');
	cout<<pos<<endl;
	pos = str.find('o',pos+1);
	cout<<pos<<endl;

	string str4 = str.substr(2,5);
	cout<<str4<<endl;
	str.insert(3,"-taihu-");
	cout<<str<<endl;
	str.insert(2,"-xueyuan-",3,2);
	cout<<str<<endl;
	str.erase(str.begin()+2,str.end());
	cout<<str<<endl;
#endif
	return 0;
}
```

按照上面的测试程序，我们的String类应该有：带默认参数的构造函数、拷贝构造函数等其他函数，应该重载运算符<<、+=,+、[]等，例如，我们可以写出如下的String类:

```cpp
// String类的头文件，比如叫做"String.h"
#pragma once
#include <cstring>
#include <iostream>
class String
{
	char *data;
	int size_;
public:
	String(const char* s=nullptr);
	String(const String& s);

	int size(){return size_;}
	const char operator[](int i)const{ return data[i]; }
	char& operator[](int i){ return data[i]; }

	String& operator+=(const String& s);
	friend std::ostream& operator<<(std::ostream& out,const String& str);
	friend String operator+(const String& str1,const String& str2);
};
```

```cpp
// String类的源程序文件，比如叫做"String.cpp"
#include "String.h"

String::String(const char* s){
	if(s==nullptr){	 data = nullptr;  size_ = 0;	return ;	}
	size_ = strlen(s);
	data =new char[size_+1];
	if(!data){	size_ = 0;			return ;	}
	for(int i = 0;i<size_;i++)
		data[i] = s[i];
	data[size_] = '\0';
}

std::ostream& operator<<(std::ostream& out,const String& str){
	if(str.data)
		out<<str.data;
	return out;
}

String::String(const String& s){
	if(s.data==nullptr){ data = nullptr;  size_ = 0;	return ;	}
	size_ = s.size_;
	data =new char[size_+1];
	if(!data){	size_ = 0;			return ;	}
	for(int i = 0;i<size_;i++)
		data[i] = s.data[i];
	data[size_] = '\0';
}
String& String::operator+=(const String& s){
	int new_size = size_+s.size_;
	char *p = new char[new_size+1];
	if(!p) return *this;
	for(int i = 0 ; i<size_;i++) p[i] = data[i];
	for(int i = 0 ; i<s.size_;i++) p[size_+i] = s.data[i];
	p[new_size] = '\0';
	size_ = new_size;
	delete[] data;
	data = p;
	return *this;
}
String operator+(const String& str1,const String& str2){
	String s(str1);
	s+=str2;
	return s;
}
```

可以在此基础上，继续实现其他的各种对String类对象的操作函数（成员函数或外部函数形式），比如: substr、append、push_back、insert、erase等