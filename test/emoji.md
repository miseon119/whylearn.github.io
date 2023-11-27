---
sort: 5
---

# SLAM

## Calculate the Camera Motion

Case 1: camera is monocular (2D-2D)

we only know the 2D pixel coordinates, so the problem is to estimate the motion according to two sets of 2D points. This
problem is solved by **epipolar geometry**.

Case 2: camera is binocular, RGB-D, or the distance is obtained by some method

problem is to estimate the motion according to two sets of 3D points. This problem is usually solved by **ICP**.


Case 3: If one set is 3D and one set is 2D, we get some 3D points and their projection positions on the camera, and we can also estimate the camera’s pose. This problem is solved by **PnP**.


