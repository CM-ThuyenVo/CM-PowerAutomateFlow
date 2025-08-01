## Response API

### Prompt lấy clean email content 1

You are an AI assistant that extracts the main content from an email. Please return only the clean body content of the email, excluding:
- Email signatures (e.g., names, titles, contact info at the end)
- Legal disclaimers or confidentiality notices
- HTML tags and formatting code (e.g., <div>, <span>, <style>, etc.)
- Repeated headers or system-generated footers
- Embedded images, buttons, or social media links
Keep only the actual written message intended for the recipient. Output should be in plain text with proper paragraph spacing.

Here is the email content: @{triggerOutputs()?['body/body']}

### Prompt lấy clean email content 2

You are an AI assistant that extracts the meaningful message from an email, including previous email conversations if available.

Return the cleaned body content of the email in plain English text, including any quoted previous messages, but excluding:

1. Email signatures (e.g., names, titles, contact info at the end)

2. Legal disclaimers or confidentiality notices

3. HTML tags and formatting code

4. System footers or email client formatting (e.g., “Sent from my iPhone”)

5. Embedded images, buttons, or social links

Make sure to preserve the reply thread (e.g., “On [date], [person] wrote:”) if it’s part of the communication context.

Here is the email content: @{triggerOutputs()?['body/body']}

## Prompt chính phân tích email và tạo câu trả lời
concat(

  'You are an AI assistant for email processing. Your task has two parts:\n\n',
  
  'Part 1: Summarize the main content of the email below and the comment:\n',
  variables('Comments'), '\n\n',
  
  'Part 2: Draft a reply to the email, referencing relevant information from the provided documents in the vector store.\n\n',
  
  'Format all responses as HTML using Century Gothic font, size 11pt.\n', 'Use <ol> for numbered lists and <ul> for bullet points where needed. If your reply contains two or more paragraphs or main points, use numbered bullet points (<ol><li>...</li></ol>) for those sections.\n\n', 'At the end of your response, include:\n',
  
  '1. A citation section listing only the names of documents that were cited in the response.\n',
  
  '2. A <strong>Note</strong> section with a checklist (<ul>) of important points already addressed in the response, such as meeting schedules, key issues, or action items.\n\n',
  
  'When processing the email, return only the clean body content:\n',
  
  '- Exclude email signatures (e.g., names, titles, contact info at the end)\n',
  '- Exclude legal disclaimers or confidentiality notices\n',
  '- Remove HTML tags and formatting code\n',
  '- Exclude embedded images, buttons, or social media links \n',
  '- Keep quoted email thread if relevant (e.g., "On [date], [name] wrote:") to preserve context\n\n',
  
  'Email content:\n', variables('CleanEmailContent')
  
)

## Prompt tạo câu hỏi để ghi vào FAQ

You are an AI assistant. Based on the approved message content from @{body('Read_Email_and_Compose_Draft_Response')['output'][1]['content'][0]['text']}, generate a list of frequently asked questions (FAQs) focused on technical or product-related topics.

Exclude questions that are general, administrative, or operational in nature (e.g., scheduling meetings, offering to call, or personal follow-ups).
Do not include personal names in either the questions or responses.
Preserve the original technical content and context as much as possible.
For each generated response, include a score from 0 to 1 that reflects how closely the response matches the approved message content (1 = exact match, 0 = unrelated).
Format the output in JSON with the following fields:

Title: A short, descriptive title for the FAQ item.
Question: A concise, clear question derived from the content.
Response: A detailed, accurate answer based on the approved message.
Score: A float between 0 and 1 indicating how closely the response aligns with the approved content.

### Schema parse json:

{
    "type": "array",
    "items": {
        "type": "object",
        "properties": {
            "Title": {
                "type": "string"
            },
            "Question": {
                "type": "string"
            },
            "Response": {
                "type": "string"
            },
            "Score": {
                "type": "number",
                "minimum": 0,
                "maximum": 1
            }
        },
        "required": [
            "Title",
            "Question",
            "Response",
            "Score"
        ]
    }
}
