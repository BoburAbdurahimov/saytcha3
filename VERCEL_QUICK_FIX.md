# 🚨 QUICK FIX: Vercel Not Saving to Google Sheets

## The Problem
Your `.env` file works locally but Vercel doesn't use it. You need to add the environment variable in Vercel's dashboard.

---

## ⚡ Quick Fix (5 Minutes)

### 1️⃣ Get Your Google Apps Script URL

**First time?** Deploy the script:
1. Open: https://docs.google.com/spreadsheets/d/1Ystv4eBqN1Be4hoKrq9ya6A1lHIUqqVsSdromGp4XH0/edit
2. **Extensions** → **Apps Script**
3. Paste code from `google-apps-script.js`
4. **Deploy** → **New deployment** → **Web app**
5. Set: Execute as **Me**, Access **Anyone**
6. Click **Deploy** and authorize
7. **Copy the URL** (ends with `/exec`)

**Already deployed?** Get your URL:
1. Open Apps Script editor
2. **Deploy** → **Manage deployments**
3. Copy the **Web App** URL

### 2️⃣ Add to Vercel

1. Go to: https://vercel.com/dashboard
2. Click your **project**
3. **Settings** → **Environment Variables**
4. Click **Add**
5. Enter:
   ```
   Name:  VITE_GOOGLE_APPS_SCRIPT_URL_3
   Value: https://script.google.com/macros/s/YOUR_ID/exec
   ```
6. Check all three: ✅ Production ✅ Preview ✅ Development
7. Click **Save**

### 3️⃣ Redeploy

Choose one method:

**Method A - Git Push:**
```bash
git add .
git commit -m "trigger redeploy"
git push
```

**Method B - Dashboard:**
1. **Deployments** tab
2. **•••** menu → **Redeploy**

**Method C - CLI:**
```bash
vercel --prod
```

### 4️⃣ Test

1. Visit your live site
2. Fill and submit form
3. Check Google Sheet for new entry

---

## ✅ Success Checklist

Before testing, verify:

- [ ] Google Apps Script is deployed (check: Extensions → Apps Script → Deploy → Manage deployments)
- [ ] "Execute as" = **Me** (not "User accessing the app")
- [ ] "Who has access" = **Anyone**
- [ ] Web App URL ends with `/exec` (not `/edit`)
- [ ] Vercel environment variable name is **exactly**: `VITE_GOOGLE_APPS_SCRIPT_URL_3`
- [ ] Environment variable is enabled for **Production**
- [ ] You redeployed **after** adding the variable

---

## 🔍 Still Not Working?

### Check Browser Console
1. Open your Vercel site
2. Press **F12**
3. Go to **Console** tab
4. Submit form
5. Look for errors

**Common Errors:**

| Error Message | Solution |
|--------------|----------|
| "URL not configured" | Variable not set in Vercel |
| Network error / Failed to fetch | Script not deployed or wrong URL |
| CORS error | Script "Who has access" not set to "Anyone" |

### Check Apps Script Executions
1. Apps Script editor
2. Click **⏰ Executions** (left sidebar)
3. Look for recent runs
4. Check for errors

### Verify Environment Variable
In Vercel:
- Settings → Environment Variables
- Confirm `VITE_GOOGLE_APPS_SCRIPT_URL_3` exists
- Click the variable to see the value
- Make sure it starts with `https://script.google.com/macros/s/`

---

## 🎯 Quick Test

Test if your Apps Script is accessible:

1. Copy your Web App URL
2. Paste in browser address bar
3. You should see:
   - Google page (might say "Method Not Allowed" - that's OK!)
   - NOT a 404 error
   - NOT an access denied error

---

## 💡 Why This Happens

**Local (.env file)**:
- Works because Vite reads `.env` during development
- `.env` is in `.gitignore` so it doesn't get pushed to Git

**Vercel (Production)**:
- Doesn't have access to your local `.env`
- Needs variables configured in dashboard
- Variables are injected during build time

---

## 📞 Need More Help?

See full guide: `VERCEL_SETUP.md`

**When asking for help, provide:**
1. Error from browser console (F12)
2. Apps Script execution logs
3. Screenshot of Vercel environment variables
4. Confirmation that you redeployed

---

**Remember**: Always redeploy after adding/changing environment variables! 🔄
