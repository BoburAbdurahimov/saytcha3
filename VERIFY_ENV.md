# 🔴 ERROR: "Google Apps Script URL not configured"

## What This Error Means
Vercel **CANNOT** find the `VITE_GOOGLE_APPS_SCRIPT_URL_3` environment variable. This means it's NOT set in Vercel's dashboard, or you haven't redeployed yet.

---

## ✅ SOLUTION: Follow These Steps Carefully

### Step 1: Verify You Have the Google Apps Script URL

Do you have the Google Apps Script deployed? 

**Check by doing this:**
1. Open: https://docs.google.com/spreadsheets/d/1Ystv4eBqN1Be4hoKrq9ya6A1lHIUqqVsSdromGp4XH0/edit
2. Click **Extensions** → **Apps Script**
3. Click **Deploy** → **Manage deployments**

**Do you see a Web App deployment?**
- ✅ **YES** → Copy the Web App URL (should end with `/exec`) and go to Step 2
- ❌ **NO** → Follow "First Time Setup" below, then go to Step 2

---

### First Time Setup (If No Deployment Exists)

1. In the Apps Script editor, **DELETE** all existing code
2. Open the file `google-apps-script.js` in your project
3. **Copy ALL the code** from that file
4. **Paste** it into the Apps Script editor
5. Click **💾 Save** (or Ctrl+S)
6. Click **Deploy** → **New deployment**
7. Click the **⚙️ gear icon** next to "Select type"
8. Choose **Web app**
9. Fill in:
   - Description: "Hayot Yuli Form Handler"
   - **Execute as**: **Me** (select your email)
   - **Who has access**: **Anyone**
10. Click **Deploy**
11. Click **Authorize access**
12. Select your Google account
13. Click **Advanced** → **Go to [Project Name] (unsafe)**
14. Click **Allow**
15. **COPY THE WEB APP URL** (it looks like `https://script.google.com/macros/s/AKfycby...LONG_ID.../exec`)

---

### Step 2: Add Environment Variable to Vercel Dashboard

**IMPORTANT**: Your local `.env` file does NOT work on Vercel. You MUST add it in Vercel's dashboard.

1. Go to: **https://vercel.com/dashboard**
2. Click on your **project** (hayotyuli or whatever you named it)
3. Click the **Settings** tab at the top
4. In the LEFT sidebar, click **Environment Variables**
5. Look for `VITE_GOOGLE_APPS_SCRIPT_URL_3`

**Is it there?**

#### If NO (variable doesn't exist):
1. Click **Add New** or **Add** button
2. Enter **EXACTLY** this:
   ```
   Name: VITE_GOOGLE_APPS_SCRIPT_URL_3
   ```
3. In the Value field, paste your Web App URL (from Step 1)
4. Under "Environment", check ALL THREE boxes:
   - ✅ Production
   - ✅ Preview
   - ✅ Development
5. Click **Save**
6. **GO TO STEP 3** (you MUST redeploy)

#### If YES (variable exists):
1. Click on the variable to view it
2. Verify the value:
   - Should start with: `https://script.google.com/macros/s/`
   - Should end with: `/exec`
   - Should be the EXACT URL from your Apps Script deployment
3. Verify **Production** is checked ✅
4. If anything is wrong, click **Edit** and fix it
5. **GO TO STEP 3** (you MUST redeploy)

---

### Step 3: Redeploy Your Application

**CRITICAL**: Environment variables are only loaded during the BUILD process. You MUST redeploy!

**Choose ONE method:**

#### Method A: Via Git (Recommended)
```bash
cd c:\Users\user\OneDrive\Desktop\HayotYuli-main
git add .
git commit -m "trigger redeploy with env vars"
git push
```

#### Method B: Via Vercel Dashboard
1. In your Vercel project, click the **Deployments** tab
2. Find the most recent deployment
3. Click the **•••** (three dots) menu button
4. Click **Redeploy**
5. Click **Redeploy** again to confirm

#### Method C: Via Vercel CLI (if installed)
```bash
cd c:\Users\user\OneDrive\Desktop\HayotYuli-main
vercel --prod
```

---

### Step 4: Wait for Deployment to Complete

1. In Vercel dashboard, go to **Deployments** tab
2. Wait for the deployment to show **"Ready"** status (usually 1-2 minutes)
3. The deployment card should have a green checkmark ✅

---

### Step 5: Test Again

1. Visit your Vercel site (e.g., `https://your-app.vercel.app`)
2. **Hard refresh** the page (Ctrl + Shift + R or Cmd + Shift + R)
3. Fill out the form and submit
4. Check the browser console (F12 → Console tab)
5. You should NOT see the error anymore

---

## 🔍 VERIFICATION CHECKLIST

Before testing, verify each of these:

### ✅ Google Apps Script
- [ ] Script is deployed (Extensions → Apps Script → Deploy → Manage deployments)
- [ ] Deployment type is "Web app"
- [ ] "Execute as" = **Me** (shows your email)
- [ ] "Who has access" = **Anyone**
- [ ] Web App URL ends with `/exec` (NOT `/edit`)
- [ ] You can access the URL in a browser (might show "Method Not Allowed" - that's OK)

### ✅ Vercel Environment Variable
- [ ] Variable name is **EXACTLY**: `VITE_GOOGLE_APPS_SCRIPT_URL_3` (case-sensitive!)
- [ ] Variable value is the full Web App URL from Apps Script
- [ ] Variable is enabled for **Production** environment
- [ ] Variable was entered in **Vercel Dashboard** (not just local .env)

### ✅ Deployment
- [ ] You redeployed AFTER adding/updating the environment variable
- [ ] Latest deployment shows "Ready" status with green checkmark
- [ ] Deployment was completed AFTER you added the env variable (check timestamp)

---

## 🎯 Common Issues

### Issue 1: "I added the variable but still get the error"
**Solution**: You MUST redeploy. Environment variables are only injected during build time, not runtime.

### Issue 2: "The variable is in my .env file"
**Solution**: Vercel CANNOT read your local `.env` file. You must add it in Vercel's dashboard.

### Issue 3: "I redeployed but still get the error"
**Solutions**:
1. Hard refresh your browser (Ctrl + Shift + R)
2. Clear browser cache
3. Verify the variable name is EXACTLY `VITE_GOOGLE_APPS_SCRIPT_URL_3` (check for typos)
4. Make sure "Production" environment is checked

### Issue 4: "Where do I find my Vercel project?"
1. Go to https://vercel.com/dashboard
2. You should see your project listed (might be called hayotyuli-main or similar)
3. Click on it to open project settings

---

## 📸 Screenshot Locations

I've generated visual guides showing:
1. Where to add environment variables in Vercel
2. What the Google Apps Script deployment should look like

Check the generated images in this conversation!

---

## 🆘 Still Getting the Error?

If you followed ALL steps above and still get the error, provide:

1. **Screenshot** of your Vercel Environment Variables page (Settings → Environment Variables)
2. **Screenshot** of your Apps Script deployment (Deploy → Manage deployments)
3. **Timestamp** of your latest Vercel deployment
4. **Exact error** from browser console (F12)

Then I can help diagnose the specific issue!

---

## ✅ Success Indicator

You'll know it's working when:
- ✅ Form submits WITHOUT the "URL not configured" error
- ✅ New row appears in your Google Sheet
- ✅ Apps Script shows execution in the Executions log

---

**Remember**: The #1 reason for this error is forgetting to redeploy after adding the environment variable! 🔄
