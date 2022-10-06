---
title: 複寫
seo-title: Replication
description: 了解如何在AEM中設定和監視復寫代理。
seo-description: Learn how to configure and monitor replication agents in AEM.
uuid: 6c0bc2fe-523a-401f-8d93-e5795f2e88b9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 3cae081e-93e3-4317-b307-1316283c307a
docset: aem65
feature: Configuring
exl-id: 09943de5-8d62-4354-a37f-0521a66b4c49
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '3425'
ht-degree: 4%

---

# 複寫{#replication}

復寫代理是Adobe Experience Manager(AEM)的中心，作為用於：

* [發佈（啟動）](/help/sites-authoring/publishing-pages.md#activatingcontent) 內容（從作者到發佈環境）。
* 明確排清Dispatcher快取中的內容。
* 將使用者輸入（例如，表單輸入）從發佈環境傳回製作環境（在製作環境控制之下）。

請求為 [佇列](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) 轉給適當的代理處理。

>[!NOTE]
>
>使用者資料（使用者、使用者群組和使用者設定檔）不會在製作執行個體和發佈執行個體之間複製。
>
>若為多個發佈例項，當 [使用者同步](/help/sites-administering/sync.md) 啟用。

## 從製作複製到發佈 {#replicating-from-author-to-publish}

復寫（至發佈執行個體或Dispatcher）會進行數個步驟：

* 作者要求發佈（啟動）某些內容；這可由手動請求啟動，或由已預先設定的自動觸發器啟動。
* 請求會傳遞至適當的預設復寫代理；一個環境可以有多個預設代理，這些代理將始終被選中用於此類操作。
* 復寫代理會「封裝」內容，並將其置於復寫佇列中。
* 在「網站」標籤中， [顏色狀態指示器](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) 已針對個別頁面設定。
* 內容從隊列中提取，並使用配置的協定傳輸到發佈環境；這通常是HTTP。
* 發佈環境中的servlet接收請求並發佈接收的內容；預設的servlet為 `https://localhost:4503/bin/receive`.

* 可設定多個製作和發佈環境。

![chlimage_1-21](assets/chlimage_1-21.png)

### 從發佈複製到作者 {#replicating-from-publish-to-author}

有些功能可讓使用者在發佈執行個體上輸入資料。

在某些情況下，需要一種稱為反向復寫的復寫類型，才能將此資料傳回至製作環境，從該環境將資料重新分發至其他發佈環境。 基於安全考量，從發佈到製作環境的任何流量都必須受到嚴格控制。

反向復寫會使用發佈環境中參考製作環境的代理程式。 此代理將資料放入發件箱。 此寄件匣與製作環境中的復寫接聽程式相符。 監聽程式輪詢發件箱以收集所輸入的任何資料，然後根據需要分發。 這可確保製作環境控制所有流量。

在其他情況下，例如針對Communities功能（例如論壇、部落格、留言和評論），在發佈環境中輸入的使用者產生內容(UGC)數量，在使用複製的AEM執行個體間難以有效同步。

AEM [社群](/help/communities/overview.md) 從不對UGC使用複製。 相反地，Communities的部署需要UGC的通用儲存(請參閱 [社群內容儲存](/help/communities/working-with-srp.md))。

### 復寫 — 立即可用 {#replication-out-of-the-box}

標準安裝AEM中包含的we-retail網站可用於說明復寫。

要按照此示例操作並使用所需的預設複製代理 [安裝AEM](/help/sites-deploying/deploy.md) 包含：

* 港口的製作環境 `4502`
* 連接埠上的發佈環境 `4503`

>[!NOTE]
>
>預設為啟用 :
>
>* 作者代理：預設代理（發佈）
>
>預設會有效停用(自AEM 6.1起):
>
>* 作者代理：反向復寫代理(publish_reverse)
>* 發佈時的代理程式：反向複製（發件箱）
>
>要檢查代理或隊列的狀態，請使用 **工具** 控制台。
>請參閱 [監視複製代理](#monitoring-your-replication-agents).

#### 復寫（製作至發佈） {#replication-author-to-publish}

1. 導覽至製作環境上的支援頁面。
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. 編輯頁面以新增一些文字。
1. **啟動頁面** 來發佈變更。
1. 在發佈環境中開啟支援頁面：
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. 您現在可以看到您在作者上輸入的變更。

此復寫是透過製作環境執行：

* **預設代理（發佈）**
此代理將內容複製到預設發佈實例。
這項（設定和記錄）的詳細資訊可從製作環境的「工具」主控台存取；或：

   `https://localhost:4502/etc/replication/agents.author/publish.html`。

#### 復寫代理 — 立即可用 {#replication-agents-out-of-the-box}

標準AEM安裝中提供下列代理：

* [預設代理](#replication-author-to-publish)
用於從作者複製到發佈。

* Dispatcher排清此功能用於管理Dispatcher快取。 請參閱 [使Dispatcher快取從製作環境失效](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment) 和 [從發佈執行個體使Dispatcher快取失效](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance) 以取得更多資訊。

* [反向復寫](#reverse-replication-publish-to-author)
用於從發佈複製到作者。 反向複製不用於Communities功能，如論壇、部落格和評論。 由於未啟用發件匣，因此會有效停用。 使用反向復寫需要自訂配置。

* 靜態代理這是「將節點的靜態表示儲存到檔案系統中的代理」。
例如，使用預設設定時，內容頁面和dam資產會儲存在 `/tmp`，以HTML或適當的資產格式。 請參閱 `Settings` 和 `Rules` 標籤。
這是為了當直接從應用程式伺服器請求頁面時，就可以看到內容。 這是專門的代理程式，且（可能）在大多數情況下都不需要。

## 複製代理 — 配置參數 {#replication-agents-configuration-parameters}

從「工具」控制台配置複製代理時，對話框內有四個頁簽：

### 設定 {#settings}

* **名稱**

   復寫代理的唯一名稱。

* **說明**

   此複製代理將提供的用途的說明。

* **已啟用**

   指示複製代理當前是否已啟用。

   當代理為 **已啟用** 佇列將顯示為：

   * **作用中** 處理項目時。
   * **空閒** 隊列為空時。
   * **已阻止** 項目在佇列中時，但無法處理；例如，當接收佇列停用時。

* **序列化類型**

   序列化的類型：

   * **預設**:如果要自動選擇代理，則設定。
   * **Dispatcher排清**:如果要使用代理來排清調度程式快取，請選擇此選項。

* **重試延遲**

   兩次重試之間的延遲(等待時間（毫秒），如果遇到問題。

   預設: `60000`

* **代理使用者 ID**

   根據環境，代理將使用此用戶帳戶：

   * 從製作環境收集並封裝內容
   * 在發佈環境中建立和撰寫內容

   將此欄位留空，以使用系統使用者帳戶（sling中定義為管理員使用者的帳戶）;依預設，這是 `admin`)。

   >[!CAUTION]
   >
   >針對製作環境上的代理，此帳戶 *必須* 對要複製的所有路徑具有讀取訪問權限。

   >[!CAUTION]
   >
   >若是發佈環境上的代理，此帳戶 *必須* 具有複製內容所需的建立/寫入權限。

   >[!NOTE]
   >
   >這可作為選取復寫特定內容的機制。

* **記錄層級**

   指定用於日誌消息的詳細程度。

   * `Error`:將只記錄錯誤
   * `Info`:將記錄錯誤、警告和其他資訊性消息
   * `Debug`:訊息中將會使用高層級的詳細資訊，主要用於除錯用途

   預設: `Info`

* **用於反向複寫**

   指示是否將此代理用於反向複製；從發佈至製作環境傳回使用者輸入。

* **別名更新**

   選取此選項，即可向Dispatcher啟用別名或虛名路徑失效請求。 另請參閱 [設定Dispatcher排清代理](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent).

#### 傳輸 {#transport}

* **URI**

   這會指定目標位置的接收servlet。 尤其是，您可以在此處指定目標例項的主機名稱（或別名）和內容路徑。

   例如：

   * 預設代理可複製到 `https://localhost:4503/bin/receive`
   * Dispatcher排清代理程式可復寫至 `https://localhost:8000/dispatcher/invalidate.cache`

   此處指定的協定（HTTP或HTTPS）將決定傳輸方法。

   對於Dispatcher排清代理，只有在使用基於路徑的虛擬主機條目來區分伺服器陣列時，才會使用URI屬性，您才使用此欄位來定位要使伺服器陣列失效的伺服器陣列。 例如，陣列 #1 的虛擬主機為 `www.mysite.com/path1/*`，而陣列 #2 的虛擬主機為 `www.mysite.com/path2/*`。 您可以使用 URL `/path1/invalidate.cache` 鎖定第一個陣列，並使用 `/path2/invalidate.cache` 鎖定第二個陣列。 

* **使用者**

   用於訪問目標的帳戶的用戶名。

* **密碼**

   用於訪問目標的帳戶的密碼。

* **NTLM 網域**

   NTML驗證的域。

* **NTLM 主機**

   NTML驗證的主機。

* **啟用寬鬆 SSL**

   如果您希望接受自我認證的SSL憑證，請啟用。

* **允許過期的憑證**

   如果您希望接受過期的SSL憑證，請啟用。

#### Proxy {#proxy}

只有在需要代理時才需要下列設定：

* **Proxy 主機**

   用於傳輸的代理的主機名。

* **Proxy 連接埠**

   代理的埠。

* **Proxy 使用者**

   要使用的帳戶的使用者名稱。

* **Proxy 密碼**

   要使用的帳戶的密碼。

* **Proxy NTLM 網域**

   代理NTLM域。

* **Proxy NTLM 主機**

   代理NTLM域。

#### 延伸 {#extended}

* **介面**

   在此，您可以定義要綁定到的套接字介面。

   這會設定建立連線時使用的本機位址。 若未設定，則會使用預設位址。 這對於指定要在多宿主系統或群集系統上使用的介面非常有用。

* **HTTP 方法**

   要使用的HTTP方法。

   對於Dispatcher排清代理程式，這幾乎永遠是GET，不應變更(POST會是另一個可能的值)。

* **HTTP 標頭**

   這些功能用於Dispatcher排清代理，並指定必須清除的元素。

   對於Dispatcher排清代理程式，三個標準項目不需要變更：

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

   這些參數（如適用）用於指示刷新手柄或路徑時要使用的操作。 子參數為動態：

   * `{action}` 指示複製操作

   * `{path}` 指示路徑

   它們會由與要求相關的路徑/動作取代，因此不需要「硬式編碼」：

   >[!NOTE]
   >
   >如果您已在建議的預設內容以外的內容中安裝AEM，則需要在HTTP標題中註冊內容。 例如：
   >`CQ-Handle:/<*yourContext*>{path}`

* **關閉連線**

   啟用以在每次請求後關閉連線。

* **連線逾時**

   嘗試建立連線時要套用的逾時（毫秒）。

* **通訊端逾時**

   在建立連線後等待流量時，要套用的逾時（毫秒）。

* **通訊協定版本**

   協定的版本；例如 `1.0` （針對HTTP/1.0）。

#### 觸發器 {#triggers}

以下設定用於定義自動複製的觸發器：

* **忽略預設值**

   如果勾選此選項，則會從預設復寫中排除代理；這表示如果內容作者發出復寫動作，則不會使用它。

* **於修改**

   在此，修改頁面時將自動觸發此代理的復寫。 這主要用於Dispatcher排清代理，但也用於反向復寫。

* **頁尾 (設計)**

   如果選中，則代理將在修改時自動複製標籤為要分發的任何內容。

* **已到期/已到期**

   這會在為頁面定義的同時或離線發生時觸發自動復寫（視情況啟用或停用頁面）。 這主要用於Dispatcher排清代理。

* **接收時**

   如果選中此選項，則每當收到複製事件時，代理都會鏈式複製。

* **無狀態更新**

   勾選後，代理將不會強制更新復寫狀態。

* **無版本設定**

   勾選後，代理程式不會強製版本化已啟用的頁面。

## 配置複製代理 {#configuring-your-replication-agents}

如需使用MSSL將復寫代理連結至發佈執行個體的相關資訊，請參閱 [使用Mutual SSL進行複製](/help/sites-deploying/mssl-replication.md).

### 從製作環境設定復寫代理 {#configuring-your-replication-agents-from-the-author-environment}

從製作環境的「工具」標籤中，您可以設定位於製作環境(**作者代理**)或發佈環境(**發佈時的代理**)。 下列程式說明為製作環境設定代理，但可用於兩者。

>[!NOTE]
>
>當Dispatcher處理製作或發佈執行個體的HTTP請求時，來自復寫代理的HTTP請求必須包含PATH標題。 除了下列程式外，您還必須將PATH標題新增至用戶端標題的Dispatcher清單。 (請參閱 [/clientheaders（用戶端標題）](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders).

1. 存取 **工具** 標籤。
1. 按一下 **復寫** （左窗格以開啟資料夾）。
1. 按兩下 **作者代理** （左窗格或右窗格）。
1. 按一下相應的代理名（即連結）以顯示有關該代理的詳細資訊。
1. 按一下 **編輯** 要開啟配置對話框，請執行以下操作：

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. 提供的值應足以用於預設安裝。 如果您進行變更，請按一下 **確定** 儲存(請參閱 [複製代理 — 配置參數](#replication-agents-configuration-parameters) 以取得個別參數的詳細資訊)。

>[!NOTE]
>
>AEM的標準安裝會指定 `admin` 作為預設複製代理內傳輸憑據的用戶。
>
>此帳戶應變更為具有複製所需路徑之權限的網站特定復寫使用者帳戶。

### 配置反向複製 {#configuring-reverse-replication}

反向復寫可用來將發佈執行個體上產生的使用者內容復原到製作執行個體。 這通常用於調查和註冊表單等功能。

出於安全原因，大多數網路拓撲不允許連接 *從* 「非軍事區」(向不受信任的網路（如Internet）提供外部服務的子網路)。

由於發佈環境通常位於DMZ中，若要將內容傳回製作環境，必須從製作例項啟動連線。 這是透過：

* an *outbox* 在放置內容的發佈環境中。
* 製作環境中的代理（發佈），會定期輪詢新內容的寄件匣。

>[!NOTE]
>
>針對AEM [社群](/help/communities/overview.md)，復寫不會用於發佈執行個體上使用者產生的內容。 請參閱 [社群內容儲存](/help/communities/working-with-srp.md).

要執行此操作，您需要：

**製作環境中的反向復寫代理** 這會作為作用中元件，用於從發佈環境的寄件匣收集資訊：

如果要使用反向複製，請確保已激活此代理。

![chlimage_1-23](assets/chlimage_1-23.png)

**發佈環境中的反向復寫代理（寄件匣）** 這是被動元素，因為它是「出貨箱」。 使用者輸入會放置在此處，由製作環境中的代理程式從此處收集。

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### 為多個發佈實例配置複製 {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>僅複製內容 — 不複製用戶資料（用戶、用戶組和用戶配置檔案）。
>
>若要同步多個發佈執行個體的使用者資料，請啟用 [使用者同步](/help/sites-administering/sync.md).

安裝時，已配置預設代理，以將內容複製到本地主機埠4503上運行的發佈實例。

要為其他發佈實例配置內容複製，您需要建立和配置新複製代理：

1. 開啟 **工具** 標籤。
1. 選擇 **復寫**，然後 **作者代理** 中。
1. 選擇 **新……**.
1. 設定 **標題** 和 **名稱**，然後選取 **復寫代理**.
1. 按一下 **建立** 來建立新代理。
1. 按兩下新代理項以開啟配置面板。
1. 按一下 **編輯** - **代理設定** 對話框將開啟 —  **序列化類型** 已定義為預設值，則必須維持。

   * 在 **設定** 標籤：

      * 啟動 **已啟用**.
      * 輸入 **說明**.
      * 設定 **重試延遲** to `60000`.

      * 保留 **序列化類型** as `Default`.
   * 在 **運輸** 標籤：

      * 輸入新發佈實例所需的URI;例如，
         `https://localhost:4504/bin/receive`。

      * 輸入用於複製的特定站點用戶帳戶。
      * 您可以視需要設定其他參數。


1. 按一下 **確定** 以儲存設定。

接著，您可以在製作環境中更新並發佈頁面，以測試操作。

更新會顯示在所有已依上述方式設定的發佈執行個體上。

如果您遇到任何問題，可以檢查製作例項的記錄。 您也可以根據所需的詳細程度來設定 **記錄層級** to `Debug` 使用 **代理設定** 對話框。

>[!NOTE]
>
>這可與 [代理用戶Id](#agentuserid) 選取不同內容，以複製至個別發佈環境。 針對每個發佈環境：
>
>1. 配置複製代理以複製到該發佈環境。
>1. 設定使用者帳戶；具有讀取將複製到該特定發佈環境的內容所需的訪問權限。
>1. 將使用者帳戶指派為 **代理用戶Id** 復寫代理。

>


### 設定Dispatcher排清代理 {#configuring-a-dispatcher-flush-agent}

安裝中包含預設代理。 但是，如果要定義新代理，則仍需要某些配置，這同樣適用：

1. 開啟 **工具** 標籤。
1. 按一下 **部署**.
1. 選擇 **復寫** 然後 **發佈時的代理**.
1. 按兩下 **Dispatcher排清** 項目以開啟概覽。
1. 按一下 **編輯** - **代理設定** 對話框將開啟：

   * 在 **設定** 標籤：

      * 啟動 **已啟用**.
      * 輸入 **說明**.
      * 保留 **序列化類型** as `Dispatcher Flush`，或在建立新代理時將其設定為。

      * （可選）選取 **別名更新** 為Dispatcher啟用別名或虛名路徑無效請求。
   * 在 **運輸** 標籤：

      * 輸入新發佈實例所需的URI;例如，
         `https://localhost:80/dispatcher/invalidate.cache`。

      * 輸入用於複製的特定站點用戶帳戶。
      * 您可以視需要設定其他參數。

   對於Dispatcher排清代理，只有在使用基於路徑的虛擬主機條目來區分伺服器陣列時，才會使用URI屬性，您才使用此欄位來定位要使伺服器陣列失效的伺服器陣列。 例如，陣列 #1 的虛擬主機為 `www.mysite.com/path1/*`，而陣列 #2 的虛擬主機為 `www.mysite.com/path2/*`。 您可以使用 URL `/path1/invalidate.cache` 鎖定第一個陣列，並使用 `/path2/invalidate.cache` 鎖定第二個陣列。 

   >[!NOTE]
   >
   >如果您已在建議的預設內容以外的內容中安裝AEM，則您需要設定 [HTTP標題](#extended) 在 **延伸** 標籤。

1. 按一下 **確定** 以儲存變更。
1. 返回 **工具** 標籤，您可以 **啟動** the **Dispatcher排清** 代理(**發佈時的代理**)。

此 **Dispatcher排清** 復寫代理在作者上未作用。 您可以使用對等URI來存取發佈環境中的相同頁面；例如， `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### 控制對複製代理的訪問 {#controlling-access-to-replication-agents}

可使用 `etc/replication` 節點。

>[!NOTE]
>
>設定此類權限不會影響複製內容的使用者（例如，從網站主控台或sidekick選項）。 複製框架在複製頁時不使用當前用戶的「用戶會話」訪問複製代理。

### 從CRXDE Lite配置複製代理 {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>只有 `/etc/replication` 儲存庫位置。 這是正確處理關聯ACL所必需的。 在樹的其他位置建立複製代理可能導致未授權的訪問。

可以使用CRXDE Lite配置複製代理的各種參數。

如果您導覽至 `/etc/replication` 您可以看到下列三個節點：

* `agents.author`
* `agents.publish`
* `treeactivation`

兩個 `agents` 保留有關適當環境的配置資訊，並且僅當該環境運行時才處於活動狀態。 例如， `agents.publish` 只會在發佈環境中使用。 以下螢幕擷圖顯示製作環境中的發佈代理程式，如AEM WCM所包含：

![chlimage_1-24](assets/chlimage_1-24.png)

## 監視複製代理 {#monitoring-your-replication-agents}

要監視複製代理，請執行以下操作：

1. 存取 **工具** 標籤。
1. 按一下 **復寫**.
1. 按兩下相應環境（左窗格或右窗格）的指向代理的連結；例如 **作者代理**.

   產生的視窗會顯示製作環境中所有復寫代理的概述，包括其目標和狀態。

1. 按一下相應的代理名稱（即連結）以顯示有關該代理的詳細資訊：

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   您可以在此：

   * 查看是否啟用了代理。
   * 查看任何複製的目標。
   * 查看複製隊列當前是否處於活動狀態（已啟用）。
   * 查看隊列中是否有任何項。
   * **重新整理** 或 **清除** 更新隊列條目的顯示；這可協助您查看項目進入並離開佇列。

   * **檢視記錄** 訪問複製代理的任何操作日誌。
   * **測試連線** 到目標例項。
   * **強制重試** 在任何佇列項目上（如果需要）。

   >[!CAUTION]
   >
   >請勿在發佈執行個體上對「反向復寫寄件匣」使用「測試連線」連結。
   >
   >
   >如果對發件箱隊列執行複製測試，則任何早於測試複製的項目都會隨著每次反向複製而重新處理。
   >
   >
   >如果隊列中已存在此類項，則可以使用以下XPath JCR查詢找到這些項，並應將其刪除。
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## 批次復寫 {#batch-replication}

批次復寫不會復寫個別頁面或資產，而會等待觸發兩個頁面或資產的第一個臨界值（根據時間或大小）。

然後，它將所有複製項目打包到一個包中，然後將該包作為單個檔案複製到發佈伺服器。

發佈商會解壓縮所有項目、儲存這些項目並向作者回報。

### 配置批複製 {#configuring-batch-replication}

1. 前往 `http://serveraddress:serverport/siteadmin`
1. 按下 **[!UICONTROL 工具]** 圖示
1. 從左側導覽邊欄，前往 **[!UICONTROL 復寫 — 作者上的代理]** 按兩下 **[!UICONTROL 預設代理]**.
   * 您也可以直接前往 `http://serveraddress:serverport/etc/replication/agents.author/publish.html`
1. 按下 **[!UICONTROL 編輯]** 按鈕。
1. 在下列視窗中，前往 **[!UICONTROL 批次]** 標籤：
   ![batchreplication](assets/batchreplication.png)
1. 配置代理。

### 參數 {#parameters}

* `[!UICONTROL Enable Batch Mode]`  — 啟用或禁用批複製模式
* `[!UICONTROL Max Wait Time]`  — 批處理請求開始前的等待時間上限（以秒為單位）。 預設值為2秒。
* `[!UICONTROL Trigger Size]`  — 在此大小限制時啟動批處理複製

## 其他資源 {#additional-resources}

如需疑難排解的詳細資訊，請參閱 [疑難排解復寫](/help/sites-deploying/troubleshoot-rep.md) 頁面。
