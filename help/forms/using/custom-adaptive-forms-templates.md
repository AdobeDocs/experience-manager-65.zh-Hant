---
title: 建立自訂最適化表單範本
description: 本文介紹如何建立自訂最適化表單範本。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 35b50573-0be8-469d-a1ac-f51b9aaa5fef
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 5723e9990969dff1b508062d69a68f68a20eb576
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 0%

---

# 建立自訂最適化表單範本{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms匯入了動態範本。 您可以使用AEM Sites範本編輯器[建立或編輯動態範本](../../forms/using/template-editor.md)。 下文中提及的範本為靜態範本。 預設安裝中無法使用這些選項。 [安裝相容性套件](../../forms/using/compatibility-package.md)以在您的環境中取得這些範本。

## 先決條件 {#prerequisites}

* 瞭解AEM [頁面範本](/help/sites-authoring/templates.md)和[最適化表單製作](https://helpx.adobe.com/tw/aem-forms/6-1/introduction-forms-authoring.html)

* 瞭解AEM [使用者端資料庫](/help/sites-developing/clientlibs.md)

## 自適應表單範本 {#adaptive-form-template}

調適型表單範本是專用的AEM頁面範本，具有用來建立調適型表單的特定屬性和內容結構。 範本有預先設定的版面、樣式和基本初始內容結構。

建立表單後，對原始範本內容結構所做的任何變更都不會反映在表單中。

## 預設最適化表單範本 {#default-adaptive-form-templates}

AEM QuickStart提供下列最適化表單範本：

* 調查範本：可讓您使用已設定多個欄的回應式版面，建立單頁最適化表單。 版面會根據您要顯示表單的各種熒幕的尺寸自動調整。
* Simple Enrollment範本：可讓您使用精靈版面配置建立多步驟最適化表單。 在此配置中，您可以為每個步驟指定步驟完成運算式，在精靈進行下一步之前會驗證此運算式。
* 索引標籤註冊範本：可讓您使用索引標籤左側的版面配置建立多索引標籤的最適化表單，您可以在此以任意順序造訪索引標籤。
* 進階註冊範本：可讓您建立包含多個索引標籤和精靈的表單。 它使用索引標籤在左側的版面，可讓您依任何順序造訪索引標籤。 它使用Adobe Document Cloud設計服務來簽署和驗證。
* 空白範本：可讓您建立不含任何頁首、頁尾和初始內容的表單。 您可以新增元件，例如文字方塊、按鈕和影像。 空白範本可讓您建立可[內嵌於AEM網站頁面](/help/forms/using/embed-adaptive-form-aem-sites.md)的表單。

這些範本已將`sling:resourceType`屬性設定為對應的頁面元件。 頁面元件會轉譯CQ頁面（包含調適型表單容器），接著轉譯調適型表單。

下表列舉範本與頁面元件之間的關聯：

<table>
 <tbody>
  <tr>
   <td><p><strong>範本</strong></p> </td>
   <td><p><strong>頁面元件</strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/survey</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/simpleEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenrollment</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advancedenrollment</p> </td>
  </tr>
 </tbody>
</table>

## 使用範本編輯器建立最適化表單範本 {#creating-an-adaptive-form-template-using-template-editor}

您可以使用範本編輯器來指定最適化表單的結構和初始內容。 例如，您希望所有表格作者在登錄檔格中都有幾個文字方塊、導覽按鈕和提交按鈕。 您可以建立範本，供作者用來建立與其他登錄檔單一致的表單。 AEM範本編輯器可讓您：

* 在結構圖層中新增表單的頁首與頁尾元件
* 提供表單的初始內容。
* 指定主題。
* 指定提交、重設和導覽等動作。

如需詳細資訊，請參閱[範本編輯器](../../forms/using/template-editor.md)。

## 從CRXDE建立最適化表單範本 {#creating-an-adaptive-form-template-from-crxde}

您可以建立範本並使用它來建立調適型表單，而不使用可用的範本。 自訂範本以參照最適化表單容器和頁面元素（例如頁首和頁尾）的各種頁面元件為基礎。

您可以使用網站的基底頁面元件來建立這些元件。 或者，您也可以擴充現成範本使用的最適化表單的頁面元件。

執行以下步驟來建立自訂範本，例如simpleEnrollmentTemplate。

1. 導覽至您編寫執行個體上的CRXDE Lite。

1. 在/apps目錄下，為您的應用程式建立資料夾結構。 例如，如果應用程式名稱為mycompany，請建立具有此名稱的資料夾。 通常，應用程式資料夾包含元件、組態、範本、src和安裝目錄。 在此範例中，請建立元件、組態和範本資料夾。

1. 導覽至資料夾/libs/fd/af/templates。
1. 複製`simpleEnrollmentTemplate`節點。
1. 導覽至資料夾/apps/mycompany/templates。 用滑鼠右鍵按一下並選取&#x200B;**[!UICONTROL 貼上]**。
1. 如有必要，請重新命名您所複製的範本節點。 例如，將其重新命名為註冊範本。

1. 導覽至/apps/mycompany/templates/enrollment-template位置。

1. 修改`jcr:content`節點的`jcr:title`和`jcr:description`屬性，以區分範本和您複製的範本。

1. 修改範本的`jcr:content`節點包含`guideContainer`和`guideformtitle`元件。 `guideContainer`是儲存最適化表單的容器。 `guideformtitle`元件會顯示應用程式名稱、說明等。

   您可以包含自訂元件或`parsys`元件，而非`guideformtitle`。 例如，移除`guideformtitle`，然後新增自訂元件或`parsys`元件節點。 請確定元件的`sling:resourceType`屬性參考元件，且已在頁面`component.jsp`檔案中定義相同的元件。

1. 導覽至/apps/mycompany/templates/enrollment-template/jcr：content位置。

1. 開啟&#x200B;**[!UICONTROL 屬性]**&#x200B;標籤，並將`cq:designPath`屬性的值變更為/etc/designs/mycompany。

1. 現在為`cq:Page`型別建立/etc/designs/mycompany節點。

## 建立最適化表單頁面元件 {#create-an-adaptive-form-page-component}

自訂範本的樣式與預設範本相同，因為範本會參考頁面元件/libs/fd/af/components/page/base。 您可以在節點/apps/mycompany/templates/enrollment-template/jcr：content中找到定義為屬性`sling:resourceType`的元件參考。 由於基礎是核心產品元件，請勿修改此元件。

1. 導覽至節點/apps/mycompany/templates/enrollment-template/jcr：content，並將屬性`sling:resourceType`的值修改為/apps/mycompany/components/page/enrollmentpage
1. 將節點/libs/fd/af/components/page/base複製到資料夾/apps/mycompany/components/page。

1. 將複製的元件重新命名為`enrollmentpage`。

1. **（只有當您已經有contentpage時）**&#x200B;如果您的網站已有`contentpage`元件，請執行下列步驟(a-d)。 如果您的網站沒有現有的`contentpage`元件，您可以保留`resourceSuperType`屬性以指向現成可用的基本頁面。

   1. 針對`enrollmentpage`節點，將屬性`sling:resourceSuperType`的值設為mycompany/components/page/contentpage。 `contentpage`元件是您網站的基礎頁面元件。 其他頁面元件可加以擴充。 移除`enrollmentpage`底下的指令碼檔案，`head.jsp`、`content.jsp`和`library.jsp`除外。 `sling:resourceSuperType`元件（在此例中為`contentpage`）包含所有此類指令碼。 標題（包括導覽列和頁尾）繼承自`contentpage`元件。

   1. 開啟檔案`head.jsp`。

      JSP檔案包含第`<cq.include script="library.jsp"/>`行。

      `library.jsp`檔案包含`guide.theme.simpleEnrollment`使用者端資料庫，其中包含最適化表單的樣式。

      頁面元件`enrollmentpage`有一個獨佔的`head.jsp`檔案，它覆寫了`contentpage`元件的`head.jsp`檔案。

   1. 在`contentpage`元件的`head.jsp`檔案中包含`enrollmentpage`元件的`head.jsp`檔案中的所有指令碼。
   1. 在`content.jsp`指令碼中，您可以新增其他頁面內容或參考至頁面轉譯時包含的其他元件。 例如，如果您新增自訂元件`applicationformheader`，請確定您在JSP檔案中新增以下元件參考：

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      同樣地，如果您在範本節點結構中新增`parsys`元件，也要包含自訂元件。

## 建立最適化表單使用者端程式庫 {#creating-an-adaptive-form-client-library}

新範本之`enrollmentpage`元件的`head.jsp`檔案包含使用者端程式庫`guide.theme.simpleEnrollment`。 預設範本也使用此使用者端程式庫。 使用以下方法之一變更新範本中的樣式：

* 定義自訂主題，並將預設主題`guide.theme.simpleEnrollment`取代為自訂主題。
* 在/etc/designs/mycompany下定義新的使用者端程式庫。 在jsp頁面中的預設主題專案之後包含從屬端程式庫。 在此使用者端資料庫中包含所有覆寫樣式和其他Java指令碼檔案。

>[!NOTE]
>
>主題是指包含在用於呈現最適化表單的頁面元件中的使用者端資料庫。 使用者端資料庫主要控管最適化表單的外觀。
