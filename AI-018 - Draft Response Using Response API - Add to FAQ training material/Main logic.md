# Main logic

1.Trigger: The flow starts when an email is flagged in a specific folder.

2.Initialize Variables: Sets up variables for authorization, model, user email, and placeholders for input, comments, and cleaned email content.

3.Extract Email Content: Uses OpenAI to clean and extract the main message from the email, removing signatures and disclaimers.

4.Draft Response: Composes a draft reply using OpenAI, referencing relevant documents and formatting as required. 

5.Approval Loop:
    Sends the draft for user approval.
    If not approved, allows for comments and re-drafting, repeating until approved or a limit is reached.

6.Post-Approval:
    Asks if the approved response should be added to the FAQ.
    If yes, creates a new FAQ entry in SharePoint and notifies the user.
    If no, sends a notification email. 7.Error Handling: Sends notifications if any step fails.

    