---
title: 將登錄頁與Adobe Analytics整合
seo-title: Integrating Landing Pages with Adobe Analytics
description: 瞭解如何將登錄頁與Adobe Analytics整合。
seo-description: Learn how to integrate landing pages with Adobe Analytics.
uuid: 8f6672d1-497f-4ccb-b3cc-f6120fc467ba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 8ae7ccec-489b-4d20-ac56-6101402fb18a
exl-id: da3f7b7e-87e5-446a-9a77-4b12b850a381
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 將登錄頁與Adobe Analytics整合{#integrating-landing-pages-with-adobe-analytics}

已將登AEM錄頁解決方案與 [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) 使用以下行動要求(CTA)元件：

1. 按一下「穿透元件」(Through Component)
1. 圖形連結元件

這些元件公開了某些屬性，這些屬性可以通過Adobe Analytics變數（流量、轉換變數）和成功事件映射，以向Adobe Analytics發送資訊。

## 必備條件 {#prerequisites}

Adobe建議您 [現有AEMAdobe Analytics一體化](/help/sites-administering/adobeanalytics.md) 瞭解此整合的工作原理。

## 可用於映射的元件 {#components-available-for-mapping}

在AEM中 **行動要求** 元件 —  **按一下直通連結** 和 **圖形連結**  — 顯示在旁踢中，可以映射到Adobe Analytics變數。

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### 將登錄頁元件映射到Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

要將登錄頁元件映射到Adobe Analytics:

1. 建立Adobe Analytics配置並建立新框架後，從下拉菜單中選擇相應的報告套件。 這會導致提取Adobe Analytics變數並在內容查找器中顯示它們。
1. 根據需要將「動作調用」(CTA)元件從側腳拖放到頁面中間的映射區域。

<table>
 <tbody>
  <tr>
   <td><strong>元件名稱</strong></td>
   <td><strong>公開的屬性</strong></td>
   <td><strong>屬性的含義</strong></td>
  </tr>
  <tr>
   <td><strong>CTA按一下「通過」連結</strong></td>
   <td><i>事件data.clickthroughLinkLabel</i> <br /> </td>
   <td>連結上的標籤或連結的文本 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>事件data.clickthroughLinkTarget</i> <br /> </td>
   <td>按一下連結時要獲取的目標 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLink按一下</i> <br /> </td>
   <td>按一下事件 </td>
  </tr>
  <tr>
   <td><strong>CTA圖形連結</strong></td>
   <td><i>事件資料.clicktroughImageLabel</i> <br /> </td>
   <td>CTA影像的標題 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>事件資料.clicktroughImageTarget</i> <br /> </td>
   <td>按一下包含連結的影像時要拍攝的目標</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>事件資料.clicktroughImageAsset</i> <br /> </td>
   <td>儲存庫中映像資產的路徑 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clicktroughImage按一下</i> <br /> </td>
   <td>按一下事件</td>
  </tr>
 </tbody>
</table>

1. 將這些暴露的屬性與內容查找器中的任何Adobe Analytics變數映射。 該框架現已準備使用。
1. 現在，您可以建立新登錄頁，或使用現有CTA元件開啟現有登錄頁，然後按一下 **Cloud Services** 頁籤 **頁面屬性** 從側腳(在觸控優化用戶介面中，選擇 **開啟屬性** 按一下 **Cloud Services**)並配置框架以用於登錄頁。 從下拉清單中選擇框架。

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. 在使用登錄頁配置框架後，您現在可以使用已檢測的元件，並且CTA上的任何點擊都記錄在Adobe Analytics。
