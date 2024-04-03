:original_name: ocr_03_0031.html

.. _ocr_03_0031:

General Table
=============

Function
--------

This API detects and extracts text from table images and converts the text into JSON format. The returned results include two types of image area (words_region): text area (text) and table area (table). They also include table structures (rows and columns) and text information.

Constraints and Limitations
---------------------------

-  Only images in PNG, JPG, JPEG, BMP, or TIFF format can be recognized.
-  No side of the image can be smaller than 15 or larger than 8,192 pixels.
-  The area to be recognized must occupy more than 80% of the image. When scanning a table, ensure that the entire table and its surrounding area are included in the image.
-  An image can be rotated to any angle.
-  Text in images with complex backgrounds (such as outdoor scenery or anti-counterfeit watermarks) or distorted table lines cannot be recognized.
-  English and Chinese are supported but support for traditional Chinese characters is limited.

URI
---

POST /v2/{project_id}/ocr/general-table

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

   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                              |
   +=================+=================+=================+==========================================================================================================================================================+
   | X-Auth-Token    | Yes             | String          | User token.                                                                                                                                              |
   |                 |                 |                 |                                                                                                                                                          |
   |                 |                 |                 | Used to obtain the permission to call APIs. The token is the value of **X-Subject-Token** in the response header in :ref:`Authentication <ocr_03_0005>`. |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Content-Type    | Yes             | String          | MIME type of the request body. The value is **application/json**.                                                                                        |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +-----------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                   | Mandatory       | Type            | Description                                                                                                                                                                                             |
   +=============================+=================+=================+=========================================================================================================================================================================================================+
   | image                       | No              | String          | Set either this parameter or **url**.                                                                                                                                                                   |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | Base64-encoded image file. The image file has a size limit of 10 MB.                                                                                                                                    |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | No side of the image can be smaller than 15 or larger than 8,192 pixels. Only images in JPEG, JPG, PNG, BMP, or TIFF format can be recognized.                                                          |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | An example is **/9j/4AAQSkZJRgABAg...**. If the image data contains an unnecessary prefix, the error "The image format is not supported" is reported.                                                   |
   +-----------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | url                         | No              | String          | Set either this parameter or **image**. Image URL. Currently, the following URLs are supported:                                                                                                         |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | -  Public HTTP/HTTPS URL                                                                                                                                                                                |
   |                             |                 |                 | -  URL provided by OBS.                                                                                                                                                                                 |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | .. note::                                                                                                                                                                                               |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 |    -  The API response time depends on the image download time. If the image download takes a long time, the API call will fail.                                                                        |
   |                             |                 |                 |    -  Ensure that the storage service where the images to be detected reside is stable and reliable. OBS is recommended for storing image data.                                                         |
   |                             |                 |                 |    -  The URL cannot contain Chinese characters. If Chinese characters exist, they must be encoded using UTF-8.                                                                                         |
   +-----------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | return_text_location        | No              | Boolean         | Whether to return coordinates of text blocks and cells. Possible values are as follows:                                                                                                                 |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | -  **true**: Coordinates of text blocks and cells will be returned.                                                                                                                                     |
   |                             |                 |                 | -  **false**: Coordinates of text blocks and cells will not be returned.                                                                                                                                |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | If this parameter is not specified, **false** is used by default.                                                                                                                                       |
   +-----------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | return_char_location        | No              | Boolean         | Coordinate information of a single character. The options are as follows:                                                                                                                               |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | -  **true**: The coordinates of a single character will be returned.                                                                                                                                    |
   |                             |                 |                 | -  **false**: The coordinates of a single character will not be returned.                                                                                                                               |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | If this parameter is not specified, **false** is used by default. If this parameter is set to **true**, **return_text_location** must be **true**.                                                      |
   +-----------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | return_confidence           | No              | Boolean         | Whether the confidence will be returned. The options are as follows:                                                                                                                                    |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | -  **true**: The confidence will be returned.                                                                                                                                                           |
   |                             |                 |                 | -  **false**: The confidence will not be returned.                                                                                                                                                      |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | If this parameter is not specified, **false** is used by default. In this case, the confidence will not be returned.                                                                                    |
   +-----------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | return_excel                | No              | Boolean         | Whether to return the Base64-encoded field for converting a table into a Microsoft Excel file. The options are as follows:                                                                              |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | -  **true**: The Base64-encoded **excel** field will be returned.                                                                                                                                       |
   |                             |                 |                 | -  **false**: The Base64-encoded **excel** field will not be returned. The default value is **false**.                                                                                                  |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | You can use the Python function **base64.b64decode** to decode the returned Excel code and save it as an .xlsx file.                                                                                    |
   +-----------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | return_rectification_matrix | No              | Boolean         | The options are as follows:                                                                                                                                                                             |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | -  **true**: The perspective transformation matrix will be returned.                                                                                                                                    |
   |                             |                 |                 | -  **false**: The perspective transformation matrix will not be returned.                                                                                                                               |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | If this parameter is not specified, **false** is used by default. In this case, the perspective transformation matrix will not be returned.                                                             |
   +-----------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | with_borders                | No              | Boolean         | The options are as follows:                                                                                                                                                                             |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | -  **true**: The input image contains only bordered tables, and only such tables are recognized.                                                                                                        |
   |                             |                 |                 | -  **false**: The input image may contain borderless tables, and both bordered and borderless tables are recognized.                                                                                    |
   |                             |                 |                 |                                                                                                                                                                                                         |
   |                             |                 |                 | If this parameter is not specified, the default value **false** is used. If the input image contains only bordered tables, set this parameter to **true** to achieve more accurate recognition results. |
   +-----------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

.. note::

   The status code may vary depending on the recognition results. For example, **200** indicates that the API is successfully called, and **400** indicates that the API fails to be called. The following describes the status codes and corresponding response parameters.

**Status code: 200**

.. table:: **Table 4** Response body parameter

   +-----------------------+--------------------------------------------------+-----------------------------------------------------------------+
   | Parameter             | Type                                             | Description                                                     |
   +=======================+==================================================+=================================================================+
   | result                | :ref:`Table 5 <ocr_03_0031__table1561310103163>` | Calling result of a successful API call                         |
   |                       |                                                  |                                                                 |
   |                       |                                                  | This parameter is not included when the API fails to be called. |
   +-----------------------+--------------------------------------------------+-----------------------------------------------------------------+

.. _ocr_03_0031__table1561310103163:

.. table:: **Table 5** GeneralTableResult

   +--------------------+-----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter          | Type                                                      | Description                                                                                                                                                                                                                                        |
   +====================+===========================================================+====================================================================================================================================================================================================================================================+
   | words_region_count | Integer                                                   | Number of text areas                                                                                                                                                                                                                               |
   +--------------------+-----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | words_region_list  | Array of :ref:`Table 6 <ocr_03_0031__table9622110181613>` | List of recognition results in text areas. The output sequence is from left to right and from top to bottom.                                                                                                                                       |
   +--------------------+-----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | excel              | String                                                    | The table image is converted into the Base64 code of the Excel file. The text and table in the image are written into the Excel file by position. You can use **base64.b64decode** to decode the returned Excel code and save it as an .xlsx file. |
   +--------------------+-----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ocr_03_0031__table9622110181613:

.. table:: **Table 6** WordsRegionList

   +-----------------------+---------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                    | Description                                                                                                     |
   +=======================+=========================================================+=================================================================================================================+
   | type                  | String                                                  | Type of the text identification area. The options are as follows:                                               |
   |                       |                                                         |                                                                                                                 |
   |                       |                                                         | -  **text**: text recognition area                                                                              |
   |                       |                                                         | -  **table**: table recognition area                                                                            |
   +-----------------------+---------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | words_block_count     | Integer                                                 | Number of text blocks recognized in a sub-area                                                                  |
   +-----------------------+---------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | words_block_list      | Array of :ref:`Table 7 <ocr_03_0031__table16308106165>` | List of text blocks recognized in a sub-area. The output sequence is from left to right and from top to bottom. |
   +-----------------------+---------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------+

.. _ocr_03_0031__table16308106165:

.. table:: **Table 7** GeneralTableWordsBlockList

   +---------------+-----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter     | Type                                                      | Description                                                                                                                                                                                                                                  |
   +===============+===========================================================+==============================================================================================================================================================================================================================================+
   | words         | String                                                    | Recognition result of a text block                                                                                                                                                                                                           |
   +---------------+-----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | confidence    | Float                                                     | Average confidence of fields. A higher confidence indicates a higher accuracy of the field identified. The confidence is calculated using algorithms and is not the measured accuracy.                                                       |
   +---------------+-----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | location      | Array<Array<Integer>>                                     | Text block location information, in list format, indicating the X and Y coordinates of the four vertices in a text block. The coordinate origin is the upper left corner of the image, the X axis is horizontal, and the Y axis is vertical. |
   +---------------+-----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | words_list    | Array of :ref:`Table 8 <ocr_03_0031__table1664361091619>` | List of the character blocks in a cell. The text is from left to right and from top to bottom. This parameter is available only when the input parameter **return_text_location** is set to **true**.                                        |
   +---------------+-----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | rows          | Array of integers                                         | Rows occupied by text. The values start from 0 and are displayed in a list. The data type is **Integer**. This parameter is valid only in table recognition areas, that is, this parameter is valid only when **type** is **table**.         |
   +---------------+-----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | columns       | Array of integers                                         | Columns occupied by text. The values start from 0 and are displayed in a list. The data type is **Integer**. This parameter is valid only in table recognition areas, that is, this parameter is valid only when **type** is **table**.      |
   +---------------+-----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | cell_location | Array<Array<Integer>>                                     | Cell position information, in list format, indicating the X and Y coordinates of the four vertices in a cell. The coordinate origin is the upper left corner of the image, the X axis is horizontal, and the Y axis is vertical.             |
   +---------------+-----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ocr_03_0031__table1664361091619:

.. table:: **Table 8** WordsListIem

   +------------+-------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter  | Type                                                        | Description                                                                                                                                                                                                                                  |
   +============+=============================================================+==============================================================================================================================================================================================================================================+
   | words      | String                                                      | Recognition result of a text block                                                                                                                                                                                                           |
   +------------+-------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | confidence | Float                                                       | Average confidence of fields. A higher confidence indicates a higher accuracy of the field identified. The confidence is calculated using algorithms and is not the measured accuracy.                                                       |
   +------------+-------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | location   | Array<Array<Integer>>                                       | Text block location information, in list format, indicating the X and Y coordinates of the four vertices in a text block. The coordinate origin is the upper left corner of the image, the X axis is horizontal, and the Y axis is vertical. |
   +------------+-------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | char_list  | Array of :ref:`Table 9 <ocr_03_0031__table166501710111617>` | List of the character blocks in a cell. The text is from left to right and from top to bottom. This parameter is available only when the input parameters **return_text_location** and **return_char_location** are both set to **true**.    |
   +------------+-------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ocr_03_0031__table166501710111617:

.. table:: **Table 9** CharListIem

   +-----------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                  | Description                                                                                                                                                                                                                                             |
   +=================+=======================+=========================================================================================================================================================================================================================================================+
   | char            | String                | Recognition result of a single character                                                                                                                                                                                                                |
   +-----------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | char_confidence | Float                 | Confidence of a single character. A higher confidence indicates a higher accuracy of the field identified. The confidence is calculated using algorithms and is not equal to the accuracy.                                                              |
   +-----------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | char_location   | Array<Array<Integer>> | Location information of a single character, in list format, indicating the X and Y coordinates of the four vertices in a text block. The coordinate origin is the upper left corner of the image, the X axis is horizontal, and the Y axis is vertical. |
   +-----------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Status code: 400**

.. table:: **Table 10** Response body parameters

   +-----------------------+-----------------------+---------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                         |
   +=======================+=======================+=====================================================================+
   | error_code            | String                | Error code when calling the API failed                              |
   |                       |                       |                                                                     |
   |                       |                       | This parameter is not returned when the API is successfully called. |
   +-----------------------+-----------------------+---------------------------------------------------------------------+
   | error_msg             | String                | Error message when the API call fails                               |
   |                       |                       |                                                                     |
   |                       |                       | This parameter is not included when the API is successfully called. |
   +-----------------------+-----------------------+---------------------------------------------------------------------+

Example Request
---------------

-  Transfer the Base64 code of a table image for recognition and does not return the confidence.

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/ocr/general-table
        Request Header:
        Content-Type: application/json
        X-Auth-Token: MIINRwYJKoZIhvcNAQcCoIINODCCDTQCAQExDTALBglghkgBZQMEAgEwgguVBgkqhkiG...
        Request Body:
        {
           "image":"/9j/4AAQSkZJRgABAgEASABIAAD/4RFZRXhpZgAATU0AKgAAAAg...",
           "return_confidence":false
         }

-  Transfer the URL of a table image for recognition and does not return the confidence.

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/ocr/general-table
        Request Header:
        Content-Type: application/json
        X-Auth-Token: MIINRwYJKoZIhvcNAQcCoIINODCCDTQCAQExDTALBglghkgBZQMEAgEwgguVBgkqhkiG...
        Request Body:
        {
            "url":"https://BucketName.obs.xxxx.com/ObjectName",
            "return_confidence":false
         }

Example Response
----------------

**Status code: 200**

Example response for a successful request

.. code-block::

   {
     "result" : {
       "words_region_count" : 2,
       "words_region_list" : [ {
         "type" : "text",
         "words_block_count" : 1,
         "words_block_list" : [ {
           "words": "Text block 1 recognized in the text area",
           "confidence" : 0.9991
         } ]
       }, {
         "type" : "table",
         "words_block_count" : 2,
         "words_block_list" : [ {
           "words": "Text block 1 recognized in the table area",
           "confidence" : 0.9942,
           "rows" : [ 0 ],
           "columns" : [ 0 ]
         }, {
           "words": "Text block 2 recognized in the table area",
           "confidence" : 0.914,
           "rows" : [ 0 ],
           "columns" : [ 1, 2 ]
         } ]
       } ]
     }
   }

**Status code: 400**

Example response for a failed request

.. code-block::

   {
     "result" : {
       "error_code" : "AIS.0103",
       "error_msg" : "The image size does not meet the requirements."
     }
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
