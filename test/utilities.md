---
sort: 9
---

# OpenCV

## Use **pointPolygonTest** to find target points 

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

Text can be **bold**, _italic_, or ~~strikethrough~~. [Links](https://github.com) should be blue with no underlines (unless hovered over).

{:.text-red}
Text can be **bold**, _italic_, or ~~strikethrough~~. [Links](https://github.com) should be blue with no underlines (unless hovered over).

{:.bg-yellow-dark}
Text can be **bold**, _italic_, or ~~strikethrough~~. [Links](https://github.com) should be blue with no underlines (unless hovered over).

{:.bg-yellow-dark.text-white}
Text can be **bold**, _italic_, or ~~strikethrough~~. [Links](https://github.com) should be blue with no underlines (unless hovered over).

{:.bg-yellow-dark.text-white.m-5}
Text can be **bold**, _italic_, or ~~strikethrough~~. [Links](https://github.com) should be blue with no underlines (unless hovered over).

{:.bg-yellow-dark.text-white.p-5.mb-6}
Text can be **bold**, _italic_, or ~~strikethrough~~. [Links](https://github.com) should be blue with no underlines (unless hovered over).

{:.bg-yellow-dark.text-white.p-5.mb-6}
Text can be **bold**{:.h1}, _italic_, or ~~strikethrough~~. [Links](https://github.com) should be blue with no underlines (unless hovered over).

{:.bg-yellow-dark.text-white.p-2.box-shadow-large}
Text can be **bold**{:.h1}, _italic_, or ~~strikethrough~~. [Links](https://github.com) should be blue with no underlines (unless hovered over).

{:.bg-yellow-dark.text-white.p-5.box-shadow-large.anim-pulse}
Text can be **bold**{:.h1}, _italic_, or ~~strikethrough~~. [Links](https://github.com) should be blue with no underlines (unless hovered over).

```tip
Edit this page to see how to add this to your docs, theme can use [@primer/css utilities](https://primer.style/css/utilities)
```
