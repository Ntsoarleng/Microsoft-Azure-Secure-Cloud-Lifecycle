## Operational Excellence and Cost Management

The objectie here was to ensure that the WordPress migration remained within a predefined budget and to configure automated alerting to prevent cloud sprawl or unauthorized resource consumption. 

### Configuration details

1. Logged in to the Azure Portal
2. Navigated to "Cost Management + Billing" on the left menu and navigated to "Budgets".
   
   <img width="1600" height="750" alt="Screenshot (1087)" src="https://github.com/user-attachments/assets/41cb17b9-26b6-486c-860f-21e195e122d9" />

   <br>
3. I then created the budget, included its name, made it to reset monthly, and set it to $57 as per the suggested budget based on forecast.
   
   <img width="1600" height="758" alt="Screenshot (1088)" src="https://github.com/user-attachments/assets/1b948402-aa12-4402-8505-1fe3fc2648c0" />

   <br>
4. After creating the budget, I clicked "Next" to create the alerts. I set an alert for when the resources have consumed 50% of the budget and for when they are approaching 90% of the budget. The alerts will be sent to me through my email address.
   
   <img width="1600" height="758" alt="Screenshot (1089)" src="https://github.com/user-attachments/assets/6381df9b-bae4-49b0-becb-556fcd4b5174" />

   <br>
5. When I was done, I verified this configuration through "Budget summary", and everything was as I had set it.

   <img width="1600" height="761" alt="Screenshot (1090)" src="https://github.com/user-attachments/assets/491e64c8-4f28-4df5-a265-56847e9ef1ec" />

   <br>
Also, there is a real-time cost monitoring dashboard on the homepage of the Azure portal. It showed exactly what my Azure VM and storage had cost me since I started.

<img width="1600" height="659" alt="Screenshot (1091)" src="https://github.com/user-attachments/assets/a38920f6-8e2c-43ee-8d37-e87919163cb2" />

<br>

<br>

The implementation of automated budget thresholds and real-time cost alerts serves as a critical Governance guardrail, transitioning the project from a purely technical exercise to a managed business operation. By establishing a 50% warning and a 90% threshold, I have ensured continuous fiscal visibility and mitigated the risk of hidden costs or resource leaks. This practice aligns with AZ-900 best practices and enterprise GRC standards, proving that cloud resources are not only effectively deployed but are also monitored under a strict framework of financial and operational accountability.





   
