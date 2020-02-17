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

---


# 建立自訂最適化表單範本{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms已推出動態範本。 您可以使用AEM Sites範本編輯器來 [建立或編輯動態範本](../../forms/using/template-editor.md)。 下文提及的範本為靜態範本。 預設安裝中不提供這些。 [安裝相容性軟體包](../../forms/using/compatibility-package.md) ，以便在您的環境中獲取這些模板。

## 必備條件 {#prerequisites}

* 瞭解AEM頁面 [範本](/help/sites-authoring/templates.md) 和 [最適化表單](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* 瞭解AEM用戶 [端程式庫](/help/sites-developing/clientlibs.md)

## Adaptive form template {#adaptive-form-template}

「最適化表單」範本是專用的AEM頁面範本，具有用於建立最適化表單的特定屬性和內容結構。 範本已預先設定版面、樣式和基本的初始內容結構。

建立表單後，對原始範本內容結構所做的任何變更都不會反映在表單中。

## 預設最適化表單範本 {#default-adaptive-form-templates}

AEM quickStart提供下列最適化表單範本：

* 調查範本：可讓您使用已設定多欄的回應式版面建立單一頁面最適化表單。 版面會根據您要顯示表單之各種螢幕的尺寸自動調整。
* 簡易註冊範本：可讓您使用精靈版面建立多步驟可調式表單。 在此配置中，您可以為每個步驟指定步驟完成表達式，該表達式在嚮導繼續執行下一步之前進行驗證。
* 標籤式登記模板：可讓您使用左側標籤的版面建立多標籤可調式表單，您可以在其中以任何隨機順序瀏覽標籤。
* 進階註冊範本：可讓您建立包含多個標籤和精靈的表單。 它使用左側標籤的版面配置，可讓您依任何順序瀏覽標籤。 它使用Adobe Document cloud電子簽名服務進行簽署和驗證。
* 空白範本：可讓您建立不含任何頁首、頁尾和初始內容的表格。 您可以新增元件，例如文字方塊、按鈕和影像。 空白範本可讓您建立可內嵌在AEM網 [站頁面中的表單](/help/forms/using/embed-adaptive-form-aem-sites.md)。

這些範本的屬 `sling:resourceType` 性已設為對應的頁面元件。 頁面元件轉譯CQ頁面，其中包含最適化表單容器，而最適化表單又轉譯為最適化表單。

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

## 使用模板編輯器建立自適應表單模板 {#creating-an-adaptive-form-template-using-template-editor}

您可以使用範本編輯器指定最適化表單的結構和初始內容。 例如，您希望所有表單作者在註冊表單中有幾個文字方塊、導覽按鈕和送出按鈕。 您可以建立範本，供作者用來建立與其他註冊表單一致的表單。 AEM範本編輯器可讓您：

* 在結構層中添加表單的頁首和頁尾元件
* 提供表單的初始內容。
* 指定主題。
* 指定提交、重設和導覽等動作。

如需詳細資訊，請參閱范 [本編輯器](../../forms/using/template-editor.md)。

## 從CRXDE建立自適應表單模板 {#creating-an-adaptive-form-template-from-crxde}

您可以建立範本並使用它來建立最適化表單，而不需使用可用的範本。 自訂範本是以參考最適化表單容器和頁面元素（例如頁首和頁尾）的各種頁面元件為基礎。

您可以使用網站的基本頁面元件來建立這些元件。 或者，您也可以將範本使用的最適化表單的頁面元件延伸出方塊。

執行下列步驟以建立自訂範本，例如simpleEnrollmentTemplate。

1. 導覽至您編寫執行個體上的CRXDE Lite。

1. 在/apps目錄下，建立應用程式的檔案夾結構。 例如，如果應用程式名稱為mycompany，請建立具有此名稱的檔案夾。 通常，應用程式資料夾包含元件、配置、模板、src和安裝目錄。 在此示例中，建立元件、配置和模板資料夾。

1. 導覽至資料夾/libs/fd/af/templates。
1. 複製節 `simpleEnrollmentTemplate` 點。
1. 導覽至資料夾/apps/mycompany/templates。 按一下右鍵並選擇「 **[!UICONTROL 貼上」]**。
1. 如有必要，請更名您複製的模板節點。 例如，將其重新命名為enrollment-template。

1. 導覽至位置/apps/mycompany/templates/enrollment-template。

1. 修改節 `jcr:title` 點的 `jcr:description` 和屬 `jcr:content` 性，以區分範本和您複製的範本。

1. 已修 `jcr:content` 改模板的節點包含 `guideContainer` 和 `guideformtitle` 元件。 `guideContainer` 是容納最適化表單的容器。 組 `guideformtitle` 件顯示應用程式名稱、說明等。

   您可以包 `guideformtitle`含自訂元件或元件，而不是這 `parsys` 樣。 例如，移除 `guideformtitle`並新增自訂元件或元件 `parsys` 節點。 請確定元 `sling:resourceType` 件的屬性會參照元件，並在頁面檔案中定義該元 `component.jsp` 件。

1. 導覽至位置/apps/mycompany/templates/enrollment-template/jcr:content。

1. 開啟「 **[!UICONTROL 屬性]** 」標籤，並將屬性值 `cq:designPath` 變更為/etc/designs/mycompany。

1. 現在，請為類型建立/etc/designs/mycompany節 `cq:Page` 點。

## 建立最適化表單頁面元件 {#create-an-adaptive-form-page-component}

自訂範本的樣式與預設範本相同，因為範本會參照頁面元件/libs/fd/af/components/page/base。 您可以找到元件引用作為在節 `sling:resourceType` 點/apps/mycompany/templates/enrollment-template/jcr:content中定義的屬性。 由於基礎是核心產品元件，因此不要修改此元件。

1. 導覽至節點/apps/mycompany/templates/enrollment-template/jcr:content，並將屬性值修改為 `sling:resourceType` /apps/mycompany/components/page/enrollmentpage
1. 將節點/libs/fd/af/components/page/base複製到資料夾/apps/mycompany/components/page。

1. 將複製的元件更名為 `enrollmentpage`。

1. **（僅當您已有內容頁面時）** ，如果您有網站的現有元件，請執行下 `contentpage`列步驟(a-d)。 如果您的網站沒有現 `contentpage`有的元件，您可 `resourceSuperType`以保留屬性以指向OOTB基本頁面。

   1. 對於節 `enrollmentpage` 點，將屬性的值設 `sling:resourceSuperType` 置為mycompany/components/page/contentpage。 元 `contentpage` 件是您網站的基本頁面元件。 其他頁面元件可加以擴充。 移除下方 `enrollmentpage`的指令 `head.jsp`碼檔 `content.jsp`案，除外、和 `library.jsp`。 在本 `sling:resourceSuperType` 例中，此組 `contentpage` 件包含所有此類指令碼。 頁首（包括導覽列和頁尾）會繼承自元件 `contentpage` 中。

   1. 開啟檔案 `head.jsp`。

      JSP檔案包含該行 `<cq.include script="library.jsp"/>`。

      檔 `library.jsp` 案包含用戶 `guide.theme.simpleEnrollment` 端程式庫，其中包含最適化表單的樣式。

      頁面元 `enrollmentpage` 件有專屬 `head.jsp` 檔案，會覆寫 `head.jsp` 元件的檔 `contentpage` 案。

   1. 將元件的所有腳 `head.jsp` 本都包括在該 `contentpage` 元件的 `head.jsp` 檔案中的 `enrollmentpage` 檔案中。
   1. 在指令 `content.jsp` 碼中，您可以新增其他頁面內容或參考在頁面轉譯時包含的其他元件。 例如，如果添加自定義元件， `applicationformheader`請確保在JSP檔案中向該元件添加以下引用：

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      同樣地，如果在模板節 `parsys` 點結構中添加元件，也包括自定義元件。

## 建立自適應表單客戶端庫 {#creating-an-adaptive-form-client-library}

新模 `head.jsp` 板的組 `enrollmentpage` 件檔案包含一個客戶端庫 `guide.theme.simpleEnrollment`。 預設範本也使用此用戶端程式庫。 使用下列方法變更新範本的樣式：

* 定義自訂主題，並以自訂主題 `guide.theme.simpleEnrollment` 取代預設主題。
* 在/etc/designs/mycompany下定義新的用戶端程式庫。 在jsp頁中，在預設主題項後加入客戶端庫。 在此用戶端程式庫中包含所有覆寫的樣式和其他Java script檔案。

>[!NOTE]
>
>主題是指用於轉換最適化表單的頁面元件所包含的用戶端程式庫。 用戶端程式庫主要控制最適化表單的外觀。

