---
title: 6.4中AEM Communities的存放庫重組
description: 瞭解如何進行必要的變更，以移轉至適用於社群的AEM 6.4中的新存放庫結構。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4d2bdd45-a29a-4936-b8da-f7e011d81e83
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 1%

---

# 6.5中AEM Communities的存放庫重組 {#repository-restructuring-for-aem-communities-in}

如AEM 6.4](/help/sites-deploying/repository-restructuring.md)頁面的上層[存放庫重新調整中所述，升級至AEM 6.5的客戶應使用此頁面來評估與影響AEM Communities解決方案的存放庫變更相關的工作量。 在AEM 6.5升級程式期間，有些變更需要投入大量精力，而其他變更則可能延遲到未來升級。

**升級為6.5**

* [電子郵件通知範本](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [訂閱設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**未來升級之前**

* [徽章設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [傳統Communities主控台設計](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [facebook社交登入設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [語言選項設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [pinterest社交登入設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [評分設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [twitter社交登入設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [雜項](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## 6.5版升級 {#with-upgrade}

### 電子郵件通知範本 {#e-mail-notification-templates}

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
   <td><strong>重組指南</strong></td>
   <td><p>如果您想要移至"<code>/apps/settings</code>"下的新路徑，則需要手動移轉。 您可以使用Granite Configuration Manager來執行移轉。</p> <p>您可以在<code>/libs/settings/community/subscriptions</code>節點上將屬性<code>mergeList</code>設定為<code>true</code>並新增<code>nt:unstructured</code>子節點來執行移轉。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
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
   <td><strong>重組指南</strong></td>
   <td><p>如果您想要移至"<code>/apps/settings</code>"下的新路徑，則需要手動移轉。 您可以使用Granite Configuration Manager來執行移轉。</p> <p>您可以在<code>/libs/settings/community/subscriptions</code>節點上將屬性<code>mergeList</code>設定為<code>true</code>並新增<code>nt:unstructured</code>子節點來執行移轉。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
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
   <td><strong>重組指南</strong></td>
   <td>延遲移轉工作可用於清除Communities設定。<br /> <p>任務會將關注字詞從<code>/etc/watchwords</code>移至<code>/conf/global/settings/community/watchwords</code>。</p> <p>如果自訂標語儲存在SCM中，則應將其部署到<code>/apps/settings/...</code>，您必須確保沒有優先的重疊<code>/conf/global/settings/...</code>設定。</p> <p>移轉工作已移除<code>/etc</code>個位置。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

## 未來升級之前 {#prior-to-upgrade}

### 徽章設定 {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><strong>徽章規則：</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>徽章影像：</strong></p> <p>對於預設影像： <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>對於自訂影像： <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>需要手動移轉。</p> <p>如果您的執行個體已自訂徽章/評分規則，則沒有自動方式將所有規則放置在貯體下。 需要客戶輸入您要用於您網站的conf貯體（全域或網站特定）。</p> <p>沒有可用於設定網站徽章和評分的UI。</p> <p>若要與新的存放庫結構保持一致：</p>
    <ol>
     <li>使用<strong>工具</strong>下的<strong>設定瀏覽器</strong>建立網站內容貯體</li>
     <li>移至網站根目錄</li>
     <li>將<code>cq:confproperty</code>設定為您要儲存所有設定的貯體路徑。 相同可透過網站<strong>編輯精靈 — 設定雲端組態輸入</strong>設定。</li>
     <li>將相關的徽章規則和評分規則從<code>/etc/community/*</code>移至在上一步中建立的網站內容貯體。</li>
     <li>調整網站根目錄上的徽章規則和評分規則屬性，使其具有新規則位置的相對參照。
      <ol>
       <li>例如，如果<code>cq:conf = /conf/we-retail</code>的屬性，則<code>badgingRules [] = community/badging/rules</code> （如果規則）現在會移至此新貯體。</li>
      </ol> </li>
     <li>同樣地，調整徽章規則節點中評分規則的參考，以擁有相對路徑。</li>
    </ol> <p> </p> <p>最後，移除資源以清除 <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

### 傳統Communities主控台設計 {#classic-communities-console-designs}

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
   <td><strong>重組指南</strong></td>
   <td>不適用</td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

### facebook社交登入設定 {#facebook-social-login-configurations}

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
   <td><strong>重組指南</strong></td>
   <td><p>任何新的Facebook雲端設定都必須移轉至新位置。</p>
    <ol>
     <li>將先前位置中的現有組態移轉到新位置。
      <ol>
       <li>透過AEM編寫UI，在<strong>工具&gt;Cloud Service&gt; Facebook社交登入設定</strong>手動重新建立新的Facebook社交登入設定。<br /> 或 <br /> </li>
       <li>將任何新的Facebook雲端設定從先前位置複製到<code>/conf/global or /conf/&lt;tenant&gt;</code>下的適當新位置。</li>
      </ol> </li>
     <li>透過將<code>[cq:Page]/jcr:content@cq:conf</code>屬性設定為新位置中的絕對路徑，更新任何AEM Communities網站根以參考新的Facebook社交登入設定。</li>
     <li>解除舊版Facebook ConnectCloud Service與任何更新以參照新位置的AEM Communities網站根目錄的關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

### 語言選項設定 {#language-options-configurations}

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
   <td><strong>重組指南</strong></td>
   <td>不適用<br /> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

### pinterest社交登入設定 {#pinterest-social-login-configurations}

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
   <td><strong>重組指南</strong></td>
   <td><p>任何新的Pinterest雲端設定都必須移轉至新位置。</p>
    <ol>
     <li>將先前位置中的現有組態移轉到新位置。
      <ol>
       <li>透過AEM編寫UI，在<strong>工具&gt;Cloud Service&gt; Pinterest社交登入設定</strong>手動重新建立新的Pinterest社交登入設定。<br />或</li>
       <li>將任何新的Pinterest雲端設定從先前的位置複製到<code>/conf/global or /conf/&lt;tenant&gt;</code>下適當的新位置。</li>
      </ol> </li>
     <li>透過將<code>[cq:Page]/jcr:content@cq:conf</code>屬性設定為新位置中的絕對路徑，更新任何AEM Communities網站根以參考新的Pinterest社交登入設定。</li>
     <li>解除舊版Pinterest ConnectCloud Service與任何更新以參照新位置的AEM Communities網站根目錄的關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

### 評分設定 {#scoring-configurations}

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
   <td><strong>重組指南</strong></td>
   <td><p>為了符合新的存放庫結構，評分規則可以儲存在<code>/apps/settings/</code>或/<code>conf/.../settings</code></p>
    <ol>
     <li>對於<code>/apps/settings</code>，這會當作在SCM中管理的全域或預設規則。</li>
    </ol> <p>使用CRXDELite在<code>/conf/</code>中建立內容感知設定：</p>
    <ol>
     <li>在所需的<code>/conf/.../settings</code>位置<br />中建立設定 </li>
     <li>Communities網站必須設定<code>cq:conf </code>屬性。
      <ol>
       <li>如果未設定<code>cq:conf</code>，評分規則會直接從網站根節點屬性'<code>scoringRules</code>'的指定路徑讀取，例如： <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>清除：移除資源 <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

### twitter社交登入設定 {#twitter-social-login-configurations}

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
   <td><strong>重組指南</strong></td>
   <td><p>任何新的Twitter雲端設定都必須移轉至新位置。</p>
    <ol>
     <li>將先前位置中的現有組態移轉到新位置。
      <ol>
       <li>透過<strong>工具&gt;Cloud Service&gt;Twitter社交登入設定</strong>的AEM編寫UI，手動重新建立新的Twitter社交登入設定。<br /> 或 <br /> </li>
       <li>將任何新Twitter雲端設定從先前位置複製到<code>/conf/global or /conf/&lt;tenant&gt;</code>下的適當新位置。</li>
      </ol> </li>
     <li>將<code>[cq:Page]/jcr:content@cq:conf</code>屬性設定為「新位置」中的絕對Twitter，更新任何AEM Communities網站根以參照新的網站社交登入設定。</li>
     <li>解除舊版Twitter連線Cloud Service與任何已更新為參考新位置的AEM Communities網站根目錄的關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
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
   <td><strong>重組指南</strong></td>
   <td><p>Adobe已在以下位置提供移轉公用程式：</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>現有的自訂範本將會移至 <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>
