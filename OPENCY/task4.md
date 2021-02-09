几何变换

```python
import cv2 as cv
import numpy as np
from matplotlib import pyplot as plt
img = cv.imread("C:/Users/Vad/Desktop/task3_1.jpg")


rows,cols,ch = img.shape
pts1 = np.float32([[2100,500],[500,1500],[2000,2700],[3400,1000]])
pts2 = np.float32([[1000,500],[1000,2400],[2600,2400],[2600,500]])
M = cv.getPerspectiveTransform(pts1,pts2)
dst = cv.warpPerspective(img,M,(3000,3000))
plt.subplot(121),plt.imshow(img),plt.title('Input')
plt.subplot(122),plt.imshow(dst),plt.title('Output')
plt.show()
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210209173919279.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Y1MzYzNjY=,size_16,color_FFFFFF,t_70)
