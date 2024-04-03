:original_name: ocr_01_0062.html

.. _ocr_01_0062:

What Are the Username, Domain Name, and Project Name in the Token Message Body?
===============================================================================

*username* indicates the name of the user, and *domainname* indicates the name of the account to which the user belongs.

-  If the token is obtained by an account, **user name** and **domain name** are the same.
-  If the token is obtained by an IAM user (multiple IAM users can be created under an account), **user name** is a real-world username and is different from **domain name**.

*project name* indicates the project name, for example, **eu-de**. For details about how to obtain a project ID, see "Obtaining a Project ID" in *Optical Character Recognition API Reference*.
