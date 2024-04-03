:original_name: ocr_01_0133.html

.. _ocr_01_0133:

Why Is the Header Overflowing When I Call an OCR API Using Postman?
===================================================================

If the error message "Error: Header overflow" is displayed when calling an API using Postman to obtain an authentication token, it means that the header has exceeded its limit. To resolve this issue, follow these steps:

Modify the environment variables of the operating system. In Windows 10, right click **This PC** and choose **Properties**. Click **Advanced system settings**. On the **Advanced** tab, click **Environment Variables...**. In the **Environment Variables** dialog box, click **New...** in the **System variables** area. Configure **Variable name** and **Variable value** as follows:

-  **Variable name**: **NODE_OPTIONS**
-  **Variable value**: **--max-http-header-size=16384**
