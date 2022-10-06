---
title: AEM Sites - GDPR整備
seo-title: AEM Sites - GDPR Readiness
description: 了解AEM Sites GDPR整備的詳細資訊。
seo-description: Learn about the details of GDPR Readiness for AEM Sites.
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
exl-id: 8c1ea483-7319-4e5c-be4c-d43a2b67d316
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---

# AEM Sites - GDPR整備{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR是以下各節中的範例，但涵蓋的詳細資訊適用於所有資料保護和隱私權法規；例如GDPR、CCPA等

歐盟資料隱私權一般資料保護規範自2018年5月起生效。

AEM Sites已準備好協助客戶履行其GDPR法規遵循義務。 本頁引導客戶完成在AEM Sites中處理GDPR請求的程式。 它說明了儲存的私人資料位置，以及如何手動或使用程式碼移除這些資料。

如需詳細資訊，請參閱 [Adobe隱私權中心的GDPR頁面](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>請參閱 [AEM GDPR整備](/help/managing/data-protection-and-privacy.md) 以取得詳細資訊。

## 作者伺服器 {#author-server}

作者伺服器上的使用者帳戶和UGC內容在 [平台GDPR檔案](/help/managing/data-protection-and-privacy.md).

## 發佈伺服器 {#publish-server}

用於驗證網站訪客的使用者帳戶，以及發佈伺服器上的UGC內容，在 [平台GDPR檔案](/help/managing/data-protection-and-privacy.md).

依預設，AEM Sites元件不會儲存訪客在發佈伺服器上輸入的表單資料。 建議將資料轉送至協力廠商系統或Adobe Campaign以進行進一步處理。

## 選擇加入/選擇退出 {#opt-in-opt-out}

AEM有 [cookie選擇退出服務](/help/sites-developing/cookie-optout.md) 可用來管理使用者的選擇加入/退出。

## Analytics提供的增強深入分析 {#enhanced-insights-by-analytics}

AEM Sites包含選用的Enhanced Insights by Analytics整合，該整合使用Adobe Analytics On-demand Service中的功能。

如需管理與Adobe Analytics相關之GDPR資料主體請求的詳細資訊，請參閱 [Adobe Analytics與GDPR](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html).

## 增強Target的個人化功能 {#enhanced-personalization-by-target}

AEM Sites包含選用的與Enhanced Personalization by Target整合，該整合使用Adobe Target隨需服務中的功能。

如需管理與Adobe Target相關之GDPR資料主體請求的詳細資訊，請參閱 [Adobe Target — 隱私權與一般資料保護規範](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html).

## ContextHub {#contexthub}

AEM提供選用的資料層，搭配 [ContextHub](/help/sites-developing/contexthub.md). 這可讓瀏覽器中的訪客專屬資料保留，以用於規則型個人化。

依預設，此訪客資料不會儲存在AEM中；AEM會將規則傳送至資料層，以在瀏覽器中做出個人化決策。

>[!NOTE]
>
>在Adobe CQ 5.6之前，ClientContext（舊版ContextHub）已將資料傳送至伺服器，但並未儲存。
>
>Adobe CQ 5.5及更舊版本現已停用，本檔案未涵蓋。

### 實作選擇加入/選擇退出 {#implementing-opt-in-opt-out}

網站擁有者必鬚根據下列准則實作選擇退出元件。

這些准則會將選擇加入設為預設。 因此，網站訪客必須明確同意，才會將任何個人資料儲存在瀏覽器（用戶端）的持續性中。

* 每次包含ContextHub元件時，都應包含選擇退出元件。
* 與網站GDPR相關的條款與條件必須顯示給網站訪客，讓他們能夠：

   * 接受
   * 拒絕
   * 改變先前的選擇

* 如果網站訪客接受網站的條款與條件，應移除ContextHub選擇退出Cookie:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* 如果網站訪客不接受網站的條款與條件，應設定ContextHub選擇退出Cookie:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* 若要檢查ContextHub是否在選擇退出模式中執行，應在瀏覽器的主控台中進行下列呼叫：

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### ContextHub的預覽持續性 {#previewing-persistence-of-contexthub}

若要預覽使用ContextHub的持續時間，使用者可以：

* 使用瀏覽器的主控台；例如：

   * 鉻黃：

      * 開啟開發人員工具>應用程式>儲存：

         * 本機儲存>（網站）> ContextHubPersistence
         * 工作階段儲存>（網站）> ContextHubPersistence
         * Cookie >（網站）> SessionPersistence
   * Firefox:

      * 開啟開發人員工具>儲存：

         * 本機儲存>（網站）> ContextHubPersistence
         * 工作階段儲存>（網站）> ContextHubPersistence
         * Cookie >（網站）> SessionPersistence
   * Safari:

      * 在菜單欄中開啟「首選項」>「高級」>「顯示開發」菜單
      * 開啟「開發>顯示JavaScript主控台」

         * 控制台>儲存>本地儲存>（網站）> ContextHubPersistence
         * 控制台>儲存>工作階段儲存>（網站）> ContextHubPersistence
         * 控制台>儲存> Cookie >（網站）> ContextHubPersistence
   * Internet Explorer:

      * 開啟開發人員工具>主控台

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie




* 在瀏覽器的主控台中使用ContextHub API:

   * ContextHub提供下列資料持續性層：

      * ContextHub.Utils.Persistence.Modes.LOCAL（預設）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      ContextHub存放區會定義將使用的持續性層，因此，若要檢視持續性的目前狀態，應檢查所有層。


例如，要查看儲存在localStorage中的資料：

若要預覽使用ContextHub的持續時間，使用者可以：

* 使用瀏覽器的主控台：

   * Chrome — 開啟開發人員工具>應用程式>儲存：

      * 本機儲存>（網站）> ContextHubPersistence
      * 工作階段儲存>（網站）> ContextHubPersistence
      * Cookie >（網站）> SessionPersistence
   * Firefox — 開啟開發人員工具>儲存：

      * 本機儲存>（網站）> ContextHubPersistence
      * 工作階段儲存>（網站）> ContextHubPersistence
      * Cookie >（網站）> SessionPersistence


* 在瀏覽器的主控台中使用ContextHub API:

   * ContextHub提供下列資料持續性層：

      * ContextHub.Utils.Persistence.Modes.LOCAL（預設）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      ContextHub存放區會定義將使用的持續性層，因此，若要檢視持續性的目前狀態，應檢查所有層。


例如，要查看儲存在localStorage中的資料：

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除ContextHub的持續性 {#clearing-persistence-of-contexthub}

若要清除ContextHub持續性：

* 要清除當前載入的儲存的持久性，請執行以下操作：

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 清除特定持久層；例如，sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* 若要清除所有ContextHub持續性層，必須為所有層呼叫適當的程式碼：

   * ContextHub.Utils.Persistence.Modes.LOCAL（預設）
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW
