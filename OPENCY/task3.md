
一个图片逐渐过渡到另一个图片的视频

```python
import numpy as np
import cv2 as cv
img1 = cv.imread("C:/Users/Vad/Desktop/src5.jpg")
img2 = cv.imread("C:/Users/Vad/Desktop/src6.jpg")
fourcc = cv.VideoWriter_fourcc('X','V','I','D')
video = cv.VideoWriter('lll', fourcc, 30, (800,800))
for i in range(0, 100):
    x = i / 100
    y = 1 - x
    video1 = cv.addWeighted(img1, x, img2, y, 0)
    video.write(video1)
    cv.namedWindow("videos", 0)
    cv.imshow('videos', video1)
    cv.waitKey(1)
cv.waitKey(0)
cv.destroyAllWindows()
```

