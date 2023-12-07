---
title: 互動式通訊設定屬性
description: 編輯互動式通訊的預設設定屬性
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
docset: aem65
feature: Interactive Communication
exl-id: 09eeade6-e16d-4159-b26a-803c7201097a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 6%

---

# 互動式通訊設定屬性{#interactive-communications-configuration-properties}

互動式通訊包含安裝後自動設定的屬性 [AEM Forms附加元件](../../forms/using/installing-configuring-aem-forms-osgi.md) 封裝。 互動式通訊作者可使用下列工具來編輯這些預設設定屬性： **Adobe Experience Manager Web主控台設定** 頁面。

開啟 **Adobe Experience Manager Web主控台設定** 頁面使用下列URL：

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

設定屬性包括：

* [檔案片段設定](#document-fragments-configuration)
* [建立通訊設定](#create-correspondence-configuration)
* [最適化表單和互動式通訊Web頻道設定](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [最適化表單和互動式通訊Web Channel主題設定](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## 檔案片段設定 {#document-fragments-configuration}

選取 **檔案片段設定** 於 **Adobe Experience Manager Web主控台設定** 頁面以檢視檔案片段的設定屬性。

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
   <td>為列印和Web頻道建立互動式通訊時，可用的欄位、變數和表單資料模型元素的區域設定特定顯示格式。</td> 
   <td> 
    <ul> 
     <li>locale = en_US， de_DE， fr_FR和ja_JP</li> 
     <li>日期格式= dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = 。</li> 
     <li>numberGroupSeparator = ，</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>—</p> </td> 
  </tr> 
  <tr> 
   <td>縮排</td> 
   <td>套用至清單檔案片段中文字的單一縮排單位寬度。</td> 
   <td>12.7毫米</td> 
   <td>數字</td> 
  </tr> 
  <tr> 
   <td>羅馬數字最小寬度</td> 
   <td>在清單檔案片段中使用羅馬數字時，要套用至專案符號或數字欄位的最小寬度。 </td> 
   <td>12.7毫米</td> 
   <td>數字</td> 
  </tr> 
  <tr> 
   <td>數字最小寬度</td> 
   <td>在清單檔案片段中使用羅馬數字以外的編號清單時，要套用至專案符號或數字欄位的最小寬度。</td> 
   <td>8.0毫米</td> 
   <td>數字</td> 
  </tr> 
 </tbody> 
</table>

## 建立通訊設定 {#create-correspondence-configuration}

選取 **建立通訊設定** 於 **Adobe Experience Manager Web主控台設定** 頁面以檢視Agent UI的組態特性。

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
   <td>在代理程式UI上編輯文字模組時，選取核取方塊以顯示已解析的內容（實際值而非預留位置）。</td> 
   <td>未選取</td> 
   <td>不適用</td> 
  </tr> 
  <tr> 
   <td>在預覽期間套用浮水印</td> 
   <td>選取核取方塊，在預覽模式下將浮水印套用至互動式通訊的列印通道。</td> 
   <td>未選取</td> 
   <td>不適用</td> 
  </tr> 
  <tr> 
   <td>在PDF中啟用字型內嵌</td> 
   <td><p>選取核取方塊以啟用在PDF檔案中嵌入字型。 選取此選項後，您可在使用Agent UI產生或預覽PDF檔案後內嵌新字型。 使用互動式通訊的列印通道來產生和預覽PDF檔案。</p> <p>如果用於產生PDF的機器上有字型，而存取PDF的使用者端機器上沒有字型，則在PDF檔案中嵌入字型會很有用。</p> <p>如需內嵌字型的詳細資訊，請參閱 <a href="../../forms/using/customize-text-editor.md" target="_blank">自訂文字編輯器</a>.</p> </td> 
   <td>未選取</td> 
   <td>不適用</td> 
  </tr> 
 </tbody> 
</table>

## 最適化表單和互動式通訊Web頻道設定 {#adaptive-form-and-interactive-communication-web-channel-configuration}

選取 **最適化表單和互動式通訊Web頻道設定** 於 **Adobe Experience Manager Web主控台設定** 頁面以檢視最適化Forms和互動式通訊Web通道的設定屬性。 下表說明互動式通訊的相關特性：

| 屬性 | 說明 | 預設 | 可接受的值 |
|---|---|---|---|
| 顯示預留位置 | 選取核取方塊可啟用最適化表單和互動式通訊中所包含欄位的預留位置顯示。 | 已選取 | 不適用 |
| 快取專案上限 | 設定可使用快取記憶體擷取的最適化表單和互動式通訊數量上限。 | 100 | 數字 |
| 將檔案名稱設為唯一 | 選取核取方塊，以使Adaptive Forms和互動式通訊中作為附件包含的檔案名稱唯一。 | 未選取 | 不適用 |

## 最適化表單和互動式通訊Web Channel主題設定 {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

選取 **最適化表單和互動式通訊Web Channel主題設定** 於 **Adobe Experience Manager Web主控台設定** 頁面以檢視最適化Forms和互動式通訊Web頻道主題的設定屬性。

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
   <td>建立最適化Forms和互動式通訊時可使用的字型清單。</td> 
   <td><p>喬治亞</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>影響</p> <p>Palatino Linotype</p> </td> 
   <td>所有有效的Adobe伺服器字型</td> 
  </tr> 
 </tbody> 
</table>
