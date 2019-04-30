[TOC]

# CPP

#### vector:: insert

```#include<vector>  
#include<iostream>  
using namespace std;  
 
int main()  
{  
    vector<int> v(3);  
    v[0]=2; //v[0]是第0个元素 
    v[1]=7;  
    v[2]=9;  
    v.insert(v.begin(),8);//在最前面插入新元素。  
    v.insert(v.begin()+2,1);//在迭代器中第二个元素前插入新元素  
    v.insert(v.end(),3);//在向量末尾追加新元素。  
 
	v.insert(v.end(),4,1);//在尾部插入4个1
 
	int a[] = {1,2,3,4};
	v.insert(v.end(),a[1],a[3]);//在尾部插入a[1]个a[3]
 
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



# Opencv

### Install

Project properties setting :

- C/C++ > General > Additional Include Directories > `D:\opencv-3.4.3\opencv\build\include`
- Linker > General > Additional Library Directories > `D:\opencv-3.4.3\opencv\build\x64\vc15\lib`
- Linker > Additional Dependencies > `opencv_world343.lib;opencv_world343d.lib`



### Function

#### flann:: radiusSearch

```cpp
vector<Point2f> pointsForSearch; //Insert all 2D points to this vector
flann::KDTreeIndexParams indexParams;
flann::Index kdtree(Mat(pointsForSearch).reshape(1), indexParams);
vector<float> query;
query.push_back(pnt.x); //Insert the 2D point we need to find neighbours to the query
query.push_back(pnt.y); //Insert the 2D point we need to find neighbours to the query
vector<int> indices;
vector<float> dists;
kdtree.radiusSearch(query, indices, dists, range, numOfPoints);
```

#### medianBlur

```	c++
medianBlur(blur, blur, 3);
```

#### erode / dilate

```c++
Mat element = getStructuringElement(MORPH_ELLIPSE, Size(3, 3));
dilate(clahe, clahe, element, Point(-1, -1), 1);
erode(clahe, clahe, element, Point(-1, -1), 2);
```



