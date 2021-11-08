---
title: 更新過期的Reader擴展服務證書
description: 'Reader擴展文檔無法工作，請更新證書 '
source-git-commit: 5f2fc6a32f67cfed3bc4b09b63bcf9689659a99d
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 0%

---


# 更新過期的Reader擴展服務證書 {#Updating-expired-Reader-Extension-service-certificates}

Adobe Experience Manager Forms(AEM Forms)擁有Adobe Managed Services或內部部署企業基礎授權的客戶，有權使用Reader擴充功能服務。 此服務可讓組織透過擴充Adobe Reader的功能與其他使用權限，輕鬆共用互動式PDF檔案。 此服務向PDF文檔添加使用權限，並激活在使用Adobe Acrobat Reader DC開啟PDF文檔時通常不可用的功能，例如向文檔添加註釋、填寫表單和保存文檔。 協力廠商使用者不需要其他軟體或外掛程式，即可使用啟用權限的檔案。 添加了使用權限的PDF文檔稱為啟用權限的文檔。 在Adobe Reader中開啟啟用權限的PDF文檔的用戶可以執行為該文檔啟用的操作。

Adobe利用PKI（公鑰基礎設施）頒發用於許可和功能啟用的數字證書。 Adobe已根據憑證授權單位「Adobe根CA」核發憑證，預計於2023年1月7日到期。 這將導致根據此證書頒發機構頒發的所有證書過期。 憑證過期後，依賴憑證的所有功能都將無法繼續運作。 例如，可使用Adobe Acrobat Reader新增註解的Reader延伸PDF檔案，在2023年1月7日後停止供客戶使用。 要解決此問題，Reader擴充服務的管理員應使用舊憑證，取得新Adobe根CA G2核發的新憑證，並重新套用至其PDF檔案(閱讀器會以新憑證擴充PDF檔案)。

憑證的過期將同時影響JEE上的AEM Forms和OSGi堆疊上的AEM Forms。 這兩個堆棧都具有不同的指令集。 根據您的堆疊，選擇下列其中一個路徑：

* 更新JEE環境上AEM Forms的憑證
* 更新OSGi環境上AEM Forms的憑證

>[!NOTE]
>
>該檔案交互使用術語證書和憑據。

## 先決條件 {#Pre-requisites}

更新憑證時，必須使用AEM Forms提供之AEM Forms管理員主控台和Reader擴充功能API上的動作。 本檔案適用於熟悉使用Adobe Experience Manager Forms API的使用者和管理員。 開始之前，請確定：

* 使用者具有基礎AEM Forms環境的管理員權限。
* 使用者已設定 [開發環境](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) 並且有權訪問。
* 取得憑證。

### 取得憑證 {#obtain-the-certificates}

權限憑證是以數位憑證的形式傳送，其中包含公開金鑰、私密金鑰和用來存取憑證的密碼。

如果您的組織購買生產版本的Reader擴充功能，則生產權限憑證是由Adobe授權網站(LWS)傳送。 生產權限憑證是貴組織專屬的，可啟用您需要的特定使用權限。

如果您是透過將Reader擴充功能整合至其軟體的合作夥伴或軟體提供者取得Reader擴充功能，該合作夥伴會向您提供權限憑證，而該合作夥伴又會從Adobe接收此憑證。

>[!NOTE]
>
>權限憑據不能用於典型文檔簽名或身份聲明。 對於這些應用程式，您可以使用自簽名證書或從證書頒發機構(CA)獲取身份證書。

可使用下列類型的權限憑證：

**客戶評估**:為想評估Reader擴展的客戶提供的具有短有效期的憑據。 應用於使用此憑據的文檔的使用權限在憑據過期時到期。 此類型的憑據只有兩到三個月的有效期。

**生產**:為購買完整產品的客戶提供的具有長有效期的憑據。 每個客戶都有專屬的生產憑證，但可安裝在多個系統上。

如果您已使用憑證來讀取器擴充PDF檔案，請從下載生產憑證 [Adobe授權網站(LWS)](https://licensing.adobe.com/).

## 更新和套用JEE環境上AEM Forms的憑證 {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment}

在JEE堆疊上更新和套用AEM Forms上的新憑證時，需要匯入新憑證、從現有PDF檔案中移除使用權限，以及套用使用權限。 您可以使用Admin Console匯入憑證，並使用AEM FormsReader擴充功能API來移除和套用使用權限。

### 匯入和設定憑證

您可以使用「信任儲存管理」頁導入新憑據或替換憑據。 信任儲存可包含多個Reader擴展憑據。 您必須指定其中一個憑據作為預設Reader擴展憑據。 當Workbench使用者無法判斷在建立程式期間要使用的憑證時，會使用預設憑證。 這些規則適用於預設憑證：

* 如果您匯入Reader擴充功能憑證，且信任存放區不包含其他Reader擴充功能憑證，則會將其設為預設。
* 如果導入了「預設」選項的Reader擴展憑據，則預設類型將從現有預設憑據中刪除。 導入的憑據成為預設憑據。
* 無法刪除預設Reader擴展憑據。 要刪除預設憑據，請首先將另一個憑據設定為預設憑據。 此規則的一個例外是，如果只有一個憑據，則即使是預設憑證，您仍可將其刪除。
* 無法更新預設Reader擴展憑據。

要導入憑據，請執行以下操作：

1. 在管理控制台中，按一下「設定」>「信任儲存管理」>「本地憑據」。
1. 按一下「匯入」 ，然後在「信任存放區類型」下方選取「Acrobat Reader DC擴充功能憑證」。
1. （可選）若要指出此憑證是搭配Acrobat Reader DC擴充功能使用的預設憑證，請選取「預設」。
1. 在「別名」框中，鍵入憑據的標識符。 此識別碼會作為Acrobat Reader DC擴充功能中憑證的顯示名稱。 此別名也可用來使用AEM Forms SDK以程式設計方式存取憑證。
1. 按一下選擇檔案以查找憑據，鍵入憑據的密碼，然後按一下確定。

如果出現「由於檔案格式不正確或密碼錯誤而導致無法導入憑據」錯誤消息，請驗證密碼是否有效。

您也可以以程式設計方式匯入和刪除憑證。 (請參閱 [使用AEM表單進行程式設計](../../developing/credentials.md).)

### 從啟用權限的現有PDF文檔中刪除使用權限

在應用具有最新憑據的使用權限之前，從啟用權限的現有PDF文檔中刪除使用權限。 AEM Forms on JEE提供API來移除使用權限。 如需詳細指示，請參閱 [從PDF文檔中刪除使用權限](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

若要移除在Workbench中開發之AEM Forms JEE程式上的使用權限，請參閱 [Workbench說明](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf).

### 將使用權應用於PDF文檔

導入新憑據並從啟用權限的現有PDF文檔中刪除使用權限後，使用新憑據將使用權限應用於PDF文檔。 您可以使用Acrobat Reader DC擴充功能Java Client API和網站服務，將使用權套用至PDF檔案。  如需詳細資訊，請參閱 [將使用權應用於PDF文檔](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).


## 在OSGi環境中更新和套用AEM Forms的憑證 {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

在OSGi堆疊上更新和套用AEM Forms上的新憑證時，需要匯入新憑證、從現有PDF檔案中移除使用權限，以及套用使用權限。 您可以使用Admin Console匯入憑證，並使用AEM FormsReader擴充功能API來移除和套用使用權限。

### 導入憑據 {#Import-credentials}

在OSGi環境上的AEM Forms中，Reader擴充功能憑證與fd-service使用者相關聯。 添加fd-user密鑰儲存的憑據之前，請執行以下步驟以建立密鑰儲存：

1. 以管理員身分登入您的AEM Author例項。
1. 前往「工具>安全性>使用者」。
1. 向下捲動使用者清單，直到找到fd-service使用者帳戶為止。
1. 按一下fd-service用戶。
1. 按一下金鑰存放區索引標籤。
1. 按一下「建立金鑰存放區」。
1. 設定KeyStore訪問密碼並保存您的設定以建立KeyStore密碼。

建立金鑰存放區後，將憑證新增至fd-service使用者。

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

以下命令列出pfx檔案的詳細資訊。 在運行命令之前，導航到包含.pfx檔案的目錄。

`keytool -v -list -storetype pkcs12 -keystore <name of your .pfx file>`

例如keytool -v -list -storetype pkcs12 -keystore 1005566.pfx，其中1005566.pfx是我的pfx檔案的名稱

### 從啟用權限的現有PDF文檔中刪除使用權限

在應用具有最新憑據的使用權限之前，從啟用權限的現有PDF文檔中刪除使用權限。 通過從docAssuranceServiceAPI中調用removeUsageRights API，可以刪除文檔的使用權限。 如需詳細資訊，請參閱 [移除使用權限](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) 檔案。

### 將使用權應用於PDF文檔

若要在OSGi環境上套用AEM Forms中的使用權限，請建立自訂OSGi服務以套用檔案的使用權限。 您也可以使用POST方法建立Servlet，將Reader延伸PDF傳回給使用者。 如需詳細指示，請參閱 [套用Reader擴充功能](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).

## 常見問題

**如有其他問題，應聯絡誰？**

您可以聯絡 [Adobe支援](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) 或提供支援票。

**如果我在2023年1月7日之前未更新憑證，會發生什麼事？**

嘗試開啟PDF文檔Reader時，用戶將遇到錯誤消息，無法再訪問讀者擴展功能。 範例錯誤為。

`The document has been changed since it was created and use of extended features in no longer available. Please contact the author for the orignal version of this document.`

**新說明的名稱有任何變更嗎？**

新的Reader擴充功能憑證在說明中將G3-P24列為方案名稱。 在舊證書中，說明中提到了方案名P24。