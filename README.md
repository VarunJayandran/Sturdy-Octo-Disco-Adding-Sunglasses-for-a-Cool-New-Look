# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

Feel free to fork, contribute, or customize this project for your creative needs!
## PROGRAM
```
# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
```
# Load the Face Image
faceImage = cv2.imread('pass.jpeg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```

```
faceImage.shape
```


```
#resized_faceImage.shape
faceImage.shape
```

```
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glassPNG = cv2.imread('sglass.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```


```
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(293,95))
print("image Dimension ={}".format(glassPNG.shape))
```


```
# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
```

```
# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```

```
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[390:485, 215:508]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```

```
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[390:485, 215:508]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```


```
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[390:485, 215:508]=eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```

## OUTPUT


<img width="441" height="585" alt="image" src="https://github.com/user-attachments/assets/114508dd-87fc-41ed-95d7-ddeb332022a0" />



<img width="726" height="585" alt="image" src="https://github.com/user-attachments/assets/ff28f852-0343-4c61-858a-94cb031b0ec4" />




<img width="1375" height="277" alt="image" src="https://github.com/user-attachments/assets/bd133b2f-dd89-4020-a446-dcf46a831269" />



<img width="428" height="563" alt="image" src="https://github.com/user-attachments/assets/1310d1be-89b1-4e4c-a4ac-93139666900c" />




<img width="1377" height="223" alt="image" src="https://github.com/user-attachments/assets/92f4540d-21ee-42e1-bd37-848f7195ec8c" />




<img width="1377" height="925" alt="image" src="https://github.com/user-attachments/assets/bfc17bf9-924f-456c-ab0a-30d3e7182925" />

