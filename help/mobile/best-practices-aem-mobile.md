---
title: AEM Mobile On-demand Services最佳作法
description: 了解最佳實務和准則，協助有經驗的網站AEM開發人員建立行動應用程式範本和元件。
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# 最佳做法 {#best-practices}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

建置AEM Mobile On-demand Services應用程式與直接在Cordova（或PhoneGap）殼層中執行的應用程式不同。 開發人員應熟悉：

* 立即支援的外掛程式，以及AEM Mobile專用外掛程式。

>[!NOTE]
>
>若要深入了解外掛程式，請參閱下列資源：
>
>* [在AEM Mobile中使用Cordova外掛程式](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [使用AEM Mobile專用的Cordova外掛程式](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>


* 使用外掛程式功能的範本，應以在瀏覽器中仍可授權的方式撰寫，而不應存在外掛程式橋接器。

   * 例如，請務必等候 *deviceready* 函式，再嘗試存取外掛程式的API。

## AEM開發人員准則 {#guidelines-for-aem-developers}

下列指引將協助經驗豐富的網站AEM開發人員，協助他們建立行動應用程式範本和元件：

**建構AEM網站範本，以鼓勵重複使用和擴充**

* 與單個整體式指令碼檔案相比，首選多個元件指令碼檔案

   * 提供許多空的延伸點，例如 *customheaderlibs.html* 和 *customfooterlibs.html*，可讓開發人員變更頁面範本，同時盡可能複製最少的核心程式碼
   * 接著，您就可以透過Sling擴充和自訂範本 *sling:resourceSuperType* 機構

* 使用Sightly/HTL而非JSP作為範本語言

   * 使用此功能可促進程式碼與標籤、內建XSS保護的選件分離，且有更熟悉的語法

**針對設備效能進行優化**

* 應使用dps-article contentsync模板將特定文章指令碼和樣式表包含在文章裝載中
* 應透過dps-HTMLResources contentsync範本，將多篇文章共用的指令碼和樣式表納入共用資源中
* 請勿參考任何呈現封鎖的外部指令碼

>[!NOTE]
>
>您可以深入了解關於呈現封鎖外部指令碼的詳細資訊 [此處](https://developers.google.com/speed/docs/insights/BlockingJS).

**偏好使用應用程式專屬的用戶端JS和CSS程式庫，而非網頁專用**

* 避免jQuery Mobile等程式庫的額外負荷，以處理大量裝置和瀏覽器
* 當範本在應用程式的網頁檢視中執行時，您可以控制應用程式將要支援的平台和版本，以及了解將會有JavaScript支援。 例如，偏好Ionic（可能只是CSS）而非jQuery Mobile，偏好Onsen UI，而非Bootstrap。

>[!NOTE]
>
>若要深入了解jQuery行動裝置，請按一下 [此處](https://jquerymobile.com/browser-support/1.4/).

**偏好微程式庫，而非完整堆疊**

* 將內容放到裝置玻璃上所花的時間，會因您文章所依賴的每個程式庫而減少。 使用新的網頁檢視來轉譯每篇文章時，速度會更加緩慢，因此每個程式庫必須從頭再次初始化
* 如果您的文章未建置為SPA（單頁應用程式），則您可能不需要包含完整堆疊程式庫，如Angular
* 偏好較小的單一用途程式庫，以協助您新增頁面所需的互動功能，例如 [快速點按](https://github.com/ftlabs/fastclick) 或 [Velocity.js](https://velocityjs.org)

**將文章有效負載的大小減到最小**

* 使用盡可能小的資產，以合理的解析度有效覆蓋您要支援的最大檢視區
* 使用類似的工具 *ImageOptim* 移除任何多餘的中繼資料

## 搶先 {#getting-ahead}

若要深入了解其他兩個角色和責任，請參閱下列資源：

* [管理員](/help/mobile/aem-mobile.md)
* [作者](/help/mobile/aem-mobile-on-demand.md)
