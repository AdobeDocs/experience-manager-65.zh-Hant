---
title: 建立自訂最適化表單範本
seo-title: 建立自訂最適化表單範本
description: 本文說明如何建立自訂最適化表單範本。
seo-description: 本文說明如何建立自訂最適化表單範本。
uuid: 11b5f8cd-c56a-4525-97d5-1938ef5f183d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: affba49e-9712-4d29-858b-2f8ec4f2b1f1
docset: aem65
exl-id: 35b50573-0be8-469d-a1ac-f51b9aaa5fef
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 0%

---

# 建立自訂最適化表單範本{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms推出了動態範本。 您可以使用AEM Sites範本編輯器來[建立或編輯動態範本](../../forms/using/template-editor.md)。 以下文章中提及的範本為靜態範本。 預設安裝中不提供這些。 [安裝相容性](../../forms/using/compatibility-package.md) 套件以在您的環境中取得這些範本。

## 必備條件 {#prerequisites}

* 了解AEM [頁面範本](/help/sites-authoring/templates.md)和[最適化表單編寫](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* 了解AEM [用戶端程式庫](/help/sites-developing/clientlibs.md)

## 適用性表單範本{#adaptive-form-template}

適用性表單範本是專用的AEM頁面範本，具有用於建立適用性表單的特定屬性和內容結構。 範本已預先設定配置、樣式和基本初始內容結構。

建立表單後，對原始範本內容結構所做的任何變更都不會反映在表單中。

## 預設最適化表單範本{#default-adaptive-form-templates}

AEM快速入門提供下列最適化表單範本：

* 調查範本：可讓您使用設定了多欄的回應式版面來建立單頁最適化表單。 版面會根據您要顯示表單之各種螢幕的尺寸自動調整。
* 簡單註冊模板：可讓您使用精靈版面來建立多步驟最適化表單。 在此配置中，您可以為每個步驟指定步驟完成表達式，該表達式將在嚮導繼續到下一個步驟之前驗證。
* 頁簽式登記模板：可讓您使用左側的索引標籤版面來建立多索引標籤適用性表單，以便以任何隨機順序造訪索引標籤。
* 高級註冊模板：可讓您使用多個索引標籤和精靈建立表單。 它使用左上標籤版面，可讓您以任何順序造訪標籤。 它使用Adobe Document Cloud設計服務進行簽署和驗證。
* 空白範本：可讓您建立表單，不含任何頁首、頁尾和初始內容。 您可以新增元件，例如文字方塊、按鈕和影像。 空白範本可讓您建立表單，以在AEM網站頁面](/help/forms/using/embed-adaptive-form-aem-sites.md)中內嵌[。

這些範本的`sling:resourceType`屬性已設為對應的頁面元件。 頁面元件會轉譯CQ頁面，其中包含最適化表單容器，而最適化表單則轉譯為最適化表單。

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
   <td><p>/libs/fd/afaddon/components/page/advandenrollment</p> </td>
  </tr>
 </tbody>
</table>

## 使用範本編輯器{#creating-an-adaptive-form-template-using-template-editor}建立最適化表單範本

您可以使用範本編輯器來指定最適化表單的結構和初始內容。 例如，您希望所有表單作者在註冊表單中都有幾個文本框、導航按鈕和提交按鈕。 您可以建立模板，供作者用來建立與其他註冊表單一致的表單。 AEM範本編輯器可讓您：

* 在結構層中添加表單的頁眉和頁腳元件
* 提供表單的初始內容。
* 指定主題。
* 指定提交、重設和導覽等動作。

如需詳細資訊，請參閱[範本編輯器](../../forms/using/template-editor.md)。

## 從CRXDE {#creating-an-adaptive-form-template-from-crxde}建立最適化表單範本

您可以建立範本，並使用範本建立最適化表單，而不使用可用的範本。 自訂範本是以參考最適化表單容器和頁面元素（例如頁首和頁尾）的各種頁面元件為基礎。

您可以使用網站的基礎頁面元件來建立這些元件。 或者，您也可以擴充使用現成範本的最適化表單的頁面元件。

執行以下步驟以建立自定義模板，如simpleEnrollmentTemplate。

1. 導覽至製作執行個體上的CRXDE Lite。

1. 在/apps目錄下，建立應用程式的資料夾結構。 例如，如果應用程式名稱為mycompany，請建立具有此名稱的資料夾。 應用程式資料夾通常包含元件、配置、模板、src和安裝目錄。 在此範例中，建立元件、設定和範本資料夾。

1. 導覽至資料夾/libs/fd/af/templates。
1. 複製`simpleEnrollmentTemplate`節點。
1. 導覽至資料夾/apps/mycompany/templates。 按一下右鍵，然後選擇&#x200B;**[!UICONTROL 貼上]**。
1. 如有必要，請重新命名您複製的範本節點。 例如，將其更名為註冊模板。

1. 導覽至/apps/mycompany/templates/enrollment-template位置。

1. 修改`jcr:content`節點的`jcr:title`和`jcr:description`屬性，以區分範本與您複製的範本。

1. 修改的模板的`jcr:content`節點包含`guideContainer`和`guideformtitle`元件。 `guideContainer` 是容納最適化表單的容器。`guideformtitle`元件顯示應用程式名稱、說明等。

   您可以包含自訂元件或`parsys`元件，而非`guideformtitle`。 例如，刪除`guideformtitle`，然後添加自定義元件或`parsys`元件節點。 請確定元件的`sling:resourceType`屬性會參考元件，並在頁面`component.jsp`檔案中定義相同的屬性。

1. 導覽至/apps/mycompany/templates/enrollment-template/jcr:content位置。

1. 開啟&#x200B;**[!UICONTROL Properties]**&#x200B;標籤，並將`cq:designPath`屬性的值變更為/etc/designs/mycompany。

1. 現在為`cq:Page`類型建立/etc/designs/mycompany節點。

## 建立最適化表單頁面元件{#create-an-adaptive-form-page-component}

自訂範本的樣式與預設範本相同，因為範本會參照頁面元件/libs/fd/af/components/page/base。 您可以找到元件引用，該元件引用為在節點/apps/mycompany/templates/enrollment-template/jcr:content中定義的屬性`sling:resourceType`。 由於基礎是核心產品元件，因此請勿修改此元件。

1. 導覽至節點/apps/mycompany/templates/enrollment-template/jcr:content ，並將屬性`sling:resourceType`的值修改至/apps/mycompany/components/page/enrollmentpage
1. 將節點/libs/fd/af/components/page/base複製到資料夾/apps/mycompany/components/page。

1. 將複製的元件更名為`enrollmentpage`。

1. **（僅限您已有內容頁面）** 如果您的網站有現有元件，請執行下列步 `contentpage`驟(a-d)。如果您的網站沒有現有的`contentpage`元件，可以保留`resourceSuperType`屬性以指向OOTB基本頁面。

   1. 對於`enrollmentpage`節點，將屬性`sling:resourceSuperType`的值設定為mycompany/components/page/contentpage。 `contentpage`元件是您網站的基本頁面元件。 其他頁面元件可加以擴充。 移除`enrollmentpage`下的指令碼檔案，但`head.jsp`、`content.jsp`和`library.jsp`除外。 `sling:resourceSuperType`元件（在此例中為`contentpage`）包含所有此類指令碼。 標題（包括導航欄和頁尾）繼承自`contentpage`元件。

   1. 開啟檔案`head.jsp`。

      JSP檔案包含行`<cq.include script="library.jsp"/>`。

      `library.jsp`檔案包含`guide.theme.simpleEnrollment`用戶端程式庫，其中包含最適化表單的樣式。

      頁面元件`enrollmentpage`具有專用的`head.jsp`檔案，該檔案覆蓋`contentpage`元件的`head.jsp`檔案。

   1. 將`contentpage`元件的`head.jsp`檔案中的所有指令碼包含到`enrollmentpage`元件的`head.jsp`檔案中。
   1. 在`content.jsp`指令碼中，您可以新增其他頁面內容或參考至頁面呈現時包含的其他元件。 例如，如果添加自定義元件`applicationformheader`，請確保將以下引用添加到JSP檔案中的元件：

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      同樣地，如果您在範本節點結構中新增`parsys`元件，也納入自訂元件。

## 建立最適化表單用戶端程式庫{#creating-an-adaptive-form-client-library}

新模板的`enrollmentpage`元件的`head.jsp`檔案包含客戶端庫`guide.theme.simpleEnrollment`。 預設模板還使用此客戶端庫。 使用下列方法的，更改新模板中的樣式：

* 定義自訂主題，並將預設主題`guide.theme.simpleEnrollment`替換為自訂主題。
* 在/etc/designs/mycompany下定義新的用戶端程式庫。 在jsp頁中的預設主題條目後面包括客戶端庫。 在此客戶端庫中包含所有被覆蓋的樣式和其他Java Script檔案。

>[!NOTE]
>
>主題是指包含在頁面元件中用於轉譯最適化表單的用戶端程式庫。 用戶端程式庫主要控制最適化表單的外觀。
