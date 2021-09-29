---
title: 配置翻譯整合框架
seo-title: Configuring the Translation Integration Framework
description: 了解如何配置翻譯整合框架。
seo-description: Learn how to configure the Translation Integration Framework.
uuid: 5ecfe154-732f-4a13-96f8-92f55023c54d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 200f51ab-f9bf-4989-91af-c3904fc673e5
feature: Language Copy
exl-id: 7562754b-d9fd-441b-8ae5-c7eebe458cef
source-git-commit: cadf2e240327ef52ef57f8fb2e911f36fd003852
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 1%

---

# 配置翻譯整合框架{#configuring-the-translation-integration-framework}

翻譯整合框架與第三方翻譯服務整合，以協調AEM內容的翻譯。

* 連接到翻譯服務提供商。
* 建立翻譯整合架構設定。
* 將雲端設定與您的頁面建立關聯。

如需AEM中內容翻譯功能的概觀，請參閱[多語言網站的翻譯內容](/help/sites-administering/translation.md)。

## 連接到翻譯服務提供商 {#connecting-to-a-translation-service-provider}

建立將AEM連接至翻譯服務提供者的雲端設定。 AEM預設包含連接到Microsoft Translator的功能。
下列翻譯廠商提供翻譯專案的新API實作。 深入了解整合的連結：

* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html) (AdobeExchange首要合作夥伴)
* [粘土片技術](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [雲字](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [XTM雲](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [林戈泰克](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [智慧](https://exchange.adobe.com/experiencecloud.details.90101.smartling-connector-for-adobe-experience-manager.html)
* [SDL](https://exchange.adobe.com/experiencecloud.details.100110.sdl-translation-management.html)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)
* [阿爾特朗](https://exchange.adobe.com/experiencecloud.details.90222.altlang.html)
* Microsoft(AEM中預裝了Microsoft Translator)

>[!NOTE]
>
>若要尋找最新的人文和機器翻譯提供者清單，請查看下列頁面：
>
>
>* [AEM人文翻譯](https://www.adobe.com/go/aem-human-translation-connectors)
>* [AEM機器翻譯](https://www.adobe.com/go/aem-machine-translation-connectors)

>


安裝連接器封裝後，您可以為連接器建立雲端設定。 通常，您需要提供認證以驗證翻譯服務。 有關為Microsoft Translator連接器添加雲配置的資訊，請參閱[與Microsoft Translator整合](/help/sites-administering/tc-msconf.md)。

您可以視需要為相同連接器建立多個雲端設定。 例如，為您與相同供應商擁有的每個帳戶或項目建立一個配置。

配置連接後，可以建立使用該連接的翻譯整合框架配置。

## 建立翻譯整合設定 {#creating-a-translation-integration-configuration}

建立翻譯整合架構設定，以指定如何翻譯您的內容。 設定包含下列資訊：

* 要使用哪個翻譯服務提供商。
* 無論是人翻譯還是機器翻譯。
* 是否翻譯與頁面或資產相關聯的其他內容，例如標籤。

建立框架配置後，可將雲配置與要根據配置翻譯的頁面相關聯。 當翻譯過程開始時，翻譯工作流程會根據相關的框架配置進行。

當您網站的不同區段有不同的翻譯需求時，請據此建立多個架構設定。 例如，多語言網站包含英文、西班牙文和日文語言副本。 網站擁有者使用兩個不同的翻譯服務提供者提供西班牙文和日文翻譯。 因此，框架的兩個配置已配置。 每個配置使用不同的翻譯服務提供程式。

配置翻譯整合框架後，您可以[將其與使用該框架的頁面](/help/sites-administering/tc-prep.md)關聯。

**注意：** 如需AEM內容翻譯功能的概觀，請參閱 [多語言網站的翻譯內容](/help/sites-administering/translation.md)。

架構的單一設定可控制如何翻譯頁面內容、社群內容和資產。
![chlimage_1-386](assets/translation-config-65.jpg)

### 站點配置屬性 {#sites-configuration-properties}

Sites屬性可控制頁面內容轉譯的執行方式。

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>轉換工作流程</td>
   <td><p>選擇框架對網站內容執行的翻譯方法：</p>
    <ul>
     <li>機器翻譯：翻譯提供者使用機器翻譯即時執行翻譯。</li>
     <li>人類翻譯：內容被發送到翻譯提供者，由翻譯者翻譯。 </li>
     <li>不翻譯：內容不會傳送以供翻譯。 這是為了略過某些內容分支，這些分支不會翻譯，但可以以最新內容更新。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻譯提供者</td>
   <td>選擇要執行翻譯的翻譯提供程式。 安裝相應連接器時，提供者會出現在清單中。</td>
  </tr>
  <tr>
   <td>內容類別</td>
   <td>（僅限機器翻譯）描述要翻譯內容的類別。 翻譯內容時，類別可能會影響術語和措辭的選擇。</td>
  </tr>
  <tr>
   <td>翻譯標記</td>
   <td>選取「 」即可轉譯與頁面相關聯的標籤。</td>
  </tr>
  <tr>
   <td>翻譯頁面資產</td>
   <td><p>選取如何轉譯從檔案系統新增至元件或從資產參考的資產：</p>
    <ul>
     <li>請勿翻譯：頁面資產不會翻譯。</li>
     <li>使用網站翻譯工作流程：系統會根據Sites標籤上的設定屬性來處理資產。</li>
     <li>使用資產翻譯工作流程：系統會根據「資產」標籤上屬性的設定來處理資產。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>自動執行翻譯</td>
   <td>選擇以在建立翻譯項目後自動執行翻譯作業。 選擇此選項時，您沒有機會複查和調整翻譯工作的範圍。</td>
  </tr>
 </tbody>
</table>

### Communities配置屬性 {#communities-configuration-properties}

Communities屬性可控制如何執行使用者產生的內容翻譯。 翻譯使用者產生的內容一律使用機器翻譯。 如需詳細資訊，請參閱[轉譯使用者產生的內容](/help/communities/translate-ugc.md)。

| 屬性 | 說明 |
|---|---|
| 翻譯提供者 | 選擇要執行翻譯的翻譯提供程式。 建立雲配置的提供程式將顯示在清單中。 |
| 內容類別 | 描述要翻譯的內容的類別。 翻譯內容時，類別可能會影響術語和措辭的選擇。 |
| 選擇要用作全局共用儲存的區域設定 | （可選）選擇儲存UGC的地區設定後，來自所有語言副本的貼文將出現在一個全域對話中。 根據慣例，為網站的[基語](/help/communities/sites-console.md#translation)選擇語言環境。 選擇「不共用儲存」將禁用全局翻譯。 預設情況下，全局翻譯將被禁用。 |

### Assets設定屬性 {#assets-configuration-properties}

資產屬性可控制如何設定資產。 如需轉譯資產的詳細資訊，請參閱[建立資產的語言副本](/help/assets/translation-projects.md)。

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>轉換工作流程</td>
   <td><p>選取架構對資產執行的轉譯類型：</p>
    <ul>
     <li>機器翻譯：翻譯提供者使用機器翻譯立即執行翻譯。</li>
     <li>人類翻譯：內容會自動傳送至翻譯提供者，以供手動翻譯。 </li>
     <li>不翻譯：不會傳送資產以進行翻譯。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻譯提供者</td>
   <td>選擇要執行翻譯的翻譯提供程式。 安裝相應連接器時，提供者會出現在清單中。</td>
  </tr>
  <tr>
   <td>內容類別</td>
   <td>（僅限機器翻譯）描述要翻譯內容的類別。 翻譯內容時，類別可能會影響術語和措辭的選擇。</td>
  </tr>
  <tr>
   <td>翻譯資產</td>
   <td>選取「 」，在翻譯專案中納入資產。 </td>
  </tr>
  <tr>
   <td>翻譯中繼資料</td>
   <td>選取「 」以轉譯資產中繼資料。</td>
  </tr>
  <tr>
   <td>翻譯標記</td>
   <td>選取「 」以轉換與資產相關聯的標籤。</td>
  </tr>
  <tr>
   <td>自動執行翻譯</td>
   <td>選擇以在建立翻譯項目後自動執行翻譯作業。 選擇此選項時，您沒有機會複查或限定翻譯工作的範圍。</td>
  </tr>
 </tbody>
</table>

1. 在側欄中，按一下或點選「工具>作業>雲端>Cloud Services」。
1. 在「翻譯整合」區域中，是否已建立任何設定，會決定要顯示哪個連結：

   * 如果尚未建立任何設定，請按一下或點選「立即設定」。
   * 如果設定已存在，請按一下或點選「顯示設定」，然後按一下或點選「可用設定」旁的+連結。

1. 輸入設定的名稱，然後按一下或點選「建立」。
1. 在「網站」、「社群」和「資產」標籤上設定屬性，然後按一下或點選「確定」。

## 配置翻譯頁面 {#configuring-pages-for-translation}

若要配置將源頁面翻譯成其他語言，請將這些頁面與以下雲配置關聯：

* 將AEM連接至翻譯提供者的雲端設定。
* 配置翻譯詳細資訊的翻譯整合框架。

請注意，翻譯整合架構雲配置標識了用於連接到服務提供商的雲配置。 將源頁面與框架雲配置關聯時，該頁面必須與框架雲配置所使用的服務提供商雲配置關聯。

將頁面與雲配置關聯時，頁面的子體將繼承關聯。 例如，如果將/content/geometrixx/en/products頁面與翻譯整合架構相關聯，則產品頁面及其下方的所有頁面會根據架構進行翻譯。

如有需要，您可以在子代頁面上覆寫關聯。 例如，網站的內容大多與服裝有關。 不過，有一個分頁描述了公司。 網站的根頁面與「翻譯整合架構」相關聯，該架構會使用「服裝」類別指定機器翻譯。 描述公司的分支使用框架，該框架使用「一般」類別執行機器翻譯。

此外，對於頁面上的任何社區[SCF元件](/help/communities/scf.md)，用戶生成的內容(UGC)將包括用戶翻譯內容的能力。 如需詳細資訊，請參閱[轉譯使用者產生的內容](/help/communities/translate-ugc.md)。

### 將頁面與翻譯提供者關聯 {#associating-a-page-with-a-translation-provider}

將頁面與翻譯提供者建立關聯，您使用該提供者翻譯頁面和子代頁面。

1. 在Sites Console中，選取要設定的頁面，然後按一下或點選「檢視屬性」。
1. 按一下或點選「編輯」，然後按一下或點選「Cloud Services」標籤。
1. 按一下或點選「新增設定>翻譯整合」。
1. 選取要使用的翻譯提供者，然後按一下或點選「完成」。

### 將頁面與翻譯整合框架關聯 {#associating-pages-with-a-translation-integration-framework}

將頁面與定義您要如何執行頁面和子代頁面翻譯的翻譯整合框架相關聯。

1. 在Sites Console中，選取要設定的頁面，然後按一下或點選「檢視屬性」。
1. 按一下或點選「編輯」，然後按一下或點選「Cloud Services」標籤。
1. 按一下或點選「新增設定>翻譯整合」。
1. 選取要使用的翻譯整合架構，然後按一下或點選「完成」。
