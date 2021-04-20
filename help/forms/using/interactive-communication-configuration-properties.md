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
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 5%

---


# 交互通信配置屬性{#interactive-communications-configuration-properties}

Interactive Communications包含在安裝[AEM Forms附加程式包後自動配置的屬性。 ](../../forms/using/installing-configuring-aem-forms-osgi.md)Interactive Communication作者可以使用&#x200B;**Adobe Experience ManagerWeb控制台配置**&#x200B;頁編輯這些預設配置屬性。

使用以下URL開啟「Adobe Experience ManagerWeb控制台配置」頁：****

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

配置屬性包括：

* [檔案片段設定](#document-fragments-configuration)
* [建立對應配置](#create-correspondence-configuration)
* [自適應表單與互動式通訊Web頻道配置](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [自適應表單與互動式通訊Web頻道主題配置](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## 檔案片段設定{#document-fragments-configuration}

點選&#x200B;**Adobe Experience ManagerWeb控制台配置**&#x200B;頁面上的&#x200B;**文檔片段配置**&#x200B;以查看文檔片段的配置屬性。

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
   <td><p>—</p> </td> 
  </tr> 
  <tr> 
   <td>縮排</td> 
   <td>應用於清單文檔片段中文本的單個縮進單位的寬度。</td> 
   <td>12.7毫米</td> 
   <td>數量</td> 
  </tr> 
  <tr> 
   <td>羅馬數字最小寬度</td> 
   <td>在清單文檔片段中使用羅馬數字時，應應用於項目符號或數字欄位的最小寬度。 </td> 
   <td>12.7毫米</td> 
   <td>數量</td> 
  </tr> 
  <tr> 
   <td>最小寬度數</td> 
   <td>在清單文檔片段中使用編號清單（除羅馬數字外）時，應應用於項目符號或數字欄位的最小寬度。</td> 
   <td>8.0毫米</td> 
   <td>數量</td> 
  </tr> 
 </tbody> 
</table>

## 建立對應配置{#create-correspondence-configuration}

在&#x200B;**Adobe Experience ManagerWeb控制台配置**&#x200B;頁上按一下&#x200B;**建立對應配置**&#x200B;以查看代理UI的配置屬性。

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
   <td>選中該複選框可將水印應用於「預覽」模式下交互通信的打印通道。</td> 
   <td>未選擇</td> 
   <td>不適用</td> 
  </tr> 
  <tr> 
   <td>在PDF中啟用字型內嵌</td> 
   <td><p>選取核取方塊以啟用PDF檔案中的內嵌字型。 選取此選項後，您就可以在使用Agent UI產生或預覽PDF檔案後，嵌入新字型。 使用互動式通訊的列印頻道產生和預覽PDF檔案。</p> <p>如果用於產生PDF的機器上有字型，而用於存取PDF的用戶端機器上沒有字型，將字型內嵌在PDF檔案中就很有用。</p> <p>如需內嵌字型的詳細資訊，請參閱<a href="../../forms/using/customize-text-editor.md" target="_blank">自訂文字編輯器</a>。</p> </td> 
   <td>未選擇</td> 
   <td>不適用</td> 
  </tr> 
 </tbody> 
</table>

## 最適化表單與互動式通訊Web頻道設定{#adaptive-form-and-interactive-communication-web-channel-configuration}

在&#x200B;**Adobe Experience ManagerWeb控制台配置**&#x200B;頁上按一下&#x200B;**自適應表單和互動式通信Web通道配置** ，以查看自適應Forms和互動式通信Web通道的配置屬性。 下表說明與Interactive Communications相關的屬性：

| 屬性 | 說明 | 預設 | 可接受的值 |
|---|---|---|---|
| 顯示預留位置 | 選取核取方塊，可顯示最適化表單和互動式通訊中欄位的預留位置。 | 已選取 | 不適用 |
| 最大快取條目數 | 設定使用快取記憶體可檢索的最大自適應表單和互動式通信數。 | 100 | 數量 |
| 使檔案名稱唯一 | 選中該複選框，可在最適化Forms和互動式通信中為包含為附件的檔案提供唯一的名稱。 | 未選擇 | 不適用 |

## 最適化表單與互動式通訊Web頻道主題設定{#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

點選&#x200B;**Adobe Experience ManagerWeb控制台配置**&#x200B;頁上的&#x200B;**最適化表單和互動式通信Web通道主題配置**，查看最適化Forms和互動式通信Web通道主題的配置屬性。

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

