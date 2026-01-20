# Gameluck Publisher Technical Integration Guide

🌐 **Languages**
- [English](README.md)
- [简体中文](README.zh-CN.md)

---

## 1. Integration Overview

Gameluck is a leading **H5 Offerwall** product.

Publishers **do NOT need to integrate any SDK**.  
They only need to provide an entry point in their App / Game / H5 / Web product
that redirects users to the **system browser** to open the Gameluck H5 link.

**After integration:**
- All user flows and monetization logic are handled by Gameluck
- Data tracking and revenue settlement are managed by Gameluck
- Publishers only need to review reports and receive revenue settlements on schedule

---

## 2. What Publishers Need to Do

### 1. Obtain the H5 Link

After business confirmation, Gameluck will provide an **official H5 link (URL)**.

> This link is maintained and updated by Gameluck  
> No additional maintenance is required from publishers

---

### 2. Provide an Entry and Redirect to the System Browser

Publishers should add an entry point in their App / Game / H5 / Web product  
(e.g. button, banner, card).

When the user clicks the entry, it **must open the link in the system browser**.

> ❗ WebView is NOT allowed  
> ❗ Do NOT embed the page inside the app

---

### 3. Go Live and Receive Revenue

Once the entry is live, monetization starts immediately.

Publishers only need to check reports and receive revenue settlements  
according to the agreed commercial schedule.

---

## 3. Platform Redirect Examples (System Browser Only)

Replace the URL below with the official Gameluck link provided to you.

```
https://YOUR_GAMELUCK_URL
```

### Android (Kotlin)

```kotlin
val url = "https://YOUR_GAMELUCK_URL"
val intent = Intent(Intent.ACTION_VIEW, Uri.parse(url))
intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK)
startActivity(intent)
```

### Android (Java)

```java
String url = "https://YOUR_GAMELUCK_URL";
Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(url));
intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
startActivity(intent);
```

### iOS (Swift)

```swift
let urlString = "https://YOUR_GAMELUCK_URL"
if let url = URL(string: urlString) {
    UIApplication.shared.open(url, options: [:], completionHandler: nil)
}
```

### Unity (C#)

```csharp
Application.OpenURL("https://YOUR_GAMELUCK_URL");
```

### Cocos Creator (TypeScript)

```ts
cc.sys.openURL("https://YOUR_GAMELUCK_URL");
```

### Cocos2d-x (C++)

```cpp
Application::getInstance()->openURL("https://YOUR_GAMELUCK_URL");
```

---

## 4. URL Tracking Parameters & Examples (Must Read)

### 1. URL Format Example

```
https://gameluck.io/?key=YOUR_KEY&gaid={gaid}&click_id={click_id}
```

> `{gaid}` and `{click_id}` are placeholders only  
> **Do NOT include curly braces `{}` in real requests**

---

### 2. Fully Constructed Example URLs

#### Example 1: GAID + click_id (Recommended)

```
https://gameluck.io/?key=JDy9K9LVwPtP2EKj&gaid=38400000-8cf0-11bd-b23e-10b96e40000d&click_id=user_102938
```

#### Example 2: GAID Only

```
https://gameluck.io/?key=JDy9K9LVwPtP2EKj&gaid=38400000-8cf0-11bd-b23e-10b96e40000d
```

#### Example 3: Minimum Required Parameters

```
https://gameluck.io/?key=JDy9K9LVwPtP2EKj
```

---

### 3. Parameter Description

| Parameter | Required | Description |
|----------|----------|-------------|
| key | Yes | Access key assigned by Gameluck |
| gaid | Recommended | Google Advertising ID (Android only) |
| click_id | Optional | Publisher-defined unique identifier (user ID or click ID) |

---

## 5. Postback Support (Optional)

If `click_id` is provided, Gameluck can send postback callbacks  
when subsequent user events occur (e.g. **registration event**).

Publishers need to provide:
- Postback URL
- Supported event types

> The original `click_id` will be included in the postback request.

Postback is **optional** and does **not affect monetization or settlement**.

---

### Postback URL Examples

Gameluck supports both **GET** and **POST** postback formats.  
Postbacks are sent **server-to-server**.

---

#### Example 1: GET Method

**Configured postback URL:**

```
https://publisher.example.com/postback?event=register&click_id={click_id}
```

> `{click_id}` is a placeholder and will be replaced by Gameluck.

**Actual callback example:**

```
https://publisher.example.com/postback?event=register&click_id=user_102938
```

---

#### Example 2: POST Method (JSON)

**Postback URL:**

```
https://publisher.example.com/postback
```

**Request Body:**

```json
{
  "event": "register",
  "click_id": "user_102938",
  "timestamp": 1710000000
}
```

---

## 6. How to Obtain GAID (Android)

GAID is **Android-only** and optional.

### Kotlin Example

```kotlin
fun getGaid(context: Context): String? {
    return try {
        AdvertisingIdClient.getAdvertisingIdInfo(context).id
    } catch (e: Exception) {
        null
    }
}
```

### Java Example

```java
public static String getGaid(Context context) {
    try {
        return AdvertisingIdClient
            .getAdvertisingIdInfo(context)
            .getId();
    } catch (Exception e) {
        return null;
    }
}
```

> If GAID cannot be obtained, the integration still works normally  
> and monetization is not affected.
