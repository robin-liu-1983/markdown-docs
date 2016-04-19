# C++动态分配二维和三维数组
> 目的:熟悉c++动态内存分配 描述:使用c++程序定义动态数组类，使用new和delete操作符实现动态二维数组和三维数组的定义

//main.cpp //主程序类

```cpp
#include <iostream>
#include "DynamicArray.h"
#include "DynamicArray3d.h"
using namespace std;

int main()
{
    cout < < "Hello world!" << endl;
    DynamicArray a;
    a.printArray();
    DynamicArray3d b;
    b.printArray();
     return 0;
}
```

//DynamicArray.h //二维数组头文件

```cpp
#ifndef DYNAMICARRAY_H
#define DYNAMICARRAY_H
#include <iostream>
using namespace std;
class DynamicArray
{
public:
    DynamicArray(int m=5,int n=5);
    ~DynamicArray();
    void printArray();
private:
    int m_pArray;
    int m_iSize;
    int n_iSize;
};

#endif
```

//DynamicArray.cpp //二位数组源文件

```cpp
#include "DynamicArray.h"

DynamicArray::DynamicArray(int m,int n)
{
     int i,j;
     m_iSize=m;
     n_iSize=n;
     m_pArray = new int* [m_iSize];
     for (i = 0; i < m_iSize; i++)
          m_pArray [i] = new int[n_iSize];
     for (i = 0; i < m_iSize; i++)
         for (j = 0; j < n_iSize; j++)
          {
               m_pArray[i][j]=i+10*j;
          }
}

DynamicArray::~DynamicArray()
{
    for (int i = m_iSize; i > 0;)
          delete[] m_pArray[--i];
     delete[] m_pArray;
}
void DynamicArray::printArray()
{
     int i,j;
     cout < < "Print Array:" << endl;
     for (i = 0; i < m_iSize; i++)
     {
          for(j = 0; j < n_iSize; j++)
          cout<<m_pArray [i][j]<<"   ";
          cout<<endl;
     }

}
```

//DynamicArray3d.h //三维数组头文件

```cpp
#ifndef DYNAMICARRAY3D_H
#define DYNAMICARRAY3D_H
#include <iostream>
using namespace std;

class DynamicArray3d
{
     public:
          DynamicArray3d(int m=5,int n=5,int o=5);
          ~DynamicArray3d();
          void printArray();
     private:
          int m_pArray;
          int m_iSize;
          int n_iSize;
          int o_iSize;
};
#endif
```

//三维数组源文件

```cpp
#include "DynamicArray3d.h"

DynamicArray3d::DynamicArray3d(int m,int n,int o)
{
     int i,j,k ;
     m_iSize=m;
     n_iSize=n;
     o_iSize=o;
     m_pArray= new int**[m_iSize] ;
     for( i = 0 ; i < m_iSize ; i ++ )
          m_pArray[i] = new int*[n_iSize] ;
     for( i = 0 ; i < m_iSize ; i ++ )
          for( j = 0 ; j < n_iSize ; j ++ )
          m_pArray[i][j] = new int[o_iSize ] ;
   for(i = 0 ; i <m_iSize ; i ++ )
    for(j = 0 ; j < n_iSize ; j ++ )
     for( k = 0 ; k < o_iSize ; k ++)
      m_pArray[i][j][k] = i*100+j*10+k;
}

DynamicArray3d::~DynamicArray3d()
{

}

void DynamicArray3d::printArray()
{
     int i,j,k ;
     for(i = 0 ; i <m_iSize ; i ++ )
     {
          for(j = 0 ; j < n_iSize ; j ++ )
          {
                for( k = 0 ; k < o_iSize ; k ++)
                      cout<<m_pArray[i][j][k]<<" ";
               cout<<" ";
          }
     cout<<endl;
     }

}
```
