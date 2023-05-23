---
title: 與Adobe動態Tag Management整合
seo-title: Integrating with Adobe Dynamic Tag Management
description: 瞭解與Adobe動態Tag Management的整合。
seo-description: Learn about integration with Adobe Dynamic Tag Management.
uuid: cbb9f942-44e3-4cd5-b07d-4298a7a08376
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b8c7a20a-7694-4a49-b66a-060720f17dad
exl-id: 1e0821f5-627f-4262-ba76-62303890e112
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2208'
ht-degree: 1%

---

# 與Adobe動態Tag Management整合 {#integrating-with-adobe-dynamic-tag-management}

整合 [Adobe力Tag Management](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) 以AEM便您使用動態Tag Management網站屬性跟蹤AEM網站。 動態Tag Management使營銷人員能夠管理用於收集資料的標籤，並跨數字營銷系統分發資料。 例如，使用動態Tag Management收集網站的使AEM用資料並分發資料以在Adobe Analytics或Adobe Target進行分析。

在整合之前，您需要建立動態Tag Management [Web屬性](https://microsite.omniture.com/t2/help/en_US/dtm/#Web_Properties) 跟蹤你網站的AEM域。 的 [托管選項](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) 必須配置web屬性，以便您可以配置AEM以訪問動態Tag Management庫。

配置整合後，對動態Tag Management部署工具和規則的更改不要求您更改中的動態Tag Management配置AEM。 更改可自動AEM使用。

>[!NOTE]
>
>如果將DTM與自定義代理配置一起使用，則需要配置兩個HTTP客戶端代理配置AEM，因為某些功能使用3.x API，而另一些則使用4.x API:
>
>* 3.x配置 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x配置 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


## 部署選項 {#deployment-options}

以下部署選項會影響與動態Tag Management的整合配置。

### 動態Tag Management托管 {#dynamic-tag-management-hosting}

支AEM持在雲中托管或在上托管的動態Tag ManagementAEM。

* 雲托管：動態Tag Managementjavascript庫儲存在雲中，您的頁面AEM直接引用它們。
* 托AEM管：動態Tag Management生成javascript庫。 使AEM用工作流模型獲取和安裝庫。

您的實施所使用的托管類型決定了您執行的某些配置和實施任務。 有關托管選項的資訊，請參見 [托管 — 嵌入頁籤](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) 在動態Tag Management幫助中。

### 暫存和生產庫 {#staging-and-production-library}

確定作者實AEM例是使用動態Tag Management登台還是生產代碼。

通常，作者實例使用動態Tag Management暫存庫，而生產實例使用生產庫。 此方案使您能夠使用作者實例test未批准的動態Tag Management配置。

如果需要，您的作者實例可以使用生產庫。 Web瀏覽器插件可用，使您能夠在使用臨時庫進行測試時在這些庫承載雲時進行切換。

### 使用動態Tag Management部署掛接 {#using-the-dynamic-tag-management-deployment-hook}

承載AEM動態Tag Management庫時，可以使用動態Tag Management部署掛接服務自動將庫更新推送到AEM。 在對庫進行更改時(如編輯動態Tag ManagementWeb屬性時)推送庫更新。

要使用部署掛接，動態Tag Management必須能夠連AEM接到承載庫的實例。 你必須 [啟用訪問權AEM](/help/sites-administering/dtm.md#enabling-access-for-the-deployment-hook-service) 動態Tag Management伺服器。

在某些AEM情況下，如當位於防火牆AEM後面時，可能無法訪問。 在這些情況下，可使用輪AEM詢導入程式選項定期檢索庫。 cron作業表達式指定庫下載的時間表。

## 為部署掛接服務啟用訪問 {#enabling-access-for-the-deployment-hook-service}

啟用動態Tag Management部署掛接服務AEM以訪問，以便該服務可以更AEM新托管庫。 指定動態Tag Management伺服器的IP地址，根據需要更新暫存和生產庫：

* 分段: `107.21.99.31`
* 生產： `23.23.225.112` 和 `204.236.240.48`

使用 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [`sling:OsgiConfig`](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) 節點：

* 在Web控制台中，使用「配置」頁上的AdobeDTM部署掛接配置項。
* 對於OSGi配置，服務PID為 `com.adobe.cq.dtm.impl.servlets.DTMDeployHookServlet`。

下表說明了要配置的屬性。

| Web控制台屬性 | OSGi屬性 | 說明 |
|---|---|---|
| 暫存DTM IP白名單 | `dtm.staging.ip.whitelist` | 更新臨時庫的動態Tag Management伺服器的IP地址。 |
| 生產DTM IP白名單 | `dtm.production.ip.whitelist` | 更新生產庫的動態Tag Management伺服器的IP地址。 |

## 建立動態Tag Management配置 {#creating-the-dynamic-tag-management-configuration}

建立雲配置，以便實AEM例可以通過動態Tag Management驗證並與Web屬性交互。

>[!NOTE]
>
>當您的DTM Web屬性包含Adobe Analytics工具並且您還在使用 [內容透視](/help/sites-authoring/content-insights.md)。 在 [Adobe Analytics雲配置](/help/sites-administering/adobeanalytics-connect.md#configuring-the-connection-to-adobe-analytics)，選擇「不包括跟蹤代碼」選項。

### 一般設定 {#general-settings}

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>API令牌</td>
   <td>動態Tag Management用戶帳戶的API令牌屬性的值。 使AEM用此屬性向動態Tag Management驗證</td>
  </tr>
  <tr>
   <td>公司</td>
   <td>與您的登錄ID關聯的公司。</td>
  </tr>
  <tr>
   <td>屬性</td>
   <td>為管理站點的標籤而建立的Web屬性的AEM名稱。</td>
  </tr>
  <tr>
   <td>加入有關作者的生產代碼</td>
   <td><p>選擇此選項可AEM使作者和發佈實例使用動態Tag Management庫的生產版本。 </p> <p>如果未選中此選項，「暫存設定」將應用於作者實例，「生產設定」將應用於發佈實例。</p> </td>
  </tr>
 </tbody>
</table>

### 自主承載屬性 — 暫存和生產 {#self-hosting-properties-staging-and-production}

動態Tag Management配置的以下屬性可AEM以承載動態Tag Management庫。 這些屬性AEM可以下載和安裝庫。 （可選）您可以自動更新庫，以確保它們反映在動態Tag Management管理應用程式中所做的任何更改。

某些屬性使用您從「嵌入」頁籤的「庫下載」部分獲取的「動態Tag Management」Web屬性值。 有關資訊，請參見 [庫下載](https://microsite.omniture.com/t2/help/en_US/dtm/#Library_Download) 在動態Tag Management幫助中。

>[!NOTE]
>
>在上承載動態Tag Management捆綁包AEM時，必須先在動態Tag Management中啟用「庫下載」，然後才能建立配置。 此外，必須啟用Akamai，因為Akamai提供用於下載的庫。

在上承載動態Tag ManagementAEM庫AEM時，會根據您的配置自動配置Web屬性的某些屬性。 請參見下表中的說明。

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>使用自主托管</td>
   <td>選擇在上承載動態Tag Management庫檔案的時AEM間。 選擇此選項將顯示此表中的其他屬性。</td>
  </tr>
  <tr>
   <td>DTM 組合包 URL</td>
   <td>用於下載動態Tag Management庫的URL。 從動態Tag Management的庫下載頁面的下載URL部分獲取此值。 出於安全原因，必須手動配置此值。</td>
  </tr>
  <tr>
   <td>下載工作流程</td>
   <td><p>用於下載和安裝動態Tag Management庫的工作流模型。 預設模型為「預設DTM包下載」(Default DTM Bundle Download)。 除非已建立自定義模型，否則使用此模型。</p> <p>請注意，預設下載工作流會在下載庫時自動激活它們。</p> </td>
  </tr>
  <tr>
   <td>網域提示</td>
   <td><p>（可選）承載動態AEMTag Management庫的伺服器的域。 指定值以覆蓋為 <a href="/help/sites-developing/externalizer.md">第CQ天連結外部化程式服務</a>。</p> <p>連接到動態Tag ManagementAEM後，使用此值為動態Tag ManagementWeb屬性配置「庫下載」屬性的「暫存HTTP路徑」或「生產HTTP路徑」。</p> </td>
  </tr>
  <tr>
   <td>安全域提示</td>
   <td><p>（可選）承載HTTPSAEM動態Tag Management庫的伺服器域。 指定值以覆蓋為 <a href="/help/sites-developing/externalizer.md">第CQ天連結外部化程式服務</a>。</p> <p>連接到動態Tag ManagementAEM後，使用此值為動態Tag ManagementWeb屬性配置「庫下載」屬性的「暫存HTTPS路徑」或「生產HTTPS路徑」。</p> </td>
  </tr>
  <tr>
   <td>共用機密</td>
   <td><p>（可選）用於解密下載的共用密鑰。 從動態Tag Management的庫下載頁面的共用密鑰欄位獲取此值。</p> <p><strong>注：</strong> 您必須 <a href="https://www.openssl.org/docs/apps/openssl.html">OpenSSL</a> 安裝在電腦上AEM的庫，以便AEM解密下載的庫。</p> </td>
  </tr>
  <tr>
   <td>啟用 Polling Importer</td>
   <td><p>（可選）選擇定期下載和安裝動態Tag Management庫，以確保您使用的是更新的版本。 選中後，動態Tag Management不會將HTTPPOST請求發送到部署掛接URL。</p> <p>自AEM動配置動態Tag ManagementWeb屬性的「庫下載」屬性的「部署掛接URL」屬性。 選中後，該屬性將配置為無值。 如果未選中，則使用動態Tag Management配置的URL配置屬性。</p> <p>當動態Tag Management部署掛接無法連接時啟AEM用輪詢導入程式，例AEM如在防火牆後。</p> </td>
  </tr>
  <tr>
   <td>排程運算式</td>
   <td>（顯示並在選擇「啟用輪詢導入程式」時是必需的。） 控制下載動態標籤管理庫的時間的cron表達式。</td>
  </tr>
 </tbody>
</table>

![chlimage_1-352](assets/chlimage_1-352.png)

### 雲托管屬性 — 暫存和生產 {#cloud-hosting-properties-staging-and-production}

在雲托管動態標籤配置時，可為動態Tag Management配置配置配置以下屬性。

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>使用自主托管</td>
   <td>在雲中托管動態Tag Management庫檔案時清除此選項。</td>
  </tr>
  <tr>
   <td>頁首程式碼</td>
   <td><p>從主機的動態Tag Management獲取的用於轉移的標頭代碼。 連接到「動態Tag Management」時，會自動填充此值。</p> <p> 要查看動態Tag Management中的代碼，請按一下「嵌入」頁籤，然後按一下主機名。 展開「題頭代碼」部分，然後根據需要按一下「臨時嵌入代碼」或「生產嵌入代碼」區域的「複製嵌入代碼」。</p> </td>
  </tr>
  <tr>
   <td>頁尾程式碼</td>
   <td><p>從主機的動態Tag Management獲取的用於暫存的腳注代碼。 連接到「動態Tag Management」時，會自動填充此值。</p> <p>要查看動態Tag Management中的代碼，請按一下「嵌入」頁籤，然後按一下主機名。 展開「頁腳代碼」部分，然後根據需要按一下「臨時嵌入代碼」或「生產嵌入代碼」區域的「複製嵌入代碼」。</p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-353](assets/chlimage_1-353.png)

以下過程使用觸控優化的UI配置與動態Tag Management的整合。

1. 在滑軌上，按一下「工具」>「操作」>「雲」>「Cloud Services」。
1. 在「動態Tag Management」區域中，將顯示以下用於添加配置的連結之一：

   * 如果這是您添加的第一個配置，請按一下「立即配置」。
   * 如果已建立一個或多個配置，請按一下「顯示配置」，然後按一下「可用配置」旁的+連結。

   ![chlimage_1-354](assets/chlimage_1-354.png)

1. 鍵入配置的標題，然後按一下「建立」。
1. 在「API令牌」欄位中，輸入動態Tag Management用戶帳戶的API令牌屬性的值。

   要獲取API令牌的值，請與DTM Client Care聯繫。

   >[!NOTE]
   >
   >API令牌在動態Tag Management用戶明確請求之前不會過期。

   ![chlimage_1-355](assets/chlimage_1-355.png)

1. 按一下「Connect to DTM（連接到DTM）」。 使AEM用動態Tag Management驗證並檢索您的帳戶關聯的公司清單。
1. 選擇公司，然後選擇您用於跟蹤站點的屬AEM性。
1. 如果在作者實例上使用臨時代碼，請取消選擇「在作者上包括生產代碼」。
1. 如果需要，請在「轉移設定」頁籤和「生產設定」頁籤上提供屬性值，然後按一下「確定」。

## 手動下載動態Tag Management庫 {#manually-downloading-the-dynamic-tag-management-library}

手動下載動態Tag Management庫，以立即更新AEM。 例如，在計畫輪詢導入程式自動下載庫之前，如果要test更新的庫，請手動下載。

1. 在滑軌上，按一下「工具」>「操作」>「雲」>「Cloud Services」。
1. 在「動態Tag Management」區域，按一下「顯示配置」，然後按一下配置。
1. 在「暫存設定」區域或「生產設定」區域中，按一下「觸發器下載工作流」按鈕以下載和部署庫包。

   ![chlimage_1-356](assets/chlimage_1-356.png)

>[!NOTE]
>
>下載的檔案儲存在 `/etc/clientlibs/dtm/my config/companyID/propertyID/servertype`。
>
>以下內容直接從 [DTM配置](#creating-the-dynamic-tag-management-configuration)。
>
>* `myconfig`
>* `companyID`
>* `propertyID`
>* `servertype`
>


## 將動態Tag Management配置與您的站點關聯 {#associating-a-dynamic-tag-management-configuration-with-your-site}

將動態Tag Management配置與網站的頁面相關聯，AEM以便向頁面添加所需指令碼。 將站點的根頁與配置關聯。 該頁的所有子體都繼承關聯。 如果需要，可覆蓋子體頁面上的關聯。

請按下列步驟將頁面和子體與動態Tag Management配置關聯。

1. 在經典UI中開啟站點的根頁。
1. 使用Sidekick開啟頁面屬性。
1. 在「Cloud Services」頁籤上，按一下「添加服務」，選擇「動態Tag Management」，然後按一下「確定」。

   ![chlimage_1-357](assets/chlimage_1-357.png)

1. 使用「動態Tag Management」下拉菜單選擇配置，然後按一下「確定」。

請按下列步驟覆蓋頁的繼承配置關聯。 覆蓋會影響頁面和所有頁面子體。

1. 在經典UI中開啟頁面。
1. 使用Sidekick開啟頁面屬性。
1. 在「Cloud Services」頁籤上，按一下「繼承自」屬性旁邊的掛鎖表徵圖，然後在確認對話框中按一下「是」。

   ![chlimage_1-358](assets/chlimage_1-358.png)

1. 刪除或選擇其他動態Tag Management配置，然後按一下確定。
