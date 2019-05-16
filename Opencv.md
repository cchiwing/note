[TOC]

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

#### hconcat / vconcat

```c++
Mat out;
vector<Mat> imgs;
vconcat(imgs, out);
imwrite(str_path, out);
```