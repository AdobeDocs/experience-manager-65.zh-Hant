---
title: 基於XDP的自適應形式中的XFA支援
seo-title: XFA support in XDP-based adaptive forms
description: 在自適應表單中列出支援的XFA事件、屬性、指令碼和驗證。
seo-description: Lists supported XFA events, properties, scripts, and validation in adaptive forms.
uuid: 75d3c292-cfed-438f-afdb-4071d95a08b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 05303b29-9058-4723-b134-4ba605fe40c7
docset: aem65
feature: Adaptive Forms
exl-id: 255be73f-3169-457c-aaa7-a2fb59f1f2cd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 5%

---

# 基於XDP的自適應形式中的XFA支援{#xfa-support-in-xdp-based-adaptive-forms}

## 簡介 {#introduction}

自適應表單支援在XDP檔案中定義的各種XFA事件、屬性、指令碼和驗證，包括：

* 執行在XDP檔案中的事件上定義的指令碼。
* 捕獲XDP檔案中欄位的預設值和行為屬性。
* 執行XDP檔案中定義的驗證指令碼。

當基於XDP檔案建立自適應表單時，屬性、事件和驗證將在創作UI表單中自動填充。 但是，表單作者可以覆蓋其中的一些元素以建立替代體驗。

本文列出了在自適應表單中遵守的受支援的XFA事件、屬性和驗證，並說明如何在自適應表單中覆蓋它們。

## 支援的XFA元素及其自適應形式的映射 {#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}

### 欄位 {#fields}

使用XDP檔案建立自適應表單時，可以將XFA欄位拖放到自適應表單上。 下表列出了XFA欄位如何映射到自適應表單欄位。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA欄位或容器</strong></p> </td>
   <td><p><strong>相應的自適應形狀元件</strong></p> </td>
  </tr>
  <tr>
   <td><p>按鈕 </p> </td>
   <td><p>按鈕</p> </td>
  </tr>
  <tr>
   <td><p>核取方塊 </p> </td>
   <td><p>核取方塊</p> </td>
  </tr>
  <tr>
   <td><p>清單框 </p> </td>
   <td><p>下拉式清單</p> </td>
  </tr>
  <tr>
   <td><p>日期/時間欄位 </p> </td>
   <td><p>日期挑選器</p> </td>
  </tr>
  <tr>
   <td><p>簽名Scribble</p> </td>
   <td><p>草寫簽名</p> </td>
  </tr>
  <tr>
   <td><p>數字欄位 </p> </td>
   <td><p>數值方塊</p> </td>
  </tr>
  <tr>
   <td><p>小數欄位</p> </td>
   <td><p>數值方塊</p> </td>
  </tr>
  <tr>
   <td><p>文字欄位 </p> </td>
   <td><p>文字方塊</p> </td>
  </tr>
  <tr>
   <td><p>密碼欄位 </p> </td>
   <td><p>密碼方塊</p> </td>
  </tr>
  <tr>
   <td><p>影像</p> </td>
   <td><p>影像</p> </td>
  </tr>
  <tr>
   <td><p>文字</p> </td>
   <td><p>文字</p> </td>
  </tr>
  <tr>
   <td><p>子窗體 </p> </td>
   <td><p>面板</p> </td>
  </tr>
  <tr>
   <td><p>區域（組）</p> </td>
   <td><p>面板</p> </td>
  </tr>
  <tr>
   <td><p>子窗體集 </p> </td>
   <td><p>面板</p> </td>
  </tr>
 </tbody>
</table>

### 屬性 {#properties}

下表捕獲了在XDP檔案中定義的各種XFA指令碼在自適應表單中的行為。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA元件屬性</strong></p> </td>
   <td><p><strong>自適應形式中的對應行為</strong></p> </td>
  </tr>
  <tr>
   <td><p>som表達式 </p> </td>
   <td><p>以自適應形式映射到Bind引用(bindRef)屬性。</p> </td>
  </tr>
  <tr>
   <td><p>存在 </p> </td>
   <td><p>以自適應形式映射到可見屬性。 可以使用「可見性」(Visibility)表達式覆蓋它。</p> </td>
  </tr>
  <tr>
   <td><p>訪問 </p> </td>
   <td><p>以自適應形式映射到enabled屬性。 可以使用Access表達式覆蓋它。</p> </td>
  </tr>
  <tr>
   <td><p>輔助功能：角色 </p> </td>
   <td><p>映射到自適應表單中的角色屬性。</p> </td>
  </tr>
  <tr>
   <td><p>輔助功能：講話優先順序 </p> </td>
   <td><p>以自適應形式映射到speakPriority屬性。</p> </td>
  </tr>
  <tr>
   <td><p>輔助功能：講話文本</p> </td>
   <td><p>以自適應形式映射到自定義輔助功能文本。</p> </td>
  </tr>
  <tr>
   <td><p>輔助功能：工具提示 </p> </td>
   <td><p>映射到自適應表單中的簡短描述屬性。</p> </td>
  </tr>
  <tr>
   <td><p>字幕<em> （所有欄位類型）</em></p> </td>
   <td><p>以自適應形式映射到Title屬性。</p> </td>
  </tr>
  <tr>
   <td><p>displayFormat<em> （所有欄位類型）</em></p> </td>
   <td><p>以自適應形式映射到「顯示模式」。</p> </td>
  </tr>
  <tr>
   <td><p>原始值<em> （所有欄位類型）</em></p> </td>
   <td><p>映射到自適應窗體中的值屬性。</p> </td>
  </tr>
  <tr>
   <td><p>項目<em> （清單框，複選框）</em></p> </td>
   <td><p>映射到自適應窗體中的選項屬性。 可以使用「選項」表達式覆蓋它。</p> </td>
  </tr>
  <tr>
   <td><p>最大字元<em> （文本欄位）</em></p> </td>
   <td><p>映射到自適應格式中允許的最大字元數屬性。</p> </td>
  </tr>
  <tr>
   <td><p>多線<em> （文本欄位）</em></p> </td>
   <td><p>以自適應形式映射到「允許多行」屬性。</p> </td>
  </tr>
  <tr>
   <td><p>frac數字<em> （數字欄位、小數欄位）</em></p> </td>
   <td><p>以自適應形式映射到Frac數字屬性。</p> </td>
  </tr>
  <tr>
   <td><p>leadDigit<em> （數字欄位、小數欄位）</em></p> </td>
   <td><p>以自適應形式映射到Lead digits屬性。</p> </td>
  </tr>
  <tr>
   <td><p>多選擇<em> （清單框）</em></p> </td>
   <td><p>映射到「允許多個選擇」屬性（以自適應形式）。</p> </td>
  </tr>
 </tbody>
</table>

### 指令碼 {#scripts}

下表捕獲了在XDP檔案中定義的各種XFA指令碼在自適應表單中的行為。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA指令碼事件</strong></p> </td>
   <td><p><strong>自適應形式中的對應行為</strong></p> </td>
  </tr>
  <tr>
   <td><p>初始化 </p> </td>
   <td><p>此指令碼在運行時執行，無法以自適應格式覆蓋。</p> </td>
  </tr>
  <tr>
   <td><p>計算</p> </td>
   <td><p>以自適應形式映射到「計算」表達式。</p> </td>
  </tr>
  <tr>
   <td><p>驗證 </p> </td>
   <td><p>以自適應形式映射到驗證表達式。</p> </td>
  </tr>
  <tr>
   <td><p>驗證狀態 </p> </td>
   <td><p>此指令碼在運行時執行，無法以自適應格式覆蓋。<br /> </p> </td>
  </tr>
  <tr>
   <td><p>退出 </p> </td>
   <td><p>此指令碼在運行時執行，無法以自適應格式覆蓋。</p> </td>
  </tr>
  <tr>
   <td><p>按一下（按鈕欄位）</p> </td>
   <td><p>映射到按鈕的「按一下」表達式。</p> </td>
  </tr>
  <tr>
   <td><p>支援伺服器端指令碼</p> </td>
   <td><p>此指令碼在運行時執行，無法以自適應格式覆蓋。</p> </td>
  </tr>
  <tr>
   <td><p>支援Web服務</p> </td>
   <td><p>此指令碼在運行時執行，無法以自適應格式覆蓋。</p> </td>
  </tr>
  <tr>
   <td><p>更改（Scribble欄位、單選按鈕、複選框）</p> </td>
   <td><p>此指令碼在運行時執行，無法以自適應格式覆蓋。</p> </td>
  </tr>
 </tbody>
</table>

### 驗證 {#validations}

下表捕獲了XFA驗證如何映射到自適應表單中的驗證。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA驗證</strong></p> </td>
   <td><p><strong>自適應形式中的相應驗證</strong></p> </td>
  </tr>
  <tr>
   <td><p>驗證模式(formatTest)</p> </td>
   <td><p>validatePictureClause</p> </td>
  </tr>
  <tr>
   <td><p>驗證模式消息(formatTestMessage)</p> </td>
   <td><p>驗證圖片消息</p> </td>
  </tr>
  <tr>
   <td><p>必需（空測試）</p> </td>
   <td><p>強制 </p> </td>
  </tr>
  <tr>
   <td><p>空消息(nullTestMessage) </p> </td>
   <td><p>強制消息</p> </td>
  </tr>
  <tr>
   <td><p>驗證指令碼(scriptTest)</p> </td>
   <td><p>validateExp</p> </td>
  </tr>
  <tr>
   <td><p>驗證指令碼消息(scriptTestMessage)</p> </td>
   <td><p>驗證消息</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>不能覆蓋綁定到XFA複選框的自適應表單單選按鈕和複選框組的強制屬性。
