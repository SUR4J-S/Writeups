## Broken QRRR
**Title:** Broken QRRR  
**Author:** Suraj 
**Points:** 200  

**Description:**  
Participants are provided with an RMQR code divided into four pieces. Upon joining the RMQR, they receive a fake flag, but hidden within the images are comments containing Morse code that reveals the real flag.

---

## Writeup
**Step 1: Analyze the RMQR Pieces**:  
   The challenge presents four pieces of an RMQR code. Initially, when participants join the RMQR, they receive a fake flag, creating a deceptive sense of accomplishment.

**Step 2: Use ExifTool to Inspect Metadata**:  
   Each RMQR piece may contain hidden comments or metadata. To extract this information, participants can use **ExifTool**, a powerful command-line utility for reading, writing, and editing metadata in various file formats,    including images. This tool is essential for uncovering any concealed messages.
   
   To inspect an image, the command is as follows:

   ```bash
   exiftool H5k7W2.jpg
   ```

   ![Exiftool](img/image.png)

**Step 3: Decode Morse Code:**

   Upon analyzing the images, you'll find a User Comment in the metadata consisting of dashes and dots, resembling Morse code. For example, the comment may appear as `.. . -- -... .-.. -.--`.

   To retrieve the actual flag, you need to join these Morse code segments in the order that reflects the arrangement of the original QR code pieces.

   The order is: X7f4J9.jpg, L2b8Q3.jpg, P9v1Z6.jpg, H5k7W2.jpg.

   You can use an online Morse code decoder to get the flag.

   [Morse Code Translator](https://morsecode.world/international/translator.html)

   ![Output Image](img/output.png)

**Flag:** cyberarc{d4sh_d0t_4ssembly}



