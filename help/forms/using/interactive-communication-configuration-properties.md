---
title: 互動式通信配置屬性
seo-title: Interactive Communication configuration properties
description: 編輯Interactive Communications的預設配置屬性
seo-description: Edit default configuration properties for Interactive Communications
uuid: 4030078f-64a3-40bb-9892-49e22a8da561
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
discoiquuid: acb61d37-cd22-422e-bbf3-a2979b13ad41
docset: aem65
feature: Interactive Communication
exl-id: 09eeade6-e16d-4159-b26a-803c7201097a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 7%

---

# 互動式通信配置屬性{#interactive-communications-configuration-properties}

互動式通訊包括在安裝 [AEM Forms附加元件](../../forms/using/installing-configuring-aem-forms-osgi.md) 包。 互動式通訊作者可使用 **Adobe Experience Manager Web主控台設定** 頁面。

開啟 **Adobe Experience Manager Web主控台設定** 頁面的URL:

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

配置屬性包括：

* [檔案片段設定](#document-fragments-configuration)
* [建立通信配置](#create-correspondence-configuration)
* [最適化表單與互動式通訊Web通道設定](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [最適化表單與互動式通訊Web通道主題設定](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## 檔案片段設定 {#document-fragments-configuration}

點選 **檔案片段設定** 在 **Adobe Experience Manager Web主控台設定** 頁面，檢視檔案片段的設定屬性。

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
   <td>建立「打印」和「Web」通道的「互動式通信」時，可用的欄位、變數和表單資料模型元素的區域設定特定顯示格式。</td> 
   <td> 
    <ul> 
     <li>locale = en_US、de_DE、fr_FR和ja_JP</li> 
     <li>dateFormat = dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = 。</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>—</p> </td> 
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
   <td>數字最小寬度</td> 
   <td>在清單文檔片段中使用除羅馬數字之外的編號清單時，應應用於項目符號或編號欄位的最小寬度。</td> 
   <td>8.0mm</td> 
   <td>數字</td> 
  </tr> 
 </tbody> 
</table>

## 建立通信配置 {#create-correspondence-configuration}

點選 **建立通信配置** 在 **Adobe Experience Manager Web主控台設定** 頁面，查看代理UI的配置屬性。

<table>
 <tbody> 
  <tr> 
   <td>屬性</td> 
   <td>說明</td> 
   <td>預設</td> 
   <td>可接受的值</td> 
  </tr> 
  <tr> 
   <td>顯示要編輯的已解析內容</td> 
   <td>選取核取方塊，在編輯代理UI上的文字模組時顯示已解析的內容（實際值而非預留位置）。</td> 
   <td>未選擇</td> 
   <td>不適用</td> 
  </tr> 
  <tr> 
   <td>預覽期間套用浮水印</td> 
   <td>選中複選框，以在預覽模式下將水印應用到互動式通信的打印通道。</td> 
   <td>未選擇</td> 
   <td>不適用</td> 
  </tr> 
  <tr> 
   <td>啟用字型嵌入PDF</td> 
   <td><p>選中複選框以啟用PDF文檔中的嵌入字型。 選擇此選項後，可以在使用代理UI生成或預覽PDF文檔後嵌入新字型。 使用互動式通信的打印通道生成和預覽PDF文檔。</p> <p>如果在用於生成PDF的電腦上可用字型，並且在訪問PDF的客戶端電腦上不可用，則將字型嵌入到PDF文檔中非常有用。</p> <p>有關嵌入字型的詳細資訊，請參閱 <a href="../../forms/using/customize-text-editor.md" target="_blank">自訂文字編輯器</a>.</p> </td> 
   <td>未選擇</td> 
   <td>不適用</td> 
  </tr> 
 </tbody> 
</table>

## 最適化表單與互動式通訊Web通道設定 {#adaptive-form-and-interactive-communication-web-channel-configuration}

點選 **最適化表單與互動式通訊Web通道設定** 在 **Adobe Experience Manager Web主控台設定** 頁面，檢視適用性Forms和互動式通訊Web通道的設定屬性。 下表介紹了與Interactive Communications相關的屬性：

| 屬性 | 說明 | 預設 | 可接受的值 |
|---|---|---|---|
| 顯示佔位符 | 選取核取方塊，即可針對適用性表單和互動式通訊中包含的欄位顯示預留位置。 | 已選取 | 不適用 |
| 最大快取條目數 | 設定使用快取記憶體可擷取的最大適用性表單和互動式通訊數量。 | 100 | 數字 |
| 使檔案名稱唯一 | 選取核取方塊，在適用性Forms和互動式通訊中為包含作為附件的檔案指定唯一名稱。 | 未選擇 | 不適用 |

## 最適化表單與互動式通訊Web通道主題設定 {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

點選 **最適化表單與互動式通訊Web通道主題設定** 在 **Adobe Experience Manager Web主控台設定** 頁面，檢視適用性Forms和互動式通訊Web通道主題的設定屬性。

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
   <td>建立最適化Forms和互動式通訊時可用的字型清單。</td> 
   <td><p>喬治亞</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>影響</p> <p>Palatino Linotype</p> </td> 
   <td>所有有效的Adobe伺服器字型</td> 
  </tr> 
 </tbody> 
</table>
