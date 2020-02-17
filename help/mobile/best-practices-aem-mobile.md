---
title: 最佳實務
seo-title: 最佳實務
description: 請依照本頁瞭解最佳實務和准則，以協助想要建立行動應用程式範本和元件的資深AEM開發人員建立網站。
seo-description: 請依照本頁瞭解最佳實務和准則，以協助想要建立行動應用程式範本和元件的資深AEM開發人員建立網站。
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Best Practices {#best-practices}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

建立AEM Mobile隨選服務應用程式與建立直接在Cordova（或PhoneGap）殼層中執行的應用程式不同。 開發人員應熟悉：

* 現成可支援的外掛程式，以及AEM mobile專用的外掛程式。

>[!NOTE]
>
>若要深入瞭解外掛程式，請參閱下列資源：
>
>* [在AEM mobile中使用Cordova增效模組](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [使用AEM mobile專用的Cordova增效模組](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>



* 使用外掛程式功能的範本，應以在瀏覽器中仍可授權的方式編寫，而不需使用外掛程式橋接器。

   * 例如，請務必先等待 *deviceready函式* ，再嘗試存取外掛程式的API。

## AEM開發人員的准則 {#guidelines-for-aem-developers}

下列准則將協助想要建立行動應用程式範本和元件的資深網站AEM開發人員：

**建構AEM網站範本，以鼓勵重複使用和擴充性**

* 比單一整體式檔案更偏好多個元件指令碼檔案

   * 提供許多空的擴充點，例如 *customheaderlibs.html**和customfooterlibs.html*，讓開發人員在盡可能少複製核心程式碼的同時，變更頁面範本
   * 然後，範本可透過Sling&#39;s *sling:resourceSuperType* mechanism進行擴充和自訂

* 相較於JSP，偏好Sightly/HTL做為範本語言

   * 使用它可讓程式碼與標籤分離，提供內建XSS保護的選件，並提供更熟悉的語法

**最佳化裝置上效能**

* 文章特定指令碼和樣式表應包含在文章裝載中，使用dps-article contentsync範本
* 應透過dps-HTMLResources內容同步範本，將多個文章共用的指令碼和樣式表納入共用資源
* 不要引用任何渲染阻止的外部指令碼

>[!NOTE]
>
>您可以在這裡進一步詳細瞭解封鎖演算的外部指令 [碼](https://developers.google.com/speed/docs/insights/BlockingJS)。

**偏好應用程式專用的用戶端JS和CSS程式庫，而非網頁專用的程式庫**

* 若要避免在jQuery mobile等程式庫中產生負擔，以處理大量裝置和瀏覽器
* 當範本在應用程式的Web檢視中執行時，您可以控制應用程式將要支援的平台和版本，以及JavaScript支援將會存在的知識。 例如，相較於jQuery Mobile和Onsen UI，偏好Ion（可能只是CSS），而非Bootstrap。

>[!NOTE]
>
>若要深入瞭解jQuery Mobile，請按一下 [這裡](https://jquerymobile.com/browser-support/1.4/)。

**偏好微型程式庫而非完整堆疊**

* 將內容放在裝置玻璃上所花的時間，會因您的文章所依賴的每個資料庫而減慢。 當使用新的網頁檢視來轉換每篇文章時，會加劇此速度變慢，因此每個資料庫必須從頭開始重新初始化
* 如果您的文章未建置為SPA（單頁應用程式），您可能不需要包含完整的堆疊資料庫，例如Angular
* 偏好較小的單一用途程式庫，以協助您新增頁面所需的互動功能，例如 [Fastclick](https://github.com/ftlabs/fastclick)[或Velocity.js](https://velocityjs.org)

**將文章有效載荷的大小降到最低**

* 以合理的解析度，使用最小的資產，以有效覆蓋您所支援的最大檢視區
* 在影像上使用 *ImageOptim* 等工具，移除多餘的中繼資料

## 搶先一步 {#getting-ahead}

若要進一步瞭解其他兩個角色和責任，請參閱以下資源：

* [管理員](/help/mobile/aem-mobile.md)
* [作者](/help/mobile/aem-mobile-on-demand.md)
