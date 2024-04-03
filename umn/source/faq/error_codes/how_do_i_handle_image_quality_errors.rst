:original_name: ocr_01_0096.html

.. _ocr_01_0096:

How Do I Handle Image Quality Errors?
=====================================

Symptom
-------

When calling an OCR API, the following error codes may occur related to image quality:

-  Error code AIS.0102: Unsupported image format.
-  Error code AIS.0103: Image size does not meet requirements.
-  Error code AIS.0104: Unsupported image type or poor image quality.

Solution
--------

-  Check whether the image format and pixel meet the requirements by referring to :ref:`Constraints and Limitations <ocr_01_0006>` in *Optical Character Recognition Service Overview*.
-  Verify that the Base64 encoding of the image is complete.
-  Check the image quality to ensure that the text in the image is clear and legible to the naked eye.
-  Verify that the API function matches the input image.
