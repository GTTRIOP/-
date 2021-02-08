img.item(x,y,通道)#通道分为0，1，2；

img.itemset（(x,y,通道)，要修改成的值）；

要检查图像是否为灰度图像可以用img.shape,返回值会只有两个数字。

face= [上限:下限，左限:右限] ，可以用来选定一个区域

b,g,r = cv.split(img)是把图像分成三个通道

img = cv.merge((b,g,r))是把三个通道的图像和起来

cat[:,:,2] = 0可以把图片的红色通道去除

常用的颜色空间：BGR,HSV(色调，饱和度，明度)，灰度

OpenCV 的 HSV 格式中，H（色彩/色度）的取值范围是 [0，179]， S（饱和度）的取值范围 [0，255]，V（亮度）的取值范围 [0，255]。但是不 同的软件使用的值可能不同。所以当你需要拿 OpenCV 的 HSV 值与其他软 件的 HSV 值进行对比时，一定要记得归一化。

HSV中更容易表达一个物体的颜色，

：视频中获取每一帧图像

：图像转化为HSV

：设置HSV阈值到蓝色范围

：获取蓝色物体，，，



unit8储存rgb

用这种方法找对象的hsv

```python  
green = np.uint8([[[0,255,0 ]]])
hsv_green = cv.cvtColor(green,cv.COLOR_BGR2HSV)
print( hsv_green )
[[[ 60 255 255]]]
```

**思考题**：

1. HSV和BGR三原色在图片信息存储的差别在哪？

rgb 基于颜色的加法混色原理，从黑色不断叠加Red，Green，Blue的颜色，最终可以得到白色光。

HSV模型的三维表示从RGB立方体演化而来。设想从RGB沿立方体对角线的白色顶点向黑色顶点观察，就可以看到立方体的六边形外形。六边形边界表示色彩，水平轴表示纯度，明度沿垂直轴测量。与加法减法混色的术语相比，使用色相，饱和度等概念描述色彩更自然直观。

2.![在这里插入图片描述](https://img-blog.csdnimg.cn/20210208165513931.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Y1MzYzNjY=,size_16,color_FFFFFF,t_70)
