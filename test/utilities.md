---
sort: 9
---

# OpenCV

## Draw Contour

`custom_roi_points` are user defined points, and we use `cv2.drawContours` to draw its contour.

```python
import numpy as np
import cv2
from numpy import array

img = np.zeros((512,512,3), np.uint8)
custom_roi_points = array([(50,50),(50,100),(100,100),(100,50)])

cv2.drawContours(img, [custom_roi_points], 0, (0,255,0), 2)
cv2.imshow('draw rect', img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
Result:
![DrawRect2](images/contour1.png)

---

## Use pointPolygonTest to find target points 

If you want to check a **point** inside or outside of a **polygon**, use `cv2.pointPolygonTest`:

sample code:   
```python
import cv2
import numpy as np

blank_image = np.zeros((720,1280,3), np.uint8)
custom_roi_points= np.array([(430,360),(860,360),(860,710),(430,710)]) 

dist = cv2.pointPolygonTest(custom_roi_points, (500,600),True)
cv2.circle(blank_image,(500,600),1,[255,0,0],7)
cv2.drawContours(blank_image,[custom_roi_points], 0, (0,255,255),2)

print("dist= " + str(dist))
cv2.imshow('img',blank_image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
___
