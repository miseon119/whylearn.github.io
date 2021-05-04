---
sort: 3
---

# Python Lib

## Numpy

**sum** an array:
```python
import numpy as np  
a=np.array([0.4,0.5])  
b=np.sum(a)  
```

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


## OS LIB

**Generate Dir**
```python
from pathlib import Path
Path("/my/directory").mkdir(parents=True, exist_ok=True)
```
