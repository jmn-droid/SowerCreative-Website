# Client Intake System — To-Do

## Status
Tier 1 is fully done and tested. Tiers 2 and 3 still need to be built.

---

## Done
- [x] Tier 1 form live at `jmn-droid.github.io/SowerCreative-Website/intake/tier-1.html`
- [x] EmailJS wired — sends all form answers to jmn@sowercreative.com and kellen.r.snider@gmail.com
- [x] GHL webhook wired — creates contact on submission
- [x] GHL workflow "Web Intake V2" published (Inbound Webhook → Create/Update Contact → Add tag intake-tier1)
- [x] Tested and confirmed working

---

## To Do

### Step 1 — Create two GHL workflows for Tier 2 and Tier 3
In GHL, create two new workflows identical in structure to "Web Intake V2":
- Trigger: Inbound Webhook
- Action 1: Create/Update Contact (Email → Q7 - Lead email, Notes → Q1 - Business Info)
- Action 2: Add tag — `intake-tier2` for Tier 2, `intake-tier3` for Tier 3

Copy both webhook URLs and have them ready.

### Step 2 — Build Tier 2 and Tier 3 forms
Source files are at:
- `/Users/joedennelson/CLAUDE-WEBDESIGN/projects/sower-creative/forms/client-intake-tier2.html`
- `/Users/joedennelson/CLAUDE-WEBDESIGN/projects/sower-creative/forms/client-intake-tier3.html`

Claude will convert both using the same pattern as Tier 1:
- Remove Netlify attributes (`data-netlify`, `action="/"`, `method="POST"`, hidden `form-name` input)
- Add `<meta name="robots" content="noindex, nofollow">`
- Add EmailJS SDK and submit handler
- Wire GHL webhook URL (unique per tier)
- Change tier label in the send call

Output files go to:
- `SowerCreative-Website/intake/tier-2.html`
- `SowerCreative-Website/intake/tier-3.html`

### Step 3 — Push to GitHub
```
cd /Users/joedennelson/Desktop/SowerCreative-Website
git add intake/tier-2.html intake/tier-3.html
git commit -m "Add Tier 2 and Tier 3 intake forms"
git push origin main
```

### Step 4 — Test both forms
- Submit a fake intake on each form
- Confirm email lands in jmn@sowercreative.com and kellen.r.snider@gmail.com
- Confirm contact appears in GHL with correct tag

---

## Credentials

### EmailJS (already wired into all forms)
- Service ID: `service_p46bkwg`
- Template ID: `template_yq8jnns`
- Public Key: `qCrgLEk4HbUrkVyLh`
- Template subject: `New Intake — {{tier}}: {{client_name}}`
- Template body: `{{form_data}}`
- To Email field: `{{to_email}}`

### GHL
- Sub-account: Sower Creative LLC
- Location ID: `5Y0Jf0mLBFALgKRlteH3`
- Tier 1 webhook: `https://services.leadconnectorhq.com/hooks/5Y0Jf0mLBFALgKRlteH3/webhook-trigger/4454b349-b8c6-4969-8fa1-569e57686775`
- Tier 2 webhook: PENDING — create workflow and paste URL here
- Tier 3 webhook: PENDING — create workflow and paste URL here

---

## On the New Machine
Pull latest before starting:
```
cd /Users/joedennelson/Desktop/SowerCreative-Website
git pull origin main
```
