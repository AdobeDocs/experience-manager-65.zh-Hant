---
title: 將登入頁面與Adobe Analytics整合
description: 瞭解如何將登入頁面與Adobe Analytics整合。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: da3f7b7e-87e5-446a-9a77-4b12b850a381
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 1%

---

# 將登入頁面與Adobe Analytics整合{#integrating-landing-pages-with-adobe-analytics}

AEM已整合登入頁面解決方案與 [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) 使用下列行動號召(CTA)元件：

1. 點進元件
1. 圖形連結元件

這些元件會公開可透過Adobe Analytics變數（流量、轉換變數）和成功事件對應的特定屬性，以將資訊傳送至Adobe Analytics。

## 先決條件 {#prerequisites}

Adobe建議您透過 [現有的AEM-Adobe Analytics整合](/help/sites-administering/adobeanalytics.md) 以瞭解此整合的運作方式。

## 可用於對應的元件 {#components-available-for-mapping}

在AEM中 **行動號召** 元件 —  **點進連結** 和 **GraphicalLink**  — 在sidekick中在此處顯示，可以對應至Adobe Analytics變數。

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### 將登陸頁面元件對應至Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

若要將登入頁面元件對應至Adobe Analytics：

1. 建立Adobe Analytics設定和建立框架後，請從下拉式選單中選取適當的報表套裝。 這會擷取Adobe Analytics變數，並在內容尋找器中顯示它們。
1. 視需要將行動號召(CTA)元件從Sidekick拖放到頁面中間的對應區域。

<table>
 <tbody>
  <tr>
   <td><strong>元件名稱</strong></td>
   <td><strong>屬性已公開</strong></td>
   <td><strong>屬性的含義</strong></td>
  </tr>
  <tr>
   <td><strong>cta點進連結</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td>
   <td>連結上的標籤或連結的文字 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td>
   <td>按一下連結時所前往的目的地 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td>
   <td>點按事件 </td>
  </tr>
  <tr>
   <td><strong>CTA圖形連結</strong></td>
   <td><i>eventdata.clickthroughImageLabel</i> <br /> </td>
   <td>CTA影像的標題 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughImageTarget</i> <br /> </td>
   <td>按一下包含連結的影像時拍攝的目的地</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughImageAsset</i> <br /> </td>
   <td>存放庫中影像資產的路徑 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughImageClick</i> <br /> </td>
   <td>點按事件</td>
  </tr>
 </tbody>
</table>

1. 從內容尋找器將這些公開的屬性與任何Adobe Analytics變數對應。 架構現已準備就緒，可供使用。
1. 您現在可以建立登入頁面，或使用現有CTA元件開啟現有登入頁面，然後按一下 **Cloud Service** 定位於 **頁面屬性** 從sidekick (在觸控最佳化UI中，選取 **開啟屬性** 並按一下 **Cloud Service**)並設定框架以搭配登陸頁面使用。 從下拉式清單中選取架構。

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. 使用登入頁面設定框架後，您現在可以使用儀表化的元件，對CTA的任何點按都會記錄在Adobe Analytics中。
