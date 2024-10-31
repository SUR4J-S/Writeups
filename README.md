## Broken QRRR
**Title:** Broken QRRR  
**Author:** Suraj 
**Points:** 200  

**Description:**  
We've been provided with an RMQR code divided into four pieces. Upon scanning the RMQR using the **SCANDIT** app available on the Play Store, we will receive a fake flag. However, hidden within the images are comments containing Morse code that reveals the real flag.


---

## Writeup
**Step 1: Analyze the RMQR Pieces**:  
   The challenge presents four pieces of an RMQR code. Initially, when we scan the RMQR, we receive a fake flag.

**Step 2: Use ExifTool to Inspect Metadata**:  
   Each RMQR piece contains hidden comments or metadata. To extract this information, we can use **ExifTool**, a powerful command-line utility for reading, writing, and editing metadata in various file formats, including       images. This tool is essential for uncovering any concealed messages.
   
   To inspect an image, the command is as follows:

   ```bash
   exiftool H5k7W2.jpg
   ```

   ![Exiftool](img/image.png)

**Step 3: Decode Morse Code:**

   Upon analyzing the images, we'll find a User Comment in the metadata consisting of dashes and dots, resembling Morse code. For example, the comment may appear as `.. . -- -... .-.. -.--`.

   To retrieve the actual flag, we need to join these Morse code segments in the order that reflects the arrangement of the original QR code pieces.

   The order is: X7f4J9.jpg, L2b8Q3.jpg, P9v1Z6.jpg, H5k7W2.jpg.

   You can use an online Morse code decoder to get the flag.

   [Morse Code Translator](https://morsecode.world/international/translator.html)

   ![Output Image](img/output.png)

**Flag:** cyberarc{d4sh_d0t_4ssembly}



