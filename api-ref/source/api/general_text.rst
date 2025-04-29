:original_name: ocr_03_0042.html

.. _ocr_03_0042:

General Text
============

Function
--------

This API detects and extracts text from images and converts the text and coordinates into JSON format. It can be used in various scenarios, such as scanned documents, electronic documents, books, receipts, and forms.

Constraints and Limitations
---------------------------

-  Only images in PNG, JPG, JPEG, BMP, GIF, TIFF, WebP, PCX, ICO, PSD, or PDF format can be recognized.
-  No side of the image can be smaller than 15 or larger than 8,192 pixels.
-  The area to be recognized must occupy more than 80% of the image. When scanning a table, ensure that all text and its surrounding area are included in the image.
-  An image can be rotated to any angle.
-  Text in images with complex backgrounds (such as outdoor scenery or anti-counterfeit watermarks) or distorted text cannot be recognized.
-  Supported languages: Chinese, English, some traditional Chinese, Malay, Ukrainian, Hindi, Russian, Vietnamese, Indonesian, Thai, Arabic, German, Latin, French, Italian, Spanish, Portuguese, Romanian, Polish Amharic, Japanese, Korean, Turkish, Norwegian, Danish, Swedish, Khmer, and Hebrew.

URI
---

POST /v2/{project_id}/ocr/general-text

.. table:: **Table 1** URI parameters

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Mandatory             | Description                                                                                                          |
   +=======================+=======================+======================================================================================================================+
   | endpoint              | Yes                   | Endpoint, which is the request address for calling an API.                                                           |
   |                       |                       |                                                                                                                      |
   |                       |                       | The endpoint varies depending on services in different regions. For more details, see :ref:`Endpoint <ocr_03_0062>`. |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------+
   | project_id            | Yes                   | Project ID, which can be obtained by referring to :ref:`Obtaining the Project ID <ocr_03_0130>`.                     |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request header parameters

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                             |
   +=================+=================+=================+=========================================================================================================================================================+
   | X-Auth-Token    | Yes             | String          | User token.                                                                                                                                             |
   |                 |                 |                 |                                                                                                                                                         |
   |                 |                 |                 | Used to obtain the permission to use APIs. The token is the value of **X-Subject-Token** in the response header in :ref:`Authentication <ocr_03_0005>`. |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Content-Type    | Yes             | String          | MIME type of the request body. The value is **application/json**.                                                                                       |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +-------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter               | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                        |
   +=========================+=================+=================+====================================================================================================================================================================================================================================================================================+
   | image                   | No              | String          | Set either this parameter or **url**.                                                                                                                                                                                                                                              |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | Base64-encoded image file. The image file has a size limit of 10 MB.                                                                                                                                                                                                               |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | No side of the image can be smaller than 15 or larger than 8,192 pixels. Only images in JPEG, JPG, PNG, BMP, GIF, or TIFF format can be recognized.                                                                                                                                |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | An example is **/9j/4AAQSkZJRgABAg...**. If the image data contains an unnecessary prefix, the error "The image format is not supported" is reported.                                                                                                                              |
   +-------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | url                     | No              | String          | Set either this parameter or **image**. The image file has a size limit of 10 MB. The following image URLs are currently supported:                                                                                                                                                |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | -  Public HTTP/HTTPS URL                                                                                                                                                                                                                                                           |
   |                         |                 |                 | -  URL provided by OBS.                                                                                                                                                                                                                                                            |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | .. note::                                                                                                                                                                                                                                                                          |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 |    -  The API response time depends on the image download time. If the image download takes a long time, the API call will fail.                                                                                                                                                   |
   |                         |                 |                 |    -  Ensure that the storage service where the images to be detected reside is stable and reliable. OBS is recommended for storing image data.                                                                                                                                    |
   |                         |                 |                 |    -  The URL cannot contain Chinese characters. If Chinese characters exist, they must be encoded using UTF-8.                                                                                                                                                                    |
   +-------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | detect_direction        | No              | Boolean         | Whether to align the tilted image. The options are as follows:                                                                                                                                                                                                                     |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | -  **true**: The tilted image will be aligned.                                                                                                                                                                                                                                     |
   |                         |                 |                 | -  **false**: The tilted image will not be aligned.                                                                                                                                                                                                                                |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | An image tilted to any angle can be aligned. If this parameter is not specified, **false** is used by default.                                                                                                                                                                     |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | If the image to be recognized is tilted, you are advised to set this parameter to **true**.                                                                                                                                                                                        |
   +-------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | quick_mode              | No              | Boolean         | Whether to enable the quick mode. For a single-line text image (the image contains only one line of text and the text area occupies more than 50% of the image), the recognition results can be returned more quickly when this quick mode is enabled. The options are as follows: |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | -  **true**: The quick mode will be enabled.                                                                                                                                                                                                                                       |
   |                         |                 |                 | -  **false**: The quick mode will be disabled.                                                                                                                                                                                                                                     |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | If this parameter is not specified, **false** is used by default.                                                                                                                                                                                                                  |
   +-------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | character_mode          | No              | Boolean         | Whether to enable the single-character mode. The options are as follows:                                                                                                                                                                                                           |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | -  **true**: The single-character mode is enabled.                                                                                                                                                                                                                                 |
   |                         |                 |                 | -  **false**: The single-character mode is disabled.                                                                                                                                                                                                                               |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | If this parameter is not transferred, the default value **false** is used, and information about a single character that occupies a text line is not returned.                                                                                                                     |
   +-------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | language                | No              | String          | Language. If this parameter is not specified, German and English will be used by default. The options are:                                                                                                                                                                         |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | -  **auto**: automatic language classification                                                                                                                                                                                                                                     |
   |                         |                 |                 | -  **ms**: Malay                                                                                                                                                                                                                                                                   |
   |                         |                 |                 | -  **uk**: Ukrainian                                                                                                                                                                                                                                                               |
   |                         |                 |                 | -  **hi**: Hindi                                                                                                                                                                                                                                                                   |
   |                         |                 |                 | -  **ru**: Russian                                                                                                                                                                                                                                                                 |
   |                         |                 |                 | -  **vi**: Vietnamese                                                                                                                                                                                                                                                              |
   |                         |                 |                 | -  **id**: Indonesian                                                                                                                                                                                                                                                              |
   |                         |                 |                 | -  **th**: Thai                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | -  **zh**: Chinese and English                                                                                                                                                                                                                                                     |
   |                         |                 |                 | -  **ar**: Arabic                                                                                                                                                                                                                                                                  |
   |                         |                 |                 | -  **de**: German                                                                                                                                                                                                                                                                  |
   |                         |                 |                 | -  **la**: Latin                                                                                                                                                                                                                                                                   |
   |                         |                 |                 | -  **fr**: French                                                                                                                                                                                                                                                                  |
   |                         |                 |                 | -  **it**: Italian                                                                                                                                                                                                                                                                 |
   |                         |                 |                 | -  **es**: Spanish                                                                                                                                                                                                                                                                 |
   |                         |                 |                 | -  **pt**: Portuguese                                                                                                                                                                                                                                                              |
   |                         |                 |                 | -  **ro**: Romanian                                                                                                                                                                                                                                                                |
   |                         |                 |                 | -  **pl**: Polish                                                                                                                                                                                                                                                                  |
   |                         |                 |                 | -  **am**: Amharic                                                                                                                                                                                                                                                                 |
   |                         |                 |                 | -  **ja**: Japanese                                                                                                                                                                                                                                                                |
   |                         |                 |                 | -  **ko**: Korean                                                                                                                                                                                                                                                                  |
   |                         |                 |                 | -  **tr**: Turkish                                                                                                                                                                                                                                                                 |
   |                         |                 |                 | -  **no**: Norwegian                                                                                                                                                                                                                                                               |
   |                         |                 |                 | -  **da**: Danish                                                                                                                                                                                                                                                                  |
   |                         |                 |                 | -  **sv**: Swedish                                                                                                                                                                                                                                                                 |
   |                         |                 |                 | -  **km**: Khmer                                                                                                                                                                                                                                                                   |
   |                         |                 |                 | -  **he**: Hebrew                                                                                                                                                                                                                                                                  |
   +-------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | single_orientation_mode | No              | Boolean         | Whether to enable the single direction mode. The options are as follows:                                                                                                                                                                                                           |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | -  **true**: The single direction mode is enabled.                                                                                                                                                                                                                                 |
   |                         |                 |                 | -  **false**: The single direction mode is disabled.                                                                                                                                                                                                                               |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | If this parameter is not specified, **false** is used by default. In this case, the fields in the image are recognized as in multiple directions by default.                                                                                                                       |
   +-------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | pdf_page_number         | No              | Integer         | Specify which page of the PDF to recognize. If this parameter is specified, the content on the specified page is identified. If not specified, the default is to recognize the first page.                                                                                         |
   +-------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

.. note::

   The status code may vary depending on the recognition results. For example, **200** indicates that the API is successfully called, and **400** indicates that the API fails to be called. The following describes the status codes and corresponding response parameters.

**Status code: 200**

.. table:: **Table 4** Response body parameter

   +-----------------------+--------------------------------------------------+-----------------------------------------------------------------+
   | Parameter             | Type                                             | Description                                                     |
   +=======================+==================================================+=================================================================+
   | result                | :ref:`Table 5 <ocr_03_0042__table2201135023416>` | Recognition result                                              |
   |                       |                                                  |                                                                 |
   |                       |                                                  | This parameter is not returned when the API fails to be called. |
   +-----------------------+--------------------------------------------------+-----------------------------------------------------------------+

.. _ocr_03_0042__table2201135023416:

.. table:: **Table 5** GeneralTextResult

   +-----------------------+----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                     | Description                                                                                                                                                                  |
   +=======================+==========================================================+==============================================================================================================================================================================+
   | direction             | Float                                                    | Image direction                                                                                                                                                              |
   |                       |                                                          |                                                                                                                                                                              |
   |                       |                                                          | -  This parameter is available only when **detect_direction** is set to **true**. The anti-clockwise rotation angle of an image is returned. The value ranges from 0 to 359. |
   |                       |                                                          | -  When **detect_direction** is set to **false**, the value of this parameter is **-1**.                                                                                     |
   +-----------------------+----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | words_block_count     | Integer                                                  | Number of detected text blocks                                                                                                                                               |
   +-----------------------+----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | words_block_list      | Array of :ref:`Table 6 <ocr_03_0042__table122257509346>` | List of recognized text blocks. The output sequence is from left to right and from top to bottom.                                                                            |
   +-----------------------+----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ocr_03_0042__table122257509346:

.. table:: **Table 6** GeneralTextWordsBlockList

   +------------+-------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter  | Type                                                        | Description                                                                                                                                                                                                                                      |
   +============+=============================================================+==================================================================================================================================================================================================================================================+
   | words      | String                                                      | Recognition result of a text block                                                                                                                                                                                                               |
   +------------+-------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | location   | Array<Array<Integer>>                                       | List of location information about a text block, including the 2D coordinates (x, y) of four vertexes in the text area, where the coordinate origin is the upper-left corner of the image, the X axis is horizontal, and the Y axis is vertical. |
   +------------+-------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | confidence | Float                                                       | Confidence of a recognized text block                                                                                                                                                                                                            |
   +------------+-------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | char_list  | Array of :ref:`Table 7 <ocr_03_0042__table152461450153416>` | Single-character recognition list corresponding to a text block. The output sequence is from left to right and from top to bottom.                                                                                                               |
   +------------+-------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ocr_03_0042__table152461450153416:

.. table:: **Table 7** GeneralTextCharList

   +-----------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                  | Description                                                                                                                                                                                                                                                 |
   +=================+=======================+=============================================================================================================================================================================================================================================================+
   | char            | String                | Recognition result of a single character                                                                                                                                                                                                                    |
   +-----------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | char_location   | Array<Array<Integer>> | List of location information about a single character, including the 2D coordinates (x, y) of four vertexes in the character area, where the coordinate origin is the upper-left corner of the image, the X axis is horizontal, and the Y axis is vertical. |
   +-----------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | char_confidence | Float                 | Confidence of a recognized character                                                                                                                                                                                                                        |
   +-----------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Status code: 400**

.. table:: **Table 8** Response body parameters

   +-----------------------+-----------------------+---------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                         |
   +=======================+=======================+=====================================================================+
   | error_code            | String                | Error code when calling the API failed                              |
   |                       |                       |                                                                     |
   |                       |                       | This parameter is not returned when the API is successfully called. |
   +-----------------------+-----------------------+---------------------------------------------------------------------+
   | error_msg             | String                | Error message when the API call fails                               |
   |                       |                       |                                                                     |
   |                       |                       | This parameter is not returned when the API is successfully called. |
   +-----------------------+-----------------------+---------------------------------------------------------------------+

Example Request
---------------

-  Transfer the Base64 code of the image for recognition. During the recognition, the tilt angle of the image is not verified, and the quick mode is disabled.

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/ocr/general-text
        Request Header:
        Content-Type: application/json
        X-Auth-Token: MIINRwYJKoZIhvcNAQcCoIINODCCDTQCAQExDTALBglghkgBZQMEAgEwgguVBgkqhkiG...
        Request Body:
        {
           "image":"/9j/4AAQSkZJRgABAgEASABIAAD/4RFZRXhpZgAATU0AKgAAAA...",
           "detect_direction":false,
           "quick_mode":false
         }

-  Transfer the URL of the image for recognition. During the recognition, the tilt angle of the image is not verified, and the quick mode is disabled.

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/ocr/general-text
        Request Header:
        Content-Type: application/json
        X-Auth-Token: MIINRwYJKoZIhvcNAQcCoIINODCCDTQCAQExDTALBglghkgBZQMEAgEwgguVBgkqhkiG...
        Request Body:
        {
            "url":"https://BucketName.obs.xxxx.com/ObjectName",
            "detect_direction":false,
            "quick_mode":false
         }

Example Response
----------------

**Status code: 200**

Example response for a successful request

.. code-block::

   {
     "result" : {
       "direction" : 67.6506,
       "words_block_count" : 1,
       "words_block_list" : [ {
         "words": "Word",
         "confidence" : 0.9999,
         "location" : [ [ 517, 447 ], [ 540, 504 ], [ 505, 518 ], [ 482, 461 ] ],
         "char_list" : [ {
           "char": "Character",
           "char_location" : [ [ 517, 447 ], [ 530, 479 ], [ 495, 493 ], [ 482, 461 ] ],
           "char_confidence" : 0.9999
         }, {
           "char": "Character",
           "char_location" : [ [ 530, 479 ], [ 540, 504 ], [ 505, 518 ], [ 495, 493 ] ],
           "char_confidence" : 0.9999
         } ]
       } ]
     }
   }

**Status code: 400**

Example response for a failed request

.. code-block::

   {
       "error_code": "AIS.0103",
       "error_msg": "The image size does not meet the requirements."
   }

Status Codes
------------

=========== =================================
Status Code Description
=========== =================================
200         Response for a successful request
400         Response for a failed request
=========== =================================

See :ref:`Status Codes <ocr_03_0090>`.

Error Codes
-----------

See :ref:`Error Codes <ocr_03_0028>`.
