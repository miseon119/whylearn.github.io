---
sort: 3
---

# Python Lib

## pytorch

### check version
```python
import torch
import torch.nn as nn
import torchvision
print(torch.__version__)
print(torch.version.cuda)
print(torch.backends.cudnn.version())
print(torch.cuda.get_device_name(0))
```

### Use GPU

Single GPU:
```python
# Device configuration
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
```

Multi-GPU:
```python
import os
os.environ['CUDA_VISIBLE_DEVICES'] = '0,1'
```
in CLI:
```bash
CUDA_VISIBLE_DEVICES=0,1 python train.py
```

clear GPU cache:
```python
torch.cuda.empty_cache()
```

reset gpu
```bash
$ nvidia-smi --gpu-reset -i [gpu_id]
```

### torchvision

#### PIL Image/ numpy.ndarray to pytorch tensor

> torchvision.transform.ToTensor

```python
transforms.ToTensor()
```
#### Normalize

> torchvision.transforms.Normalize(mean, std, inplace=False)

```python
transforms.Normalize((0.5, 0.5, 0.5), (0.5, 0.5, 0.5))
```

### squeeze and unsqueeze

squeeze sample:
```python
import torch

x = torch.rand(3, 1, 20, 128)
x = x.squeeze() #[3, 1, 20, 128] -> [3, 20, 128]
```
unsqueeze sample:
```python
x2 = torch.rand(1, 1, 20, 128)
x2 = x2.squeeze(dim=1) # [1, 1, 20, 128] -> [1, 20, 128]
```

### tensor info

```python
tensor = torch.randn(3,4,5)
print(tensor.type())  # 数据类型
print(tensor.size())  # 张量的shape，是个元组
print(tensor.dim())   # 维度的数量
```

#### set tensor name
```python
# 在PyTorch 1.3之前，需要使用注释
# Tensor[N, C, H, W]
images = torch.randn(32, 3, 56, 56)
images.sum(dim=1)
images.select(dim=1, index=0)

# PyTorch 1.3之后
NCHW = [‘N’, ‘C’, ‘H’, ‘W’]
images = torch.randn(32, 3, 56, 56, names=NCHW)
images.sum('C')
images.select('C', index=0)
# 也可以这么设置
tensor = torch.rand(3,4,1,2,names=('C', 'N', 'H', 'W'))
# 使用align_to可以对维度方便地排序
tensor = tensor.align_to('N', 'C', 'H', 'W')
```

### Data type transform
```python

# 设置默认类型，pytorch中的FloatTensor远远快于DoubleTensor
torch.set_default_tensor_type(torch.FloatTensor)

# 类型转换
tensor = tensor.cuda()
tensor = tensor.cpu()
tensor = tensor.float()
tensor = tensor.long()
```

#### numpy array to Pytorch Tensor:
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


#### torch Tensor to numpy

```python
import torch
import numpy as np

a = torch.rand(3,3)
b = a.numpy()
```
or
```python
ndarray = tensor.cpu().numpy()
#tensor = torch.from_numpy(ndarray).float()
#tensor = torch.from_numpy(ndarray.copy()).float() # If ndarray has negative stride.
```

### Torch tensor to PIL.Image
```python
# pytorch中的张量默认采用[N, C, H, W]的顺序，并且数据范围在[0,1]，需要进行转置和规范化
# torch.Tensor -> PIL.Image
image = PIL.Image.fromarray(torch.clamp(tensor*255, min=0, max=255).byte().permute(1,2,0).cpu().numpy())
image = torchvision.transforms.functional.to_pil_image(tensor)  # Equivalently way

# PIL.Image -> torch.Tensor
path = r'./figure.jpg'
tensor = torch.from_numpy(np.asarray(PIL.Image.open(path))).permute(2,0,1).float() / 255
tensor = torchvision.transforms.functional.to_tensor(PIL.Image.open(path)) # Equivalently way
```

### np.array to PIL.Image
```python
image = PIL.Image.fromarray(ndarray.astype(np.uint8))

ndarray = np.asarray(PIL.Image.open(path))
```

### tensor transform

```python
# 在将卷积层输入全连接层的情况下通常需要对张量做形变处理，
# 相比torch.view，torch.reshape可以自动处理输入张量不连续的情况。
tensor = torch.rand(2,3,4)
shape = (6, 4)
tensor = torch.reshape(tensor, shape)
```

### Flip tensor
e.g.
```python
# [0 1 2 3 4 5 6 7 8 9]
# to [9 8 7 6 5 4 3 2 1 0]

# pytorch不支持tensor[::-1]这样的负步长操作，水平翻转可以通过张量索引实现
# 假设张量的维度为[N, D, H, W].
tensor = tensor[:,:,:,torch.arange(tensor.size(3) - 1, -1, -1).long()]
```

### copy tensor
```python
# Operation                 |  New/Shared memory | Still in computation graph |
tensor.clone()            # |        New         |          Yes               |
tensor.detach()           # |      Shared        |          No                |
tensor.detach.clone()()   # |        New         |          No                |
```

### concate tensor
```python

'''
注意torch.cat和torch.stack的区别在于torch.cat沿着给定的维度拼接，
而torch.stack会新增一维。例如当参数是3个10x5的张量，torch.cat的结果是30x5的张量，
而torch.stack的结果是3x10x5的张量。
'''
tensor = torch.cat(list_of_tensors, dim=0)
tensor = torch.stack(list_of_tensors, dim=0)
```

---

## Numpy

### squeeze
```python
x = np.array([[[0], [1], [2]]])
np.squeeze(x).shape
np.squeeze(x, axis=0).shape
np.squeeze(x, axis=1).shape
```

### Create random array
```python
# a random integer in the given range
rand_int = np.random.randint(5,10)  

# random numpy array of shape (4,5)
rand_int2 = np.random.randint(10,90,(4,5)) 

rand_int3 = np.random.randint(50,75,(2,2), dtype='int64')
```

`randint()` parameters:

`Low`  lower limit of the range, `High` upper limit of the range, `Size` shape of the array, `dtype` datatype of the values.


### Save array as txt file
```python
a = np.array([1, 2, 3, 4])
np.savetxt('test1.txt', a, fmt='%d')
b = np.loadtxt('test1.txt', dtype=int)
a == b
``` 
or
```python
a.tofile('test2.dat')
c = np.fromfile('test2.dat', dtype=int)
c == a
```
or There is a platform independent format for NumPy arrays:
```python
np.save('test3.npy', a)    # .npy extension is added if not given
d = np.load('test3.npy')
a == d
```

[more](https://stackoverflow.com/questions/28439701/how-to-save-and-load-numpy-array-data-properly)

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

## Tensorflow 1.x

Limit Gpu Growth
```python
gpu_options = tf.GPUOptions(per_process_gpu_memory_fraction=0.333)
sess = tf.Session(config=tf.ConfigProto(gpu_options=gpu_options))
```
Auto Adjuct Gpu Growth
```python
config = tf.ConfigProto()
config.gpu_options.allow_growth = True
session = tf.Session(config=config)
```

### Troubleshooting

> Flask uses multiple threads. The problem you are running into is because the tensorflow model is not loaded and used in the same thread. One workaround is to force tensorflow to use the gloabl default graph .

solution: Add this after you load your model
```python
global graph
graph = tf.get_default_graph() 
```
And inside your predict
```python
with graph.as_default():
    y_hat = keras_model_loaded.predict(predict_request, batch_size=1, verbose=1)
```

## Flask

Disable the reloader
```python
run(use_reloader=False)
```