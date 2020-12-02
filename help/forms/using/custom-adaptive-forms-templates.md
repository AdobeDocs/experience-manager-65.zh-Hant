---
title: 建立自訂最適化表單範本
seo-title: 建立自訂最適化表單範本
description: 本文說明如何建立自訂的最適化表單範本。
seo-description: 本文說明如何建立自訂的最適化表單範本。
uuid: 11b5f8cd-c56a-4525-97d5-1938ef5f183d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: affba49e-9712-4d29-858b-2f8ec4f2b1f1
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 0%

---


# 建立自訂最適化表單範本{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms已推出動態範本。 您可以使用AEM Sites範本編輯器來建立或編輯動態範本[。 ](../../forms/using/template-editor.md)下文提及的範本為靜態範本。 預設安裝中不提供這些。 [安裝相容](../../forms/using/compatibility-package.md) 性包，在您的環境中獲取這些模板。

## 必備條件 {#prerequisites}

* 瞭解AEM [頁面範本](/help/sites-authoring/templates.md)和[最適化表單製作](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* 瞭解AEM [用戶端程式庫](/help/sites-developing/clientlibs.md)

## 最適化表單範本{#adaptive-form-template}

「最適化表單」範本是專用的AEM頁面範本，具有用於建立最適化表單的特定屬性和內容結構。 範本已預先設定版面、樣式和基本的初始內容結構。

建立表單後，對原始範本內容結構所做的任何變更都不會反映在表單中。

## 預設自適應表單模板{#default-adaptive-form-templates}

AEM QuickStart提供下列最適化表單範本：

* 調查範本：可讓您使用已設定多欄的回應式版面建立單一頁面最適化表單。 版面會根據您要顯示表單之各種螢幕的尺寸自動調整。
* 簡易註冊範本：可讓您使用精靈版面建立多步驟可調式表單。 在此配置中，您可以為每個步驟指定步驟完成表達式，該表達式在嚮導繼續下一步之前進行驗證。
* 標籤式登記模板：可讓您使用左側標籤的版面建立多標籤可調式表單，您可以在其中以任何隨機順序瀏覽標籤。
* 進階註冊範本：可讓您建立包含多個標籤和精靈的表單。 它使用左側標籤的版面配置，可讓您依任何順序瀏覽標籤。 它使用Adobe Document Cloud電子簽名服務進行簽署和驗證。
* 空白範本：可讓您建立不含任何頁首、頁尾和初始內容的表格。 您可以新增元件，例如文字方塊、按鈕和影像。 空白範本可讓您建立可以[內嵌於AEM網站頁面](/help/forms/using/embed-adaptive-form-aem-sites.md)的表單。

這些模板將`sling:resourceType`屬性設定為相應的頁元件。 頁面元件轉譯CQ頁面，其中包含最適化表單容器，而最適化表單容器則轉譯最適化表單。

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

## 使用模板編輯器{#creating-an-adaptive-form-template-using-template-editor}建立自適應表單模板

您可以使用範本編輯器指定最適化表單的結構和初始內容。 例如，您希望所有表單作者在註冊表單中有幾個文字方塊、導覽按鈕和送出按鈕。 您可以建立範本，供作者用來建立與其他註冊表單一致的表單。 AEM範本編輯器可讓您：

* 在結構層中添加表單的頁首和頁尾元件
* 提供表單的初始內容。
* 指定主題。
* 指定提交、重設和導覽等動作。

如需詳細資訊，請參閱[範本編輯器](../../forms/using/template-editor.md)。

## 從CRXDE {#creating-an-adaptive-form-template-from-crxde}建立自適應表單模板

您可以建立範本並使用它來建立最適化表單，而不需使用可用的範本。 自訂範本是以參考最適化表單容器和頁面元素（例如頁首和頁尾）的各種頁面元件為基礎。

您可以使用網站的基本頁面元件來建立這些元件。 或者，您也可以將範本使用的最適化表單的頁面元件延伸出方塊。

執行下列步驟以建立自訂範本，例如simpleEnrollmentTemplate。

1. 導覽至您編寫執行個體上的CRXDE Lite。

1. 在/apps目錄下，建立應用程式的檔案夾結構。 例如，如果應用程式名稱為mycompany，請建立具有此名稱的檔案夾。 通常，應用程式資料夾包含元件、配置、模板、src和安裝目錄。 在此示例中，建立元件、配置和模板資料夾。

1. 導覽至資料夾/libs/fd/af/templates。
1. 複製`simpleEnrollmentTemplate`節點。
1. 導覽至資料夾/apps/mycompany/templates。 按一下右鍵它並選擇&#x200B;**[!UICONTROL 貼上]**。
1. 如有必要，請更名您複製的模板節點。 例如，將其重新命名為enrollment-template。

1. 導覽至位置/apps/mycompany/templates/enrollment-template。

1. 修改`jcr:content`節點的`jcr:title`和`jcr:description`屬性，以區分模板與您複製的模板。

1. 已修改模板的`jcr:content`節點包含`guideContainer`和`guideformtitle`元件。 `guideContainer` 是容納最適化表單的容器。`guideformtitle`元件顯示應用程式名稱、說明等。

   您可以包含自訂元件或`parsys`元件，而非`guideformtitle`。 例如，移除`guideformtitle`，並新增自訂元件或`parsys`元件節點。 請確定元件的`sling:resourceType`屬性引用元件，並且該屬性在頁面`component.jsp`檔案中定義。

1. 導覽至/apps/mycompany/templates/enrollment-template/jcr:content位置。

1. 開啟「**[!UICONTROL 屬性]**」標籤，將`cq:designPath`屬性的值變更為/etc/designs/mycompany。

1. 現在，請為`cq:Page`類型建立/etc/designs/mycompany節點。

## 建立最適化表單頁元件{#create-an-adaptive-form-page-component}

自訂範本的樣式與預設範本相同，因為範本會參照頁面元件/libs/fd/af/components/page/base。 您可以將元件引用作為在節點/apps/mycompany/templates/enrollment-template/jcr:content中定義的屬性`sling:resourceType`。 由於基礎是核心產品元件，因此不要修改此元件。

1. 導覽至節點/apps/mycompany/templates/enrollment-template/jcr:content，並將屬性`sling:resourceType`的值修改為/apps/mycompany/components/page/enrollmentpage
1. 將節點/libs/fd/af/components/page/base複製到資料夾/apps/mycompany/components/page。

1. 將複製的元件更名為`enrollmentpage`。

1. **（僅當您已有內容頁面時）** 如果您有網站的現有元件，請執行下列 `contentpage`步驟(a-d)。如果您的網站沒有現有的`contentpage`元件，您可以保留`resourceSuperType`屬性來指向OOTB基本頁面。

   1. 對於`enrollmentpage`節點，將屬性`sling:resourceSuperType`的值設定為mycompany/components/page/contentpage。 `contentpage`元件是您網站的基本頁面元件。 其他頁面元件可加以擴充。 刪除`enrollmentpage`下的指令碼檔案，但`head.jsp`、`content.jsp`和`library.jsp`除外。 `sling:resourceSuperType`元件（在本例中為`contentpage`）包含所有此類指令碼。 頁首（包括導覽列和頁尾）會繼承自`contentpage`元件。

   1. 開啟檔案`head.jsp`。

      JSP檔案包含行`<cq.include script="library.jsp"/>`。

      `library.jsp`檔案包含`guide.theme.simpleEnrollment`用戶端程式庫，其中包含最適化表單的樣式。

      頁面元件`enrollmentpage`有一個專用的`head.jsp`檔案，該檔案覆蓋`contentpage`元件的`head.jsp`檔案。

   1. 將`contentpage`元件的`head.jsp`檔案中的所有指令碼包括到`enrollmentpage`元件的`head.jsp`檔案中。
   1. 在`content.jsp`指令碼中，您可以新增其他頁面內容或參考至在頁面轉譯時包含的其他元件。 例如，如果添加自定義元件`applicationformheader`，請確保在JSP檔案中向該元件添加以下引用：

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      同樣地，如果在模板節點結構中添加`parsys`元件，也包括自定義元件。

## 建立自適應表單客戶端庫{#creating-an-adaptive-form-client-library}

新模板的`enrollmentpage`元件的`head.jsp`檔案包含客戶端庫`guide.theme.simpleEnrollment`。 預設範本也使用此用戶端程式庫。 使用下列方法變更新範本的樣式：

* 定義自訂主題，並以自訂主題取代預設主題`guide.theme.simpleEnrollment`。
* 在/etc/designs/mycompany下定義新的用戶端程式庫。 在jsp頁中，在預設主題項後加入客戶端庫。 在此用戶端程式庫中包含所有覆寫的樣式和其他Java Script檔案。

>[!NOTE]
>
>主題是指用於轉換最適化表單的頁面元件所包含的用戶端程式庫。 用戶端程式庫主要控制最適化表單的外觀。

