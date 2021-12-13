---
sort: 3
---

# Python Lib

## pytorch

### numpy array to Pytorch Tensor:
1. torch.Tensor()
2. torch.from_numpy()

> torch.Tensor() 는 Numpy array의 사본일 뿐이다. 그래서 tensor의 값을 변경하더라도 Numpy array자체의 값이 달라지지 않는다.

```python
import torch
import numpy as np
a=np.array([1,2,3,4])
b=torch.Tensor(a)
print('output tensor:',b)

b[0]=-1
print('It cannot change np.array:',a)
```

> torch.from_numpy()는 자동으로 input array의 dtype을 상속받고 tensor와 메모리 버퍼를 공유하기 때문에 tensor의 값이 변경되면 Numpy array값이 변경된다. 

```python
a=np.array([1,2,3,4])
b=torch.from_numpy(a)
print('output tensor:',b)

b[0]=-1
print('It can change np.array:',a)
```

### torch Tensor to numpy

```python
import torch
import numpy as np

a = torch.rand(3,3)
b = a.numpy()
```

---

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

**Change data type:**
```python 
img = data.astype(np.uint8)
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
