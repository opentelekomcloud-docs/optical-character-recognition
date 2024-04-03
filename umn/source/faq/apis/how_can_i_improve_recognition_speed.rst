:original_name: ocr_01_0123.html

.. _ocr_01_0123:

How Can I Improve Recognition Speed?
====================================

The recognition speed is related to the image size, which affects the time required for network transmission and image Base64 decoding. To speed up image processing by the OCR API, it is recommended that you compress the images while maintaining the required level of resolution before processing them. It is recommended to upload images in JPG format.

Based on practical experience, it is generally recommended that small images of documents (with less text) should be below 1 MB, and large images of dense A4-sized documents should be below 2 MB.

Refer to the following code for how to compress images:

.. code-block::

   import cv2
   def resize_image(image, max_size):
       """
       This code is used to expand or downsize an image proportionally. It compares the long side of the image with the input parameter max_size. If the long side of the image exceeds max_size, the image is downsized proportionally. Otherwise, the original image is returned.
       :param max_size: maximum length of the long side of an image. (Set this parameter based on site requirements. You are advised to set this parameter to a value as small as possible as long as the resolution requirement is met.)
       :return: returns the downsized image or the original image.
       """

       height, width = image.shape[:2]
       max_side = max(height, width)
       if max_side > max_size:
           scale = max_size / max_side
           image = cv2.resize(image, None, fx=scale, fy=scale)

       return image

   image = cv2.imread('test.png')
   image = resize_image(image, max_size=1024)
