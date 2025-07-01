:original_name: ocr_01_0089.html

.. _ocr_01_0089:

How Do I Handle the Error APIG.0307?
====================================

If error message "The token must be updated." and error code "APIG.0307" are displayed when you call an OCR API, the token has expired and needs to be updated.

Perform the following steps to rectify the fault:

-  The validity period of a token is 24 hours. Obtain the token again to call the API.
-  Check whether the `endpoint <https://docs.otc.t-systems.com/regions-and-endpoints/index.html>`__ in the API URL is correct. Services deployed in different regions cannot be called across regions. If APIs in different regions are called, the token is invalid and error code APIG.0307 is displayed.
