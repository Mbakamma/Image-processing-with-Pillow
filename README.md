Image Processing with Pillow (PIL) in Python

Objective
The objective of this project was to gain a fundamental understanding of image processing using the Pillow (PIL) library in Python. This includes tasks such as loading, displaying, manipulating, and converting images into NumPy arrays for further analysis. The project also aimed to demonstrate how to work with grayscale images, color quantization, and individual color channels.

Key Tasks and Findings
Loading and Displaying Images

Images were loaded using the Image.open method from the Pillow library.
Displayed images using both the show method from Pillow and imshow from Matplotlib.
Image Attributes

Retrieved and printed essential image attributes like size, format, and mode.
Grayscale Conversion

Converted color images to grayscale using the ImageOps.grayscale method.
Demonstrated how grayscale images represent different shades of gray based on pixel intensity.
Image Quantization

Performed image quantization to reduce the number of unique intensity levels.
Observed the effect of reducing quantization levels on image quality.
Color Channels

Extracted individual color channels (red, green, blue) from an image.
Visualized the intensity of each color channel in grayscale format.
PIL Images into NumPy Arrays

Converted PIL images into NumPy arrays for manipulation and analysis.
Demonstrated how to access and modify specific image regions and color channels using NumPy slicing.
Highlighted the importance of using the copy method to avoid unintentional modifications.
Exercise: Blue Channel Manipulation

Created a PIL Image object called blue_lenna.
Converted the image into a NumPy array and set all but the blue channel to zero.
Displayed the modified image, showing only the blue color channel.

Conclusion
This project provided a solid foundation in image processing using Python's Pillow library. By learning to load, manipulate, and display images, as well as convert them into NumPy arrays, users can now perform more advanced tasks in image processing and computer vision. The hands-on exercises and examples demonstrated the versatility of Pillow in handling various image formats and operations, making it a valuable tool for both beginners and experienced developers in the field of image processing.




Overview
This project provides a comprehensive tutorial on basic image processing tasks using the Pillow (PIL) library in Python. You will learn to load, manipulate, and display images, as well as convert them into NumPy arrays for further processing. The skills acquired here are fundamental for more advanced tasks in image processing and computer vision.

Table of Contents
- Overview
- Setup
- Helper Function
- Image Files and Paths
- Loading and Displaying Images
- Grayscale Images and Quantization
- Color Channels
- PIL Images into NumPy Arrays
- Blue Channel Manipulation
- Authors and Acknowledgments
- References


Setup
Download the required images for this project:
!wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-CV0101EN-SkillsNetwork/images%20/images_part_1/lenna.png -O lenna.png
!wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-CV0101EN-SkillsNetwork/images%20/images_part_1/baboon.png -O baboon.png
!wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-CV0101EN-SkillsNetwork/images%20/images_part_1/barbara.png -O barbara.png

Helper Function
Define a helper function to concatenate two images side-by-side:
from PIL import Image

def get_concat_h(im1, im2):
    dst = Image.new('RGB', (im1.width + im2.width, im1.height))
    dst.paste(im1, (0, 0))
    dst.paste(im2, (im1.width, 0))
    return dst

Image Files and Paths
1. Get the current working directory:
  import os
  cwd = os.getcwd()

2. Set the image file path:
   my_image = "lenna.png"
  image_path = os.path.join(cwd, my_image)


Loading and Displaying Images
1. Load an image using PIL:
   from PIL import Image
  image = Image.open(my_image)

2. Display the image using matplotlib:
   import matplotlib.pyplot as plt
  plt.figure(figsize=(5,5))
  plt.imshow(image)
  plt.show()

3. Get image attributes:
   print(image.size)  # Output: (512, 512)
  print(image.mode)  # Output: 'RGB'

Grayscale Images and Quantization

1. Convert to grayscale:
   from PIL import ImageOps
  image_gray = ImageOps.grayscale(image)
  image_gray.show()

2. Quantize the grayscale image:
for n in range(3, 8):
    plt.figure(figsize=(10,10))
    plt.imshow(get_concat_h(image_gray, image_gray.quantize(256//2**n)))
    plt.title("256 Quantization Levels left vs {} Quantization Levels right".format(256//2**n))
    plt.show()

Color Channels
1. Extract and display color channels:
   baboon = Image.open('baboon.png')
  red, green, blue = baboon.split()
  get_concat_h(baboon, red).show()
  get_concat_h(baboon, blue).show()
  get_concat_h(baboon, green).show()

PIL Images into NumPy Arrays
1. Convert a PIL image to a NumPy array:
   import numpy as np
  array = np.asarray(image)
  print(array.shape)  # Output: (512, 512, 3)

2. Display the NumPy array as an image:
plt.figure(figsize=(10,10))
plt.imshow(array)
plt.show()

3. Manipulate image sections using NumPy slicing:
rows = 256
plt.figure(figsize=(10,10))
plt.imshow(array[0:rows,:,:])
plt.show()

columns = 256
plt.figure(figsize=(10,10))
plt.imshow(array[:,0:columns,:])
plt.show()

4. Work with individual color channels in a NumPy array:
baboon_array = np.array(baboon)
plt.figure(figsize=(10,10))
plt.imshow(baboon_array[:,:,0], cmap='gray')
plt.show()

baboon_red = baboon_array.copy()
baboon_red[:,:,1] = 0
baboon_red[:,:,2] = 0
plt.figure(figsize=(10,10))
plt.imshow(baboon_red)
plt.show()


Blue Channel Manipulation
1. Open the image and create a PIL Image object called blue_lenna. Convert the image into a NumPy array called blue_array. Set all but the blue channel to zero and plot the image.
   blue_lenna = Image.open('lenna.png')
  blue_array = np.array(blue_lenna)
  blue_array[:,:,0] = 0
  blue_array[:,:,1] = 0
  plt.figure(figsize=(10,10))
  plt.imshow(blue_array)
  plt.show()















