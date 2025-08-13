# Main logic

1. Trigger: The flow starts when an email is flagged in a specific folder.

2. Initialize Variables: Sets up variables for authorization, model, user email, and placeholders for input, comments, and cleaned email content.

3. Extract Email Content: Uses OpenAI to clean and extract the main message from the email, removing signatures and disclaimers.

<img width="281" height="664" alt="image" src="https://github.com/user-attachments/assets/9f4561d4-14c0-4365-810f-d962c259f87f" />

4. Draft Response: Composes a draft reply using OpenAI, referencing relevant documents and formatting as required.
   
<img width="715" height="477" alt="image" src="https://github.com/user-attachments/assets/8880969f-7eb2-4532-9571-061d04d05378" />

6. Approval Loop:
    Sends the draft for user approval.
    If not approved, allows for comments and re-drafting, repeating until approved or a limit is reached.
   
![alt text](image.png)

If the responses is Reject the verify if you want to redo with the comments or cancel the progress.

![alt text](image-1.png)


8. Post-Approval:
    If the responses is approved, create a new FAQ entries in SharePoint and notify the user. Including the Score of the Answer.
    
![alt text](image-2.png)

9. Error Handling: Sends notifications if any step fails.


    
