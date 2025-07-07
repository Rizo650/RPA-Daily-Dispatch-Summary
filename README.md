# Daily Dispatch Summary Automation - UiPath RPA

This UiPath RPA project automates the dispatch reporting process by responding to **Power BI report emails** in real time using **Outlook Integration Service**. The bot extracts report images, performs **OCR** to detect valid content, and sends the image to **WhatsApp Web** with a static caption.

If the report is empty (e.g., contains “blank”), the process is intelligently skipped.

---

## Project Description

When a Power BI-generated dispatch report email arrives, the bot is triggered automatically through a webhook configured using **UiPath Integration Service for Outlook**. The bot reads the email, extracts the embedded report image, runs **OCR** on the image to determine whether it contains meaningful data, and takes further action accordingly.

If valid content is found, the bot sends the report image along with a captioned summary to a designated WhatsApp contact or group. A success notification email is also sent. If the report is blank or an error occurs, the bot logs the result and may send a failure email.

---

## Key Features

- **Real-time email trigger** via UiPath Integration Service (Outlook)
- Extracts embedded **Power BI report images** from incoming email
- Uses **OCR** to detect if the report is “blank”
- Skips processing if no dispatch data is found
- Sends the report image with caption via **WhatsApp Web**
- Sends success or error notification via email
- Built with **REFramework** for robust error handling and logging

---

## WhatsApp Message Format

- The bot sends the original **report image** from Power BI email.
- The image is sent with this fixed caption:

```
Daily Dispatch Summary 05 Juli 2025 from PowerBI

This message is generated automatically by Robotic Process Automation.
```

> Note: The date is dynamically generated based on system date or email metadata.

---

## Project Structure

| Folder/File                          | Description                                                      |
|--------------------------------------|------------------------------------------------------------------|
| Main.xaml                            | Main workflow, triggered by Outlook Integration webhook          |
| Modular/EmailProcessing.xaml         | Extracts image content from the dispatch report email            |
| Modular/ConstructMessage.xaml        | Generates static caption based on date                           |
| Modular/WhatsApp_OpenAndSendMsg.xaml | Sends image and caption via WhatsApp Web                         |
| Modular/EmailSuccess.xaml            | Sends email upon successful message delivery                     |
| Modular/EmailError.xaml              | Sends failure notification email in case of errors               |
| Data/Config.xlsx                     | Configuration file for email filters, contacts, etc.             |
| project.json                         | Project metadata and dependencies                                |
| README.md                            | Project documentation                                            |

---

## Process Workflow

1. **Trigger via Outlook Webhook**  
   - Automation starts automatically when a matching Power BI dispatch report email is received.

2. **Email & Image Extraction**  
   - Extracts embedded or attached report image from the email body.

3. **OCR Detection**  
   - Runs OCR to determine if the report contains valid data.  
   - If “blank” or no values are detected → process is skipped.

4. **Generate Message Caption**  
   - Constructs the following static message format:

     ```
     Daily Dispatch Summary [DATE] from PowerBI

     This message is generated automatically by Robotic Process Automation.
     ```

5. **Send to WhatsApp Web**  
   - Opens WhatsApp Web in a browser  
   - Sends the report image + caption to a predefined contact/group

6. **Send Notification Email**  
   - On success: `EmailSuccess.xaml` sends a confirmation  
   - On failure: `EmailError.xaml` is triggered

---

## How to Run

> Fully automated via Outlook webhook (Integration Service)

### Manual Testing Steps:

1. Open the project in **UiPath Studio**
2. Update `Config.xlsx` with:
   - Email subject filters (e.g., "Power BI Dispatch Report")
   - WhatsApp recipient/group name
3. Run `Main.xaml`
4. Check WhatsApp and email results

---

## Requirements

- UiPath Studio 2022.10 or later
- UiPath Integration Service with Outlook trigger enabled
- OCR Engine (e.g., UiPath.Tesseract OCR, Microsoft OCR)
- Access to WhatsApp Web in Chrome/Edge with extension
- Email access via Outlook or SMTP
- Network access to UiPath Orchestrator (recommended)

---

## Contact

For support, improvement suggestions, or collaboration:

- **Email:** fadillah650@gmail.com  
- **LinkedIn:** [Enrico Naufal Fadilla](https://linkedin.com/in/enrico-naufal-fadilla-54338a256)
