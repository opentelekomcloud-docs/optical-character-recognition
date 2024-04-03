:original_name: ocr_01_0063.html

.. _ocr_01_0063:

How Do I Handle the Error APIG.0301?
====================================

If an error message and error code are returned when an API is called:

-  If error message "Incorrect IAM authentication information: decrypt token fail" and error code "APIG.0301" are displayed, the token fails to decrypt.

   Solution:

   (1) Check whether the token has expired.

   (2) Check whether the request body is correct and whether the token is correct and complete.

   (3) Check whether the environment where the token is obtained is the same as that where the token is invoked.
