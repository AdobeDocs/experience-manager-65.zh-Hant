---
title: AEM Sites - GDPR整備
seo-title: AEM Sites - GDPR Readiness
description: 了解AEM Sites GDPR整備的詳細資訊。
seo-description: Learn about the details of GDPR Readiness for AEM Sites.
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
exl-id: 8c1ea483-7319-4e5c-be4c-d43a2b67d316
source-git-commit: d8ae63edd71c7d27fe93d24b30fb00a29332658d
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 54%

---

# AEM Sites - GDPR整備{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR是以下各節中的範例，但涵蓋的詳細資訊適用於所有資料保護和隱私權法規；例如GDPR、CCPA等

歐盟資料隱私權一般資料保護規範自2018年5月起生效。

AEM Sites已準備好協助客戶履行其GDPR法規遵循義務。 本頁引導客戶完成在AEM Sites中處理GDPR請求的程式。 它描述了儲存私人資料的位置，以及如何以手動方式或使用程式碼移除它們。

如需詳細資訊，請參閱 [Adobe隱私權中心的GDPR頁面](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>請參閱 [AEM GDPR整備](/help/managing/data-protection-and-privacy.md) 以取得詳細資訊。

## 作者伺服器 {#author-server}

作者伺服器上的使用者帳戶和UGC內容在 [平台GDPR檔案](/help/managing/data-protection-and-privacy.md).

## 發佈伺服器 {#publish-server}

用於驗證網站訪客的使用者帳戶，以及發佈伺服器上的UGC內容，在 [平台GDPR檔案](/help/managing/data-protection-and-privacy.md).

預設情況下，AEM Sites 元件不會將訪客輸入的表單資料存放在發佈伺服器上。 建議將資料轉發給第三方系統或 Adobe Campaign 進行進一步處理。

## 選擇退出/選擇加入 {#opt-in-opt-out}

AEM有 [cookie選擇退出服務](/help/sites-developing/cookie-optout.md) 可用來管理使用者的選擇加入/退出。

## Analytics提供的增強深入分析 {#enhanced-insights-by-analytics}

AEM Sites包含選用的Enhanced Insights by Analytics整合，該整合使用Adobe Analytics On-demand Service中的功能。

如需管理與Adobe Analytics相關之GDPR資料主體請求的詳細資訊，請參閱 [Adobe Analytics與GDPR](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html).

## 增強Target的個人化功能 {#enhanced-personalization-by-target}

AEM Sites包含選用的與Enhanced Personalization by Target整合，該整合使用Adobe Target隨需服務中的功能。

如需管理與Adobe Target相關之GDPR資料主體請求的詳細資訊，請參閱 [Adobe Target — 隱私權與一般資料保護規範](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en).

## ContextHub {#contexthub}

AEM提供選用的資料層，搭配 [ContextHub](/help/sites-developing/contexthub.md). 這會將訪客特定的資料保存在瀏覽器中，用於規則型個人化。

預設情況下，此訪客資料不儲存在 AEM 中；AEM 將規則傳送到資料層以在瀏覽器中做出個人化決策。

>[!NOTE]
>
>在Adobe CQ 5.6之前，ClientContext（舊版ContextHub）已將資料傳送至伺服器，但並未儲存。
>
>Adobe CQ 5.5及更舊版本現已停用，本檔案未涵蓋。

### 實施選擇加入/選擇退出 {#implementing-opt-in-opt-out}

網站擁有者需要根據以下準則實施選擇退出元件。

這些準則會將選擇加入實施為預設值。因此，網站訪客必須明確同意，才會將任何個人資料儲存在瀏覽器（用戶端）的持續性中。

* 每次包含 ContextHub 元件時都應包含選擇退出元件。
* 與網站GDPR相關的條款與條件必須顯示給網站訪客，讓他們能夠：

   * 接受
   * 拒絕
   * 變更他們之前的選擇

* 如果網站訪客接受網站的條款與條件，則應移除 ContextHub 選擇退出 cookie：

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* 如果網站訪客不接受網站的條款與條件，則應設定 ContextHub 選擇退出 cookie：

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* 要檢查 ContextHub 是否以選擇退出模式執行，應在瀏覽器的主控台中進行以下呼叫：

   ```
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

      * ContextHub.Utils.Persistence.Modes.LOCAL（預設）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      ContextHub 存放區會定義將使用哪個持續層，因此要檢視持續性的目前狀態，應檢查所有層。


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

      * ContextHub.Utils.Persistence.Modes.LOCAL（預設）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      ContextHub 存放區會定義將使用哪個持續層，因此要檢視持續性的目前狀態，應檢查所有層。


例如，檢視儲存在 localStorage 中的資料：

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除 ContextHub 的持續性 {#clearing-persistence-of-contexthub}

要清除 ContextHub 的持續性：

* 要清除目前載入之存放區的持續性：

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 要清除特定的持續層；例如，sessionStorage：

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* 要清除所有 ContextHub 持續層，必須為所有層呼叫適當的程式碼：

   * ContextHub.Utils.Persistence.Modes.LOCAL（預設）
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW
