---
title: 使用外部提供程式進行分析
seo-title: Analytics with External Providers
description: 瞭解與外部提供程式的分析。
seo-description: Learn about Analytics with External Providers.
uuid: 31a773ca-901e-45f2-be8f-951c26f9dbc5
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bab465bc-1ff4-4f21-9885-e4a875c73a8d
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# 使用外部提供程式進行分析 {#analytics-with-external-providers}

分析可為您提供有關網站使用情況的重要而有趣的資訊。

各種現成配置可用於與相應服務整合，例如：

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

您也可以配置您自己的實例 **通用分析片段** 定義新服務配置。

然後通過添加到網頁的代碼的小片段來收集資訊。 例如：

>[!CAUTION]
>
>指令碼不能包含在 `script` 標籤。

```
var _gaq = _gaq || [];
_gaq.push(['_setAccount', 'UA-XXXXX-X']);
_gaq.push(['_trackPageview']);

(function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
})();
```

這樣的片段使得能夠收集資料並生成報告。 收集的實際資料取決於提供程式和使用的實際代碼段。 示例統計資訊包括：

* 多少訪客
* 訪問的頁數
* 搜索詞
* 登錄頁

>[!CAUTION]
>
>配置Geometrixx — 戶外演示網站，以便將「頁面屬性」中提供的屬性附加到html原始碼(剛好位於 `</html>` endtag) `js` 的下界。
>
>如果你自己 `/apps` 不從預設頁面元件繼承( `/libs/foundation/components/page`)您（或您的開發人員）必須確保 `js` 包括指令碼，例如，通過 `cq/cloudserviceconfigs/components/servicescomponents`或使用類似的機制。
>
>沒有這一點，所有服務（一般、分析、目標等）都不能工作。

## 使用通用代碼段建立新服務 {#creating-a-new-service-with-a-generic-snippet}

對於基本配置：

1. 開啟 **工具** 控制台。
1. 從左窗格展開 **Cloud Services配置**。
1. 按兩下 **一般分析代碼段** 要開啟頁面：

   ![](assets/analytics_genericoverview.png)

1. 按一下+，使用對話框添加新配置；至少指定一個名稱，例如google analytics:

   ![](assets/analytics_addconfig.png)

1. 按一下 **建立**，代碼段對話框將立即開啟 — 將相應的javascript代碼段貼上到欄位中：

   ![](assets/analytics_snippet.png)

1. 按一下 **確定** 來保存。

## 在頁面上使用新服務 {#using-your-new-service-on-pages}

建立了服務配置後，您現在需要配置所需的頁才能使用它：

1. 導航到該頁。
1. 開啟 **頁面屬性** 從側腳，然後 **Cloud Services** 頁籤。
1. 按一下 **添加服務**，然後選擇所需的服務；例如 **一般分析代碼段**:

   ![](assets/analytics_selectservice.png)

1. 按一下 **確定** 來保存。
1. 您將返回 **Cloud Services** 頁籤。 的 **一般分析代碼段** 現在與消息一起列出 `Configuration reference missing`。 使用下拉清單選擇您的特定服務實例；例如google analytics:

   ![](assets/analytics_selectspecificservice.png)

1. 按一下 **確定** 來保存。

   如果查看該頁的頁源，則現在可以看到該段。

   經過適當的時間段後，您將能夠查看已收集的統計資訊。

   >[!NOTE]
   >
   >如果配置附加到具有子頁的頁面，則這些頁面也會繼承服務。
