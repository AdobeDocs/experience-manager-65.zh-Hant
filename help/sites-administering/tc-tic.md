---
title: 配置翻譯整合框架
seo-title: 配置翻譯整合框架
description: 瞭解如何配置翻譯整合框架。
seo-description: 瞭解如何配置翻譯整合框架。
uuid: 5ecfe154-732f-4a13-96f8-92f55023c54d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 200f51ab-f9bf-4989-91af-c3904fc673e5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置翻譯整合框架{#configuring-the-translation-integration-framework}

翻譯整合框架與第三方翻譯服務整合，以協調AEM內容的翻譯。

* 連接到您的翻譯服務提供商。
* 建立翻譯整合框架配置。
* 將雲端組態與您的頁面建立關聯。

如需AEM中內容轉譯功能的概觀，請參閱「多語 [言網站的轉譯內容」](/help/sites-administering/translation.md)。

## 連接到翻譯服務提供商 {#connecting-to-a-translation-service-provider}

建立將AEM連結至您的翻譯服務供應商的雲端設定。 AEM包含依預設連線至Microsoft Translator的功能。 對於其他翻譯提供者，請從「套件共用」下載 [連接器套件](/help/sites-administering/package-manager.md#package-share)。
以下翻譯供應商為翻譯項目提供了新API的實施。 連結，以進一步瞭解整合以及如何從Package Share下載：

* [Clay Tablet Technologies](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/clay-tablet-translation-connector-for-aem.html) （不在PackageShare上，請直接聯絡廠商）
* [Lionbridge](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/lionbridge-for-adobe-experience-manager.html)
* [雲字](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/cloudwords-for-adobe-translations-connector.html)
* [CrossLang NV](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/crosslang-xtm-for-adobe-experience-manager.html)
* [林戈特克](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/lingotek-for-adobe-experience-manager.html)
* Microsoft（Microsoft Translator已預先安裝在AEM中）
* [Smartling](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/smartling-connector-for-adobe-experience-manager.html)
* [Translations.com](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/globallink-connect-for-adobe-experience-manager.html)
* [SDL worldServer](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/sdlworldserver-connector.html)
* [SDL TMS](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/sdl-tms-translation-connector-for-adobe-experience-manager.html)
* [Systran](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/systran-for-adobe-experience-manager.html)
* [阿爾特朗](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/Altlang.html)

>[!NOTE]
>
>要查找人文和機器翻譯提供者的最新清單，請查看以下頁：
>
>
>* [AEM Human Translation](https://www.adobe.com/go/aem-human-translation-connectors)
>* [AEM機器翻譯](https://www.adobe.com/go/aem-machine-translation-connectors)
>



在安裝連接器套件後，您可以為連接器建立雲端組態。 通常，您需要提供認證，以便向翻譯服務進行驗證。 有關為Microsoft Translator連接器添加雲配置的資訊，請參 [閱與Microsoft Translator整合](/help/sites-administering/tc-msconf.md)。

如有需要，您可以為同一個連接器建立多個雲端組態。 例如，為您與相同供應商擁有的每個帳戶或專案建立一個組態。

在配置連接後，可以建立使用該連接的翻譯整合框架配置。

## 建立翻譯整合配置 {#creating-a-translation-integration-configuration}

建立翻譯整合架構設定，以指定如何翻譯您的內容。 配置包括以下資訊：

* 要使用的翻譯服務提供商。
* 無論要執行人文還是機器翻譯。
* 是否翻譯與頁面或資產相關聯的其他內容，例如標籤。

建立架構設定後，您會將雲端設定與您要根據設定轉譯的頁面建立關聯。 當翻譯過程啟動時，翻譯工作流會根據相關框架配置進行。

當您網站的不同區域有不同的翻譯需求時，請依此建立多個架構設定。 例如，多語言網站包含英文、西班牙文和日文版。 網站擁有者使用兩種不同的翻譯服務供應商進行西班牙文和日文翻譯。 因此，配置了框架的兩種配置。 每個配置使用不同的翻譯服務提供方。

在配置翻譯整合框架後，您可 [以將其與使用該框架的頁](/help/sites-administering/tc-prep.md) 關聯。

**** 注意：如需AEM中內容轉譯功能的概觀，請參閱「多語 [言網站的轉譯內容」](/help/sites-administering/translation.md)。

此架構的單一設定可控制如何翻譯頁面內容、社群內容和資產。
![chlimage_1-386](assets/chlimage_1-386.png)

### 站點配置屬性 {#sites-configuration-properties}

「網站」屬性可控制頁面內容的轉譯方式。

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>轉換工作流程</td>
   <td><p>選擇框架對站點內容執行的轉換方法：</p>
    <ul>
     <li>機器翻譯：翻譯提供者使用機器翻譯即時執行翻譯。</li>
     <li>人文翻譯：內容將發送到翻譯提供者，翻譯者將翻譯。 </li>
     <li>不要翻譯：內容不會傳送以供翻譯。 這是為了略過某些無法翻譯但可更新為最新內容的內容分支。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻譯提供者</td>
   <td>選擇要執行翻譯的翻譯提供程式。 當安裝了相應的連接器時，提供器將出現在清單中。</td>
  </tr>
  <tr>
   <td>內容類別</td>
   <td>（僅限機器翻譯）描述要翻譯的內容的類別。 在翻譯內容時，類別可能會影響術語和措辭的選擇。</td>
  </tr>
  <tr>
   <td>翻譯標記</td>
   <td>選取以轉譯與頁面相關聯的標籤。</td>
  </tr>
  <tr>
   <td>翻譯頁面資產</td>
   <td><p>選擇如何轉換從檔案系統新增至元件或從「資產」參考的資產：</p>
    <ul>
     <li>不要翻譯：頁面資產不會轉譯。</li>
     <li>使用網站轉譯工作流程：資產會根據「網站」標籤上的設定屬性處理。</li>
     <li>使用資產轉換工作流程：資產會根據「資產」標籤上屬性的設定來處理。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>自動執行翻譯</td>
   <td>選擇該選項可在建立翻譯項目後自動執行翻譯作業。 選擇此選項時，您沒有機會複查和調整翻譯作業的範圍。</td>
  </tr>
 </tbody>
</table>

### 社群配置屬性 {#communities-configuration-properties}

社群屬性控制如何執行使用者產生的內容轉譯。 使用者產生的內容翻譯一律使用機器翻譯。 如需詳細資訊，請參 [閱轉譯使用者產生的內容](/help/communities/translate-ugc.md)。

| 屬性 | 說明 |
|---|---|
| 翻譯提供者 | 選擇要執行翻譯的翻譯提供程式。 建立雲端組態的提供者會出現在清單中。 |
| 內容類別 | 說明您要翻譯之內容的類別。 在翻譯內容時，類別可能會影響術語和措辭的選擇。 |
| 選擇地區設定以用作全域共用商店 | （選擇性）透過選取儲存UGC的地區設定，所有語言副本的貼文都會出現在一個全域對話中。 依慣例，選擇網站基 [本語言的地](/help/communities/sites-console.md#translation) 區設定。 選擇「無公用商店」將禁用全局轉換。 預設情況下，全局轉換處於禁用狀態。 |

### 資產配置屬性 {#assets-configuration-properties}

資產屬性可控制如何設定資產。 如需有關轉譯資產的詳細資訊，請參 [閱建立資產的語言副本](/help/assets/translation-projects.md)。

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>轉換工作流程</td>
   <td><p>選擇框架為資產執行的翻譯類型：</p>
    <ul>
     <li>機器翻譯：翻譯提供者使用機器翻譯立即執行翻譯。</li>
     <li>人文翻譯：內容會自動傳送給翻譯提供者，以手動翻譯。 </li>
     <li>不要翻譯：資產不會傳送以進行翻譯。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻譯提供者</td>
   <td>選擇要執行翻譯的翻譯提供程式。 當安裝了相應的連接器時，提供器將出現在清單中。</td>
  </tr>
  <tr>
   <td>內容類別</td>
   <td>（僅限機器翻譯）描述要翻譯的內容的類別。 在翻譯內容時，類別可能會影響術語和措辭的選擇。</td>
  </tr>
  <tr>
   <td>翻譯資產</td>
   <td>選擇此項可將資產包含在翻譯專案中。 </td>
  </tr>
  <tr>
   <td>翻譯中繼資料</td>
   <td>選取以轉換資產中繼資料。</td>
  </tr>
  <tr>
   <td>翻譯標記</td>
   <td>選取以轉換與資產相關聯的標籤。</td>
  </tr>
  <tr>
   <td>自動執行翻譯</td>
   <td>選擇該選項可在建立翻譯項目後自動執行翻譯作業。 選擇此選項時，您沒有機會複查或調整翻譯作業的範圍。</td>
  </tr>
 </tbody>
</table>

1. 在側欄中，按一下或點選「工具>作業>雲端>雲端服務」。
1. 在「翻譯整合」區域中，是否建立了任何配置將決定顯示哪個連結：

   * 如果尚未建立任何配置，請按一下或點選「立即配置」。
   * 如果配置已存在，請按一下或點選「顯示配置」，然後按一下或點選「可用配置」旁顯示的+連結。

1. 鍵入配置的名稱，然後按一下或點選「建立」。
1. 在「網站」、「社群」和「資產」標籤上設定屬性，然後按一下或點選「確定」。

## 配置翻譯頁面 {#configuring-pages-for-translation}

若要設定將來源頁面翻譯成其他語言，請將頁面與下列雲端設定建立關聯：

* 將AEM連結至您的翻譯提供者的雲端設定。
* 配置翻譯詳細資訊的翻譯整合框架。

請注意，翻譯整合架構雲端組態可識別用於連線至服務提供者的雲端組態。 將源頁面與Framework雲端配置關聯時，該頁面必須與Framework雲端配置使用的服務提供商雲端配置關聯。

將頁面與雲端設定關聯時，頁面的子系會繼承關聯。 例如，如果您將/content/geometrixx/tw/products頁面與Translation Integration Framework建立關聯，則會根據框架翻譯「產品」頁面及其下面的所有頁面。

如有需要，您可以覆寫子系頁面上的關聯。 例如，網站的內容主要是服裝。 不過，其中一個頁面分支會說明該公司。 網站的根頁面與「翻譯整合框架」關聯，該框架指定使用Clothing類別進行機器翻譯。 描述公司的分支使用使用使用「常規」類別執行機器翻譯的框架。

此外，對於頁面上的 [任何社群](/help/communities/scf.md) SCF元件，使用者產生的內容(UGC)將包含使用者翻譯內容的能力。 如需詳細資訊，請參 [閱轉譯使用者產生的內容](/help/communities/translate-ugc.md)。

### 將頁面與翻譯提供者關聯 {#associating-a-page-with-a-translation-provider}

將頁面與翻譯提供者建立關聯，您使用該提供者翻譯頁面和後代頁面。

1. 在Sites主控台中，選取要設定的頁面，然後按一下或點選「檢視屬性」。
1. 按一下或點選「編輯」，然後按一下或點選「雲端服務」標籤。
1. 按一下或點選「新增設定>轉譯整合」。
1. 選擇要使用的翻譯提供器，然後按一下或點選「完成」。

### 將頁面與翻譯整合框架關聯 {#associating-pages-with-a-translation-integration-framework}

將頁面與Translation Integration Framework關聯，該框架定義了如何執行頁面和後代頁面的翻譯。

1. 在Sites主控台中，選取要設定的頁面，然後按一下或點選「檢視屬性」。
1. 按一下或點選「編輯」，然後按一下或點選「雲端服務」標籤。
1. 按一下或點選「新增設定>轉譯整合」。
1. 選擇要使用的翻譯整合框架，然後按一下或點選「完成」。

