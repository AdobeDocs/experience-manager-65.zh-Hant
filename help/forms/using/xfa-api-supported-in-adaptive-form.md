---
title: 基於XDP的自適應表單中的XFA支援
seo-title: 基於XDP的自適應表單中的XFA支援
description: 列出最適化表單中支援的XFA事件、屬性、指令碼和驗證。
seo-description: 列出最適化表單中支援的XFA事件、屬性、指令碼和驗證。
uuid: 75d3c292-cfed-438f-afdb-4071d95a08b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 05303b29-9058-4723-b134-4ba605fe40c7
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe

---


# 基於XDP的自適應表單中的XFA支援{#xfa-support-in-xdp-based-adaptive-forms}

## 簡介 {#introduction}

最適化表單支援在XDP檔案中定義的各種XFA事件、屬性、指令碼和驗證，包括：

* 執行在XDP檔案中事件上定義的指令碼。
* 擷取XDP檔案欄位的預設值和行為屬性。
* 執行在XDP檔案中定義的驗證指令碼。

根據XDP檔案建立最適化表單時，屬性、事件和驗證會自動填入表單製作UI。 不過，表單作者可以覆寫其中一些元素，以建立替代體驗。

本文列出在最適化表單中採用的支援XFA事件、屬性和驗證，並說明如何在最適化表單中覆寫它們。

## 支援的XFA元素及其在最適化表單中的對應 {#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}

### 欄位 {#fields}

當使用XDP檔案建立自適應表單時，可以將XFA欄位拖放到自適應表單上。 下表列出XFA欄位如何對應至最適化表單欄位。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA欄位或容器</strong></p> </td>
   <td><p><strong>對應的自適應表單元件</strong></p> </td>
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
   <td><p>日期／時間欄位 </p> </td>
   <td><p>日期挑選器</p> </td>
  </tr>
  <tr>
   <td><p>簽名塗鴉</p> </td>
   <td><p>（已過時）塗鴉簽名</p> </td>
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
   <td><p>區域（群組）</p> </td>
   <td><p>面板</p> </td>
  </tr>
  <tr>
   <td><p>子表單集 </p> </td>
   <td><p>面板</p> </td>
  </tr>
 </tbody>
</table>

### 屬性 {#properties}

下表說明在XDP檔案中定義的各種XFA指令碼如何以最適化格式運作。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA元件屬性</strong></p> </td>
   <td><p><strong>自適應形式中的對應行為</strong></p> </td>
  </tr>
  <tr>
   <td><p>somExpression </p> </td>
   <td><p>以最適化形式映射至Bind reference(bindRef)屬性。</p> </td>
  </tr>
  <tr>
   <td><p>存在 </p> </td>
   <td><p>以最適化形式映射至可見屬性。 您可以使用「可見性」運算式來覆寫它。</p> </td>
  </tr>
  <tr>
   <td><p>存取 </p> </td>
   <td><p>以最適化形式映射至enabled屬性。 您可以使用「存取」運算式來覆寫它。</p> </td>
  </tr>
  <tr>
   <td><p>協助功能：角色 </p> </td>
   <td><p>映射至最適化格式的角色屬性。</p> </td>
  </tr>
  <tr>
   <td><p>協助功能：speakPriority </p> </td>
   <td><p>以最適化形式映射至speakPriority屬性。</p> </td>
  </tr>
  <tr>
   <td><p>協助功能：speakText</p> </td>
   <td><p>以最適化格式對應至自訂協助工具文字。</p> </td>
  </tr>
  <tr>
   <td><p>協助功能：工具提示 </p> </td>
   <td><p>映射至最適化格式的簡短描述屬性。</p> </td>
  </tr>
  <tr>
   <td><p>標題<em> （所有欄位類型）</em></p> </td>
   <td><p>以最適化形式映射至Title屬性。</p> </td>
  </tr>
  <tr>
   <td><p>displayFormat<em> （所有欄位類型）</em></p> </td>
   <td><p>以最適化形式映射至「顯示模式」。</p> </td>
  </tr>
  <tr>
   <td><p>rawValue<em> （所有欄位類型）</em></p> </td>
   <td><p>映射至最適化表單中的值屬性。</p> </td>
  </tr>
  <tr>
   <td><p>項目<em> （清單框、複選框）</em></p> </td>
   <td><p>以最適化格式映射至選項屬性。 您可以使用「選項」運算式來覆寫它。</p> </td>
  </tr>
  <tr>
   <td><p>maxChar<em> （文字欄位）</em></p> </td>
   <td><p>以最適化格式映射至「允許的字元數上限」屬性。</p> </td>
  </tr>
  <tr>
   <td><p>多行<em> （文字欄位）</em></p> </td>
   <td><p>映射至最適化格式的「允許多行」屬性。</p> </td>
  </tr>
  <tr>
   <td><p>fracDigit<em> （數值欄位、小數欄位）</em></p> </td>
   <td><p>以最適化形式映射到Frac digits屬性。</p> </td>
  </tr>
  <tr>
   <td><p>leadDigit<em> （數值欄位、小數欄位）</em></p> </td>
   <td><p>以最適化形式映射至Lead digits屬性。</p> </td>
  </tr>
  <tr>
   <td><p>multiSelect<em> （清單框）</em></p> </td>
   <td><p>以最適化形式映射至「允許多選項」屬性。</p> </td>
  </tr>
 </tbody>
</table>

### 指令碼 {#scripts}

下表顯示了在XDP檔案中定義的各種XFA指令碼在最適化表單中的行為。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA指令碼事件</strong></p> </td>
   <td><p><strong>自適應形式中的對應行為</strong></p> </td>
  </tr>
  <tr>
   <td><p>初始化 </p> </td>
   <td><p>此指令碼會在執行時期執行，無法以最適化格式覆寫。</p> </td>
  </tr>
  <tr>
   <td><p>計算</p> </td>
   <td><p>以自適應形式映射到「計算」表達式。</p> </td>
  </tr>
  <tr>
   <td><p>驗證 </p> </td>
   <td><p>以最適化形式映射至驗證運算式。</p> </td>
  </tr>
  <tr>
   <td><p>validationState </p> </td>
   <td><p>此指令碼會在執行時期執行，無法以最適化格式覆寫。<br /> </p> </td>
  </tr>
  <tr>
   <td><p>退出 </p> </td>
   <td><p>此指令碼會在執行時期執行，無法以最適化格式覆寫。</p> </td>
  </tr>
  <tr>
   <td><p>按一下（按鈕欄位）</p> </td>
   <td><p>映射至按鈕的點按運算式。</p> </td>
  </tr>
  <tr>
   <td><p>支援伺服器端指令碼</p> </td>
   <td><p>此指令碼會在執行時期執行，無法以最適化格式覆寫。</p> </td>
  </tr>
  <tr>
   <td><p>支援web services</p> </td>
   <td><p>此指令碼會在執行時期執行，無法以最適化格式覆寫。</p> </td>
  </tr>
  <tr>
   <td><p>變更（塗鴉欄位、選項按鈕、核取方塊）</p> </td>
   <td><p>此指令碼會在執行時期執行，無法以最適化格式覆寫。</p> </td>
  </tr>
 </tbody>
</table>

### 驗證 {#validations}

下表顯示了XFA驗證如何映射到自適應表單中的驗證。

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
   <td><p>驗證模式訊息(formatTestMessage)</p> </td>
   <td><p>validatePictureMessage</p> </td>
  </tr>
  <tr>
   <td><p>必要(nullTest)</p> </td>
   <td><p>強制 </p> </td>
  </tr>
  <tr>
   <td><p>空白訊息(nullTestMessage) </p> </td>
   <td><p>mandatoryMessage</p> </td>
  </tr>
  <tr>
   <td><p>驗證指令碼(scriptTest)</p> </td>
   <td><p>validateExp</p> </td>
  </tr>
  <tr>
   <td><p>驗證指令碼訊息(scriptTestMessage)</p> </td>
   <td><p>validateMessage</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您無法覆寫最適化表單選項按鈕和核取方塊群組的強制屬性，這些核取方塊群組會系結至XFA核取按鈕。

