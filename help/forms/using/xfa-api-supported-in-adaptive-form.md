---
title: XDP型最適化表單的XFA支援
seo-title: XFA support in XDP-based adaptive forms
description: 列出適用性表單中支援的XFA事件、屬性、指令碼和驗證。
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

# XDP型最適化表單的XFA支援{#xfa-support-in-xdp-based-adaptive-forms}

## 簡介 {#introduction}

適用性表單支援XDP檔案中定義的各種XFA事件、屬性、指令碼和驗證，包括：

* 執行XDP檔案中事件上定義的指令碼。
* 擷取XDP檔案中欄位的預設值和行為屬性。
* 執行XDP檔案中定義的驗證指令碼。

根據XDP檔案建立適用性表單時，表單製作UI會自動填入屬性、事件和驗證。 不過，表單作者可以覆寫其中的某些元素，以建立替代體驗。

本文列出適用性表單中採用的支援XFA事件、屬性和驗證，並說明如何在適用性表單中覆寫它們。

## 支援的XFA元素及其在最適化表單中的對應 {#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}

### 欄位 {#fields}

使用XDP檔案建立適用性表單時，您可以將XFA欄位拖放至適用性表單。 下表列出XFA欄位對應至最適化表單欄位的方式。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA欄位或容器</strong></p> </td>
   <td><p><strong>對應的最適化表單元件</strong></p> </td>
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
   <td><p>簽名手寫</p> </td>
   <td><p>草寫簽名</p> </td>
  </tr>
  <tr>
   <td><p>數值欄位 </p> </td>
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
   <td><p>子表單 </p> </td>
   <td><p>面板</p> </td>
  </tr>
  <tr>
   <td><p>區域（組）</p> </td>
   <td><p>面板</p> </td>
  </tr>
  <tr>
   <td><p>子表單集 </p> </td>
   <td><p>面板</p> </td>
  </tr>
 </tbody>
</table>

### 屬性 {#properties}

下表說明在XDP檔案中定義的各種XFA指令碼在最適化表單中的行為。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA元件屬性</strong></p> </td>
   <td><p><strong>適用性表單中的對應行為</strong></p> </td>
  </tr>
  <tr>
   <td><p>somExpression </p> </td>
   <td><p>以最適化形式映射到Bind reference(bindRef)屬性。</p> </td>
  </tr>
  <tr>
   <td><p>存在 </p> </td>
   <td><p>以最適化表單對應至可見屬性。 您可以使用「可見性」運算式來覆寫它。</p> </td>
  </tr>
  <tr>
   <td><p>存取 </p> </td>
   <td><p>以最適化表單對應至enabled屬性。 您可以使用存取運算式來覆寫它。</p> </td>
  </tr>
  <tr>
   <td><p>協助工具：角色 </p> </td>
   <td><p>已對應至適用性表單中的角色屬性。</p> </td>
  </tr>
  <tr>
   <td><p>協助工具：seakPriority </p> </td>
   <td><p>以最適化形式對應至seakPriority屬性。</p> </td>
  </tr>
  <tr>
   <td><p>協助工具：seakText</p> </td>
   <td><p>以最適化表單對應至自訂協助工具文字。</p> </td>
  </tr>
  <tr>
   <td><p>協助工具：工具提示 </p> </td>
   <td><p>以最適化表單對應至簡短說明屬性。</p> </td>
  </tr>
  <tr>
   <td><p>字幕<em> （所有欄位類型）</em></p> </td>
   <td><p>以最適化表單對應至Title屬性。</p> </td>
  </tr>
  <tr>
   <td><p>displayFormat<em> （所有欄位類型）</em></p> </td>
   <td><p>以最適化表單對應至「顯示模式」。</p> </td>
  </tr>
  <tr>
   <td><p>rawValue<em> （所有欄位類型）</em></p> </td>
   <td><p>已對應至適用性表單中的值屬性。</p> </td>
  </tr>
  <tr>
   <td><p>項目<em> （清單框、複選框）</em></p> </td>
   <td><p>以最適化表單對應至options屬性。 您可以使用Options運算式來覆寫它。</p> </td>
  </tr>
  <tr>
   <td><p>maxChar<em> （文字欄位）</em></p> </td>
   <td><p>以最適化表單對應至允許的字元數上限屬性。</p> </td>
  </tr>
  <tr>
   <td><p>多線<em> （文字欄位）</em></p> </td>
   <td><p>以最適化表單對應至「允許多行」屬性。</p> </td>
  </tr>
  <tr>
   <td><p>fracDigit<em> （數值欄位、小數欄位）</em></p> </td>
   <td><p>以最適化形式映射到Frac數字屬性。</p> </td>
  </tr>
  <tr>
   <td><p>leadDigit<em> （數值欄位、小數欄位）</em></p> </td>
   <td><p>以最適化表單對應至Lead digits屬性。</p> </td>
  </tr>
  <tr>
   <td><p>multiSelect<em> （清單框）</em></p> </td>
   <td><p>以最適化表單對應至允許多個選取屬性。</p> </td>
  </tr>
 </tbody>
</table>

### 指令碼 {#scripts}

下表說明XDP檔案中定義的各種XFA指令碼在最適化表單中的行為。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA指令碼事件</strong></p> </td>
   <td><p><strong>適用性表單中的對應行為</strong></p> </td>
  </tr>
  <tr>
   <td><p>初始化 </p> </td>
   <td><p>此指令碼會在執行階段執行，且無法以最適化表單覆寫。</p> </td>
  </tr>
  <tr>
   <td><p>計算</p> </td>
   <td><p>已對應至適用性表單中的「計算」運算式。</p> </td>
  </tr>
  <tr>
   <td><p>驗證 </p> </td>
   <td><p>以最適化表單對應至驗證運算式。</p> </td>
  </tr>
  <tr>
   <td><p>validationState </p> </td>
   <td><p>此指令碼會在執行階段執行，且無法以最適化表單覆寫。<br /> </p> </td>
  </tr>
  <tr>
   <td><p>退出 </p> </td>
   <td><p>此指令碼會在執行階段執行，且無法以最適化表單覆寫。</p> </td>
  </tr>
  <tr>
   <td><p>按一下（按鈕欄位）</p> </td>
   <td><p>對應至按鈕的「點按」運算式。</p> </td>
  </tr>
  <tr>
   <td><p>支援伺服器端指令碼</p> </td>
   <td><p>此指令碼會在執行階段執行，且無法以最適化表單覆寫。</p> </td>
  </tr>
  <tr>
   <td><p>支援網站服務</p> </td>
   <td><p>此指令碼會在執行階段執行，且無法以最適化表單覆寫。</p> </td>
  </tr>
  <tr>
   <td><p>更改（手寫欄位、單選按鈕、複選框）</p> </td>
   <td><p>此指令碼會在執行階段執行，且無法以最適化表單覆寫。</p> </td>
  </tr>
 </tbody>
</table>

### 驗證 {#validations}

下表說明XFA驗證與適用性表單中驗證的對應方式。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA驗證</strong></p> </td>
   <td><p><strong>適用性表單中的對應驗證</strong></p> </td>
  </tr>
  <tr>
   <td><p>驗證模式(formatTest)</p> </td>
   <td><p>validatePictureClause</p> </td>
  </tr>
  <tr>
   <td><p>驗證模式消息(formatTestMessage)</p> </td>
   <td><p>validatePictureMessage</p> </td>
  </tr>
  <tr>
   <td><p>必要(nullTest)</p> </td>
   <td><p>強制 </p> </td>
  </tr>
  <tr>
   <td><p>空消息(nullTestMessage) </p> </td>
   <td><p>mandatoryMessage</p> </td>
  </tr>
  <tr>
   <td><p>驗證指令碼(scriptTest)</p> </td>
   <td><p>validateExp</p> </td>
  </tr>
  <tr>
   <td><p>驗證指令碼消息(scriptTestMessage)</p> </td>
   <td><p>validateMessage</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您無法覆寫綁定到XFA核取按鈕的適用性表單選項按鈕和核取方塊群組的強制屬性。
