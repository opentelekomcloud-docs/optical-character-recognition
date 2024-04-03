:original_name: ocr_01_0041.html

.. _ocr_01_0041:

How Do I Handle the Error APIG.0308?
====================================

The error message "The throttling threshold has been reached: policy user over ratelimit,limit:XX,time:1 minute" and error code "APIG.0308" are displayed when you call an OCR API.

Rectify the fault using either of the following methods:

#. Use the retry mechanism to rectify the fault by checking the return value in the code and retrying the requests after a short period of time (for example, 2 to 5 seconds).
#. You can also check whether the result of the previous request is returned at the backend. After the result of the previous request is returned, send the next request.
