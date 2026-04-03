# 🏫 School Fee Notification System

An automated fee notification workflow built with **n8n** that sends real-time **Telegram messages in Bangla** to parents when their child's semester fee status is updated in Google Sheets.

> Built as a portfolio project to demonstrate real-world automation for school management using no-code/low-code tools.

---

## 📸 Workflow Preview

> Import the JSON into your n8n instance to see the full canvas with sticky note.

---

## ✨ Features

- ✅ **Payment Confirmation** — Instantly notifies parents when fee is marked as paid
- ⚠️ **Payment Reminder** — Sends a polite reminder when fee remains unpaid
- 🔁 **Deduplication** — `message_sent` flag prevents duplicate notifications
- 🛡️ **Error Handling** — Error Trigger sends instant Telegram alert if workflow fails
- 🌐 **Bangla Language** — All parent messages sent in Bangla for local accessibility
- ⏰ **Runs Every Hour** — Fully automated, no manual intervention needed

---

## 🔁 Workflow Flow

```
Google Sheets Trigger (every hour)
  ↓
  ├── ✅ Filter: Paid & Unsent
  │     → Telegram: Payment Confirmation Message (Bangla)
  │     → Google Sheets: Mark Paid Notified (message_sent = true)
  │
  └── ⚠️ Filter: Unpaid & Unsent
        → Telegram: Payment Reminder Message (Bangla)
        → Google Sheets: Mark Unpaid Notified (message_sent = true)

Error Trigger → Telegram: Error Alert (instant admin notification)
```

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| n8n | Workflow automation engine |
| Google Sheets | Student data & fee records |
| Telegram Bot API | Parent notification delivery |

---

## 📊 Google Sheets Structure

Your sheet must have these columns:

| Column | Description |
|--------|-------------|
| `student_id` | Unique student identifier |
| `student_name` | Full name of student |
| `semester_fees` | Fee amount in BDT (৳) |
| `telegram_chat_id` | Parent's Telegram chat ID |
| `payment_status` | `paid` or empty |
| `message_sent` | `true` once notified |

---

## ⚙️ Setup & Installation

### Prerequisites
- n8n instance (self-hosted or cloud)
- Google Sheets with OAuth2 credentials
- Telegram Bot (create via [@BotFather](https://t.me/botfather))

### Steps

**1. Clone this repo**
```bash
git clone https://github.com/Siratalm/n8n_school_automation.git
```

**2. Import the workflow**
- Open your n8n instance
- Go to **Workflows → Import from file**
- Select `School_Fee_Notification_System.json`

**3. Configure credentials**
- Connect your **Google Sheets OAuth2** account
- Connect your **Telegram Bot API** token

**4. Update your Google Sheet ID**
- Replace the Sheet ID in the Google Sheets Trigger node with your own

**5. Set your admin Chat ID**
- In the `Error Alert` node, replace the Chat ID with your own Telegram ID
- Get yours by messaging [@userinfobot](https://t.me/userinfobot)

**6. Activate the workflow**
- Toggle the workflow to **Active**
- It will now run automatically every hour

---

## 📩 Sample Telegram Messages

**Payment Confirmation (Bangla)**
```
প্রিয় অভিভাবক,

আপনার সন্তান [Name] (আইডি: [ID]) এর এই সেমিস্টারের
ফি [Amount] টাকা সফলভাবে গ্রহণ করা হয়েছে। ✅

আপনার সময়মতো পেমেন্টের জন্য আন্তরিক ধন্যবাদ। 🎓✨

শুভকামনায়,
প্রশাসন বিভাগ 🌟
```

**Payment Reminder (Bangla)**
```
সম্মানিত অভিভাবক,

আপনার সন্তান [Name] এর এই সেমিস্টারের ফি বাবদ
[Amount] টাকা এখনও পরিশোধ করা হয়নি।

অনুগ্রহ করে দ্রুত ফি পরিশোধ করুন।

ধন্যবাদ,
প্রশাসন বিভাগ
```

---

## 🗂️ Project Structure

```
n8n_school_automation/
│
├── School_Fee_Notification_System.json   # n8n workflow export
└── README.md                             # Project documentation
```

---

## 🚀 Future Improvements

- [ ] Add attendance tracking workflow
- [ ] Monthly fee summary report via Telegram
- [ ] Multi-class support with class-wise filtering
- [ ] PostgreSQL integration for more robust data storage

---

## 👤 Author

**Md Mustakim Ali**
- GitHub: [@Siratalm](https://github.com/Siratalm)
- Built with n8n | Open to automation freelance projects

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
