##   Data Migration and Content Integrity

Firstly, I checked the IP Address of the Cloud Shell and it was still the same as the one from the previous phase. This means that the session had not experired and changed the IP Address. Therefore, there was no need to change the NSG rules as the IP Address has remained the same from the last time the NSG rules were updated.

<img width="445" height="67" alt="Screenshot (1053)" src="https://github.com/user-attachments/assets/ec1d7732-a08d-467d-8402-e8e3897e3dfe" />

<br>

### Migration Overview:
In this phase, I will follow a 3 part process: The Export, The Handshake, and The Import.

1. The Export: I went to the WordPress legacy site and logged in.
   - Went to Tools > Export > All Content > Clicked on Download Export File. A .xml file downloaded on my computer. This file contained every post, page, commnent, amd category I ever made.

   <img width="1600" height="753" alt="Screenshot (1058)" src="https://github.com/user-attachments/assets/a4c862d9-b37c-4195-839d-a181fb50ba93" />
   <br>
   <img width="1268" height="143" alt="Screenshot (1059)" src="https://github.com/user-attachments/assets/17b691cf-12e0-43a4-b1b3-24bde5c0e700" />

   <br>

   The WordPress file was successfully exported.

3. The Setup: I went to my Virtual machine's publiv IP in my browser to finish the installation so as to have a dashboard to work in
   - Language: English
   - Site Title: Cyber Portfolio
   - Username: pinkyndlazi
   - Password: **** (chose a strong one suggested by the password manager)
   - Your email: provided my email address
   
     <img width="1600" height="779" alt="Screenshot (1060)" src="https://github.com/user-attachments/assets/1fa1f556-ef8f-48e9-8ab4-e2116480c42e" />
     <br>

     <img width="1600" height="521" alt="Screenshot (1062)" src="https://github.com/user-attachments/assets/652c243c-5335-44fb-b66b-4cae840d4448" />
     <br>

     WordPress installed successfully. I then logged in.

     <img width="1600" height="723" alt="Screenshot (1063)" src="https://github.com/user-attachments/assets/b569a594-d6f1-499b-a1bd-2e82b287a26a" />

     <br>


4. The Import: In the new, clean dashboard, I went to:
   - Tools > Import > Looked for WordPress at the bottom and clicked Install.
   - Once installed, I clicked on Run Importer > Upload the .xml file I doownloaded in step 1
   - Assign Authors: I decided to remain the author and not add new authors.
   - CRITICAL STEP: I checked the box that said, "Download and import file attachments". This tells the new server to reach out to the old one and grab all the images.

  <img width="1600" height="563" alt="Screenshot (1065)" src="https://github.com/user-attachments/assets/9c4c890f-e309-439d-977b-1de261490b2b" />
  <br>
  - Clicked sumbit and it was done.

    <img width="1600" height="443" alt="Screenshot (1066)" src="https://github.com/user-attachments/assets/a099d668-d294-4ea7-bb5d-f4d8d7a12981" />

    <br>


  




