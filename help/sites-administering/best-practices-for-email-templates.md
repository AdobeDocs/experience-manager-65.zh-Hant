---
title: 電子郵件模板的最佳做法
seo-title: Best Practices for Email Templates
description: 查找中有關建立電子郵件模板的最佳AEM做法。
seo-description: Find best practices on creating email templates in AEM.
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
exl-id: 6666eddc-dc17-4bd4-9d55-e6522f40a680
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 1%

---

# 電子郵件模板的最佳做法 {#best-practices-for-email-templates}

>[!CAUTION]
>
>電子AEM郵件元件已棄用。 由於電子郵件的性質，即內容和樣式的合併，現成提供的電子郵件元件對客戶的重用變得有限AEM，因為需要將自定義樣式實施到項目所需的任何元件中。
>
>電子郵件元件可以在項目級別上實施，不建議使用的AEM電子郵件元件說明了如何實現這一點。 但是，不應在項目中使用這些已過時的元件。

本文檔介紹一些有關電子郵件設計的最佳做法，最終生成了一個完善的電子郵件活動模板。

中提供的演示活AEM動遵循了所有這些最佳做法。 介紹了在演示活動中如何實施最佳實踐，以便瞭解每種最佳實踐。

在建立您自己的新聞稿時，請使用這些最佳做法。

>[!NOTE]
>
>應在 `master` 類型頁 `cq/personalization/components/ambitpage`。
>
>例如，如果計畫的促銷活動結構類似
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>應確保它位於 `master` 頁
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>為Adobe Campaign建立郵件模板時，必須包括該屬性 **acMapping** 值 **mapRecipient** 的 **jcr：內容** 節點，或者您無法在 **頁面屬性** { 0AEM}。

## 模板/頁面元件 {#template-page-component}

***/libs/mcm/camping/components/campaigment_ewlestterpage***

<table>
 <tbody>
  <tr>
   <td><strong>最佳實踐</strong></td>
   <td><strong>實施</strong></td>
  </tr>
  <tr>
   <td><p>指定文檔類型以確保一致的呈現。</p> <p>在開頭添加DOCTYPE(HTML或XHTML)</p> </td>
   <td><p>可通過設計更改 <i>cq:doctype</i> 物業<i>"/etc/designs/default/jcr:content/campaigment_ellestripage"</i></p> <p>預設值為"XHTML":</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>可以更改為「HTML5」：</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>指定字元定義以確保正確呈現特殊字元。</p> <p>將CHARSET聲明（例如iso-8859-15、UTF-8）添加到 &lt;head&gt;</p> </td>
   <td><p>設定為UTF-8。</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>使用 &lt;table&gt;的子菜單。 對於更複雜的佈局，應嵌套表以構建複雜結構。</p> <p>即使沒有CSS，電子郵件也應該看起來不錯。</p> </td>
   <td><p>表在整個模板中用於構建內容。 當前使用最多四個嵌套表（1個基表+最大）。 3個嵌套級別)</p> <p>&lt;div&gt; 標籤僅在作者模式下使用，以確保正確編輯元件。</p> </td>
  </tr>
  <tr>
   <td>使用元素屬性（如單元格填充、驗證和寬度）來設定表維。 這將強制使用框模型結構。</td>
   <td><p>所有表都包含必要的屬性，如 <i>邊界</i>。 <i>單元格填充</i>。 <i>細胞間距</i> 和 <i>寬度</i>。</p> <p>要協調表內的元素定位，所有表單元格都具有屬性 <i>valign="top"</i> 正在設定。</p> </td>
  </tr>
  <tr>
   <td><p>如果可能的話，說明移動友好。 使用媒體查詢來增加小螢幕上的文本大小，為連結提供拇指大小的點擊區域。</p> <p>如果設計允許，請立即發送電子郵件。</p> </td>
   <td>就CSS樣式用於演示設計而言，媒體查詢用於提供移動友好版本。</td>
  </tr>
  <tr>
   <td>內聯CSS比將所有CSS放在開頭要好。</td>
   <td><p>為了更好地演示底層HTML結構，並簡化自定義新聞稿結構的可能性，只嵌入了一些CSS定義。</p> <p>基本樣式和模板變體已提取到 &lt;head&gt; 的下界。 在最後提交新聞稿時，這些CSS定義應嵌入HTML。 已計畫自動安裝機制，但目前不可用。</p> </td>
  </tr>
  <tr>
   <td>保持CSS簡單。 避免複合樣式聲明、速記代碼、CSS佈局屬性、複雜選擇器和偽元素。</td>
   <td>就CSS樣式用於演示設計而言，將遵循CSS建議。</td>
  </tr>
  <tr>
   <td>電子郵件的最大寬度應為600-800像素。 這樣，在許多客戶端提供的預覽窗格大小內，它們的行為會更好。</td>
   <td>的 <i>寬度</i> 在演示設計中，內容表限制為600px。</td>
  </tr>
 </tbody>
</table>

### 影像 {#images}

/libs/mcm/camping/components/image

| **最佳實踐** | **實施** |
|---|---|
| 添加 *按住* 影像的屬性 | 的 *按住* 屬性已定義為映像元件的必需屬性。 |
| 使用 *圖* 而不是 *png* 影像格式 | 影像元件始終將影像用作JPG。 |
| 使用 `<img>` 元素，而不是表中的背景影像。 | 模板中不使用背景影像資料。 |
| 在圖片上添加屬性style=&quot;display block&quot;。 允許在Gmail上顯示良好。 | 預設情況下，所有映像包含 *style=&quot;顯示塊&quot;* 屬性。 |

### 文本和連結 {#text-and-links}

/libs/mcm/camm/camp/component/heading//libs/mcm/camm/camp/compents/textimage//compent/compents/textimage//compents/textimage

<table>
 <tbody>
  <tr>
   <td><strong>最佳實踐</strong></td>
   <td><strong>實施</strong></td>
  </tr>
  <tr>
   <td>在CSS(字型系列)中使用html而不是樣式</td>
   <td>RichTextEditor（例如，在文本時間元件中）現在支援選擇並將font-families和font-sizes應用到所選文本。 它們將呈現為標記。</td>
  </tr>
  <tr>
   <td>使用基本的跨平台字型，如 <i>宋體，宋體，喬治亞州</i> 和 <i>《時代新羅馬》</i>。</td>
   <td><p>取決於新聞稿的設計。</p> <p>對於演示設計，使用字型"Helvetica"，但如果不存在，將回退到普通的無襯線字型。</p> </td>
  </tr>
 </tbody>
</table>

### 通用 {#generic}

| **最佳實踐** | **實施** |
|---|---|
| 使用W3C驗證程式更正HTML代碼。 確保所有開啟的標籤都正確關閉。 | 代碼已驗證。 對於XHTML過渡Doctype，僅缺少的xmlns屬性 `<html>` 缺少元素。 |
| 不要為JavaScript或Flash費心 — 這些技術基本上不受電子郵件客戶端的支援。 | 新聞稿模板中不使用JavaScript和Flash。 |
| 為多部件發送添加純文字檔案版本。 | 將新小部件構建到頁面屬性中，以便從頁面內容中輕鬆提取純文字檔案版本。 這可用作最終純文字檔案版本的起點。 |

## 市場活動新聞簡訊模板和示例 {#campaign-newsletter-templates-and-examples}

隨附AEM了多種模板和元件，供您建立市場活動新聞稿。 您可以使用這些模板和元件建立自定義新聞稿。

### 範本 {#templates}

為了提供堅實的基礎，並擴大內容流的可能性，出廠時提供了三種稍微不同的模板類型。 您可以輕鬆使用這些工具來構建定制新聞稿。

都有 **標題**&#x200B;的 **頁腳** 和 **體** 的子菜單。 在正文部分下，每個模板的不同之處 **柱設計** （1欄、2欄或3欄）。

![](assets/chlimage_1-69.png)

### 元件 {#components}

當前 [七個元件可用於市場活動模板](/help/sites-authoring/adobe-campaign-components.md)。 這些元件都基於Adobe標籤語言 **HTL**。

| **元件名稱** | **元件路徑** |
|---|---|
| 標題 | /libs/mcm/camp/compents/components/heading/ |
| 影像 | /libs/mcm/camping/components/image |
| 文字和個人化 | /libs/mcm/campaig/components/components/personalization//libs/mcm/campaig/components/components/personalization//personalization///libs/mcm/campag/components/personalization// |
| 文本時間 | /libs/mcm/campaig/components/textimage |
| 連結 | /libs/mcm/camping/components/reference |
| Dynamic Media Classic(前Scene7)影像模板 | /libs/mcm/camping/simage |
| 目標引用 | /libs/mcm/camping/components/reference |

>[!NOTE]
>
>這些元件針對郵件內容進行了優化；即，它們遵守本文檔中概述的最佳做法。 使用其他出廠設定元件通常會違反這些規則。

這些元件在 [Adobe Campaign元件](/help/sites-authoring/adobe-campaign-components.md)。
