# Didit Privacy Policy

**Effective date: November 1, 2026**

[한국어](../) · English

Didit (the "App") is developed and operated by KiHoon Nam (남기훈), an individual developer in the Republic of Korea (the "Operator"). The Operator respects your privacy and complies with applicable laws, including the Korean Personal Information Protection Act and, where it applies to you, the EU and UK General Data Protection Regulation (GDPR), as well as the Google Play Developer Policy and the Apple App Store Review Guidelines. This policy explains how the Didit apps for Android, iOS (including widgets), macOS (including widgets) and Windows, and the Didit websites, handle your information.

This English version is a translation of the Korean original. If they differ, the Korean version prevails, except where the law of your country requires otherwise.

---

## 1. Information we process

Didit has no sign-up, does not collect advertising identifiers, and uses no analytics, usage tracking or ads. The Operator's servers do not store your tasks or account information.

### 1) Data stored on your device (required)
* **What**: the tasks you write, completion times, app settings (notifications, widgets, theme, etc.), and a random identifier for each device (used for sync, see 3 below).
* **Where**: your device's internal storage (Android: the app's private database; iOS and macOS: a private storage area shared only by the app and its Didit widgets; Windows: the `%LOCALAPPDATA%\Didit` folder).
* **Leaving the device**: unless you turn on cloud sync, the App does not send your tasks off your device. However, operating-system backup and transfer features that you have turned on (such as Google backup and device-to-device transfer on Android, or iCloud Backup and device transfer on iPhone) may include your tasks and settings. Your Google sign-in credentials are never included in such backups or transfers.
* **Error logs**: error logs stay on your device and are never sent anywhere.
* **Siri and Shortcuts (iOS)**: when you add a task with "Add to Didit", Apple handles the speech recognition and the App only receives the recognized task text, which it stores on your device.

### 2) Google account connection and cloud sync (optional)
Processed only if you connect a Google account in Settings.
* **What and where**:
  * Your Google account email address: kept in the app settings on your device. Even after you disconnect, it stays on the device as the "previous account" so that, when you later connect a different account, the App can decide how to protect your existing tasks. It is deleted when you uninstall the App.
  * The task sync file (`todonotification_backup.json`, containing your tasks and the random identifier of the device that last uploaded it) and a device activity record (one empty file per device whose name contains the device's random identifier and type — Android, iOS, Windows or macOS — and whose modification time serves as the last activity time): kept in a hidden app-specific folder (`appDataFolder`) in your own Google Drive.
* **Purpose**: syncing and backing up your tasks across your devices. The device activity record is used only to avoid sending real-time sync signals (see 3 below) when no other recently used device exists on the same account.
* **Access scope**: the App cannot access your Drive as a whole; it can only access the folder Didit created. The only Google permissions requested are access to that app folder (`https://www.googleapis.com/auth/drive.appdata`) and sign-in with email verification (`openid`, `email`).
* **Google API Services User Data Policy**: Didit's use and transfer of information received from Google APIs adheres to the [Google API Services User Data Policy](https://developers.google.com/terms/api-services-user-data-policy), including the Limited Use requirements. This information is used only to sync your tasks. It is not used for advertising, not sold, not transferred to third parties, and not used to develop, improve or train generalized artificial intelligence or machine learning models.
* **Sign-in credentials**: kept only on your device (Android: Google Play services; iOS: the device keychain, shared by the app and its Didit widgets so that widgets and Siri can sync without opening the app, usable only on that device and never moved by backup or device transfer; macOS: the device keychain, used only by the app; Windows: the `%LOCALAPPDATA%\Didit\GoogleAuth` folder).

### 3) Real-time sync signals
When a task changes on one device, the App sends a signal so that your other devices can fetch the latest data right away. **The signal does not contain your tasks.** Signals are sent and received only after you connect a Google account, and the App registers with the push services below only when you connect an account and removes that registration when you disconnect. If you do not connect an account, none of the processing in this section takes place.
* **Didit relay server (operated on Cloudflare Workers)**
  * Sent: a hash value derived from your account email (not the email itself) and the device's random identifier.
  * Purpose: delivering sync signals to your other devices on the same account.
  * Retention: not stored. To avoid duplicate deliveries, the hash value and request time are kept in memory for a few seconds only. Cloudflare may process network information (such as IP addresses) while handling requests.
* **Firebase Cloud Messaging (Google; Android and iOS apps)**
  * Processed: the device registration token (Firebase installation ID, created when you connect an account; the token and installation ID are deleted when you disconnect) needed for push delivery and a subscription topic made from the hash value above (created after you connect an account). On iOS, the Apple Push Notification service (APNs) device token is processed as well.
  * Device information processed with it: when registering, Firebase also receives device information such as the device model, OS version, app version, language and time zone. Google states that it uses this information to deliver push messages and to understand platform and version adoption, and that it does not link it to a user or device identifier.
  * Purpose: delivering the relay's signals to Android devices and to iOS devices (when the app is not on screen). On Android nothing is displayed. On iOS the signal arrives as a silent notification; the device syncs on its own and then fills the notification with tasks already stored on the device (the signal itself contains no tasks). If you have not allowed notifications on iOS, nothing is displayed and the App only syncs.
* **Apple Push Notification service (Apple; iOS app)**
  * Processed: the signal above (no tasks) and the APNs device token.
  * Purpose: delivering signals sent by Firebase Cloud Messaging to iOS devices.
* **Signal reception on Windows, macOS and iOS (the relay server above)**
  * The Windows and macOS apps keep a connection to the relay server while running, and the iOS app while it is on screen. When the iOS app is not on screen, it receives signals through push instead.
  * Used: only the hash value above. Neither your email nor the device identifier is used for the connection.
  * Retention: connection information exists only in the relay server's memory while the connection lasts and disappears when it closes. Cloudflare may process network information (such as IP addresses) during the connection.

### 4) App update check
When you open the app screen, the App downloads one public file — identical for every user — from the Didit website (`hoonest.net`, hosted on GitHub Pages) to check whether your version is still supported.
* **Sent**: nothing. The request contains no account, device identifier or tasks.
* **Purpose**: telling you to update if your version is no longer supported.
* **Retention**: the App stores only the minimum version value on your device. GitHub may process network information (such as IP addresses) while handling the request.

### 5) Website visits
The Didit websites (`hoonest.net`, `didit.hoonest.net`) have no sign-up, forms, analytics or ads. Hosting providers (GitHub, Cloudflare) may process visitors' network information (such as IP addresses and browser information) to deliver the pages.

---

## 2. Purposes and legal bases

We use the information above only to:
* show your tasks in persistent notifications, home screen, lock screen and desktop widgets, the menu bar, the system tray and the compact bar;
* sync and back up your tasks across your devices through Google Drive when you ask us to;
* keep your app settings;
* tell you when an outdated version is no longer supported.

If the GDPR applies to you, we rely on the following legal bases: providing the features you request (Art. 6(1)(b) GDPR) for storing and syncing your tasks and delivering sync signals, and our legitimate interests in operating the App securely and keeping it up to date (Art. 6(1)(f) GDPR) for the update check and for the network information processed by our hosting providers. We do not make decisions based solely on automated processing, including profiling.

---

## 3. Retention and deletion

| Information | Retention | How it is deleted |
| :--- | :--- | :--- |
| Tasks and settings on your device | Until you delete them or uninstall the App. Completed tasks are deleted automatically after the retention period you choose (30 days by default) | Deleted from the device when you uninstall the App or clear its data |
| Sync file and device activity records in Google Drive | Until you delete them in Drive or delete your Google account. **They remain even if you disconnect your account.** The sync file holds completed tasks from the last 30 days (up to 200) and deletion records for 30 days only, and activity records of other devices inactive for more than 30 days are removed | Delete the app data in Drive as described in section 6 |
| Google account email (device settings) | As the current account while connected, and as the previous account after you disconnect, until you uninstall the App | Deleted from the device when you uninstall the App or clear its data |
| Google sign-in credentials | Until you disconnect your account or uninstall the App | Deleted from the device when you disconnect |
| Real-time sync subscription (Firebase) | Until you disconnect your account or uninstall the App | Unsubscribed when you disconnect |
| Push device registration tokens (Firebase, APNs) | Until you disconnect your account or uninstall the App | The FCM token and Firebase installation ID are deleted when you disconnect (if this fails because you are offline, the App retries the next time you open it; the APNs registration is managed by Apple and is no longer used) |
| Signals passing through the relay server | Not stored (kept in memory only for the few seconds needed to deliver them, or while a connection lasts) | Disappear immediately after delivery or when the connection closes |

---

## 4. Sharing and service providers

Didit **does not provide, sell, rent or share your personal information or tasks with third parties**, including "selling" or "sharing" as defined under California law. The sync file is stored, at your request, in your own Google account.

To provide the App's features, we use the following service providers (processors). All transfers are encrypted (HTTPS).

| Provider | Service | Task |
| :--- | :--- | :--- |
| Google LLC | Google Drive API, Google Sign-In | Storing the sync file in your Drive app folder, account authentication |
| Google LLC | Firebase Cloud Messaging | Delivering sync signals to Android and iOS devices |
| Apple Inc. | Apple Push Notification service (APNs) | Delivering sync signals to iOS devices (no tasks) |
| Cloudflare, Inc. | Cloudflare Workers | Relaying sync signals (no tasks, not stored), hosting the Didit website |
| GitHub, Inc. | GitHub Pages | Serving the public file for the update check, hosting the website (no account or task information is sent; only network information such as IP addresses is processed to handle requests) |

---

## 5. International transfers

The providers above are located outside Korea, and the following information is transferred abroad while you use the App. Transfers happen whenever needed while you use the App, over encrypted connections (HTTPS).

| Recipient (contact) | Country | Information | When | Purpose | Retention |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Google LLC ([privacy contact](https://policies.google.com/privacy)) | United States and other countries where Google has data centers | Account email, task sync file, device activity records, push device token, subscription topic made from a hash | When you sign in, sync, register for push or receive signals after connecting a Google account | Authentication, sync and backup, signal delivery | As in section 3 |
| Apple Inc. ([privacy contact](https://www.apple.com/legal/privacy/contact/)) | United States | APNs device token, sync signals (no tasks) | When the iOS app registers for push after you connect an account, and when it receives sync signals | Delivering signals to iOS devices | Until delivered |
| Cloudflare, Inc. ([privacy contact](https://www.cloudflare.com/privacypolicy/)) | United States and the countries of the Cloudflare data centers handling the request | Hash value, random device identifier, network information (such as IP address) | When signals are sent or connections are kept after connecting an account, and when you visit the website | Relaying sync signals, serving the website | Not stored (seconds, or in memory while connected) |
| GitHub, Inc. ([privacy contact](https://docs.github.com/site-policy/privacy-policies/github-general-privacy-statement)) | United States | Network information (such as IP address) | When you open the app screen (update check) and when you visit the website | Serving the update file and the website | Not received by the Operator (subject to GitHub's policy) |

* **How to refuse and its effect**:
  * If you do not connect a Google account, no transfers to Google, Apple or Cloudflare (account email, tasks, device identifiers, push registration) take place; you can use your tasks on the device only (without sync). After connecting, you can stop at any time with [Disconnect Google account] in Settings, which also removes the push registration.
  * There is no setting to turn off the network information (such as IP addresses) processed for the update check and website visits. If you do not want this, you can stop using or uninstall the App. If you use the App offline, the update check does not happen, but you will not be told when your version is no longer supported.
* **Safeguards**: these providers state that they protect such transfers with recognized safeguards, such as the EU–U.S. Data Privacy Framework or Standard Contractual Clauses. See each provider's privacy policy linked above for details.

---

## 6. Your rights and how to exercise them

You may at any time access, correct or delete your personal information, or ask us to stop processing it. If the GDPR applies to you, you also have the rights to restrict processing, to object, and to data portability, and you may lodge a complaint with the data protection authority in your country. Because Didit's data is only on your devices and in your own Google Drive, you can do most of this yourself:
* **Access and correction**: view and edit your tasks in the task and completed lists of the App.
* **Deleting data on the device**: permanently delete tasks or uninstall the App.
* **Stopping processing (disconnecting sync)**: use [Settings] → [Disconnect Google account] at any time. Your tasks stay on the device; cloud sync and real-time sync signals stop.
* **Deleting cloud data**: in Google Drive on the web, go to [Settings] → [Manage apps], find Didit and choose **Delete hidden app data**. This deletes the sync file and device activity records stored in Drive.
* **Portability**: the sync file in your Drive app folder is a JSON file containing your tasks.
* **Revoking Google access**: revoke Didit's access at any time on the [Google Account permissions](https://myaccount.google.com/permissions) page.
* **Requests**: send any other request to the contact in section 11. We will reply within 10 days. The Operator cannot access your tasks or Drive data, so please handle that data yourself using the methods above.

---

## 7. Security measures

* All network transfers are encrypted with HTTPS (TLS).
* Google permissions are limited to the app folder and email verification; your other Drive files are never accessed.
* Google sign-in credentials are kept only in the secure storage provided by the operating system (such as the keychain) or the app's private folder, and are excluded from backups.
* Your email address itself is never sent to the Operator's server; sync signals use only a hash value.
* The Operator's servers do not store your tasks or account information.
* App error logs never contain task text, account email or credentials.

---

## 8. Cookies and similar technologies

The App does not use cookies or similar tracking technologies. The websites do not use cookies; they only store the display theme you choose (light or dark) in your browser, which is deleted when you clear site data in your browser.

---

## 9. Children

Didit is not directed to children under 14 (or under the minimum age for digital consent in your country) and does not knowingly collect their personal information.

---

## 10. Changes to this policy

If the App's data processing changes, we update this policy and its effective date before the change takes effect. Previous versions are available in the [change history](https://github.com/surprisen/didit/commits/main/privacy).

---

## 11. Privacy officer and contact

Please send questions about this policy, complaints and requests about your personal information to:

* **Privacy officer (controller)**: KiHoon Nam (남기훈), Didit operator (individual developer), Republic of Korea
* **Email**: didit@hoonest.net

---

## 12. Remedies for users in Korea

To seek remedies for infringements of personal information, users in Korea may contact:
* Personal Information Dispute Mediation Committee: 1833-6972 (www.kopico.go.kr)
* Personal Information Infringement Report Center: 118 (privacy.kisa.or.kr)
* Supreme Prosecutors' Office: 1301 (www.spo.go.kr)
* Korean National Police Agency: 182 (ecrm.police.go.kr)
