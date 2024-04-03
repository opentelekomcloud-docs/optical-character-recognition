:original_name: ocr_03_0130.html

.. _ocr_03_0130:

Obtaining the Project ID
========================

A project ID or project name is required in some API requests. You need to obtain the project ID and name before calling an API.

Obtaining a Project ID and Name from the Console
------------------------------------------------

#. Log in to the management console.

#. In the upper right corner of the page, click the username and choose **My Credentials** from the drop-down list. The **My Credentials** page is displayed.

#. In the project list, view **Project ID** and **Project Name**.


   .. figure:: /_static/images/en-us_image_0000001750904201.png
      :alt: **Figure 1** Viewing the project ID and name

      **Figure 1** Viewing the project ID and name

   If there are multiple projects, unfold the target region and obtain the project ID from the **Project ID** column.

Obtaining a Project ID by Calling an API
----------------------------------------

You can obtain a project ID by calling the API used to `query project information based on the specified criteria <https://docs.otc.t-systems.com/identity-access-management/api-ref/apis/project_management/querying_project_information_based_on_the_specified_criteria.html>`__.

The API for obtaining a project ID is **GET https://**\ *{iam-endpoint}*\ **/v3/projects**. *{iam-endpoint}* indicates the endpoint of IAM, which can be obtained from :ref:`Endpoint <ocr_03_0062>`. For details about how to obtain the IAM endpoint, see :ref:`Authentication <ocr_03_0005>`.

The following is an example response. For example, if OCR is deployed in the **xxx** region, the value of **name** in the response body is **xxx**. The value of **id** in **projects** is the project ID. If there are multiple projects, unfold the target region and obtain the project ID from the **Project ID** column.

.. code-block::

   {
       "projects": [
           {
               "domain_id": "65382450e8f64ac0870cd180d14exxxx",
               "is_domain": false,
               "parent_id": "65382450e8f64ac0870cd180d14exxxx",
               "name": "xxx",    // Project name, which is the name of the deployment region.
               "description": "",
               "links": {
                   "next": null,
                   "previous": null,
                   "self": "https://www.example.com/v3/projects/a4a5d4098fb4474fa22cd05f897dxxxx"
               },
               "id": "a4a5d4098fb4474fa22cd05f897dxxxx",    // Project ID
               "enabled": true
           }
       ],
       "links": {
           "next": null,
           "previous": null,
           "self": "https://www.example.com/v3/projects"
       }
   }
