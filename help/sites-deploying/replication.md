---
title: 複製
description: 瞭解如何在Adobe Experience Manager中設定和監控復寫代理。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
docset: aem65
feature: Configuring
exl-id: 09943de5-8d62-4354-a37f-0521a66b4c49
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3363'
ht-degree: 2%

---

# 複製{#replication}

復寫代理是Adobe Experience Manager (AEM)的核心，因為此機制可用於：

* [發佈（啟動）](/help/sites-authoring/publishing-pages.md#activatingcontent) 內容從作者環境移至發佈環境。
* 明確地從Dispatcher快取排清內容。
* 將使用者輸入（例如表單輸入）從發佈環境傳回至作者環境（在作者環境的控制下）。

請求為 [已排入佇列](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) 至適當的代理程式以進行處理。

>[!NOTE]
>
>使用者資料（使用者、使用者群組和使用者設定檔）不會在製作和發佈執行個體之間復寫。
>
>對於多個Publish執行個體，使用者資料是在以下情況下發佈： [使用者同步](/help/sites-administering/sync.md) 已啟用。

## 從作者復寫至發佈 {#replicating-from-author-to-publish}

復寫至Publish執行個體或Dispatcher需要幾個步驟：

* 作者要求發佈（啟動）特定內容；這可以由手動要求或預先設定的自動觸發程式啟動。
* 此請求會傳遞至適當的預設復寫代理程式；一個環境可以有多個預設代理程式，這些代理程式一律會選取用於此類動作。
* 復寫代理程式會「封裝」內容，並將其置於復寫佇列中。
* 在網站標籤中 [彩色狀態指示器](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) 會針對個別頁面設定。
* 內容會從佇列中提取，並使用設定的通訊協定傳輸至發佈環境；這通常是HTTP。
* 發佈環境中的servlet會接收請求並發佈收到的內容；預設servlet為 `https://localhost:4503/bin/receive`.

* 可以設定多個作者和發佈環境。

![chlimage_1-21](assets/chlimage_1-21.png)

### 從發佈復寫至作者 {#replicating-from-publish-to-author}

部分功能可讓使用者在發佈執行個體上輸入資料。

有時候，需要有一種稱為反向復寫的復寫型別，將此資料傳回至製作環境，再從此處重新分配至其他發佈環境。 基於安全性考量，從發佈到製作環境的任何流量都必須受到嚴格控制。

反向復寫會在參照製作環境的發佈環境中使用代理程式。 此代理程式會將資料放入寄件匣。 此寄件匣與製作環境中的復寫接聽程式相符。 監聽器會輪詢寄件匣，以收集輸入的任何資料，然後視需要加以散發。 這可確保作者環境可控制所有流量。

在其他情況下，例如對於Communities功能（例如論壇、部落格、評論和評論），在發佈環境中輸入的使用者產生內容(UGC)量，很難使用復寫在AEM執行個體之間有效同步。

AEM [Communities](/help/communities/overview.md) 絕不使用針對UGC的復寫。 因此，社群的部署需要UGC的共同存放區(請參閱 [社群內容儲存](/help/communities/working-with-srp.md))。

### 復寫 — 立即可用 {#replication-out-of-the-box}

AEM標準安裝中包含的We-Retail網站可用於說明復寫。

若要遵循此範例，並使用預設的復寫代理， [安裝AEM](/help/sites-deploying/deploy.md) 替換為：

* 連線埠上的作者環境 `4502`
* 連線埠上的發佈環境 `4503`

>[!NOTE]
>
>預設為啟用：
>
>* 作者上的代理程式：預設代理程式（發佈）
>
>預設有效停用(自AEM 6.1起) ：
>
>* 製作代理程式：反向復寫代理程式(publish_reverse)
>* 發佈代理程式：反向復寫（寄件匣）
>
>若要檢查代理程式或佇列的狀態，請使用 **工具** 主控台。
>另請參閱 [監視復寫代理程式](#monitoring-your-replication-agents).

#### 復寫（作者至發佈） {#replication-author-to-publish}

1. 導覽至作者環境上的支援頁面。
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. 編輯頁面，以便新增一些文字。
1. **啟動頁面** 以便發佈變更。
1. 在發佈環境中開啟支援頁面：
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. 您現在可以看到您在Author上輸入的變更。

系統會從製作環境執行下列動作來執行此復寫：

* **預設代理程式（發佈）**
此代理程式會將內容復寫至預設的發佈執行個體。
您可以從製作環境的「工具」主控台存取此專案的詳細資訊（設定和記錄）；或：
  `https://localhost:4502/etc/replication/agents.author/publish.html`。

#### 復寫代理程式 — 立即可用 {#replication-agents-out-of-the-box}

標準AEM安裝提供下列代理程式：

* [預設代理程式](#replication-author-to-publish)
用於從Author復寫至Publish。

* Dispatcher Flush這是用於管理Dispatcher快取。 另請參閱 [使編寫環境中的Dispatcher快取失效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment) 和 [使發佈執行個體中的Dispatcher快取失效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance) 以取得詳細資訊。

* [反向復寫](#reverse-replication-publish-to-author)
用於從發佈復寫至作者。 反向復寫不適用於Communities功能，例如論壇、部落格和評論。 由於未啟用寄件匣，因此此功能實際上已停用。 使用反向復寫需要自訂設定。

* 靜態代理程式這是將節點的靜態表示儲存到檔案系統中的代理程式。
例如，使用預設設定時，內容頁面和DAM資產會儲存在 `/tmp`，以HTML或適當的資產格式顯示。 請參閱 `Settings` 和 `Rules` 用於設定的標籤。
已要求此專案，以便當直接從應用程式伺服器要求頁面時，可以看到內容。 這是專門的代理程式，（可能）在大多數執行個體中並非必要。

## 復寫代理程式 — 設定引數 {#replication-agents-configuration-parameters}

從「工具」控制檯設定復寫代理程式時，對話方塊中有四個索引標籤可用：

### 設定 {#settings}

* **名稱**

  復寫代理的唯一名稱。

* **說明**

  此復寫代理程式用途的說明。

* **已啟用**

  表示復寫代理程式是否已啟用。

  當代理程式為 **已啟用**，則佇列顯示為：

   * **作用中** 處理專案時。
   * **閒置** 當佇列為空時。
   * **已封鎖** 當專案在佇列中，但無法處理時；例如，當接收佇列停用時。

* **序列化型別**

  序列化的型別：

   * **預設**：設定是否自動選取代理程式。
   * **Dispatcher排清**：如果要使用代理程式來排清Dispatcher快取，請選取此選項。

* **重試延遲**

  若發生問題，兩次重試之間的延遲（等待時間，以毫秒為單位）。

  預設： `60000`

* **代理使用者ID**

  根據環境，代理程式會使用此使用者帳戶來：

   * 從製作環境收集內容並封裝
   * 在發佈環境中建立和寫入內容

  將此欄位留空以使用系統使用者帳戶(在sling中定義為管理員使用者的帳戶；預設為 `admin`)。

  >[!CAUTION]
  >
  >對於作者環境上的代理程式，此帳戶 *必須* 擁有您要復寫之所有路徑的讀取存取權。

  >[!CAUTION]
  >
  >對於發佈環境上的代理程式，此帳戶 *必須* 具有復寫內容所需的建立/寫入許可權。

  >[!NOTE]
  >
  >這可用來作為選取復製作業特定內容的機制。

* **記錄層級**

  指定用於記錄訊息的詳細資訊等級。

   * `Error`：僅記錄錯誤
   * `Info`：記錄錯誤、警告和其他資訊訊息
   * `Debug`：訊息會使用高層次的詳細資料，主要用於偵錯

  預設： `Info`

* **用於反向復寫**

  指出此代理程式是否用於反向復寫；從發佈環境傳回使用者輸入至製作環境。

* **別名更新**

  選取此選項會啟用對Dispatcher的別名或虛名路徑失效請求。 另請參閱 [設定Dispatcher Flush代理程式](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent).

#### 傳輸 {#transport}

* **URI**

  這會指定目標位置的接收servlet。 尤其是，您可以在此處指定目標執行個體的主機名稱（或別名）和內容路徑。

  例如：

   * 預設代理程式可以復寫至 `https://localhost:4503/bin/receive`
   * Dispatcher Flush代理程式可能會復寫到 `https://localhost:8000/dispatcher/invalidate.cache`

  此處指定的通訊協定（HTTP或HTTPS）會決定傳輸方法。

  對於Dispatcher Flush代理程式，只有當您使用以路徑為根據的虛擬主機專案來區分陣列時，才會使用URI屬性，而您會使用此欄位來鎖定要失效的陣列。 例如，陣列 #1 的虛擬主機為 `www.mysite.com/path1/*`，而陣列 #2 的虛擬主機為 `www.mysite.com/path2/*`。 您可以使用URL `/path1/invalidate.cache` 以第一個陣列為目標，並 `/path2/invalidate.cache` 以定位第二個陣列。

* **使用者**

  用於存取目標的帳戶使用者名稱。

* **密碼**

  用於存取目標的帳戶密碼。

* **NTLM網域**

  NTML驗證的網域。

* **NTLM主機**

  NTML驗證的主機。

* **啟用寬鬆SSL**

  如果您希望接受自我認證的SSL憑證，請啟用。

* **允許過期的憑證**

  若要接受過期的SSL憑證，請啟用。

#### Proxy {#proxy}

只有在需要Proxy時，才需要下列設定：

* **Proxy主機**

  用於傳輸的Proxy主機名稱。

* **Proxy連線埠**

  Proxy的連線埠。

* **Proxy使用者**

  要使用的帳戶使用者名稱。

* **Proxy密碼**

  要使用的帳戶密碼。

* **Proxy NTLM網域**

  代理NTLM網域。

* **Proxy NTLM主機**

  代理NTLM網域。

#### 延伸 {#extended}

* **介面**

  您可以在此處定義要繫結的通訊端介面。

  這會設定建立連線時要使用的本機位址。 如果未設定，則使用預設地址。 這對於指定要在多主伺服器或叢集化系統上使用的介面非常有用。

* **HTTP方法**

  要使用的HTTP方法。

  對於Dispatcher Flush代理程式，這幾乎一律為GET且不應變更(POST是另一個可能的值)。

* **HTTP標題**

  這些用於Dispatcher Flush代理程式，並指定必須清除的元素。

  對於Dispatcher Flush代理程式，不需要變更三個標準專案：

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

  在適當情況下，這些字元可用於指出排清控制代碼或路徑時要使用的動作。 子引數是動態的：

   * `{action}` 表示復寫動作

   * `{path}` 表示路徑

  這些變數會由與請求相關的路徑/動作取代，因此不需要「硬式編碼」：

  >[!NOTE]
  >
  >如果您在建議預設內容以外的內容中安裝了AEM，則必須在HTTP標頭中註冊該內容。 例如：
  >`CQ-Handle:/<*yourContext*>{path}`

* **關閉連線**

  啟用，以便您在每次請求後都可關閉連線。

* **連線逾時**

  嘗試建立連線時要套用的逾時（毫秒）。

* **通訊端逾時**

  建立連線後等待流量時所套用的逾時（毫秒）。

* **通訊協定版本**

  通訊協定的版本。 例如， `1.0` 適用於HTTP/1.0。

#### 觸發器 {#triggers}

這些設定是用來定義自動復寫的觸發程式：

* **忽略預設值**

  如果勾選，代理將從預設復寫中排除；這意味著如果內容作者發出復寫動作，則不會使用代理。

* **修改**

  在此，當頁面修改時，將自動觸發此代理程式的復寫。 用於Dispatcher Flush代理程式，也用於反向復寫。

* **於散佈**

  如果勾選，代理程式會在修改內容時自動複製標籤為分發的任何內容。

* **已達到開啟/關閉時間**

  當為頁面定義的時間或折扣發生時，就會觸發自動復寫（以視需要啟用或停用頁面）。 這主要用於Dispatcher Flush代理程式。

* **接收時**

  如果勾選，代理會在接收到復寫事件時進行復寫。

* **無狀態更新**

  選取後，代理程式不會強制復寫狀態更新。

* **無版本設定**

  選取後，代理程式不會強制活動頁面的版本設定。

## 設定復寫代理 {#configuring-your-replication-agents}

如需有關使用MSSL將復寫代理程式連線至發佈執行個體的資訊，請參閱 [使用雙向SSL復寫](/help/sites-deploying/mssl-replication.md).

### 從製作環境設定復寫代理 {#configuring-your-replication-agents-from-the-author-environment}

在「作者」環境的「工具」標籤中，您可以設定存放在「作者」環境(**作者上的代理程式**)或發佈環境(**發佈代理程式**)。 以下程式說明為Author環境設定代理程式，但可用於兩者。

>[!NOTE]
>
>當Dispatcher處理製作或發佈執行個體的HTTP請求時，來自復寫代理程式的HTTP請求必須包含PATH標頭。 除了以下程式外，您必須將PATH標頭新增到Dispatcher的使用者端標頭清單。 另請參閱 [/clientheaders （使用者端標頭）](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders).
>

1. 存取 **工具** AEM索引標籤中的「 」。
1. 按一下 **復寫** （左窗格以開啟資料夾）。
1. 按兩下 **作者上的代理程式** （左窗格或右窗格）。
1. 按一下適當的代理程式名稱（連結）以顯示該代理程式的詳細資訊。
1. 按一下 **編輯** 因此會開啟設定對話方塊：

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. 提供的值應足以進行預設安裝。 若您進行變更，請按一下 **確定** 以儲存它們(請參閱 [復寫代理程式 — 設定引數](#replication-agents-configuration-parameters) 以取得個別引數的詳細資訊)。

>[!NOTE]
>
>AEM的標準安裝會指定 `admin` 在預設的復寫代理程式中作為傳輸認證的使用者。
>
>這應該變更為具有複製所需路徑之許可權的站台特定複製使用者帳戶。

### 設定反向復寫 {#configuring-reverse-replication}

反向復寫是用來將發佈執行個體上產生的使用者內容傳回作者執行個體。 這通常用於調查和登錄檔單等功能。

基於安全理由，大多數網路拓撲都不允許連線 *從* 「非軍事區域」(將外部服務公開給不受信任的網路（例如網際網路）的子網路)。

由於發佈環境通常位於DMZ，若要將內容取回製作環境，必須從製作執行個體起始連線。 這是透過下列專案完成的：

* 一個 *寄件匣* 在放置內容的發佈環境中。
* 製作環境中的代理程式（發佈），會定期輪詢寄件匣以尋找新內容。

>[!NOTE]
>
>適用於AEM [Communities](/help/communities/overview.md)，復寫不適用於發佈執行個體上使用者產生的內容。 另請參閱 [社群內容儲存](/help/communities/working-with-srp.md).

若要這麼做，您需要：

**創作環境中的反向復寫代理程式**  — 作為使用中元件，從發佈環境中的寄件匣收集資訊：

如果您想要使用反向復寫，請確定此代理程式已啟用。

![chlimage_1-23](assets/chlimage_1-23.png)

**發佈環境中的反向復寫代理程式（寄件匣）**  — 被動元素作為「寄件匣」。 使用者輸入會放置在這裡，由代理程式在製作環境中收集。

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### 為多個發佈執行個體設定復寫 {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>僅複製內容 — 不複製使用者資料（使用者、使用者群組和使用者設定檔）。
>
>若要同步多個發佈執行個體的使用者資料，請啟用 [使用者同步](/help/sites-administering/sync.md).

安裝後，已設定預設代理程式，以便將內容復寫至在localhost的連線埠4503上執行的發佈執行個體。

若要設定其他發佈執行個體的內容復寫，請建立並設定新的復寫代理程式：

1. 開啟 **工具** AEM索引標籤中的「 」。
1. 選取 **復寫**，然後 **作者上的代理程式** 在左側面板中。
1. 選取 **新增……**.
1. 設定 **標題** 和 **名稱**，然後選取 **復寫代理**.
1. 按一下 **建立** 以便建立代理程式。
1. 連按兩下新代理程式專案，組態面板就會開啟。
1. 按一下 **編輯** - **代理程式設定** 對話方塊開啟 —  **序列化型別** 已定義為「預設」，此狀態必須維持不變。

   * 在 **設定** 標籤：

      * 啟動 **已啟用**.
      * 輸入 **說明**.
      * 設定 **重試延遲** 至 `60000`.

      * 離開 **序列化型別** 作為 `Default`.

   * 在 **傳輸** 標籤：

      * 輸入新發佈執行個體的必要URI；例如，
        `https://localhost:4504/bin/receive`。

      * 輸入用於復寫的站台特定使用者帳戶。
      * 您可以視需要設定其他引數。

1. 按一下&#x200B;**「確定」**。

接著，您可以在作者環境中更新，然後發佈頁面，以測試操作。

更新會顯示在已依上述方式設定的所有發佈執行個體上。

如果您遇到任何問題，可以檢視Author執行個體上的記錄。 視所需的詳細程度而定，您也可以設定 **記錄層級** 至 `Debug` 使用 **代理程式設定** 對話方塊，如上所述。

>[!NOTE]
>
>這可以結合使用 [代理使用者ID](#agentuserid) 以選取不同的內容來復寫至個別發佈環境。 對於每個發佈環境：
>
>1. 設定復寫代理以復寫至該發佈環境。
>1. 設定使用者帳戶；具有讀取復寫至該特定發佈環境的內容所需的存取許可權。
>1. 將使用者帳戶指派為 **代理使用者ID** 用於復寫代理程式。
>

### 設定Dispatcher Flush代理程式 {#configuring-a-dispatcher-flush-agent}

預設代理程式會包含在安裝中。 不過，您仍需要特定設定，如果您定義新的代理程式，也同樣適用：

1. 開啟 **工具** AEM索引標籤中的「 」。
1. 按一下 **部署**.
1. 選取 **復寫** 然後 **發佈代理程式**.
1. 按兩下 **Dispatcher排清** 專案以開啟總覽。
1. 按一下 **編輯** - **代理程式設定** 對話方塊開啟：

   * 在 **設定** 標籤：

      * 啟動 **已啟用**.
      * 輸入 **說明**.
      * 離開 **序列化型別** 作為 `Dispatcher Flush`，或若建立代理程式則進行此設定。

      * （選擇性）選取 **別名更新** 啟用對Dispatcher的別名或虛名路徑失效請求。

   * 在 **傳輸** 標籤：

      * 輸入新發佈執行個體的必要URI；例如，
        `https://localhost:80/dispatcher/invalidate.cache`。

      * 輸入用於復寫的站台特定使用者帳戶。
      * 您可以視需要設定其他引數。

   對於Dispatcher Flush代理程式，只有當您使用以路徑為根據的虛擬主機專案來區分陣列時，才會使用URI屬性，而您會使用此欄位來鎖定要失效的陣列。 例如，陣列 #1 的虛擬主機為 `www.mysite.com/path1/*`，而陣列 #2 的虛擬主機為 `www.mysite.com/path2/*`。 您可以使用URL `/path1/invalidate.cache` 以第一個陣列為目標，並 `/path2/invalidate.cache` 以定位第二個陣列。

   >[!NOTE]
   >
   >如果您已在非建議預設內容中安裝AEM，請設定 [HTTP標題](#extended) 在 **延伸** 標籤。

1. 按一下&#x200B;**「確定」**。
1. 返回 **工具** 標籤，從這裡您可以 **啟動** 此 **Dispatcher排清** 代理程式(**發佈代理程式**)。

此 **Dispatcher排清** 復寫代理程式在作者上並非作用中。 您可以使用對等的URI，在發佈環境中存取相同的頁面；例如， `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### 控制對復寫代理程式的存取 {#controlling-access-to-replication-agents}

對用來設定復寫代理的頁面的存取權，可以透過以下專案上的使用者和/或群組頁面許可權來控制： `etc/replication` 節點。

>[!NOTE]
>
>設定這類許可權不會影響使用者復寫內容（例如，從網站主控台或Sidekick選項）。 復寫架構在復寫頁面時，不會使用目前使用者的「使用者工作階段」來存取復寫代理。

### 從CRXDE Lite設定您的復寫代理 {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>僅支援在中建立復寫代理 `/etc/replication` 存放庫位置。 必須具備此條件才能正確處理關聯的ACL。 在樹狀結構的其他位置建立復寫代理程式，可能會導致未經授權的存取。

您可以使用CRXDE Lite來設定復寫代理的各種引數。

如果您導覽至 `/etc/replication`，您會看到下列三個節點：

* `agents.author`
* `agents.publish`
* `treeactivation`

兩個 `agents` 保留適當環境的組態資訊，而且僅在該環境執行時有效。 例如， `agents.publish` 僅用於發佈環境。 以下熒幕擷圖顯示製作環境中的Publish代理程式(包含在AEM WCM中)：

![chlimage_1-24](assets/chlimage_1-24.png)

## 監視復寫代理程式 {#monitoring-your-replication-agents}

監督復寫代理程式：

1. 存取 **工具** AEM索引標籤中的「 」。
1. 按一下 **復寫**.
1. 連按兩下適當環境（左窗格或右窗格）代理程式的連結。 例如， **作者上的代理程式**.

   產生的視窗會顯示製作環境的所有復寫代理程式概觀，包括其目標和狀態。

1. 按一下適當的代理程式名稱（連結）以顯示該代理程式的詳細資訊：

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   您可以在這裡進行以下作業︰

   * 檢視代理程式是否已啟用。
   * 檢視任何復寫的目標。
   * 檢視復寫佇列是否為使用中（已啟用）。
   * 檢視佇列中是否有任何專案。
   * **重新整理** 或 **清除** 更新佇列專案的顯示。 這可協助您檢視專案是否進入及離開佇列。

   * **檢視記錄** 存取復寫代理程式的任何動作記錄。
   * **測試連線** 至目標執行個體。
   * **強制重試** 在任何佇列專案上（如有必要）。

   >[!CAUTION]
   >
   >請勿在發佈執行個體上的反向復寫寄件匣使用「測試連線」連結。
   >
   >
   >如果對Outbox佇列執行復寫測試，則任何早於測試復寫的專案都會透過每次反向復寫重新處理。
   >
   >
   >如果佇列中存有這類專案，可在下列XPath JCR查詢中找到並移除它們。
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## 批次復寫 {#batch-replication}

批次複製不會複製個別頁面或資產，但會根據時間或大小等待觸發兩者的第一個臨界值。

接著，它會將所有復寫專案封裝到一個封裝中，然後以單一檔案的形式復寫到發行者。

Publisher會解壓縮所有專案、儲存專案，並向作者回報。

### 設定批次複製 {#configuring-batch-replication}

1. 前往 `http://serveraddress:serverport/siteadmin`
1. 按下 **[!UICONTROL 工具]** 圖示加以顯示
1. 從左側導覽邊欄，前往 **[!UICONTROL 復寫 — 作者上的代理]** 並連按兩下 **[!UICONTROL 預設代理程式]**.
   * 您也可以直接前往「 」，存取預設發佈復寫代理程式。 `http://serveraddress:serverport/etc/replication/agents.author/publish.html`
1. 按下 **[!UICONTROL 編輯]** 按鈕進行複製。
1. 在下列視窗中，移至 **[!UICONTROL 批次]** 標籤：
   ![批次復寫](assets/batchreplication.png)
1. 設定代理。

### 參數 {#parameters}

* `[!UICONTROL Enable Batch Mode]`  — 啟用或停用批次複製模式
* `[!UICONTROL Max Wait Time]`  — 開始批次要求前的等待時間上限（以秒為單位）。 預設值為2秒。
* `[!UICONTROL Trigger Size]`  — 在此大小限制時開始批次復寫

## 其他資源 {#additional-resources}

如需疑難排解的詳細資訊，請參閱 [疑難排解復寫](/help/sites-deploying/troubleshoot-rep.md) 頁面。
