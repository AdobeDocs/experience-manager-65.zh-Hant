---
title: 正在更新過期的Reader擴展服務證書
description: Reader擴展文檔無法工作，更新證書
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 0%

---

# 正在更新過期的Reader擴展服務證書 {#Updating-expired-Reader-Extension-service-certificates}

Adobe Experience Manager Forms(AEM Forms)擁有Adobe托管服務或內部部署企業基礎許可證的客戶有權使用Reader擴展服務。 該服務通過擴展Adobe Reader的功能和附加的使用權限，使組織能夠方便地共用互動式PDF文檔。 該服務將使用權限添加到PDF文檔，並激活在使用Adobe Acrobat Reader DC開啟PDF文檔時通常不可用的功能，例如向文檔添加註釋、填寫表單和保存文檔。 第三方用戶不需要使用其他軟體或插件來處理啟用權限的文檔。 PDF文檔添加了使用權限，稱為啟用權限的文檔。 在Adobe Reader開啟啟用了權限的PDF文檔的用戶可以執行為該文檔啟用的操作。

Adobe利用PKI（公鑰基礎架構）頒發數字證書，用於許可和功能啟用。 Adobe已根據證書頒發機構「Adobe根CA」頒發證書，該證書定於2023年1月7日到期。 它將導致根據此證書頒發機構頒發的所有證書過期。 證書過期後，依賴於證書的所有功能將不再工作。 例如，允許使用Adobe Acrobat Reader添加註釋的讀者擴展PDF文檔在2023年1月7日後停止為客戶工作。 要解決此問題，Reader擴展服務管理員應使用舊證書獲取新Adobe根CA G2頒發的新證書並將其重新應用於其PDF文檔(閱讀器用新證書擴展PDF文檔)。

證書的過期對AEM FormsJEE和AEM FormsOSGi堆棧都有影響。 兩個堆棧都有不同的指令集。 在與 [預請求](#Pre-requisites) 和 [獲取新證書](#obtain-the-certificates)，根據堆棧，選擇以下路徑之一：

* [更新JEE環境上AEM Forms的證書](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment)
* [在OSGi環境上更新AEM Forms的證書](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>文檔可互換地使用術語證書和憑據。

## 先決條件 {#Pre-requisites}

更新證書需要使用AEM Forms管理員控制台和AEM Forms提供的Reader擴展API上可用的操作。 本文檔旨在為瞭解使用Adobe Experience MangerFormsAPI的用戶和管理員提供。 開始之前，請確保：

* 用戶對基礎AEM Forms環境具有管理員權限。
* 用戶已設定 [開發環境](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) 並有權訪問。
* 獲取證書。

### 獲取證書 {#obtain-the-certificates}

權限憑據作為數字證書傳遞，該證書包含用於訪問憑據的公鑰、私鑰和密碼。

如果您的組織購買了生產版本的Reader擴展，則生產權限憑據由Adobe授權網站(LWS)提供。 生產權限憑據是您的組織所特有的，並且可以啟用您需要的特定使用權限。

如果您通過將Reader擴展整合到其軟體中的合作夥伴或軟體提供商獲得了Reader擴展，則該合作夥伴將向您提供權限憑據，而該合作夥伴又從Adobe中接收此憑據。

>[!NOTE]
>
>權限憑據不能用於典型的文檔簽名或身份聲明。 對於這些應用程式，您可以使用自簽名證書或從證書頒發機構(CA)獲取身份證書。

以下類型的權限憑據可用：

**客戶評估**:向要評估Reader擴展的客戶提供具有短有效期的憑據。 應用於使用此憑據的文檔的使用權限在憑據過期時過期。 此類憑據只有效兩到三個月。

**生產**:向購買完整產品的客戶提供具有長有效期的憑據。 生產憑據對於每個客戶都是唯一的，但可以安裝在多個系統上。

如果您已使用證書來讀取擴展PDF檔案，請從 [Adobe許可網站(LWS)](https://licensing.adobe.com/)。

## 在JEE環境上更新和申請AEM Forms證書 {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment}

在JEE堆棧上更新和應用AEM Forms上的新證書需要導入新憑據、從現有PDF文檔中刪除使用權限以及應用使用權限。 您可以使用管理控制台導入憑據，而AEM FormsReader擴展API則刪除和應用使用權限。

### 導入和配置憑據

可以使用「信任儲存管理」頁導入新憑據或替換憑據。 信任儲存可能包含多個Reader擴展憑據。 必須將其中一個憑據指定為預設的Reader擴展憑據。 當Workbench用戶無法確定在建立流程期間要使用的憑據時，將使用預設憑據。 這些規則適用於預設憑據：

* 如果導入Reader擴展憑據，而信任儲存不包含其他Reader擴展憑據，則將其設定為預設值。
* 如果導入了Reader擴展憑據，並且選擇了「預設」選項，則會從現有預設憑據中刪除預設類型。 導入的憑據將成為預設值。
* 無法刪除預設的Reader擴展憑據。 要刪除預設憑據，請先將另一個憑據設定為預設憑據。 此規則的一個例外是，如果只有一個憑據，則即使是預設憑據，也可以刪除它。
* 無法更新預設Reader擴展憑據。

要導入憑據：

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「本地憑據」。
1. 按一下導入，在信任儲存類型下，選擇Acrobat Reader DC擴展憑據。
1. （可選）要指明此憑據是與Acrobat Reader DC擴展一起使用的預設憑據，請選擇「預設」。
1. 在「別名」框中，鍵入憑據的標識符。 此標識符用作Acrobat Reader DC擴展中憑據的顯示名稱。 此別名還用於使用表單SDK以寫程式方式訪AEM問憑據。
1. 按一下選擇檔案以查找憑據，鍵入憑據的密碼，然後按一下確定。

如果出現錯誤消息「由於檔案格式不正確或密碼不正確而導入憑據失敗」，請驗證密碼是否有效。

您也可以以寫程式方式導入和刪除憑據。 (請參閱 [用表格編AEM程](../../developing/credentials.md)。)

### 從現有啟用權限的PDF文檔中刪除使用權限

在應用具有最新憑據的使用權限之前，從現有啟用權限的PDF文檔中刪除使用權限。 AEM Forms在JEE上提供API以刪除使用權限。 有關詳細說明，請參見 [從PDF文檔中刪除使用權限](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)。

要刪除在Workbench中開發的JEE流程上AEM Forms的使用權限，請參閱 [工作台幫助](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf)。

### 將使用權限應用於PDF文檔

在導入新憑據並從現有啟用權限的PDF文檔中刪除使用權限後，使用新憑據將使用權限應用於PDF文檔。 可以使用Acrobat Reader DC擴展Java客戶端API和Web服務對PDF文檔應用使用權限。  有關詳細資訊，請參閱 [將使用權限應用於PDF文檔](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。


## 在OSGi環境上更新和申請AEM Forms證書 {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

在OSGi堆棧上更新和應用AEM Forms上的新證書需要導入新憑據、從現有PDF文檔中刪除使用權限以及應用使用權限。 您可以使用管理控制台導入憑據，而AEM FormsReader擴展API則刪除和應用使用權限。

### 導入憑據 {#Import-credentials}

在OSGi環境上的AEM Forms中，Reader擴展憑據與fd-service用戶相關聯。 添加fd用戶密鑰儲存的憑據之前，請執行以下步驟建立密鑰儲存：

1. 以管理員身份登錄到AEM作者實例。
1. 轉到 **[!UICONTROL 工具]**> **[!UICONTROL 安全]**>**[!UICONTROL 用戶]**。
1. 向下滾動用戶清單，直到找到fd-service用戶帳戶。
1. 按一下 **[!UICONTROL fd服務]** 。
1. 按一下「密鑰庫」頁籤。
1. 按一下 **[!UICONTROL 建立密鑰儲存]**。
1. 設定KeyStore訪問密碼並保存設定以建立KeyStore密碼。

建立密鑰儲存後，向fd-service用戶添加憑據。 以下視頻說明了步驟：

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

以下命令列出pfx檔案的詳細資訊。 在運行命令之前，導航到包含.pfx檔案的目錄。

`keytool -v -list -storetype pkcs12 -keystore <name of your .pfx file>`

例如keytool -v -list -storetype pkcs12 -keystore 1005566.pfx，其中1005566.pfx是我的pfx檔案的名稱

### 從現有啟用權限的PDF文檔中刪除使用權限

在應用具有最新憑據的使用權限之前，從現有啟用權限的PDF文檔中刪除使用權限。 通過從docAssuranceServiceAPI中調用removeUsageRights API，可以刪除文檔的使用權限。 有關詳細資訊，請參見 [刪除使用權限](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) 的子菜單。

### 將使用權限應用於PDF文檔

要在OSGi環境上的AEM Forms中應用使用權，請建立自定義OSGi服務以獲取文檔的使用權。 還可以使用POST方法建立Servlet，以將讀取器擴展PDF返回給用戶。 有關詳細說明，請參見 [應用Reader擴展](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html)。

## 常見問題

**如果我有其他問題，應聯繫誰？**

您可以聯繫 [Adobe支援](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) 或者提出支援票。

**如果我在2023年1月7日之前不更新我的證書，會發生什麼情況？**

在嘗試開啟PDF文檔時，用戶會遇到錯誤消息，並且無法再訪問讀取器擴展的功能。 示例錯誤為。

`The document has been changed since it was created and use of extended features in no longer available. Please contact the author for the orignal version of this document.`

**新描述的名稱是否有任何更改？**

新Reader擴展證書在說明中將G3-P24作為程式名稱。 在較舊的證書中，說明中提到了程式名P24。
