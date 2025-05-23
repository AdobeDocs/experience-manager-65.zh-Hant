---
title: Analytics與外部提供者
description: 瞭解如何設定您自己的Generic Analytics程式碼片段例項，以定義新的服務設定。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---


# Analytics與外部提供者 {#analytics-with-external-providers}

Analytics可提供您如何使用網站的重要且有趣資訊。

各種現成的設定可用於與適當的服務整合，例如：

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

您也可以設定自己的&#x200B;**Generic Analytics程式碼片段**&#x200B;執行個體，以定義新的服務組態。

接著，系統會以新增至網頁的程式碼片段來收集資訊。 例如：

>[!CAUTION]
>
>請勿將指令碼包含在`script`標籤中。

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

這類片段可讓您收集資料並產生報表。 實際收集的資料取決於提供者和實際使用的程式碼片段。 統計資料範例包括：

* 一段時間內有多少訪客
* 造訪了多少頁面
* 使用的搜尋辭彙
* 登陸頁面

>[!CAUTION]
>
>Geometrixx-Outdoors示範網站已設定為將「頁面屬性」中提供的屬性附加至相對應`js`指令碼中的html原始程式碼（`</html>`結束標籤正上方）。
>
>如果您自己的`/apps`並非繼承自預設頁面元件( `/libs/foundation/components/page`)，您（或您的開發人員）必須確定已包含對應的`js`指令碼，例如，可包含`cq/cloudserviceconfigs/components/servicescomponents`或使用類似的機制。
>
>如果沒有此專案，任何服務（一般、Analytics、Target等）都無法運作。

## 使用一般程式碼片段建立服務 {#creating-a-new-service-with-a-generic-snippet}

對於基本設定：

1. 開啟&#x200B;**工具**&#x200B;主控台。
1. 從左窗格中，展開&#x200B;**Cloud Service設定**。
1. 連按兩下&#x200B;**Generic Analytics Snippet**&#x200B;以開啟頁面：

   ![一般Analytics程式碼片段](assets/analytics_genericoverview.png)

1. 按一下+即可使用對話方塊新增組態。 至少要指定一個名稱，例如Google Analytics：

   ![建立設定](assets/analytics_addconfig.png)

1. 按一下&#x200B;**建立**，程式碼片段對話方塊會立即開啟 — 將適當的JavaScript程式碼片段貼入欄位：

   ![正在編輯元件](assets/analytics_snippet.png)

1. 按一下&#x200B;**確定**&#x200B;以儲存。

## 在頁面上使用您的新服務 {#using-your-new-service-on-pages}

建立服務組態之後，您必須設定使用它所需的頁面：

1. 導覽至頁面。
1. 從Sidekick開啟&#x200B;**頁面屬性**，然後開啟&#x200B;**Cloud Service**&#x200B;索引標籤。
1. 按一下&#x200B;**新增服務**，然後選取所需的服務。 例如，**Generic Analytics程式碼片段**：

   ![正在新增雲端服務](assets/analytics_selectservice.png)

1. 按一下&#x200B;**確定**&#x200B;以儲存。
1. 您返回&#x200B;**Cloud Service**&#x200B;標籤。 **Generic Analytics程式碼片段**&#x200B;現在會與訊息`Configuration reference missing`一併列出。 使用下拉式清單來選取您的特定服務執行個體。 例如，google-analytics：

   ![正在新增雲端服務組態](assets/analytics_selectspecificservice.png)

1. 按一下&#x200B;**確定**&#x200B;以儲存。

   現在，如果您檢視該頁面的頁面Source，即可看到程式碼片段。

   經過一段時間後，您可以檢視收集的統計資料。

   >[!NOTE]
   >
   >如果設定附加至具有子頁面的頁面，則這些頁面也會繼承服務。
