# Tesla email verification setup (EmailJS)

The board can email a 6-digit code to `@tesla.com` addresses using **EmailJS** (works from static GitHub Pages).

## Free setup (~5 minutes)

1. Create an account at [https://www.emailjs.com/](https://www.emailjs.com/)
2. **Email Services** → Add service (Gmail / Outlook / etc. that can send)
3. **Email Templates** → Create template with:

**To email:** `{{to_email}}`  
**Subject:** `Your Tonight's Tasks verification code`  
**Body example:**

```text
Your verification code for Tonight's Tasks is:

{{passcode}}

It expires in 10 minutes.
```

4. Copy:
   - **Public Key** (Account → API Keys)
   - **Service ID**
   - **Template ID**

5. In `index.html`, find `EMAIL_CONFIG` and fill in:

```javascript
const EMAIL_CONFIG = {
  publicKey: "YOUR_PUBLIC_KEY",
  serviceId: "YOUR_SERVICE_ID",
  templateId: "YOUR_TEMPLATE_ID",
  allowedDomains: ["tesla.com"],
  codeTtlMs: 10 * 60 * 1000,
  allowDemoCode: false, // turn off demo once email works
};
```

6. Push `index.html` to GitHub and hard-refresh.

## Demo mode

If EmailJS keys are empty and `allowDemoCode: true`, the code is **shown on screen** so you can test sign-in without email. Turn this **off** for real use.

## Flow

1. User taps **Sign in** (bottom-left)
2. Enters `name@tesla.com` → **Send Code**
3. Enters 6-digit code → **Verify**
4. Completing a task requires sign-in and writes to the **Audit Log**
5. Admin → **Audit Log** sees who completed what (synced via `board.json` on GitHub)

## Notes

- Only emails on allowed domains (default `tesla.com`)
- Session is stored in the browser until **Sign Out**
- Audit entries sync with the board over GitHub like tasks
