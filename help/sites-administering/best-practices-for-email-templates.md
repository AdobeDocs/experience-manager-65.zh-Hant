---
title: 電子郵件範本最佳作法
seo-title: Best Practices for Email Templates
description: 了解在AEM中建立電子郵件範本的最佳實務。
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

# 電子郵件範本最佳作法 {#best-practices-for-email-templates}

>[!CAUTION]
>
>已棄用AEM電子郵件元件。 由於電子郵件的性質（可合併內容和樣式）,AEM提供的現成可用電子郵件元件對客戶的重複使用有限，因為需要將自訂樣式實施至專案所需的任何元件中。
>
>您可以在專案層級實作電子郵件元件，而過時的AEM電子郵件元件則說明如何達成此目標。 不過，這些已棄用的元件不應用於專案。

本檔案說明電子郵件設計的一些最佳實務，以建立完善的電子郵件行銷活動範本。

AEM中提供的示範行銷活動遵循所有這些最佳實務。 針對每個最佳實務，說明如何在示範行銷活動中實作最佳實務。

建立自己的電子報時，請使用這些最佳實務。

>[!NOTE]
>
>所有促銷活動內容應建立在 `master` 類型頁面 `cq/personalization/components/ambitpage`.
>
>例如，如果您的計畫促銷活動結構類似
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>您應確定它位於 `master` 頁面
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>為Adobe Campaign建立郵件範本時，您必須包含屬性 **acMapping** 值 **mapRecipient** 在 **jcr:content** 節點，或您將無法在 **頁面屬性** 的（欄位已停用）。

## 範本/頁面元件 {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>最佳實務</strong></td>
   <td><strong>實施</strong></td>
  </tr>
  <tr>
   <td><p>指定文檔類型以確保一致的呈現。</p> <p>在開頭添加DOCTYPE(HTML或XHTML)</p> </td>
   <td><p>可透過設計變更 <i>cq:doctype</i> 屬性<i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i></p> <p>預設為「XHTML」：</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>可變更為「HTML5」：</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>指定字元定義以確保正確呈現特殊字元。</p> <p>將CHARSET聲明（例如iso-8859-15、UTF-8）添加到 &lt;head&gt;</p> </td>
   <td><p>設為UTF-8。</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>使用 &lt;table&gt;元素。 對於更複雜的佈局，應嵌套表以構建複雜結構。</p> <p>即使沒有CSS，電子郵件也應該看起來不錯。</p> </td>
   <td><p>在整個範本中都會使用表格來建構內容。 目前最多使用四個巢狀表（1個基表+最大）。 3個嵌套級別)</p> <p>&lt;div&gt; 標籤只會在製作模式中使用，以確保能正確編輯元件。</p> </td>
  </tr>
  <tr>
   <td>使用元素屬性（例如儲存格邊框間距、驗證和寬度）來設定表格維度。 這會強制一個盒型結構。</td>
   <td><p>所有表都包含必要的屬性，如 <i>邊框</i>, <i>儲存</i>, <i>儲存空間</i> 和 <i>寬度</i>.</p> <p>為了協調表內的元素定位，所有表單元都具有屬性 <i>valign="top"</i> 正在設定。</p> </td>
  </tr>
  <tr>
   <td><p>如果可能的話，可以考慮移動友好性。 使用媒體查詢增加小螢幕上的文字大小，為連結提供縮圖大小的點擊區域。</p> <p>如果設計允許，請讓電子郵件回應。</p> </td>
   <td>就CSS樣式來說明示範設計而言，媒體查詢可用來提供適合行動裝置的版本。</td>
  </tr>
  <tr>
   <td>內嵌CSS比將所有CSS放在開頭好。</td>
   <td><p>為了更妥善地展示基礎HTML結構，並簡化自訂電子報結構的可能性，僅內嵌部分CSS定義。</p> <p>基本樣式和範本變異已擷取至 &lt;head&gt; 頁面的下一個頁面。 在最終提交電子報時，這些CSS定義應內嵌在HTML中。 已規劃自動啟用機制，但目前不可用。</p> </td>
  </tr>
  <tr>
   <td>讓CSS保持簡單。 避免複合樣式聲明、速記代碼、CSS佈局屬性、複雜的選取器和偽元素。</td>
   <td>就CSS樣式來說明示範設計而言，會遵循CSS建議。</td>
  </tr>
  <tr>
   <td>電子郵件的寬度上限應為600-800像素。 這樣，在許多用戶端提供的預覽窗格大小內，它們的行為就會更好。</td>
   <td>此 <i>寬度</i> 在示範設計中，內容表格的上限為600px。</td>
  </tr>
 </tbody>
</table>

### 影像 {#images}

/libs/mcm/campaign/components/image

| **最佳實務** | **實施** |
|---|---|
| 新增 *alt* 屬性至影像 | 此 *alt* 屬性已定義為影像元件的必要屬性。 |
| 使用 *jp* 而非 *png* 影像格式 | 影像元件一律會將影像當作JPG。 |
| 使用 `<img>` 元素，而非表格中的背景影像。 | 範本中未使用背景影像資料。 |
| 在圖片上添加屬性style=&quot;display block&quot;。 可在Gmail上正常顯示。 | 預設情況下，所有影像都包含 *style=&quot;display block&quot;* 屬性。 |

### 文字和連結 {#text-and-links}

/libs/mcm/campaign/components/heading, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>最佳實務</strong></td>
   <td><strong>實施</strong></td>
  </tr>
  <tr>
   <td>在CSS中使用html而非樣式(font-family)</td>
   <td>RichTextEditor（例如，在文本時間元件中）現在支援選擇字型系列和字型大小，並將其應用於選定文本。 它們會呈現為標記。</td>
  </tr>
  <tr>
   <td>使用基本、跨平台字型，例如 <i>阿里亞爾、韋爾達納、喬治亞</i> 和 <i>《泰晤士報新羅馬》</i>.</td>
   <td><p>取決於電子報設計。</p> <p>在示範設計中，字型「Helvetica」已使用，但若不存在，將回復為通用的無襯線字型。</p> </td>
  </tr>
 </tbody>
</table>

### 通用 {#generic}

| **最佳實務** | **實施** |
|---|---|
| 使用W3C驗證器來修正HTML程式碼。 請確定所有開啟的標籤皆已正確關閉。 | 代碼已驗證。 對於XHTML過渡Doctype，只有 `<html>` 元素遺失。 |
| 不需費心使用JavaScript或Flash，這些技術基本上不受電子郵件用戶端支援。 | 電子報範本中不使用JavaScript或Flash。 |
| 新增純文字版本以用於多部分傳送。 | 頁面屬性中已建置新介面工具集，以便輕鬆從頁面內容擷取純文字版本。 這可作為最終純文字版本的起點。 |

## 行銷活動電子報範本和範例 {#campaign-newsletter-templates-and-examples}

AEM隨附數個現成的範本和元件，供您建立campaign電子報。 您可以使用這些範本和元件來建立自訂電子報。

### 範本 {#templates}

為了提供堅實的基礎並擴大內容流的可能性，現成可用的範本類型稍有不同。 您可以輕鬆使用這些資料來建立自訂電子報。

都有 **標題**, **頁腳** 和 **身體** 區段。 在內文章節下方，每個範本的 **欄設計** （1、2或3欄）。

![](assets/chlimage_1-69.png)

### 元件 {#components}

目前有 [在行銷活動範本中可用的七個元件](/help/sites-authoring/adobe-campaign-components.md). 這些元件都基於Adobe標籤語言 **HTL**.

| **元件名稱** | **元件路徑** |
|---|---|
| 標題 | /libs/mcm/campaign/components/heading |
| 影像 | /libs/mcm/campaign/components/image |
| 文字和個人化 | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| 連結 | /libs/mcm/campaign/components/reference |
| Dynamic Media Classic(原稱Scene7)影像範本 | /libs/mcm/campaign/s7image |
| 目標參考 | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>這些元件針對郵件內容進行了優化；也就是說，他們遵守本檔案中概述的最佳實務。 使用其他現成可用的元件通常會違反這些規則。

這些元件在 [Adobe Campaign元件](/help/sites-authoring/adobe-campaign-components.md).
