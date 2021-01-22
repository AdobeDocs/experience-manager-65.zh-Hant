---
title: 電子郵件範本的最佳做法
seo-title: 電子郵件範本的最佳做法
description: 尋找在AEM中建立電子郵件範本的最佳實務。
seo-description: 尋找在AEM中建立電子郵件範本的最佳實務。
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
translation-type: tm+mt
source-git-commit: 4333cfde433d00ddc4cb013b31fe52956791da46
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 1%

---


# 電子郵件範本的最佳做法{#best-practices-for-email-templates}

>[!CAUTION]
>
>AEM電子郵件元件已過時。 由於電子郵件的性質將內容與樣式合併，AEM提供的現成可用電子郵件元件對客戶的重複使用有限，因為客戶需要將自訂樣式建置在專案所需的任何元件中。
>
>電子郵件元件可在專案層級實作，而過時的AEM電子郵件元件則說明如何實現。 不過，這些已過時的元件不應用於專案。

本檔案說明電子郵件設計的一些最佳實務，以建立完備的電子郵件宣傳範本。

AEM中提供的示範促銷活動會遵循所有這些最佳實務。 針對每個最佳實務，說明如何在示範促銷活動中實作最佳實務。

建立您自己的電子報時，請使用這些最佳實務。

>[!NOTE]
>
>所有促銷活動內容都應建立在`master`類型`cq/personalization/components/ambitpage`的頁面下。
>
>例如，如果您的計畫促銷活動結構類似
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>您應確定它位於`master`頁面下方
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>建立Adobe Campaign的郵件範本時，您必須在範本的&#x200B;**jcr:content**&#x200B;節點中包含值&#x200B;**acMapping**&#x200B;的屬性&#x200B;**mapRecipient**，否則您將無法在&#x200B;**的「頁面屬性」**&#x200B;中選取Adobe Campaigampapaign範本aem（欄位已停用）。

## 範本／頁面元件{#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>最佳實務</strong></td>
   <td><strong>實施</strong></td>
  </tr>
  <tr>
   <td><p>指定檔案類型，以確保一致的轉譯。</p> <p>在開頭加入DOCTYPE（HTML或XHTML）</p> </td>
   <td><p>可透過設計變更<i>cq:doctype</i>屬性（位於<i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i>）來設定</p> <p>預設值為"XHTML":</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>可變更為「HTML_5」:</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>指定字元定義，以確保正確轉譯特殊字元。</p> <p>將CHARSET聲明（例如iso-8859-15、UTF-8）新增至&lt;head&gt;</p> </td>
   <td><p>設為UTF-8。</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>使用&lt;table&gt;元素對所有結構進行編碼。 對於更複雜的版面，您應巢狀內嵌表格以建立複雜的結構。</p> <p>即使沒有css，電子郵件看起來也不錯。</p> </td>
   <td><p>整個範本都使用表格來建構內容。 目前最多使用4個嵌套表（1個基表+最大）。 3個巢狀層級)</p> <p>&lt;div&gt; 標籤僅用於作者模式，以確保正確編輯元件。</p> </td>
  </tr>
  <tr>
   <td>使用元素屬性（例如儲存格填補、驗證和寬度）來設定表格尺寸。 這會強制使用框模型結構。</td>
   <td><p>所有表都包含必要的屬性，如<i>border</i>、<i>cellpadding</i>、<i>cellspacing</i>和<i>width</i>。</p> <p>為了協調表內的元素定位，所有表單元格都設定了屬性<i>valign="top"</i>。</p> </td>
  </tr>
  <tr>
   <td><p>說明行動友好性（如果可能）。 使用媒體查詢來增加小螢幕上的文字大小，並為連結提供拇指大小的點擊區域。</p> <p>在設計允許的情況下，讓電子郵件回應速度更快。</p> </td>
   <td>就CSS樣式來展示示範設計而言，媒體查詢可用來提供適用於行動裝置的版本。</td>
  </tr>
  <tr>
   <td>內嵌CSS比將所有CSS放在開頭要好。</td>
   <td><p>為了更好地展示基礎HTML結構，並簡化自訂電子報結構的可能性，只內嵌了部分CSS定義。</p> <p>基本樣式和範本變化已擷取至頁面&lt;head&gt;中的樣式區塊。 在最終提交電子報時，這些CSS定義應內嵌在HTML中。 已規劃自動啟動機制，但目前尚未推出。</p> </td>
  </tr>
  <tr>
   <td>讓CSS變得簡單。 避免複合樣式聲明、速記程式碼、CSS版面屬性、複雜的選擇器和偽元素。</td>
   <td>就CSS樣式用於展示示範設計而言，CSS建議仍在遵循中。</td>
  </tr>
  <tr>
   <td>電子郵件的寬度應為600-800像素。 這樣，在許多用戶端提供的預覽窗格大小中，他們的行為會更好。</td>
   <td>內容表格的<i>width</i>在示範設計中限制為600px。</td>
  </tr>
 </tbody>
</table>

### 影像 {#images}

/libs/mcm/campaign/components/image

| **最佳實務** | **實施** |
|---|---|
| 將&#x200B;*alt*&#x200B;屬性新增至影像 | *alt*&#x200B;屬性已定義為影像元件的必備屬性。 |
| 使用&#x200B;*jpg*&#x200B;取代&#x200B;*png*&#x200B;格式來處理影像 | 影像元件一律會以JPG格式提供影像。 |
| 請使用`<img>`元素，而非表格中的背景影像。 | 範本中未使用背景影像資料。 |
| 在圖片上新增屬性style=&quot;display block&quot;。 讓Gmail顯示更好。 | 所有影像都依預設包含&#x200B;*style=&quot;display block&quot;*&#x200B;屬性。 |

### 文字和連結{#text-and-links}

/libs/mcm/campaign/components/heading, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>最佳實務</strong></td>
   <td><strong>實施</strong></td>
  </tr>
  <tr>
   <td>在CSS中使用html &lt;font&gt;而非樣式(font-family)</td>
   <td>RichTextEditor（例如，在textimage元件中）現在支援選擇字型系列和字型大小並套用至選取的文字。 它們會呈現為&lt;font&gt;標籤。</td>
  </tr>
  <tr>
   <td>使用基本的跨平台字型，例如<i>Arial、Verdana、Georgia</i>和<i>Times New Roman</i>。</td>
   <td><p>視電子報設計而定。</p> <p>在示範設計中，使用「Helvetica」字型，但如果不存在，將返回一般的sans-serif字型。</p> </td>
  </tr>
 </tbody>
</table>

### 通用 {#generic}

| **最佳實務** | **實施** |
|---|---|
| 使用W3C驗證器來修正HTML程式碼。 請確定所有開啟的標籤都已正確關閉。 | 代碼已驗證。 對於XHTML過渡Doctype,`<html>`元素的缺少xmlns屬性。 |
| 不需費心使用JavaScript或Flash —— 這些技術基本上不受電子郵件用戶端支援。 | 電子報範本中不使用JavaScript和Flash。 |
| 新增純文字版本以傳送多部份。 | 頁面屬性中已內建新介面工具集，以輕鬆從頁面內容擷取明文版本。 這可做為最終明文版的起點。 |

## 促銷活動電子報範本和範例{#campaign-newsletter-templates-and-examples}

AEM隨附數個範本和元件，讓您建立促銷活動電子報。 您可以使用這些範本和元件來建立自訂電子報。

### 範本 {#templates}

為提供穩固的基礎並擴大內容流的各種可能性，現成可用的範本類型有三種稍微不同。 您可以輕鬆使用這些項目來建立自訂電子報。

所有檔案均具有&#x200B;**標題**、**頁尾**&#x200B;和&#x200B;**正文**&#x200B;部分。 在內文部分下方，每個範本在&#x200B;**欄設計**（1、2或3欄）中不同。

![](assets/chlimage_1-69.png)

### 元件 {#components}

目前有[7個元件可用於促銷活動範本](/help/sites-authoring/adobe-campaign-components.md)內。 這些元件都以Adobe標籤語言&#x200B;**HTL**&#x200B;為基礎。

| **元件名稱** | **元件路徑** |
|---|---|
| 標題 | /libs/mcm/campaign/components/heading |
| 影像 | /libs/mcm/campaign/components/image |
| 文字和個人化 | /libs/mcm/campaign/components/personalization |
| 文字貼文 | /libs/mcm/campaign/components/textimage |
| 連結 | /libs/mcm/campaign/components/reference |
| Dynamic Media Classic（之前稱為Scene7）影像範本 | /libs/mcm/campaign/s7image |
| 定位參考 | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>這些元件針對郵件內容進行了優化；也就是說，他們遵守本檔案中概述的最佳實務。 使用其他現成可用的元件通常會違反這些規則。

這些元件在[Adobe Campaign元件](/help/sites-authoring/adobe-campaign-components.md)中有詳細說明。