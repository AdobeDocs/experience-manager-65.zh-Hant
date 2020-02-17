---
title: 6.4中AEM Communities的儲存庫重組
seo-title: 6.4中AEM Communities的儲存庫重組
description: 瞭解如何進行必要的變更，以移轉至AEM 6.4 for Communities中的新儲存庫結構。
seo-description: 瞭解如何進行必要的變更，以移轉至AEM 6.4 for Communities中的新儲存庫結構。
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# 6.5版中AEM Communities的儲存庫重組 {#repository-restructuring-for-aem-communities-in}

如AEM 6.4 [(AEM 6.4)頁面中的父資料庫重組(](/help/sites-deploying/repository-restructuring.md) Repository Restructing)所述，升級至AEM 6.5的客戶應使用此頁面來評估與影響AEM Communities Solution的資料庫變更相關的工作成果。 有些變更需要在AEM 6.5升級程式中努力工作，而其他變更則可延後至日後升級。

**使用6.5升級**

* [電子郵件通知模板](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [訂閱設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**未來升級前**

* [標籤配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [Classic Communities主控台設計](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Facebook社交登入設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [語言選項配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Pinterest Social登入設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [計分配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Twitter社交登入設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [其他](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## 使用6.5升級 {#with-upgrade}

### 電子郵件通知模板 {#e-mail-notification-templates}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>如果要移至「」下的新路徑，則需要手動<code>/apps/settings</code>移轉。 您可以使用Granite Configuration manager執行遷移。</p> <p>通過將屬性設定為" <code>mergeList</code> "節 <code>true</code> 點並添加子節<code>/libs/settings/community/subscriptions</code><code>nt:unstructured</code> 點，可以執行遷移。</p> </td>
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
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>如果要移至「」下的新路徑，則需要手動<code>/apps/settings</code>移轉。 您可以使用Granite Configuration manager執行遷移。</p> <p>通過將屬性設定為" <code>mergeList</code> "節 <code>true</code> 點並添加子節<code>/libs/settings/community/subscriptions</code><code>nt:unstructured</code> 點，可以執行遷移。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 關注字詞設定 {#watchwords-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td>/etc/watchwords</td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td>/libs/community/watchwords</td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td>A Lazy Migration task is available to clean the Communities Configurations.<br /> <p>Task會將關注字詞從移 <code>/etc/watchwords</code> 動到 <code>/conf/global/settings/community/watchwords</code>。</p> <p>如果自訂的監看字儲存在SCM中，則應將其部署至 <code>/apps/settings/...</code> ，且您必須確保沒有優先 <code>/conf/global/settings/...</code> 的覆蓋設定。</p> <p>遷移任務刪除 <code>/etc</code> 位置。</p> </td>
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
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><strong>徽章規則：</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>徽章影像：</strong></p> <p>對於預設影像： <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>針對自訂影像： <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>需要手動遷移。</p> <p>如果您的例項已自訂標籤／計分規則，則無法自動將所有規則放在儲存貯體下。 需要客戶輸入您要用於您網站的會議時段（全域或網站特定）。</p> <p>沒有可用來設定網站標籤和計分的UI。</p> <p>要與新的儲存庫結構一致：</p>
    <ol>
     <li>使用「工具」下的「設定瀏覽器」 <strong>建立網站內容</strong> 儲 <strong>存貯體</strong></li>
     <li>前往網站根目錄</li>
     <li>設 <code>cq:confproperty</code> 定為儲存所有設定的儲存貯體路徑。 您也可以透過網站編輯精靈——設定 <strong>雲端組態輸入來設定相同的設定</strong>。</li>
     <li>將相關的標籤規則和計分規則從上 <code>/etc/community/*</code> 一步驟中建立的網站內容儲存區移至。</li>
     <li>調整網站根目錄上的標籤規則和計分規則屬性，以便具有新規則位置的相對參照。
      <ol>
       <li>例如，如果屬性為 <code>cq:conf = /conf/we-retail</code>, <code>badgingRules [] = community/badging/rules</code> 則規則現在會移至此新儲存貯體。</li>
      </ol> </li>
     <li>同樣地，調整標籤規則節點中對計分規則的引用，使其具有相對路徑。</li>
    </ol> <p> </p> <p>最後，通過刪除資源來清理 <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Classic Communities主控台設計 {#classic-communities-console-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
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

### Facebook Social Login Configurations {#facebook-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
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
     <li>將「上一個位置」中的現有配置遷移到「新位置」。
      <ol>
       <li>透過「工具&gt;雲端服務&gt; facebook社交登入設定」的AEM編寫UI, <strong>手動重新建立新的Facebook社交登入設定</strong>。<br /> 或 <br /> </li>
       <li>將任何新的Facebook雲端設定從「上一個位置」複製至「適當的新位置」下方 <code>/conf/global or /conf/&lt;tenant&gt;</code>。</li>
      </ol> </li>
     <li>將屬性設為「新位置」中的絕對路徑，以更新任何AEM Communities網站根目錄 <code>[cq:Page]/jcr:content@cq:conf</code> 來參考新的Facebook Social登入設定。</li>
     <li>將舊版Facebook Connect cloud服務與任何更新為參考新位置的AEM Communities網站根目錄取消關聯。</li>
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
   <td><strong>上一個位置</strong></td>
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

### Pinterest Social Login Configurations {#pinterest-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
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
     <li>將「上一個位置」中的現有配置遷移到「新位置」。
      <ol>
       <li>透過AEM編寫UI，在「工具&gt;雲端服務&gt; Pinterest Social登入設定」 <strong>中手動重新建立新的Pinterest Social登入設定</strong>。<br /> 或</li>
       <li>將任何新的Pinterest雲端設定從「上一個位置」複製至下方的適當新位置 <code>/conf/global or /conf/&lt;tenant&gt;</code>。</li>
      </ol> </li>
     <li>更新任何AEM Communities網站根目錄，以參考新Pinterest Social登入設定，方法是將屬性設 <code>[cq:Page]/jcr:content@cq:conf</code> 定為「新位置」中的絕對路徑。</li>
     <li>將舊版Pinterest Connect cloud服務與任何更新以參考新位置的AEM Communities網站根目錄取消關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 計分配置 {#scoring-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>要與新的儲存庫結構對齊，可將計分規則儲存在或/ <code>/apps/settings/</code> 中<code>conf/.../settings</code></p>
    <ol>
     <li>對於 <code>/apps/settings</code>，這將充當在SCM中管理的全局或預設規則。</li>
    </ol> <p>使用CRXDELite在中創 <code>/conf/</code> 建上下文感知配置：</p>
    <ol>
     <li>在所需位置建立設 <code>/conf/.../settings</code> 定<br /> </li>
     <li>社群網站必須設 <code>cq:conf </code>定屬性。
      <ol>
       <li>如果未 <code>cq:conf</code> 設定，則將直接從站點根節點上屬性'<code>scoringRules</code>'的給定路徑讀取計分規則，例如： <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>清除：刪除資源 <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Twitter Social Login Configurations {#twitter-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
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
     <li>將「上一個位置」中的現有配置遷移到「新位置」。
      <ol>
       <li>透過「工具&gt;雲端服務&gt; twitter社交登入設定」的AEM編寫UI, <strong>手動重新建立新的Twitter社交登入設定</strong>。<br /> 或 <br /> </li>
       <li>將任何新的Twitter雲端設定從「上一個位置」複製至「適當的新位置」下方 <code>/conf/global or /conf/&lt;tenant&gt;</code>。</li>
      </ol> </li>
     <li>將屬性設為「新位置」中的絕對路徑，以更新任何AEM Communities網站根目錄 <code>[cq:Page]/jcr:content@cq:conf</code> 來參考新的Twitter Social登入設定。</li>
     <li>將舊版Twitter Connect cloud服務與任何更新為參考新位置的AEM Communities網站根目錄取消關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 其他 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>Adobe已提供移轉公用程式，網址為：</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>現有的自訂範本會移至 <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>

