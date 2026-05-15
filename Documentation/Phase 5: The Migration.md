##   Data Migration and Content Integrity

Firstly, I checked the IP Address of the Cloud Shell and it was still the same as the one from the previous phase. This meant that the session had not expired and changed the IP Address. Therefore, there was no need to change the NSG rules as the IP Address had remained the same as the last time the NSG rules were updated.

<img width="445" height="67" alt="Screenshot (1053)" src="https://github.com/user-attachments/assets/ec1d7732-a08d-467d-8402-e8e3897e3dfe" />

<br>

### Migration Overview:
In this phase, I will follow a 3 part process: The Export, The Handshake, and The Import.

1. The Export: I went to the WordPress legacy site and logged in.
   - Went to Tools > Export > All Content > Clicked on Download Export File. A .xml file downloaded on my computer. This file contained every post, page, commnent, amd category I ever made.
   <br>

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
  
  Clicked on submit and it was done.

  <img width="1600" height="443" alt="Screenshot (1066)" src="https://github.com/user-attachments/assets/1679e6da-bba7-4d48-a9be-ec5f098cdaff" />

<br>

Lastly, after the migration I had to verify that it was carried out successfully and the result was what was expected.

I went to the browser, opened a new tab and pasted the virtual machine's IP address.

The result was:

<img width="1559" height="816" alt="wrong wordpress portfolio" src="https://github.com/user-attachments/assets/cb02e81a-50de-4176-8e22-6e541920dba0" />

<br>
<br>
This was not at all my portfolio page, and the theme was also wrong. To try to remediate this, I downloaded the LeanCV theme that I used for my portfolio because there was clearly a mismatch of schema. After downloading the theme, I applied it, and also tried to ensure that data integrity was maintained by going to All pages and making sure that all the migrated content in the .xml file was traslating in this environment, but first, I deleted all the pages and imported the .xml file again, just to reset everything.

<br>
<br>

The result:

<img width="1600" height="722" alt="theme default" src="https://github.com/user-attachments/assets/c790a6f6-2189-42dd-9980-bf859ffaa44f" />

<br>
<br>

The theme appeared along with the default content on the page. Nothing that belonged to my website portfolio reflected. I then went to the downloaded .xml file and opened it using Notepad:

<img width="1600" height="711" alt="Screenshot (1085)" src="https://github.com/user-attachments/assets/4af3dafd-8abe-46c9-a7d4-50f44cb710a1" />

<br>
<br>

The deployment phase encountered a significant Data Integrity hurdle during the migration from the legacy environment to the Azure-hosted WordPressinstance. The primary challenge was a Schema Mismatch within the source XML file; the automated import utility failed to parse the payload because the core content was nested within non-standard metadata tags ("<description >", "<title>", .etc) rather than the expected body tags ("<content:encoded >") as shown in the screenshot above. This resulted in "skeleton pages" that required immediate intervention to prevent data loss.

To remediate this, a surgical Manual Data Recovery strategy was executed. This involved a deep-dive audit of the XML source code to extract fragmented strings and a manual injection of the HTML payload directly into the WordPress application layer. 

<img width="1600" height="778" alt="copy-pasted xml file" src="https://github.com/user-attachments/assets/57992fbf-5edb-458f-b31e-6db4a34f0a10" />
<br>
<br>
<br>

By bypassing the faulty automated middleware, the project moved from a failed automated migration to a successful Verified Manual Reconstruction, ensuring that all professional credentials and project details were accurately reflected and localized on the Azure VM storage. 

Proof-of-Concept:

<img width="1600" height="790" alt="wordpress final result" src="https://github.com/user-attachments/assets/07814d21-6063-4e5d-9ad6-0749ce23f7ac" />







    


  




