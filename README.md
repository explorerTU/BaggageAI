# BaggageAI


## Importing Libraries
> cv2

> matplotlib.pyplot

> numpy

> scipy

## Importing Images
* `cv2.imread` function reads the image for further processing. In bracket, we have to write the path of image.
* `type(image)` returns the type of image. here, image is nd array. And `image.shape` returns the shape of image.
	
## Displaying Image.
* `np.copy(image)` makes copy of original image.
* `cv2.cvtColor()` function changes the color of image from BGR to RGB. (OpenCv library reads the image in BGR format instead of RGB.)
* `plt.imshow(image)` displays the image using scale.
	
## Cropping the image.
* `image[h,w]` function crops the image for desired values. h specifies the height to crop and w specifies width to crop.

## Rotating the image.
* `ndimage.rotate(image, angle)` ndimage function from scipy is useful to rotate the image. we need to input the image and speciffy the angle for which image is to rotate.

## Converting black pixels into white pixels.
* rotated image contains black pixels. to remove those black pixels, we have to convert each pixel to white.
* `np.where` function defines each color channels. setting each color channel to 0, detects each black color channel.
* setting color channels to `[255,255,255]` which is maximum value of each pixel, converts each black pixel into white color.
```python
black_pixels = np.where(
    (image[:, :, 0] == 0) &  # specifies red color channel
    (image[:, :, 1] == 0) &  # specifies green color channel
    (image[:, :, 2] == 0)    # specifies blue color channel
)

# set those pixels to white
image[black_pixels] = [255, 255, 255] # converts black color to white color.
plt.imshow(image)
```
## Background image.
* import the background image and print the shape, to know the hight and width.

## Resize the image.
* resize the original image with respect to background image using `cv2.resize(image,(w,h))` function. where w is the width and h is the hight of BACKGROUND IMAGE.

## Mask the image.
* masking the original image by selecting areas of interest. removing the white pixels to select the region of threat object.
* `cv2.inRange` function selects pixels which are specified colors.
```python
lower_white = np.array([230,230,230]) 
upper_white = np.array([255,255,255])

masked = cv2.inRange(image, lower_white, upper_white) # selects the pixels which are white colored.
```

## Selecting areas of interest.
* Selecting the threat object and setting other pixels to black by setting masked pixels not equal to 0.
```python
masked_image[masked != 0] = [0, 0, 0]
```
## Processing background image.
> Note: threat object image parameters must be equal to background image parameters. (we can do it by resizing the threat image equal to background image)
* Setting masked pixels to black by equating them to zero. Setting the mask on background image.
```python
background_image[masked == 0] = [0, 0, 0]
```
## Complete Image.
* Add the two images together to create a complete image!
> complete_image = masked_image + background_image
