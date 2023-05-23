---
title: 生成XDP表單的HTML5預覽
seo-title: Generate HTML5 preview of an XDP form
description: 「HTML設計器」中的「預覽LiveCycle」頁籤可用於在瀏覽器中顯示表單時預覽表單。
seo-description: Preview HTML tab in LiveCycle Designer can be used to preview forms as they appear in a browser.
uuid: cbee956f-bf2d-40c5-8e03-58fce0fa215b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 34e6d1bc-4eca-42dc-9ae5-9a2107fbefce
docset: aem65
feature: Mobile Forms
exl-id: 548f302b-57f0-4bdc-8a99-1a4967caa32f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# 生成XDP表單的HTML5預覽{#generate-html-preview-of-an-xdp-form}

在AEM Forms設計器中設計表單時，除了預覽表單的PDF格式副本外，還可以預覽表單的HTML5格式副本。 您可以使用 **預覽HTML** 按鈕，將選定控制項在Tab鍵次序中上移一個位置。

## 在設計器中為XDP表單啟用HTML預覽 {#html-preview-of-forms-in-forms-designer}

要使設計器能夠生成XDP表單的HTML預覽，請執行以下配置：

* 配置Apache Sling身份驗證服務
* 禁用保護模式
* 提供AEM Forms伺服器的詳細資訊

### 配置Apache Sling身份驗證服務 {#configure-apache-sling-authentication-service}

1. 轉到 `https://'[server]:[port]'/system/console/configMgr` AEM Forms在OSGi或
   `https://'[server]:[port]'/lc/system/console/configMgr` 在AEM Forms的JEE上。
1. 查找並按一下 **Apache Sling身份驗證服務** 以編輯模式開啟它的配置。

1. 根據您是在OSGi還是JEE上運行AEM Forms，在 **身份驗證要求** 欄位：

   * AEM FormsJEE

      * -/content/xfaforms
      * -/etc/clientlib
   * AEM Forms

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms

   >[!NOTE]
   >
   >請勿複製並貼上「驗證要求」欄位中的指定值，因為它可能會損壞值中的特殊字元。 而是在欄位中鍵入指定的值。

1. 在中指定用戶名和密碼 **[!UICONTROL 匿名用戶名]** 和 **[!UICONTROL 匿名用戶密碼]** 的下界。 指定的憑據用於處理匿名身份驗證並允許匿名用戶訪問。
1. 按一下 **保存** 的子菜單。

### 禁用保護模式 {#disable-protected-mode}

的 [保護模式](../../forms/using/get-xdp-pdf-documents-aem.md) 預設為開啟。 使其在生產環境中保持啟用狀態。 您可以在開發環境中禁用它，以在desinger中預覽HTML5Forms。 執行以下步驟以禁用它：

1. 以管理員身AEM份登錄到Web控制台。

   * OSGi上AEM Forms的URL為 `https://'[server]:[port]'/system/console/configMgr`
   * JEE上AEM Forms的URL是 `https://'[server]:[port]'/lc/system/console/configMgr`

1. 開啟 **[!UICONTROL 移動Forms配置]** 的子菜單。
1. 取消選擇 **[!UICONTROL 保護模式]** 選項 **[!UICONTROL 保存]**。

### 提供AEM Forms伺服器的詳細資訊 {#provide-details-of-aem-forms-server}

1. 在設計器中，轉到 **工具** > **選項**。
1. 在「選項」窗口中，選擇 **伺服器選項** 頁，提供以下詳細資訊，然後按一下 **確定**。

   * **伺服器URL**:AEM Forms伺服器URL。

   * **HTTP埠號**:服AEM務器埠。 預設值為 4502。
   * **HTML預覽上下文：** 用於呈現XFA表單的配置檔案的路徑。 以下預設配置檔案用於在設計器中預覽表單。 但是，您也可以指定自定義配置檔案的路徑。

      * `/content/xfaforms/profiles/default.html` (AEM FormsOSGi)

      * `/lc/content/xfaforms/profiles/default.html` (AEM FormsJEE)
   * **Forms經理上下文：** 部署Forms管理器UI的上下文路徑。 預設值為：

      * `/aem/forms` (AEM FormsOSGi)
      * `/lc/forms` (AEM FormsJEE)

   >[!NOTE]
   >
   >確保AEM Forms伺服器已啟動並正在運行。 HTML預覽連接到CRX伺服器 *生成* 的子菜單。

   ![AEM Forms設計器選項 ](assets/server_options.png)

   AEM Forms設計器選項

1. 要以HTML預覽窗體，請按一下 **預覽HTML** 頁籤。

   >[!NOTE]
   >
   >
   >
   >
   >    * 如果HTML預覽頁籤已關閉，請按F4開啟預覽HTML頁籤。 也可以從「視圖」菜單中選擇「預覽HTML」以開啟「預覽HTML」頁籤。
   >    * HTML預覽不支援PDF文檔，HTML預覽僅用於XDP文檔。


   >[!CAUTION]
   >
   >要test真正的最終用戶體驗，請在外部瀏覽器(GoogleChrome、MicrosoftEdge、Mozilla Firefox等)中預覽您的表單。 每個瀏覽器都使用單獨的引擎來渲染HTML，因此在設計器和外部瀏覽器中預覽表單的方式可能存在一些差異。

## 使用示例資料預覽表單 {#to-preview-a-form-using-sample-data}

設計器允許您使用示例XML資料預覽和test表單。 建議您經常將表單與示例資料test，以確保表單呈現正確。

如果沒有示例資料，Designer可以建立它，也可以自己建立它。 (請參閱 [自動生成示例資料以預覽表單](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2) 和 [建立示例資料以預覽窗體](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2)。)

使用示例資料源測試表單可確保資料和欄位被映射，並且重複的子表單會按預期重複。 您可以建立平衡的窗體佈局，為每個對象提供適當的空間來顯示合併的資料。

1. 選擇 **「檔案」>「窗體屬性」**。

1. 按一下 **預覽** 頁籤，然後在「資料檔案」框中，鍵入test資料檔案的完整路徑。 您還可以使用「瀏覽」按鈕導航到檔案。

1. 按一下&#x200B;**「確定」**。下次在 **預覽HTML** 頁籤中，示例XML檔案中的資料值將出現在相應對象中。

## 預覽位於儲存庫中的表單 {#html-preview-of-forms-in-forms-manager}

在AEM Forms，可以在儲存庫中預覽表單和文檔。 預覽有助於確切瞭解表單的外觀和行為方式，如最終用戶所使用的。
