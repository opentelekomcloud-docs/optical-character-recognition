:original_name: ocr_01_0065.html

.. _ocr_01_0065:

How Do I Handle the Error APIG.0201?
====================================

If error message "Backend timeout." and error code "APIG.0201" are displayed when you call an OCR API, the request timed out.

Perform the following steps to rectify the fault:

Use a tool, such as Postman, to call the service and check whether the call is successful. If the call is successful, the service API is normal. Perform the following steps to proceed:

#. Check whether the original API call requests are excessively frequent. If so, check the return value in the code and resend the requests later (for example, 2 to 5 seconds later). You can also check whether the result of the previous request is returned at the backend. After the result of the previous request is returned, send the next request.
#. Check whether the image is too large or the network delay is too long. If the image is too large, compress the image in proportion while ensuring the image definition. If the network delay is long, increase the network transmission speed.

If the fault persists, contact technical support.
