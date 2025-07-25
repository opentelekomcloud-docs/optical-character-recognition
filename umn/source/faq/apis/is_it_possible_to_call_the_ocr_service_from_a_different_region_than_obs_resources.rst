:original_name: ocr_01_0078.html

.. _ocr_01_0078:

Is It Possible to Call the OCR Service From a Different Region Than OBS Resources?
==================================================================================

Cross-region OBS is not supported, and the OBS region must match the region of the service being called.

For OBS resources with public read authorization, they can be accessed over the Internet and can support cross-region calls. Although this is convenient, there is a risk of sensitive information leakage, such as personal private data. It is recommended that you use OCR and OBS services in the same region to avoid this risk.
