:original_name: ocr_01_0137.html

.. _ocr_01_0137:

How Do I Handle the Error APIG.0106?
====================================

If error message and error code **"error_msg":"Orchestration error.","error_code":"APIG.0106"** are returned when an API is called, check whether the frontend and backend parameters configured for the API are correct.

This error is reported when the verification rule configured for frontend parameters of APIs is not met during API calling.

Rectify the fault using either of the following methods:

-  Check whether all mandatory parameters are configured.
-  Check whether parameter configuration rules are met. For example, the parameter value must be a number.
