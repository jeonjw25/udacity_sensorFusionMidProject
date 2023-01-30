# Writeup: Track 3D-Objects Over Time

Please use this starter template to answer the following questions:

### 1. Write a short recap of the four tracking steps and what you implemented there (filter, track management, association, camera fusion). Which results did you achieve? Which part of the project was most difficult for you to complete, and why?

<br><br>

# Final Project Report

## step1

- EKF implement(Using np.matrix())
- Implements F, Q, gamma, S, predict(), update(), etc.

<br><br>

![step1_plot2](https://user-images.githubusercontent.com/54730375/215388217-2f15a549-1d9c-44a4-a82b-c6dfd5cf5ccf.png)

![step1_rmse2](https://user-images.githubusercontent.com/54730375/215388218-8a52fe0c-bd9f-4a28-8a9a-c162a65282d5.png)

<br> 

## step2
- track.state() initialization[‘initialized’, ‘tentative’, ‘confirmed’]
- reset track.score
- Implementing track updates with handle_update_track()

<br><br>

![step2_delete](https://user-images.githubusercontent.com/54730375/215388262-77db80ec-e149-4782-8b34-38d12d393116.png)

![step2_bash](https://user-images.githubusercontent.com/54730375/215388264-addf5a07-3fa3-41c1-8578-59520897d837.png)
![tracking075](https://user-images.githubusercontent.com/54730375/215389985-36a89d9e-ead3-45ae-a35c-4f1b73c5cbf5.png)

![step2_rmse](https://user-images.githubusercontent.com/54730375/215388266-2160207c-ade1-4a1e-bd01-027d951a5213.png)

<br> 


## step3

- Derive association matrices for all track lists and all measurements

- Implementation of Mahalanobis distance derivation function MHD()

- Implement a gating() function to check if a measurement is inside a track

- Change the elements with gating() = false in the association matrix to np.inf

- Implementation of get_closest_track_and_meas()
  - Find the minimum item in the association matrix and delete the corresponding row and column

  <br><br>

![step3_plot](https://user-images.githubusercontent.com/54730375/215388309-fea22164-d7e0-4254-90bf-89eeab58d5c7.png)

![step3_rmse](https://user-images.githubusercontent.com/54730375/215388311-0a13259b-b8e2-4e6a-9466-5911e3c1f823.png)

<br> 

## step4
- Implementation of sensor fusion

- Implementation of function in_fov() to check if an object is within line of sight

  - α is derived using the arctan function

  - true if x > 0 & α < self.fov

- Implementation of non-linear camera measurement function (camera projection function) get_hx()

  - veh -> sensor coor(x, y, z)

  - Implement camera projection using camera intrinsic matrix

- Camera measurement class definition

  - Initialize 2D coordinates

  - Noise covariance initialization from configuration file (sigma_cam_i, sigma_cam_j)

- Add camera sensor measurements to the measurement list
-  saved track image in /results
<br><br>

![step4_rmse](https://user-images.githubusercontent.com/54730375/215388346-dfe7f57a-c88a-49dd-8ab3-fcd6db9ce91d.png)

![step4_plot](https://user-images.githubusercontent.com/54730375/215388348-4b1dded5-e352-410b-b331-b97516bd586d.png)


- Implementing the get_hx() function in measurements.py was difficult. I had to see the error message for a long time because the type conversion for NumPy was not done.

- It was difficult to adjust the track state because the conditions for changing the track state in trackmanagement.py were confusing.


<br><br>


### 2. Do you see any benefits in camera-lidar fusion compared to lidar-only tracking (in theory and in your concrete results)? 
- When comparing the results of step 3 and step 4, rmse decreased more when sensor fusion was used than when only lidar was used.

<br><br>

### 3. Which challenges will a sensor fusion system face in real-life scenarios? Did you see any of these challenges in the project?
- Tracking is not possible when false positives occur in all sensors.

- Obscured and invisible objects are highly unlikely to be captured by LiDAR.

<br><br>

### 4. Can you think of ways to improve your tracking results in the future?

- It seems that we can apply other algorithms than Mahalobis distance to association matrices.

- It seems that the performance can be improved by adjusting the gating threshold.

<br><br>

### 5. Tracking video
https://www.youtube.com/watch?v=Qfd4Hk17SJ8