---
title: 整合著陸頁面與Adobe Analytics
seo-title: 整合著陸頁面與Adobe Analytics
description: 瞭解如何將登陸頁面與Adobe Analytics整合。
seo-description: 瞭解如何將登陸頁面與Adobe Analytics整合。
uuid: 8f6672d1-497f-4ccb-b3cc-f6120fc467ba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 8ae7ccec-489b-4d20-ac56-6101402fb18a
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# 整合著陸頁面與Adobe Analytics{#integrating-landing-pages-with-adobe-analytics}

AEM已使用下列行動要求(CTA)元件，將著陸頁面解決方案與 [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) 整合：

1. 點進元件
1. 圖形連結元件

這些元件會公開某些屬性，這些屬性可透過Adobe Analytics變數（流量、轉換變數）和成功事件進行映射，以傳送資訊至Adobe Analytics。

## 必備條件 {#prerequisites}

Adobe建議您進行現有的AEM [-Adobe Analytics整合](/help/sites-administering/adobeanalytics.md) ，以瞭解此整合的運作方式。

## 可用於映射的元件 {#components-available-for-mapping}

在AEM中，此處 **的側腳中顯示的** Call to Action **components -** ClickThroughLink **and** GraphicalLink —— 可以對應至Adobe Analytics變數。

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### 將著陸頁面元件對應至Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

若要將著陸頁面元件對應至Adobe Analytics:

1. 建立Adobe Analytics設定並建立新架構後，從下拉式選單中選取適當的報表套裝。 這會導致擷取Adobe Analytics變數並在內容搜尋器中顯示。
1. 視需要將Call to Action(CTA)元件從側腳拖放至頁面中間的對應區域。

<table>
 <tbody>
  <tr>
   <td><strong>元件名稱</strong></td>
   <td><strong>公開的屬性</strong></td>
   <td><strong>屬性含義</strong></td>
  </tr>
  <tr>
   <td><strong>CTA點進連結</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i><br /> </td>
   <td>連結上的標籤或連結的文字 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i><br /> </td>
   <td>當您按一下連結時，您被帶到的目的地 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i><br /> </td>
   <td>點按事件 </td>
  </tr>
  <tr>
   <td><strong>CTA圖形連結</strong></td>
   <td><i>eventdata.clicktroughImageLabel</i><br /> </td>
   <td>CTA影像的標題 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageTarget</i><br /> </td>
   <td>當您按一下包含連結的影像時所拍攝的目標</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageAsset</i><br /> </td>
   <td>儲存庫中映像資產的路徑 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clicktroughImageClick</i><br /> </td>
   <td>點按事件</td>
  </tr>
 </tbody>
</table>

1. 從內容搜尋器將這些公開的屬性與任何Adobe Analytics變數對應。 此架構現已可供使用。
1. 您現在可以使用現有的CTA元件建立新的登陸頁面，或從側點按一下「 **Page Properties** 」(在觸控最佳化的UI中，選取 **Open Properties** ，然後按一下「 ******** Cloud Services Services」)，在現有的登陸頁面中開啟現有的著陸頁面，並設定使用著陸頁面的架構。 從下拉式清單中選取架構。

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. 使用著陸頁面設定架構後，您現在可以使用受工具化的元件，而且Adobe Analytics中會記錄任何對CTA的點按。

