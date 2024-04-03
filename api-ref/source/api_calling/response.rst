:original_name: ocr_03_0006.html

.. _ocr_03_0006:

Response
========

After sending a request, you will receive a response, including a status code, response header, and response body.

Status Codes
------------

A status code is a group of digits, ranging from 1xx to 5xx. It indicates the status of a request. For more information, see :ref:`Status Codes <ocr_03_0090>`.

If status code **201** is returned, the request is successful.

Response Header
---------------

Similar to a request, a response also has a header, for example, **Content-Type**.

.. table:: **Table 1** Common response headers

   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Header                | Description                                                                                                                                                                                                                    | Mandatory             |
   +=======================+================================================================================================================================================================================================================================+=======================+
   | Content-Type          | Media type of the response body sent to a recipient                                                                                                                                                                            | Yes                   |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Type: string                                                                                                                                                                                                                   |                       |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Default value: **application/json; charset=UTF-8**                                                                                                                                                                             |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | X-request-id          | Request ID for task tracing                                                                                                                                                                                                    | No                    |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Type: string **request_id-timestamp-hostname** (**request_id** is the UUID generated on the server. **timestamp** indicates the current timestamp, and **hostname** is the name of the server that processes the current API.) |                       |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Default value: none                                                                                                                                                                                                            |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | X-ratelimit           | Total number of flow control requests                                                                                                                                                                                          | No                    |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Type: integer                                                                                                                                                                                                                  |                       |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Default value: none                                                                                                                                                                                                            |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | X-ratelimit-used      | Number of remaining requests                                                                                                                                                                                                   | No                    |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Type: integer                                                                                                                                                                                                                  |                       |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Default value: none                                                                                                                                                                                                            |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | X-ratelimit-window    | Flow control unit                                                                                                                                                                                                              | No                    |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Type: string. The unit is in minute, hour, or day.                                                                                                                                                                             |                       |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Default value: hour                                                                                                                                                                                                            |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

The message header shown in Figure 3-1 is returned.

**x-subject-token** is the desired user token. This token can then be used to authenticate the calling of other APIs.


.. figure:: /_static/images/en-us_image_0000001744559845.png
   :alt: **Figure 1** Header fields of the response to the request for obtaining a user token

   **Figure 1** Header fields of the response to the request for obtaining a user token

Response Body
-------------

A response body conveys information other than the response header and is generally sent in a structured format (for example, JSON or XML) defined by the **Content-Type** field in the response header.

The following message body is returned. The following is part of the response body:

.. code-block::

   {
       "token": {
           "expires_at": "2019-02-13T06:52:13.855000Z",
           "methods": [
               "password"
           ],
           "catalog": [
               {
                   "endpoints": [
                       {
                           "region_id": "********",
   ......

If an error occurs during API calling, an error code and error message will be displayed. An error response body is shown as follows:

.. code-block::

   {
       "error_msg": "The input parameter is invalid.",
       "error_code": "AIS.0101"
   }

In the error response body, **error_code** is an error code, and **error_msg** provides information about the error. For more information, see :ref:`Error Codes <ocr_03_0028>`.
