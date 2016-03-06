# HW2
for special project. 

#Introduction
熟悉影像基本處理，運用C++實現線性和非線性的濾波器，將圖片平滑化或進行邊緣偵測。探討的濾波器有以下幾種:<br>
1.  線性濾波器 : Box_filter,Gaussian_filter,Sobel_filter,Laplacian_filter.<br>
2.  非線性濾波器 : Max_filter,min_filter,Median_filter.<br>
#Theory
* 因為一些不可抗因素，取到的數據有雜訊時，我們會需要用濾波器把不需要的數據給篩選掉。資料剃除掉時，原本資料的儲存位置就需要填補新的數值。藉由參考周圍其他的資料數值進行補值的動作，可以找最大、最小、中間值又或者取平均等等。因為濾波器是二維的，所以我宣告一個二維的Mat型別的變數去儲存。另外因為我覺得RGB三通道在作convolution會比較麻煩，所以我是在灰度圖上做運算。在轉換回uchar之前，我讓超過255的值等於255，低於0的等於0。以下code只是簡略表示我的意思，不完全正確。
```
Mat m = zeros(height,width,CV_32S);                         //通常我在宣告Mat時，會先給予值等於零
Mat image = zeros(height,width,CV_8U);                      //最後轉回uchar的容器

if( m.at<int>(i,j)>255 )  m.at<int>(i,j)=255;               //必須檢查運算完的m內所有值都界在0到255
ekse if(  m.at<int>(i,j)<0 )  m.at<int>(i,j)=0;

image.at<uchar>(i,j) = m.at<int>(i,j);                      //把int轉回uchar;
```
* 為了方變觀察濾波器大小變化對圖片的影響，我們讓濾波器存寫在.txt方便修改。讀檔需要用到freopen的函式，一行一行用getline去讀，所以我先將每行字串用vector容器去暫存。
* 了解濾波器怎麼實現外，我還要去改變濾波器的大小變成5乘5、7乘7等等，另外很多濾波器都有平滑的效果，所以把不同種但同樣大小的濾波器去作比較。


#Result





## Q1
* Linear filter
* Any size with specified filter mask
<br/>
Flow : 
  1. Padding
  2. 2D convolution ij is the index within the filter window
    y = sum{ Pij*Wij }
## Q2
* Nonlinear filter
* Any size, max/min median
<br/>
Flow :
  1. Padding
  2. Sort Pij within the filter window
  3. Choose max/min/median as result

## Q3
* Sobel
* Gaussian
* Laplacian
* Unsharp (USM)
** Amount (A)
** Radious (R)
** Threshold (T)

Based on Q1, test and compare the effect of different filter

123456789
