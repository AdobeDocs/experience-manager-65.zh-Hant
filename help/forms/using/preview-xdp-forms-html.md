---
title: 產生XDP表單的HTML5預覽
seo-title: 產生XDP表單的HTML5預覽
description: 在LiveCycle Designer中預覽HTML標籤可用來預覽表單在瀏覽器中的顯示效果。
seo-description: 在LiveCycle Designer中預覽HTML標籤可用來預覽表單在瀏覽器中的顯示效果。
uuid: cbee956f-bf2d-40c5-8e03-58fce0fa215b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 34e6d1bc-4eca-42dc-9ae5-9a2107fbefce
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---


# 產生XDP表單的HTML5預覽{#generate-html-preview-of-an-xdp-form}

在AEM Forms Designer中設計表格時，除了預覽表格的PDF轉譯外，您也可以預覽表格的HTML5轉譯。 您可以使用&#x200B;**預覽HTML**&#x200B;標籤來預覽表單在瀏覽器中的顯示效果。

## 在Designer {#html-preview-of-forms-in-forms-designer}中啟用XDP表單的HTML預覽

若要讓設計人員產生XDP表單的HTML預覽，請執行下列設定：

* 設定Apache Sling Authentication Service
* 禁用保護模式
* 提供AEM Forms伺服器的詳細資訊

### 設定Apache Sling Authentication Service {#configure-apache-sling-authentication-service}

1. 前往OSGi上執行的AEM Forms上的`https://'[server]:[port]'/system/console/configMgr`或
   `https://'[server]:[port]'/lc/system/console/configMgr` 在JEE上執行的AEM Forms。
1. 找到並按一下&#x200B;**Apache Sling Authentication Service**&#x200B;組態，以在編輯模式中開啟它。

1. 視您是在OSGi或JEE上執行AEM Forms而定，請在&#x200B;**Authentication Requirements**&#x200B;欄位中新增下列項目：

   * AEM Forms on JEE

      * -/content/xfaforms
      * -/etc/clientlibs
   * OSGi上的AEM Forms

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms

   >[!NOTE]
   >
   >請勿在「驗證要求」欄位中複製並貼上指定的值，因為它可能會損壞值中的特殊字元。 請改為在欄位中輸入指定的值。

1. 在&#x200B;**[!UICONTROL 匿名用戶名]**&#x200B;和&#x200B;**[!UICONTROL 匿名用戶密碼]**&#x200B;欄位中分別指定用戶名和密碼。 指定的認證用於處理匿名驗證並允許匿名用戶訪問。
1. 按一下&#x200B;**保存**&#x200B;保存配置。

### 禁用保護模式{#disable-protected-mode}

預設情況下，[保護模式](../../forms/using/get-xdp-pdf-documents-aem.md)處於開啟狀態。 讓它在生產環境中保持啟用。 您可以停用它，讓開發環境在設計中預覽HTML5 Forms。 請執行下列步驟以停用它：

1. 以管理員身分登入AEM Web Console。

   * OSGi上AEM Forms的URL為`https://'[server]:[port]'/system/console/configMgr`
   * JEE上的AEM Forms URL為`https://'[server]:[port]'/lc/system/console/configMgr`

1. 開啟&#x200B;**[!UICONTROL 行動表單組態]**&#x200B;以進行編輯。
1. 取消選擇&#x200B;**[!UICONTROL 保護模式]**&#x200B;選項，然後按一下&#x200B;**[!UICONTROL 保存]**。

### 提供AEM Forms伺服器{#provide-details-of-aem-forms-server}的詳細資訊

1. 在設計器中，轉至&#x200B;**工具** > **選項**。
1. 在「選項」窗口中，選擇「伺服器選項」頁，提供以下詳細資訊，然後按一下「確定」。********

   * **伺服器URL**:AEM Forms伺服器URL。

   * **HTTP埠號**:AEM伺服器埠。預設值為4502。
   * **HTML預覽內容：** 轉換XFA表單的描述檔路徑。以下預設配置檔案用於在設計器中預覽表單。 不過，您也可以指定自訂描述檔的路徑。

      * `/content/xfaforms/profiles/default.html` （OSGi上的AEM Forms）

      * `/lc/content/xfaforms/profiles/default.html` (AEM Forms on JEE)
   * **Forms Manager上下文：** 部署Forms Manager UI的上下文路徑。預設值為：

      * `/aem/forms` （OSGi上的AEM Forms）
      * `/lc/forms` (AEM Forms on JEE)

   >[!NOTE]
   >
   >請確定AEM Forms伺服器已啟動並正在執行。 HTML預覽會連接至CRX伺服器，以產生&#x200B;*預覽。*

   ![AEM Forms Designer選項  ](assets/server_options.png)

   AEM Forms Designer選項

1. 若要預覽HTML中的表單，請按一下「預覽HTML **」標籤。**

   >[!NOTE]
   >
   >
   >
   >
   >    * 如果關閉「HTML預覽」標籤，請按F4以開啟「預覽HTML」標籤。 您也可以選取「從檢視」選單中預覽HTML，以開啟「預覽HTML」標籤。
   >    * HTML預覽不支援PDF檔案，HTML預覽僅適用於XDP檔案。


   >[!CAUTION]
   >
   >若要測試真正的使用者體驗，請在外部瀏覽器（Google Chrome、Microsoft Edge、Mozilla Firefox等）中預覽您的表格。 每個瀏覽器都使用不同的引擎來轉換HTML，因此在設計人員和外部瀏覽器中預覽表單的方式可能會有一些不同。

## 使用範例資料{#to-preview-a-form-using-sample-data}預覽表格

設計人員可讓您使用範例XML資料來預覽和測試表格。 建議您經常使用範例資料來測試表格，以確保表格能正確呈現。

如果您沒有範例資料，設計人員可以建立它，或者您可以自行建立它。 （請參閱[自動產生範例資料以預覽您的表單](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2)和[建立範例資料以預覽您的表單](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2)）。

使用範例資料來源來測試表單，可確保資料和欄位已映射，且重複的子表單會如預期般重複。 您可以建立平衡的表單配置，為每個物件提供適當的空間以顯示合併的資料。

1. 選擇&#x200B;**檔案>表單屬性**。

1. 按一下「預覽&#x200B;****」標籤，然後在「資料檔案」方塊中，輸入測試資料檔案的完整路徑。 您也可以使用「瀏覽」按鈕來導覽至檔案。

1. 按一下&#x200B;**「確定」**。下次在&#x200B;**預覽HTML**&#x200B;標籤中預覽表格時，範例XML檔案中的資料值會出現在個別物件中。

## 預覽位於儲存庫{#html-preview-of-forms-in-forms-manager}中的表單

在AEM Forms中，您可以在儲存庫中預覽表單和檔案。 預覽功能有助於確切瞭解表單的外觀和行為方式，讓使用者也能使用。
