:original_name: ocr_03_0005.html

.. _ocr_03_0005:

Authentication
==============

Token-based Authentication
--------------------------

.. note::

   A token is valid for 24 hours. When using a token for authentication, cache it to prevent frequently calling the IAM API.

A token is used to acquire temporary permissions. During API authentication using a token, the token is added to a request to get permissions for calling the API.

To call an API to obtain a user token, you need to set **auth.scope** to **project** in the request body.

.. code-block::

   {
       "auth": {
           "identity": {
               "methods": [
                   "password"
               ],
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

After a token is obtained, the **X-Auth-Token** header must be added to requests to specify the token when calling other APIs. For example, if the token is **ABCDEFJ....**, add **X-Auth-Token: ABCDEFJ....** to a request as follows:

.. code-block::

   Content-Type: application/json
   X-Auth-Token: ABCDEFJ....
