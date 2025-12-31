# Gameluck 媒体接入说明

🌐 **语言**
- [English](README.md)
- [简体中文](README.zh-CN.md)

---

## 1. 接入概览

Gameluck 是一款领先的 **H5 积分墙（Offerwall）** 产品。

媒体方 **无需接入任何 SDK**，只需在自己的产品中提供一个入口，
将用户 **跳转到系统浏览器** 打开 Gameluck 的 H5 页面即可。

**接入后：**
- 用户流程与变现逻辑由 Gameluck 统一负责
- 数据追踪与收入结算由 Gameluck 统一完成
- 媒体方只需定期查看报表并按约定周期收款

---

## 2. 媒体需要做什么

### 1. 获取 H5 链接

在商务确认后，Gameluck 将提供一个 **官方 H5 链接（URL）**。

> 该链接由 Gameluck 维护和更新  
> 媒体方无需自行修改或维护

---

### 2. 提供入口并跳转系统浏览器

媒体方需要在 App / 游戏 / H5 / Web 产品中提供一个入口  
（如按钮、Banner、卡片等）。

当用户点击入口时，**必须使用系统浏览器打开链接**。

> ❗ 不允许使用 WebView  
> ❗ 不要将页面嵌入 App 内部

---

### 3. 上线并开始变现

入口上线后即可开始变现。

媒体方只需根据约定周期查看数据报表并接收结算收入。

---

## 3. 各平台跳转示例（系统浏览器）

请将下方 URL 替换为 Gameluck 提供的正式链接。

```
https://YOUR_GAMELUCK_URL
```

### Android（Kotlin）

```kotlin
val url = "https://YOUR_GAMELUCK_URL"
val intent = Intent(Intent.ACTION_VIEW, Uri.parse(url))
intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK)
startActivity(intent)
```

### Android（Java）

```java
String url = "https://YOUR_GAMELUCK_URL";
Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(url));
intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
startActivity(intent);
```

### iOS（Swift）

```swift
let urlString = "https://YOUR_GAMELUCK_URL"
if let url = URL(string: urlString) {
    UIApplication.shared.open(url, options: [:], completionHandler: nil)
}
```

### Unity（C#）

```csharp
Application.OpenURL("https://YOUR_GAMELUCK_URL");
```

### Cocos Creator（TypeScript）

```ts
cc.sys.openURL("https://YOUR_GAMELUCK_URL");
```

### Cocos2d-x（C++）

```cpp
Application::getInstance()->openURL("https://YOUR_GAMELUCK_URL");
```

---

## 4. 链接参数说明与示例（必读）

### 1. 链接格式示例

```
https://gameluck.io/?key=YOUR_KEY&gaid={gaid}&click_id={click_id}
```

> `{gaid}` 与 `{click_id}` 仅为占位符示例  
> **实际请求中请不要包含大括号 `{}`**

---

### 2. 拼好的完整示例链接

#### 示例 1：包含 GAID 与 click_id（推荐）

```
https://gameluck.io/?key=JDy9K9LVwPtP2EKj&gaid=38400000-8cf0-11bd-b23e-10b96e40000d&click_id=user_102938
```

#### 示例 2：仅包含 GAID

```
https://gameluck.io/?key=JDy9K9LVwPtP2EKj&gaid=38400000-8cf0-11bd-b23e-10b96e40000d
```

#### 示例 3：最小接入参数

```
https://gameluck.io/?key=JDy9K9LVwPtP2EKj
```

---

### 3. 参数说明

| 参数名 | 是否必填 | 说明 |
|------|----------|------|
| key | 是 | 由 Gameluck 分配的接入 Key |
| gaid | 推荐 | Android 用户的 GAID |
| click_id | 可选 | 媒体方自定义的唯一标识（用户 ID 或点击唯一 ID） |

---

## 5. 回调（Postback）支持（可选）

当媒体方传入 `click_id` 时，Gameluck 可在用户后续行为  
（如 **注册事件**）发生后向媒体方发起回调。

媒体方需提供：
- 回调地址（Postback URL）
- 支持的事件类型

> 回调请求中将携带原始的 `click_id`，用于事件匹配。

回调为 **可选功能**，  
是否接入 **不影响前期变现与结算**。

---

### 回调（Postback）URL 示例

Gameluck 支持 **GET** 与 **POST** 两种回调方式，  
回调请求为 **服务器对服务器（Server-to-Server）**。

#### 示例一：GET 方式

```
https://publisher.example.com/postback?event=register&click_id={click_id}
```

实际回调示例：

```
https://publisher.example.com/postback?event=register&click_id=user_102938
```

---

#### 示例二：POST 方式（JSON）

**回调地址**
```
https://publisher.example.com/postback
```

**请求体**
```json
{
  "event": "register",
  "click_id": "user_102938",
  "timestamp": 1710000000
}
```

---

## 6. 如何获取 GAID（Android）

GAID 仅适用于 **Android 平台**，为可选参数。

### Kotlin 示例

```kotlin
fun getGaid(context: Context): String? {
    return try {
        AdvertisingIdClient.getAdvertisingIdInfo(context).id
    } catch (e: Exception) {
        null
    }
}
```

### Java 示例

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

> 若无法获取 GAID，接入流程仍可正常工作，  
> 不影响用户变现与收入结算。
