---
sort: 3
---

# Python Lib

## Numpy

### Statistics

**sum** an array:
```python
import numpy as np  
a=np.array([0.4,0.5])  
b=np.sum(a)  
```
or
```python
import numpy as np  
a=np.array([[1,4],[3,5]])  
b=np.sum(a,axis=0) 
```

**mean**
```python
numpy.mean(arr)
```

**variance**
```python
numpy.var(arr)
```

**standard deviation**
```python
numpy.std(arr)
```

**count elements**
```python
cnt = np.count_nonzero(hue_roi > 0)
```

**MSE**
```python
np.square(np.subtract(A, B)).mean()
```

**padding 2D array**
```python
up=2
down=2
left=2
right=2
np.pad(img, ((up,down),(left,right)), 'constant', constant_values=0)
```

**show array's all elements**
```python
import sys
import numpy
numpy.set_printoptions(threshold=sys.maxsize)
```

### Change element 

```python 
 a[a < 0] = 0
```
```python 
np.where(a < 0, 0, a)
```
```python 
np.clip(a, 0, 4)
```



## matplotlib

Preinstall:
```console
$ sudo apt-get install python3-tk
```

Save plot:
```python 
import matplotlib.pyplot as plt
plt.plot([1,2,3], [5,7,4])
plt.savefig("mygraph.png")
```

### plot numpy array

Show array distribution:
```python
import numpy as np
import matplotlib.pyplot as plt
n, bins, patches = plt.hist(np_array)
plt.show()
```
or 
```python
from matplotlib import pyplot as plt 
import numpy as np  
   
a = np.array([22,87,5,43,56,73,55,54,11,20,51,5,79,31,27]) 
plt.hist(a, bins = [0,20,40,60,80,100]) 
plt.title("histogram") 
plt.show()
```

## OS LIB

**Generate Dir**
```python
from pathlib import Path
Path("/my/directory").mkdir(parents=True, exist_ok=True)
```
