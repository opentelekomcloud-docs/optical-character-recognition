:original_name: ocr_03_0002.html

.. _ocr_03_0002:

Making an API Request
=====================

This section describes the structure of a REST API request, and uses the API `for obtaining a user token <https://docs.otc.t-systems.com/identity-access-management/api-ref/apis/token_management/obtaining_a_user_token.html>`__ as an example to demonstrate how to call an API. The obtained token can then be used to authenticate the calling of other APIs.

Request URI
-----------

A request URI is in the following format:

**{URI-scheme} :// {Endpoint} / {resource-path} ? {query-string}**

.. table:: **Table 1** Request URI

   +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter     | Description                                                                                                                                                                                                                |
   +===============+============================================================================================================================================================================================================================+
   | URI-scheme    | Protocol used to transmit requests. All APIs use **HTTPS**.                                                                                                                                                                |
   +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Endpoint      | Domain name or IP address of the server for the REST service endpoint. The endpoint varies depending on services in different regions. It can be obtained in :ref:`Endpoint <ocr_03_0062>`.                                |
   +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource-path | Access path of an API. Obtain the path from the URI of an API. For example, the **resource-path** of the API for obtaining a user token is **/v3/auth/tokens**.                                                            |
   +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | query-string  | (Optional) Query parameter. Put a question mark (?) at the beginning. The format is *Parameter name*\ **=**\ *Parameter value*. For example, **? limit=10** indicates that a maximum of 10 data records will be displayed. |
   +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   To simplify the URI display, each API is provided with only a **resource-path** and a request method. All API URI schemes are HTTPS and the endpoints are the same in the same region.

Request Method
--------------

HTTP defines the following request modes that can be used to send a request to the server:

.. table:: **Table 2** HTTP methods

   +-----------------------------------+-----------------------------------------------------------------------------+
   | Method                            | Description                                                                 |
   +===================================+=============================================================================+
   | GET                               | Request the server to return a specific resource.                           |
   +-----------------------------------+-----------------------------------------------------------------------------+
   | PUT                               | Request the server to update a specific resource.                           |
   +-----------------------------------+-----------------------------------------------------------------------------+
   | POST                              | Request the server to create a new resource or perform a special operation. |
   +-----------------------------------+-----------------------------------------------------------------------------+
   | DELETE                            | Request the server to delete a specific resource, such as an object.        |
   +-----------------------------------+-----------------------------------------------------------------------------+
   | HEAD                              | Request the server for the resource headers.                                |
   +-----------------------------------+-----------------------------------------------------------------------------+
   | PATCH                             | Request the server to update a portion of the resource content.             |
   |                                   |                                                                             |
   |                                   | PATCH may create a new resource if it does not exist.                       |
   +-----------------------------------+-----------------------------------------------------------------------------+

For example, if you use the POST method to obtain the URI of a user token, the request is as follows:

.. code-block:: text

   POST https://{iam-endpoint}/v3/auth/tokens

Request Header
--------------

You can add additional fields, for example, the fields required by a specified URI or HTTP method, to a request header. For example, add **Content-Type**, which specifies the request body type, to a request for the authentication information.

:ref:`Table 3 <ocr_03_0002__table2075523694911>` describes the common request header fields to be added to the request.

.. _ocr_03_0002__table2075523694911:

.. table:: **Table 3** Common request headers

   +-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+--------------------------------------------+
   | Header          | Description                                                                                                                                                                                                                                                                                                                                                        | Mandatory                                | Example                                    |
   +=================+====================================================================================================================================================================================================================================================================================================================================================================+==========================================+============================================+
   | Content-type    | Message body type (format). The default value is **application/json**.                                                                                                                                                                                                                                                                                             | Yes                                      | application/json                           |
   +-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+--------------------------------------------+
   | X-Auth-Token    | User token                                                                                                                                                                                                                                                                                                                                                         | Mandatory for token-based authentication | MIIPAgYJKoZIhvcNAQcCo...ggg1BBIINPXsidG9rZ |
   |                 |                                                                                                                                                                                                                                                                                                                                                                    |                                          |                                            |
   |                 | Response for calling the `Obtaining a User Token <https://docs.otc.t-systems.com/identity-access-management/api-ref/apis/token_management/obtaining_a_user_token.html>`__ API. This API is the only one that does not require authentication. After the request is processed, the value of **X-Subject-Token** in the response header (Header) is the token value. |                                          |                                            |
   +-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+--------------------------------------------+

The API used to `obtain a user token <https://docs.otc.t-systems.com/identity-access-management/api-ref/apis/token_management/obtaining_a_user_token.html>`__ does not require authentication. Therefore, only the **Content-Type** field needs to be added to requests for calling the API. An example of such requests is as follows:

.. code-block:: text

   POST https://{iam-endpoint}/v3/auth/tokens
   Content-Type: application/json

Request Body
------------

The body of a request is often sent in a structured format (JSON or XML) as specified in the **Content-Type** header field. The request body transfers content except the request header.

For an API, the request parameters and parameter description are available in the request. The following provides an example request with a body included. Replace *user_name*, *domain_name*, ``********`` (login password), and *xxxxxxxx* (project ID) with the actual values. To learn how to obtain a project ID, see :ref:`Obtaining the Project ID <ocr_03_0130>`.

.. note::

   The **scope** parameter specifies where a token takes effect. In the example, the token takes effect only for the resources in a specified project. OCR uses a region-specific endpoint to call this API. Set **scope** to **project**. You can set **scope** to an account or a project under an account.

.. code-block:: text

   POST https://{iam-endpoint}/v3/auth/tokens
   Content-Type:application/json
   {
     "auth": {
       "identity": {
         "methods": ["password"],
         "password": {
           "user": {
             "name": "user_name",
             "password": "********",
             "domain": {
               "name": "domain_name"
             }
           }
         }
       },
       "scope": {
         "project": {
           "name": "xxxxxxxx"
         }
       }
     }
   }

If all data required for the API request is available, you can send the request to call the API through `curl <https://curl.haxx.se/>`__, `Postman <https://www.getpostman.com/>`__, or coding. **x-subject-token** in the response header is the desired user token. This token can then be used to authenticate the calling of other APIs.
