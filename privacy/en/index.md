# LiTodo Privacy Policy

**Effective date: November 8, 2026**

[한국어](../) · English

LiTodo (the "App") is developed and operated by KiHoon Nam (남기훈), an individual developer in the Republic of Korea (the "Operator"). The Operator respects your privacy and complies with applicable laws, including the Korean Personal Information Protection Act and, where it applies to you, the EU and UK General Data Protection Regulation (GDPR), as well as the Google Play Developer Policy and the Apple App Store Review Guidelines. This policy explains how the LiTodo apps for Android, iOS (including widgets), macOS (including widgets) and Windows, and the LiTodo websites, handle your information.

This English version is a translation of the Korean original. If they differ, the Korean version prevails, except where the law of your country requires otherwise.

---

## 1. Information we process

LiTodo has no sign-up, does not collect advertising identifiers, and uses no analytics, usage tracking or ads. The Operator's servers do not store your tasks or account information.

### 1) Data stored on your device (required)
* **What**: the tasks you write, completion times, app settings (notifications, widgets, theme, etc.), and a random identifier for each device (used for sync, see 3 below).
* **Where**: your device's internal storage (Android: the app's private database; iOS and macOS: a private storage area shared only by the app and its LiTodo widgets; Windows: the `%LOCALAPPDATA%\LiTodo` folder).
* **Leaving the device**: unless you turn on cloud sync, the App does not send your tasks off your device. However, operating-system backup and transfer features that you have turned on (such as Google backup and device-to-device transfer on Android, or iCloud Backup and device transfer on iPhone) may include your tasks and settings. Your Google sign-in credentials are never included in such backups or transfers.
* **On-device backups**: so that you can bring back tasks deleted by mistake or removed by sync, the App automatically keeps copies of your tasks and deletion records in its private storage on your device. For the last 30 days it keeps one copy for each day you change your tasks plus one right before each bulk change (clearing completed tasks, syncing a deletion made on another device, an app update, etc.); after that it keeps one copy per month for up to one year and then deletes them. If the total size exceeds a set limit, the oldest copies are deleted first. However, the most recent copy of each kind of change is kept regardless of age so that it can still be restored (it is replaced when the same kind of change happens again). Backups are never sent off your device and are excluded from operating-system backup and device transfer.
* **Diagnostic records**: to help find the cause when something goes wrong, the App keeps a record of its activity (sync, sync signals, account connection, errors and similar) in its private storage on your device for 30 days (about 2 MB in total). It never records task text, account email or sign-in credentials. Diagnostic records are never sent off your device and are excluded from operating-system backup and device transfer; they leave your device only when you send them yourself by email in a problem report (see 6 below).
* **Siri and Shortcuts (iOS)**: when you add a task with "Add to LiTodo", Apple handles the speech recognition and the App only receives the recognized task text, which it stores on your device.

### 2) Google account connection and cloud sync (optional)
Processed only if you connect a Google account in Settings.
* **What and where**:
  * Your Google account email address: kept in the app settings on your device. Even after you disconnect, it stays on the device as the "previous account" so that, when you later connect a different account, the App can decide how to protect your existing tasks. It is deleted when you uninstall the App.
  * The task sync file (`todonotification_backup.json`, containing your tasks and the random identifier of the device that last uploaded it) and a device activity record (one empty file per device whose name contains the device's random identifier and type — Android, iOS, Windows or macOS — and whose modification time serves as the last activity time): kept in a hidden app-specific folder (`appDataFolder`) in your own Google Drive.
* **Purpose**: syncing and backing up your tasks across your devices. The device activity record is used only to avoid sending real-time sync signals (see 3 below) when no other recently used device exists on the same account.
* **Access scope**: the App cannot access your Drive as a whole; it can only access the folder LiTodo created. The only Google permissions requested are access to that app folder (`https://www.googleapis.com/auth/drive.appdata`) and sign-in with email verification (`openid`, `email`).
* **Google API Services User Data Policy**: LiTodo's use and transfer of information received from Google APIs adheres to the [Google API Services User Data Policy](https://developers.google.com/terms/api-services-user-data-policy), including the Limited Use requirements. This information is used only to sync your tasks. It is not used for advertising, not sold, not transferred to third parties, and not used to develop, improve or train generalized artificial intelligence or machine learning models.
* **Sign-in credentials**: kept only on your device (Android: Google Play services; iOS: the device keychain, shared by the app and its LiTodo widgets so that widgets and Siri can sync without opening the app, usable only on that device and never moved by backup or device transfer; macOS: the device keychain, used only by the app; Windows: the `%LOCALAPPDATA%\LiTodo\GoogleAuth` folder).

### 3) Real-time sync signals
When a task changes on one device, the App sends a signal so that your other devices can fetch the latest data right away. **The signal does not contain your tasks.** Signals are sent and received only after you connect a Google account, and the App registers with the push services below only when you connect an account and removes that registration when you disconnect. If you do not connect an account, none of the processing in this section takes place.
* **LiTodo relay server (operated on Cloudflare Workers)**
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
When you open the app screen, the App downloads one public file — identical for every user — from the LiTodo website (`hoonest.net`, hosted on GitHub Pages) to check whether your version is still supported.
* **Sent**: nothing. The request contains no account, device identifier or tasks.
* **Purpose**: telling you to update if your version is no longer supported.
* **Retention**: the App stores only the minimum version value on your device. GitHub may process network information (such as IP addresses) while handling the request.

### 5) Website visits
The LiTodo websites (`hoonest.net`, `litodo.hoonest.net`) have no sign-up, forms, analytics or ads. Hosting providers (GitHub, Cloudflare) may process visitors' network information (such as IP addresses and browser information) to deliver the pages.

### 6) Questions and problem reports (optional)
Processed only when you contact the Operator through [Send feedback] in the App's settings or by writing an email yourself.
* **What we receive**: your email address and what you write. If you choose [Report a problem], a diagnostic file made by the App is attached to the email. It contains the app version, device model, OS version, language and time zone, app settings, permission states (notifications, battery usage, etc.), free storage, sync state and error codes, the number of tasks and completed tasks with each item's random identifier, state and times (no task text), the random device identifier, the first part of the account hash value (to check whether your devices are connected to the same account), the kinds and last activity times of devices connected to the same account, the number and times of on-device backups, the diagnostic records described in 1 above, and crash information recorded by the App. On Android it also includes the system log entries written by the App. The diagnostic file never contains task text, the account email itself or sign-in credentials, and user names in file paths and text that looks like an email address are masked.
* **How it is sent**: the App only fills in the recipient, subject, body and attachment in your email app; you send the email yourself from that app, and you can open, remove or edit the attachment before sending. On Windows the App saves the diagnostic file on your device and shows it so that you can attach it yourself.
* **Purpose**: answering your questions, and finding and fixing the problems you report
* **Storage**: kept in the Operator's mailbox (Gmail). Email sent to `litodo@hoonest.net` is forwarded to that mailbox through Cloudflare Email Routing.

---

## 2. Purposes and legal bases

We use the information above only to:
* show your tasks in persistent notifications, home screen, lock screen and desktop widgets, the menu bar, the system tray and the compact bar;
* sync and back up your tasks across your devices through Google Drive when you ask us to;
* keep your app settings;
* tell you when an outdated version is no longer supported;
* answer your questions and find and fix the problems you report.

If the GDPR applies to you, we rely on the following legal bases: providing the features you request (Art. 6(1)(b) GDPR) for storing and syncing your tasks and delivering sync signals, and our legitimate interests in operating the App securely and keeping it up to date (Art. 6(1)(f) GDPR) for the update check, for the network information processed by our hosting providers, and for answering the questions and problem reports you send us and keeping them for one year. We do not make decisions based solely on automated processing, including profiling.

---

## 3. Retention and deletion

| Information | Retention | How it is deleted |
| :--- | :--- | :--- |
| Tasks and settings on your device | Until you delete them or uninstall the App. Completed tasks are deleted automatically after the retention period you choose (30 days by default) | Deleted from the device when you uninstall the App or clear its data |
| On-device backups | All copies from the last 30 days, then one per month for up to one year. The most recent copy of each kind of change is kept regardless of age. Tasks you permanently deleted or that were deleted automatically may remain in backups during this time | Deleted automatically by the App when the period ends; all deleted when you uninstall the App or clear its data |
| Sync file and device activity records in Google Drive | Until you delete them in Drive or delete your Google account. **They remain even if you disconnect your account.** The sync file holds completed tasks from the last 30 days (up to 200) and deletion records for 30 days only, and activity records of other devices inactive for more than 30 days are removed | Delete the app data in Drive as described in section 6 |
| Google account email (device settings) | As the current account while connected, and as the previous account after you disconnect, until you uninstall the App | Deleted from the device when you uninstall the App or clear its data |
| Google sign-in credentials | Until you disconnect your account or uninstall the App | Deleted from the device when you disconnect |
| Real-time sync subscription (Firebase) | Until you disconnect your account or uninstall the App | Unsubscribed when you disconnect |
| Push device registration tokens (Firebase, APNs) | Until you disconnect your account or uninstall the App | The FCM token and Firebase installation ID are deleted when you disconnect (if this fails because you are offline, the App retries the next time you open it; the APNs registration is managed by Apple and is no longer used) |
| Diagnostic records on your device | 30 days; if the total exceeds about 2 MB, the oldest records are deleted first | Deleted automatically by the App when the period ends; all deleted when you uninstall the App or clear its data |
| Questions and problem reports you sent (including attachments) | One year after your request has been handled, kept so that a recurring problem can be compared; deleted right away if you ask | Deleted from the Operator's mailbox |
| Signals passing through the relay server | Not stored (kept in memory only for the few seconds needed to deliver them, or while a connection lasts) | Disappear immediately after delivery or when the connection closes |

---

## 4. Sharing and service providers

LiTodo **does not provide, sell, rent or share your personal information or tasks with third parties**, including "selling" or "sharing" as defined under California law. The sync file is stored, at your request, in your own Google account.

To provide the App's features, we use the following service providers (processors). All transfers are encrypted (HTTPS).

| Provider | Service | Task |
| :--- | :--- | :--- |
| Google LLC | Google Drive API, Google Sign-In | Storing the sync file in your Drive app folder, account authentication |
| Google LLC | Firebase Cloud Messaging | Delivering sync signals to Android and iOS devices |
| Apple Inc. | Apple Push Notification service (APNs) | Delivering sync signals to iOS devices (no tasks) |
| Cloudflare, Inc. | Cloudflare Workers | Relaying sync signals (no tasks, not stored), hosting the LiTodo website |
| Google LLC | Gmail | Storing questions and problem reports sent by email |
| Cloudflare, Inc. | Cloudflare Email Routing | Forwarding email sent to `litodo@hoonest.net` to the Operator's mailbox (not stored) |
| GitHub, Inc. | GitHub Pages | Serving the public file for the update check, hosting the website (no account or task information is sent; only network information such as IP addresses is processed to handle requests) |

---

## 5. International transfers

The providers above are located outside Korea, and the following information is transferred abroad while you use the App. Transfers happen whenever needed while you use the App, over encrypted connections (HTTPS).

| Recipient (contact) | Country | Information | When | Purpose | Retention |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Google LLC ([privacy contact](https://policies.google.com/privacy)) | United States and other countries where Google has data centers | Account email, task sync file, device activity records, push device token, subscription topic made from a hash | When you sign in, sync, register for push or receive signals after connecting a Google account | Authentication, sync and backup, signal delivery | As in section 3 |
| Apple Inc. ([privacy contact](https://www.apple.com/legal/privacy/contact/)) | United States | APNs device token, sync signals (no tasks) | When the iOS app registers for push after you connect an account, and when it receives sync signals | Delivering signals to iOS devices | Until delivered |
| Cloudflare, Inc. ([privacy contact](https://www.cloudflare.com/privacypolicy/)) | United States and the countries of the Cloudflare data centers handling the request | Hash value, random device identifier, network information (such as IP address) | When signals are sent or connections are kept after connecting an account, and when you visit the website | Relaying sync signals, serving the website | Not stored (seconds, or in memory while connected) |
| Google LLC, Cloudflare, Inc. (contacts above) | United States and the countries of each provider's data centers | Email you send us (your email address, what you write, the attached diagnostic file) | When you send us an email | Forwarding (Cloudflare) and storing (Google) the email | Cloudflare: until forwarded; Google: one year after your request has been handled |
| GitHub, Inc. ([privacy contact](https://docs.github.com/site-policy/privacy-policies/github-general-privacy-statement)) | United States | Network information (such as IP address) | When you open the app screen (update check) and when you visit the website | Serving the update file and the website | Not received by the Operator (subject to GitHub's policy) |

* **How to refuse and its effect**:
  * If you do not connect a Google account, no transfers to Google, Apple or Cloudflare (account email, tasks, device identifiers, push registration) take place; you can use your tasks on the device only (without sync). After connecting, you can stop at any time with [Disconnect Google account] in Settings, which also removes the push registration.
  * Emails to the Operator are transferred only when you send them; if you do not send one, no transfer takes place.
  * There is no setting to turn off the network information (such as IP addresses) processed for the update check and website visits. If you do not want this, you can stop using or uninstall the App. If you use the App offline, the update check does not happen, but you will not be told when your version is no longer supported.
* **Safeguards**: these providers state that they protect such transfers with recognized safeguards, such as the EU–U.S. Data Privacy Framework or Standard Contractual Clauses. See each provider's privacy policy linked above for details.

---

## 6. Your rights and how to exercise them

You may at any time access, correct or delete your personal information, or ask us to stop processing it. If the GDPR applies to you, you also have the rights to restrict processing, to object, and to data portability, and you may lodge a complaint with the data protection authority in your country. Because LiTodo's data is only on your devices and in your own Google Drive, you can do most of this yourself:
* **Access and correction**: view and edit your tasks in the task and completed lists of the App.
* **Deleting data on the device**: when you permanently delete a task it disappears from your lists immediately, and from on-device backups once their retention period ends (usually up to one year; the most recent copy of each kind of change stays until it is replaced by a newer one). To delete everything, including backups, right away, uninstall the App or clear its data (on Windows, delete the `%LOCALAPPDATA%\LiTodo` folder).
* **Stopping processing (disconnecting sync)**: use [Settings] → [Disconnect Google account] at any time. Your tasks stay on the device; cloud sync and real-time sync signals stop.
* **Deleting cloud data**: in Google Drive on the web, go to [Settings] → [Manage apps], find LiTodo and choose **Delete hidden app data**. This deletes the sync file and device activity records stored in Drive.
* **Portability**: the sync file in your Drive app folder is a JSON file containing your tasks.
* **Revoking Google access**: revoke LiTodo's access at any time on the [Google Account permissions](https://myaccount.google.com/permissions) page.
* **Deleting emails you sent us**: to have a question or problem report you sent deleted, ask through the contact in section 11. We delete it right away.
* **Requests**: send any other request to the contact in section 11. We will reply within 10 days. The Operator cannot access your tasks or Drive data, so please handle that data yourself using the methods above.

---

## 7. Security measures

* All network transfers are encrypted with HTTPS (TLS).
* Google permissions are limited to the app folder and email verification; your other Drive files are never accessed.
* Google sign-in credentials are kept only in the secure storage provided by the operating system (such as the keychain) or the app's private folder, and are excluded from backups.
* Your email address itself is never sent to the Operator's server; sync signals use only a hash value.
* The Operator's servers do not store your tasks or account information.
* On-device diagnostic records and the diagnostic files for problem reports never contain task text, account email or credentials, and user names in file paths and text that looks like an email address are masked.

---

## 8. Cookies and similar technologies

The App does not use cookies or similar tracking technologies. The websites do not use cookies; they only store the display theme you choose (light or dark) in your browser, which is deleted when you clear site data in your browser.

---

## 9. Children

LiTodo is not directed to children under 14 (or under the minimum age for digital consent in your country) and does not knowingly collect their personal information.

---

## 10. Changes to this policy

If the App's data processing changes, we update this policy and its effective date before the change takes effect. Previous versions are available in the [change history](https://github.com/surprisen/litodo/commits/main/privacy).

---

## 11. Privacy officer and contact

Please send questions about this policy, complaints and requests about your personal information to:

* **Privacy officer (controller)**: KiHoon Nam (남기훈), LiTodo operator (individual developer), Republic of Korea
* **Email**: litodo@hoonest.net

---

## 12. Remedies for users in Korea

To seek remedies for infringements of personal information, users in Korea may contact:
* Personal Information Dispute Mediation Committee: 1833-6972 (www.kopico.go.kr)
* Personal Information Infringement Report Center: 118 (privacy.kisa.or.kr)
* Supreme Prosecutors' Office: 1301 (www.spo.go.kr)
* Korean National Police Agency: 182 (ecrm.police.go.kr)
