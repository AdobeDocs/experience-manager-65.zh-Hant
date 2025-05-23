---
title: AEM Mobile On-demand Services的最佳作法
description: Adobe Experience Manager瞭解最佳實務和指導方針，協助有能力的網站開發人員(AEM)建立行動應用程式範本和元件。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# 最佳做法 {#best-practices}

{{ue-over-mobile}}

建置AEM Mobile On-demand Services應用程式與直接在Cordova （或PhoneGap）殼層中建置應用程式不同。 開發人員應該熟悉：

* 現成支援的外掛程式和Adobe Experience Manager (AEM)行動專用的外掛程式。

>[!NOTE]
>
>若要深入瞭解外掛程式，請參閱下列資源：
>
>* [在AEM Mobile中使用Cordova外掛程式](https://helpx.adobe.com/tw/digital-publishing-solution/help/cordova-api.html)
>* [使用AEM Mobile特定的Cordova啟用外掛程式](https://helpx.adobe.com/tw/digital-publishing-solution/help/app-runtime-api.html)
>

* 使用外掛程式功能的範本應以可在瀏覽器中編寫的方式撰寫，而不使用外掛程式橋接器。

   * 例如，在嘗試存取外掛程式的API之前，請務必等待&#x200B;*deviceready*&#x200B;函式。

## AEM開發人員指南 {#guidelines-for-aem-developers}

下列指引可協助有能力的網站開發AEM人員，協助他們建立行動應用程式範本和元件：

**建構AEM網站範本以鼓勵重複使用和擴充性**

* 偏好使用多個元件指令碼檔案，而非單一整體式指令碼檔案

   * 提供了數個空白的擴充點，例如&#x200B;*customheaderlibs.html*&#x200B;和&#x200B;*customfooterlibs.html*，讓開發人員可以變更頁面範本，同時儘可能複製較少的核心程式碼
   * 然後可以透過Sling的&#x200B;*sling：resourceSuperType*&#x200B;機制擴充和自訂範本

* 在範本化語言上，偏好使用Sightly/HTL而非JSP

   * 使用此項可鼓勵將程式碼與標籤分開、提供內建的XSS保護，且語法較為熟悉

**裝置上效能最佳化**

* 文章特定的指令碼和樣式表應使用dps-article contentsync範本包含在文章裝載中
* 共用資源應透過dps-HTMLResources contentsync範本，包含由多篇文章共用的指令碼和樣式表
* 請勿參考任何會封鎖轉譯器的外部指令碼

>[!NOTE]
>
>您可以在[此處](https://developers.google.com/speed/docs/insights/BlockingJS)進一步了解轉譯器封鎖外部指令碼。

**偏好應用程式特定使用者端JS和CSS程式庫而非Web特定資料庫**

* 為了避免jQuery Mobile等程式庫有額外負荷，而需要處理廣泛的裝置和瀏覽器
* 在應用程式的Webview中執行範本時，您可以控制應用程式將支援的平台和版本，並須具備JavaScript支援的知識。 例如，與jQuery Mobile和Onsen UI相比，偏好Ionic （只是CSS）而非Bootstrap。

>[!NOTE]
>
>若要深入瞭解jQuery行動裝置，請按一下[這裡](https://jquerymobile.com/browser-support/1.4/)。

**較完整棧疊偏好micro libraries**

* 文章所依賴的每個程式庫都會將您的內容放到裝置玻璃上的時間變慢。 當使用新的Webview來呈現每篇文章時，這種速度放緩會加劇，因此必須從頭開始再次初始化每個程式庫
* 如果您的文章不是以SPA （單頁應用程式）建置，則可能不需要包含Angular之類的完整棧疊程式庫
* 偏好有助於新增頁面所需互動性的小型單一用途資料庫，例如[Fastclick](https://github.com/ftlabs/fastclick)或[Velocity.js](https://velocityjs.org)

**將文章承載的大小最小化**

* 以合理的解析度，使用可能有效涵蓋您支援的最大檢視區的最小資產
* 在影像上使用&#x200B;*ImageOptim*&#x200B;之類的工具，以便移除任何多餘的中繼資料

## 快速入門 {#getting-ahead}

若要進一步瞭解其他兩個角色和職責，請參閱下列資源：

* [管理員](/help/mobile/aem-mobile.md)
* [作者](/help/mobile/aem-mobile-on-demand.md)
