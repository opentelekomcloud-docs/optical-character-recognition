:original_name: ocr_01_0032.html

.. _ocr_01_0032:

How Can I Get the Base64 Encoding of an Image?
==============================================

To recognize an image, it must first be converted to its Base64 coding. This section provides an example using Python to explain how to convert a local image to Base64 code. You can also use an online conversion tool.

Replace **d:\\demo.jpg** in the code with the actual image path.

.. code-block::

   import base64
   with open("d:\demo.jpg", "rb") as image_file:
       encoded_string = base64.b64encode(image_file.read()).decode()
   print(encoded_string)
