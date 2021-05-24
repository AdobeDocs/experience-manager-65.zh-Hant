---
title: 整合登錄頁面與Adobe Analytics
seo-title: 整合登錄頁面與Adobe Analytics
description: 了解如何將登錄頁面與Adobe Analytics整合。
seo-description: 了解如何將登錄頁面與Adobe Analytics整合。
uuid: 8f6672d1-497f-4ccb-b3cc-f6120fc467ba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 8ae7ccec-489b-4d20-ac56-6101402fb18a
exl-id: da3f7b7e-87e5-446a-9a77-4b12b850a381
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# 將登錄頁面與Adobe Analytics整合{#integrating-landing-pages-with-adobe-analytics}

AEM已透過下列呼叫動作(CTA)元件，將登錄頁面解決方案與[Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst)整合：

1. 點進元件
1. 圖形連結元件

這些元件會公開某些屬性，可透過Adobe Analytics變數（流量、轉換變數）和成功事件來對應，以將資訊傳送至Adobe Analytics。

## 必備條件 {#prerequisites}

Adobe建議您進行[現有的AEM-Adobe Analytics整合](/help/sites-administering/adobeanalytics.md)，了解此整合的運作方式。

## 可用於映射{#components-available-for-mapping}的元件

在AEM中，顯示於sidekick中的&#x200B;**動作呼叫**&#x200B;元件 — **點進連結**&#x200B;和&#x200B;**GraphicalLink** — 可對應至Adobe Analytics變數。

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### 將登錄頁面元件對應至Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

若要將登錄頁面元件對應至Adobe Analytics:

1. 建立Adobe Analytics設定並建立新架構後，請從下拉式功能表中選取適當的報表套裝。 這會導致擷取Adobe Analytics變數，並在內容尋找器中顯示。
1. 視情況將動作呼叫(CTA)元件從sidekick拖放至頁面中間的對應區域。

<table>
 <tbody>
  <tr>
   <td><strong>元件名稱</strong></td>
   <td><strong>公開的屬性</strong></td>
   <td><strong>屬性的含義</strong></td>
  </tr>
  <tr>
   <td><strong>CTA點進連結</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td>
   <td>連結上的標籤或連結的文字 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td>
   <td>按一下連結時被帶往的目的地 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td>
   <td>點按事件 </td>
  </tr>
  <tr>
   <td><strong>CTA圖形連結</strong></td>
   <td><i>eventdata.clicktroughImageLabel</i> <br /> </td>
   <td>CTA影像的標題 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageTarget</i> <br /> </td>
   <td>按一下包含連結的影像時所拍攝的目的地</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageAsset</i> <br /> </td>
   <td>存放庫中影像資產的路徑 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clicktroughImageClick</i> <br /> </td>
   <td>點按事件</td>
  </tr>
 </tbody>
</table>

1. 從內容尋找器將這些公開的屬性對應至任何Adobe Analytics變數。 架構現已可供使用。
1. 您現在可以建立新的登錄頁面，或開啟具有現有CTA元件的現有登錄頁面，然後從sidekick按一下&#x200B;**Page Properties**&#x200B;中的&#x200B;**Cloud Services**&#x200B;標籤(在觸控最佳化的UI中，選取&#x200B;**開啟屬性**，然後按一下&#x200B;**Cloud Services**)，並設定框架以與登錄頁面搭配使用。 從下拉式清單中選取架構。

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. 使用登錄頁面設定架構後，您現在可以使用已檢測的元件，而CTA上的任何點按都會記錄在Adobe Analytics中。
