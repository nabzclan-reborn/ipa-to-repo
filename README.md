# 📦 IPA to Repo Integration Guide

This guide will help you convert your IPA file into a ready-to-use repository and integrate it with iOS app signers like AltStore, Scarlet, or Esign and more.

## 📌 Overview

The endpoint extracts necessary metadata from your IPA file and generates a repository JSON structure, which you can add to your iOS app signer of choice to make the app available for easy sideloading.

## 🌐 Endpoint URL

```
https://cdn.nabzclan.vip/ipa-to-repo
```

## 💭 Test

```bash
https://cdn.nabzclan.vip/ipa-to-repo?ipa_url=https://cloud.nabzclan.vip/file/5wc/P12Cracker_(Beta)-nabzclan.vip_1.0.ipa
```

## 🛠️ How to Use the Endpoint

### **Step 1: Provide Your IPA URL**

Ensure you have a direct download link to your IPA file. The URL must be publicly accessible.

### **Step 2: Make a Request**

You can use the following example to make a request to the endpoint using cURL, your browser, or any HTTP client.

#### Example Request

```text
 https://cdn.nabzclan.vip/ipa-to-repo?ipa_url=https://example.com/path/to/yourfile.ipa
```

### **Step 3: Obtain the Repository JSON**

The endpoint will return a JSON response containing your IPA's metadata formatted as a repository.

#### Example JSON Response

```json
{
  "name": "IPA TO Repo - YourAppName",
  "identifier": "org.repotoipa.repo-yourappname",
  "sourceURL": "https://cdn.nabzclan.vip/ipa-to-repo?ipa_url=https%3A%2F%2Fexample.com%2Fpath%2Fto%2Fyourfile.ipa",
  "iconURL": "https://cdn.nabzclan.vip/imgs/logo/logo_400x400.jpg",
  "website": "https://apps.nabzclan.vip",
  "subtitle": "Find more apps on the nabzclan - ipa library",
  "META": {
    "repoName": "IPA TO Repo - YourAppName",
    "repoIcon": "https://cdn.nabzclan.vip/imgs/logo/logo_400x400.jpg"
  },
  "apps": [
    {
      "name": "YourAppName",
      "type": 1,
      "bundleID": "com.example.yourapp",
      "bundleIdentifier": "com.example.yourapp",
      "version": "1.0.0",
      "versionDate": "2024-09-27",
      "fullDate": "20240927123456",
      "size": 12345678,
      "down": "https://example.com/path/to/yourfile.ipa",
      "downloadURL": "https://example.com/path/to/yourfile.ipa",
      "developerName": "",
      "localizedDescription": "Repo to install the YourAppName app",
      "icon": "data:image/png;base64,...",
      "iconURL": "data:image/png;base64,..."
    }
  ]
}
```

## 📲 Adding to iOS App Signers

Follow the steps below to add the generated repository to popular iOS app signers.

### 🔵 **Scarlet**

1. **Open Scarlet** on your iOS device.
2. Go to **Sources** and tap on the **+** icon to add a new source.
3. **Enter the `sourceURL`** from the JSON response as the URL:
   ```
   https://cdn.nabzclan.vip/ipa-to-repo?ipa_url=https%3A%2F%2Fexample.com%2Fpath%2Fto%2Fyourfile.ipa
   ```
4. Tap **Add** and wait for Scarlet to fetch the repository details.
5. Once added, your app should appear under the available apps list in Scarlet.

### 🟢 **AltStore**

1. Open **AltStore** on your iOS device.
2. Navigate to the **Sources** tab and tap the **+** button.
3. Enter the `sourceURL`:
   ```
   https://cdn.nabzclan.vip/ipa-to-repo?ipa_url=https%3A%2F%2Fexample.com%2Fpath%2Fto%2Fyourfile.ipa
   ```
4. Tap **Add Source** and allow AltStore to fetch the repository details.
5. The app will now be listed in AltStore, and you can sideload it directly.

### 🔴 **Esign**

1. Open the **Esign** app on your iOS device.
2. Go to **Repo** and tap on the **+** icon to add a new repository.
3. Paste the `sourceURL`:
   ```
   https://cdn.nabzclan.vip/ipa-to-repo?ipa_url=https%3A%2F%2Fexample.com%2Fpath%2Fto%2Fyourfile.ipa
   ```
4. Tap **Add** and wait for Esign to load the apps.
5. Your app should now be visible and ready for installation.

## ⚠️ Important Tips

- Always ensure your IPA URL is a **direct download link** (no redirects or authentication).
- Some cloud storage services (e.g., Google Drive, Dropbox) might not provide direct URLs; you may need to adjust sharing settings to generate a valid direct link.

## 🛠 Troubleshooting

- **Invalid URL Error**: Ensure that the `ipa_url` parameter is a valid, accessible URL.
- **Metadata Fallbacks**: If your IPA file doesn’t have all the required metadata, the system will use default values.

---

**Disclaimer**: This service is intended for legal use only. Ensure that you have the rights to distribute any IPA files you upload. Unauthorized distribution of IPA files may violate copyright laws.
