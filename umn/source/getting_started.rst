:original_name: ocr_01_0153.html

.. _ocr_01_0153:

Getting Started
===============

Use Postman to call the General Text OCR API.

To call an OCR API, perform the following steps:

:ref:`Step 1: Subscribing to a Service <ocr_01_0153__section1471165201415>`

:ref:`Step 2: Configuring the Environment <ocr_01_0153__section169054167464>`

:ref:`Step 3: Using a Token for Authentication <ocr_01_0153__section92251373345>`

:ref:`Step 4: Calling the Service <ocr_01_0153__section26131714406>`

.. _ocr_01_0153__section1471165201415:

Step 1: Subscribing to a Service
--------------------------------

#. Log in to the OCR management console.

   Select a region based on service requirements. For details about the region where each service is deployed, see `Regions and Endpoints <https://docs.otc.t-systems.com/additional/endpoints.html>`__.

#. On the page displayed, select and subscribe to your desired APIs.

   For this example, subscribe to the General Text OCR API.

.. _ocr_01_0153__section169054167464:

Step 2: Configuring the Environment
-----------------------------------

Download and install `Postman <https://www.postman.com/downloads/>`__.

.. _ocr_01_0153__section92251373345:

Step 3: Using a Token for Authentication
----------------------------------------

Tokens are used for identity authentication and permission management when calling an OCR API.

Before calling an OCR API, you need first use the "Obtaining a Token" API to obtain the token value. Then, pass the token value into the request header parameter of the OCR API to authenticate the user's API request and enable the OCR service to verify their identity.

.. note::

   The token is valid for 24 hours.

To obtain the token, perform the following steps:

#. Log in to the cloud, hover your cursor over the username in the upper right corner, and choose **My Credentials**. On the **API Credentials** page displayed, obtain the username, domain name, and project ID.


   .. figure:: /_static/images/en-us_image_0000001707122028.png
      :alt: **Figure 1** Obtaining the username, domain name, and project ID

      **Figure 1** Obtaining the username, domain name, and project ID

#. Start Postman and create a POST request. For example, to obtain a token in the **eu-de** region, enter the following URL and request header parameter:

   -  URL: **https://iam.eu-de.otc.t-systems.com/v3/auth/tokens**
   -  Request header parameter: **Content-Type**; parameter value: **application/json**


   .. figure:: /_static/images/en-us_image_0000001755213865.png
      :alt: **Figure 2** Entering the URL and request header parameter

      **Figure 2** Entering the URL and request header parameter

#. Enter the request body of the API for obtaining a token. Click **Body**, select **raw**, copy and enter the following code by referring to :ref:`Figure 3 <ocr_01_0153__fig127711342268>`, and enter the username, domain name, and password.

   .. code-block::

      {
          "auth": {
              "identity": {
                  "methods": [
                      "password"
                  ],
                  "password": {
                      "user": {
                          "name": "username", // IAM username
                          "password": "********", // User password
                          "domain": {
                              "name": "domainname" // Domain name
                          }
                      }
                  }
              },
              "scope": {
                  "project": {
                      "name": "eu-de"
                  }
              }
          }
      }

   .. _ocr_01_0153__fig127711342268:

   .. figure:: /_static/images/en-us_image_0000001755220149.png
      :alt: **Figure 3** Request body

      **Figure 3** Request body

#. Click **Send** to send the request. If the status code **201** is returned, the API is successfully called. In this case, click **Headers**, find and copy the **X-Subject-Token** value, which is the token.

   .. _ocr_01_0153__fig173861228114918:

   .. figure:: /_static/images/en-us_image_0000001707404882.png
      :alt: **Figure 4** Obtaining a token

      **Figure 4** Obtaining a token

.. _ocr_01_0153__section26131714406:

Step 4: Calling the Service
---------------------------

#. Create a POST request in Postman and enter the API request address. For details, see "APIs" in *Optical Character Recognition API Reference*.

   Example: **https://ocr.eu-de.otc.t-systems.com/v2/{project_id}/ocr/general-text**

#. Set two request header parameters by referring to :ref:`Figure 5 <ocr_01_0153__fig14631357133312>`.

   -  **KEY**: **Content-Type**; **VALUE**: **application/json**

   -  **KEY**: **X-Auth-Token**; **VALUE**: the token value obtained in :ref:`Figure 4 <ocr_01_0153__fig173861228114918>`

      .. _ocr_01_0153__fig14631357133312:

      .. figure:: /_static/images/en-us_image_0000001707228246.png
         :alt: **Figure 5** Request header

         **Figure 5** Request header

#. Click **Body**, select **raw**, copy and enter the following code by referring to :ref:`Figure 6 <ocr_01_0153__fig0629142183912>`, and enter the request body.

   .. code-block::

      {
           "image":"/9j/4AAQSkZJRgABAgEASABIAAD/4RFZRXhpZgAATU0AKgAAAA...",
           "detect_direction":false,
           "quick_mode":false
         }

   .. _ocr_01_0153__fig0629142183912:

   .. figure:: /_static/images/en-us_image_0000001707396210.png
      :alt: **Figure 6** Request body

      **Figure 6** Request body

#. Click **Send** to send the request. If the status code **200** is returned, the API is successfully called and you can view the returned information in Postman.


   .. figure:: /_static/images/en-us_image_0000001707409654.png
      :alt: **Figure 7** Obtaining the calling result

      **Figure 7** Obtaining the calling result

.. note::

   -  If you encounter an error message in Postman while calling APIs that indicates an invalid SSL certificate, such as **self signed certificate**, **certificate has expired**, or **unable to verify the first certificate**, you can resolve the issue by disabling **SSL certificate verification** in Postman's settings.
   -  For details about the request and response parameters of OCR APIs, see *Optical Character API Reference*.
