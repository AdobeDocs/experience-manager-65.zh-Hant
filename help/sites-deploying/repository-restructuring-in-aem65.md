---
title: AEM 6.5中的資料庫重組
seo-title: AEM 6.5中的資料庫重組
description: 瞭解AEM 6.5中的儲存庫重組
seo-description: 瞭解AEM 6.5中的儲存庫重組
uuid: bc577c82-3279-4ddd-898c-607864868db0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 274a7f5a-d509-4ca9-9ae5-30e48f34f171
docset: aem65
redirecttarget: /content/help/en/experience-manager/6-5/help/sites-deploying/repository-restructuring.html
translation-type: tm+mt
source-git-commit: bd0dc09ea230416ad3544d14440b7b74b80ec406

---


# AEM 6.5中的資料庫重組 {#repository-restructuring-in-aem}

## 簡介 {#introduction}

在AEM 6.5之前，客戶程式碼部署在JCR的不可預測區域，這些區域可能會因升級而變更。 因此，正式的AEM版本（主要版本、功能套件、Service pack或Hotfix）常會覆寫自訂程式碼、設定或內容。 此外，客戶變更有時會覆寫AEM產品代碼或內容，突破產品功能。

這些衝突並不總是能夠自動解決的，需要大量的處理時間來標籤，需要人為干預來解決，其解決方法並不總是明確的。 透過清楚說明AEM產品程式碼和客戶程式碼的階層，可以避免這些衝突。

為此，從AEM 6.5開始，並在未來版本中繼續，內容將從儲存庫中的其他檔案夾重新架構，以及內容所在位置的准則，並遵守下列高階規則： `/etc`

* AEM產品程式碼一律會放入 `/libs`，自訂程式碼不得覆寫
* 自訂代碼應放 `/apps`入、 `/content`和 `/conf`

本文分為三個部分，代表已移出的內容類型 `/etc`:

1. 設定
1. 用戶端資源庫
1. 其他

每個部分包括：

* 具有重組位置和附加上下文的表。 在不久的將來，預計表格將格式化為更平坦的結構，以改善可讀性。
* 擴充性策略，可讓自訂程式碼成功擴充位於下方的AEM應用程式 `/libs`碼。

## 向後相容性 {#backwards-compatibility}

在大多數情況下，在升級至AEM 6.5後，會維持與舊位置的回溯相容性。除了新增的位置外，舊位置也會保留並受到產品程式碼的尊重。 在大多數情況下，條件式邏輯會用來檢查舊資料夾是否存在，並從中讀取內容，而非新位置。

在6.5升級後，建議客戶自行移除舊位置，以便使用新位置的內容。 下表說明如何依據每個位置遵循新的內容結構。

>[!NOTE]
>
>就地升級實例除了新位置外，還將包括舊內容位置。 全新的開發人員安裝將僅包含新位置。

## 如何閱讀表格 {#how-to-read-the-tables}

每節中的表格包括：

* 與此內容相關的AEM解決方案（網站、資產、表單等）
* 舊（6.4和舊版）位置
* 新的6.5位置
* 與新內容結構對齊的指示。 例如，在6.5升級後的數週或數月內，可能需要執行指令碼或手動移動檔案
* AEM使用的方法，可讓從舊版升級至AEM 6.5的客戶，維持舊內容位置向後相容性

## 設定 {#configuration}

本節中的內容位置通常是指位於、或下 `/settings` 方的資 `/libs`料 `/apps`夾下的內容 `/conf`。

### 擴充性策略 {#extensibility-strategy}

一般而言，但除少數例外情況外，您可使用Apache Sling的 [ Context Aware Configuration功能擴充本節中的內容](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) 。

簡而言之，上下文感知配置允許儲存庫的一部分內容通過儲存庫的其他部分的內容被多次覆蓋。 例如，中的內容 `/libs` 可以由中的內容覆蓋， `/apps`然後可以由中的內容覆蓋 `/conf`。 此外，下方全域資料夾中的 `/conf` 內容可由特定「租用戶」或「網站」(例如 `/conf/we-retail/settings`)。

通常，上下文感知配置用作擴展功能配置的策略，但有些情況下，其他內容類型會使用該配置。

下表包含名為「配置類型」的另一列，以說明可以覆蓋配置的範圍。 以下是這些配置類型的其他詳細資訊：

**不感知上下文**

* 資源恰好位於上下文感知的資料夾結構(如 `/libs/settings`)中，但始終通過絕對路徑引用，因此上下文感知無效。
* 資源可以隨處使用。 例如，資產DRM授權可能位於 `/content/my-customer/licenses/creative-commons.html`
* 範例：

   * 工作流程指令碼-> `/apps/settings/workflow/scripts/noop.ecma`
   * 資產DRM授權-> `/apps/settings/dam/drm/my-license`

**僅全局**

* 僅包含全局配置的功能
* 作為參考點，請優先選擇此示例中的設定： `/libs/settings` &lt; `/apps/settings` &lt; `/conf/global`

* AEM僅支援全域設定，不支援租用戶化設定
* AEM將始終開始在/conf/global級別首先查找配置

* 範例：

   * 工作流程啟動器 -> `/libs/settings/workflow/launcher`
   * 工作流程模型 -> `/conf/global/settings/workflow/models`

**租用戶感知**

* 若為租用戶感知的設定，請參閱此範例以取得設定路徑的優先順序： `/libs/settings` &lt; `/apps/settings``/conf/global` &lt; `/conf/we-retail`，其中we-retail是租用戶名。 租戶感知配置也支援子租戶。

* AEM支援趨勢化組態。 它尊重 `cq:conf` 等級制度
* 範例：

   * 可編輯的範本 -> `/conf/we-retail/settings/wcm/templates`
   * 雲配置-> `/conf/we-retail/settings/cloudsettings`

<table>
 <tbody>
  <tr>
   <td><strong>解決方案</strong></td>
   <td><strong>上一個位置</strong><br /> </td>
   <td><strong>新位置</strong></td>
   <td><strong>上下文感知配置類型</strong><br /> </td>
   <td><strong>向後相容性方法</strong></td>
   <td><strong>符合最新機型的需求</strong></td>
  </tr>
  <tr>
   <td>AEM Sites / AEM Forms</td>
   <td><p><code>/etc/cloudservices/typekit</code></p> <p><code>/etc/cloudservices/recaptcha</code></p> <p><code>/etc/cloudservices/echosign</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/typekit</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/recaptcha</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/echosign</code></p> </td>
   <td>租用戶感知</td>
   <td><p>舊式雲端服務。</p> <p>堅持就地升級。 AEM中仍會以備援方式顯示清單和閱讀的程式碼。</p> </td>
   <td>Forms Migration UI可觸發延遲內容移轉公用程式，以自動轉換為新路徑。<br /> </td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/cloudservices/fdm</code></td>
   <td><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/fdm</code></td>
   <td>租用戶感知</td>
   <td><p>舊式雲端服務。</p> <p>堅持就地升級設定。 AEM中仍會以備援方式顯示清單和閱讀的程式碼。</p> </td>
   <td>Forms Migration UI可觸發延遲內容移轉公用程式，以自動轉換為新路徑。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/adhocassetshare</code></td>
   <td><code>/libs/settings/dam/adhocassetshare</code></td>
   <td>租用戶感知</td>
   <td>舊式內容結構比新的OOTB結構更優先。</td>
   <td>專案層級自訂必須視需要剪下並貼入等 <code>/apps</code> 同或 <code>/conf</code> 路徑中。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
   <td><code>/libs/settings/dam/workflow</code></td>
   <td>租用戶感知</td>
   <td>舊式內容結構比新的OOTB結構更優先。</td>
   <td>專案層級自訂必須視需要剪下並貼入等 <code>/apps</code> 同或 <code>/conf</code> 路徑中。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/drm/licenses/</code></td>
   <td><code>/libs/settings/dam/drm</code></td>
   <td>不感知上下文</td>
   <td>舊式內容結構比新的OOTB結構更優先。</td>
   <td>專案層級自訂必須視需要剪下並貼入等 <code>/apps</code> 同或 <code>/conf</code> 路徑中。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/indesign/scripts</code></td>
   <td><code>/libs/settings/dam/indesign</code></td>
   <td>租用戶感知</td>
   <td>舊式內容結構比新的OOTB結構更優先。</td>
   <td><p>專案層級自訂需視需要剪下並貼在等 <code>/apps</code> 同或 <code>/conf</code> 路徑下。</p> <p>當執行自訂的「資產擷取」工作流程時，「媒體擷取程式設定」中仍會有/etc中舊位置的參考。 除了將指令碼從/etc移出到對等的/apps和/conf路徑外，還需要將自定義的「媒體抽取」進程參數從絕對路徑更改為相對路徑，以適應這些更改。</p> <p>如需詳細資訊，請參 <a href="https://helpx.adobe.com/experience-manager/6-2/help/assets/indesign.html">閱本頁</a>。</p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video</code></td>
   <td><code>/libs/settings/dam/video</code></td>
   <td>租用戶感知</td>
   <td>舊式內容結構比新式、現成可用的內容結構更優先。</td>
   <td>專案層級自訂必須視需要剪下並貼入等 <code>/apps</code> 同或 <code>/conf</code> 路徑中。</td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/notification/email/default</code></td>
   <td><code>/libs/settings/dam/notification</code></td>
   <td>租用戶感知</td>
   <td>舊式內容結構比新式、現成可用的內容結構更優先。</td>
   <td>專案層級自訂必須視需要剪下並貼入等 <code>/apps</code> 同或 <code>/conf</code> 路徑中。</td>
  </tr>
  <tr>
   <td>AEM Sites / AEM Assets</td>
   <td><code>/etc/designs</code> </td>
   <td><code>/libs/settings/wcm/designs</code></td>
   <td>不感知上下文</td>
   <td><p>消費服務會知道舊位置。</p> <p>從舊位置進行配置時將考慮</p> </td>
   <td><br /> 將自訂內容從移 <code>/etc/design</code> 動到 <code>/apps/settings/wcm/design</code> 新的儲存庫結構。 未來，請考慮將網站升級為使用可編輯的範本功能，以取代對設計模式的需求，進而取代此內容。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/scaffolding</code></td>
   <td><p><code>/libs/settings/wcm/template-types/scaffolding/scaffolding</code></p> <p><code>/apps/settings/wcm/template-types/scaffolding/scaffolding</code></p> </td>
   <td>不感知內容</td>
   <td>舊位置中的元件仍 <code>/etc/scaffolding</code> 將繼續運作，但已過時。</td>
   <td>Adobe建議您在新位置下使用新的Scaffold元件。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/blueprints</code></td>
   <td><p>/libs/msm開箱即用螢幕和商務藍圖設定</p> <p> </p> </td>
   <td>不感知上下文</td>
   <td><p>消費服務會知道舊位置。</p> <p>會考慮從舊位置進行的配置。</p> </td>
   <td>需要將配置複製到新位置。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/mobile</code></td>
   <td><code>/libs/settings/mobile</code></td>
   <td>租用戶感知</td>
   <td>該功能利用配置管理器，並仍支援舊位置作為備援。</td>
   <td>
    <ol>
     <li>將配置從重新定 <code>/etc</code> 位到 <code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li>然後，依下列方式更新內容中的參考：</li>
    </ol> <p><code>/content/&lt;tenant&gt;/jcr:content/cq:deviceGroups{String[]}=mobile/groups/responsive</code></p> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/msm/rolloutConfigs</code></td>
   <td><code>/libs/msm/wcm/rolloutconfigs</code></td>
   <td>N/A</td>
   <td><p>消費性服務會知道舊位置。</p> <p>如果在舊位置中檢測到配置，則將使用這些配置。</p> </td>
   <td>要與新模型對齊，需要在新位置中建立配置，而且必須刪除下面的 <code>/etc</code> 舊配置。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/segmentation/contexthub</code></td>
   <td><code>/conf/we-retail/settings/wcm/segments</code></td>
   <td>租用戶感知</td>
   <td><p>舊位置的區段：</p>
    <ul>
     <li>在觀眾主控台中保持唯讀模式。</li>
     <li>仍會載入頁面(如果在「頁面屬性&gt;個人化&gt;區段路 <strong>徑」中選取了指定路徑</strong>)。</li>
     <li>可用於內容定位。</li>
    </ul> </td>
   <td>您可以使用 <a href="/help/sites-deploying/upgrading-code-and-customizations.md#migrateconfigurations">區段移轉工具</a> ，移轉至新位置。</td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/social/config/languageOpts</code></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
   <td>N/A</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/templates</code></td>
   <td><code>/libs/settings/community/templates</code></td>
   <td> </td>
   <td><p>程式碼會感知舊範本的位置。 現有範本將繼續參考，並從中讀取／寫入 <code>/etc</code>。</p> <p><br /> 對於電子郵件範本，如果客戶已在 <strong>AEM Communities電子郵件回覆設定中設定</strong> Templates root <strong></strong> path，將自訂範本放在其他路徑上，則會維持原狀。</p> </td>
   <td><p>移 <a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration" target="_blank">轉公用程式</a> ，可與最新的AEM Communities範本模型對齊。</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/badging</code></td>
   <td><p><strong>徽章規則：</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>徽章影像：</strong></p> <p>將舊位置的出廠影像移 <code>/etc/community/badging/images</code> 至 <code>/libs/community/badging/images </code> </p> <p> </p> <p>自訂影像會移至 <code>/content/community/badging/images</code>。</p> <p> </p> </td>
   <td>租用戶感知</td>
   <td><p>程式碼會感知舊的標籤路徑。</p> <p><br /> 它會先檢查舊路徑是否存在<br /> 。 如果路徑不存在，則會使用新路徑。</p> </td>
   <td><p>需要手動遷移才能與最新型號一致。 請依照下列步驟進行，以達成此目標：</p>
    <ol>
     <li>使用「工具」下的設定瀏覽器建立網站內容儲 <strong>存貯體</strong></li>
     <li>前往網站根目錄</li>
     <li>將屬 <code>cq:conf</code> 性設定為要儲存所有配置的桶路徑。 您也可以透過網站編輯精靈——設 <strong>定雲端設定輸入</strong>，然後儲存變更</li>
     <li>將相關的標籤規則和計分規則從上 <code>etc/community/*</code> 一步驟中建立的網站內容區隔移至</li>
     <li>調整網 <code>badgingRules</code> 站根 <code>scoringRules</code> 目錄上的和屬性，以具有新規則位置的相對參照。 例如，如果設 <code>cq:conf</code> 為 <code>/conf/we-retail</code>，則規則現 <code>badgingRules</code> 在會移 <code>community/badging/rules</code> 至此新儲存貯體的值</li>
     <li>同樣地，調整標籤規則節點中對計分規則的引用，使其具有相對路徑。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/cloudservices/facebookconnect</code></p> <p><code>/etc/cloudservices/twitterconnect</code></p> <p><code>/etc/cloudservices/pinterestconnect</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> </td>
   <td>租用戶感知</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/scoring</code></td>
   <td><code>/libs/settings/community/scoring</code></td>
   <td> </td>
   <td><p>程式碼會感知舊的標籤路徑。</p> <p><br /> 它會先檢查舊路徑是否存在<br /> 。 如果路徑不存在，則會使用新路徑。</p> </td>
   <td><p>需要手動遷移步驟才能與最新型號一致。</p> <p>上述標籤規則中的步驟相同。</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/notifications</code></td>
   <td><code>/libs/settings/community/notifications</code></td>
   <td>不感知上下文</td>
   <td><p>這些配置不向後相容。 如需如何移轉至新位置的步驟，請參閱「與最新模型對齊的需求」欄。<br /> </p> <br /> </td>
   <td><p>需要手動遷移才能與最新型號一致。 可以使用Granite Configuration manager將配置移動到下的新路徑 <code>/apps/settings</code>。</p> <p>因此，您需要在節點上 <code>mergeList</code> 將屬性設為true, <code>/libs/settings/community/subscriptions</code> 然後添加子 <code>nt:unstructured</code> 節點。<br /> </p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/subscriptions</code></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
   <td>不感知上下文</td>
   <td>這些配置不向後相容。 如需如何移轉至新位置的步驟，請參閱「與最新模型對齊的需求」欄。</td>
   <td><p>需要手動遷移才能與最新型號一致。 可以使用Granite Configuration manager將配置移動到下的新路徑 <code>/apps/settings</code>。</p> <p>因此，您需要在節點上 <code>mergeList</code> 將屬性設為true, <code>/libs/settings/community/subscriptions</code> 然後添加子 <code>nt:unstructured</code> 節點。</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/socialconfig/srpc/defaultconfiguration</code></td>
   <td><code>/conf/global/settings/community/srpc/defaultconfiguration</code></td>
   <td>全域</td>
   <td>這些配置向後相容。 如果檢測到舊路徑，則將使用它們。 否則，新路徑優先。</td>
   <td><p>Lazy Content Migration Task（懶惰內容移轉任務）的形式為 <code>CQ64CommunitiesConfigsCleanupTask</code>。</p> <p>如需詳細資訊，請參閱「 <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">延遲移轉」檔案</a>。</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/watchwords</code></td>
   <td><code>/libs/community/watchwords</code></td>
   <td>N/A</td>
   <td>這些配置向後相容。 如果檢測到舊路徑，則將使用它們。 否則，新路徑優先。</td>
   <td><p>Lazy Content Migration Task（懶惰內容移轉任務）的形式為 <code>CQ64CommunitiesConfigsCleanupTask</code>。</p> <p>必須手動將關注字詞從移 <code>/etc/watchwords</code> 至 <code>/conf/global/settings/community/watchwords</code>。</p> </td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code> </p> <p><code>/var/workflow/models</code></p> </td>
   <td>全域</td>
   <td><p>如果存在，且或中不存在配置，則使用舊 <code>/libs</code> 位置 <code>/conf</code>。</p> <p>編輯OOTB工作流程模型時，必須在下方建立內容感 <code>/conf</code> 應覆蓋，才能加以修改。</p> <p>套件匯出需要在或中包含模 <code>/libs</code> 型， <code>/conf</code> 而執行時期模型在 <code>/var/workflow/models.</code></p> </td>
   <td><p>新建立的模型將建立在該位 <code>/conf/global/settings</code> 置。</p> <p>編輯之前， <code>/etc</code> 您 <code>/libs</code> 必須先在中明確建立覆寫， <code>/conf/global/settings</code> 或在中進行任何編輯。 必須選擇「編輯」按鈕，它將允許建立和編 <code>/conf</code> 輯中的覆蓋。</p> </td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/workflow/launcher</code></td>
   <td><p><code>/libs/settings/workflow/launcher</code></p> <p><code>/conf/global/settings/workflow/launcher</code></p> </td>
   <td>全域</td>
   <td>如果存在，且位置中不存在配置<br /> ，則使用 <code>/libs</code> 舊位 <code>/conf</code> 置。 如此，自訂啟動器就會保留。</td>
   <td><p>新建立或編輯的啟動程式配置位於該 <code>/conf</code> 位置。</p> <p>所有啟動器都應從舊位置移 <code>/etc</code> 至<code> /conf/global/settings/workflow/launcher.</code></p> </td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> </td>
   <td>全域</td>
   <td>如果存在，且位置中不存在配置<br /> ，則使用 <code>/libs</code> 舊位 <code>/conf</code> 置。 如此，自訂的工作流程模型就會保留下來。</td>
   <td><p>所有工作流程模型應從舊版位置移 <code>/etc</code> 至舊版 <code>/conf/global/settings/workflow/models</code>。</p> <p> </p> </td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/workflow/notification</code></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
   <td>不感知上下文</td>
   <td><p>為了向後相容，會使用舊版位置（若有）。</p> <p>以前，必須在中編輯現成的範本來覆寫範本 <code>/etc</code>。 現在，覆寫應儲存在 <code>/conf/global</code>。</p> </td>
   <td>如需詳細資訊，請參閱工作流程檔案。<br /> </td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/cloudservices/translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> <p> </p> </td>
   <td>租用戶感知</td>
   <td>舊式雲端服務。 將持續進行就地升級設定。 列出並閱讀的程式碼仍會顯示在產品中，做為備援。</td>
   <td><p>為了將雲配置移至 <code>/conf</code>，您可以：</p>
    <ul>
     <li>使用全新的Touch UI建立設定<br /> ，或<br /> </li>
     <li>將配置從 <code>/etc/cloudservices/translation</code> 各自的新位置複製</li>
    </ul> <p>完成此操作後，配置需要通過用戶介面中的「站點」 <strong>&gt;「屬性</strong> 」與「站點」關聯。</p> <p><em>注意：翻譯連接器必須與AEM 6.5相容，才能運作。</em></p> </td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/cloudservices/msft-translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/msft-translation</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/msft-translation</code></p> </td>
   <td>租用戶感知</td>
   <td>舊式雲端服務。 將持續進行就地升級設定。 列出並閱讀的程式碼仍會顯示在產品中，做為備援。</td>
   <td><p>為了將雲配置移至 <code>/conf</code>，您可以：</p>
    <ul>
     <li>使用全新的Touch UI建立設定，或<br /> </li>
     <li>將舊配置從 <code>/etc/cloudservices/translation</code> 各自的新位置複製</li>
    </ul> <p>完成此操作後，配置需要通過用戶介面中的「站點」 <strong>&gt;「屬性</strong> 」與「站點」關聯。</p> </td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/cloudsettings</code></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
   <td>租用戶感知</td>
   <td><p>升級實例 <code>/etc</code> 時，現有條目仍然有效。</p> <p>升級後存取雲端設定UI會將現有的雲端設定複製至新的儲存庫結構，同時保留現有內容以進行回溯相容性。</p> </td>
   <td><p>內容模型相同，只有位置已變更為與內容感知組態一致。</p> <p>涵蓋這 <a href="/help/sites-deploying/lazy-content-migration.md">些雲端設定的「延遲移轉</a> 」工作將執行下列動作：</p>
    <ul>
     <li>將現有的雲端設定複製 <code>/etc/cloudsettings</code> 至 <code>/conf/global/settings/cloudsettings</code></li>
     <li>移除 <code>/etc/cloudsettings</code></li>
    </ul> <p>但是，在升級後和執行延遲遷移任務之前，需要執行以下手動步驟：</p>
    <ul>
     <li>所有指向的參 <code>/etc/cloudsettings/*</code> 照都需要更新，以指向 <code>/conf/global</code></li>
    </ul> <p>警告：</p>
    <ul>
     <li>容 <code>/etc/cloudsettings</code> 器需要保留</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
   <td>僅全局</td>
   <td><p>動態媒體的雲端設定- Scene7(<code>dynamicmedia_scene7</code> 執行模式)設定將維持在相同位置。 此程式正如現狀般運作。 如果您需要調整雲端設定值，則有兩個選項可執行此動作：</p>
    <ol>
     <li>透過舊版雲端設定UI更新現有設定。</li>
     <li>透過新的Touch UI建立新的雲端設定。 這比舊的高。</li>
    </ol> </td>
   <td><p>為了與最新模型對齊，您需要執行位於：</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/viewer</code></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
   <td>僅全局</td>
   <td><p>OOTB檢視器預設集將只能在新位置使用，而自訂檢視器預設集仍在下方，直 <code>/etc</code> 到發生修改為止。</p> <p>修改後，將通過延遲遷移將其保存到新位置。 當內嵌影像伺服器收到請求時，會同時檢視舊有路徑和新路徑。 因此，您不需要變更其內嵌代碼或URL。</p> </td>
   <td><p>現成可用的檢視器預設集只能在新位置使用。 對於自訂檢視器預設集，您必須在此位置執行移轉指令碼：</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p>與向後相容性案例類似，您不需要調整copyURL/embed程式碼來指向 <code>/conf</code>。 要傳送的現 <code>/etc</code> 有請求將重新路由至引擎蓋下，以取得正確的內容 <code>/conf</code>。</p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/imageserver/macros</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
   <td>僅全局</td>
   <td>下面的宏 <code>/etc</code> 仍然有效。 如果修改該節點，則修改的節點將通過「延遲遷移」任 <code>/conf</code> 務移動到新位置。</td>
   <td><p>您需要在此位置運行遷移指令碼：</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia/Adaptive Video Encoding</code></td>
   <td><code>/libs/settings/dam/dm/presets/video/jcr:content/Adaptive Video Encoding</code></td>
   <td>N/A</td>
   <td><p>立即可用的視訊描述檔將會移除，而不會更新資產資料夾屬性以連結至描述檔。</p> <p>編碼程式已在新舊位置之間內建翻譯。 它會轉換舊路徑，以查看新的描述檔路徑。</p> </td>
   <td>不需要變更。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
   <td>僅全局</td>
   <td><p>自訂視訊描述檔會依原樣保留，直到您修改為止。</p> <p>然後，它將通過延遲遷移任務移動到新位置。 這類似於編碼查閱的現成視訊預設集。 編碼程式具有內建路徑轉換器，可先查看舊位置，再查看視訊描述檔的新位置。</p> </td>
   <td><p>為了與最新模型對齊，您可在以下位置運行遷移指令碼：</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
   <td>僅全局</td>
   <td><p>動態媒體混合設定(<code>dynamicmedia</code> runmode)的雲端設定將維持在相同位置。 此程式按原樣運作。 如果您需要調整設定值，可以透過兩種方式進行。</p>
    <ol>
     <li>透過舊版雲端設定UI更新現有設定。</li>
     <li>透過新的觸控UI建立新的雲端設定。 這比舊的高。</li>
    </ol> </td>
   <td><p>您需要執行移轉指令碼，才能與最新的模型對齊。 您可以在以下位置找到指令碼：<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/youtube</code></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
   <td>僅全局</td>
   <td><p>DM-Youtube設定的雲端設定將維持在相同位置。 此程式按原樣運作。 如果您需要調整雲端設定值，可以透過兩種方式進行：</p>
    <ol>
     <li>透過舊版雲端設定UI更新現有設定。</li>
     <li>透過新的觸控UI建立新的雲端設定。 這比舊的高。</li>
    </ol> </td>
   <td><p>您可以執行移轉指令碼，以符合最新的模型。 此位置可找到該指令碼：<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/analytics</code></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
   <td>僅全局</td>
   <td>不需執行任何動作。</td>
   <td><p>您可以執行移轉指令碼，以與最新模式對齊。 此位置可找到該指令碼：<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td>全部</td>
   <td><p><code>/etc/notification/email/default/com.day.cq.replication</code></p> <p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
   <td><code>/libs/settings/notification-templates</code></td>
   <td>僅全局</td>
   <td>中的模 <code>/etc/notification/email/default/</code> 板優先於中的模板 <code>/libs/settings/notification-templates</code>。</td>
   <td>為了與最新模型對齊，您可以在下面建立新範本，並 <code>/apps/settings/notification-templates</code> 在此處執行新修改。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/msm/rolloutconfigs/launch</code></p> <p><code>/etc/msm/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td><p><code>/libs/msm/launches/rolloutconfigs/launch</code></p> <p><code>/libs/msm/launches/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td>N/A</td>
   <td><p>消費服務會知道舊位置。</p> <p>如果在舊位置中檢測到配置，則將使用這些配置。</p> </td>
   <td>要與新模型對齊，需要在新位置中建立配置，而且必須刪除下面的 <code>/etc</code> 舊配置。</td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/translation/supportedLanguages</code></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
   <td>不感知上下文</td>
   <td>但需注意的是，自訂語言必須新增至清單。<br /> </td>
   <td>以其他語言（如果有）覆蓋並更新新清單。 或者，將舊清單複製到位 <code>/apps</code> 置也可以。</td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
   <td>僅全局</td>
   <td>將會持續使用就地升級設定。 請撰寫程式碼，列出並閱讀產品中仍然存在的程式碼。</td>
   <td>要保存更改，請將XML檔案從復 <code>/etc</code> 制到 <code>/libs</code> 或 <code>/conf</code>。 或者，<strong> 從 </strong>中刪除檔案 <code>/etc</code>。</td>
  </tr>
 </tbody>
</table>

## 用戶端資源庫 {#client-side-libraries}

[用戶端程式庫](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/clientlibs.html) ，是在瀏覽器中處理的Javascript和CSS程式碼。

### 擴充性策略 {#extensibility-strategy-1}

AEM提供擴充性架構，可附加多個JavaScript檔案。 任何具有相同「類別」屬性的檔案都會附加，允許自訂代碼擴充位於下方的AEM代碼 `/libs`。

<table>
 <tbody>
  <tr>
   <td><strong>解決方案</strong></td>
   <td><strong>上一個位置</strong><br /> </td>
   <td><strong>新位置</strong></td>
   <td><strong>向後相容性方法</strong></td>
   <td><strong>符合最新機型的需求</strong></td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/fp</code></td>
   <td><code>/libs/fd/fp/components</code></td>
   <td><p>舊版clientlib，將持續存在已透過就地升級升級的例項上。</p> <p>新客戶端lib與"<strong><code>replaces</code></strong>"屬性具有相同的類別名稱，以避免合併舊客戶端lib和新客戶端lib。</p> </td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/rte</code></td>
   <td><code>/libs/fd/rte</code></td>
   <td><p>舊版clientlibs，將持續存在已透過就地升級升級的例項上。</p> <p>新客戶端lib與"<strong><code>replaces</code></strong>"屬性具有相同的類別名稱，以避免合併舊客戶端lib和新客戶端lib。</p> </td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/af</code></td>
   <td><code>/libs/fd/af/authoring/clientlibs</code></td>
   <td>舊版clientlibs。 將持續存在已通過就地升級升級的實例上。 新客戶端lib與"<strong><code>replaces</code></strong>"屬性具有相同的類別名稱，以避免合併舊客戶端lib和新客戶端lib。</td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/themes/themeLibrary</code></td>
   <td>這不再是AEM 6.5現成可用套件的一部分。</td>
   <td><p>最適化表單中立即可用的主題。</p> <p>將會持續使用就地升級設定。</p> </td>
   <td>這部分是使用者產生的內容。 這將以名稱的參考內容套件形式傳 <code>aem-forms-reference-themes</code> 送。</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/expeditor</code></td>
   <td><code>/libs/fd/expeditor/clientlibs</code></td>
   <td>舊版clientlibs。 將持續存在已通過就地升級升級的實例上。 新客戶端lib與"<strong><code>replaces</code></strong>"屬性具有相同的類別名稱，以避免合併舊客戶端lib和新客戶端lib。</td>
   <td>不需執行任何動作。<p> </p> </td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/fmaddon</code></td>
   <td><code>/libs/fd/fmaddon</code></td>
   <td>不打算直接使用的舊版Analytics和Target客戶端。 </td>
   <td>已使用清除篩選器清除升級後的問題。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
   <td><code>/libs/dam/clientlibs</code></td>
   <td>舊版clientlibs有不同的用戶端類別名稱。</td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td> </td>
   <td><code>/etc/clientlibs/ckeditor</code></td>
   <td><code>/libs/clientlibs/ckeditor</code></td>
   <td>這些是舊版clientlibs。 他們將持續使用一個就地升級設定。 新客戶端lib與"<code>replaces</code>"屬性具有相同的類別名稱，以避免新舊客戶端lib的合併。</td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/sitecatalyst</code></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
   <td><p>這些是舊版clientlibs。 將會持續使用就地升級設定。</p> <p>新的clientlib具有相同的類別名稱。</p> </td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/personalization</code></td>
   <td><code>/libs/cq/personalization/clientlibs/personalization</code></td>
   <td><p>這些是舊版clientlibs。 將會持續使用就地升級設定。</p> <p>新的clientlib具有相同的類別名稱。</p> </td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/searchpromote</code></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
   <td><p>這些是舊版clientlibs。 將會持續使用就地升級設定。</p> <p>新客戶端庫的類別名稱相同</p> </td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/target</code></td>
   <td><code>/libs/cq/target/clientlibs/target</code></td>
   <td><p>這些是舊版clientlibs。 將會持續使用就地升級設定。</p> <p>新的clientlib具有相同的類別名稱。</p> </td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/address</code></td>
   <td><code>/libs/cq/address/clientlibs</code></td>
   <td>新的clientlib具有相同的類別名稱。</td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation</code></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
   <td>舊版clientlibs。 將會持續使用就地升級設定。 新clientlib與"replaces"屬性具有相同的類<strong>別名稱</strong>，以避免合併舊客戶端和新客戶端lib。</td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
   <td><p><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></p> </td>
   <td><p>在就地升級時，舊版檔案(/etc/clientlibs/wcm/..._)將會保留且不會自動移除，因此對舊版/etc/clientlibs/wcm/foundation/grid/grid_base.less的參考將會繼續保留。</p> <p><em>請注意，此為異常情況，此LESS檔案通過LESS @import語句由絕對路徑引用，而NOT由clientlib類別引用。</em></p> <p>如果引用「grid_base.less」的客戶LESS指向非現有檔案，則「可編輯模板佈局」模式將中斷，並且不會顯示使用其進行的任何調整（即）。 所有元件將為頁面的全寬)。</p> </td>
   <td>更新自訂程式碼中的任何參照（例如，在任何參照已移動grid_base.less檔案的LESS檔案中），以指向新位置，並移除舊位置。</td>
  </tr>
 </tbody>
</table>

這些是前幾章所沒有涉及的其它重組。

### 擴充性策略 {#extensibility-strategy-2}

請參閱每個表格列，以取得任何支援的擴充性模型。 本節中的內容通常不會延伸。

## 其他 {#miscellaneous}

<table>
 <tbody>
  <tr>
   <td><strong>解決方案</strong></td>
   <td><strong>上一個位置</strong><br /> </td>
   <td><strong>新位置</strong></td>
   <td><strong>向後相容性方法</strong></td>
   <td><strong>符合最新機型的需求</strong></td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/designs/fd/fp</code></td>
   <td><code>/libs/fd/fp</code></td>
   <td><p>舊版AEM Forms Portal OOTB範本。 在就地升級後，這些範本將保留在/etc中。</p> <p>在範本清單中，將會在範本標題中新增<em> "deprecated</em>"，以區分這些字詞與較新範本。</p> </td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/aep</code></td>
   <td><code>/var/fd/content/annotations</code></td>
   <td>舊式對應管理注釋檔案。 不是直接消費的。 將在升級後使用清除篩選器進行清除。</td>
   <td>舊版位置已使用清除篩選器清理升級後的位置。</td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/tags</code></td>
   <td><code>/content/cq:tags</code></td>
   <td>標籤管理器API支援舊版和新位置。 當JCR Tag Manager Factory OSGi元件啟動時，它會檢測它是否在升級實例或舊實例上運行，並使用適當的位置。<br /> </td>
   <td><p>為了與新模型正確對齊：</p>
    <ol>
     <li>使用<code>/etc/tags</code><code>/content/cq:tags</code> <code>tagID.</code></li>
     <li>登入CRXDE Lite</li>
     <li>將標籤從移 <code>/etc/tags</code> 至 <code>/content/cq:tags</code></li>
     <li>重新啟動OSGi元件 <code class="code">com.day.cq.tagging.impl.JcrTagManagerFactoryImpl.
        </code></li>
    </ol> <p> </p> </td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>處理飛行中工作流程時<br /> ，使用的舊版位置。 新的工作流程使用 <code>/var.</code></td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/workflow/scripts</code></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
   <td><p>現有工作流模型參考舊位置的工作流指令碼的步驟 <code>/etc/workflow/scripts</code> 在升級後將繼續指向這些指令碼，並正確執行。</p> <p>請注意AEM UI，以製作工作流程步驟』（「處理」、「分割」等）不再列出用於工 <code>/etc/workflow/scripts</code> 作流指令碼的下拉清單中的指令碼。</p> </td>
   <td><p>如果AEM中未編輯關聯的工作流程程式步驟，則運用這些指令碼的工作流程將繼續如預期般運作。</p> <p>但是，為了完全向後相容，包括編輯步驟時，需要客戶在升級後採取手動操作：</p>
    <ul>
     <li>指令碼必須從移 <code>/etc/workflow/scripts</code> 至 <code>/apps/workflow/scripts.</code></li>
     <li>必<strong> 須更新 </strong>工作流模型步驟中的任何參照，以引用新 <code>/etc/workflow/scripts</code><code>/apps/workflow/scripts</code> 位置。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/replication/treeactivation</code></td>
   <td><code>/libs/replication/treeactivation</code></td>
   <td>升級時，ClassicUI實用程式頁面仍保持不變。</td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/jobs</code></td>
   <td><code>/var/dam/jobs</code></td>
   <td><p>暫存位置，以儲存為AEM Assets下載動作呼叫產生的zip檔案。</p> <p>不需要更新，因為當用戶端要求下載資產時，它會在新位置產生檔案。</p> </td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/products</code></td>
   <td><code>/var/commerce/products</code></td>
   <td><p>舊內容在升級後仍可使用。</p> <p>Lazy Migration任務被提供用於遷移到新位置。</p> </td>
   <td><p>遷移通過「延遲遷移」任務執行： <code>CQ64CommerceMigrationTask.</code></p> <p>它執行以下步驟：</p>
    <ul>
     <li>調整從舊位置到指向新位置的參照</li>
     <li>將內容從舊位置移至新位置</li>
     <li><p>移除舊位置，最終激活整個系統中新位置的使用</p> </li>
    </ul> <p>任務涵蓋的位置包括：</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>若是較大的型錄，建議將下列Java系統屬性傳遞至AEM，以個別執行商務移轉工作：</p>
    <ul>
     <li>屬性名稱: <code>com.adobe.upgrade.forcemigration</code></li>
     <li>屬性值: <code>com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></li>
    </ul> <p>移轉後，AEM需要重新啟動。</p> </td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/orders</code></td>
   <td><code>/var/commerce/orders</code></td>
   <td><p>舊內容在升級後仍可使用。</p> <p>Lazy Migration任務被提供用於遷移到新位置。</p> </td>
   <td>請參閱上述說明 <code>/etc/commerce/products</code>。</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/collections</code></td>
   <td><code>/var/commerce/collections</code></td>
   <td><p>舊內容在升級後仍可使用。</p> <p>Lazy Migration任務被提供用於遷移到新位置。</p> </td>
   <td>請參閱上述說明 <code>/etc/commerce/products</code>。</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/classifications</code></td>
   <td><code>/var/commerce/classifications</code></td>
   <td>不需執行任何動作。</td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/shipping-methods</code></td>
   <td><code>/var/commerce/shipping-methods</code></td>
   <td><p>舊內容在升級後仍可使用。</p> <p>Lazy Migration任務被提供用於遷移到新位置。</p> </td>
   <td>請參閱上述說明 <code>/etc/commerce/products</code>。</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/payment-methods</code></td>
   <td><code>/var/commerce/payment-methods</code></td>
   <td><p>舊內容在升級後仍可使用。</p> <p>Lazy Migration任務被提供用於遷移到新位置。</p> </td>
   <td>請參閱上述說明 <code>/etc/commerce/products</code>。</td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/taskmanagement</code></td>
   <td><code>/var/taskmanagement</code></td>
   <td><p>新任務在 <code>/var/taskmanagement</code></p> <p>舊位置中的現有工作仍會顯示在AEM收件匣中。</p> </td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/workflow/packages</code></td>
   <td><code>/var/workflow/packages</code></td>
   <td><p>透過AEM Package manager建立的AEM套件仍儲存在 <code>/etc/workflow/packages.</code></p> <p>透過AEM Sites和Workflows建立的其他套件會持續儲存在<code>/var/workflow/packages.</code></p> <p>在兩者中找到 <code>/etc/workflow/packages</code> 的套 <code>/var/workflow/packages</code> 件，仍可透過AEM的Package Manager編輯。 </p> </td>
   <td><p>不需執行任何動作。</p> <p> </p> </td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>新的工作流程例項會自動建立在 <code>/var</code> 下。</td>
   <td>不需執行任何動作。</td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/commerce/searchpromote</code></td>
   <td><code>/var/cq/searchpromote</code></td>
   <td><p>搜尋和促銷動態消息內容的新位置。</p> <p>舊URL仍繼續運作，ServletFilter會將請求轉送至新位置。</p> </td>
   <td><br /> 不需執行任何動作。 <br /> </td>
  </tr>
  <tr>
   <td>全部</td>
   <td><code>/etc/dtm-hook</code></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
   <td><p>DTM Web-Hook的新位置。</p> <p>舊URL仍繼續運作，ServletFilter會將請求轉送至新位置。</p> </td>
   <td><br /> 不需執行任何動作。 <br /> </td>
  </tr>
 </tbody>
</table>

