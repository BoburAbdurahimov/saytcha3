# Vercel Deployment Setup Guide 🚀

## Issue: Google Sheets Not Saving Data on Vercel

When you deploy to Vercel, your local `.env` file is **NOT** uploaded (it's in `.gitignore`). You need to configure environment variables directly in Vercel's dashboard.

---

## ✅ Solution: Configure Environment Variables in Vercel

### Step 1: Deploy Your Google Apps Script (If Not Done)

1. Open your Google Sheet: https://docs.google.com/spreadsheets/d/1Ystv4eBqN1Be4hoKrq9ya6A1lHIUqqVsSdromGp4XH0/edit
2. Click **Extensions** → **Apps Script**
3. Delete any existing code and paste the code from `google-apps-script.js`
4. Click **💾 Save**
5. Click **Deploy** → **New deployment**
6. Click the gear icon ⚙️ → Select **Web app**
7. Configure:
   - **Description**: "Hayot Yuli Form Handler"
   - **Execute as**: **Me (your email)**
   - **Who has access**: **Anyone**
8. Click **Deploy**
9. Click **Authorize access** and follow the prompts
10. **Copy the Web App URL** (looks like `https://script.google.com/macros/s/AKfycby.../exec`)

### Step 2: Add Environment Variable in Vercel

#### Option A: Via Vercel Dashboard (Recommended)

1. Go to your Vercel dashboard: https://vercel.com/dashboard
2. Click on your **hayotyuli-main** project
3. Click the **Settings** tab
4. In the left sidebar, click **Environment Variables**
5. Add a new variable:
   - **Name**: `VITE_GOOGLE_APPS_SCRIPT_URL_3`
   - **Value**: Paste the Web App URL you copied (e.g., `https://script.google.com/macros/s/AKfycby.../exec`)
   - **Environment**: Check all three boxes:
     - ✅ Production
     - ✅ Preview
     - ✅ Development
6. Click **Save**

#### Option B: Via Vercel CLI

```bash
vercel env add VITE_GOOGLE_APPS_SCRIPT_URL_3
```
Then paste your Google Apps Script URL when prompted.

### Step 3: Redeploy Your Application

After adding the environment variable, you need to redeploy:

#### Method 1: Via Dashboard
1. Go to **Deployments** tab
2. Click the **•••** menu on the latest deployment
3. Click **Redeploy**

#### Method 2: Push to Git
```bash
git add .
git commit -m "Trigger redeploy"
git push
```

#### Method 3: Via CLI
```bash
vercel --prod
```

### Step 4: Verify the Setup

1. Visit your Vercel site (e.g., `https://your-app.vercel.app`)
2. Fill out the registration form completely
3. Select subjects and complete the test
4. Check your Google Sheet for the new entry

---

## 🔍 Troubleshooting

### Still not saving data?

#### 1. Check if the environment variable is set correctly

In your Vercel dashboard:
- Go to **Settings** → **Environment Variables**
- Verify `VITE_GOOGLE_APPS_SCRIPT_URL_3` exists and has the correct URL
- Make sure it's enabled for **Production**

#### 2. Check the browser console

1. Open your deployed site
2. Press **F12** to open Developer Tools
3. Go to the **Console** tab
4. Submit a form
5. Look for any errors related to Google Sheets or CORS

Common errors:
- `"Google Apps Script URL not configured"` → Environment variable not set
- Network errors → Google Script deployment issue
- CORS errors → Script deployment settings incorrect

#### 3. Verify Google Apps Script Deployment

1. Open Apps Script editor
2. Click **Deploy** → **Manage deployments**
3. Verify:
   - **Execute as**: Me
   - **Who has access**: Anyone
4. Copy the **Web App URL** again and update in Vercel if different

#### 4. Test the Google Apps Script directly

Open this URL in your browser (replace with your actual Web App URL):
```
https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec
```

You should see a Google page (might show "Method Not Allowed" - that's OK, means it's accessible)

#### 5. Check Google Apps Script Logs

1. In Apps Script editor, click **Executions** (clock icon) in left sidebar
2. Look for recent executions
3. Check for any errors

---

## 📋 Quick Checklist

- [ ] Google Apps Script is deployed as Web App
- [ ] "Execute as" is set to "Me"
- [ ] "Who has access" is set to "Anyone"
- [ ] Web App URL is copied correctly
- [ ] Environment variable `VITE_GOOGLE_APPS_SCRIPT_URL_3` is added in Vercel
- [ ] Environment variable is enabled for Production
- [ ] Application has been redeployed after adding the variable
- [ ] Browser console shows no errors when submitting form

---

## 🎯 Common Mistakes

### ❌ Mistake 1: Using the wrong URL
- **Wrong**: Apps Script editor URL (ends with `/edit`)
- **Correct**: Web App deployment URL (ends with `/exec`)

### ❌ Mistake 2: Not redeploying after adding env variable
- Environment variables are loaded at **build time**
- You **must redeploy** after adding/changing them

### ❌ Mistake 3: Wrong environment variable name
- **Must be**: `VITE_GOOGLE_APPS_SCRIPT_URL_3` (exact spelling, including `VITE_`)
- Vite requires the `VITE_` prefix to expose variables to client code

### ❌ Mistake 4: Apps Script not authorized
- Make sure you clicked "Authorize access" during deployment
- You may need to approve permissions for the script

---

## 🔐 Security Note

The Google Apps Script Web App URL is designed to be public. However:
- Only people with access to the Google Sheet can **view** the data
- The script only **writes** data (doesn't expose existing data)
- Keep your Google Sheet permissions restricted

---

## 💡 Testing Locally (Optional)

To test with the same setup as Vercel locally:

1. Make sure your `.env` file has:
   ```
   VITE_GOOGLE_APPS_SCRIPT_URL_3=https://script.google.com/macros/s/.../exec
   ```

2. Restart your dev server:
   ```bash
   npm run dev
   ```

3. Test the form submission

---

## 📞 Still Having Issues?

If data is still not saving after following all steps:

1. **Check the exact error**: Open browser console (F12) and look for error messages
2. **Verify the deployment**: Make sure the Google Apps Script shows recent executions
3. **Test the endpoint**: Try accessing the Web App URL directly in your browser
4. **Check permissions**: Ensure your Google account has edit access to the spreadsheet

### Getting Help

When asking for help, provide:
- The error message from browser console
- Screenshot of Vercel environment variables page
- Confirmation that Google Apps Script is deployed
- Whether the script shows any executions in the Apps Script dashboard

---

## ✅ Success Indicators

You'll know it's working when:
1. ✅ Form submits without errors in console
2. ✅ You see new entries in Google Sheet "Responses" tab
3. ✅ Apps Script "Executions" log shows successful runs
4. ✅ Data includes all fields (including parent information)

---

**Remember**: The key difference between local and Vercel is that Vercel needs environment variables set in its dashboard, not in the `.env` file!
