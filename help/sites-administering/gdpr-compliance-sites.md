---
title: AEM Sites - GDPR整備
description: 瞭解在AEM Sites中處理GDPR請求的程式以及如何使用它們。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 8c1ea483-7319-4e5c-be4c-d43a2b67d316
solution: Experience Manager, Experience Manager Sites
feature: Compliance
role: Admin, Developer, Leader, User
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 54%

---

# AEM Sites - GDPR整備{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>以下各節以GDPR為例，但說明的詳細資料適用於所有資料保護和隱私權法規，例如GDPR、CCPA等。

歐盟資料隱私權的一般資料保護規範於2018年5月起生效。

AEM Sites已準備好協助客戶履行GDPR法規遵循義務。 本頁將指導客戶完成在AEM Sites中處理GDPR請求的程式。 它描述了儲存私人資料的位置，以及如何以手動方式或使用程式碼移除它們。

如需進一步資訊，請參閱Adobe隱私權中心[的](https://www.adobe.com/privacy/general-data-protection-regulation.html)GDPR頁面。

>[!NOTE]
>
>如需詳細資訊，請參閱[AEM GDPR整備](/help/managing/data-protection-and-privacy.md)。

## 作者伺服器 {#author-server}

作者伺服器上的使用者帳戶和UGC內容包含在[平台GDPR檔案](/help/managing/data-protection-and-privacy.md)中。

## 發佈伺服器 {#publish-server}

[Platform GDPR檔案](/help/managing/data-protection-and-privacy.md)涵蓋了用來驗證網站訪客的使用者帳戶以及發佈伺服器上的UGC內容。

預設情況下，AEM Sites 元件不會將訪客輸入的表單資料存放在發佈伺服器上。建議將資料轉發給第三方系統或 Adobe Campaign 進行進一步處理。

## 選擇退出/選擇加入 {#opt-in-opt-out}

AEM有[Cookie選擇退出服務](/help/sites-developing/cookie-optout.md)，可用來管理使用者的選擇加入/選擇退出。

## Analytics的增強型分析 {#enhanced-insights-by-analytics}

AEM Sites包括與Analytics增強型分析的選擇性整合，後者使用Adobe Analytics隨選服務中的功能。

有關管理與Adobe Analytics相關的GDPR資料主體請求的進一步資訊，請參閱[Adobe Analytics和GDPR](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html?lang=zh-Hant)。

## 目標增強型Personalization {#enhanced-personalization-by-target}

AEM Sites包括與Enhanced Personalization by Target的選擇性整合，後者使用Adobe Target隨選服務中的功能。

有關管理與Adobe Target相關的GDPR資料主體請求的進一步資訊，請參閱[Adobe Target — 隱私權與一般資料保護規範](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en)。

## ContextHub {#contexthub}

AEM提供具有[ContextHub](/help/sites-developing/contexthub.md)的選用資料層。 這會將訪客特定的資料保存在瀏覽器中，用於規則型個人化。

預設情況下，此訪客資料不儲存在 AEM 中；AEM 將規則傳送到資料層以在瀏覽器中做出個人化決策。

>[!NOTE]
>
>在Adobe AEM (CQ) 5.6之前，ClientContext （舊版ContextHub）確實將資料傳送至伺服器，但並未儲存。
>
>Adobe AEM 6.4及舊版現已終止服務，本檔案未涵蓋該版本。 請參閱[舊版Adobe Experience Manager、CQ和CRX檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions)。

### 實作選擇加入/選擇退出 {#implementing-opt-in-opt-out}

網站擁有者需要根據以下準則實作選擇退出元件。

這些準則會將選擇加入實作為預設值。因此，網站訪客必須先明確同意，才會將任何個人資料儲存在瀏覽器（使用者端）的持續性中。

* 每次包含 ContextHub 元件時都應包含選擇退出元件。
* 與網站的GDPR相關的條款與條件必須顯示給網站訪客，允許他們：

   * 接受
   * 拒絕
   * 變更他們之前的選擇

* 如果網站訪客接受網站的條款與條件，則應移除 ContextHub 選擇退出 cookie：

  ```java
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  ```

* 如果網站訪客不接受網站的條款與條件，則應設定 ContextHub 選擇退出 cookie：

  ```java
  ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
  ```

* 要檢查 ContextHub 是否以選擇退出模式執行，應在瀏覽器的主控台中進行以下呼叫：

  ```java
  var isOptedOut = ContextHub.isOptedOut(true) === true;
  // if isOptedOut is true, ContextHub is running in opt-out mode
  ```

### 預覽 ContextHub 的持續性 {#previewing-persistence-of-contexthub}

要預覽使用 ContextHub 的持續性，使用者可以：

* 使用瀏覽器的主控台；例如：

   * Chrome：

      * 開啟「開發人員工具」>「應用程式」>「儲存」：

         * 「本機儲存」> (網站) > ContextHubPersistence
         * 「工作階段儲存」> (網站) > ContextHubPersistence
         * 「Cookie」> (網站) > SessionPersistence

   * Firefox：

      * 開啟「開發人員工具」>「儲存」：

         * 「本機儲存」> (網站) > ContextHubPersistence
         * 「工作階段儲存」> (網站) > ContextHubPersistence
         * 「Cookie」> (網站) > SessionPersistence

   * Safari：

      * 開啟「偏好設定」>「進階」> 在選單列中顯示「開發」選單
      * 開啟「開發」>「顯示 JavaScript 主控台」

         * 「主控台」>「儲存」>「本機儲存」> (網站) > ContextHubPersistence
         * 「主控台」>「儲存」>「工作階段儲存」> (網站) > ContextHubPersistence
         * 「主控台」>「儲存」>「Cookie」> (網站) > ContextHubPersistence

   * Internet Explorer：

      * 開啟「開發人員工具」>「主控台」

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie

* 在瀏覽器的主控台中使用 ContextHub API：

   * ContextHub 提供以下資料持續層：

      * ContextHub.Utils.Persistence.Modes.LOCAL （預設）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

     ContextHub 存放區會定義要使用哪個持續層，因此要檢視持續性的目前狀態，應檢查所有層。

例如，檢視儲存在 localStorage 中的資料：

要預覽使用 ContextHub 的持續性，使用者可以：

* 使用瀏覽器的主控台：

   * Chrome - 開啟「開發人員工具」>「應用程式」>「儲存」：

      * 「本機儲存」> (網站) > ContextHubPersistence
      * 「工作階段儲存」> (網站) > ContextHubPersistence
      * 「Cookie」> (網站) > SessionPersistence

   * Firefox - 開啟「開發人員工具」>「儲存」：

      * 「本機儲存」> (網站) > ContextHubPersistence
      * 「工作階段儲存」> (網站) > ContextHubPersistence
      * 「Cookie」> (網站) > SessionPersistence

* 在瀏覽器的主控台中使用 ContextHub API：

   * ContextHub 提供以下資料持續層：

      * ContextHub.Utils.Persistence.Modes.LOCAL （預設）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

     ContextHub 存放區會定義要使用哪個持續層，因此要檢視持續性的目前狀態，應檢查所有層。

例如，檢視儲存在 localStorage 中的資料：

```java
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除 ContextHub 的持續性 {#clearing-persistence-of-contexthub}

要清除 ContextHub 的持續性：

* 要清除目前載入之存放區的持續性：

  ```java
  // to be able to fully access persistence layer, Opt-Out must be turned off
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  
  // following call asks all currently loaded stores to clear their data
  ContextHub.cleanAllStores();
  
  // following call asks all currently loaded stores to set back default values (provided in their configs)
  ContextHub.resetAllStores();
  ```

* 要清除特定的持續層；例如，sessionStorage：

  ```java
  var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
  storage.setItem('/store', null);
  storage.setItem('/_', null);
  
  // to confirm that nothing is stored:
  console.log(storage.getTree());
  ```

* 要清除所有 ContextHub 持續層，必須為所有層呼叫適當的程式碼：

   * ContextHub.Utils.Persistence.Modes.LOCAL （預設）
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW
