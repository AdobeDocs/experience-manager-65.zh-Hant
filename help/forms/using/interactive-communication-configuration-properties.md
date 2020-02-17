---
title: 互動式通訊設定屬性
seo-title: 互動式通信配置屬性
description: 編輯互動式通信的預設配置屬性
seo-description: 編輯互動式通信的預設配置屬性
uuid: 4030078f-64a3-40bb-9892-49e22a8da561
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
discoiquuid: acb61d37-cd22-422e-bbf3-a2979b13ad41
docset: aem65
translation-type: tm+mt
source-git-commit: a326e508a781b3afaba8b5e371aa862a30536740

---


# 互動式通訊設定屬性{#interactive-communications-configuration-properties}

Interactive Communications包含在安裝 [AEM Forms附加元件套件後自動設定的屬性](../../forms/using/installing-configuring-aem-forms-osgi.md) 。 「互動式通訊」作者可以使用 **Adobe Experience Manager Web Console的「設定」頁面來編輯這些預設設定屬性** 。

使用 **下列URL開啟Adobe Experience Manager Web Console設定頁** :

`https://&lt;server&gt;:&lt;port&gt;/&lt;contextPath&gt;/system/console/configMgr`

配置屬性包括：

* [檔案片段設定](#document-fragments-configuration)
* [建立對應配置](#create-correspondence-configuration)
* [自適應表單與互動式通訊Web頻道配置](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [自適應表單與互動式通訊Web頻道主題配置](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## 檔案片段設定 {#document-fragments-configuration}

在 **Adobe Experience Manager Web Console的「設定」頁面上，點選「檔案片段設定」****** ，以檢視檔案片段的設定屬性。

<table>
 <tbody> 
  <tr> 
   <td>屬性</td> 
   <td>說明</td> 
   <td>預設</td> 
   <td>可接受的值</td> 
  </tr> 
  <tr> 
   <td>資料顯示格式</td> 
   <td>建立適用於列印和網頁頻道的互動式通訊時，欄位、變數和表單資料模型元素的地區設定特定顯示格式。</td> 
   <td> 
    <ul> 
     <li>locale = en_US、de_DE、fr_FR和ja_JP</li> 
     <li>dateFormat = dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator =,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>--</p> </td> 
  </tr> 
  <tr> 
   <td>縮排</td> 
   <td>應用於清單文檔片段中文本的單個縮進單位的寬度。</td> 
   <td>12.7mm</td> 
   <td>數字</td> 
  </tr> 
  <tr> 
   <td>羅馬數字最小寬度</td> 
   <td>在清單文檔片段中使用羅馬數字時，應應用於項目符號或數字欄位的最小寬度。 </td> 
   <td>12.7mm</td> 
   <td>數字</td> 
  </tr> 
  <tr> 
   <td>最小寬度數</td> 
   <td>在清單文檔片段中使用編號清單（除羅馬數字外）時，應應用於項目符號或數字欄位的最小寬度。</td> 
   <td>8.0mm</td> 
   <td>數字</td> 
  </tr> 
 </tbody> 
</table>

## 建立對應配置 {#create-correspondence-configuration}

在 **Adobe Experience Manager Web Console的「設定」頁面上，點選「建立對應設定」****** ，以檢視Agent UI的設定屬性。

<table>
 <tbody> 
  <tr> 
   <td>屬性</td> 
   <td>說明</td> 
   <td>預設</td> 
   <td>可接受的值</td> 
  </tr> 
  <tr> 
   <td>顯示已解析的內容以進行編輯</td> 
   <td>選取核取方塊，在編輯Agent UI上的文字模組時顯示已解析的內容（實際值而非預留位置）。</td> 
   <td>未選擇</td> 
   <td>不適用</td> 
  </tr> 
  <tr> 
   <td>預覽時套用浮水印</td> 
   <td>選中該複選框可將水印應用於「預覽」模式下互動式通信的打印通道。</td> 
   <td>未選擇</td> 
   <td>不適用</td> 
  </tr> 
  <tr> 
   <td>在PDF中啟用字型內嵌</td> 
   <td><p>選取核取方塊以啟用PDF檔案中的內嵌字型。 選取此選項後，您就可以在使用Agent UI產生或預覽PDF檔案後，嵌入新字型。 使用互動式通訊的列印頻道產生和預覽PDF檔案。</p> <p>如果用於產生PDF的機器上有字型，而用於存取PDF的用戶端機器上沒有字型，將字型內嵌在PDF檔案中就很有用。</p> <p>如需內嵌字型的詳細資訊，請參閱「自 <a href="../../forms/using/customize-text-editor.md" target="_blank">訂文字編輯器」</a>。</p> </td> 
   <td>未選擇</td> 
   <td>不適用</td> 
  </tr> 
 </tbody> 
</table>

## 自適應表單與互動式通訊Web頻道配置 {#adaptive-form-and-interactive-communication-web-channel-configuration}

在 ******** Adobe Experience Manager Web Console的「設定」頁面上，點選「最適化表單與互動式通訊Web頻道設定」，以檢視最適化表單與互動式通訊Web頻道的設定屬性。 下表說明與Interactive Communications相關的屬性：

| 屬性 | 說明 | 預設 | 可接受的值 |
|---|---|---|---|
| 顯示預留位置 | 選取核取方塊，可顯示最適化表單和互動式通訊中欄位的預留位置。 | 已選取 | 不適用 |
| 最大快取條目數 | 設定使用快取記憶體可檢索的最大自適應表單和互動式通信數。 | 100 | 數字 |
| 使檔案名稱唯一 | 選中該複選框，可在最適化表單和互動式通信中為作為附件包含的檔案提供唯一的名稱。 | 未選擇 | 不適用 |

## 自適應表單與互動式通訊Web頻道主題配置 {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

在 ******** Adobe Experience Manager Web Console的「設定」頁面上，點選「最適化表單與互動式通訊Web頻道主題設定」，以檢視最適化表單與互動式通訊Web頻道主題的設定屬性。

<table>
 <tbody> 
  <tr> 
   <td>屬性</td> 
   <td>說明</td> 
   <td>預設</td> 
   <td>可接受的值</td> 
  </tr> 
  <tr> 
   <td>字型清單名稱</td> 
   <td>建立最適化表單和互動式通訊時可用的字型清單。</td> 
   <td><p>喬治亞</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>影響</p> <p>Palatino Linotype</p> </td> 
   <td>所有有效的Adobe伺服器字型</td> 
  </tr> 
 </tbody> 
</table>

