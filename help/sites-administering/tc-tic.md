---
title: 設定翻譯整合框架
seo-title: Configuring the Translation Integration Framework
description: 瞭解如何配置翻譯整合框架。
seo-description: Learn how to configure the Translation Integration Framework.
uuid: 5ecfe154-732f-4a13-96f8-92f55023c54d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 200f51ab-f9bf-4989-91af-c3904fc673e5
feature: Language Copy
exl-id: 7562754b-d9fd-441b-8ae5-c7eebe458cef
source-git-commit: 6dea3a23c70fdb5f07bdf724547e799776002c61
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 5%

---

# 設定翻譯整合框架{#configuring-the-translation-integration-framework}

翻譯整合框架與第三方翻譯服務整合以協調內容的AEM翻譯。

* 連接到您的翻譯服務提供者。
* 建立翻譯整合框架設定。
* 將雲配置與您的頁面關聯。

有關中的內容翻譯功能的概AEM述，請參見 [翻譯多語言站點的內容](/help/sites-administering/translation.md)。

## 連接到翻譯服務提供者 {#connecting-to-a-translation-service-provider}

建立連接到翻譯服AEM務提供商的雲配置。 包AEM括預設連接到Microsoft翻譯器的功能。
以下翻譯供應商為翻譯項目提供了新API的實現。 連結以瞭解有關整合的詳細資訊：

* [翻譯.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html) (AdobeExchange Premier合作夥伴)
* [粘土平板技術](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [萊博智](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [梅姆索](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [雲字](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [XTM雲](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [林戈泰克](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [RWS](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108277.html)
* [智慧靈](https://www.smartling.com/software/integrations/adobe-experience-manager/)
* [瑟斯特蘭](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)
* [阿爾特朗](https://exchange.adobe.com/experiencecloud.details.90222.altlang.html)
* Microsoft(Microsoft翻譯器預裝於AEM中)

>[!NOTE]
>
>要查找最新的人工和機器翻譯提供商清單，請查看以下頁面：
>
>
>* [人AEM類翻譯](https://www.adobe.com/go/aem-human-translation-connectors)
>* [機器AEM翻譯](https://www.adobe.com/go/aem-machine-translation-connectors)
>


安裝連接器包後，可以為連接器建立雲配置。 通常，您需要提供憑據，以便向翻譯服務進行身份驗證。 有關為Microsoft翻譯器連接器添加雲配置的資訊，請參見 [與Microsoft翻譯器整合](/help/sites-administering/tc-msconf.md)。

如果需要，可以為同一連接器建立多個雲配置。 例如，為您與同一供應商擁有的每個帳戶或項目建立一個配置。

配置連接後，可以建立使用該連接的轉換整合框架配置。

## 建立翻譯整合設定 {#creating-a-translation-integration-configuration}

建立翻譯整合框架配置以指定如何翻譯內容。 設定包括以下資訊：

* 要使用哪個翻譯服務提供者.
* 是否進行人工翻譯或機器翻譯.
* 是否翻譯與頁面或資產關聯的其他內容，如標籤。

在建立框架配置後，將雲配置與要根據配置翻譯的頁面相關聯。 當翻譯過程被啟動時，翻譯工作流根據關聯的框架配置繼續進行。

當網站的不同部分有不同的翻譯要求時，請相應地建立多個框架配置。 例如，多語種網站包含英語、西班牙語和日語副本。 站點所有者使用兩種不同的翻譯服務提供商進行西班牙語和日語翻譯。 因此，配置了框架的兩種配置。 每個配置都使用不同的翻譯服務提供程式。

配置翻譯整合框架後，您可以 [將其與頁面關聯](/help/sites-administering/tc-prep.md) 用它。

**注：** 有關中的內容翻譯功能的概AEM述，請參見 [翻譯多語言站點的內容](/help/sites-administering/translation.md)。

框架的單個配置控制如何翻譯頁面內容、社區內容和資產。
![chlimage_1-386](assets/translation-config-65.jpg)

### 站點配置屬性 {#sites-configuration-properties}

「站點」屬性控制頁面內容的翻譯方式。

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>轉換工作流程</td>
   <td><p>選擇框架對站點內容執行的翻譯方法：</p>
    <ul>
     <li>機器翻譯：翻譯提供器使用機器翻譯即時執行翻譯。</li>
     <li>人文翻譯：內容將發送到翻譯提供商，由翻譯員翻譯。 </li>
     <li>不翻譯：不發送內容進行翻譯。 這將跳過某些內容分支，這些分支不會被翻譯，但可以用最新內容進行更新。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻譯提供程式</td>
   <td>選擇要執行翻譯的翻譯提供程式。 當安裝了相應的連接器時，提供程式將出現在清單中。</td>
  </tr>
  <tr>
   <td>內容類別</td>
   <td>（僅限機器翻譯）描述要翻譯的內容的類別。 在翻譯內容時，該類別會影響術語和措辭的選擇。</td>
  </tr>
  <tr>
   <td>翻譯標記</td>
   <td>選擇以轉換與頁面關聯的標籤。</td>
  </tr>
  <tr>
   <td>翻譯頁面資產</td>
   <td><p>選擇如何轉換從檔案系統添加到元件或從資產引用的資產：</p>
    <ul>
     <li>不翻譯：頁面資產不進行轉換。</li>
     <li>使用「站點」翻譯工作流：根據「站點」(Sites)頁籤上的配置屬性處理資產。</li>
     <li>使用資產轉換工作流：資產根據「資產」頁籤上的屬性配置進行處理。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>自動執行翻譯</td>
   <td>選擇以在建立翻譯項目後自動執行翻譯作業。 選擇此選項時，您沒有機會複查和確定翻譯作業的範圍。</td>
  </tr>
 </tbody>
</table>

### 社區配置屬性 {#communities-configuration-properties}

社區屬性控制如何執行用戶生成內容的翻譯。 用戶生成內容的翻譯始終使用機器翻譯。 有關詳細資訊，請參見 [翻譯用戶生成的內容](/help/communities/translate-ugc.md)。

| 屬性 | 說明 |
|---|---|
| 翻譯提供程式 | 選擇要執行翻譯的翻譯提供程式。 為其建立雲配置的提供程式將出現在清單中。 |
| 內容類別 | 描述要翻譯的內容的類別。 在翻譯內容時，該類別會影響術語和措辭的選擇。 |
| 選擇要用作全局共用儲存的區域設定 | （可選）通過選擇儲存UGC的區域設定，所有語言副本中的帖子將出現在一個全局對話中。 按慣例，選擇 [基語](/help/communities/sites-console.md#translation) 的雙曲餘切值。 選擇「無公用儲存」將禁用全局轉換。 預設情況下，全局轉換處於禁用狀態。 |

### 資產配置屬性 {#assets-configuration-properties}

資產屬性控制如何配置資產。 有關轉換資產的詳細資訊，請參閱 [為資產建立語言副本](/help/assets/translation-projects.md)。

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>轉換工作流程</td>
   <td><p>選擇框架對資產執行的轉換類型：</p>
    <ul>
     <li>機器翻譯：翻譯提供器使用機器翻譯立即執行翻譯。</li>
     <li>人文翻譯：內容自動發送到翻譯提供程式以被手動翻譯。 </li>
     <li>不翻譯：不發送資產進行翻譯。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻譯提供程式</td>
   <td>選擇要執行翻譯的翻譯提供程式。 當安裝了相應的連接器時，提供程式將出現在清單中。</td>
  </tr>
  <tr>
   <td>內容類別</td>
   <td>（僅限機器翻譯）描述要翻譯的內容的類別。 在翻譯內容時，該類別會影響術語和措辭的選擇。</td>
  </tr>
  <tr>
   <td>翻譯資產</td>
   <td>選擇以在轉換項目中包括資產。 </td>
  </tr>
  <tr>
   <td>翻譯中繼資料</td>
   <td>選擇以轉換資產元資料。</td>
  </tr>
  <tr>
   <td>翻譯標記</td>
   <td>選擇以轉換與資產關聯的標籤。</td>
  </tr>
  <tr>
   <td>自動執行翻譯</td>
   <td>選擇以在建立翻譯項目後自動執行翻譯作業。 選擇此選項時，您沒有機會複查或確定翻譯作業的範圍。</td>
  </tr>
 </tbody>
</table>

1. 在側欄中，按一下或點擊「工具」>「操作」>「雲」>「Cloud Services」。
1. 在「翻譯整合」區域中，是否已建立任何配置將確定出現哪個連結：

   * 如果未建立任何配置，請按一下或點擊「立即配置」。
   * 如果配置已存在，請按一下或點擊「顯示配置」，然後按一下或點擊「可用配置」旁邊出現的+連結。

1. 鍵入配置的名稱，然後按一下或點擊「建立」。
1. 在「站點」、「社區」和「資產」頁籤上配置屬性，然後按一下或點擊「確定」。

## 配置翻譯頁面 {#configuring-pages-for-translation}

要將源頁面翻譯成其他語言，請將這些頁面與以下雲配置關聯：

* 連接到翻譯提供AEM商的雲配置。
* 配置翻譯詳細資訊的翻譯整合框架。

請注意，翻譯整合框架雲配置標識了用於連接到服務提供商的雲配置。 將源頁與框架雲配置關聯時，該頁必須與框架雲配置使用的服務提供商雲配置關聯。

將頁面與雲配置關聯時，頁面的子體將繼承關聯。 例如，如果將/content/geometrixx/en/products頁與翻譯整合框架相關聯，則「產品」頁及其下面的所有頁都會根據框架進行翻譯。

如果需要，可以覆蓋子代頁面上的關聯。 例如，網站的內容主要是關於服裝。 不過，有一頁分部描述了該公司。 站點的根頁與一個翻譯整合框架關聯，該框架使用Clothing類別指定機器翻譯。 描述公司的分支使用使用「常規」類別執行機器翻譯的框架。

此外，對任何社區 [SCF元件](/help/communities/scf.md) 在頁面上，用戶生成的內容(UGC)將包括用戶翻譯內容的能力。 有關詳細資訊，請參見 [用戶生成內容的翻譯](/help/communities/translate-ugc.md)。

### 將頁面與翻譯提供程式關聯 {#associating-a-page-with-a-translation-provider}

將頁面與用於翻譯頁面和後代頁面的翻譯提供程式關聯。

1. 在「站點」控制台中，選擇要配置的頁面，然後按一下或點擊「查看屬性」。
1. 按一下或點擊「Edit（編輯）」 ，然後按一下或點擊「Cloud Services」頁籤。
1. 按一下或按一下「添加配置」>「翻譯整合」。
1. 選擇要使用的翻譯提供程式，然後按一下或點擊「完成」。

### 將頁面與翻譯整合框架關聯 {#associating-pages-with-a-translation-integration-framework}

將頁面與翻譯整合框架關聯，該框架定義了要如何執行頁面和子代頁面的翻譯。

1. 在「站點」控制台中，選擇要配置的頁面，然後按一下或點擊「查看屬性」。
1. 按一下或點擊「Edit（編輯）」 ，然後按一下或點擊「Cloud Services」頁籤。
1. 按一下或按一下「添加配置」>「翻譯整合」。
1. 選擇要使用的翻譯整合框架，然後按一下或點擊「完成」。
