# Email Setup Instructions for Intake Form

This guide will help you set up EmailJS to send intake form submissions directly to your email (nazkorch@gmail.com) without needing a backend server.

## Step 1: Create a Free EmailJS Account

1. Go to [https://www.emailjs.com/](https://www.emailjs.com/)
2. Click "Sign Up" (it's free for up to 200 emails/month)
3. Create your account using your email

## Step 2: Add an Email Service

1. Once logged in, go to the **Email Services** page
2. Click **"Add New Service"**
3. Choose **Gmail** (since you're using nazkorch@gmail.com)
4. Click **"Connect Account"** and authorize with your Gmail account
5. After connecting, you'll see a **Service ID** (e.g., `service_abc123`)
6. **Copy this Service ID** - you'll need it later

## Step 3: Create an Email Template

1. Go to the **Email Templates** page
2. Click **"Create New Template"**
3. Give it a name like "Intake Form Submission"
4. In the template editor, use this content:

### Subject Line:
```
New Intake Form Submission from {{client_name}}
```

### Email Body (use the "Content" tab):
```
You have received a new intake form submission!

Client Name: {{client_name}}
Client Email: {{client_email}}
Client Phone: {{client_phone}}
Submission Date: {{submission_date}}

═══════════════════════════════════════
COMPLETE FORM RESPONSES
═══════════════════════════════════════

{{form_content}}

═══════════════════════════════════════
Reply to this client at: {{client_email}}
═══════════════════════════════════════
```

5. In the **Settings** tab:
   - Set "To Email" to: `nazkorch@gmail.com`
   - Set "From Name" to: `MindMapManifesto Intake Form`
   - Set "Reply To" to: `{{client_email}}`

6. Click **"Save"**
7. You'll see a **Template ID** (e.g., `template_xyz789`)
8. **Copy this Template ID** - you'll need it later

## Step 4: Get Your Public Key

1. Go to **Account** → **General** (or click your profile)
2. Find your **Public Key** (looks like a long string, e.g., `AbCdEfGh123456789`)
3. **Copy this Public Key**

## Step 5: Update the HTML File

Open `hypnotherapy_intake_page3.html` and find these three places to update:

### Location 1: Initialize EmailJS (around line 576)
```javascript
emailjs.init('YOUR_PUBLIC_KEY'); // Replace with your actual public key
```
Replace `YOUR_PUBLIC_KEY` with the public key you copied in Step 4.

### Location 2: Send Email (around line 650)
```javascript
emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', {
```
Replace:
- `YOUR_SERVICE_ID` with the Service ID from Step 2
- `YOUR_TEMPLATE_ID` with the Template ID from Step 3

### Example of what it should look like:
```javascript
// If your Public Key is: AbCdEfGh123456789
emailjs.init('AbCdEfGh123456789');

// If your Service ID is: service_abc123
// If your Template ID is: template_xyz789
emailjs.send('service_abc123', 'template_xyz789', {
    to_email: 'nazkorch@gmail.com',
    client_name: responses.full_name,
    client_email: responses.email,
    client_phone: responses.phone,
    form_content: emailContent,
    submission_date: new Date().toLocaleString()
})
```

## Step 6: Test the Form

1. Open `hypnotherapy_intake_page1.html` in your web browser
2. Fill out all three pages of the intake form
3. Submit the form on page 3
4. Check your email at nazkorch@gmail.com for the submission

## Troubleshooting

### Emails Not Arriving?
1. Check your EmailJS dashboard to see if the email was sent
2. Check your spam/junk folder
3. Verify all three IDs (Public Key, Service ID, Template ID) are correct
4. Make sure you authorized your Gmail account in EmailJS

### Error Messages?
1. Open browser console (F12) and check for errors
2. Make sure you have internet connection
3. Verify you haven't exceeded the 200 emails/month limit (check EmailJS dashboard)

### Gmail Security Issues?
- If EmailJS can't connect to Gmail, you may need to:
  1. Enable "Less secure app access" in Gmail settings, OR
  2. Use an "App Password" if you have 2-factor authentication enabled

## Privacy & Security

- EmailJS does NOT store your form data on their servers
- Data is transmitted directly via email
- No database or server storage is involved
- Client data is only temporarily in browser localStorage until submission
- After successful submission, localStorage is cleared

## Free Tier Limits

EmailJS free tier includes:
- 200 emails per month
- 2 email templates
- 1 email service
- Basic support

If you expect more than 200 submissions per month, consider upgrading to a paid plan.

## Need Help?

If you have issues setting this up, feel free to contact EmailJS support or check their documentation at:
https://www.emailjs.com/docs/
