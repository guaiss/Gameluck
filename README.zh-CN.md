# Gameluck 媒体接入说明

🌐 **语言**
- [English](README.md)
- [简体中文](README.zh-CN.md)

## 一、接入方式总览

Gameluck 为 H5 积分墙产品。  
媒体**无需集成任何 SDK**，仅需在产品内提供一个入口，  
将用户**跳转到系统浏览器**打开 Gameluck 提供的 H5 链接即可完成接入。

**接入后：**
- 用户行为、变现逻辑由 Gameluck 统一处理  
- 数据统计与收益结算由 Gameluck 负责  
- 媒体无需处理后续流程，仅按周期结算收益  

---

## 二、媒体需要做的事情

### 1. 获取 H5 链接
完成商务对接后，Gameluck 将提供一个**正式 H5 链接（URL）**。

> 该链接由 Gameluck 维护与更新，媒体无需关心后续变更。

---

### 2. 提供入口并跳转到系统浏览器
媒体在 App / 游戏 / H5 / Web 中提供一个入口（如按钮、Banner、卡片等），  
用户点击后**必须通过系统浏览器打开该链接**。

> ❗ 不使用 WebView，不内嵌页面。

---

### 3. 上线后等待收益结算
入口上线后即可开始产生收益，  
媒体仅需按约定周期查看数据并进行收益结算。

---

## 三、平台跳转示例（系统浏览器）

请将示例中的 URL 替换为 Gameluck 提供的正式链接：

```
https://YOUR_GAMELUCK_URL
```

### Android（Kotlin，系统浏览器）

```kotlin
val url = "https://YOUR_GAMELUCK_URL"
val intent = Intent(Intent.ACTION_VIEW, Uri.parse(url))
intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK)
startActivity(intent)
```

### Android（Java，系统浏览器）

```java
String url = "https://YOUR_GAMELUCK_URL";
Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(url));
intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
startActivity(intent);
```

### iOS（Swift，系统浏览器 Safari）

```swift
let urlString = "https://YOUR_GAMELUCK_URL"
if let url = URL(string: urlString) {
    UIApplication.shared.open(url, options: [:], completionHandler: nil)
}
```

### Unity（C#，系统浏览器）

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

### Cocos Creator（TypeScript，系统浏览器）

```ts
const url = "https://YOUR_GAMELUCK_URL";
cc.sys.openURL(url);
```

### Cocos2d-x（C++，系统浏览器）

```cpp
#include "platform/CCApplication.h"

std::string url = "https://YOUR_GAMELUCK_URL";
Application::getInstance()->openURL(url);
```


