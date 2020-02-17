---
title: 已過時和已移除的功能
description: Adobe Experience Manager 6.5中已過時和已移除功能的發行說明。
uuid: 81d9a064-e712-4eff-bd3b-6e15513a5435
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: e8e2e01b-0117-48c3-86d8-609d29a147be
docset: aem65
translation-type: tm+mt
source-git-commit: 471b57a52efc849eb57201e6397221fa4f88c746

---


# 已過時和已移除的功能 {#deprecated-and-removed-features}

Adobe會持續評估產品功能，以更現代的替代方式來革新或取代舊功能，以改善整體客戶價值，並時時考慮回溯相容性。

若要傳達即將移除／取代AEM功能，請套用下列規則：

1. 首先宣佈放棄。 雖然已過時，但功能仍可用，但無法進一步增強。
1. 在下列主要版本中，將最早移除已過時的功能。 將公佈實際的移除目標日期。

此程式可讓客戶在實際移除之前，至少有一個發行週期，以調整其實作方式，以適應已過時功能的新版本或後繼版本。

## 不建議使用的功能 {#deprecated-features}

本節列出已標示為不再提倡的AEM 6.5功能。通常，計畫在未來版本中移除的功能會先設為不建議使用，並提供其他選項。

建議客戶在目前的部署中是否運用了功能／功能，並規劃變更實施以使用提供的替代方案。

<table>
 <tbody>
  <tr>
   <td><b>區域</b></td>
   <td><b>功能</b></td>
   <td><b>取代</b></td>
  </tr>
  <tr>
   <td>Creative cloud整合</td>
   <td><p><a href="/help/assets/aem-cc-folder-sharing-best-practices.md">AEM to Creative Cloud Folder Sharing</a> is in AEM 6.2 as as as save give creative users access of AEM, so they thay bey open the CC applications and upload new files or save changes to AEM. Creative cloud應用程式中發行的新功能Adobe Asset Link提供更佳的使用者體驗，並可直接從Photoshop、InDesign和Illustrator內部，以更強大的方式存取AEM中的資產。</p> <p>Adobe不打算對AEM做進一步的增強，以整合Creative cloud資料夾共用。 雖然AEM中包含此功能，但強烈建議客戶使用取代解決方案。</p> </td>
   <td>建議客戶改用新的Creative cloud整合功能，包括Adobe Asset Link或AEM案頭應用程式。 請參閱 <a href="/help/assets/aem-cc-integration-best-practices.md">AEM和Creative cloud整合最佳實務</a> ，以取得詳細資訊。</td>
  </tr>
  <tr>
   <td>資產</td>
   <td>
    <ol>
     <li>AssetDownloadServlet預設會停用發佈例項。 如需詳細資訊，請參 <a href="/help/sites-administering/security-checklist.md">閱AEM安全性檢查清單</a>。</li>
     <li>如果使用者對/content/dam/collections沒有足夠的（讀取和寫入）權限，則使用者無法建立系列。</li>
    </ol> </td>
   <td>
    <ol>
     <li>AEM安全性檢查清 <a href="/help/sites-administering/security-checklist.md">單中說明的設定</a>。</li>
     <li>遵循使用者的存取控制設定，並確保適當的權限。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Adobe Search &amp; Promote</td>
   <td><p>不再提倡與Adobe Search &amp; Promote的整合。</p> <p>Adobe不打算對「搜尋與促銷」整合做進一步的增強。 請注意，Search &amp; Promote整合仍完全受支援，但不建議使用。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>DTM標籤管理器</td>
   <td>不再支援與DTM（動態標籤管理器）的整合。</td>
   <td>改用Adobe Experience Platform Launch做為標籤管理程式</td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>在AEM 6.5中新增AEM使用Adobe I/O架構的Adobe Target Standard API(Rest API)連線至Adobe Target服務的功能，Target Classic API(XML)方式已過時。</td>
   <td><a href="https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html">重新設定整合，以使用新的API</a></td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>不建議在AEM中使用與Adobe target的mbox.js整合。</td>
   <td>切換為使用at.js 1.x</td>
  </tr>
  <tr>
   <td>商務</td>
   <td><p><a href="https://github.com/adobe/commerce-cif-api" target="_blank">CIF REST</a> 於2018年提供為一套微型服務，以整合AEM和商務引擎。</p> <p>Adobe在2018年年中收購Magento後，決定改變其方式，原因有二： </p> <p><strong>1.</strong> Magento有自己的一組商務API（REST和GraphQL），維護兩組API並不好 </p> <p><strong>2.</strong> 市場趨勢表明，客戶正在向GraphQL靠攏，因為GraphQL是一種更高效的資料查詢方式。 在2019年，Adobe已推出新的商務整合架構，使用Magento的GraphQL API作為真相來源。</p> <p>Adobe並不打算進一步投資CIF REST。 強烈建議客戶使用更換解決方案。</p> </td>
   <td><p>針對AEM-Magento整合，請切換至 <a href="https://github.com/adobe/aem-cif-project-archetype" target="_blank">AEM CIF Archetype</a>和 <a href="https://github.com/adobe/aem-core-cif-components" target="_blank">AEM CIF Core Components</a></p> <p>請參閱「使用商 <a href="https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md" target="_blank">務整合架構進行AEM和Magento整合」</a> ，以取得詳細資訊。</p> <p>我們的規劃藍圖中已列出支援協力廠商（Magento除外）與新方法整合的功能。</p> </td>
  </tr>
  <tr>
   <td>元件(AEM Sites)</td>
   <td><p>Adobe不打算對儲存在/libs/foundation/components中的大部分Foundation Components進行進一步的增強。</p> <p>在元件資 <strong>料夾中尋找cq:deprecated</strong> 和 <strong>cq:deprecatedReason</strong> 屬性。</p> <p>AEM 6.5包含Foundation Components，而從舊版升級的客戶可依現狀繼續使用這些元件。 此外，Foundation Components仍完全受支援，但已過時。 </p> </td>
   <td>建議客戶將核心元件用於未來的專案。 現有網站可維持原狀，或使用 <a href="https://github.com/adobe/aem-modernize-tools">AEM Modestance Tools Suite</a> ，重新調整網站以使用核心元件。</td>
  </tr>
  <tr>
   <td>元件(AEM Sites)</td>
   <td>Design Importer元件/libs/wcm/designimporter/components已標示為自6.5起已過時。Adobe不打算對該設計匯入工具的實作進行進一步的增強。</td>
   <td>Adobe計畫在未來版本中提供此使用案例的替代實作。</td>
  </tr>
  <tr>
   <td>元件(AEM Forms)</td>
   <td><p>簽名步驟可讓使用者驗證並簽署最適化表單。 在舊版中，簽名步驟可以同時使用Adobe Sign和Scribble Signature元件做為簽名欄位。 在AEM 6.5 Forms中，「簽名步驟」的「Scribble Signature」（草簽簽名）簽署體驗已過時。</p> </td>
   <td>
    <ul>
     <li>如果您已執行新安裝：
      <ul>
       <li>在最適化表單的「簽名」步驟中使用Adobe Sign型簽署體驗。</li>
       <li>在最適化表單、互動式通訊和HTML5表單中使用獨立的Scribble Signature元件。</li>
      </ul> </li>
     <li>如果您已從舊版升級至AEM 6.5 Forms:<br />
      <ul>
       <li>在已使用此功能的表單中，繼續使用「簽名步驟」的Scribble簽名簽署體驗。<br /> </li>
       <li>當您建立新表格時，請在「簽名」步驟中使用獨立的Scribble Signature元件或以Adobe Sign為基礎的簽署體驗。 </li>
      </ul> </li>
    </ul> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>基礎</td>
   <td><p>Granite卸載框架</p> <p>Adobe不打算對5.6.1中引進的卸載架構做進一步的增強，以將資產處理外部化。 </p> </td>
   <td>Adobe正在研發新一代雲端原生卸載架構。</td>
  </tr>
  <tr>
   <td>開發人員</td>
   <td><p>Hobbes.js</p> <p>Adobe不打算對hobbes.js使用者介面測試架構做進一步的增強。</p> </td>
   <td>Adobe建議客戶使用Selenium自動化。</td>
  </tr>
  <tr>
   <td>開發人員</td>
   <td><p>jQuery UI用戶端程式庫</p> <p>Adobe不打算進一步維護和更新發佈時隨附的jQuery UI用戶端程式庫（快速入門）</p> </td>
   <td>Adobe建議仍需要jQuery UI才能使用其程式碼的客戶，將其新增至專案程式碼庫。</td>
  </tr>
  <tr>
   <td>開發人員</td>
   <td><p>jQuery Animation用戶端程式庫(granite.jquery.animation)</p> <p>Adobe不打算進一步維護和更新作為分發一部分而出貨的jQuery Animation用戶端程式庫(Quickstart)</p> </td>
   <td>Adobe建議仍需jQuery Animations才能使用其程式碼的客戶，將其新增至專案程式碼庫。</td>
  </tr>
  <tr>
   <td>開發人員</td>
   <td><p>Handlebars用戶端程式庫</p> <p>Adobe不打算進一步維護和更新Handlebar用戶端程式庫，此程式庫是做為散發的一部份(Quickstart)</p> </td>
   <td>Adobe建議仍需要Handlebars代碼的客戶，將其加入專案代碼庫。</td>
  </tr>
  <tr>
   <td>開發人員</td>
   <td><p>Lawnchair用戶端資料庫</p> <p>Adobe不打算進一步維護和更新Lawnshair用戶端程式庫(Quickstart)，此程式庫會隨散發一起運送</p> </td>
   <td>Adobe建議仍需Lawnchair才能使用程式碼的客戶，將其新增至專案程式碼庫。</td>
  </tr>
  <tr>
   <td>開發人員</td>
   <td><p>Granite.Sling.js用戶端程式庫</p> <p>Adobe不打算進一步增強Granite.Sling.js用戶端程式庫，此程式庫會隨散發(Quickstart)一起出貨</p> </td>
   <td>Adobe建議依賴程式庫功能的客戶重新調整其程式碼，以便不再使用。</td>
  </tr>
  <tr>
   <td>開發人員</td>
   <td>使用UI來壓縮／精簡JavaScript用戶端程式庫。 Adobe不打算進一步更新UYI程式庫。 在AEM 6.4之前，UYI預設為使用切換至Google Closure Compiler(GCC)的選項來精簡JavaScript。 從AEM 6.5開始，GCC為預設值。</td>
   <td>Adobe建議升級至AEM 6.5的客戶切換至GCC以進行實作</td>
  </tr>
  <tr>
   <td>開發人員</td>
   <td><p>CRXDE lite中的傳統UI對話框編輯器</p> <p>Adobe不打算進一步增強散發時隨附的Classic UI Dialog Editor（快速入門）</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 已移除功能 {#removed-features}

本節列出已從AEM 6.5移除的功能。舊版的這些功能已標示為已過時。

| 區域 | 功能 | 取代 |
|--- |--- |--- |
| Analytics Activity Map | AEM中包含的Activity Map版本。 | 由於Adobe Analytics API中的安全性變更，無法再使用AEM中包含的Activity Map版本。 使用Adobe [Analytics提供的ActivityMap外掛程式](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)。 |
| 整合 | ExactTarget整合已從預設分發（快速入門）中移除，現已不再提供。 | 無取代 |
| 整合 | Salesforce Force API整合已從預設散發(Quickstart)中移除，現在是要從PackageShare安裝的額外套件。 | 功能仍然可用。 |
| 表單 | Adobe Central Migration bridge服務的支援已移除，因為不再支援Adobe Central產品。 | 無取代 |
| 表單 | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 無取代 |
| 表單 | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 無取代 |
| 開發人員 | Firebug Lite已從預設散發中移除（快速入門） | 使用瀏覽器內建的開發人員主控台 |
| 開發人員 | 移除 `customJavaScriptPath` HTML用戶端程式庫管理員的支援。 | 無取代 |
| 資產 | AEM 6.5中已移除「資產」卸載功能 | 無取代 |
| 快取 | `system/console/slingjsp` is removed is nore available in AEM 6.5. | Classes and Lightly cache會儲存在Apache Sling Commons FileSystem ClassLoader套件下。 您可以在AEM Web Console中檢查套件編號，並直接從檔案系統(`crx-quickstart/launchpad/felix/bundle<ID>`)移除快取檔案夾。 |

## 下一版產品的預發佈 {#pre-announcement-for-next-release}

本節用於在未來版本中預先發佈變更，這些變更不會過時，但會影響客戶。 這些是為規劃目的而提供的。

| 區域 | 功能 | 公告 |
|--- |--- |--- |
| 基礎 | UI架構 | Adobe計畫在2019年淘汰Coral UI 2元件。 AEM 6.2已推出Coral UI 3，而AEM 6.5則完全以Coral 3為基礎。 Adobe建議已使用Coral 2建立自訂UI的客戶和合作夥伴，將它們重新分解至Coral 3。 Adobe提供工具，將Coral 2對話方塊轉換為Coral 3 —— 閱 [讀更多](/help/sites-developing/dialog-conversion.md)。 |
