:original_name: ocr_01_0064.html

.. _ocr_01_0064:

How Do I Handle the Error ModelArts.4603 or ModelArts.4704?
===========================================================

"error_code":"ModelArts.4603","error_msg":"Obtaining the file from the URL failed."
-----------------------------------------------------------------------------------

If "error_code":"ModelArts.4603","error_msg":"Obtaining the file from the URL failed." is displayed, it indicates that the image file fails to be obtained from the URL. To locate the fault, follow these steps:

(1) Make sure that the provided URL supports the HTTP/HTTPS request protocol, which should be in the format of **http/https** *URL*.

(2) Check if the server where the images are stored is stable and reliable, if the network connection is normal, and if it is publicly accessible.

(3) Check if the content-type of the downloaded images is a standard type, such as **image/gif**, **image/jpeg**, **image/png**, **image/tiff**. It is recommended to use OBS URL for the request.

"error_code":"ModelArts.4704","error_msg":"Obtaining the file from the OBS failed."
-----------------------------------------------------------------------------------

If ""error_code":"ModelArts.4704","error_msg":"Obtaining the file from the OBS failed."" is displayed, it means that the image data fails to be obtained from OBS. Make sure that the OBS path where the images are stored exists and is accessible. If the path exists, make sure that the OBS bucket policy is set to public.

It is recommended not to use OBS paths across regions. If OBS and the deployment region of the service to be called are not in the same region, it is suggested to download the images locally and call the service using the image method.
