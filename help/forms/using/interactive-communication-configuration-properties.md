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

Interactive Communications包括在安裝 [AEM Forms附加](../../forms/using/installing-configuring-aem-forms-osgi.md) 檔案。 交互通信作者可以使用 **Adobe Experience ManagerWeb控制台配置** 的子菜單。

開啟 **Adobe Experience ManagerWeb控制台配置** 的子菜單：

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

配置屬性包括：

* [文檔片段配置](#document-fragments-configuration)
* [建立對應配置](#create-correspondence-configuration)
* [自適應形式與交互通信Web通道配置](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [自適應形式與交互通信Web通道主題配置](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## 文檔片段配置 {#document-fragments-configuration}

點擊 **文檔片段配置** 的 **Adobe Experience ManagerWeb控制台配置** 頁，查看文檔片段的配置屬性。

<table>
 <tbody> 
  <tr> 
   <td>屬性</td> 
   <td>說明</td> 
   <td>預設</td> 
   <td>可接受值</td> 
  </tr> 
  <tr> 
   <td>資料顯示格式</td> 
   <td>為打印和Web通道建立互動式通信時可用的欄位、變數和表單資料模型元素的區域設定特定的顯示格式。</td> 
   <td> 
    <ul> 
     <li>區域設定= en_US、de_DE、fr_FR和ja_JP</li> 
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
   <td>12.7mm</td> 
   <td>數字</td> 
  </tr> 
  <tr> 
   <td>羅馬數字最小寬度</td> 
   <td>在清單文檔片段中使用羅馬數字時，要應用於項目符號或數字欄位的最小寬度。 </td> 
   <td>12.7mm</td> 
   <td>數字</td> 
  </tr> 
  <tr> 
   <td>最小寬度</td> 
   <td>使用清單文檔片段中除羅馬字編號之外的編號清單時，要應用於項目符號或編號欄位的最小寬度。</td> 
   <td>8.0mm</td> 
   <td>數字</td> 
  </tr> 
 </tbody> 
</table>

## 建立對應配置 {#create-correspondence-configuration}

點擊 **建立對應配置** 的 **Adobe Experience ManagerWeb控制台配置** 頁，查看代理UI的配置屬性。

<table>
 <tbody> 
  <tr> 
   <td>屬性</td> 
   <td>說明</td> 
   <td>預設</td> 
   <td>可接受值</td> 
  </tr> 
  <tr> 
   <td>顯示已解析的內容以供編輯</td> 
   <td>選中該複選框可在編輯代理UI上的文本模組時顯示已解析的內容（實際值而不是佔位符）。</td> 
   <td>未選擇</td> 
   <td>不適用</td> 
  </tr> 
  <tr> 
   <td>預覽期間應用水印</td> 
   <td>選中該複選框可將水印應用於預覽模式下的互動式通信的打印通道。</td> 
   <td>未選擇</td> 
   <td>不適用</td> 
  </tr> 
  <tr> 
   <td>在PDF中啟用字型嵌入</td> 
   <td><p>選中複選框以啟用在PDF文檔中嵌入字型。 選擇此選項後，可以在使用代理UI生成或預覽PDF文檔後嵌入新字型。 使用互動式通信的打印通道生成和預覽PDF文檔。</p> <p>在PDF文檔中嵌入字型非常有用，如果用於生成PDF的電腦上有字型，而訪問PDF的客戶機上沒有字型，則嵌入字型非常有用。</p> <p>有關嵌入字型的詳細資訊，請參見 <a href="../../forms/using/customize-text-editor.md" target="_blank">自定義文本編輯器</a>。</p> </td> 
   <td>未選擇</td> 
   <td>不適用</td> 
  </tr> 
 </tbody> 
</table>

## 自適應形式與交互通信Web通道配置 {#adaptive-form-and-interactive-communication-web-channel-configuration}

點擊 **自適應形式與交互通信Web通道配置** 的 **Adobe Experience ManagerWeb控制台配置** 的子菜單。 下表介紹了與Interactive Communications相關的屬性：

| 屬性 | 說明 | 預設 | 可接受值 |
|---|---|---|---|
| 顯示佔位符 | 選中該複選框可為自適應表單和互動式通信中包含的欄位啟用佔位符顯示。 | 已選取 | 不適用 |
| 最大快取條目數 | 設定可使用快取記憶體檢索的最大自適應表單和互動式通信數。 | 100 | 數字 |
| 使檔案名唯一 | 選中該複選框可在Adaptive Forms和Interactive Communications中將檔案作為附件包含的唯一名稱。 | 未選擇 | 不適用 |

## 自適應形式與交互通信Web通道主題配置 {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

點擊 **自適應形式與交互通信Web通道主題配置** 的 **Adobe Experience ManagerWeb控制台配置** 的子菜單。

<table>
 <tbody> 
  <tr> 
   <td>屬性</td> 
   <td>說明</td> 
   <td>預設</td> 
   <td>可接受值</td> 
  </tr> 
  <tr> 
   <td>字型清單名稱</td> 
   <td>建立自適應Forms和互動式通信時可用的字型清單。</td> 
   <td><p>喬治亞</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>影響</p> <p>Palatino Linotype</p> </td> 
   <td>所有有效的Adobe伺服器字型</td> 
  </tr> 
 </tbody> 
</table>
