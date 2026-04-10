<h2>WEEK 4: METADATA</h2>
a) Ocean.jpg image:

1. open browser and search for exif.tools
   <img width="1261" height="804" alt="image" src="https://github.com/user-attachments/assets/988d44a9-1a58-4b12-8a5a-7ef84171b9f9" />

2. upload the image into the exiftools section.
   <img width="1235" height="622" alt="Screenshot From 2026-04-10 22-10-55" src="https://github.com/user-attachments/assets/e01c184b-b585-47e2-88e8-394870ed1088" />

3. Then in the comment section shows the flags written directly "THIS IS THE HIDDEN FLAG"


b) Dog.jpg
1. navigate to the iamge folder where the image located.
2. run binwalk on the dog.jpg image
   <img width="545" height="357" alt="image" src="https://github.com/user-attachments/assets/d156db3a-11a7-4184-bc2c-cb5d2cd526f7" />

3. there are hidden_text.txt file
<img width="663" height="268" alt="image" src="https://github.com/user-attachments/assets/8025f376-647c-4a22-8a29-fef883bd4a9a" />

4. next extract the file using `binwalk -e dog.jpg`
   <img width="663" height="348" alt="image" src="https://github.com/user-attachments/assets/9b8b2853-befd-4ee5-b674-997461051c9e" />

5. then navigate to the extracted folder: `cd _dog.jpg.extracted`
   <img width="663" height="185" alt="image" src="https://github.com/user-attachments/assets/ef4b6721-ca6a-45de-9a81-8d1b8fcecc89" />

6. cat the hidden_text.txt file
7. the flag will show.
<img width="663" height="185" alt="image" src="https://github.com/user-attachments/assets/c1fc0d08-a90b-4240-a8be-8efb9cfc3b3d" />

   
c) Solitare.exe
1. check the solitare.exe using `file` command.
<img width="663" height="133" alt="image" src="https://github.com/user-attachments/assets/976588ff-c76b-44dd-9076-31ae970b6412" />

2. looks like the file type are .exe but it is .png .
3. rename the solitaire.exe file to the solitaire.png using `mv` command.
<img width="663" height="133" alt="image" src="https://github.com/user-attachments/assets/86d72c2b-2a50-425f-aa9a-23e96598e305" />

4. open the image using `ristretto` command.
   <img width="1920" height="963" alt="image" src="https://github.com/user-attachments/assets/55220081-a765-4e95-8f7d-ce46965111ba" />


d) rubiks.png
1. run the `file` command to check is it true png or just another illusion but the file is .jpg but after `file` command it shows PNG image data
   <img width="663" height="133" alt="image" src="https://github.com/user-attachments/assets/0dca0117-2c84-478b-b31c-001b512bdba8" />

2. rename the file using `mv` command.
<img width="663" height="182" alt="image" src="https://github.com/user-attachments/assets/05300931-5a10-4976-835e-92611da1eb7b" />

3. open the image using `ristretto` command
   <img width="1920" height="963" alt="image" src="https://github.com/user-attachments/assets/78792f0f-a885-4557-b02c-b9557f216b7c" />

d) computer.jpg
1. use `string` command to see the text hidden in the image.
   <img width="385" height="415" alt="image" src="https://github.com/user-attachments/assets/076e6871-c40f-49e5-be70-ec5ff22f6a76" />

2. open strings extractor in browser to find out what the strings is.
   <img width="1920" height="963" alt="image" src="https://github.com/user-attachments/assets/9badbcbf-f311-4753-82ec-4dc08ad0ffac" />







