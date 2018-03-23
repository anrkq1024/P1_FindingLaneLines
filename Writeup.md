
## Udacity SDCND Project_1 : Finding lane lines on the Road

### In this project, Use computer vision technology to find lane lines in the picture 

---
### Process
  From the pictures of the road I extracts the part where the lane is present. Then, the part is clarified in color 
  and synthesized with the original photograph to recognize the lane. And apply the result to video of the car
  
---
### Details (soildWhiteRight soildYellowLeft)
#### First, include library to deal with mathematical operation and receive image

- mpimg.imread()
 
 ![screenshot from 2018-03-23 14-08-00](https://user-images.githubusercontent.com/35591154/37812738-ea027b4e-2ea4-11e8-97db-e6955dab7e26.png)
![screenshot from 2018-03-23 14-41-06](https://user-images.githubusercontent.com/35591154/37813526-cb840080-2ea8-11e8-8293-adfb27ae83f4.png)

#### And make the image gry_color then use the Gaussian function to smooth the wrong pixels in the image

- cv2.cvtColor(image,cv2.COLOR_RGB2GRAY), cv2.GaussianBlur(gray,(kernel_size, kernel_size),0)

![screenshot from 2018-03-23 14-08-25](https://user-images.githubusercontent.com/35591154/37812769-1184b394-2ea5-11e8-8e3b-0419be1bb393.png)
![screenshot from 2018-03-23 14-39-19](https://user-images.githubusercontent.com/35591154/37813542-de442f1a-2ea8-11e8-9e18-c9d23189f2fd.png)

#### Use a candy effect to select boundaries on the photo.

- cv2.Canny(blur_gray, low_threshold, high_threshold)

The rate of change with respect to the color of the pixel becomes larger at the boundary value of the object of the photograph. Pixels smaller than the minimum threshold of this rate of change are removed and pixels between the highest threshold and the lowest threshold are alive if they are associated with pixels above the highest threshold.

![screenshot from 2018-03-23 14-12-16](https://user-images.githubusercontent.com/35591154/37812840-6cad5e9c-2ea5-11e8-8b16-1725bb757d6b.png)
![screenshot from 2018-03-23 14-39-29](https://user-images.githubusercontent.com/35591154/37813568-0533b56e-2ea9-11e8-8fa0-c662c3b4d8d1.png)

#### Now that an area where the lane is present in the picture is constant, Remove other pixels except the area.
- cv2.fillPoly(mask, vertices, ignore_mask_color)

![screenshot from 2018-03-23 14-12-37](https://user-images.githubusercontent.com/35591154/37813205-71320ab0-2ea7-11e8-9f03-7e490179c337.png)
![screenshot from 2018-03-23 14-39-44](https://user-images.githubusercontent.com/35591154/37813579-1111e87e-2ea9-11e8-9b4a-5c87d7497d85.png)


#### Detect lines on the image through the hough transform to fill the lines with color and plot the lines in blank image
- cv2.HoughLinesP(masked_edges, rho, theta, threshold, np.array([]), min_line_length, max_line_gap)

![screenshot from 2018-03-23 14-12-49](https://user-images.githubusercontent.com/35591154/37813323-fa83c790-2ea7-11e8-8884-7de892ca6ae0.png)
![screenshot from 2018-03-23 14-39-53](https://user-images.githubusercontent.com/35591154/37813584-197c152a-2ea9-11e8-8fa3-7fdc32d4bf71.png)





#### The last process is to combine original image and detected lines
- cv2.addWeighted(line_image, 1, image, 1, 0) 

![screenshot from 2018-03-23 14-13-00](https://user-images.githubusercontent.com/35591154/37813424-6ab242a8-2ea8-11e8-8c31-8db0354d8c77.png)
![screenshot from 2018-03-23 14-40-02](https://user-images.githubusercontent.com/35591154/37813597-229083e4-2ea9-11e8-9e08-e6c47565565c.png)



