:original_name: ocr_03_0162.html

.. _ocr_03_0162:

Permissions Policies and Supported Actions
==========================================

This section describes how you can use Identity and Access Management (IAM) for fine-grained permissions management of your OCR resources. If your account does not need individual IAM users, you may skip over this section.

New IAM users do not have any permissions by default. You need to add them to one or more groups and assign policies or roles to these groups. Users inherit permissions from the groups. Users then can perform specified operations on cloud services based on the permissions they have been granted.

You can grant permissions using roles and policies. Roles are a type of service-based, coarse-grained authorization mechanism provided by IAM to define permissions that match user responsibilities. Policies are more fine-grained, API-based permissions required to perform operations on specific cloud resources under certain conditions, meeting requirements for secure access control.

.. note::

   If you want to allow or deny the access to an API, use policy-based authorization.

An account has full permissions to call all APIs, but IAM users under the account must be granted the required permissions to make successful API calls. The permissions required for calling an API are determined by the actions supported by the API. Only users with granted permissions can call the API successfully.

Supported Actions
-----------------

OCR provides system-defined policies that can be directly used in IAM. You can also create custom policies to supplement system-defined policies for more refined access control. Actions supported by policies are specific to APIs. The following are common concepts related to actions:

-  Permissions: statements in a policy that allow or deny certain operations on specific resources under specific conditions.
-  APIs: APIs that can be called by a custom policy.
-  Actions: specific operations that are allowed or denied.
-  Dependencies: actions which a specific action depends on. When allowing an action for a user, you also need to allow any existing action dependencies for that user.

-  IAM or enterprise projects: type of projects for which an action will take effect. Policies that contain actions supporting both IAM and enterprise projects can be assigned to user groups and take effect in both IAM and Enterprise Management. Policies that only contain actions supporting IAM projects can be assigned to user groups and only take effect for IAM.

.. note::

   Y: supported; x: not supported

.. table:: **Table 1** Actions supported by OCR

   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
   | Permission                                                         | API         | Action                                           | IAM Project | Enterprise Project   |
   |                                                                    |             |                                                  |             |                      |
   |                                                                    |             |                                                  | (Project)   | (Enterprise Project) |
   +====================================================================+=============+==================================================+=============+======================+
   | Subscribing to General Text OCR                                    | x           | ocr:generalText:subscribe                        | Y           | x                    |
   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
   | Unsubscribing from General Text OCR                                | x           | ocr:generalText:unsubscribe                      | Y           | x                    |
   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
   | Listing the users who have subscribed to General Text OCR          | x           | ocr:generalText:getSubscribeUserList             | Y           | x                    |
   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
   | Subscribing to General Text OCR for other IAM users                | x           | ocr:generalText:subscribeAllUsers                | Y           | x                    |
   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
   | Unsubscribing from General Text OCR for other IAM users            | x           | ocr:generalText:unsubscribeAllUsers              | Y           | x                    |
   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
   | Subscribing to General Table OCR                                   | x           | ocr:generalTable:subscribe                       | Y           | x                    |
   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
   | Unsubscribing from General Table OCR                               | x           | ocr:generalTable:unsubscribe                     | Y           | x                    |
   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
   | Listing the users who have subscribed to General Table OCR         | x           | ocr:generalTable:getSubscribeUserList            | Y           | x                    |
   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
   | Subscribing to General Table OCR for other IAM users               | x           | ocr:generalTable:subscribeAllUsers               | Y           | x                    |
   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
   | Unsubscribing from General Table OCR for other IAM users           | x           | ocr:generalTable:unsubscribeAllUsers             | Y           | x                    |
   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
   | Subscribing to Smart Document Recognizer                           | x           | ocr:smartDocumentRecognizer:subscribe            | Y           | x                    |
   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
   | Unsubscribing from Smart Document Recognizer                       | x           | ocr:smartDocumentRecognizer:unsubscribe          | Y           | x                    |
   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
   | Listing the users who have subscribed to Smart Document Recognizer | x           | ocr:smartDocumentRecognizer:getSubscribeUserList | Y           | x                    |
   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
   | Subscribing to Smart Document Recognizer for other IAM users       | x           | ocr:smartDocumentRecognizer:subscribeAllUsers    | Y           | x                    |
   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
   | Unsubscribing from Smart Document Recognizer for other IAM users   | x           | ocr:smartDocumentRecognizer:unsubscribeAllUsers  | Y           | x                    |
   +--------------------------------------------------------------------+-------------+--------------------------------------------------+-------------+----------------------+
