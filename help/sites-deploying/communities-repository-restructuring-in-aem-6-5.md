---
title: 6.4中的AEM Communities存放庫重新調整
seo-title: Repository Restructuring for AEM Communities in 6.4
description: 了解如何進行必要的變更，以移轉至AEM 6.4 for Communities的新存放庫結構。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.4 for Communities.
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
feature: Upgrading
exl-id: 4d2bdd45-a29a-4936-b8da-f7e011d81e83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 3%

---

# AEM Communities 6.5的存放庫重新調整架構 {#repository-restructuring-for-aem-communities-in}

如父項所述 [AEM 6.4中的存放庫重新調整架構](/help/sites-deploying/repository-restructuring.md) 頁面中，升級至AEM 6.5的客戶應使用此頁面評估與影響AEM Communities解決方案的存放庫變更相關的工作量。 有些變更需要AEM 6.5升級程式中的工作量，而有些變更可能會延遲至日後升級。

**使用6.5升級**

* [電子郵件通知模板](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [訂閱設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**未來升級前**

* [標籤配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [傳統Communities主控台設計](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Facebook Social登入設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [語言選項配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Pinterest Social登入設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [計分設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Twitter Social登入設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [雜項](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## 使用6.5升級 {#with-upgrade}

### 電子郵件通知模板 {#e-mail-notification-templates}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>如果您想要移至「 」下的新路徑，則需要手動移轉。<code>/apps/settings</code>」。 您可以使用Granite Configuration Manager執行移轉。</p> <p>您可以設定屬性以執行移轉 <code>mergeList</code> to <code>true</code> 在「<code>/libs/settings/community/subscriptions</code>"節點並新增 <code>nt:unstructured</code> 子節點。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 訂閱設定 {#subscription-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>如果您想要移至「 」下的新路徑，則需要手動移轉。<code>/apps/settings</code>」。 您可以使用Granite Configuration Manager執行移轉。</p> <p>您可以設定屬性以執行移轉 <code>mergeList</code> to <code>true</code> 在「<code>/libs/settings/community/subscriptions</code>"節點並新增 <code>nt:unstructured</code> 子節點。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 觀看詞設定 {#watchwords-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td>/etc/watchwords</td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td>/libs/community/watchwords</td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td>延遲遷移任務可用於清除社區配置。<br /> <p>「任務」會將關注字詞從 <code>/etc/watchwords</code> to <code>/conf/global/settings/community/watchwords</code>.</p> <p>如果自訂的口令儲存在SCM中，則應將其部署至 <code>/apps/settings/...</code> 你必須確保沒有覆蓋 <code>/conf/global/settings/...</code> 優先的設定。</p> <p>遷移任務刪除 <code>/etc</code> 位置。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

## 未來升級前 {#prior-to-upgrade}

### 標籤配置 {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><strong>徽章規則：</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>徽章影像：</strong></p> <p>預設影像： <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>自訂影像： <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>需要手動遷移。</p> <p>如果您的例項已自訂徽章/計分規則，則沒有自動方式將所有規則放在貯體下。 需要客戶輸入，以便用於您網站的會議貯體（全域或網站特定）。</p> <p>沒有可用於配置網站徽章和評分的UI。</p> <p>要與新的儲存庫結構一致：</p>
    <ol>
     <li>使用建立網站內容貯體 <strong>配置瀏覽器</strong> 在 <strong>工具</strong></li>
     <li>前往網站根目錄</li>
     <li>設定 <code>cq:confproperty</code> 儲存所有設定的貯體路徑。 也可透過網站設定 <strong>編輯嚮導 — 設定雲配置輸入</strong>.</li>
     <li>將相關簽名規則和評分規則從 <code>/etc/community/*</code> 至上一步驟中建立的網站內容貯體。</li>
     <li>調整網站根目錄上的標籤規則和計分規則屬性，以具有新規則位置的相對參照。
      <ol>
       <li>例如，如果 <code>cq:conf = /conf/we-retail</code>，然後 <code>badgingRules [] = community/badging/rules</code> 如果規則現在已移至此新貯體。</li>
      </ol> </li>
     <li>同樣，調整標籤規則節點中對計分規則的引用，使其具有相對路徑。</li>
    </ol> <p> </p> <p>最後，移除資源以清理 <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 傳統Communities主控台設計 {#classic-communities-console-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/social/console</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/social/console</code></p> <p><code>/apps/settings/wcm/designs/social/console</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Facebook Social登入設定 {#facebook-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudservices/facebookconnect</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/facebookconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的Facebook雲端設定都必須移轉至新位置。</p>
    <ol>
     <li>將「上一位置」中的現有配置遷移到「新位置」。
      <ol>
       <li>透過AEM編寫UI，手動重新建立新的Facebook Social登入設定，位於 <strong>工具&gt;Cloud Services&gt; Facebook Social登入設定</strong>.<br /> 或 <br /> </li>
       <li>將任何新的Facebook雲端設定從先前位置複製到適當的新位置，位於 <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>更新任何AEM Communities網站根目錄，以參考新的Facebook Social登入設定，方法是設定 <code>[cq:Page]/jcr:content@cq:conf</code> 屬性到「新位置」中的絕對路徑。</li>
     <li>將舊版Facebook ConnectCloud Service與任何更新為參考新位置的AEM Communities網站根取消關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 語言選項配置 {#language-options-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/social/config/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td>N/A<br /> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Pinterest Social登入設定 {#pinterest-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudservices/pinterestconnect</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/pinterestconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的Pinterest雲端設定都必須移轉至新位置。</p>
    <ol>
     <li>將「上一位置」中的現有配置遷移到「新位置」。
      <ol>
       <li>透過AEM編寫UI，手動重新建立新的Pinterest Social登入設定，位於 <strong>工具&gt;Cloud Services&gt; Pinterest Social登入設定</strong>.<br /> 或</li>
       <li>將任何新的Pinterest雲端設定從先前位置複製到 <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>更新任何AEM Communities網站根目錄，以透過 <code>[cq:Page]/jcr:content@cq:conf</code> 屬性到「新位置」中的絕對路徑。</li>
     <li>將舊版Pinterest ConnectCloud Service與任何更新為參考新位置的AEM Communities網站根取消關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 計分設定 {#scoring-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>若要與新的存放庫結構一致，可將計分規則儲存在 <code>/apps/settings/</code> 或/<code>conf/.../settings</code></p>
    <ol>
     <li>針對 <code>/apps/settings</code>，這將作為在SCM中管理的全域或預設規則。</li>
    </ol> <p>在中建立內容感知設定 <code>/conf/</code> 使用CRXDELite:</p>
    <ol>
     <li>在所需的中建立設定 <code>/conf/.../settings</code> 位置<br /> </li>
     <li>Communities網站必須具有 <code>cq:conf </code>屬性集。
      <ol>
       <li>若否 <code>cq:conf</code> 已設定，則會從屬性'的指定路徑直接讀取計分規則<code>scoringRules</code>「 」位於站點的根節點，例如： <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>清理：移除資源 <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Twitter Social登入設定 {#twitter-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudservices/twitterconnect</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/twitterconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的Twitter雲端設定都必須移轉至新位置。</p>
    <ol>
     <li>將「上一位置」中的現有配置遷移到「新位置」。
      <ol>
       <li>透過AEM編寫UI，手動重新建立新的Twitter Social登入設定，位於 <strong>工具&gt;Cloud Services&gt; Twitter Social登入設定</strong>.<br /> 或 <br /> </li>
       <li>將任何新的Twitter雲端設定從先前位置複製到適當的新位置，位於 <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>更新任何AEM Communities網站根目錄，以參考新的Twitter Social登入設定，方法是設定 <code>[cq:Page]/jcr:content@cq:conf</code> 屬性到「新位置」中的絕對路徑。</li>
     <li>將舊版Twitter ConnectCloud Service與任何更新為參考新位置的AEM Communities網站根取消關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 雜項 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>Adobe已提供移轉公用程式：</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>現有的自訂範本會移至 <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>
