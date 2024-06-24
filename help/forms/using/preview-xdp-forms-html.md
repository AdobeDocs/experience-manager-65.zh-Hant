---
title: 產生XDP表單的HTML5預覽
description: LiveCycleDesigner中的預覽HTML索引標籤可用於預覽表單在瀏覽器中顯示的效果。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 548f302b-57f0-4bdc-8a99-1a4967caa32f
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# 產生XDP表單的HTML5預覽{#generate-html-preview-of-an-xdp-form}

在AEM Forms Designer中設計表單時，除了預覽表單的PDF轉譯外，您還可以預覽表單的HTML5轉譯。 您可以使用 **預覽HTML** 標籤來預覽顯示在瀏覽器中的表單。

## 在Designer中啟用XDP表單的HTML預覽 {#html-preview-of-forms-in-forms-designer}

若要讓Designer產生XDP表單的HTML預覽，請執行以下設定：

* 設定Apache Sling驗證服務
* 停用保護模式
* 提供AEM Forms伺服器的詳細資訊

### 設定Apache Sling驗證服務 {#configure-apache-sling-authentication-service}

1. 前往 `https://'[server]:[port]'/system/console/configMgr` 在OSGi上執行的AEM Forms上或
   `https://'[server]:[port]'/lc/system/console/configMgr` 在JEE上執行的AEM Forms上。
1. 找到並按一下 **Apache Sling驗證服務** 設定，以在編輯模式中開啟它。

1. 根據您是在OSGi或JEE上執行AEM Forms，在中新增下列內容 **驗證需求** 欄位：

   * JEE上的AEM Forms

      * -/content/xfaforms
      * -/etc/clientlibs

   * OSGi上的AEM Forms

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms

   >[!NOTE]
   >
   >請勿複製並貼上「驗證需求」欄位中的指定值，因為這會損壞值中的特殊字元。 請改為在欄位中輸入指定的值。

1. 在中指定使用者名稱和密碼 **[!UICONTROL 匿名使用者名稱]** 和 **[!UICONTROL 匿名使用者密碼]** 欄位。 指定的認證用於處理匿名驗證，並允許匿名使用者存取。
1. 按一下 **儲存** 以儲存組態。

### 停用保護模式 {#disable-protected-mode}

此 [受保護模式](../../forms/using/get-xdp-pdf-documents-aem.md) 預設為開啟。 在生產環境中維持啟用。 您可以為開發環境停用它，以便在設計中預覽HTML5 Forms。 執行以下步驟來停用它：

1. 以管理員身分登入AEM Web Console。

   * OSGi上的AEM Forms URL是 `https://'[server]:[port]'/system/console/configMgr`
   * JEE上AEM Forms的URL為 `https://'[server]:[port]'/lc/system/console/configMgr`

1. 開啟 **[!UICONTROL 行動Forms設定]** 以進行編輯。
1. 取消選取 **[!UICONTROL 受保護模式]** 選項並按一下 **[!UICONTROL 儲存]**.

### 提供AEM Forms伺服器的詳細資訊 {#provide-details-of-aem-forms-server}

1. 在Designer中，前往 **工具** > **選項**.
1. 在「選項」視窗中，選取 **伺服器選項** 頁面，提供下列詳細資料，然後按一下 **確定**.

   * **伺服器URL**：AEM Forms伺服器URL。

   * **HTTP連線埠號碼**：AEM伺服器連線埠。 預設值為 4502。
   * **HTML預覽內容：** 呈現XFA表單的設定檔路徑。 下列預設設定檔是用來在Designer中預覽表單。 不過，您也可以指定自訂設定檔的路徑。

      * `/content/xfaforms/profiles/default.html` (OSGi上的AEM Forms)

      * `/lc/content/xfaforms/profiles/default.html` (JEE版AEM Forms)

   * **Forms Manager內容：** 部署Forms Manager UI的內容路徑。 預設值為：

      * `/aem/forms` (OSGi上的AEM Forms)
      * `/lc/forms` (JEE版AEM Forms)

   >[!NOTE]
   >
   >確認AEM Forms伺服器已啟動且執行中。 HTML預覽會連線至CRX伺服器，並 *產生* 預覽。

   ![AEM Forms Designer選項 ](assets/server_options.png)

   AEM Forms Designer選項

1. 若要以HTML預覽表單，請按一下 **預覽HTML** 標籤。

   >[!NOTE]
   >
   >
   >
   >
   >    * 如果「HTML預覽」標籤關閉，請按F4開啟「預覽HTML」標籤。 您也可以從「檢視」選單中選取「預覽HTML」，以開啟「預覽HTML」標籤。
   >    * HTML預覽不支援PDF檔案，HTML預覽僅適用於XDP檔案。
   >
   >

   >[!CAUTION]
   >
   >若要測試真實的一般使用者體驗，請在外部瀏覽器(Google Chrome、Microsoft Edge、Mozilla Firefox等)中預覽您的表單。 每個瀏覽器使用不同的引擎來轉譯HTML，因此Designer中的表單預覽方式與外部瀏覽器之間可能有一些差異。

## 若要使用範例資料預覽表單 {#to-preview-a-form-using-sample-data}

Designer可讓您使用範例XML資料預覽及測試表單。 建議您經常使用範例資料測試表單，以確保表單正確呈現。

如果您沒有範例資料，Designer可以建立它，您也可以自行建立。 (請參閱 [若要自動產生範例資料以預覽您的表單](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2) 和 [建立範例資料以預覽表單的方式](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2).)

使用範例資料來源測試您的表單可確保資料和欄位對應，並且重複的子表單會如預期般重複。 您可以建立平衡的表單版面配置，為每個物件提供適當的空間，以顯示合併的資料。

1. 選取 **檔案>表單屬性**.

1. 按一下 **預覽** 標籤，並在「資料檔案」方塊中，輸入測試資料檔案的完整路徑。 您也可以使用「瀏覽」按鈕來導覽至檔案。

1. 按一下 **確定**. 下次您預覽表單時 **預覽HTML** 標籤，範例XML檔案中的資料值會顯示在個別物件中。

## 在存放庫中預覽表單 {#html-preview-of-forms-in-forms-manager}

在AEM Forms中，您可以預覽存放庫中的表單和檔案。 預覽有助於瞭解一般使用者使用表單的確切外觀和行為。
