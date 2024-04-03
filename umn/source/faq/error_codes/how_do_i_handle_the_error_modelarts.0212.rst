:original_name: ocr_01_0103.html

.. _ocr_01_0103:

How Do I Handle the Error ModelArts.0212?
=========================================

If error message "Invalid Token header. The Token not contain project item." and error code "ModelArts.0212" are displayed when you call an OCR API, the token is invalid because the project information is missing.

OCR is a project-level service. To obtain the token for calling an OCR API, you need to set **scope** to **project**.
