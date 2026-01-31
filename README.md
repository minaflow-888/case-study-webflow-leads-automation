# Automated Lead Capture (Webflow → Sheets → Slack → Email)

A Make.com workflow that captures Webflow contact form leads, stores them in Google Sheets, sends a Slack alert, and replies via email automatically.



A lightweight lead-capture automation built in **Make.com**.  
When a visitor submits the **Webflow** contact form, the workflow instantly:
1) parses the email notification,  
2) logs the lead in **Google Sheets**,  
3) posts a notification to **Slack**, and  
4) sends an **automatic confirmation email** to the lead.

---

## Problem

Manual handling of contact form submissions often causes:
- missed leads (messages get buried in inboxes)
- slow response time (poor first impression)
- no centralized tracking (hard to follow up consistently)

---

## Solution (Workflow)

**Trigger:** Webflow contact form submission → Email notification → Make mailhook

**Automation steps:**
1. **Webhooks (Custom mailhook)** – receives the Webflow form email instantly  
2. **Text parser (Match pattern)** – extracts `name`, `email`, `message` from the email body  
3. **Google Sheets (Add a row)** – stores every lead (Timestamp, Name, Email, Message, Source)  
4. **Slack (Send a message)** – posts a new-lead alert in `#leads`  
5. **Email (Send an email)** – auto-reply confirmation to the lead

> **Filter:** `Email not empty` prevents invalid / empty submissions.

---

## Results

- **Instant confirmation** to the lead (better experience)
- **All leads stored** in one place (Sheets)
- **Real-time alerts** for fast follow-up (Slack)
- **Less manual work**, fewer missed messages

---

## Key Implementation Details

### 1) Parsing from Webflow email notification
Webflow sends all fields inside one email text block.  
I used **Text parser → Match pattern** with named groups to extract structured values:
- `name`
- `email`
- `message`

### 2) Reliable storage in Google Sheets
- Headers must be in **Row 1**
- If sheet columns change, refresh fields in the Make module
- `Source` is a fixed label (ex: `Webflow Contact Form`) for reusability across projects

### 3) Slack alert formatting
The Slack message includes key lead details for quick scanning:
- Name
- Email
- Message (short)

### 4) Auto-reply email
A short, professional confirmation message:
- acknowledges receipt
- sets response expectations (ex: “within 24 hours”)
- includes the original message for clarity

---

## Screenshots (to be added)

> I will add screenshots here once sensitive data is blurred.

- Webflow form submission
- Make.com scenario overview
- Text parser pattern + output
- Google Sheets row created
- Slack #leads notification
- Email auto-reply

---

## Notes on Privacy

All screenshots in this repository will have **emails / tokens blurred**.

---

## Tech Stack

- Webflow (Contact Form)
- Make.com (Scenario automation)
- Google Sheets
- Slack
- Email (SMTP/IMAP connection)
