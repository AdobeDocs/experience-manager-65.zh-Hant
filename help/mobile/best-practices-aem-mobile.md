---
title: AEM Mobile On-demand Services最佳做法
description: 瞭解幫助希望構建移動應用模板和組AEM件的有經驗的站點開發人員的最佳實踐和指導原則。
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
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

構建AEM Mobile On-demand Services應用與直接在Cordova（或PhoneGap）外殼中運行的應用不同。 開發人員應熟悉：

* 出廠時支援的插件以及AEM Mobile特定的插件。

>[!NOTE]
>
>要詳細瞭解插件，請參閱以下資源：
>
>* [在AEM Mobile使用Cordova插件](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [使用AEM Mobile特定的啟用Cordova的插件](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>


* 使用插件功能的模板應以在瀏覽器中仍可授權的方式編寫，而不應存在插件橋。

   * 例如，確保等待 *設備就緒* 函式，然後嘗試訪問插件的API。

## 開發人員指AEM南 {#guidelines-for-aem-developers}

以下指南將幫助有經AEM驗的網站開發人員，他們希望構建移動應用模板和元件：

**結構AEM站點模板以鼓勵重用和擴展**

* 比單個單片指令碼檔案更喜歡多個元件指令碼檔案

   * 提供了多個空的擴展點，例如 *customheadlibs.html* 和 *customfootlibs.html*，它允許開發人員在盡可能少地複製核心代碼的同時更改頁面模板
   * 然後，可通過Sling擴展模板並自定義模板 *sling:resourceSuperType* 機構

* 將JSP作為模板化語言，優先使用Sitley/HTL

   * 使用此功能可鼓勵將代碼與標籤分離，提供內置於XSS保護中的功能，並具有更熟悉的語法

**優化設備上效能**

* 項目特定指令碼和樣式表應使用dps-article contentsync模板包括在項目負載中
* 多個項目共用的指令碼和樣式表應通過dps-HTMLResources contentsync模板包括在共用資源中
* 不引用任何呈現阻塞的外部指令碼

>[!NOTE]
>
>您可以詳細瞭解關於渲染阻止外部指令碼的資訊 [這裡](https://developers.google.com/speed/docs/insights/BlockingJS)。

**與特定於Web的JS和CSS庫相比，首選特定於應用的客戶端**

* 避免在jQuery Mobile等庫中產生開銷，以處理大量設備和瀏覽器
* 當模板在應用的webview中運行時，您可以控制應用將支援的平台和版本，以及JavaScript支援將會存在的知識。 例如，與jQuery Mobile和Onsen UI相比，更喜歡Ionic（可能只是CSS），而不是Bootstrap。

>[!NOTE]
>
>要瞭解有關jQuery mobile的更多詳細資訊，請按一下 [這裡](https://jquerymobile.com/browser-support/1.4/)。

**比全堆棧更喜歡微庫**

* 將內容放到設備玻璃上所花的時間會因文章所依賴的每個庫而減少。 如果使用新的webview來呈現每篇文章，則會加劇這種減速，因此必須從頭開始重新初始化每個庫
* 如果您的文章未作為SPA（單頁應用）構建，則可能不需要包括像Angular這樣的完整堆棧庫
* 選擇較小的單用途庫，以幫助添加您的頁面所需的交互性，如 [快速按一下](https://github.com/ftlabs/fastclick) 或 [Velocity.js](https://velocityjs.org)

**最小化物品有效負載的大小**

* 以合理的解析度使用盡可能小的資產，以有效覆蓋您將支援的最大視區
* 使用類似的工具 *影像選項* 刪除映像上的多餘元資料

## 前進 {#getting-ahead}

要瞭解其他兩個角色和職責的詳細資訊，請參閱以下資源：

* [管理員](/help/mobile/aem-mobile.md)
* [作者](/help/mobile/aem-mobile-on-demand.md)
