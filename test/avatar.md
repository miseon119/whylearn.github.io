---
sort: 7
---

# Deep Learning Note

## YOLO v4

### Training

Modify config file paramenter:
`batch = 64`

`subdivisions=16`

`max_batches`: classes number x 2000, and larger than training images, and larger than 6000.

`steps`: 80% x max_batches, 90% x max_batches 

`width`: 416

`height`: 416

`classes`: your training object number

`filters`: (classes number +5)x3 
