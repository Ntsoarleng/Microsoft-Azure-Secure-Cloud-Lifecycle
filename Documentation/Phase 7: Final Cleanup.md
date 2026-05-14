## Resource Decommissioning and Secure Deletion

This is the part of the project where I prove that resource hygiene is just as important as deployment. By performing a clean wipe, I prove that I can manage the full lifecycle of an asset without leaving ghost resources that could lead to security vulnerabilities of unnecessary billing.


### Resource Decommissioning Overview:

1. Logged in to the **Azure Portal**.
2. Searched for **Resource Groups** in the top bar.
   <img width="1600" height="388" alt="Screenshot (1093)" src="https://github.com/user-attachments/assets/299e674b-71c4-468a-a027-5ff8941de204" />

<br>
4. Clicked on the Resource Group I had created for this project: RG-CyberPortfolio-Prod, and clicked on **Delete Resource group**.
   <img width="1600" height="542" alt="Screenshot (1094)" src="https://github.com/user-attachments/assets/02dae0bc-e5f8-414b-b58b-645b75b5edef" />
   
   <br>
   <img width="1600" height="713" alt="Screenshot (1096)" src="https://github.com/user-attachments/assets/fe46fbf3-3d2c-4ba2-89f9-cb9fb40c31c2" />

   <br>
   One of the security defenses I had enforced kicked back, and that was the lock. The resource group did not delete.

   <img width="872" height="233" alt="Screenshot (1097)" src="https://github.com/user-attachments/assets/e4eba35c-30c9-489b-9615-f96e0e328d24" />

   <br>

   To release the lock:
   - I went to the **Resource Group** that I am trying to delete.
   - On the left-hand sidebar, scrolled down to the **Settings** section, clicked on **Locks**, and saw the **Lock-PreventDelete** lock I had created earlier. Clicked the delete trash can icon next to the lock, and removed it.

     <img width="1600" height="573" alt="Screenshot (1099)" src="https://github.com/user-attachments/assets/14c9c305-e034-44b2-86f6-dc20050e1100" />

     <br>

5. I went back to the **Overview** blade and tried to delete the RG-Cyberportfolio-Prod resource group again.

   <img width="1600" height="595" alt="Screenshot (1101)" src="https://github.com/user-attachments/assets/f273056b-13c9-46c4-8480-5d26d36a6978" />

   <br>
   The resources in the Resource group were successfully deleted.




   

