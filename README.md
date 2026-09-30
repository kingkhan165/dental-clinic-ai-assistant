# Dental Clinic AI Assistant

This is an n8n workflow. It works as a WhatsApp helper for a dental clinic in Islamabad.

Patients send a message on WhatsApp. They can write in English or Roman Urdu. The bot can:

- Book an appointment
- Change (reschedule) an appointment
- Cancel an appointment
- Answer questions about services, prices, doctors and timings

## What it can do

- Uses Google Calendar to book, change and cancel appointments
- Checks if a time is free before booking
- Answers clinic questions from a text file you upload
- Remembers each patient's chat by their WhatsApp number
- If the AI forgets the name, phone, service or date, the workflow fills it back in
- Checks the rules: clinic is open Monday to Saturday, 10 AM to 8 PM, and every appointment is 1 hour
- Does not accept past dates or Sundays
- Shows an error message if something fails (it never says "booked" by mistake)

## How it works

1. A patient sends a WhatsApp message.
2. The AI reads the message and finds what the patient wants (book, change, cancel, or a question).
3. The workflow checks the details, the date and the clinic hours.
4. It checks Google Calendar.
5. It sends a reply to the patient on WhatsApp.

## What you need

- n8n
- WhatsApp Business Cloud API (from Meta)
- Google Calendar account
- Groq API key (for the AI model)
- Google Gemini API key (to read the clinic file)

## How to set it up

1. Open n8n. Click **Import from file** and choose `Dental-Clinic-AI-Assistant.json`.
2. Add your own credentials for WhatsApp, Google Calendar, Groq and Google Gemini.
3. Change these values to your own:
   - The Google Calendar email (in all calendar nodes)
   - The WhatsApp phone number ID (in the "Send message" node)
4. Open the upload form (the "On form submission" node). Upload a `.txt` file with your clinic information.
5. Publish the workflow.
6. Put the workflow's webhook URL in your Meta WhatsApp settings.

## Important notes

- The chat memory and the clinic information are saved in memory only. They are deleted when n8n restarts or when you publish again. After that, upload the clinic file again.
- The saved patient details work only in live (published) runs, not in test runs.
- The time zone is Asia/Karachi.
- A bigger AI model (like `gpt-oss-120b`) follows instructions better than a small one.

## Example clinic file

```
Clinic Name: ABC Dental Clinic

Doctors:
Dr Ahmed - General Dentist
Dr Sarah - Orthodontist

Services:
Dental Cleaning
Root Canal
Dental Filling
Braces

Prices:
Cleaning - Rs. 3000
Root Canal - Rs. 15000
Filling - Rs. 4000

Timings:
Monday to Saturday: 10 AM - 8 PM

Address:
I-9/3, Islamabad, Pakistan
```
