# CPP
[TOC]

## Visual Studio Project Setup

1. Create project: 
   
   - `New Project` > `Win32 Console Application` > Select `Console application` > `Finish`
2. Project property setting for libraries:
   
   - Open `Property Page` by right click the solution in 'Solution Explorer' 
   
   - Set library link in `Configuration Properties` :
   
     - `C/C++`>`Additional Include Directories` add `D:\opencv\build\include;D:\boost_1_60_0;`
   
     - `Linker`> `Additional Library Directories` add 
`D:\opencv\build\x86\vc12\lib;D:\boost_1_60_0\bin\vc12\lib`
   
     - `Linker`>`Input`>`Additional Dependecies` add
   
       ```yaml
       opencv_core249.lib;
       opencv_imgproc249.lib;
       opencv_highgui249.lib;
       opencv_ml249.lib;
       -- add below if needed --
       opencv_video249.lib;
       opencv_legacy249.lib;
       ```
   
       



## Functions

#### vector:: insert

```
#include<vector>  
#include<iostream>  
using namespace std;  
 
int main()  
{  
    vector<int> v(3);  
    v[0]=2; //v[0]是第0个元素 
    v[1]=7;  
    v[2]=9;  
    v.insert(v.begin(),8);			//在最前面插入新元素。  
    v.insert(v.begin()+2,1);		//在迭代器中第二个元素前插入新元素  
    v.insert(v.end(),3);			//在向量末尾追加新元素。  
 
	v.insert(v.end(),4,1);			//在尾部插入4个1
 
	int a[] = {1,2,3,4};
	v.insert(v.end(),a[1],a[3]);	//在尾部插入a[1]个a[3]
 
    vector<int>::iterator it;  
    for(it=v.begin(); it!=v.end();it++)  
    {  
        cout<<*it<<" ";  
    }  
    cout<<endl;
 
	return 0;
}  
 
//8 2 1 7 9 3 1 1 1 1 4 4
//请按任意键继续. . .
```


