---
title: 6.4中AEM Communities的資料庫重組
seo-title: Repository Restructuring for AEM Communities in 6.4
description: 瞭解如何進行必要的更改，以便遷移到6.4中的AEM社區新儲存庫結構。
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

# 6.5中AEM Communities的資料庫重組 {#repository-restructuring-for-aem-communities-in}

如父代中所述 [6.AEM4中的儲存庫重組](/help/sites-deploying/repository-restructuring.md) 頁面，升級到AEM6.5的客戶應使用此頁面評估與影響AEM Communities解決方案的儲存庫更改相關的工作量。 某些更改需要在6.5升AEM級過程中進行工作，而其他更改則可以推遲到以後升級。

**使用6.5升級**

* [電子郵件通知模板](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [訂閱配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**未來升級前**

* [標籤配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [經典社區控制台設計](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Facebook社會登錄配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [語言選項配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Pinterest社會登錄配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [評分配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Twitter社會登錄配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [雜項](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

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
   <td><p>如果要移動到「」下的新路徑，需要手動遷移<code>/apps/settings</code>。 可以使用「花崗岩配置管理器」執行遷移。</p> <p>可以通過設定屬性來執行遷移 <code>mergeList</code> 至 <code>true</code> 的<code>/libs/settings/community/subscriptions</code>"節點並添加 <code>nt:unstructured</code> 子節點。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 訂閱配置 {#subscription-configurations}

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
   <td><p>如果要移動到「」下的新路徑，需要手動遷移<code>/apps/settings</code>。 可以使用「花崗岩配置管理器」執行遷移。</p> <p>可以通過設定屬性來執行遷移 <code>mergeList</code> 至 <code>true</code> 的<code>/libs/settings/community/subscriptions</code>"節點並添加 <code>nt:unstructured</code> 子節點。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 監視詞配置 {#watchwords-configurations}

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
   <td>「懶惰遷移」任務可用於清除社區配置。<br /> <p>任務將監視詞從 <code>/etc/watchwords</code> 至 <code>/conf/global/settings/community/watchwords</code>。</p> <p>如果自定義的監視詞儲存在SCM中，則應將其部署到 <code>/apps/settings/...</code> 你必須確保不要在 <code>/conf/global/settings/...</code> 優先配置。</p> <p>遷移任務刪除 <code>/etc</code> 位置。</p> </td>
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
   <td><p><strong>徽章規則：</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>標籤影像：</strong></p> <p>對於預設映像： <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>對於自定義映像： <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>需要手動遷移。</p> <p>如果實例已自定義標籤/計分規則，則無法自動將所有規則置於儲存段下。 需要客戶輸入您希望在哪個會議儲存段（全局儲存段或特定於站點的儲存段）上為您的站點使用。</p> <p>沒有可用於配置站點的標籤和記分的UI。</p> <p>要與新的儲存庫結構對齊：</p>
    <ol>
     <li>使用 <strong>配置瀏覽器</strong> 在 <strong>工具</strong></li>
     <li>轉到站點根目錄</li>
     <li>設定 <code>cq:confproperty</code> 儲存所有設定的儲存桶路徑。 也可以通過站點設定 <strong>編輯嚮導 — 設定雲配置輸入</strong>。</li>
     <li>將相關標籤規則和評分規則從 <code>/etc/community/*</code> 到在上一步中建立的站點上下文時段。</li>
     <li>調整站點根上的標籤規則和記分規則屬性，使其具有對新規則位置的相對引用。
      <ol>
       <li>例如，如果 <code>cq:conf = /conf/we-retail</code>，則 <code>badgingRules [] = community/badging/rules</code> 是否將規則移到此新時段。</li>
      </ol> </li>
     <li>同樣，調整標籤規則節點中對記分規則的引用以具有相對路徑。</li>
    </ol> <p> </p> <p>最後，通過刪除資源來清除 <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 經典社區控制台設計 {#classic-communities-console-designs}

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

### Facebook社會登錄配置 {#facebook-social-login-configurations}

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
   <td><p>任何新的Facebook雲配置都必須遷移到新位置。</p>
    <ol>
     <li>將上一個位置中的現有配置遷移到新位置。
      <ol>
       <li>通過創作UI在以下位置手動重新建立新的Facebook社AEM交登錄配置 <strong>工具&gt;Cloud Services&gt;Facebook社會登錄配置</strong>。<br /> 或 <br /> </li>
       <li>將任何新的Facebook雲配置從上一個位置複製到相應的新位置，位於 <code>/conf/global or /conf/&lt;tenant&gt;</code>。</li>
      </ol> </li>
     <li>通過設定以下項來更新任何AEM Communities站點根目錄以引用新的Facebook社會登錄配置 <code>[cq:Page]/jcr:content@cq:conf</code> 屬性到「新建位置」中的絕對路徑。</li>
     <li>將舊版Facebook連接Cloud Service與任何更新為引用新位置的AEM Communities站點根取消關聯。</li>
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

### Pinterest社會登錄配置 {#pinterest-social-login-configurations}

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
   <td><p>任何新的Pinterest雲配置都必須遷移到新位置。</p>
    <ol>
     <li>將上一個位置中的現有配置遷移到新位置。
      <ol>
       <li>通過創作UI在以下位置手動重新建立新的Pinterest社AEM交登錄配置 <strong>工具&gt;Cloud Services&gt;Pinterest社會登錄配置</strong>。<br /> 或</li>
       <li>將任何新的Pinterest雲配置從先前位置複製到以下相應的新位置 <code>/conf/global or /conf/&lt;tenant&gt;</code>。</li>
      </ol> </li>
     <li>通過設定更新任何AEM Communities站點根目錄以引用新Pinterest社會登錄配置 <code>[cq:Page]/jcr:content@cq:conf</code> 屬性到「新建位置」中的絕對路徑。</li>
     <li>將舊版Pinterest連接Cloud Service與任何更新為引用新位置的AEM Communities站點根取消關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 評分配置 {#scoring-configurations}

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
   <td><p>要與新的儲存庫結構對齊，可將評分規則儲存在 <code>/apps/settings/</code> 或/<code>conf/.../settings</code></p>
    <ol>
     <li>對於 <code>/apps/settings</code>，它將充當在SCM中管理的全局或預設規則。</li>
    </ol> <p>在中建立上下文感知配置 <code>/conf/</code> 使用CRXDELite:</p>
    <ol>
     <li>在所需的配置中建立 <code>/conf/.../settings</code> 位置<br /> </li>
     <li>社區站點必須具有 <code>cq:conf </code>屬性屬性集。
      <ol>
       <li>否 <code>cq:conf</code> 設定，將直接從屬性「的給定路徑讀取計分規則<code>scoringRules</code>'的根節點，例如： <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>清理：刪除資源 <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Twitter社會登錄配置 {#twitter-social-login-configurations}

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
   <td><p>任何新的Twitter雲配置都必須遷移到新位置。</p>
    <ol>
     <li>將上一個位置中的現有配置遷移到新位置。
      <ol>
       <li>通過創作UI在以下位置手動重新建立新的Twitter社AEM交登錄配置 <strong>工具&gt;Cloud Services&gt;Twitter社會登錄配置</strong>。<br /> 或 <br /> </li>
       <li>將任何新的Twitter雲配置從上一個位置複製到相應的新位置，位於 <code>/conf/global or /conf/&lt;tenant&gt;</code>。</li>
      </ol> </li>
     <li>通過設定以下項來更新任何AEM Communities站點根目錄以引用新的Twitter社會登錄配置 <code>[cq:Page]/jcr:content@cq:conf</code> 屬性到「新建位置」中的絕對路徑。</li>
     <li>將舊版Twitter連接Cloud Service與任何更新為引用新位置的AEM Communities站點根取消關聯。</li>
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
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>Adobe提供了遷移實用程式：</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>現有自定義模板將移到 <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>
