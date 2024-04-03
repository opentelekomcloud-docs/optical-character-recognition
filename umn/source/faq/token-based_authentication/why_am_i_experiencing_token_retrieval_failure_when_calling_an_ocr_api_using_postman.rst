:original_name: ocr_01_0040.html

.. _ocr_01_0040:

Why Am I Experiencing Token Retrieval Failure When Calling an OCR API Using Postman?
====================================================================================

When obtaining a token, refer to the error message and select the appropriate solution.

-  Check whether the service region in the body and the corresponding key value are correct.

-  If error message "The userInfo is wrong" is displayed, do the following:

   Set **username** and **domainname** correctly. Typically, the value of **username** is the same as that of **domainname**. If you are not sure about the value, log in to the **My Credentials** page. If you use an IAM account to obtain the token, set the parameters as follows:

   **username**: IAM username (subaccount name)

   **domainname**: account name

-  If the error code "APIGW.0101" is displayed, perform the following operation:

   Check whether the URL used to obtain the token is correct.
