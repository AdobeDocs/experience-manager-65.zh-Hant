---
title: 最適化表單關鍵字
description: 您無法在最適化表單中將這些保留字當作識別碼使用。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 678e9dfc-2c46-430a-8da9-0329dda80090
feature: Adaptive Forms,Foundation Components
exl-id: 6ef5bd8c-7e7b-4501-a1be-d34fc0dbde84
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 26%

---

# 最適化表單關鍵字 {#adaptive-forms-keywords}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

調適型表單關鍵字為預先定義的保留識別碼，對調適型表單具有特殊意義。 您無法在最適化表單中將這些關鍵字當作識別碼使用。 下表列出作為適用性表單的保留識別碼的所有關鍵字。

<table>
 <tbody>
  <tr>
   <td><p>初始化</p> </td>
   <td><p>getonoffValues</p> </td>
   <td><p>minOccure</p> </td>
  </tr>
  <tr>
   <td><p>驗證</p> </td>
   <td><p>setGuideState</p> </td>
   <td><p>maxOccure</p> </td>
  </tr>
  <tr>
   <td><p>forceElementFocusChange</p> </td>
   <td><p>getGuideState</p> </td>
   <td><p>initialOccure</p> </td>
  </tr>
  <tr>
   <td><p>checkIfNull</p> </td>
   <td><p>初始化</p> </td>
   <td><p>instanceTemplateId</p> </td>
  </tr>
  <tr>
   <td><p>playJson</p> </td>
   <td><p>準備</p> </td>
   <td><p>instanceCount</p> </td>
  </tr>
  <tr>
   <td><p>resetData</p> </td>
   <td><p>runPendingExpressions</p> </td>
   <td><p>可重複</p> </td>
  </tr>
  <tr>
   <td><p>calcexp</p> </td>
   <td><p>queueExpression</p> </td>
   <td><p>執行個體</p> </td>
  </tr>
  <tr>
   <td><p>標題</p> </td>
   <td><p>resolveNode</p> </td>
   <td><p>syncXFAProps</p> </td>
  </tr>
  <tr>
   <td><p>valueCommitScript</p> </td>
   <td><p>autoSaveStart</p> </td>
   <td><p>造訪</p> </td>
  </tr>
  <tr>
   <td><p>validateExp</p> </td>
   <td><p>enableAutoSave</p> </td>
   <td><p>getElement</p> </td>
  </tr>
  <tr>
   <td><p>placeholderText</p> </td>
   <td><p>Autosavstartexpression</p> </td>
   <td><p>子項</p> </td>
  </tr>
  <tr>
   <td><p>值</p> </td>
   <td><p>autoSaveInfo</p> </td>
   <td><p>setAttribute</p> </td>
  </tr>
  <tr>
   <td><p>formattedValue</p> </td>
   <td><p>xdpRef</p> </td>
   <td><p>getGuideProp</p> </td>
  </tr>
  <tr>
   <td><p>displayPictureClause</p> </td>
   <td><p>dorTemplateRef</p> </td>
   <td><p>getXFAProp</p> </td>
  </tr>
  <tr>
   <td><p>validatePictureClause</p> </td>
   <td><p>actionType</p> </td>
   <td><p>getAttribute</p> </td>
  </tr>
  <tr>
   <td><p>editPictureClause</p> </td>
   <td><p>xsdRef</p> </td>
   <td><p>名稱</p> </td>
  </tr>
  <tr>
   <td><p>強制</p> </td>
   <td><p>面板</p> </td>
   <td><p>templateId</p> </td>
  </tr>
  <tr>
   <td><p>message</p> </td>
   <td><p>multiSelect</p> </td>
   <td>&gt;<p>id</p> </td>
  </tr>
  <tr>
   <td><p>validateExpMessage</p> </td>
   <td><p>選項運算式</p> </td>
   <td><p>somexpression</p> </td>
  </tr>
  <tr>
   <td><p>validatePictureClauseMessage</p> </td>
   <td><p>項目</p> </td>
   <td><p>nonLocalizedTitle</p> </td>
  </tr>
  <tr>
   <td><p>validationState</p> </td>
   <td><p>multiSelection</p> </td>
   <td><p>viewVisited</p> </td>
  </tr>
  <tr>
   <td><p>寬度</p> </td>
   <td><p>按鈕文字</p> </td>
   <td><p>索引</p> </td>
  </tr>
  <tr>
   <td><p>高度</p> </td>
   <td><p>showComment</p> </td>
   <td><p>可見</p> </td>
  </tr>
  <tr>
   <td><p>cssClassName</p> </td>
   <td><p>fileSizeLimit</p> </td>
   <td><p>已啟用</p> </td>
  </tr>
  <tr>
   <td><p>按一下運算式</p> </td>
   <td><p>檔案清單</p> </td>
   <td><p>enableLayoutOptimization</p> </td>
  </tr>
  <tr>
   <td><p>導覽變更費用</p> </td>
   <td><p>handleEvent</p> </td>
   <td><p>資料型別</p> </td>
  </tr>
  <tr>
   <td><p>類型</p> </td>
   <td><p>addInstance</p> </td>
   <td><p>leadDigits</p> </td>
  </tr>
  <tr>
   <td><p>showLink</p> </td>
   <td><p>insertInstance</p> </td>
   <td><p>fracDigits</p> </td>
  </tr>
  <tr>
   <td><p>clickStatus</p> </td>
   <td><p>removeInstance</p> </td>
   <td><p>maxChars</p> </td>
  </tr>
  <tr>
   <td><p>showAsPopUp</p> </td>
   <td><p>shortDescription</p> </td>
   <td><p>execNavigationChangeExpression</p> </td>
  </tr>
  <tr>
   <td><p>多行</p> </td>
   <td><p>longDescription</p> </td>
   <td><p>executeExpression</p> </td>
  </tr>
  <tr>
   <td><p>visibleExp</p> </td>
   <td><p>initScript</p> </td>
   <td><p>enabledExp</p> </td>
  </tr>
  <tr>
   <td><p>execCompletion</p> </td>
   <td><p>sectionId</p> </td>
   <td><p>setFocus</p> </td>
  </tr>
  <tr>
   <td><p>completionExp</p> </td>
   <td><p>章節標題</p> </td>
   <td><p>activeInstance</p> </td>
  </tr>
  <tr>
   <td><p>completionExpReq</p> </td>
   <td><p>completionScript</p> </td>
   <td><p>activePart</p> </td>
  </tr>
  <tr>
   <td><p>工具列</p> </td>
   <td><p>completionBeforeMessage</p> </td>
   <td><p>isLastPart</p> </td>
  </tr>
  <tr>
   <td><p>instanceManager</p> </td>
   <td><p>completionAfterMessage</p> </td>
   <td><p>isFirstPart</p> </td>
  </tr>
  <tr>
   <td><p>instanceIndex</p> </td>
   <td><p>completionSuccessScript</p> </td>
   <td><p>currentActivePart</p> </td>
  </tr>
  <tr>
   <td><p>摘要</p> </td>
   <td><p>completionFailureScript</p> </td>
   <td><p>sectionName</p> </td>
  </tr>
  <tr>
   <td><p>submitpassword</p> </td>
   <td><p>initializeChildren</p> </td>
   <td><p>sectionFields</p> </td>
  </tr>
  <tr>
   <td><p>fetchedFromService</p> </td>
   <td><p>repeatablePanelId</p> </td>
   <td><p>getSelectedIndex</p> </td>
  </tr>
  <tr>
   <td><p>Repeatablepanelpath</p> </td>
   <td><p>getItemIdentifier</p> </td>
   <td><p>mobileLayout</p> </td>
  </tr>
  <tr>
   <td><p>欄寬</p> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

除了上述關鍵字，請避免使用類似於[最適化表單JavaScript API](https://adobe.com/go/learn_aemforms_javascript_api_63)的名稱。
