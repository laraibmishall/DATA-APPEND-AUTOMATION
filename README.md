# Data Append — Feedback Form to Google Sheets

A lightweight n8n workflow that collects customer feedback through a web
form, automatically flags whether the customer should receive a discount
based on their feedback sentiment, and logs every submission to a Google
Sheet.

---

## What it does

1. **Form Trigger** — Displays a web form titled *"Test form for Feedback"*
   with the following fields:
   | Field | Type | Required |
   |---|---|---|
   | Email_id | Email | ✅ Yes |
   | Name | Text | No |
   | Age | Number | No |
   | Feedback | Dropdown (`Positive` / `Neutral` / `Negative`) | No |

2. **Conditional check (`If` node)** — Checks whether `Feedback` equals
   `"Positive"`.

3. **Tagging (`Set` nodes)**:
   - If feedback is **Positive** → adds a field `give_discount = "Yes"`
   - If feedback is **Neutral/Negative** → adds a field `give_discount = "No"`
   - (In both cases, all original form fields are preserved via
     `includeOtherFields`.)

4. **Append to Google Sheets** — Every submission (regardless of branch) is
   written as a new row to a Google Sheet, including the new
   `give_discount` field.

---

## Architecture
