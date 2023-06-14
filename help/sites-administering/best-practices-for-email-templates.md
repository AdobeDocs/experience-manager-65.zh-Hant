---
title: 電子郵件範本的最佳實務
description: 尋找在AEM中建立電子郵件範本的最佳實務。
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
exl-id: 6666eddc-dc17-4bd4-9d55-e6522f40a680
source-git-commit: d673a447e9ce2377c8645c87f12be81cbad06238
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 1%

---

# 電子郵件範本的最佳實務 {#best-practices-for-email-templates}

>[!CAUTION]
>
>本文適用於已棄用的Foundation元件型AEM電子郵件元件。
>
>建議使用者使用現代的 [核心元件電子郵件元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html)

本檔案說明產生完善開發之電子郵件行銷活動範本的電子郵件設計相關最佳實務。

AEM提供的示範行銷活動會遵循所有這些最佳實務。 說明如何在示範行銷活動中實作最佳實務，以取得每個最佳實務。

在建立您自己的Newsletter時，請使用這些最佳實務。

>[!NOTE]
>
>所有行銷活動內容應建立在 `master` 型別頁面 `cq/personalization/components/ambitpage`.
>
>例如，如果您的計畫行銷活動結構類似於
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>確定它位在 `master` 頁面
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>為Adobe Campaign建立郵件範本時，您必須包含屬性 **acMapping** 包含值 **mapRecipient** 在 **jcr：content** 範本的節點。 如果沒有該範本，則無法選取Adobe Campaign範本於 **頁面屬性** Experience Manager（欄位已停用）。

## 範本/頁面元件 {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>最佳實務</strong></td>
   <td><strong>實施</strong></td>
  </tr>
  <tr>
   <td><p>指定檔案型別，以確保轉譯的一致性。</p> <p>在開頭新增DOCTYPE (HTML或XHTML)</p> </td>
   <td><p>可藉由設計變更來設定 <i>cq：doctype</i> 中的屬性<i>"/etc/designs/default/jcr：content/campaign_newsletterpage"</i></p> <p>預設值為「XHTML」：</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional/EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>可變更為「HTML_5」：</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>指定字元定義，以確保正確轉譯特殊字元。</p> <p>將CHARSET宣告（例如iso-8859-15、UTF-8）新增至 &lt;head&gt;</p> </td>
   <td><p>設為UTF-8。</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>使用「 」為所有結構編碼 &lt;table&gt;元素。 對於更複雜的版面，您應該巢狀內嵌表格，以建置複雜的結構。</p> <p>即使沒有CSS，電子郵件應該看起來不錯。</p> </td>
   <td><p>表格在整個範本中都會用來建構內容。 目前最多使用4個巢狀表格（1個基底表格+最多）。 3個巢狀層級)</p> <p>&lt;div&gt; 標籤僅用於製作模式，以確保元件可正確編輯。</p> </td>
  </tr>
  <tr>
   <td>使用元素屬性（例如單元格間距、垂直號和寬度）來設定表格尺寸。 此方法會強制使用方塊模型結構。</td>
   <td><p>所有表格都包含必要的屬性，例如 <i>邊框</i>， <i>單元格內距</i>， <i>單元格間距</i>、和 <i>寬度</i>.</p> <p>若要協調表格內的元素位置，所有表格儲存格都會有屬性 <i>valign=」top」</i> 已設定。</p> </td>
  </tr>
  <tr>
   <td><p>儘可能提供行動便利性。 使用媒體查詢來增加小熒幕上的文字大小，為連結提供縮圖大小的點選區域。</p> <p>如果設計允許，讓電子郵件回應式。</p> </td>
   <td>就目前使用CSS樣式來說明示範設計而言，媒體查詢可用來提供行動裝置相容的版本。</td>
  </tr>
  <tr>
   <td>內嵌CSS比將所有的CSS放在開頭要好。</td>
   <td><p>為了更妥善地展示基礎HTML結構以及更輕鬆地自訂電子報結構，僅內嵌部分CSS定義。</p> <p>已將基本樣式和範本變數擷取至中的樣式區塊 &lt;head&gt; 頁面的。 在最後提交Newsletter時，這些CSS定義會內嵌至HTML中。 已規劃自動內嵌機制，但目前無法使用。</p> </td>
  </tr>
  <tr>
   <td>保持您的CSS簡單。 避免使用複合樣式宣告、簡寫程式碼、CSS版面屬性、複雜選取器和虛擬元素。</td>
   <td>就目前使用CSS樣式來說明示範設計而言，我們遵循CSS建議。</td>
  </tr>
  <tr>
   <td>電子郵件的最大寬度應為600至800畫素。 此大小調整可讓它們在許多使用者端提供的預覽窗格大小內表現更佳。</td>
   <td>此 <i>寬度</i> 在示範設計中，內容表格的PDF限製為600畫素。</td>
  </tr>
 </tbody>
</table>

### 影像 {#images}

/libs/mcm/campaign/components/image

| **最佳實務** | **實施** |
|---|---|
| 新增 *alt* 影像的屬性 | 此 *alt* 屬性已定義為影像元件的必要屬性。 |
| 使用 *jpg* 而非 *png* 影像格式 | 影像元件一律會將影像當作JPG使用。 |
| 使用 `<img>` 元素，而非表格中的背景影像。 | 範本中不使用任何背景影像資料。 |
| 在圖片上新增attribute style=&quot;display block&quot;。 如此一來，它們就能在Gmail上正常顯示。 | 根據預設，所有影像包含 *style=&quot;display block&quot;* 屬性。 |

### 文字和連結 {#text-and-links}

/libs/mcm/campaign/components/heading， /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>最佳實務</strong></td>
   <td><strong>實施</strong></td>
  </tr>
  <tr>
   <td>在CSS (font-family)中使用html而非樣式</td>
   <td>RtfEditor （例如，文字文字元件中的）現在支援選擇字型系列和字型大小並套用至選取的文字。 它們會呈現為標籤。</td>
  </tr>
  <tr>
   <td>使用基本的跨平台字型，例如 <i>Arial®， Verdana， Georgia</i>、和 <i>Times New Roman®</i>.</td>
   <td><p>取決於Newsletter的設計。</p> <p>對於示範設計，會使用「Helvetica®」字型，但如果字型不存在，則會回覆為一般無襯線字型。</p> </td>
  </tr>
 </tbody>
</table>

### 通用 {#generic}

| **最佳實務** | **實施** |
|---|---|
| 使用W3C驗證器來修正HTML代碼。 請確定所有開啟的標籤皆已正確關閉。 | 程式碼已驗證。 僅適用於XHTML可轉換Doctype，遺失的xmlns屬性 `<html>` 元素遺失。 |
| 避免使用JavaScript或Flash — 這些技術通常不受電子郵件使用者端支援。 | Newsletter範本中未使用JavaScript或Flash。 |
| 新增純文字版本以進行多部分傳送。 | 頁面屬性中內建了新的Widget，以便輕鬆從頁面內容中擷取純文字版本。 您可以使用它作為最終純文字版本的起點。 |

## Campaign電子報範本和範例 {#campaign-newsletter-templates-and-examples}

AEM隨附數個現成的範本和元件，供您建立行銷活動電子報。 您可以使用這些範本和元件來建立自訂電子報。

### 範本 {#templates}

為了提供堅實的基礎，並擴大各種內容流動的可能性，現成可用的範本型別有三種稍有不同。 您可以使用這三種型別輕鬆建立自訂電子報。

所有都有 **頁首**， a **頁尾**，和 **內文** 區段。 在body區段的下方，每個範本都不同 **欄設計** （一、二或三欄）。

![](assets/chlimage_1-69.png)

### 元件 {#components}

目前有 [行銷活動範本內可用的七個元件](/help/sites-authoring/adobe-campaign-components.md). 這些元件都以Adobe標籤語言為基礎 **HTL**.

| **元件名稱** | **元件路徑** |
|---|---|
| 標題 | /libs/mcm/campaign/components/heading |
| 影像 | /libs/mcm/campaign/components/image |
| 文字和個人化 | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| 連結 | /libs/mcm/campaign/components/reference |
| Dynamic Media Classic (前身為Scene7)影像範本 | /libs/mcm/campaign/s7image |
| 目標引用 | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>這些元件已針對郵件內容最佳化；也就是說，它們遵循本檔案中概述的最佳實務。 使用其他現成可用的元件通常違反這些規則。

以下詳細說明了這些元件： [Adobe Campaign元件](/help/sites-authoring/adobe-campaign-components.md).
