---
title: 使用策略保護文檔
seo-title: Protecting Documents with Policies
description: 使用文檔安全服務動態地將機密性設定應用於Adobe PDF文檔並維護對文檔的控制。 文檔安全服務還允許用戶對收件人使用受策略保護的PDF文檔的方式進行控制。
seo-description: Use the Document Security service to dynamically apply confidentiality settings to Adobe PDF documents and to maintain control over the documents. The Document Security service also enables the users to maintain control over how recipients use the policy-protected PDF document.
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
role: Developer
exl-id: ff42579e-6aaf-433d-8b5d-9e9dd0957250
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '15514'
ht-degree: 0%

---

# 使用策略保護文檔 {#protecting-documents-with-policies}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

**關於文檔安全服務**

文檔安全服務使用戶能夠動態地將機密性設定應用於Adobe PDF文檔，並保持對文檔的控制，無論這些文檔的分佈有多廣泛。

文檔安全服務通過讓用戶能夠保持對收件人使用受策略保護的PDF文檔的方式的控制，防止資訊擴散到用戶的範圍之外。 用戶可以指定誰可以開啟文檔，限制他們如何使用文檔，並在文檔分發後監視文檔。 用戶還可以動態地控制對受策略保護文檔的訪問，甚至可以動態地撤消對文檔的訪問。

文檔安全服務還保護其他檔案類型，如MicrosoftWord檔案（DOC檔案）。 可以使用文檔安全客戶端API來處理這些檔案類型。 支援以下版本：

* MicrosoftOffice 2003檔案（DOC、XLS、PPT檔案）
* MicrosoftOffice 2007檔案（DOCX、XLSX、PPTX檔案）
* PTC Pro/E檔案

為了清晰起見，以下兩節將討論如何使用Word文檔：

* [將策略應用於Word文檔](protecting-documents-policies.md#applying-policies-to-word-documents)
* [從Word文檔中刪除策略](protecting-documents-policies.md#removing-policies-from-word-documents)

您可以使用文檔安全服務完成以下任務：

* 建立策略。 有關資訊，請參見 [建立策略](protecting-documents-policies.md#creating-policies)。
* 修改策略。 有關資訊，請參見 [修改策略](protecting-documents-policies.md#modifying-policies)。
* 刪除策略。 有關資訊，請參見 [刪除策略](protecting-documents-policies.md#deleting-policies)。
* 將策略應用於PDF文檔。 有關資訊，請參見 [將策略應用於PDF文檔](protecting-documents-policies.md#applying-policies-to-pdf-documents)。
* 從PDF文檔中刪除策略。 有關資訊，請參見 [從PDF文檔中刪除策略](protecting-documents-policies.md#removing-policies-from-pdf-documents)。
* Inspect政策保護檔案。 有關資訊，請參見 [檢查策略保護的PDF文檔](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)。
* 撤消對PDF文檔的訪問。 有關資訊，請參見 [撤消對文檔的訪問](protecting-documents-policies.md#revoking-access-to-documents)。
* 恢復對已撤消文檔的訪問權限。 有關資訊，請參見 [恢復對已撤消文檔的訪問](protecting-documents-policies.md#reinstating-access-to-revoked-documents)。
* 建立水印。 有關資訊，請參見 [建立水印](protecting-documents-policies.md#creating-watermarks)。
* 搜索事件。 有關資訊，請參見 [搜索事件](protecting-documents-policies.md#searching-for-events)。

>[!NOTE]
>
>有關文檔安全服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 建立策略 {#creating-policies}

可以使用Document Security Java API或Web服務API以寫程式方式建立策略。 A *政策* 是包含文檔安全設定、授權用戶和使用權限的資訊的集合。 可以使用適合不同情況和用戶的安全設定建立和保存任意數量的策略。

策略使您能夠執行以下任務：

* 指定可開啟文檔的個人。 收件人可以屬於您的組織，也可以是您的組織的外部收件人。
* 指定收件人如何使用文檔。 您可以限制訪問不同的Acrobat和Adobe Reader功能。 這些功能包括打印和複製文本、添加簽名和向文檔添加註釋的能力。
* 即使在分發受策略保護的文檔後，也可以隨時更改訪問和安全設定。
* 在分發文檔後監視文檔的使用。 您可以查看文檔的使用方式以及使用者。 例如，您可以查找某人何時開啟了文檔。

### 使用Web服務建立策略 {#creating-a-policy-using-web-services}

使用Web服務API建立策略時，請參考描述該策略的現有可移植文檔權限語言(PDRL)XML檔案。 策略權限和承擔者在PDRL文檔中定義。 以下XML文檔是PDRL文檔的示例。

```xml
 <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
 <Policy PolicyInstanceVersion="1" PolicyID="5DA3F847-DE76-F9CC-63EA-49A8D59154DE" PolicyCreationTime="2004-08-30T00:02:28.294+00:00" PolicyType="1" PolicySchemaVersion="1.0" PolicyName="SDK Test Policy -4344050357301573237" PolicyDescription="An SDK Test policy" xmlns="https://www.adobe.com/schema/1.0/pdrl">
       <PolicyEntry>
          <ns1:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns1="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns2:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns2="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns3:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns3="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns4:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns4="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>all_internal_users</PrincipalName>
          </Principal>
       </PolicyEntry>
       <PolicyEntry>
          <ns5:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns5="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns6:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns6="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns7:Permission PermissionName="com.adobe.aps.pdf.copy" Access="ALLOW" xmlns:ns7="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns8:Permission PermissionName="com.adobe.aps.pdf.printLow" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns8="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns9:Permission PermissionName="com.adobe.aps.policySwitch" Access="ALLOW" xmlns:ns9="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns10:Permission PermissionName="com.adobe.aps.revoke" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns10="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns11:Permission PermissionName="com.adobe.aps.pdf.edit" Access="ALLOW" xmlns:ns11="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns12:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns12="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns13:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns13="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns14:Permission PermissionName="com.adobe.aps.pdf.printHigh" Access="ALLOW" xmlns:ns14="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>publisher</PrincipalName>
          </Principal>
       </PolicyEntry>
 
       <OfflineLeasePeriod>
          <Duration>P31D</Duration>
       </OfflineLeasePeriod>
 
       <AuditSettings isTracked="true" />
 
       <PolicyValidityPeriod isAbsoluteTime="false">
          <ValidityPeriodRelative>
             <NotBeforeRelative>PT0S</NotBeforeRelative>
 
             <NotAfterRelative>P20D</NotAfterRelative>
          </ValidityPeriodRelative>
       </PolicyValidityPeriod>
 </Policy>
 
```

>[!NOTE]
>
>有關文檔安全服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要建立策略，請執行以下步驟：

1. 包括項目檔案。
1. 建立文檔安全客戶端API對象。
1. 設定策略的屬性。
1. 建立策略條目。
1. 註冊策略。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-rightsmanagement-client.jar
* namespace.jar(如果AEM Forms部署在JBoss上)
* jaxb-api.jar(如果AEM Forms部署在JBoss上)
* jaxb-impl.jar(如果AEM Forms部署在JBoss上)
* jaxb-libs.jar(如果AEM Forms部署在JBoss上)
* jaxb-xjc.jar(如果AEM Forms部署在JBoss上)
* relangDatatype.jar(如果AEM Forms部署在JBoss上)
* xsdlib.jar(如果AEM Forms部署在JBoss上)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar(如果AEM Forms未部署在JBoss上，則使用其他JAR檔案)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立文檔安全客戶端API對象**

在以寫程式方式執行文檔安全服務操作之前，請建立文檔安全服務客戶端對象。

**設定策略的屬性**

要建立策略，請設定策略屬性。 強制屬性是策略名稱。 每個策略集的策略名稱必須唯一。 策略集只是策略的集合。 如果策略屬於單獨的策略集，則可以有兩個具有相同名稱的策略。 但是，單個策略集中的兩個策略不能具有相同的策略名稱。

要設定的另一個有用屬性是有效期。 有效期是指受策略保護的文檔可供授權的收件人訪問的時間段。 如果未設定此屬性，則策略始終有效。

有效期可設定為以下選項之一：

* 從文檔發佈時開始可訪問文檔的設定天數
* 文檔無法訪問的結束日期
* 文檔可訪問的特定日期範圍
* 始終有效

您只能指定開始日期，這將導致策略在開始日期之後有效。 如果僅指定結束日期，則策略在結束日期之前有效。 但是，如果未定義開始日期和結束日期，則會引發異常。

在設定屬於策略的屬性時，還可以設定加密設定。 這些加密設定在策略應用於文檔時生效。 可以指定以下加密值：

* **AES256**:表示AES加密算法，使用256位密鑰。
* **AES128**:表示AES加密算法，使用128位密鑰。
* **無加密：** 表示未加密。

指定 `NoEncryption` 選項，則無法設定 `PlaintextMetadata` 選項 `false`。 如果嘗試執行此操作，則會引發異常。

>[!NOTE]
>
>有關可設定的其他屬性的資訊，請參閱 `Policy` 介面說明 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**建立策略條目**

策略條目會附加承擔者（即組和用戶）和對策略的權限。 策略必須至少有一個策略條目。 例如，假定您執行以下任務：

* 建立並註冊策略條目，該條目使組只能在聯機時查看文檔，並禁止收件人複製文檔。
* 將策略條目附加到策略。
* 使用Acrobat保護策略的文檔。

這些操作導致收件人只能聯機查看文檔，無法複製文檔。 在從文檔中刪除安全性之前，文檔將保持安全。

**註冊策略**

必須先註冊新策略，然後才能使用它。 註冊策略後，可以使用它來保護文檔。

### 使用Java API建立策略 {#create-a-policy-using-the-java-api}

使用Document Security API(Java)建立策略：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-rightsmanagement-client.jar。

1. 建立文檔安全客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocumentSecurityClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 設定策略的屬性。

   * 建立 `Policy` 通過調用 `InfomodelObjectFactory` 對象的靜態 `createPolicy` 的雙曲餘切值。 此方法返回 `Policy` 的雙曲餘切值。
   * 通過調用 `Policy` 對象 `setName` 方法並傳遞指定策略名稱的字串值。
   * 通過調用 `Policy` 對象 `setDescription` 方法，並傳遞指定策略說明的字串值。
   * 通過調用 `Policy` 對象 `setPolicySetName` 方法並傳遞指定策略集名稱的字串值。 (您可以指定 `null` 將策略添加到 *我的策略* 策略集。)
   * 通過調用 `InfomodelObjectFactory` 對象的靜態 `createValidityPeriod` 的雙曲餘切值。 此方法返回 `ValidityPeriod` 的雙曲餘切值。
   * 通過調用 `ValidityPeriod` 對象 `setRelativeExpirationDays` 方法和傳遞一個指定天數的整數值。
   * 通過調用 `Policy` 對象 `setValidityPeriod` 方法和傳遞 `ValidityPeriod` 的雙曲餘切值。

1. 建立策略條目。

   * 通過調用 `InfomodelObjectFactory` 對象的靜態 `createPolicyEntry` 的雙曲餘切值。 此方法返回 `PolicyEntry` 的雙曲餘切值。
   * 通過調用 `InfomodelObjectFactory` 對象的靜態 `createPermission` 的雙曲餘切值。 傳遞屬於的靜態資料成員 `Permission` 表示權限的介面。 此方法返回 `Permission` 的雙曲餘切值。 例如，要添加允許用戶從受策略保護的PDF文檔中複製資料的權限，請傳遞 `Permission.COPY`。 （對要添加的每個權限重複此步驟）。
   * 通過調用 `PolicyEntry` 對象 `addPermission` 方法和傳遞 `Permission` 的雙曲餘切值。 (對每個 `Permission` 建立的對象)。
   * 通過調用 `InfomodelObjectFactory` 對象的靜態 `createSpecialPrincipal` 的雙曲餘切值。 傳遞屬於 `InfomodelObjectFactory` 表示主體的對象。 此方法返回 `Principal` 的雙曲餘切值。 例如，要將文檔的發佈者添加為主體，請通過 `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`。
   * 通過調用 `PolicyEntry` 對象 `setPrincipal`方法和傳遞 `Principal` 的雙曲餘切值。
   * 通過調用 `Policy` 對象 `addPolicyEntry` 方法和傳遞 `PolicyEntry` 的雙曲餘切值。

1. 註冊策略。

   * 建立 `PolicyManager` 通過調用 `DocumentSecurityClient` 對象 `getPolicyManager` 的雙曲餘切值。
   * 通過調用 `PolicyManager` 對象 `registerPolicy` 方法並傳遞以下值：

      * 的 `Policy` 表示要註冊的策略的對象。
   * 一個字串值，它表示策略所屬的策略集。

   如果在連接設定AEM中使用表單管理員帳戶建立 `DocumentSecurityClient` 對象，然後在調用策略集名稱時指定 `registerPolicy` 的雙曲餘切值。 如果你通過 `null` 策略集的值，策略是在管理員中建立的 *我的策略* 策略集。

   如果在連接設定中使用「文檔安全性」用戶，則可以調用重載 `registerPolicy` 只接受策略的方法。 即，您不需要指定策略集名稱。 但是，策略將添加到名為 *我的策略*。 如果不想將新策略添加到此策略集，則在調用 `registerPolicy` 的雙曲餘切值。

   >[!NOTE]
   >
   >建立策略時，請引用現有策略集。 如果指定不存在的策略集，則會引發異常。

有關使用文檔安全服務的代碼示例，請參閱：

* 「快速啟動（SOAP模式）:使用Java API建立策略&quot;

### 使用Web服務API建立策略 {#create-a-policy-using-the-web-service-api}

使用Document Security API（Web服務）建立策略：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立文檔安全客戶端API對象。

   * 建立 `DocumentSecurityServiceClient` 對象。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `RightsManagementServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。


1. 設定策略的屬性。

   * 建立 `PolicySpec` 對象。
   * 通過將字串值分配給 `PolicySpec` 對象 `name` 資料成員。
   * 通過將字串值分配給 `PolicySpec` 對象 `description` 資料成員。
   * 通過將字串值分配給 `PolicySpec` 對象 `policySetName` 資料成員。 必須指定現有策略集名稱。 (您可以指定 `null` 為此參數值添加策略 *我的策略*。)
   * 通過為策略分配整數值來設定策略的離線租用期 `PolicySpec` 對象 `offlineLeasePeriod` 資料成員。
   * 設定 `PolicySpec` 對象 `policyXml` 資料成員，其字串值表示PDRL XML資料。 要執行此任務，請建立.NET `StreamReader` 對象。 將表示策略的PDRL XML檔案的位置傳遞給 `StreamReader` 建構子。 接下來，調用 `StreamReader` 對象 `ReadLine` 將返回值指定給字串變數。 迭代 `StreamReader` 對象，直到 `ReadLine` 方法返回null。 將字串變數分配給 `PolicySpec` 對象 `policyXml` 資料成員。

1. 建立策略條目。

   使用Document Security Web服務API建立策略時，無需建立策略條目。 策略條目在PDRL文檔中定義。

1. 註冊策略。

   通過調用 `DocumentSecurityServiceClient` 對象 `registerPolicy` 方法並傳遞以下值：

   * 的 `PolicySpec` 表示要註冊的策略的對象。
   * 一個字串值，它表示策略所屬的策略集。 可以指定 `null` 將策略添加到 *我的策略* 策略集。

   如果在連接設定AEM中使用表單管理員帳戶建立 `DocumentSecurityClient` 對象，在調用策略集名稱時指定 `registerPolicy` 的雙曲餘切值。

   如果在連接設定中使用Document SecurityDocument Security用戶，則可以調用重載 `registerPolicy` 只接受策略的方法。 即，您不需要指定策略集名稱。 但是，策略將添加到名為 *我的策略*。 如果不想將新策略添加到此策略集，則在調用 `registerPolicy` 的雙曲餘切值。

   >[!NOTE]
   >
   >建立策略並指定策略集時，請確保指定現有策略集。 如果指定不存在的策略集，則會引發異常。

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動(MTOM):使用Web服務API建立策略&quot;
* 「快速啟動(SwaRef):使用Web服務API建立策略&quot;

## 修改策略 {#modifying-policies}

可以使用Document Security Java API或Web服務API修改現有策略。 要更改現有策略，請檢索它、修改它，然後在伺服器上更新策略。 例如，假定您檢索了現有策略並延長其有效期。 在更改生效之前，必須更新策略。

當業務要求發生更改且該策略不再反映這些要求時，您可以修改策略。 您不必建立新策略，只需更新現有策略即可。

要使用Web服務修改策略屬性（例如，使用使用JAX-WS建立的Java代理類），必須確保策略已註冊到文檔安全服務。 然後，可以使用 `PolicySpec.getPolicyXml` 方法，並使用適用的方法修改策略屬性。 例如，可以通過調用 `PolicySpec.setOfflineLeasePeriod` 的雙曲餘切值。

>[!NOTE]
>
>有關文檔安全服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要修改現有策略，請執行以下步驟：

1. 包括項目檔案。
1. 建立文檔安全客戶端API對象。
1. 檢索現有策略。
1. 更改策略屬性。
1. 更新策略。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立文檔安全客戶端API對象**

在以寫程式方式執行Document SecurityService操作之前，必須建立Document Security服務客戶端對象。 如果使用Java API，請建立 `RightsManagementClient` 的雙曲餘切值。 如果使用Document Security Web服務API，請建立 `RightsManagementServiceService` 的雙曲餘切值。

**檢索現有策略**

必須檢索現有策略才能修改它。 要檢索策略，請指定策略名稱和策略所屬的策略集。 如果指定 `null` 策略集名稱的值，從 *我的策略* 策略集。

**設定策略的屬性**

要修改策略，請修改策略屬性的值。 唯一不能更改的策略屬性是name屬性。 例如，要更改策略的離線租用期，可以修改策略的離線租用期屬性值。

使用Web服務修改策略的離線租用期時， `offlineLeasePeriod` 的 `PolicySpec` 介面被忽略。 要更新離線租用期，請修改 `OfflineLeasePeriod` 元素。 然後，使用 `PolicySpec` 介面 `policyXML` 資料成員。

>[!NOTE]
>
>有關可設定的其他屬性的資訊，請參閱 `Policy` 介面說明 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**更新策略**

在對策略所做的更改生效之前，必須使用文檔安全服務更新策略。 對保護文檔的策略的更改將在下次將受策略保護的文檔與文檔安全服務同步時更新。

### 使用Java API修改現有策略 {#modify-existing-policies-using-the-java-api}

使用Document Security API(Java)修改現有策略：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-rightsmanagement-client.jar。

1. 建立文檔安全客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `RightsManagementClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索現有策略。

   * 建立 `PolicyManager` 通過調用 `RightsManagementClient` 對象 `getPolicyManager` 的雙曲餘切值。
   * 建立 `Policy` 通過調用 `PolicyManager` 對象 `getPolicy` 方法並傳遞以下值」

      * 一個字串值，它表示策略所屬的策略集名稱。 可以指定 `null` 導致 `MyPolicies` 正在使用的策略集。
      * 表示策略名稱的字串值。

1. 設定策略的屬性。

   更改策略的屬性以滿足您的業務要求。 例如，要更改策略的離線租用期，請調用 `Policy` 對象 `setOfflineLeasePeriod` 的雙曲餘切值。

1. 更新策略。

   通過調用更新策略 `PolicyManager` 對象 `updatePolicy` 的雙曲餘切值。 通過 `Policy` 表示要更新的策略的對象。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱快速啟動（SOAP模式）:使用Java API部分修改策略。

### 使用Web服務API修改現有策略 {#modify-existing-policies-using-the-web-service-api}

使用文檔安全API（Web服務）修改現有策略：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立文檔安全客戶端API對象。

   * 建立 `RightsManagementServiceClient` 對象。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `RightsManagementServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。


1. 檢索現有策略。

   建立 `PolicySpec` 表示要通過調用 `RightsManagementServiceClient` 對象 `getPolicy` 方法並傳遞以下值：

   * 一個字串值，它指定策略所屬的策略集名稱。 可以指定 `null` 導致 `MyPolicies` 正在使用的策略集。
   * 指定策略名稱的字串值。

1. 設定策略的屬性。

   更改策略的屬性以滿足您的業務要求。

1. 更新策略。

   通過調用 `RightsManagementServiceClient` 對象 `updatePolicyFromSDK` 方法和傳遞 `PolicySpec` 表示要更新的策略的對象。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動(MTOM):使用Web服務API修改策略&quot;
* 「快速啟動(SwaRef):使用Web服務API修改策略&quot;

## 刪除策略 {#deleting-policies}

可以使用Document Security Java API或Web服務API刪除現有策略。 刪除策略後，將不能再用於保護文檔。 但是，使用策略的現有受策略保護的文檔仍受到保護。 當較新的策略可用時，可以刪除策略。

>[!NOTE]
>
>有關文檔安全服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

要刪除現有策略，請執行以下步驟：

1. 包括項目檔案
1. 建立文檔安全客戶端API對象。
1. 刪除策略。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立文檔安全客戶端API對象**

在以寫程式方式執行Document Security服務操作之前，必須建立Document Security服務客戶端對象。 如果使用Java API，請建立 `RightsManagementClient` 的雙曲餘切值。 如果使用Document Security Web服務API，請建立 `RightsManagementServiceService` 的雙曲餘切值。

**刪除策略**

要刪除策略，請指定要刪除的策略以及該策略所屬的策略集。 其設定用於調用AEM Forms的用戶必須具有刪除策略的權限；否則會發生異常。 同樣，如果嘗試刪除不存在的策略，則會發生異常。

### 使用Java API刪除策略 {#delete-policies-using-the-java-api}

使用Document Security API(Java)刪除策略：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-rightsmanagement-client.jar。

1. 建立文檔安全客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `RightsManagementClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 刪除策略。

   * 建立 `PolicyManager` 通過調用 `RightsManagementClient` 對象 `getPolicyManager` 的雙曲餘切值。
   * 通過調用 `PolicyManager` 對象 `deletePolicy` 方法並傳遞以下值：

      * 一個字串值，它指定策略所屬的策略集名稱。 可以指定 `null` 導致 `MyPolicies` 正在使用的策略集。
      * 一個字串值，它指定要刪除的策略的名稱。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動（SOAP模式）:使用Java API刪除策略&quot;

### 使用Web服務API刪除策略 {#delete-policies-using-the-web-service-api}

使用Document Security API（Web服務）刪除策略：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立文檔安全客戶端API對象。

   * 建立 `RightsManagementServiceClient` 對象。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `RightsManagementServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。


1. 刪除策略。

   通過調用 `RightsManagementServiceClient` 對象 `deletePolicy` 方法並傳遞以下值：

   * 一個字串值，它指定策略所屬的策略集名稱。 可以指定 `null` 導致 `MyPolicies` 正在使用的策略集。
   * 一個字串值，它指定要刪除的策略的名稱。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動(MTOM):使用Web服務API刪除策略&quot;
* 「快速啟動(SwaRef):使用Web服務API刪除策略&quot;

## 將策略應用於PDF文檔 {#applying-policies-to-pdf-documents}

您可以將策略應用於PDF文檔以保護文檔。 通過將策略應用於PDF文檔，可以限制對文檔的訪問。 如果文檔已使用策略進行保護，則不能將策略應用於文檔。

當文檔處於開啟狀態時，您還可以限制對Acrobat和Adobe Reader功能的訪問，包括打印和複製文本、進行更改以及向文檔添加簽名和注釋的能力。 此外，當您不再希望用戶訪問該文檔時，您可以撤消受策略保護的PDF文檔。

在分發受策略保護的文檔後，可以監視其使用情況。 即，您可以看到文檔的使用方式和使用者。 例如，您可以查找某人何時開啟了文檔。

>[!NOTE]
>
>有關文檔安全服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-3}

要將策略應用於PDF文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立文檔安全客戶端API對象。
1. 檢索應用策略的PDF文檔。
1. 將現有策略應用於PDF文檔。
1. 保存受策略保護的PDF文檔。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立文檔安全客戶端API對象**

在以寫程式方式執行文檔安全服務操作之前，請建立文檔安全服務客戶端對象。 如果使用Java API，請建立 `DocumentSecurityClient` 的雙曲餘切值。 如果使用Document Security Web服務API，請建立 `DocumentSecurityServiceService` 的雙曲餘切值。

**檢索PDF文檔**

可以檢索PDF文檔以應用策略。 將策略應用到PDF文檔後，用戶在使用文檔時受到限制。 例如，如果策略未啟用離線時開啟文檔，則用戶必須聯機才能開啟文檔。

**將現有策略應用於PDF文檔**

要將策略應用於PDF文檔，請引用現有策略並指定策略所屬的策略集。 設定連接屬性的用戶必須有權訪問指定的策略。 否則，將發生異常。

**保存PDF文檔**

文檔安全服務將策略應用於PDF文檔後，可以將受策略保護的PDF文檔另存為PDF檔案。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[撤消對文檔的訪問](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API將策略應用於PDF文檔 {#apply-a-policy-to-a-pdf-document-using-the-java-api}

使用文檔安全API(Java)將策略應用於PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-rightsmanagement-client.jar。

1. 建立文檔安全客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `RightsManagementClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索PDF文檔。

   * 建立 `java.io.FileInputStream` 表示PDF文檔的對象。 傳遞一個字串值，指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 將現有策略應用於PDF文檔。

   * 建立 `DocumentManager` 通過調用 `RightsManagementClient` 對象 `getDocumentManager` 的雙曲餘切值。
   * 通過調用PDF文檔 `DocumentManager` 對象 `protectDocument` 方法並傳遞以下值：

      * 的 `com.adobe.idp.Document` 包含應用策略的PDF文檔的對象。
      * 指定文檔名稱的字串值。
      * 一個字串值，它指定策略所屬的策略集的名稱。 可以指定 `null` 導致 `MyPolicies` 正在使用的策略集。
      * 指定策略名稱的字串值。
      * 一個字串值，它表示作為文檔發佈者的用戶的用戶管理器域的名稱。 此參數值是可選的，可以為Null（如果此參數為Null，則下一個參數值必須為Null）。
      * 一個字串值，它表示作為文檔發佈者的用戶管理器用戶的規範名稱的名稱。 此參數值是可選的，可以 `null` (如果此參數為null，則上一個參數值必須為 `null`)。
      * A `com.adobe.livecycle.rightsmanagement.Locale` 表示用於選擇MS Office模板的區域設定。 此參數值是可選的，不用於PDF文檔。 要保護PDF文檔，請指定 `null`。

      的 `protectDocument` 方法返回 `RMSecureDocumentResult` 包含受策略保護的PDF文檔的對象。


1. 保存PDF文檔。

   * 調用 `RMSecureDocumentResult` 對象 `getProtectedDoc` 方法獲取受策略保護的PDF文檔。 此方法返回 `com.adobe.idp.Document` 的雙曲餘切值。
   * 建立 `java.io.File` 並確保檔案副檔名為PDF。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `Document` 對象到檔案(確保 `Document` 返回的對象 `getProtectedDoc` )。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* &quot;快速啟動（EJB模式）:使用Java API將策略應用到PDF文檔&quot;
* 「快速啟動（SOAP模式）:使用Java API將策略應用到PDF文檔&quot;

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將策略應用於PDF文檔 {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

使用文檔安全API（Web服務）將策略應用於PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立文檔安全客戶端API對象。

   * 建立 `RightsManagementServiceClient` 對象。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `RightsManagementServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。


1. 檢索PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存應用策略的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 將現有策略應用於PDF文檔。

   通過調用PDF文檔 `RightsManagementServiceClient` 對象 `protectDocument` 方法並傳遞以下值：

   * 的 `BLOB` 包含應用策略的PDF文檔的對象。
   * 指定文檔名稱的字串值。
   * 一個字串值，它指定策略所屬的策略集的名稱。 可以指定 `null` 導致 `MyPolicies` 正在使用的策略集。
   * 指定策略名稱的字串值。
   * 一個字串值，它表示作為文檔發佈者的用戶的用戶管理器域的名稱。 此參數值是可選的，可以為Null(如果此參數為Null，則下一個參數值必須為 `null`)。
   * 一個字串值，它表示作為文檔發佈者的用戶管理器用戶的規範名稱的名稱。 此參數值是可選的，可以為Null(如果此參數為Null，則上一個參數值必須為 `null`)。
   * A `RMLocale` 指定區域設定值的值(例如， `RMLocale.en`)。
   * 用於儲存策略標識符值的字串輸出參數。
   * 用於儲存受策略保護的標識符值的字串輸出參數。
   * 用於儲存mime類型的字串輸出參數(例如， `application/pdf`)。

   的 `protectDocument` 方法返回 `BLOB` 包含受策略保護的PDF文檔的對象。

1. 保存PDF文檔。

   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值來表示受策略保護的PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `protectDocument` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動(MTOM):使用Web服務API將策略應用到PDF文檔&quot;
* 「快速啟動(SwaRef):使用Web服務API將策略應用到PDF文檔

## 從PDF文檔中刪除策略 {#removing-policies-from-pdf-documents}

可以從受策略保護的文檔中刪除策略，以便從文檔中刪除安全性。 即，如果不再希望文檔受策略保護。 如果要使用較新的策略更新受策略保護的文檔，則切換策略將比刪除策略和添加更新的策略更有效。

>[!NOTE]
>
>有關文檔安全服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-4}

要從受策略保護的PDF文檔中刪除策略，請執行以下步驟：

1. 包括項目檔案
1. 建立文檔安全客戶端API對象。
1. 檢索受策略保護的PDF文檔。
1. 從PDF文檔中刪除策略。
1. 保存不安全的PDF文檔。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立文檔安全客戶端API對象**

在以寫程式方式執行文檔安全服務操作之前，請建立文檔安全服務客戶端對象。

**檢索受策略保護的PDF文檔**

可以檢索受策略保護的PDF文檔以刪除策略。 如果嘗試從未受策略保護的PDF文檔中刪除策略，將導致異常。

**從PDF文檔中刪除策略**

如果在連接設定中指定了管理員，則可以從受策略保護的PDF文檔中刪除策略。 否則，用於保護文檔的策略必須包含 `SWITCH_POLICY` 從PDF文檔中刪除策略。 此外，在AEM Forms連接設定中指定的用戶還必須具有該權限。 否則，將引發異常。

**保存不安全的PDF文檔**

在文檔安全服務從PDF文檔中刪除策略後，可以將不安全的PDF文檔另存為PDF檔案。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[將策略應用於PDF文檔](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API從PDF文檔中刪除策略 {#remove-a-policy-from-a-pdf-document-using-the-java-api}

使用文檔安全API(Java)從受策略保護的PDF文檔中刪除策略：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-rightsmanagement-client.jar。

1. 建立文檔安全客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocumentSecurityClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索受策略保護的PDF文檔。

   * 建立 `java.io.FileInputStream` 表示受策略保護的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 從PDF文檔中刪除策略。

   * 建立 `DocumentManager` 通過調用 `DocumentSecurityClient` 對象 `getDocumentManager` 的雙曲餘切值。
   * 通過調用PDF文檔 `DocumentManager` 對象 `removeSecurity` 方法和傳遞 `com.adobe.idp.Document` 包含受策略保護的PDF文檔的對象。 此方法返回 `com.adobe.idp.Document` 包含不安全PDF文檔的對象。

1. 保存不安全的PDF文檔。

   * 建立 `java.io.File` 並確保檔案副檔名為PDF。
   * 調用 `Document` 對象 `copyToFile` 複製內容的方法 `Document` 對象到檔案(確保 `Document` 返回的對象 `removeSecurity` )。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動（SOAP模式）:使用Java API從PDF文檔中刪除策略」

### 使用Web服務API刪除策略 {#remove-a-policy-using-the-web-service-api}

使用文檔安全API（Web服務）從受策略保護的PDF文檔中刪除策略：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立文檔安全客戶端API對象。

   * 建立 `DocumentSecurityServiceClient` 對象。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `DocumentSecurityServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。


1. 檢索受策略保護的PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存從中刪除策略的受策略保護的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 從PDF文檔中刪除策略。

   通過調用PDF文檔 `DocumentSecurityServiceClient` 對象 `removePolicySecurity` 方法和傳遞 `BLOB` 包含受策略保護的PDF文檔的對象。 此方法返回 `BLOB` 包含不安全PDF文檔的對象。

1. 保存不安全的PDF文檔。

   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值來表示不安全PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `removePolicySecurity` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 的子菜單。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動(MTOM):使用Web服務API從PDF文檔中刪除策略
* 「快速啟動(SwaRef):使用Web服務API從PDF文檔中刪除策略」

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 撤消對文檔的訪問 {#revoking-access-to-documents}

您可以撤消對受策略保護的PDF文檔的訪問權限，導致用戶無法訪問該文檔的所有副本。 當用戶嘗試開啟已撤消的PDF文檔時，它們被重定向到可查看已修改文檔的指定URL。 必須以寫程式方式指定用戶重定向到的URL。 當您撤消對文檔的訪問權限時，更改將在用戶下次通過聯機開啟受策略保護的文檔與文檔安全服務同步時生效。

撤銷對文檔的訪問權能提供了額外的安全性。 例如，假定文檔的較新版本可用，並且您不再希望任何人查看過時的版本。 在這種情況下，可以撤消對舊文檔的訪問，除非恢復訪問，否則任何人都無法查看該文檔。

>[!NOTE]
>
>有關文檔安全服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-5}

要撤消受策略保護的文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立文檔安全客戶端API對象。
1. 檢索受策略保護的PDF文檔。
1. 撤消受策略保護的文檔。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立文檔安全客戶端API對象**

在以寫程式方式執行Document Security服務操作之前，必須建立Document Security服務客戶端對象。

**檢索受策略保護的PDF文檔**

必須檢索受策略保護的PDF文檔才能撤消它。 您無法撤消已撤消或不是受策略保護的文檔的文檔。

如果您知道受策略保護文檔的許可證標識符值，則無需檢索受策略保護的PDF文檔。 但是，在大多數情況下，您需要檢索PDF文檔以獲取許可證標識符值。

**撤消受策略保護的文檔**

要撤消受策略保護的文檔，請指定受策略保護文檔的許可證標識符。 此外，您還可以指定當用戶嘗試開啟撤消的文檔時可以查看的文檔的URL。 也就是說，假設一個過時的檔案被撤銷。 當用戶嘗試開啟已撤消的文檔時，他們將看到更新的文檔，而不是已撤消的文檔。

>[!NOTE]
>
>如果嘗試撤消已撤消的文檔，則會引發異常。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[將策略應用於PDF文檔](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[恢復對已撤消文檔的訪問](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### 使用Java API撤消對文檔的訪問 {#revoke-access-to-documents-using-the-java-api}

使用文檔安全API(Java)撤消對受策略保護的PDF文檔的訪問：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-rightsmanagement-client.jar。

1. 建立文檔安全客戶端API對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocumentSecurityClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索受策略保護的PDF文檔

   * 建立 `java.io.FileInputStream` 表示受策略保護的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 撤消受策略保護的文檔

   * 建立 `DocumentManager` 通過調用 `DocumentSecurityClient` 對象 `getDocumentManager` 的雙曲餘切值。
   * 通過調用 `DocumentManager` 對象 `getLicenseId` 的雙曲餘切值。 通過 `com.adobe.idp.Document` 表示受策略保護的文檔的對象。 此方法返回表示許可證標識符值的字串值。
   * 建立 `LicenseManager` 通過調用 `DocumentSecurityClient` 對象 `getLicenseManager` 的雙曲餘切值。
   * 通過調用 `LicenseManager` 對象 `revokeLicense` 方法並傳遞以下值：

      * 一個字串值，它指定受策略保護的文檔的許可證標識符值(指定 `DocumentManager` 對象 `getLicenseId` )。
      * 的靜態資料成員 `License` 指定撤消文檔的原因的介面。 例如，可以指定 `License.DOCUMENT_REVISED`。
      * A `java.net.URL` 指定修訂文檔所在位置的值。 如果不想將用戶重定向到另一個URL，則可以傳遞 `null`。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動（SOAP模式）:使用Java API撤消文檔&quot;

### 使用Web服務API撤消對文檔的訪問 {#revoke-access-to-documents-using-the-web-service-api}

使用文檔安全API（Web服務）撤消對受策略保護的PDF文檔的訪問：

1. 包括項目檔案

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立文檔安全客戶端API對象

   * 建立 `DocumentSecurityServiceClient` 對象。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `DocumentSecurityServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。


1. 檢索受策略保護的PDF文檔

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存被吊銷的受策略保護的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示要撤消的受策略保護的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 撤消受策略保護的文檔

   * 通過調用 `DocumentSecurityServiceClient` 對象 `getLicenseID` 方法和傳遞 `BLOB` 表示受策略保護的文檔的對象。 此方法返回表示許可證標識符的字串值。
   * 通過調用 `DocumentSecurityServiceClient` 對象 `revokeLicense` 方法並傳遞以下值：

      * 一個字串值，它指定受策略保護的文檔的許可證標識符值(指定 `DocumentSecurityServiceService` 對象 `getLicenseId` )。
      * 的靜態資料成員 `Reason` 指定撤消文檔原因的枚舉。 例如，可以指定 `Reason.DOCUMENT_REVISED`。
      * A `string` 指定修訂文檔所在的URL位置的值。 如果不想將用戶重定向到另一個URL，則可以傳遞 `null`。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動(MTOM):使用Web服務API撤消文檔&quot;
* 「快速啟動(SwaRef):使用Web服務API撤消文檔&quot;

**另請參閱**

[從Word文檔中刪除策略](protecting-documents-policies.md#removing-policies-from-word-documents)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 恢復對已撤消文檔的訪問 {#reinstating-access-to-revoked-documents}

您可以恢復對已撤消的PDF文檔的訪問權限，從而使用戶可以訪問已撤消文檔的所有副本。 當用戶開啟已撤消的恢復文檔時，用戶可以查看該文檔。

>[!NOTE]
>
>有關文檔安全服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-6}

要恢復對撤消的PDF文檔的訪問權限，請執行以下步驟：

1. 包括項目檔案。
1. 建立文檔安全客戶端API對象。
1. 檢索已撤消的PDF文檔的許可證標識符。
1. 恢復對撤消的PDF文檔的訪問權限。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立文檔安全客戶端API對象**

在以寫程式方式執行Document Security服務操作之前，必須建立Document Security服務客戶端對象。 如果使用Java API，請建立 `DocumentSecurityClient` 的雙曲餘切值。 如果使用Document Security Web服務API，請建立 `DocumentSecurityServiceService` 的雙曲餘切值。

**檢索已撤消的PDF文檔的許可證標識符**

必須檢索已撤消的PDF文檔的許可證標識符才能恢復已撤消的PDF文檔。 獲取許可證標識符值後，可恢復已撤消的文檔。 如果嘗試恢復未撤消的文檔，將導致異常。

**恢復對撤消的PDF文檔的訪問權限**

要恢復對已撤消PDF文檔的訪問，必須指定已撤消文檔的許可證標識符。 如果嘗試恢復對未撤消的PDF文檔的訪問權限，將導致異常。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[將策略應用於PDF文檔](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[撤消對文檔的訪問](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API恢復對已撤消文檔的訪問 {#reinstate-access-to-revoked-documents-using-the-java-api}

使用文檔安全API(Java)恢復對已撤消文檔的訪問：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-rightsmanagement-client.jar。

1. 建立文檔安全客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocumentSecurityClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索已撤消的PDF文檔的許可證標識符。

   * 建立 `java.io.FileInputStream` 表示已撤消PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。
   * 建立 `DocumentManager` 通過調用 `DocumentSecurityClient` 對象 `getDocumentManager` 的雙曲餘切值。
   * 通過調用 `DocumentManager` 對象 `getLicenseId` 方法和傳遞 `com.adobe.idp.Document` 表示已撤消文檔的對象。 此方法返回表示許可證標識符的字串值。

1. 恢復對撤消的PDF文檔的訪問權限。

   * 建立 `LicenseManager` 通過調用 `DocumentSecurityClient` 對象 `getLicenseManager` 的雙曲餘切值。
   * 通過調用對撤消的PDF文檔的恢復訪問 `LicenseManager` 對象 `unrevokeLicense` 方法，並傳遞已撤消文檔的許可證標識符值。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動（SOAP模式）:使用Web服務API恢復對已撤消文檔的訪問&quot;

### 使用Web服務API恢復對已吊銷文檔的訪問 {#reinstate-access-to-revoked-documents-using-the-web-service-api}

使用文檔安全API（Web服務）恢復對已撤消文檔的訪問：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立文檔安全客戶端API對象。

   * 建立 `DocumentSecurityServiceClient` 對象。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `DocumentSecurityServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。


1. 檢索已撤消的PDF文檔的許可證標識符。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存恢復訪問權限的撤消PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示已撤消的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 恢復對撤消的PDF文檔的訪問權限。

   * 通過調用 `DocumentSecurityServiceClient` 對象 `getLicenseID` 方法和傳遞 `BLOB` 表示已撤消文檔的對象。 此方法返回表示許可證標識符的字串值。
   * 通過調用對撤消的PDF文檔的恢復訪問 `DocumentSecurityServiceClient` 對象 `unrevokeLicense` 方法並傳遞一個字串值，該字串值指定已撤消的PDF文檔的許可證標識符值(傳遞已撤消的 `DocumentSecurityServiceClient` 對象 `getLicenseId` )。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動(MTOM):使用Web服務API恢復對已撤消文檔的訪問&quot;
* 「快速啟動(SwaRef):使用Web服務API恢復對已撤消文檔的訪問&quot;

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 檢查策略保護的PDF文檔 {#inspecting-policy-protected-pdf-documents}

可以使用Document Security Service API（Java和Web服務）來檢查受策略保護的PDF文檔。 檢查受策略保護的PDF文檔會返回有關受策略保護的PDF文檔的資訊。 例如，您可以確定用於保護文檔的策略以及文檔的保護日期。

如果LiveCycle版本為8.x或早期版本，則無法執行此任務。 在AEM Forms增加了對檢查政策保護檔案的支援。 如果嘗試使用LiveCycle8.x（或更早版本）檢查受策略保護的文檔，則會引發異常。

>[!NOTE]
>
>有關文檔安全服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-7}

要檢查受策略保護的PDF文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立文檔安全客戶端API對象。
1. 檢索要檢查的受策略保護的文檔。
1. 獲取有關受策略保護的文檔的資訊。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立文檔安全客戶端API對象**

在以寫程式方式執行文檔安全服務操作之前，請建立文檔安全服務客戶端對象。 如果使用Java API，請建立 `RightsManagementClient` 的雙曲餘切值。 如果使用Document Security Web服務API，請建立 `RightsManagementServiceService` 的雙曲餘切值。

**檢索受策略保護的文檔以進行檢查**

要檢查受策略保護的文檔，請檢索它。 如果嘗試檢查未使用策略進行保護或已撤消的文檔，則會引發異常。

**Inspect**

檢索受策略保護的文檔後，可以檢查它。

**獲取有關受策略保護的文檔的資訊**

在檢查受策略保護的PDF文檔後，可以獲取有關該文檔的資訊。 例如，您可以確定用於保護文檔的策略。

如果您使用屬於「我的策略」的策略保護文檔，然後調用 `RMInspectResult.getPolicysetName` 或 `RMInspectResult.getPolicysetId`，返回空值。

如果使用策略集中包含的策略（「我的策略」除外）保護文檔，則 `RMInspectResult.getPolicysetName` 和 `RMInspectResult.getPolicysetId` 返回有效字串。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Inspect策略保護的PDF文檔使用Java API {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspect使用Document Security Service API(Java)作為受策略保護的PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-rightsmanagement-client.jar。 有關這些檔案位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 建立文檔安全客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 建立 `RightsManagementClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索要檢查的受策略保護的文檔。

   * 建立 `java.io.FileInputStream` 使用其建構子表示受策略保護的PDF文檔的對象。 傳遞一個字串值，指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. Inspect。

   * 建立 `DocumentManager` 通過調用 `RightsManagementClient` 對象 `getDocumentManager` 的雙曲餘切值。
   * Inspect通過調用 `LicenseManager` 對象 `inspectDocument` 的雙曲餘切值。 通過 `com.adobe.idp.Document` 包含受策略保護的PDF文檔的對象。 此方法返回 `RMInspectResult` 包含有關受策略保護文檔的資訊的對象。

1. 獲取有關受策略保護的文檔的資訊。

   要獲取有關受策略保護文檔的資訊，請調用屬於的相應方法 `RMInspectResult` 的雙曲餘切值。 例如，要檢索策略名稱，請調用 `RMInspectResult` 對象 `getPolicyName` 的雙曲餘切值。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動（SOAP模式）:使用Java API檢查受策略保護的PDF文檔&quot;

### Inspect使用Web服務API的策略保護PDF文檔 {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspect使用文檔安全服務API（Web服務）提供受策略保護的PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立文檔安全客戶端API對象。

   * 建立 `RightsManagementServiceClient` 對象。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `RightsManagementServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。


1. 檢索要檢查的受策略保護的文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存要檢查的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及在中開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞位元組陣列、起始位置和流長度以進行讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. Inspect。

   Inspect通過調用 `RightsManagementServiceClient` 對象 `inspectDocument` 的雙曲餘切值。 通過 `BLOB` 包含受策略保護的PDF文檔的對象。 此方法返回 `RMInspectResult` 包含有關受策略保護文檔的資訊的對象。

1. 獲取有關受策略保護的文檔的資訊。

   要獲取有關受策略保護文檔的資訊，請獲取屬於 `RMInspectResult` 的雙曲餘切值。 例如，要檢索策略名稱，請獲取 `RMInspectResult` 對象 `policyName` 的子菜單。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動(MTOM):使用Web服務API檢查受策略保護的PDF文檔&quot;
* 「快速啟動(SwaRef):使用Web服務API檢查受策略保護的PDF文檔&quot;

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 建立水印 {#creating-watermarks}

水印通過唯一地識別文檔並控製版權侵權來幫助確保文檔的安全性。 例如，您可以建立並放置一個在文檔的所有頁面上聲明「機密」的水印。 在建立水印後，可以將其作為策略的一部分包含。 即，可以使用新建立的水印設定策略的水印屬性。 將包含水印的策略應用到文檔後，該水印將出現在受策略保護的文檔中。

>[!NOTE]
>
>只有具有文檔安全管理權限的用戶才能建立水印。 即，在定義建立Document Security服務客戶端對象所需的連接設定時，必須指定此類用戶。

>[!NOTE]
>
>有關文檔安全服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-8}

要建立水印，請執行以下步驟：

1. 包括項目檔案。
1. 建立文檔安全客戶端API對象。
1. 設定水印屬性。
1. 向文檔安全服務註冊水印。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立文檔安全客戶端API對象**

在以寫程式方式執行Document Security服務操作之前，必須建立Document Security服務客戶端對象。 如果使用Java API，請建立 `RightsManagementClient` 的雙曲餘切值。 如果使用Document Security Web服務API，請建立 `RightsManagementServiceService` 的雙曲餘切值。

**設定水印屬性**

要建立新水印，必須設定水印屬性。 必須始終定義名稱屬性。 除了name屬性外，還必須至少設定以下屬性之一：

* 自訂文字
* 包括日期
* 包含用戶ID
* 包括的用戶名

下表列出了使用Web服務建立水印時所需的鍵和值對。

<table>
 <thead>
  <tr>
   <th><p>金鑰名稱</p></th>
   <th><p>說明</p></th>
   <th><p>值</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERNAME_ENABLED</code></p></td>
   <td><p>指定開啟文檔的用戶的用戶名是否是水印的一部分。</p></td>
   <td><p>真或假</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>指定開啟文檔的用戶標識是否是水印的一部分。</p></td>
   <td><p>真或假</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>指定當前日期是否是水印的一部分。</p></td>
   <td><p>真或假</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>如果此值為true，則必須使用 <code>WaterBackCmd:SRCTEXT</code>。</p></td>
   <td><p>真或假</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>指定水印的不透明度。 如果未指定預設值為0.5。</p></td>
   <td><p>介於0.0和1.0之間的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>指定水印的旋轉。 預設值為0度。</p></td>
   <td><p>介於0和359之間的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>如果指定了此值，則 <code>WaterBackCmd:IS_SIZE_ENABLED</code> 必須存在且值必須為true。 如果未指定此屬性，則預設行為適合頁面。</p></td>
   <td><p>大於0.0且小於或等於1.0的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>指定水印的水準對齊方式。 預設值為中心。</p></td>
   <td><p>左、中或右</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>指定水印的垂直對齊方式。 預設值為中心。</p></td>
   <td><p>上、中或下</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>指定水印是否為背景。 預設值為false。</p></td>
   <td><p>真或假</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>如果指定了自定義比例，則為True。 如果此值為true，則還必須指定SCALE。 如果此值為false，則預設值適合頁面。</p></td>
   <td><p>真或假</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>指定水印的自定義文本。 如果此值存在，則 <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> 也必須存在並設定為true。</p></td>
   <td><p>真或假</p></td>
  </tr>
 </tbody>
</table>

所有水印必須定義以下屬性之一：

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

所有其它屬性都是可選的。

**註冊水印**

必須在文檔安全服務中註冊新水印，然後才能使用它。 註冊水印後，可以在策略中使用它。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[將策略應用於PDF文檔](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API建立水印 {#create-watermarks-using-the-java-api}

使用Document Security API(Java)建立水印：

1. 包括項目檔案。

   包括客戶端JAR檔案，如 `adobe-rightsmanagement-client.jar`，位於Java項目的類路徑中。

1. 建立文檔安全客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `RightsManagementClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 設定水印屬性

   * 建立 `Watermark` 通過調用 `InfomodelObjectFactory` 對象的靜態 `createWatermark` 的雙曲餘切值。 此方法返回 `Watermark` 的雙曲餘切值。
   * 通過調用 `Watermark` 對象 `setName` 方法並傳遞指定策略名稱的字串值。
   * 通過調用 `Watermark` 對象 `setBackground` 方法 `true`。 通過設定此屬性，水印將出現在文檔的背景中。
   * 通過調用 `Watermark` 對象 `setCustomText` 方法，並傳遞一個表示水印文本的字串值。
   * 通過調用 `Watermark` 對象 `setOpacity` 方法並傳遞指定不透明度級別的整數值。 值100表示水印完全不透明，值0表示水印完全透明。

1. 註冊水印。

   * 建立 `WatermarkManager` 通過調用 `RightsManagementClient` 對象 `getWatermarkManager` 的雙曲餘切值。 此方法返回 `WatermarkManager` 的雙曲餘切值。
   * 通過調用 `WatermarkManager` 對象 `registerWatermark` 方法和傳遞 `Watermark` 表示要註冊的水印的對象。 此方法返回一個表示水印標識值的字串值。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動（SOAP模式）:使用Java API建立水印&quot;

### 使用Web服務API建立水印 {#create-watermarks-using-the-web-service-api}

使用Document Security API（Web服務）建立水印：

1. 建立文檔安全客戶端API對象。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立文檔安全客戶端API對象。

   * 建立 `RightsManagementServiceClient` 對象。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `RightsManagementServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。


1. 設定水印屬性。

   * 建立 `WatermarkSpec` 通過調用 `WatermarkSpec` 建構子。
   * 通過將字串值分配給 `WatermarkSpec` 對象 `name` 資料成員。
   * 設定水印 `id` 屬性，方法是將字串值賦給 `WatermarkSpec` 對象 `id` 資料成員。
   * 對於要設定的每個水印屬性，建立一個單獨的 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的雙曲餘切值。
   * 通過為 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `key` 資料成員(例如， `WaterBackCmd:OPACITY)`。
   * 通過為 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `value` 資料成員(例如， `.25`)。
   * 建立 `MyArrayOf_xsd_anyType` 的雙曲餘切值。 每個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象，調用 `MyArrayOf_xsd_anyType` 對象 `Add` 的雙曲餘切值。 通過 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的雙曲餘切值。
   * 分配 `MyArrayOf_xsd_anyType` 對象 `WatermarkSpec` 對象 `values` 資料成員。

1. 註冊水印。

   通過調用 `RightsManagementServiceClient` 對象 `registerWatermark` 方法和傳遞 `WatermarkSpec` 表示要註冊的水印的對象。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動(MTOM):使用Web服務API建立水印&quot;
* 「快速啟動(SwaRef):使用Web服務API建立水印&quot;

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改水印 {#modifying-watermarks}

可以使用Document Security Java API或Web服務API修改現有水印。 要更改現有水印，請檢索它、修改其屬性，然後在伺服器上更新它。 例如，假定您檢索水印並修改其不透明度屬性。 在更改生效之前，必須更新水印。

修改水印時，更改會影響應用了水印的未來文檔。 即，包含水印的現有PDF文檔不受影響。

>[!NOTE]
>
>只有具有文檔安全管理權限的用戶才能修改水印。 即，在定義建立Document Security服務客戶端對象所需的連接設定時，必須指定此類用戶。

>[!NOTE]
>
>有關文檔安全服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-9}

要修改水印，請執行以下步驟：

1. 包括項目檔案。
1. 建立文檔安全客戶端API對象。
1. 檢索要修改的水印。
1. 設定水印屬性。
1. 更新水印。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立文檔安全客戶端API對象**

在以寫程式方式執行Document Security服務操作之前，必須建立Document Security服務客戶端對象。 如果使用Java API，請建立 `DocumentSecurityClient` 的雙曲餘切值。 如果使用Document Security Web服務API，請建立 `DocumentSecurityServiceService` 的雙曲餘切值。

**檢索要修改的水印**

要修改水印，必須檢索現有水印。 可以通過指定水印名稱或指定水印的標識符值來檢索水印。

**設定水印屬性**

要修改現有水印，請更改一個或多個水印屬性的值。 當使用Web服務以寫程式方式更新水印時，必須設定最初設定的所有屬性，即使該值沒有更改。 例如，假定設定了以下水印屬性： `WaterBackCmd:IS_USERID_ENABLED`。 `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`。 `WaterBackCmd:OPACITY`, `WaterBackCmd:SRCTEXT`。 雖然您唯一要修改的屬性是 `WaterBackCmd:OPACITY`，則必須將其他值設定為良好。

>[!NOTE]
>
>使用Java API修改水印時，不需要指定所有屬性。 設定要修改的水印屬性。

>[!NOTE]
>
>有關水印屬性名稱的資訊，請參見 [建立水印](protecting-documents-policies.md#creating-watermarks)。

**更新水印**

修改水印屬性後，必須更新水印。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[建立水印](protecting-documents-policies.md#creating-watermarks)

### 使用Java API修改水印 {#modify-watermarks-using-the-java-api}

使用Document Security API(Java)修改水印：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-rightsmanagement-client.jar。

1. 建立文檔安全客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocumentSecurityClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索要修改的水印。

   建立 `WatermarkManager` 通過調用 `DocumentSecurityClient` 對象 `getWatermarkManager` 方法並傳遞一個指定水印名稱的字串值。 此方法返回 `Watermark` 表示要修改的水印的對象。

1. 設定水印屬性。

   通過調用 `Watermark` 對象 `setOpacity` 方法並傳遞指定不透明度級別的整數值。 值100表示水印完全不透明，值0表示水印完全透明。

   >[!NOTE]
   >
   >此示例僅修改不透明度屬性。

1. 更新水印。

   * 通過調用 `WatermarkManager` 對象 `updateWatermark` 方法和通過 `Watermark` 屬性被修改的對象。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱快速啟動（SOAP模式）:使用Java API部分修改水印。

### 使用Web服務API修改水印 {#modify-watermarks-using-the-web-service-api}

使用Document Security API（Web服務）修改水印：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立文檔安全客戶端API對象。

   * 建立 `DocumentSecurityServiceClient` 對象。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `DocumentSecurityServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。


1. 檢索要修改的水印。

   通過調用 `DocumentSecurityServiceClient` 對象 `getWatermarkByName` 的雙曲餘切值。 傳遞指定水印名稱的字串值。 此方法返回 `WatermarkSpec` 表示要修改的水印的對象。

1. 設定水印屬性。

   * 對於要更新的每個水印屬性，建立一個單獨的 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的雙曲餘切值。
   * 通過為 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `key` 資料成員(例如， `WaterBackCmd:OPACITY)`。
   * 通過為 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `value` 資料成員(例如， `.50`)。
   * 建立 `MyArrayOf_xsd_anyType` 的雙曲餘切值。 每個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象，調用 `MyArrayOf_xsd_anyType` 對象 `Add` 的雙曲餘切值。 通過 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的雙曲餘切值。
   * 分配 `MyArrayOf_xsd_anyType` 對象 `WatermarkSpec` 對象 `values` 資料成員。

1. 更新水印。

   通過調用 `DocumentSecurityServiceClient` 對象 `updateWatermark` 方法和傳遞 `WatermarkSpec` 表示要修改的水印的對象。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動(MTOM):使用Web服務API修改水印&quot;

## 搜索事件 {#searching-for-events}

Rights Management服務在特定操作發生時跟蹤這些操作，如將策略應用於文檔、開啟受策略保護的文檔以及撤消對文檔的訪問。 必須為Rights Management服務啟用事件審計，否則不跟蹤事件。

事件分為以下類別之一：

* 管理員事件是與管理員相關的操作，如建立新管理員帳戶。
* 文檔事件是與文檔相關的操作，如關閉受策略保護的文檔。
* 策略事件是與策略相關的操作，如建立新策略。
* 服務事件是與Rights Management服務相關的操作，如與用戶目錄同步。

可以使用Rights ManagementJava API或Web服務API來搜索指定的事件。 通過搜索事件，可以執行任務，例如建立特定事件的日誌檔案。

>[!NOTE]
>
>有關Rights Management服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-10}

要搜索Rights Management事件，請執行以下步驟：

1. 包括項目檔案。
1. 建立Rights Management客戶端API對象。
1. 指定要搜索的事件。
1. 搜索事件。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立Rights Management客戶端API對象**

在以寫程式方式執行Rights Management服務操作之前，必須建立Rights Management服務客戶端對象。 如果使用Java API，請建立 `DocumentSecurityClient` 的雙曲餘切值。 如果使用Rights ManagementWeb服務API，請建立 `DocumentSecurityServiceService` 的雙曲餘切值。

**指定要搜索的事件**

必須指定要搜索的事件。 例如，可以搜索策略建立事件，該事件在建立新策略時發生。

**搜索事件**

指定要搜索的事件後，可以使用Rights ManagementJava API或Rights ManagementWeb服務API來搜索事件。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API搜索事件 {#search-for-events-using-the-java-api}

使用Rights ManagementAPI(Java)搜索事件：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-rightsmanagement-client.jar。

1. 建立Rights Management客戶端API對象

   建立 `DocumentSecurityClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定要搜索的事件

   * 建立 `EventManager` 通過調用 `DocumentSecurityClient` 對象 `getEventManager` 的雙曲餘切值。 此方法返回 `EventManager` 的雙曲餘切值。
   * 建立 `EventSearchFilter` 調用其建構子。
   * 通過調用 `EventSearchFilter` 對象 `setEventCode` 傳遞屬於靜態資料成員的方法 `EventManager` 表示要搜索的事件的類。 例如，要搜索策略建立事件，請傳遞 `EventManager.POLICY_CREATE_EVENT`。

   >[!NOTE]
   >
   >您可以通過調用 `EventSearchFilter` 對象方法。 例如，調用 `setUserName` 方法，指定與事件關聯的用戶。

1. 搜索事件

   通過調用 `EventManager` 對象 `searchForEvents` 方法和傳遞 `EventSearchFilter` 定義事件搜索條件的對象。 此方法返回 `Event` 對象。

**代碼示例**

有關使用Rights Management服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動(SOAP):使用Java API搜索事件&quot;

### 使用Web服務API搜索事件 {#search-for-events-using-the-web-service-api}

使用Rights ManagementAPI（Web服務）搜索事件：

1. 包括項目檔案

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立Rights Management客戶端API對象

   * 建立 `DocumentSecurityServiceClient` 對象。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `DocumentSecurityServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。


1. 指定要搜索的事件

   * 建立 `EventSpec` 對象。
   * 通過設定 `EventSpec` 對象 `firstTime.date` 資料成員 `DataTime` 表示事件發生時日期範圍開始的實例。
   * 分配值 `true` 到 `EventSpec` 對象 `firstTime.dateSpecified` 資料成員。
   * 通過設定 `EventSpec` 對象 `lastTime.date` 資料成員 `DataTime` 表示事件發生時日期範圍結束的實例。
   * 分配值 `true` 到 `EventSpec` 對象 `lastTime.dateSpecified` 資料成員。
   * 通過將字串值分配給 `EventSpec` 對象 `eventCode` 資料成員。 下表列出了可分配給此屬性的數值：

   <table>
    <thead>
    <tr>
    <th><p>事件類型</p></th>
    <th><p>值</p></th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><p><code>ALL_EVENTS</code></p></td>
    <td><p>999</p></td>
    </tr>
    <tr>
    <td><p><code>USER_CHANGE_PASSWORD_EVENT</code></p></td>
    <td><p>1000</p></td>
    </tr>
    <tr>
    <td><p><code>USER_REGISTER_EVENT</code></p></td>
    <td><p>1001</p></td>
    </tr>
    <tr>
    <td><p><code>USER_PREREGISTER_EVENT</code></p></td>
    <td><p>1002</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACTIVATE_EVENT</code></p></td>
    <td><p>1003</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DEACTIVATE_EVENT</code></p></td>
    <td><p>1004</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_EVENT</code></p></td>
    <td><p>1005</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_DENY_EVENT </code></p></td>
    <td><p>1006</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACCOUNT_LOCK_EVENT</code></p></td>
    <td><p>1007</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DELETE_EVENT </code></p></td>
    <td><p>1008</p></td>
    </tr>
    <tr>
    <td><p><code>USER_UPDATE_PROFILE_EVENT </code></p></td>
    <td><p>1009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_VIEW_EVENT </code></p></td>
    <td><p>2000</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_LOW_EVENT </code></p></td>
    <td><p>2001</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_HIGH_EVENT </code></p></td>
    <td><p>2002</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SIGN_EVENT </code></p></td>
    <td><p>2003</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_ADD_ANNOTATION_EVENT </code></p></td>
    <td><p>2004</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_FORM_FILL_EVENT </code></p></td>
    <td><p>2005</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CLOSE_EVENT </code></p></td>
    <td><p>2006</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_MODIFY_EVENT </code></p></td>
    <td><p>2007</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_SECURITY_HANDLER_EVENT </code></p></td>
    <td><p>2008</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SWITCH_POLICY_EVENT </code></p></td>
    <td><p>2009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_REVOKE_EVENT </code></p></td>
    <td><p>2010</p></td>
    </tr>
    <tr>
    <td><p><code>$1</code></p></td>
    <td><p>2011</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SECURE_EVENT </code></p></td>
    <td><p>2012</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_UNKNOWN_CLIENT_EVENT </code></p></td>
    <td><p>2013</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_REVOKE_URL_EVENT </code></p></td>
    <td><p>2014</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_EVENT </code></p></td>
    <td><p>3000</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_ENABLE_EVENT </code></p></td>
    <td><p>3001</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DISABLE_EVENT </code></p></td>
    <td><p>3002</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CREATE_EVENT </code></p></td>
    <td><p>3003</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DELETE_EVENT </code></p></td>
    <td><p>3004</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_OWNER_EVENT </code></p></td>
    <td><p>3005</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CLIENT_SYNC_EVENT </code></p></td>
    <td><p>4000</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_INFO_EVENT </code></p></td>
    <td><p>4001</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_COMPLETE_EVENT </code></p></td>
    <td><p>4002</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_VERSION_MISMATCH_EVENT </code></p></td>
    <td><p>4003</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CONFIG_CHANGE_EVENT </code></p></td>
    <td><p>4004</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_ENABLE_OFFLINE_ACCESS_EVENT </code></p></td>
    <td><p>4005</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ADD_EVENT </code></p></td>
    <td><p>5000</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DELETE_EVENT </code></p></td>
    <td><p>5001</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_EDIT_EVENT </code></p></td>
    <td><p>5002</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ACTIVATE_EVENT </code></p></td>
    <td><p>5003</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DEACTIVATE_EVENT </code></p></td>
    <td><p>5004</p></td>
    </tr>
    <tr>
    <td><p><code>ERROR_DIRECTORY_SERVICE_EVENT </code></p></td>
    <td><p>6000</p></td>
    </tr>
    <tr>
    <td><p><code>CREATED_POLICYSET_EVENT</code></p></td>
    <td><p>7000</p></td>
    </tr>
    <tr>
    <td><p><code>DELETED_POLICYSET_EVENT</code></p></td>
    <td><p>7001</p></td>
    </tr>
    <tr>
    <td><p><code>MODIFIED_POLICYSET_EVENT</code></p></td>
    <td><p>7002</p></td>
    </tr>
    </tbody>
    </table>

1. 搜索事件

   通過調用 `DocumentSecurityServiceClient` 對象 `searchForEvents` 方法和傳遞 `EventSpec` 表示要搜索的事件和最大結果數的對象。 此方法返回 `MyArrayOf_xsd_anyType` 集合，其中每個元素都是 `AuditSpec` 實例。 使用 `AuditSpec` 實例中，您可以獲取有關事件的資訊，如事件發生的時間。 的 `AuditSpec` 實例包含 `timestamp` 指定此資訊的資料成員。

**代碼示例**

有關使用Rights Management服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動(MTOM):使用Web服務API搜索事件&quot;
* 「快速啟動(SwaRef):使用Web服務API搜索事件&quot;

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將策略應用於Word文檔 {#applying-policies-to-word-documents}

除PDF文檔外，權限管理服務還支援其他文檔格式，如MicrosoftWord文檔（DOC檔案）和其他Micosoft辦公室檔案格式。 例如，您可以將策略應用於Word文檔以保護它。 通過將策略應用於Word文檔，可以限制對文檔的訪問。 如果文檔已使用策略進行保護，則不能將策略應用於文檔。

在分發受策略保護的Word文檔後，可以監視其使用情況。 即，您可以看到文檔的使用方式和使用者。 例如，您可以查找某人何時開啟了文檔。

>[!NOTE]
>
>有關文檔安全服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-11}

要將策略應用於Word文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立文檔安全客戶端API對象。
1. 檢索應用策略的Word文檔。
1. 將現有策略應用於Word文檔。
1. 保存受策略保護的Word文檔。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立文檔安全客戶端API對象**

在以寫程式方式執行Document Security服務操作之前，必須建立Document Security服務客戶端對象。

**檢索Word文檔**

必須檢索Word文檔才能應用策略。 將策略應用於Word文檔後，用戶在使用文檔時受到限制。 例如，如果策略未啟用離線時開啟文檔，則用戶必須聯機才能開啟文檔。

**將現有策略應用於Word文檔**

要將策略應用於Word文檔，必須引用現有策略並指定策略所屬的策略集。 設定連接屬性的用戶必須有權訪問指定的策略。 否則，將發生異常。

**保存Word文檔**

文檔安全服務將策略應用於Word文檔後，可以將受策略保護的Word文檔另存為DOC檔案。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[撤消對文檔的訪問](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API將策略應用於Word文檔 {#apply-a-policy-to-a-word-document-using-the-java-api}

使用Document Security API(Java)將策略應用於Word文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-rightsmanagement-client.jar。

1. 建立文檔安全客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocumentSecurityClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索Word文檔。

   * 建立 `java.io.FileInputStream` 表示Word文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定Word文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 將現有策略應用於Word文檔。

   * 建立 `DocumentManager` 通過調用 `DocumentSecurityClient` 對象 `getDocumentManager` 的雙曲餘切值。
   * 通過調用 `DocumentManager` 對象 `protectDocument` 方法並傳遞以下值：

      * 的 `com.adobe.idp.Document` 包含應用策略的Word文檔的對象。
      * 指定文檔名稱的字串值。
      * 一個字串值，它指定策略所屬的策略集的名稱。 可以指定 `null` 導致 `MyPolicies` 正在使用的策略集。
      * 指定策略名稱的字串值。
      * 一個字串值，它表示作為文檔發佈者的用戶的用戶管理器域的名稱。 此參數值是可選的，可以為Null（如果此參數為Null，則下一個參數值必須為Null）。
      * 一個字串值，它表示作為文檔發佈者的用戶管理器用戶的規範名稱的名稱。 此參數值是可選的，可以 `null` (如果此參數 `null`，則上一個參數值必須是 `null`)。
      * A `com.adobe.livecycle.rightsmanagement.Locale` 表示用於選擇MS Office模板的區域設定。 此參數值是可選的，您可以指定 `null`。

      的 `protectDocument` 方法返回 `RMSecureDocumentResult` 包含受策略保護的Word文檔的對象。


1. 保存Word文檔。

   * 調用 `RMSecureDocumentResult` 對象 `getProtectedDoc` 獲取受策略保護的Word文檔的方法。 此方法返回 `com.adobe.idp.Document` 的雙曲餘切值。
   * 建立 `java.io.File` 並確保檔案副檔名為DOC。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `Document` 對象到檔案(確保 `Document` 返回的對象 `getProtectedDoc` )。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動（SOAP模式）:使用Java API將策略應用到Word文檔&quot;

### 使用Web服務API將策略應用於Word文檔 {#apply-a-policy-to-a-word-document-using-the-web-service-api}

使用文檔安全API（Web服務）將策略應用於Word文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立文檔安全客戶端API對象。

   * 建立 `DocumentSecurityServiceClient` 對象。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `DocumentSecurityServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。


1. 檢索Word文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存應用策略的Word文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示Word文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 將現有策略應用於Word文檔。

   通過調用 `DocumentSecurityServiceClient` 對象 `protectDocument` 方法並傳遞以下值：

   * 的 `BLOB` 包含應用策略的Word文檔的對象。
   * 指定文檔名稱的字串值。
   * 一個字串值，它指定策略所屬的策略集的名稱。 可以指定 `null` 導致 `MyPolicies` 正在使用的策略集。
   * 指定策略名稱的字串值。
   * 一個字串值，它表示作為文檔發佈者的用戶的用戶管理器域的名稱。 此參數值是可選的，可以為Null(如果此參數為Null，則下一個參數值必須為 `null`)。
   * 一個字串值，它表示作為文檔發佈者的用戶管理器用戶的規範名稱的名稱。 此參數值是可選的，可以為Null(如果此參數為Null，則上一個參數值必須為 `null`)。
   * A `RMLocale` 指定區域設定值的值(例如， `RMLocale.en`)。
   * 用於儲存策略標識符值的字串輸出參數。
   * 用於儲存受策略保護的標識符值的字串輸出參數。
   * 用於儲存mime類型的字串輸出參數(例如， `application/doc`)。

   的 `protectDocument` 方法返回 `BLOB` 包含受策略保護的Word文檔的對象。

1. 保存Word文檔。

   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值來表示受策略保護的Word文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `protectDocument` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動(MTOM):使用Web服務API將策略應用到Word文檔

## 從Word文檔中刪除策略 {#removing-policies-from-word-documents}

可以從受策略保護的Word文檔中刪除策略，以便從文檔中刪除安全性。 即，如果不再希望文檔受策略保護。 如果要使用較新的策略更新受策略保護的Word文檔，則切換策略將更高效，而不是刪除策略並添加更新的策略。

>[!NOTE]
>
>有關文檔安全服務的詳細資訊，請參閱 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-12}

要從受策略保護的Word文檔中刪除策略，請執行以下步驟：

1. 包括項目檔案
1. 建立文檔安全客戶端API對象。
1. 檢索受策略保護的Word文檔。
1. 從Word文檔中刪除策略。
1. 保存不安全的Word文檔

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立文檔安全客戶端API對象**

在以寫程式方式執行文檔安全服務操作之前，請建立文檔安全服務客戶端對象。

**檢索受策略保護的Word文檔**

必須檢索受策略保護的Word文檔才能刪除策略。 如果嘗試從未受策略保護的Word文檔中刪除策略，將導致異常。

**從Word文檔中刪除策略**

如果在連接設定中指定了管理員，則可以從受策略保護的Word文檔中刪除策略。 否則，用於保護文檔的策略必須包含 `SWITCH_POLICY` 從Word文檔中刪除策略的權限。 此外，在AEM Forms連接設定中指定的用戶還必須具有該權限。 否則，將引發異常。

**保存不安全的Word文檔**

在文檔安全服務從Word文檔中刪除策略後，可以將不安全的Word文檔另存為DOC檔案。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[將策略應用於Word文檔](protecting-documents-policies.md#applying-policies-to-word-documents)

### 使用Java API從Word文檔中刪除策略 {#remove-a-policy-from-a-word-document-using-the-java-api}

使用Document Security API(Java)從受策略保護的Word文檔中刪除策略：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-rightsmanagement-client.jar。

1. 建立文檔安全客戶端API對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `RightsManagementClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索受策略保護的Word文檔

   * 建立 `java.io.FileInputStream` 表示受策略保護的Word文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定Word文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 從Word文檔中刪除策略

   * 建立 `DocumentManager` 通過調用 `RightsManagementClient` 對象 `getDocumentManager` 的雙曲餘切值。
   * 通過調用 `DocumentManager` 對象 `removeSecurity` 方法和傳遞 `com.adobe.idp.Document` 包含受策略保護的Word文檔的對象。 此方法返回 `com.adobe.idp.Document` 包含不安全的Word文檔的對象。

1. 保存不安全的Word文檔

   * 建立 `java.io.File` 並確保檔案副檔名為DOC。
   * 調用 `Document` 對象 `copyToFile` 複製內容的方法 `Document` 對象到檔案(確保 `Document` 返回的對象 `removeSecurity` )。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動（SOAP模式）:使用Java API從Word文檔中刪除策略&quot;

### 使用Web服務API從Word文檔中刪除策略 {#remove-a-policy-from-a-word-document-using-the-web-service-api}

使用文檔安全API（Web服務）從受策略保護的Word文檔中刪除策略：

1. 包括項目檔案

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立文檔安全客戶端API對象

   * 建立 `RightsManagementServiceClient` 對象。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`。) 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `RightsManagementServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。


1. 檢索受策略保護的Word文檔

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存從中刪除策略的受策略保護的Word文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示Word文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 從Word文檔中刪除策略

   通過調用 `RightsManagementServiceClient` 對象 `removePolicySecurity` 方法和傳遞 `BLOB` 包含受策略保護的Word文檔的對象。 此方法返回 `BLOB` 包含不安全的Word文檔的對象。

1. 保存不安全的Word文檔

   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值來表示不安全Word文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `removePolicySecurity` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 的子菜單。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。

**代碼示例**

有關使用文檔安全服務的代碼示例，請參閱以下快速啟動：

* 「快速啟動(MTOM):使用Web服務API從Word文檔中刪除策略&quot;

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
