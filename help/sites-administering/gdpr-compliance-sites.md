---
title: AEM Sites - GDPR就緒性
seo-title: AEM Sites - GDPR就緒性
description: 瞭解AEM Sites的GDPR準備詳細資訊。
seo-description: 瞭解AEM Sites的GDPR準備詳細資訊。
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# AEM Sites - GDPR就緒性{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR在以下幾節中是以範例形式使用，但涵蓋的詳細資訊適用於所有資料保護和隱私權法規；例如GDPR、CCPA等。

歐盟的資料隱私權通用資料保護條例自2018年5月起生效。

AEM Sites已準備好協助客戶履行其GDPR合規性義務。 本頁面會引導客戶完成在AEM Sites中處理GDPR要求的程式。 它說明儲存的私人資料位置，以及如何手動或使用程式碼移除這些資料。

如需詳細資訊，請 [參閱Adobe隱私權中心的GDPR頁面](https://www.adobe.com/privacy/general-data-protection-regulation.html)。

>[!NOTE]
>
>如需詳 [細資訊，請參閱AEM GDPR準備](/help/managing/data-protection-and-privacy.md) 。

## 作者伺服器 {#author-server}

作者伺服器上的使用者帳戶和UGC內容皆包含在 [Platform GDPR檔案中](/help/managing/data-protection-and-privacy.md)。

## 發佈伺服器 {#publish-server}

用於驗證網站訪客的使用者帳戶，以及發佈伺服器上的UGC內容，均在 [Platform GDPR檔案中涵蓋](/help/managing/data-protection-and-privacy.md)。

依預設，AEM Sites元件不會儲存訪客在發佈伺服器上輸入的表單資料。 建議將資料轉送至協力廠商系統或Adobe Campaign以進一步處理。

## 選擇加入／選擇退出 {#opt-in-opt-out}

AEM有 [Cookie選擇退出服務](/help/sites-developing/cookie-optout.md) ，可用來管理使用者的選擇加入／選擇退出。

## Analytics的增強見解 {#enhanced-insights-by-analytics}

AEM Sites包含Analytics的「增強前瞻分析」(Enhanced Insights by Analytics)的選購整合，此功能使用Adobe Analytics隨選服務中的功能。

如需有關管理與Adobe Analytics相關的GDPR資料主體要求的詳細資訊，請參 [閱Adobe Analytics和GDPR](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/)。

## 依Target強化個人化 {#enhanced-personalization-by-target}

AEM Sites包含與Enhanced Personalization by Target的選購整合，此整合使用Adobe Target隨選服務中的功能。

如需有關管理與Adobe target相關之GDPR資料主體要求的詳細資訊，請參閱 [Adobe Target —— 隱私與一般資料保護規則](https://marketing.adobe.com/resources/help/en_US/target/target/privacy-and-general-data-protection-regulation.html)。

## ContextHub {#contexthub}

AEM提供包含 [ContextHub的選用資料層](/help/sites-developing/contexthub.md)。 如此可保留瀏覽器中特定訪客的資料，以便用於規則型個人化。

依預設，此訪客資料不會儲存在AEM中；AEM會傳送規則至資料層，以便在瀏覽器中做個人化決策。

>[!NOTE]
>
>在Adobe CQ 5.6之前，ClientContext（舊版ContextHub）確實會將資料傳送至伺服器，但並未儲存。
>
>Adobe CQ 5.5及更早版本現已開放使用，本檔案不涵蓋此類軟體。

### 實作選擇加入／選擇退出 {#implementing-opt-in-opt-out}

網站擁有者必鬚根據下列准則建置退出元件。

這些准則會以預設方式實作選擇加入。 因此，網站訪客必須明確同意，才能將任何個人資料儲存在瀏覽器（用戶端）的永續性中。

* 每次包含ContextHub元件時，都應包含退出元件。
* 與網站GDPR相關的條款與條件必須顯示給網站訪客，讓他們能夠：

   * 接受
   * 拒絕
   * 變更先前的選擇

* 如果網站訪客接受網站的條款與條件，ContextHub選擇退出Cookie應該移除：

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* 如果網站訪客不接受網站的條款與條件，應設定ContextHub退出Cookie:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* 若要檢查ContextHub是否在選擇退出模式下執行，應在瀏覽器的主控台中進行下列呼叫：

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### 預覽ContextHub的永續性 {#previewing-persistence-of-contexthub}

若要預覽使用ContextHub的永久性，使用者可以：

* 使用瀏覽器的主控台；例如：

   * Chrome:

      * 開啟「開發人員工具>應用程式>儲存空間：

         * 本機儲存>（網站）> ContextHubPersistence
         * 作業儲存>（網站）> ContextHubPersistence
         * Cookie >（網站）> SessionPersistence
   * Firefox:

      * 開啟「開發人員工具>儲存空間」:

         * 本機儲存>（網站）> ContextHubPersistence
         * 作業儲存>（網站）> ContextHubPersistence
         * Cookie >（網站）> SessionPersistence
   * Safari:

      * 在功能表列中開啟「偏好設定>進階>顯示開發功能表」
      * 開啟「開發>顯示JavaScript主控台」

         * 控制台>儲存>本機儲存>（網站）> ContextHubPersistence
         * 控制台>儲存>作業儲存>（網站）> ContextHubPersistence
         * 控制台>儲存> Cookie >（網站）> ContextHubPersistence
   * Internet Explorer:

      * 開啟「開發人員工具>主控台」

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie




* 使用瀏覽器主控台中的ContextHub API:

   * ContextHub提供下列資料永續性層：

      * ContextHub.Utils.Persistence.Modes.LOCAL（預設）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW
      ContextHub儲存器定義將使用哪個持久性層，因此查看持久性的當前狀態，應檢查所有層。


例如，要查看儲存在localStorage中的資料：

若要預覽使用ContextHub的永久性，使用者可以：

* 使用瀏覽器的控制台：

   * Chrome —— 開啟「開發人員工具>應用程式>儲存空間」:

      * 本機儲存>（網站）> ContextHubPersistence
      * 作業儲存>（網站）> ContextHubPersistence
      * Cookie >（網站）> SessionPersistence
   * Firefox —— 開啟「開發人員工具>儲存空間」:

      * 本機儲存>（網站）> ContextHubPersistence
      * 作業儲存>（網站）> ContextHubPersistence
      * Cookie >（網站）> SessionPersistence


* 使用瀏覽器主控台中的ContextHub API:

   * ContextHub提供下列資料永續性層：

      * ContextHub.Utils.Persistence.Modes.LOCAL（預設）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW
      ContextHub儲存器定義將使用哪個持久性層，因此查看持久性的當前狀態，應檢查所有層。


例如，要查看儲存在localStorage中的資料：

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除ContextHub的永續性 {#clearing-persistence-of-contexthub}

要清除ContextHub持久性，請執行以下操作：

* 要清除當前載入的儲存的持久性，請執行以下操作：

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 清除特定的持久層；例如，sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* 要清除所有ContextHub持久層，必須對所有層調用適當的代碼：

   * ContextHub.Utils.Persistence.Modes.LOCAL（預設）
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW

