---
title: 產生XDP表單的HTML5預覽
seo-title: 產生XDP表單的HTML5預覽
description: 「LiveCycle設計工具」中的「預覽HTML」索引標籤可用來預覽表單在瀏覽器中的顯示效果。
seo-description: 「LiveCycle設計工具」中的「預覽HTML」索引標籤可用來預覽表單在瀏覽器中的顯示效果。
uuid: cbee956f-bf2d-40c5-8e03-58fce0fa215b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 34e6d1bc-4eca-42dc-9ae5-9a2107fbefce
docset: aem65
feature: 行動表單
exl-id: 548f302b-57f0-4bdc-8a99-1a4967caa32f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# 生成XDP表單的HTML5預覽{#generate-html-preview-of-an-xdp-form}

在AEM Forms Designer中設計表單時，除了預覽表單的PDF轉譯外，您也可以預覽表單的HTML5轉譯。 您可以使用&#x200B;**預覽HTML**&#x200B;標籤來預覽表單在瀏覽器中的顯示效果。

## 在Designer {#html-preview-of-forms-in-forms-designer}中為XDP表單啟用HTML預覽

要啟用Designer生成XDP表單的HTML預覽，請執行以下配置：

* 設定Apache Sling Authentication Service
* 禁用保護模式
* 提供AEM Forms伺服器的詳細資訊

### 設定Apache Sling Authentication Service {#configure-apache-sling-authentication-service}

1. 前往OSGi上執行之AEM Forms上的`https://'[server]:[port]'/system/console/configMgr`或
   `https://'[server]:[port]'/lc/system/console/configMgr` 在JEE上執行的AEM Forms。
1. 找到並按一下&#x200B;**Apache Sling Authentication Service**&#x200B;設定，以在編輯模式中開啟。

1. 視您是在OSGi或JEE上執行AEM Forms而定，請在&#x200B;**Authentication Requirements**&#x200B;欄位中新增下列項目：

   * AEM Forms on JEE

      * -/content/xfaforms
      * -/etc/clientlibs
   * AEM Forms on OSGi

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms

   >[!NOTE]
   >
   >請勿在「驗證需求」欄位中複製並貼上指定的值，因為它可能會損毀值中的特殊字元。 請改為在欄位中輸入指定值。

1. 在&#x200B;**[!UICONTROL 匿名用戶名]**&#x200B;和&#x200B;**[!UICONTROL 匿名用戶密碼]**&#x200B;欄位中指定用戶名和密碼。 指定的憑據用於處理匿名身份驗證並允許匿名用戶訪問。
1. 按一下&#x200B;**儲存**&#x200B;以儲存設定。

### 禁用保護模式{#disable-protected-mode}

預設情況下，[保護模式](../../forms/using/get-xdp-pdf-documents-aem.md)處於開啟狀態。 讓環境保持啟用狀態。 您可以停用該功能，以便在開發環境中預覽HTML5 Forms。 執行下列步驟以停用：

1. 以管理員身分登入AEM Web Console。

   * OSGi上AEM Forms的URL為`https://'[server]:[port]'/system/console/configMgr`
   * JEE上AEM Forms的URL為`https://'[server]:[port]'/lc/system/console/configMgr`

1. 開啟&#x200B;**[!UICONTROL 行動Forms設定]**&#x200B;以進行編輯。
1. 取消選擇「**[!UICONTROL 保護模式]**」選項，然後按一下「**[!UICONTROL 保存]**」。

### 提供AEM Forms伺服器{#provide-details-of-aem-forms-server}的詳細資訊

1. 在Designer中，轉至&#x200B;**Tools** > **Options**。
1. 在「選項」窗口中，選擇&#x200B;**伺服器選項**&#x200B;頁，提供以下詳細資訊，然後按一下&#x200B;**確定**。

   * **伺服器URL**:AEM Forms伺服器URL。

   * **HTTP埠號**:AEM伺服器埠。預設值為 4502。
   * **HTML預覽內容：** 轉譯XFA表單之設定檔的路徑。以下預設配置檔案用於在設計器中預覽表單。 不過，您也可以指定自訂設定檔的路徑。

      * `/content/xfaforms/profiles/default.html` (AEM Forms on OSGi)

      * `/lc/content/xfaforms/profiles/default.html` (JEE版AEM Forms)
   * **Forms Manager Context:** 部署Forms Manager UI的內容路徑。預設值為：

      * `/aem/forms` (AEM Forms on OSGi)
      * `/lc/forms` (JEE版AEM Forms)

   >[!NOTE]
   >
   >確認AEM Forms伺服器已啟動並執行。 HTML預覽會連線至CRX伺服器以&#x200B;*產生*&#x200B;預覽。

   ![AEM Forms設計工具選項  ](assets/server_options.png)

   AEM Forms設計工具選項

1. 若要預覽HTML中的表單，請按一下「**預覽HTML**」標籤。

   >[!NOTE]
   >
   >
   >
   >
   >    * 如果HTML預覽頁簽已關閉，請按F4以開啟預覽HTML頁簽。 您也可以從「檢視」功能表選取「預覽HTML」 ，以開啟「預覽HTML」標籤。
   >    * HTML預覽不支援PDF檔案，HTML預覽僅適用於XDP檔案。


   >[!CAUTION]
   >
   >若要測試真正的一般使用者體驗，請同時在外部瀏覽器（Google Chrome、Microsoft Edge、Mozilla Firefox等）中預覽表單。 每個瀏覽器都使用不同的引擎來轉譯HTML，因此在Designer和外部瀏覽器中預覽表單的方式可能會有一些差異。

## 使用範例資料{#to-preview-a-form-using-sample-data}預覽表單

Designer可讓您使用範例XML資料來預覽和測試表單。 建議您經常使用範例資料測試表單，以確保表單可正確轉譯。

如果您沒有範例資料，可由設計人員建立，或由您自行建立。 （請參閱[自動產生範例資料以預覽表單](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2)和[建立範例資料以預覽表單](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2)）。

使用範例資料來源來測試您的表單，可確保資料和欄位已對應，且重複的子表單會如預期般重複。 您可以建立平衡的表單版面，為每個物件提供適當空間以顯示合併的資料。

1. 選擇&#x200B;**檔案>表單屬性**。

1. 按一下&#x200B;**預覽**&#x200B;頁簽，然後在「資料檔案」框中鍵入測試資料檔案的完整路徑。 您也可以使用「瀏覽」按鈕來導覽至檔案。

1. 按一下&#x200B;**「確定」**。下次在&#x200B;**預覽HTML**&#x200B;頁簽中預覽表單時，示例XML檔案中的資料值將出現在相應的對象中。

## 預覽位於{#html-preview-of-forms-in-forms-manager}儲存庫中的表單

在AEM Forms中，您可以在存放庫中預覽表單和檔案。 預覽有助於確切了解使用者使用表單的外觀和行為。
