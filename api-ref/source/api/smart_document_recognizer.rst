:original_name: ocr_03_0161.html

.. _ocr_03_0161:

Smart Document Recognizer
=========================

Function
--------

This API recognizes text, analyzes layout, extracts key-value pairs, identifies tables in various formatted documents such as certificates, receipts, and forms, and converts the results into a structured JSON format.

Notes and Constraints
---------------------

-  English and Chinese are both supported, but the support for traditional Chinese characters is limited.
-  Only images in PNG, JPG, JPEG, BMP, GIF, TIFF, WebP, PCX, ICO or PSD format and PDF files can be recognized. PDF files can only be recognized one page at a time, but you can use the **pdf_page_number** parameter to specify which page you want to recognize.
-  No side of the image can be smaller than 15 or larger than 8,192 pixels.
-  The area to be recognized must occupy more than 80% of the image. When scanning a table, ensure that all text and its surrounding area are included in the image.
-  An image can be rotated to any angle.
-  For more accurate recognition results, the number of characters on a single page must be limited to 1,800 or less.
-  Text in images with complex backgrounds (such as outdoor scenery or anti-counterfeit watermarks) or distorted text cannot be analyzed.

URI
---

POST /v2/{project_id}/ocr/smart-document-recognizer

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

   +--------------+-----------+--------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter    | Mandatory | Type   | Description                                                                                                                                                                                          |
   +==============+===========+========+======================================================================================================================================================================================================+
   | X-Auth-Token | Yes       | String | User token. During API authentication using a token, the token is added to requests to obtain permissions for calling the API. The token is the value of **X-Subject-Token** in the response header. |
   +--------------+-----------+--------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Content-Type | Yes       | String | MIME type of the request body. The value is **application/json**.                                                                                                                                    |
   +--------------+-----------+--------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +-------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter               | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   +=========================+=================+=================+=====================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | data                    | No              | String          | Set either this parameter or **url**. Base64 encoded string of the image or PDF. The file has a size limit of 10 MB. No side of the image can be smaller than 15 or larger than 8,192 pixels. Only images in JPG, PNG, BMP, or TIFF format can be recognized. PDFs are converted to images with a resolution of 144 dpi for document analysis, and they must meet the image size requirements mentioned above. If a PDF has multiple pages, only the first page will be recognized. |
   +-------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | url                     | No              | String          | Set either this parameter or **image**. The image file has a size limit of 10 MB. The following image URLs are currently supported:                                                                                                                                                                                                                                                                                                                                                 |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                         |                 |                 | -  Public HTTP/HTTPS URL                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                         |                 |                 | -  URL provided by OBS.                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                         |                 |                 | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                         |                 |                 |    -  The API response time depends on the image download time. If the image download takes a long time, the API call will fail.                                                                                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 |    -  Ensure that the storage service where the images to be detected reside is stable and reliable. OBS is recommended for storing image data.                                                                                                                                                                                                                                                                                                                                     |
   |                         |                 |                 |    -  The URL cannot contain Chinese characters. If Chinese characters exist, they must be encoded using UTF-8.                                                                                                                                                                                                                                                                                                                                                                     |
   +-------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | single_orientation_mode | No              | Boolean         | Whether to enable the single direction mode. The options are:                                                                                                                                                                                                                                                                                                                                                                                                                       |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                         |                 |                 | -  **true**: Enables the single direction mode.                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                         |                 |                 | -  **false**: Disables the single direction mode.                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                         |                 |                 | Enabling this function when text in the image is oriented uniformly improves recognition accuracy. Disabling it when text in the image varies in direction allows for multi-direction text recognition. If not specified, **true** is used by default. In this case, the fields in the image are recognized as in a single direction by default.                                                                                                                                    |
   +-------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | language                | No              | String          | Language. If this parameter is not specified, German and English will be used by default. The options are:                                                                                                                                                                                                                                                                                                                                                                          |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                         |                 |                 | -  **auto**: automatic language classification                                                                                                                                                                                                                                                                                                                                                                                                                                      |
   |                         |                 |                 | -  **ms**: Malay                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | -  **uk**: Ukrainian                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
   |                         |                 |                 | -  **hi**: Hindi                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | -  **ru**: Russian                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                         |                 |                 | -  **vi**: Vietnamese                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                         |                 |                 | -  **id**: Indonesian                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                         |                 |                 | -  **th**: Thai                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                         |                 |                 | -  **zh**: Chinese and English                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
   |                         |                 |                 | -  **ar**: Arabic                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                         |                 |                 | -  **de**: German                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                         |                 |                 | -  **la**: Latin                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | -  **fr**: French                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                         |                 |                 | -  **it**: Italian                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                         |                 |                 | -  **es**: Spanish                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                         |                 |                 | -  **pt**: Portuguese                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                         |                 |                 | -  **ro**: Romanian                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   |                         |                 |                 | -  **pl**: Polish                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                         |                 |                 | -  **am**: Amharic                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                         |                 |                 | -  **ja**: Japanese                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   |                         |                 |                 | -  **ko**: Korean                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                         |                 |                 | -  **tr**: Turkish                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                         |                 |                 | -  **no**: Norwegian                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
   |                         |                 |                 | -  **da**: Danish                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                         |                 |                 | -  **sv**: Swedish                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                         |                 |                 | -  **km**: Khmer                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
   |                         |                 |                 | -  **he**: Hebrew                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   +-------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | kv                      | No              | Boolean         | Whether to extract key-value pairs. If you choose to extract key-value pairs, the results will be returned with the keyword **kv_result**.                                                                                                                                                                                                                                                                                                                                          |
   +-------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | table                   | No              | Boolean         | Whether to recognize tables. Here, tables refer to logical tables that typically have an M x N format and have a header in the first row or column. If you choose to recognize tables, the results will be returned with the keyword **table_result**.                                                                                                                                                                                                                              |
   +-------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | layout                  | No              | Boolean         | Whether to analyze the layout. If you choose to analyze the layout, the results will be returned with the keyword **layout_result**.                                                                                                                                                                                                                                                                                                                                                |
   +-------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | return_excel            | No              | Boolean         | This parameter is available only when **table** is set to **True**. Whether to return the Base64-encoded field for converting a table into a Microsoft Excel file.                                                                                                                                                                                                                                                                                                                  |
   +-------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | form                    | No              | Boolean         | Whether to recognize wired forms. A wired form displays crucial information in wired cells, like household registers and motor vehicle sales invoices. If you choose to recognize wired forms, the results will be returned with the keyword **form_result**.                                                                                                                                                                                                                       |
   +-------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | formula                 | No              | Boolean         | Whether to recognize formulas. The results are returned as a LaTeX sequence. If you choose to recognize formulas, the results will be returned with the keyword **formula_result**.                                                                                                                                                                                                                                                                                                 |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                         |                 |                 | -  Enabling formula recognition may slow down the response speed.                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                         |                 |                 | -  Recognition of formulas is currently limited to a maximum of three lines. Formulas longer than this limit will not be recognized.                                                                                                                                                                                                                                                                                                                                                |
   +-------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | kv_map                  | No              | String          | JSON-serialized string of a dictionary that needs to be passed in, which is used to normalize and map specific key values in **kv_result**. For example, if **kv_result** contains the key-value pair {"Name": "Xiaoming"}, passing in the **kv_map** {"Name": "Full name"} would result in {"Full Name": "Xiaoming"}.                                                                                                                                                              |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                         |                 |                 | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                         |                 |                 |    Example:                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |                         |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                         |                 |                 |    -  "kv_map":"{"Name":"Full name"}"                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   +-------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | erase_seal              | No              | Boolean         | Whether to erase the seal. Enabling it can enhance the character recognition accuracy in the area blocked by the seal.                                                                                                                                                                                                                                                                                                                                                              |
   +-------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | pdf_page_number         | No              | Integer         | Specify which page of the PDF to recognize. If this parameter is specified, the content on the specified page is identified. If not specified, the default is to recognize the first page.                                                                                                                                                                                                                                                                                          |
   +-------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameter

   +-----------+-----------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type                                                                                    | Description                                                                                                                                                                                      |
   +===========+=========================================================================================+==================================================================================================================================================================================================+
   | result    | Array of :ref:`SmartDocumentRecognizerResult <ocr_03_0161__table1786622902318>` objects | List of results returned in the order of the pages, with the first item in the list being the recognition result of the first page, and so on. This parameter is not included for a failed call. |
   +-----------+-----------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ocr_03_0161__table1786622902318:

.. table:: **Table 5** SmartDocumentRecognizerResult

   +----------------+-----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+
   | Parameter      | Type                                                                                                            | Description                                                                                        |
   +================+=================================================================================================================+====================================================================================================+
   | ocr_result     | :ref:`SmartDocumentRecognizerOcrResult <ocr_03_0161__table4867182911232>` object                                | Character recognition results                                                                      |
   +----------------+-----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+
   | kv_result      | :ref:`SmartDocumentRecognizerKvResult <ocr_03_0161__table1887062962312>` object                                 | Key-value pair extraction results. This parameter is returned only when **kv** is set to **true**. |
   +----------------+-----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+
   | table_result   | :ref:`SmartDocumentRecognizerTableResult <ocr_03_0161__table3873029172312>` object                              | Table recognition results. This parameter is returned only when **table** is set to **true**.      |
   +----------------+-----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+
   | layout_result  | :ref:`SmartDocumentRecognizerLayoutResult <ocr_03_0161__response_smartdocumentrecognizerlayoutresult>` object   | Layout analysis results. This parameter is returned only when **layout** is set to **true**.       |
   +----------------+-----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+
   | form_result    | :ref:`SmartDocumentRecognizerFormResult <ocr_03_0161__response_smartdocumentrecognizerformresult>` object       | Wired form recognition results. This parameter is returned only when **form** is set to **true**.  |
   +----------------+-----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+
   | formula_result | :ref:`SmartDocumentRecognizerFormulaResult <ocr_03_0161__response_smartdocumentrecognizerformularesult>` object | Formula recognition result                                                                         |
   +----------------+-----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+

.. _ocr_03_0161__table4867182911232:

.. table:: **Table 6** SmartDocumentRecognizerOcrResult

   +-------------------+--------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------+
   | Parameter         | Type                                                                                             | Description                                                                                                      |
   +===================+==================================================================================================+==================================================================================================================+
   | direction         | Float                                                                                            | Image direction                                                                                                  |
   +-------------------+--------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------+
   | words_block_count | Integer                                                                                          | Number of text blocks that have been recognized                                                                  |
   +-------------------+--------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------+
   | words_block_list  | Array of :ref:`SmartDocumentRecognizerWordsBlockList <ocr_03_0161__table58691029172319>` objects | List of text blocks that have been recognized. The output sequence is from left to right and from top to bottom. |
   +-------------------+--------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------+

.. _ocr_03_0161__table58691029172319:

.. table:: **Table 7** SmartDocumentRecognizerWordsBlockList

   +------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter  | Type                  | Description                                                                                                                                                                                                                                      |
   +============+=======================+==================================================================================================================================================================================================================================================+
   | words      | String                | Recognition result of a text block                                                                                                                                                                                                               |
   +------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | location   | Array<Array<Integer>> | List of location information about a text block, including the 2D coordinates (x, y) of four vertexes in the text area, where the coordinate origin is the upper-left corner of the image, the X axis is horizontal, and the Y axis is vertical. |
   +------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | confidence | Float                 | Confidence of a recognized text block                                                                                                                                                                                                            |
   +------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ocr_03_0161__table1887062962312:

.. table:: **Table 8** SmartDocumentRecognizerKvResult

   +----------------+--------------------------------------------------------------------------------------------+---------------------------------------------------+
   | Parameter      | Type                                                                                       | Description                                       |
   +================+============================================================================================+===================================================+
   | kv_block_count | Integer                                                                                    | Number of key-value pairs recognized by the model |
   +----------------+--------------------------------------------------------------------------------------------+---------------------------------------------------+
   | kv_block_list  | Array of :ref:`SmartDocumentRecognizerKVBlock <ocr_03_0161__table168711429142317>` objects | List of key-value pair recognition results        |
   +----------------+--------------------------------------------------------------------------------------------+---------------------------------------------------+

.. _ocr_03_0161__table168711429142317:

.. table:: **Table 9** SmartDocumentRecognizerKVBlock

   +-------------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | Parameter         | Type                                                                                         | Description                                                         |
   +===================+==============================================================================================+=====================================================================+
   | key               | String                                                                                       | Key in a key-value pair, for example, Name in Name: Xiaoming.       |
   +-------------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | value             | String                                                                                       | Value in a key-value pair, for example, Xiaoming in Name: Xiaoming. |
   +-------------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | words_block_count | Integer                                                                                      | Number of text boxes contained in the key-value pair                |
   +-------------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | words_block_list  | Array of :ref:`SmartDocumentRecognizerKVWordsBlock <ocr_03_0161__table128729290231>` objects | List of text box recognition results                                |
   +-------------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------+

.. _ocr_03_0161__table128729290231:

.. table:: **Table 10** SmartDocumentRecognizerKVWordsBlock

   +-----------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type                  | Description                                                                                                                                                                                                                                      |
   +===========+=======================+==================================================================================================================================================================================================================================================+
   | words     | String                | Recognition result of a text block                                                                                                                                                                                                               |
   +-----------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | location  | Array<Array<Integer>> | List of location information about a text block, including the 2D coordinates (x, y) of four vertexes in the text area, where the coordinate origin is the upper-left corner of the image, the X axis is horizontal, and the Y axis is vertical. |
   +-----------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | type      | String                | Type                                                                                                                                                                                                                                             |
   +-----------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ocr_03_0161__table3873029172312:

.. table:: **Table 11** SmartDocumentRecognizerTableResult

   +-------------+--------------------------------------------------------------------------------------------+------------------------------------------+
   | Parameter   | Type                                                                                       | Description                              |
   +=============+============================================================================================+==========================================+
   | table_count | Integer                                                                                    | Number of tables recognized by the model |
   +-------------+--------------------------------------------------------------------------------------------+------------------------------------------+
   | table_list  | Array of :ref:`SmartDocumentRecognizerTableBlock <ocr_03_0161__table188754293239>` objects | List of table recognition results        |
   +-------------+--------------------------------------------------------------------------------------------+------------------------------------------+

.. _ocr_03_0161__response_smartdocumentrecognizerlayoutresult:

.. table:: **Table 12** SmartDocumentRecognizerLayoutResult

   +--------------------+-----------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------+
   | Parameter          | Type                                                                                                                  | Description                                             |
   +====================+=======================================================================================================================+=========================================================+
   | layout_block_count | Integer                                                                                                               | Number of document layout areas recognized by the model |
   +--------------------+-----------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------+
   | layout_block_list  | Array of :ref:`SmartDocumentRecognizerLayoutBlock <ocr_03_0161__response_smartdocumentrecognizerlayoutblock>` objects | List of document layout area recognition results        |
   +--------------------+-----------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------+

.. _ocr_03_0161__response_smartdocumentrecognizerlayoutblock:

.. table:: **Table 13** SmartDocumentRecognizerLayoutBlock

   +-----------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type                  | Description                                                                                                                                                                                                                                      |
   +===========+=======================+==================================================================================================================================================================================================================================================+
   | location  | Array<Array<Integer>> | List of location information about a text block, including the 2D coordinates (x, y) of four vertexes in the text area, where the coordinate origin is the upper-left corner of the image, the X axis is horizontal, and the Y axis is vertical. |
   +-----------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | type      | String                | Document area type. The options are **text**, **title**, **sub_title**, **image**, **image_caption**, **form**, **table**, **table_caption**, **header**, **footer**, **page_number**, **reference**, **formula**, **stamp**, and **directory**. |
   +-----------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | text      | String                | Text in the document area. For tables and images, the text content is not returned.                                                                                                                                                              |
   +-----------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | words_ids | Array of integers     | Index list of character recognition results, indicating which text blocks in **words_block_list** of **ocr_result** are located within the document area.                                                                                        |
   +-----------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | table_id  | Integer               | This parameter is returned only when **type** is **table** and the input parameter **table** is **True**, indicating which recognition result corresponds to the current logical table area in **table_result**.                                 |
   +-----------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | form_id   | Integer               | This parameter is returned only when **type** is **form** and the input parameter **table** is **True**, indicating which recognition result corresponds to the current wired form area in **form_result**.                                      |
   +-----------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ocr_03_0161__response_smartdocumentrecognizerformresult:

.. table:: **Table 14** SmartDocumentRecognizerFormResult

   +------------+--------------------------------------------------------------------------------------------+-----------------------------------------------+
   | Parameter  | Type                                                                                       | Description                                   |
   +============+============================================================================================+===============================================+
   | form_count | Integer                                                                                    | Number of wired forms recognized by the model |
   +------------+--------------------------------------------------------------------------------------------+-----------------------------------------------+
   | form_list  | Array of :ref:`SmartDocumentRecognizerTableBlock <ocr_03_0161__table188754293239>` objects | List of wired form recognition results        |
   +------------+--------------------------------------------------------------------------------------------+-----------------------------------------------+

.. _ocr_03_0161__table188754293239:

.. table:: **Table 15** SmartDocumentRecognizerTableBlock

   +-------------------+---------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter         | Type                                                                                              | Description                                                                                                                                                                                                                                            |
   +===================+===================================================================================================+========================================================================================================================================================================================================================================================+
   | location          | Array<Array<Integer>>                                                                             | Location information of the current table, in list format, indicating the X and Y coordinates of the four vertices in a text block. The coordinate origin is the upper left corner of the image, the X axis is horizontal, and the Y axis is vertical. |
   +-------------------+---------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | words_block_count | Integer                                                                                           | Number of cells in a table                                                                                                                                                                                                                             |
   +-------------------+---------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | words_block_list  | Array of :ref:`SmartDocumentRecognizerTableWordsBlock <ocr_03_0161__table18876152942313>` objects | List of cell recognition results                                                                                                                                                                                                                       |
   +-------------------+---------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | excel             | String                                                                                            | Base64 encoded string of the table recognition results. This parameter is returned only when **return_excel** is set to **true**. You can use **base64.b64decode** to decode the returned Excel code and save it as an .xlsx file.                     |
   +-------------------+---------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ocr_03_0161__table18876152942313:

.. table:: **Table 16** SmartDocumentRecognizerTableWordsBlock

   +-----------+-------------------+--------------------------------------------------------------------------------------------------------------+
   | Parameter | Type              | Description                                                                                                  |
   +===========+===================+==============================================================================================================+
   | words     | String            | Character recognition results in a cell                                                                      |
   +-----------+-------------------+--------------------------------------------------------------------------------------------------------------+
   | rows      | Array of integers | Rows occupied by text. The values start from 0 and are displayed in a list. The data type is **Integer**.    |
   +-----------+-------------------+--------------------------------------------------------------------------------------------------------------+
   | columns   | Array of integers | Columns occupied by text. The values start from 0 and are displayed in a list. The data type is **Integer**. |
   +-----------+-------------------+--------------------------------------------------------------------------------------------------------------+

.. _ocr_03_0161__response_smartdocumentrecognizerformularesult:

.. table:: **Table 17** SmartDocumentRecognizerFormulaResult

   +---------------+-------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------+
   | Parameter     | Type                                                                                                                    | Description                                      |
   +===============+=========================================================================================================================+==================================================+
   | formula_count | Integer                                                                                                                 | Number of mathematical formulas                  |
   +---------------+-------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------+
   | formula_list  | Array of :ref:`SmartDocumentRecognizerFormulaBlock <ocr_03_0161__response_smartdocumentrecognizerformulablock>` objects | List of mathematical formula recognition results |
   +---------------+-------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------+

.. _ocr_03_0161__response_smartdocumentrecognizerformulablock:

.. table:: **Table 18** SmartDocumentRecognizerFormulaBlock

   +-----------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type                  | Description                                                                                                                                                                                                                      |
   +===========+=======================+==================================================================================================================================================================================================================================+
   | formula   | String                | Mathematical formula recognition results, which are represented as LaTeX strings                                                                                                                                                 |
   +-----------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | location  | Array<Array<Integer>> | Mathematical formula location information, in list format, indicating the X and Y coordinates of the four vertices. The coordinate origin is the upper left corner of the image and has a horizontal X axis and vertical Y axis. |
   +-----------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Status code: 400**

.. table:: **Table 19** Response body parameters

   +-----------------------+-----------------------+---------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                         |
   +=======================+=======================+=====================================================================+
   | error_code            | String                | Error code returned when the API fails to be called                 |
   |                       |                       |                                                                     |
   |                       |                       | This parameter is not returned when the API is successfully called. |
   +-----------------------+-----------------------+---------------------------------------------------------------------+
   | error_msg             | String                | Error message returned when the API fails to be called              |
   |                       |                       |                                                                     |
   |                       |                       | This parameter is not included when the API is successfully called. |
   +-----------------------+-----------------------+---------------------------------------------------------------------+

Example Request
---------------

-  Transfer the Base64 encoded string of the document image for recognition.

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/ocr/smart-document-recognizer

       {
         "data" : "/9j/4AAQSkZJRgABAgEASABIAAD/4RFZRXhpZgAATU0AKgAAAA..."
       }

-  Transfer the URL of the document image for recognition.

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/ocr/smart-document-recognizer

       {
         "url" : "https://BucketName.obs.xxxcloud.com/ObjectName"
       }

Example Response
----------------

**Status code: 200**

Example response for a successful request

.. code-block::

   {
     "result" : [ {
       "formula_result" : {
         "formula_count" : 1,
         "formula_list" : [ {
           "formula" : "\\\\int _ { L } \\\\left ( 2 x y ^ { 3 } - y ^ { 2 } \\\\cos x \\\\right ) \\\\mathrm { d } x + \\\\left ( 1 - 2 y \\\\sin x + 3 x ^ { 2 } y ^ { 2 } \\\\right ) \\\\mathrm { d } y",
           "location" : [ [ 171, 919 ], [ 950, 919 ], [ 950, 967 ], [ 171, 967 ] ]
         } ]
       }
     }, {
       "layout_result" : {
         "layout_block_count" : 19,
         "layout_block_list" : [ {
           "location" : [ [ 1165, 368 ], [ 2031, 368 ], [ 2031, 465 ], [ 1165, 465 ] ],
           "type" : "title",
           "text": "VAT Special Invoice",
           "words_ids" : [ 0 ]
         }, {
           "location" : [ [ 15, 19 ], [ 1078, 19 ], [ 1078, 637 ], [ 15, 637 ] ],
           "type" : "form",
           "text" : "xxxx",
           "words_ids" : [ 2, 3, 4 ],
           "form_id" : 0
         }, {
           "location" : [ [ 18, 180 ], [ 1077, 180 ], [ 1077, 636 ], [ 18, 636 ] ],
           "type" : "table",
           "text" : "xxxx",
           "words_ids" : [ 0, 1, 2 ],
           "table_id" : 0
         } ]
       }
     }, {
       "form_result" : {
         "form_count" : 1,
         "form_list" : [ {
           "location" : [ [ 15, 19 ], [ 1074, 19 ], [ 1074, 636 ], [ 15, 636 ] ],
           "words_block_count" : 24,
           "words_block_list" : [ {
             "words" : "xxx",
             "rows" : [ 0 ],
             "columns" : [ 0, 1, 2 ]
           }, {
             "words" : "xxxx",
             "rows" : [ 1 ],
             "columns" : [ 0, 1, 2 ]
           } ],
           "excel" : "UEsDBBQAAAAIAAAAIQBhXUk6TwEAAI8EAAATAAAAW0NvbnRlbnRfVHlwZX..."
         } ]
       }
     }, {
       "table_result" : {
         "table_count" : 1,
         "table_list" : [ {
           "words_block_count" : 24,
           "words_block_list" : [ {
             "words": "Name of goods or taxable labor services",
             "rows" : [ 0 ],
             "columns" : [ 0 ]
           }, {
             "words": "Specifications and model",
             "rows" : [ 0 ],
             "columns" : [ 1 ]
           } ],
           "excel" : "xxxx",
           "location" : [ [ 275, 967 ], [ 2919, 967 ], [ 2919, 1177 ], [ 275, 1177 ] ]
         } ]
       }
     }, {
       "kv_result" : {
         "kv_block_count" : 25,
         "kv_block_list" : [ {
           "key": "Invoice issuance date",
           "value": "August 31, 2017",
           "words_block_count" : 2,
           "words_block_list" : [ {
             "words": "Invoice issuance date",
             "location" : [ [ 2241, 589 ], [ 2480, 592 ], [ 2480, 646 ], [ 2241, 643 ] ],
             "type" : "key"
           }, {
             "words": "August 31, 2017",
             "location" : [ [ 2479, 591 ], [ 2850, 595 ], [ 2850, 649 ], [ 2479, 645 ] ],
             "type" : "value"
           } ]
         } ]
       }
     }, {
       "ocr_result" : {
         "direction" : 0.4767,
         "words_block_count" : 67,
         "words_block_list" : [ {
           "words": "Heilongjiang VAT Special Invoice",
           "location" : [ [ 430, 100 ], [ 874, 99 ], [ 874, 139 ], [ 430, 141 ] ],
           "confidence" : 0.9552
         } ]
       }
     } ]
   }

**Status code: 400**

Example response for a failed request

.. code-block::

   {
     "error_code" : "AIS.0103",
     "error_msg" : "The image size does not meet the requirements."
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
