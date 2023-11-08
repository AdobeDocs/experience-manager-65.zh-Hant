---
title: 設定翻譯整合框架
description: 瞭解如何在Adobe Experience Manager中設定翻譯整合架構。
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 7562754b-d9fd-441b-8ae5-c7eebe458cef
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 5%

---

# 設定翻譯整合框架{#configuring-the-translation-integration-framework}

翻譯整合框架會與協力廠商翻譯服務整合，以協調AEM內容的翻譯。

* 連接到您的翻譯服務提供者。
* 建立翻譯整合框架設定。
* 將雲端設定與您的頁面建立關聯。

如需AEM內容翻譯功能的總覽，請參閱 [翻譯多語言網站的內容](/help/sites-administering/translation.md).

## 連接到翻譯服務提供者 {#connecting-to-a-translation-service-provider}

建立雲端設定，將AEM連線至您的翻譯服務提供者。 AEM預設包括連線至Microsoft Translator的功能。
以下翻譯廠商為翻譯專案提供新API的實作。 深入瞭解整合的連結：

* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html) (AdobeExchange主要合作夥伴)
* [Clay平板電腦技術](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Cloudwords](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [XTM Cloud](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [Lingopek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [RWS](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108277.html)
* [Smartling](https://www.smartling.com/software/integrations/adobe-experience-manager/)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)
* [Altlang](https://exchange.adobe.com/experiencecloud.details.90222.altlang.html)
* Microsoft (AEM中已預先安裝Microsoft Translator)

>[!NOTE]
>
>若要尋找最新的人工和機器翻譯提供者清單，請檢視以下頁面：
>
>
>* [AEM人工翻譯](https://www.adobe.com/go/aem-human-translation-connectors)
>* [AEM機器翻譯](https://www.adobe.com/go/aem-machine-translation-connectors)
>

安裝聯結器套件後，您可以為聯結器建立雲端設定。 通常您需要提供認證來向翻譯服務進行驗證。 如需為Microsoft Translator聯結器新增雲端設定的詳細資訊，請參閱 [與Microsoft Translator整合](/help/sites-administering/tc-msconf.md).

您可以視需要為相同的聯結器建立多個雲端設定。 例如，為您在同一廠商的每個帳戶或專案建立一個設定。

設定連線後，您可以建立使用它的翻譯整合框架設定。

## 建立翻譯整合設定 {#creating-a-translation-integration-configuration}

建立翻譯整合框架設定，以指定如何翻譯您的內容。 設定包括以下資訊：

* 要使用哪個翻譯服務提供者.
* 是否進行人工翻譯或機器翻譯.
* 是否要翻譯與頁面或資產相關聯的其他內容，例如標籤。

建立框架設定後，請將雲端設定與您要根據該設定翻譯的頁面建立關聯。 開始翻譯流程時，翻譯工作流程會根據關聯的框架設定進行。

若您網站的不同區段有不同的翻譯需求，請據以建立多個框架設定。 例如，多語言網站包含英文、西班牙文和日文版本。 網站擁有者使用兩家不同的翻譯服務提供者提供西班牙文和日文翻譯。 因此，已設定框架的兩個設定。 每個設定使用不同的翻譯服務提供者。

設定翻譯整合框架後，您可以 [將其與頁面建立關聯](/help/sites-administering/tc-prep.md) 使用它的使用者。

**注意：** 如需AEM內容翻譯功能的總覽，請參閱 [翻譯多語言網站的內容](/help/sites-administering/translation.md).

此框架的單一設定可控制如何翻譯頁面內容、社群內容和資產。
![chlimage_1-386](assets/translation-config-65.jpg)

### 網站組態屬性 {#sites-configuration-properties}

Sites屬性可控制執行頁面內容翻譯的方式。

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>轉換工作流程</td>
   <td><p>選取框架為網站內容執行的翻譯方法：</p>
    <ul>
     <li>機器翻譯：翻譯提供者會使用機器翻譯即時執行翻譯。</li>
     <li>人工翻譯：內容會傳送給翻譯提供者，以供譯者翻譯。 </li>
     <li>不翻譯：不會傳送內容以供翻譯。 這是為了略過某些不會翻譯但可以用最新內容更新的內容分支。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻譯提供者</td>
   <td>選取要執行翻譯的翻譯提供者。 安裝提供者的對應聯結器後，清單中就會顯示提供者。</td>
  </tr>
  <tr>
   <td>內容類別</td>
   <td>（僅限機器翻譯）說明您要翻譯之內容的類別。 翻譯內容時，類別可能會影響術語和措辭的選擇。</td>
  </tr>
  <tr>
   <td>翻譯元件字串</td>
   <td>選取此選項可轉譯與頁面相關之元件的元件字串。</td>
  </tr>
  <tr>
   <td>翻譯標記</td>
   <td>選取以翻譯與頁面關聯的標籤。</td>
  </tr>
  <tr>
   <td>翻譯頁面資產</td>
   <td><p>選取如何翻譯從檔案系統新增至元件或從Assets參照的資產：</p>
    <ul>
     <li>不翻譯：頁面資產不翻譯。</li>
     <li>使用網站翻譯工作流程：根據網站標籤上的設定屬性處理資產。</li>
     <li>使用資產翻譯工作流程：根據資產索引標籤上的屬性設定來處理資產。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>自動執行翻譯</td>
   <td>選取此選項可在建立翻譯專案後自動執行翻譯工作。 選擇此選項時，您沒有機會檢閱翻譯工作並設定其範圍。</td>
  </tr>
 </tbody>
</table>

### 社群組態屬性 {#communities-configuration-properties}

Communities屬性可控制如何執行使用者產生的內容翻譯。 翻譯使用者產生的內容一律會使用機器翻譯。 如需詳細資訊，請參閱 [翻譯使用者產生的內容](/help/communities/translate-ugc.md).

| 屬性 | 說明 |
|---|---|
| 翻譯提供者 | 選取要執行翻譯的翻譯提供者。 為其建立雲端設定的提供者會出現在清單中。 |
| 內容類別 | 說明您要翻譯之內容的類別。 翻譯內容時，類別可能會影響術語和措辭的選擇。 |
| 選擇要做為全域共用存放區的地區設定 | （選擇性）選取儲存UGC的語言環境，所有語言副本的貼文都會出現在同一個全域對話中。 依照慣例，選擇 [基本語言](/help/communities/sites-console.md#translation) 用於網站。 選擇「沒有通用存放區」會停用全域轉譯。 預設會停用全域翻譯。 |

### 資產設定屬性 {#assets-configuration-properties}

資產屬性可控制如何設定資產。 如需有關轉譯資產的詳細資訊，請參閱 [建立資產的語言副本](/help/assets/translation-projects.md).

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>轉換工作流程</td>
   <td><p>選取框架為資產執行的翻譯型別：</p>
    <ul>
     <li>機器翻譯：翻譯提供者會使用機器翻譯立即執行翻譯。</li>
     <li>人工翻譯：內容會自動傳送給翻譯提供者，以供手動翻譯。 </li>
     <li>不翻譯：不會傳送資產以供翻譯。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻譯提供者</td>
   <td>選取要執行翻譯的翻譯提供者。 安裝提供者的對應聯結器後，清單中就會顯示提供者。</td>
  </tr>
  <tr>
   <td>內容類別</td>
   <td>（僅限機器翻譯）說明您要翻譯之內容的類別。 翻譯內容時，類別可能會影響術語和措辭的選擇。</td>
  </tr>
  <tr>
   <td>翻譯資產</td>
   <td>選取以在翻譯專案中包含資產。 </td>
  </tr>
  <tr>
   <td>翻譯中繼資料</td>
   <td>選取以翻譯資產中繼資料。</td>
  </tr>
  <tr>
   <td>翻譯標記</td>
   <td>選取以翻譯與資產相關聯的標籤。</td>
  </tr>
  <tr>
   <td>自動執行翻譯</td>
   <td>選取此選項可在建立翻譯專案後自動執行翻譯工作。 選擇此選項時，您沒有機會檢閱翻譯工作或劃定其範圍。</td>
  </tr>
 </tbody>
</table>

1. 在側邊欄中，按一下或點選「 Tools > Operations > Cloud > Cloud Service 」。
1. 在「翻譯整合」區域中，是否已建立任何設定會決定要顯示的連結：

   * 如果尚未建立任何設定，請按一下或點選「立即設定」。
   * 如果設定已存在，請按一下或點選「 Show Configurations 」，然後按一下或點選「 Available Configurations 」旁邊顯示的+連結。

1. 輸入設定的名稱，然後按一下或點選「建立」。
1. 在「網站」、「社群」和「資產」標籤上設定屬性，然後按一下或點選「確定」。

## 設定頁面以供翻譯 {#configuring-pages-for-translation}

若要設定將來源頁面翻譯成其他語言的功能，請將這些頁面與下列雲端設定建立關聯：

* 用於將AEM連線到您的翻譯提供商的雲端設定。
* 可設定翻譯詳細資訊的翻譯整合架構。

翻譯整合框架雲端設定會識別要用於連線至服務提供者的雲端設定。 將來源頁面與框架雲端設定建立關聯時，該頁面必須與框架雲端設定使用的服務提供者雲端設定建立關聯。

將頁面與雲端設定建立關聯時，該頁面的子系會繼承該關聯。 例如，如果您將/content/geometrixx/en/products頁面與翻譯整合框架建立關聯，產品頁面及其下方的所有頁面就會根據該框架進行翻譯。

必要時，您可以覆寫子代頁面上的關聯。 例如，網站的內容大多與服裝有關。 不過，其中一個頁面分支會說明公司。 網站的根頁面與指定使用「服飾」類別進行機器翻譯的翻譯整合架構相關聯。 說明公司的分支使用框架，該框架會使用「一般」類別執行機器翻譯。

此外，適用於任何社群 [SCF元件](/help/communities/scf.md) 在頁面上，使用者產生的內容(UGC)將包含使用者翻譯內容的能力。 如需詳細資訊，請參閱 [翻譯使用者產生的內容](/help/communities/translate-ugc.md).

### 將頁面與翻譯提供者建立關聯 {#associating-a-page-with-a-translation-provider}

將頁面與您用來翻譯頁面和後代頁面的翻譯提供者建立關聯。

1. 在網站主控台中，選取要設定的頁面，然後按一下或點選「檢視屬性」 。
1. 按一下或點選「編輯」，然後按一下或點選「Cloud Service」標籤。
1. 按一下或點選「新增設定>翻譯整合」。
1. 選取要使用的翻譯提供者，然後按一下或點選「完成」。

### 將頁面與翻譯整合框架建立關聯 {#associating-pages-with-a-translation-integration-framework}

將頁面與定義您要如何執行頁面和後代頁面翻譯的翻譯整合框架建立關聯。

1. 在網站主控台中，選取要設定的頁面，然後按一下或點選「檢視屬性」 。
1. 按一下或點選「編輯」，然後按一下或點選「Cloud Service」標籤。
1. 按一下或點選「新增設定>翻譯整合」。
1. 選取要使用的翻譯整合架構，然後按一下或點選「完成」。
