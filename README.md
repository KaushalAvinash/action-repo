# GitHub Action Repository

This repository is configured to send webhook events to a Flask application whenever Push, Pull Request, or Merge actions occur. It serves as the trigger source for the [webhook-repo](https://github.com/KaushalAvinash/webhook-repo) project.

## 🎯 Purpose

This repository demonstrates GitHub webhook integration by:
- Triggering webhook events on Git actions
- Sending event data to a webhook receiver
- Testing real-time event tracking and display

## 🔔 Webhook Events

This repository is configured to send webhooks for the following events:

### 1. **Push Event**
Triggered when code is pushed to any branch

**Example:**
```bash
git push origin main
```

### 2. **Pull Request Event**
Triggered when a pull request is opened

**Example:**
```bash
# Create feature branch
git checkout -b feature/new-feature

# Make changes and push
git push origin feature/new-feature

# Create PR on GitHub
```

### 3. **Merge Event**
Triggered when a pull request is merged

**Example:**
- Merge PR through GitHub interface

## ⚙️ Webhook Configuration

### Current Webhook Settings

- **Payload URL**: `https://your-webhook-url.com/webhook`
- **Content Type**: `application/json`
- **Events**: 
  - ✅ Pushes
  - ✅ Pull requests
- **Status**: Active ✓

### How to Update Webhook

1. Go to **Settings** → **Webhooks**
2. Click on the existing webhook
3. Update **Payload URL** if needed
4. Save changes

## 🧪 Testing the Webhook

### Test 1: Push Event
```bash
# Clone this repository
git clone https://github.com/KaushalAvinash/action-repo.git
cd action-repo

# Create a test file
echo "Test push event" > test.txt

# Commit and push
git add test.txt
git commit -m "Test push event"
git push origin main
```

**Expected Result:** Webhook receiver shows push event in UI

### Test 2: Pull Request Event
```bash
# Create feature branch
git checkout -b feature/test-pr

# Make changes
echo "Feature test" > feature.txt
git add feature.txt
git commit -m "Add feature"

# Push branch
git push origin feature/test-pr
```

Then create a Pull Request on GitHub from `feature/test-pr` to `main`

**Expected Result:** Webhook receiver shows pull request event in UI

### Test 3: Merge Event

1. Go to the Pull Request created in Test 2
2. Click **"Merge pull request"**
3. Confirm merge

**Expected Result:** Webhook receiver shows merge event in UI

## 📊 Webhook Event Data

### Push Event Payload Structure
```json
{
  "ref": "refs/heads/main",
  "pusher": {
    "name": "username"
  },
  "repository": {
    "name": "action-repo",
    "full_name": "username/action-repo"
  }
}
```

### Pull Request Event Payload Structure
```json
{
  "action": "opened",
  "pull_request": {
    "user": {
      "login": "username"
    },
    "head": {
      "ref": "feature-branch"
    },
    "base": {
      "ref": "main"
    }
  }
}
```

## 🔗 Related Repository

- [webhook-repo](https://github.com/KaushalAvinash/webhook-repo) - Flask application that receives and displays these webhook events

## 📝 Workflow
```
┌─────────────────┐
│   action-repo   │  (This Repository)
│                 │
│  1. git push    │
│  2. Create PR   │
│  3. Merge PR    │
└────────┬────────┘
         │
         │ Webhook Event
         │
         ▼
┌─────────────────┐
│  webhook-repo   │
│                 │
│  Flask Server   │
│  MongoDB Store  │
│  UI Display     │
└─────────────────┘
```

## 🛠️ Setup Instructions

### Initial Setup

1. **Fork or Clone** this repository
2. **Set up webhook** in repository settings
3. **Configure webhook receiver** URL from webhook-repo
4. **Test** by making commits, PRs, or merges

### Webhook Setup Steps

1. Go to **Settings** → **Webhooks** → **Add webhook**
2. Enter details:
   - **Payload URL**: Your webhook receiver URL + `/webhook`
   - **Content type**: `application/json`
   - **Events**: Select "Pushes" and "Pull requests"
3. Click **Add webhook**
4. Verify with a test push

## ✅ Verification

After setting up, verify the webhook is working:

1. **Check Webhook Status**
   - Go to Settings → Webhooks
   - Should show green checkmark ✓

2. **Check Recent Deliveries**
   - Click on webhook
   - Click "Recent Deliveries" tab
   - Should show successful deliveries (200 status)

3. **Check Webhook Receiver UI**
   - Visit webhook-repo UI
   - Should display recent events

## 🚨 Troubleshooting

### Webhook Shows Red X

- Check if webhook URL is accessible
- Verify webhook receiver is running
- Check firewall settings

### No Events Showing

- Ensure webhook is active
- Check "Recent Deliveries" for error messages
- Verify webhook receiver is processing events

### 401/403 Errors

- Check webhook secret (if configured)
- Verify authentication settings

## 📖 Documentation

- [GitHub Webhooks Documentation](https://docs.github.com/en/webhooks)
- [Webhook Events and Payloads](https://docs.github.com/en/webhooks/webhook-events-and-payloads)

## 🎓 Learning Resources

This repository is part of a developer assessment task focused on:
- GitHub webhook integration
- Event-driven architecture
- Real-time data synchronization
- RESTful API design

## 👤 Author

**AVINASH KAUSHAL**
- GitHub: [KaushalAvinash](https://github.com/KaushalAvinash)

## 📅 Created

January 2025

---

**Note:** This repository works in conjunction with [webhook-repo](https://github.com/KaushalAvinash/webhook-repo). Make sure both repositories are properly configured for the webhook integration to work correctly.