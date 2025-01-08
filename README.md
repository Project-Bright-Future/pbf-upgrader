# App Update Notification

This project handles app version updates through an XML-based feed that triggers alerts within the app. The update feed is structured in the [RSS format](https://www.rssboard.org/), and it integrates with the Sparkle framework for macOS updates.

## Branches

- Release Version Branch: The release version of the app is managed in the `main` branch.
- Debug Version Branch: The debug version of the app is managed in the `test001` branch.

## Key Components of the XML

### 1. **Title**  
The title of the alert that will be displayed to the user when an update is available.
This is the message shown at the top of the update alert dialog.

### 2. **Description**  
This field provides details about the update.
This message is shown in the body of the alert dialog to inform the user about the improvements and fixes.

### 3. **Enclosure URL**  
The URL where the user can download the new version of the app. This URL will be embedded in the update alert. For example:  
**[https://onelink.to/zqfayt](https://onelink.to/zqfayt)**  
This URL directs users to the appropriate download page for the latest app version.

### 4. **App Version**  
The `sparkle:version` attribute indicates the version number of the app that is being offered in the update. It is used to compare against the user's current app version. If the user's app version is lower than the one specified here, the alert will trigger.  
For example:  
**`sparkle:version="1.3.19"`**  
The app will compare the user's installed version with this value to determine whether the update alert should be shown.

### 5. **Critical Update**  
If you uncomment the `<sparkle:criticalUpdate />` tag, the update becomes a mandatory update. This means the user will not be able to dismiss the alert and will be forced to update the app.  
For example:
```xml
<sparkle:tags>
  <sparkle:criticalUpdate />
</sparkle:tags>
```
This will ensure the user must update to the latest version before proceeding with using the app.

---

## How It Works

1. **App Version Comparison**:  
   The app compares the version number in the `sparkle:version` tag with the version currently installed on the user's device. If the app's version is lower, the update alert will appear.

2. **Display Alert**:  
   If an update is available, the app will show an alert dialog with the title, description, and a button linking to the download URL.

3. **Critical Update**:  
   If the `<sparkle:criticalUpdate />` tag is uncommented, the update becomes mandatory, and the user will not be able to dismiss the alert until the update is installed.

---

### Example XML

```xml
<?xml version="1.0" encoding="utf-8"?>
<rss version="2.0" xmlns:sparkle="http://www.andymatuschak.org/xml-namespaces/sparkle">
    <channel>
        <item>
            <title>New Version Update!</title>
            <description>In this version, we have fixed some bugs, improved app performance, and enhanced stability.</description>
            <enclosure url="https://onelink.to/zqfayt" sparkle:version="1.3.19" />
            <sparkle:tags>
                <!-- <sparkle:criticalUpdate /> -->
            </sparkle:tags>
        </item>
    </channel>
</rss>
```
