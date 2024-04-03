:original_name: ocr_01_0125.html

.. _ocr_01_0125:

How Do I Convert a PDF to an Image?
===================================

.. code-block::

   # -*- coding: utf-8 -*-
   import os
   import base64
   import fitz
   import io
   from PIL import Image
   from glob import glob

   class CovertPdfToJpg:
       def __init__(self, file_path, save_root):
           self.file_path = file_path
           self.save_root = save_root

       @staticmethod
       def open_pdf(file):
           return fitz.open(file)

       @staticmethod
       def get_trans(doc, page, min_side=0, max_side=0, rotate=0.0):
           """ Create a scale object. """
           region = doc[page].rect
           scale = 1
           if max_side > min_side > 0:
               scale = min_side / min(region.width, region.height)
               if max(region.width, region.height) * scale > max_side:
                   scale = max_side / max(region.width, region.height)
           trans = fitz.Matrix(scale, scale).preRotate(rotate)
           return trans

       def page2pix(self, doc, page, trans):
           """ Parse the current page as image data based on given parameters."""
           # Obtain the PDF format of a specified page. Note that page parameters need to be pre-parsed to avoid any issues.
           return doc[page].getPixmap(matrix=trans, alpha=False)

       def pdf_to_jpg(self, width=1024, height=1400):
           doc = self.open_pdf(self.file_path)
           save_dir = os.path.join(self.save_root)
           if not os.path.exists(save_dir):
               os.makedirs(save_dir)
           print("document", len(doc), doc.pageCount)
           for i in range(len(doc)):
               trans = self.get_trans(doc, i, width, height, rotate=0)
               try:
                   pdf = self.page2pix(doc, i, trans)
               except:
                   continue
               image = pdf.getPNGData()
               image = Image.open(io.BytesIO(image))
               print(os.path.join(
                   save_dir, os.path.basename(self.file_path).replace('.pdf', '') + '_' + str(i + 1) + '.jpg'))
               image.save(
                   os.path.join(save_dir, os.path.basename(self.file_path).replace('.pdf', '') + '_' + str(i + 1) + '.jpg'))
           return
