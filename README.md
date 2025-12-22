# Gameluck Media Integration Guide

🌐 **Languages**
- [English](README.md)
- [简体中文](README.zh-CN.md)


## 1. Integration Overview

Gameluck is a leading H5 offerwall product.  
Publishers **do not need to integrate any SDK**.  
You only need to provide an entry point in your product that redirects users  
to the **system browser** to open the Gameluck H5 link.

**After integration:**
- All user flows and monetization logic are handled by Gameluck  
- Data tracking and revenue settlement are managed by Gameluck  
- Publishers only need to review and receive revenue settlements on schedule  

---

## 2. What Publishers Need to Do

### 1. Obtain the H5 Link
After business confirmation, Gameluck will provide an **official H5 link (URL)**.

> This link is maintained and updated by Gameluck. No further action is required from the publisher.

---

### 2. Provide an Entry and Redirect to the System Browser
Publishers should add an entry point in their App / Game / H5 / Web product  
(e.g. button, banner, card).

When the user clicks the entry, it **must open the link in the system browser**.

> ❗ WebView is NOT allowed.  
> ❗ Do NOT embed the page inside the app.

---

### 3. Go Live and Receive Revenue
Once the entry is live, monetization starts immediately.  
Publishers only need to check reports and receive revenue settlements  
according to the agreed schedule.

---

## 3. Platform Redirect Examples (System Browser Only)

Please replace the URL below with the official Gameluck link provided to you:

```
https://YOUR_GAMELUCK_URL
```

### Android (Kotlin, System Browser)

```kotlin
val url = "https://YOUR_GAMELUCK_URL"
val intent = Intent(Intent.ACTION_VIEW, Uri.parse(url))
intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK)
startActivity(intent)
```

### Android (Java, System Browser)

```java
String url = "https://YOUR_GAMELUCK_URL";
Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(url));
intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
startActivity(intent);
```

### iOS (Swift, Safari)

```swift
let urlString = "https://YOUR_GAMELUCK_URL"
if let url = URL(string: urlString) {
    UIApplication.shared.open(url, options: [:], completionHandler: nil)
}
```

### Unity (C#, System Browser)

```csharp
using UnityEngine;

public class OpenGameluck : MonoBehaviour
{
    public void Open()
    {
        string url = "https://YOUR_GAMELUCK_URL";
        Application.OpenURL(url);
    }
}
```

### Cocos Creator (TypeScript, System Browser)

```ts
const url = "https://YOUR_GAMELUCK_URL";
cc.sys.openURL(url);
```

### Cocos2d-x (C++, System Browser)

```cpp
#include "platform/CCApplication.h"

std::string url = "https://YOUR_GAMELUCK_URL";
Application::getInstance()->openURL(url);
```



