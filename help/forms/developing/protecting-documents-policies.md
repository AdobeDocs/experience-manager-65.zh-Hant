---
title: 使用策略保護文檔
seo-title: Protecting Documents with Policies
description: 使用檔案安全性服務，以動態方式將機密設定套用至Adobe PDF檔案，並維持對檔案的控制。 文檔安全服務還使用戶能夠控制收件人使用受策略保護的PDF文檔的方式。
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

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於檔案安全性服務**

檔案安全性服務可讓使用者動態地將機密設定套用至Adobe PDF檔案，並維持對檔案的控制，無論檔案的分送範圍有多廣。

文檔安全服務使用戶能夠控制收件人使用受策略保護的PDF文檔的方式，從而防止資訊擴散到用戶的範圍之外。 用戶可以指定誰可以開啟文檔、限制他們如何使用文檔，以及在分發文檔後監視文檔。 用戶還可以動態地控制對受策略保護文檔的訪問，甚至可以動態地撤銷對文檔的訪問。

Document Security服務也可保護其他檔案類型，例如Microsoft Word檔案（DOC檔案）。 您可以使用Document Security Client API來處理這些檔案類型。 支援下列版本：

* Microsoft Office 2003檔案（DOC、XLS、PPT檔案）
* Microsoft Office 2007檔案（DOCX、XLSX、PPTX檔案）
* PTC Pro/E檔案

為了更明確，以下兩節將討論如何使用Word文檔：

* [對Word文檔應用策略](protecting-documents-policies.md#applying-policies-to-word-documents)
* [從Word文檔中刪除策略](protecting-documents-policies.md#removing-policies-from-word-documents)

您可以使用Document Security服務完成以下任務：

* 建立原則。 如需詳細資訊，請參閱 [建立原則](protecting-documents-policies.md#creating-policies).
* 修改原則。 如需詳細資訊，請參閱 [修改策略](protecting-documents-policies.md#modifying-policies).
* 刪除原則。 如需詳細資訊，請參閱 [刪除策略](protecting-documents-policies.md#deleting-policies).
* 將策略應用於PDF文檔。 如需詳細資訊，請參閱 [將策略應用於PDF文檔](protecting-documents-policies.md#applying-policies-to-pdf-documents).
* 從PDF文檔中刪除策略。 如需詳細資訊，請參閱 [從PDF文檔中刪除策略](protecting-documents-policies.md#removing-policies-from-pdf-documents).
* Inspect受政策保護的檔案。 如需詳細資訊，請參閱 [檢查受策略保護的PDF文檔](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).
* 撤銷對PDF文檔的訪問。 如需詳細資訊，請參閱 [撤消對文檔的訪問](protecting-documents-policies.md#revoking-access-to-documents).
* 恢復對已撤銷文檔的訪問。 如需詳細資訊，請參閱 [恢復對已撤銷文檔的訪問](protecting-documents-policies.md#reinstating-access-to-revoked-documents).
* 建立水印。 如需詳細資訊，請參閱 [建立水印](protecting-documents-policies.md#creating-watermarks).
* 搜尋事件。 如需詳細資訊，請參閱 [搜尋事件](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 建立原則 {#creating-policies}

您可以使用Document Security Java API或網站服務API，以程式設計方式建立原則。 A *原則* 是資訊的集合，包括文檔安全設定、授權用戶和使用權限。 您可以使用適合不同情況和用戶的安全設定來建立和保存任意數量的策略。

策略使您可以執行以下任務：

* 指定可以開啟文檔的個人。 收件者可隸屬於您的組織，或是屬於您的組織外部。
* 指定收件者如何使用檔案。 您可以限制存取不同的Acrobat和Adobe Reader功能。 這些功能包括打印和複製文本、添加簽名以及向文檔添加註釋的功能。
* 即使在分發受策略保護的文檔之後，也可以隨時更改訪問和安全設定。
* 在分發文檔後，監視文檔的使用情況。 您可以查看檔案的使用方式，以及使用者。 例如，您可以找出有人何時開啟檔案。

### 使用Web服務建立策略 {#creating-a-policy-using-web-services}

使用Web服務API建立策略時，請參考描述該策略的現有可移植文檔權限語言(PDRL)XML檔案。 策略權限和主體在PDRL文檔中定義。 以下XML文檔是PDRL文檔的示例。

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
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

要建立策略，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security用戶端API物件。
1. 設定策略的屬性。
1. 建立策略項。
1. 註冊策略。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-rightsmanagement-client.jar
* namespace.jar(如果AEM Forms部署在JBoss上)
* jaxb-api.jar(如果AEM Forms部署在JBoss上)
* jaxb-impl.jar(如果AEM Forms部署在JBoss上)
* jaxb-libs.jar(如果AEM Forms部署在JBoss上)
* jaxb-xjc.jar(如果AEM Forms部署在JBoss上)
* relaxingDatatype.jar(如果AEM Forms部署在JBoss上)
* xsdlib.jar(如果AEM Forms部署在JBoss上)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar(若AEM Forms未部署在JBoss上，則使用其他JAR檔案)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立Document Security用戶端API物件**

在以寫程式方式執行Document Security服務操作之前，請建立Document Security服務客戶端對象。

**設定策略的屬性**

要建立策略，請設定策略屬性。 策略名稱是強制屬性。 每個策略集的策略名稱必須是唯一的。 策略集只是策略的集合。 如果策略屬於不同的策略集，則可以有兩個具有相同名稱的策略。 但是，單個策略集中的兩個策略不能具有相同的策略名稱。

要設定的另一個有用屬性是有效期。 有效期是指受策略保護的文檔可被授權的收件人訪問的時間段。 如果未設定此屬性，則策略始終有效。

有效期可設為下列其中一個選項：

* 從發佈文檔開始，文檔可以訪問的設定天數
* 在其後無法訪問文檔的結束日期
* 可訪問文檔的特定日期範圍
* 始終有效

您可以只指定開始日期，這會導致策略在開始日期之後有效。 如果只指定結束日期，則策略的有效期到結束日期為止。 但是，如果未定義開始日期和結束日期，則會擲回例外。

設定屬於策略的屬性時，還可以設定加密設定。 將策略應用於文檔時，這些加密設定將生效。 您可以指定下列加密值：

* **AES256**:使用256位密鑰表示AES加密算法。
* **AES128**:使用128位密鑰表示AES加密算法。
* **無加密：** 不表示加密。

指定 `NoEncryption` 選項，則無法設定 `PlaintextMetadata` 選項 `false`. 如果嘗試執行此操作，則會擲回例外。

>[!NOTE]
>
>如需可設定的其他屬性的相關資訊，請參閱 `Policy` 介面說明，位於 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**建立策略項**

策略項會將主體（即組和用戶）和權限附加到策略。 策略必須至少包含一個策略條目。 例如，假設您執行下列工作：

* 建立並註冊策略條目，該策略條目允許組只線上查看文檔，並禁止收件人複製文檔。
* 將策略項附加到策略。
* 使用Acrobat，使用原則保護檔案。

這些操作導致收件者只能聯機查看文檔，無法複製文檔。 在從文檔中刪除安全性之前，該文檔將保持安全。

**註冊策略**

必須先註冊新策略，才能使用它。 註冊策略後，您可以使用它來保護文檔。

### 使用Java API建立策略 {#create-a-policy-using-the-java-api}

使用Document Security API(Java)建立策略：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security用戶端API物件。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocumentSecurityClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 設定策略的屬性。

   * 建立 `Policy` 對象，方法是調用 `InfomodelObjectFactory` 對象的靜態 `createPolicy` 方法。 此方法會傳回 `Policy` 物件。
   * 調用 `Policy` 物件 `setName` 方法，並傳遞指定策略名稱的字串值。
   * 調用 `Policy` 物件 `setDescription` 方法，並傳遞指定策略說明的字串值。
   * 通過調用 `Policy` 物件 `setPolicySetName` 方法，並傳遞指定策略集名稱的字串值。 (您可以指定 `null` ，而此參數值會導致將原則新增至 *我的政策* 策略集。)
   * 調用 `InfomodelObjectFactory` 對象的靜態 `createValidityPeriod` 方法。 此方法會傳回 `ValidityPeriod` 物件。
   * 通過調用 `ValidityPeriod` 物件 `setRelativeExpirationDays` 方法，並傳遞指定天數的整數值。
   * 調用 `Policy` 物件 `setValidityPeriod` 方法和傳遞 `ValidityPeriod` 物件。

1. 建立策略項。

   * 通過調用 `InfomodelObjectFactory` 對象的靜態 `createPolicyEntry` 方法。 此方法會傳回 `PolicyEntry` 物件。
   * 叫用 `InfomodelObjectFactory` 對象的靜態 `createPermission` 方法。 傳遞屬於的靜態資料成員 `Permission` 代表權限的介面。 此方法會傳回 `Permission` 物件。 例如，要添加允許用戶從受策略保護的PDF文檔中複製資料的權限，請傳遞 `Permission.COPY`. （對要新增的每個權限重複此步驟）。
   * 調用 `PolicyEntry` 物件 `addPermission` 方法和傳遞 `Permission` 物件。 (對每個 `Permission` 物件)。
   * 通過調用 `InfomodelObjectFactory` 對象的靜態 `createSpecialPrincipal` 方法。 傳遞屬於 `InfomodelObjectFactory` 表示主體的對象。 此方法會傳回 `Principal` 物件。 例如，要將文檔的發佈者添加為主體，請傳遞 `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * 調用 `PolicyEntry` 物件 `setPrincipal`方法和傳遞 `Principal` 物件。
   * 調用 `Policy` 物件 `addPolicyEntry` 方法和傳遞 `PolicyEntry` 物件。

1. 註冊策略。

   * 建立 `PolicyManager` 對象，方法是調用 `DocumentSecurityClient` 物件 `getPolicyManager` 方法。
   * 通過調用 `PolicyManager` 物件 `registerPolicy` 方法並傳遞下列值：

      * 此 `Policy` 表示要註冊的策略的對象。
   * 表示策略所屬策略集的字串值。

   如果您在連線設定中使用AEM Forms管理員帳戶來建立 `DocumentSecurityClient` 對象，然後在調用策略集時指定策略集名稱 `registerPolicy` 方法。 如果您傳入 `null` 策略集的值，策略將在管理員中建立 *我的政策* 策略集。

   如果在連接設定中使用Document Security用戶，則可以調用超載 `registerPolicy` 僅接受策略的方法。 也就是說，您不需要指定策略集名稱。 但是，策略將添加到名為 *我的政策*. 如果不想將新策略添加到此策略集，請在調用 `registerPolicy` 方法。

   >[!NOTE]
   >
   >建立策略時，請參考現有策略集。 如果指定的策略集不存在，則會引發異常。

如需使用Document Security服務的程式碼範例，請參閱下列內容：

* &quot;快速入門（SOAP模式）:使用Java API建立策略」

### 使用Web服務API建立策略 {#create-a-policy-using-the-web-service-api}

使用Document Security API（web服務）建立策略：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立Document Security用戶端API物件。

   * 建立 `DocumentSecurityServiceClient` 物件，使用其預設建構函式。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `RightsManagementServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 設定策略的屬性。

   * 建立 `PolicySpec` 物件，使用其建構子。
   * 為 `PolicySpec` 物件 `name` 資料成員。
   * 為 `PolicySpec` 物件 `description` 資料成員。
   * 將字串值分配給 `PolicySpec` 物件 `policySetName` 資料成員。 必須指定現有策略集名稱。 (您可以指定 `null` ，而此參數值會導致將原則新增至 *我的政策*.)
   * 通過為 `PolicySpec` 物件 `offlineLeasePeriod` 資料成員。
   * 設定 `PolicySpec` 物件 `policyXml` 資料成員，其字串值表示PDRL XML資料。 要執行此任務，請建立.NET `StreamReader` 物件，使用其建構子。 將表示策略的PDRL XML檔案的位置傳遞到 `StreamReader` 建構子。 接下來，叫用 `StreamReader` 物件 `ReadLine` 方法，並將傳回值指派給字串變數。 重複 `StreamReader` 物件，直到 `ReadLine` 方法傳回null。 將字串變數指派給 `PolicySpec` 物件 `policyXml` 資料成員。

1. 建立策略項。

   使用Document Security Web服務API建立策略時，不需要建立策略項。 策略項在PDRL文檔中定義。

1. 註冊策略。

   通過調用 `DocumentSecurityServiceClient` 物件 `registerPolicy` 方法並傳遞下列值：

   * 此 `PolicySpec` 表示要註冊的策略的對象。
   * 表示策略所屬策略集的字串值。 您可以指定 `null` 會導致將原則新增至 *MyPolices* 策略集。

   如果您在連線設定中使用AEM Forms管理員帳戶來建立 `DocumentSecurityClient` 對象，請在調用策略集時指定策略集名稱 `registerPolicy` 方法。

   如果在連接設定中使用Document SecurityDocument Security用戶，則可以調用超載 `registerPolicy` 僅接受策略的方法。 也就是說，您不需要指定策略集名稱。 但是，策略將添加到名為 *我的政策*. 如果不想將新策略添加到此策略集，請在調用 `registerPolicy` 方法。

   >[!NOTE]
   >
   >建立策略並指定策略集時，請確保指定現有策略集。 如果指定的策略集不存在，則會引發異常。

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* 「快速入門(MTOM):使用Web服務API建立策略」
* 「快速入門(SwaRef):使用Web服務API建立策略」

## 修改策略 {#modifying-policies}

您可以使用Document Security Java API或Web服務API修改現有策略。 要更改現有策略，請檢索該策略，修改該策略，然後更新伺服器上的策略。 例如，假設您檢索現有策略並延長其有效期。 在更改生效之前，必須更新策略。

當業務需求改變且策略不再反映這些需求時，您可以修改策略。 您不必建立新策略，只需更新現有策略即可。

要使用Web服務修改策略屬性（例如，使用使用JAX-WS建立的Java代理類），必須確保將策略註冊到Document Security服務中。 然後，您可以使用 `PolicySpec.getPolicyXml` 方法，並使用適用的方法修改策略屬性。 例如，您可以叫用 `PolicySpec.setOfflineLeasePeriod` 方法。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

要修改現有策略，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security用戶端API物件。
1. 檢索現有策略。
1. 更改策略屬性。
1. 更新策略。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Document Security用戶端API物件**

在以寫程式方式執行Document Securityservice操作之前，必須建立Document Security服務客戶端對象。 如果您使用Java API，請建立 `RightsManagementClient` 物件。 如果您使用Document Security Web服務API，請建立 `RightsManagementServiceService` 物件。

**檢索現有策略**

必須檢索現有策略才能修改它。 要檢索策略，請指定策略名稱和策略所屬的策略集。 如果您指定 `null` 策略集名稱的值，則從 *我的政策* 策略集。

**設定策略的屬性**

要修改策略，請修改策略屬性的值。 唯一不能更改的策略屬性是名稱屬性。 例如，要更改策略的離線租用期，可以修改策略的離線租用期屬性值。

使用Web服務修改策略的離線租用期時， `offlineLeasePeriod` 欄位 `PolicySpec` 會忽略介面。 要更新離線租用期，請修改 `OfflineLeasePeriod` 元素。 然後，使用 `PolicySpec` 介面 `policyXML` 資料成員。

>[!NOTE]
>
>如需可設定的其他屬性的相關資訊，請參閱 `Policy` 介面說明，位於 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**更新策略**

在您對策略所做的更改生效之前，必須使用文檔安全服務更新策略。 對保護文檔的策略的更改將在下次與文檔安全服務同步受策略保護的文檔時更新。

### 使用Java API修改現有原則 {#modify-existing-policies-using-the-java-api}

使用Document Security API(Java)修改現有原則：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security用戶端API物件。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `RightsManagementClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 檢索現有策略。

   * 建立 `PolicyManager` 對象，方法是調用 `RightsManagementClient` 物件 `getPolicyManager` 方法。
   * 建立 `Policy` 表示要通過調用 `PolicyManager` 物件 `getPolicy` 方法並傳遞下列值」

      * 表示策略所屬的策略集名稱的字串值。 您可以指定 `null` 會導致 `MyPolicies` 正在使用的策略集。
      * 表示策略名稱的字串值。

1. 設定策略的屬性。

   更改策略的屬性以滿足您的業務需求。 例如，要更改策略的離線租用期，請調用 `Policy` 物件 `setOfflineLeasePeriod` 方法。

1. 更新策略。

   調用以更新策略 `PolicyManager` 物件 `updatePolicy` 方法。 傳遞 `Policy` 表示要更新的策略的對象。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱快速入門（SOAP模式）:使用Java API部分修改策略。

### 使用Web服務API修改現有策略 {#modify-existing-policies-using-the-web-service-api}

使用Document Security API（web服務）修改現有策略：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立Document Security用戶端API物件。

   * 建立 `RightsManagementServiceClient` 物件，使用其預設建構函式。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `RightsManagementServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 檢索現有策略。

   建立 `PolicySpec` 表示要通過調用 `RightsManagementServiceClient` 物件 `getPolicy` 方法並傳遞下列值：

   * 一個字串值，它指定策略所屬的策略集名稱。 您可以指定 `null` 會導致 `MyPolicies` 正在使用的策略集。
   * 指定策略名稱的字串值。

1. 設定策略的屬性。

   更改策略的屬性以滿足您的業務需求。

1. 更新策略。

   叫用 `RightsManagementServiceClient` 物件 `updatePolicyFromSDK` 方法和傳遞 `PolicySpec` 表示要更新的策略的對象。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* 「快速入門(MTOM):使用Web服務API修改策略」
* 「快速入門(SwaRef):使用Web服務API修改策略」

## 刪除策略 {#deleting-policies}

您可以使用Document Security Java API或Web服務API刪除現有策略。 刪除策略後，將無法再用於保護文檔。 但是，使用策略的現有受策略保護文檔仍受到保護。 當有較新的策略可用時，您可以刪除策略。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-2}

要刪除現有策略，請執行以下步驟：

1. 包含項目檔案
1. 建立Document Security用戶端API物件。
1. 刪除策略。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Document Security用戶端API物件**

在以寫程式方式執行Document Security服務操作之前，必須建立Document Security服務客戶端對象。 如果您使用Java API，請建立 `RightsManagementClient` 物件。 如果您使用Document Security Web服務API，請建立 `RightsManagementServiceService` 物件。

**刪除策略**

要刪除策略，請指定要刪除的策略以及該策略所屬的策略集。 使用其設定來叫用AEM Forms的使用者必須擁有刪除原則的權限；否則會發生例外狀況。 同樣，如果嘗試刪除不存在的策略，則會發生異常。

### 使用Java API刪除策略 {#delete-policies-using-the-java-api}

使用Document Security API(Java)刪除策略：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security用戶端API物件。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `RightsManagementClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 刪除策略。

   * 建立 `PolicyManager` 對象，方法是調用 `RightsManagementClient` 物件 `getPolicyManager` 方法。
   * 叫用 `PolicyManager` 物件 `deletePolicy` 方法並傳遞下列值：

      * 一個字串值，它指定策略所屬的策略集名稱。 您可以指定 `null` 會導致 `MyPolicies` 正在使用的策略集。
      * 一個字串值，它指定要刪除的策略的名稱。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* &quot;快速入門（SOAP模式）:使用Java API刪除策略」

### 使用Web服務API刪除策略 {#delete-policies-using-the-web-service-api}

使用Document Security API（web服務）刪除策略：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立Document Security用戶端API物件。

   * 建立 `RightsManagementServiceClient` 物件，使用其預設建構函式。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `RightsManagementServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 刪除策略。

   叫用 `RightsManagementServiceClient` 物件 `deletePolicy` 方法並傳遞下列值：

   * 一個字串值，它指定策略所屬的策略集名稱。 您可以指定 `null` 會導致 `MyPolicies` 正在使用的策略集。
   * 一個字串值，它指定要刪除的策略的名稱。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* 「快速入門(MTOM):使用Web服務API刪除策略」
* 「快速入門(SwaRef):使用Web服務API刪除策略」

## 將策略應用於PDF文檔 {#applying-policies-to-pdf-documents}

您可以將策略應用到PDF文檔以保護文檔。 通過將策略應用於PDF文檔，可以限制對文檔的訪問。 如果文檔已使用策略進行了保護，則無法將策略應用到文檔。

在檔案開啟時，您也可以限制對Acrobat和Adobe Reader功能的存取，包括列印和複製文字、進行變更，以及為檔案新增簽名和註解的功能。 此外，當您不再希望用戶訪問該文檔時，可以撤銷受策略保護的PDF文檔。

在分發受策略保護的文檔後，您可以監視其使用情況。 也就是說，您可以看到檔案的使用方式，以及使用者。 例如，您可以找出有人何時開啟檔案。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-3}

要將策略應用於PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security用戶端API物件。
1. 檢索應用策略的PDF文檔。
1. 將現有策略應用於PDF文檔。
1. 保存受策略保護的PDF文檔。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Document Security Client API對象**

在以寫程式方式執行Document Security服務操作之前，請建立Document Security服務客戶端對象。 如果您使用Java API，請建立 `DocumentSecurityClient` 物件。 如果您使用Document Security Web服務API，請建立 `DocumentSecurityServiceService` 物件。

**檢索PDF文檔**

您可以檢索PDF文檔以應用策略。 將策略應用到PDF文檔後，在使用文檔時將限制用戶。 例如，如果策略不允許離線時開啟文檔，則用戶必須聯機才能開啟文檔。

**將現有策略應用於PDF文檔**

要將策略應用於PDF文檔，請參考現有策略並指定策略所屬的策略集。 設定連接屬性的用戶必須具有對指定策略的訪問權限。 否則會發生例外。

**保存PDF文檔**

在文檔安全服務將策略應用到PDF文檔後，您可以將受策略保護的PDF文檔另存為PDF檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[撤消對文檔的訪問](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API將策略應用於PDF文檔 {#apply-a-policy-to-a-pdf-document-using-the-java-api}

使用Document Security API(Java)將策略應用於PDF文檔：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security用戶端API物件。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `RightsManagementClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 檢索PDF文檔。

   * 建立 `java.io.FileInputStream` 使用其建構子表示PDF文檔的對象。 傳遞指定PDF文檔位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 將現有策略應用於PDF文檔。

   * 建立 `DocumentManager` 對象，方法是調用 `RightsManagementClient` 物件 `getDocumentManager` 方法。
   * 通過調用 `DocumentManager` 物件 `protectDocument` 方法並傳遞下列值：

      * 此 `com.adobe.idp.Document` 包含應用策略的PDF文檔的對象。
      * 指定文檔名稱的字串值。
      * 一個字串值，它指定策略所屬的策略集的名稱。 您可以指定 `null` 產生 `MyPolicies` 正在使用的策略集。
      * 指定策略名稱的字串值。
      * 一個字串值，它表示作為文檔發佈者的用戶的用戶管理域的名稱。 此參數值為可選值，可為null（如果此參數為null，則下一個參數值必須為null）。
      * 一個字串值，它表示作為文檔發佈者的用戶管理器用戶的規範名稱的名稱。 此參數值為選用值，可以是 `null` (如果此參數為null，則上一個參數值必須為 `null`)。
      * A `com.adobe.livecycle.rightsmanagement.Locale` 表示用於選擇MS Office模板的區域設定。 此參數值為可選值，不用於PDF文檔。 要保護PDF文檔，請指定 `null`.

      此 `protectDocument` 方法傳回 `RMSecureDocumentResult` 包含受策略保護的PDF文檔的對象。


1. 保存PDF文檔。

   * 叫用 `RMSecureDocumentResult` 物件 `getProtectedDoc` 獲取受策略保護的PDF文檔的方法。 此方法會傳回 `com.adobe.idp.Document` 物件。
   * 建立 `java.io.File` 物件，並確定副檔名為PDF。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 複製內容的方法 `Document` 物件(請確定您使用 `Document` 由傳回的物件 `getProtectedDoc` 方法)。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* &quot;快速入門（EJB模式）:使用Java API將原則套用至PDF檔案」
* &quot;快速入門（SOAP模式）:使用Java API將原則套用至PDF檔案」

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將策略應用到PDF文檔 {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

使用Document Security API（web服務）將策略應用於PDF文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立Document Security用戶端API物件。

   * 建立 `RightsManagementServiceClient` 物件，使用其預設建構函式。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `RightsManagementServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 檢索PDF文檔。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存應用策略的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 透過取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 位元組陣列內容的欄位。

1. 將現有策略應用於PDF文檔。

   通過調用 `RightsManagementServiceClient` 物件 `protectDocument` 方法並傳遞下列值：

   * 此 `BLOB` 包含應用策略的PDF文檔的對象。
   * 指定文檔名稱的字串值。
   * 一個字串值，它指定策略所屬的策略集的名稱。 您可以指定 `null` 產生 `MyPolicies` 正在使用的策略集。
   * 指定策略名稱的字串值。
   * 一個字串值，它表示作為文檔發佈者的用戶的用戶管理域的名稱。 此參數值為選用值，且可為null(如果此參數為null，則下一個參數值必須為 `null`)。
   * 一個字串值，它表示作為文檔發佈者的用戶管理器用戶的規範名稱的名稱。 此參數值為選用值，且可為null(如果此參數為null，則上一個參數值必須為 `null`)。
   * A `RMLocale` 指定地區設定值的值(例如 `RMLocale.en`)。
   * 用於儲存策略標識符值的字串輸出參數。
   * 用於儲存受策略保護的標識符值的字串輸出參數。
   * 用於儲存mime類型的字串輸出參數(例如， `application/pdf`)。

   此 `protectDocument` 方法傳回 `BLOB` 包含受策略保護的PDF文檔的對象。

1. 保存PDF文檔。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示受策略保護的PDF文檔的檔案位置。
   * 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `protectDocument` 方法。 取得 `BLOB` 物件 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* 「快速入門(MTOM):使用Web服務API將策略應用到PDF文檔」
* 「快速入門(SwaRef):使用Web服務API將策略應用到PDF文檔。

## 從PDF文檔中刪除策略 {#removing-policies-from-pdf-documents}

可以從受策略保護的文檔中刪除策略，以便從文檔中刪除安全性。 也就是說，如果您不再希望該文檔受策略保護。 如果要使用較新的策略更新受策略保護的文檔，則不刪除該策略並添加更新的策略，切換該策略會更加有效。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-4}

要從受策略保護的PDF文檔中刪除策略，請執行以下步驟：

1. 包含項目檔案
1. 建立Document Security用戶端API物件。
1. 檢索受策略保護的PDF文檔。
1. 從PDF文檔中刪除策略。
1. 保存不安全的PDF文檔。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Document Security用戶端API物件**

在以寫程式方式執行Document Security服務操作之前，請建立Document Security服務客戶端對象。

**檢索受策略保護的PDF文檔**

可以檢索受策略保護的PDF文檔以刪除策略。 如果嘗試從未受策略保護的PDF文檔中刪除策略，將導致異常。

**從PDF文檔中刪除策略**

如果在連接設定中指定了管理員，則可以從受策略保護的PDF文檔中刪除策略。 否則，用於保護文檔的策略必須包含 `SWITCH_POLICY` 權限，以便從PDF文檔中刪除策略。 此外，在AEM Forms連線設定中指定的使用者也必須擁有該權限。 否則，會擲回例外。

**保存不安全的PDF文檔**

在Document Security服務從PDF文檔中刪除策略後，您可以將不安全的PDF文檔另存為PDF檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[將策略應用於PDF文檔](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API從PDF文檔中刪除策略 {#remove-a-policy-from-a-pdf-document-using-the-java-api}

使用Document Security API(Java)從受策略保護的PDF文檔中刪除策略：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security用戶端API物件。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocumentSecurityClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 檢索受策略保護的PDF文檔。

   * 建立 `java.io.FileInputStream` 表示受策略保護的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 從PDF文檔中刪除策略。

   * 建立 `DocumentManager` 對象，方法是調用 `DocumentSecurityClient` 物件 `getDocumentManager` 方法。
   * 通過調用 `DocumentManager` 物件 `removeSecurity` 方法和傳遞 `com.adobe.idp.Document` 包含受策略保護的PDF文檔的對象。 此方法會傳回 `com.adobe.idp.Document` 包含不安全PDF文檔的對象。

1. 保存不安全的PDF文檔。

   * 建立 `java.io.File` 物件，並確定副檔名為PDF。
   * 叫用 `Document` 物件 `copyToFile` 複製內容的方法 `Document` 物件(請確定您使用 `Document` 由傳回的物件 `removeSecurity` 方法)。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* &quot;快速入門（SOAP模式）:使用Java API從PDF文檔中刪除策略」

### 使用Web服務API刪除策略 {#remove-a-policy-using-the-web-service-api}

使用文檔安全API（Web服務）從受策略保護的PDF文檔中刪除策略：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立Document Security用戶端API物件。

   * 建立 `DocumentSecurityServiceClient` 物件，使用其預設建構函式。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DocumentSecurityServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 檢索受策略保護的PDF文檔。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存從中刪除策略的受策略保護的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 位元組陣列內容的欄位。

1. 從PDF文檔中刪除策略。

   通過調用 `DocumentSecurityServiceClient` 物件 `removePolicySecurity` 方法和傳遞 `BLOB` 包含受策略保護的PDF文檔的對象。 此方法會傳回 `BLOB` 包含不安全PDF文檔的對象。

1. 保存不安全的PDF文檔。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示不安全PDF文檔的檔案位置。
   * 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `removePolicySecurity` 方法。 取得 `BLOB` 物件 `MTOM` 欄位。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* 「快速入門(MTOM):使用Web服務API從PDF文檔中刪除策略「
* 「快速入門(SwaRef):使用Web服務API從PDF文檔中刪除策略」

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 撤消對文檔的訪問 {#revoking-access-to-documents}

您可以撤消對受策略保護的PDF文檔的訪問，導致用戶無法訪問該文檔的所有副本。 當使用者嘗試開啟撤銷的PDF檔案時，系統會將他們重新導向至指定的URL，以便檢視修訂的檔案。 必須以程式設計方式指定使用者重新導向的URL。 當您撤銷對文檔的訪問權時，此更改將在用戶下次通過聯機開啟受策略保護的文檔與文檔安全服務同步時生效。

撤銷對文檔的訪問權的能力提供了額外的安全性。 例如，假設文檔有較新版本，並且您不再希望任何人查看過期版本。 在這種情況下，可以撤銷對舊文檔的訪問，除非恢復訪問，否則任何人都無法查看該文檔。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-5}

要撤銷受策略保護的文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security用戶端API物件。
1. 檢索受策略保護的PDF文檔。
1. 撤消受策略保護的文檔。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Document Security用戶端API物件**

在以寫程式方式執行Document Security服務操作之前，必須建立Document Security服務客戶端對象。

**檢索受策略保護的PDF文檔**

必須檢索受策略保護的PDF文檔才能撤銷它。 不能撤消已撤銷或不是受策略保護的文檔。

如果您知道受策略保護文檔的許可證標識符值，則不需要檢索受策略保護的PDF文檔。 但是，在大多數情況下，您需要檢索PDF文檔才能獲得許可證標識符值。

**撤消受策略保護的文檔**

要撤銷受策略保護的文檔，請指定受策略保護文檔的許可證標識符。 此外，您還可以指定當用戶嘗試開啟撤消的文檔時可以查看的文檔的URL。 也就是說，假設已過時的檔案被撤銷。 當用戶嘗試開啟已撤銷的文檔時，他們將看到更新的文檔，而不是已撤銷的文檔。

>[!NOTE]
>
>如果嘗試撤消已撤消的文檔，則會引發異常。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[將策略應用於PDF文檔](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[恢復對已撤銷文檔的訪問](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### 使用Java API撤銷對文檔的訪問 {#revoke-access-to-documents-using-the-java-api}

使用Document Security API(Java)撤銷對受策略保護的PDF文檔的訪問：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security用戶端API物件

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocumentSecurityClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 檢索受策略保護的PDF文檔

   * 建立 `java.io.FileInputStream` 表示受策略保護的PDF文檔的對象，方法是使用其建構子並傳遞指定PDF文檔位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 撤消受策略保護的文檔

   * 建立 `DocumentManager` 對象，方法是調用 `DocumentSecurityClient` 物件 `getDocumentManager` 方法。
   * 通過調用 `DocumentManager` 物件 `getLicenseId` 方法。 傳遞 `com.adobe.idp.Document` 表示受策略保護文檔的對象。 此方法會傳回代表授權識別碼值的字串值。
   * 建立 `LicenseManager` 對象，方法是調用 `DocumentSecurityClient` 物件 `getLicenseManager` 方法。
   * 通過調用 `LicenseManager` 物件 `revokeLicense` 方法並傳遞下列值：

      * 一個字串值，它指定受策略保護文檔的許可證標識符值(指定 `DocumentManager` 物件 `getLicenseId` 方法)。
      * 的靜態資料成員 `License` 指定撤消文檔的原因的介面。 例如，您可以指定 `License.DOCUMENT_REVISED`.
      * A `java.net.URL` 指定修訂文檔所在位置的值。 如果您不想將使用者重新導向至其他URL，則可以傳遞 `null`.

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* &quot;快速入門（SOAP模式）:使用Java API撤銷文檔」

### 使用Web服務API撤銷對文檔的訪問 {#revoke-access-to-documents-using-the-web-service-api}

使用Document Security API（Web服務）撤消對受策略保護的PDF文檔的訪問：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立Document Security用戶端API物件

   * 建立 `DocumentSecurityServiceClient` 物件，使用其預設建構函式。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DocumentSecurityServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 檢索受策略保護的PDF文檔

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存被撤銷的受策略保護的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示要撤銷的策略保護PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 位元組陣列內容的欄位。

1. 撤消受策略保護的文檔

   * 通過調用 `DocumentSecurityServiceClient` 物件 `getLicenseID` 方法和傳遞 `BLOB` 表示受策略保護文檔的對象。 此方法會傳回代表授權識別碼的字串值。
   * 通過調用 `DocumentSecurityServiceClient` 物件 `revokeLicense` 方法並傳遞下列值：

      * 一個字串值，它指定受策略保護文檔的許可證標識符值(指定 `DocumentSecurityServiceService` 物件 `getLicenseId` 方法)。
      * 的靜態資料成員 `Reason` 指定撤消文檔的原因的枚舉。 例如，您可以指定 `Reason.DOCUMENT_REVISED`.
      * A `string` 指定修訂文檔所在的URL位置的值。 如果您不想將使用者重新導向至其他URL，則可以傳遞 `null`.

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* 「快速入門(MTOM):使用Web服務API撤消文檔」
* 「快速入門(SwaRef):使用Web服務API撤消文檔」

**另請參閱**

[從Word文檔中刪除策略](protecting-documents-policies.md#removing-policies-from-word-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 恢復對已撤銷文檔的訪問 {#reinstating-access-to-revoked-documents}

您可以恢復對已撤銷PDF文檔的訪問權，從而使用戶可以訪問已撤銷文檔的所有副本。 當用戶開啟被撤消的恢復文檔時，用戶可以查看該文檔。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-6}

要恢復對已撤銷PDF文檔的訪問，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security用戶端API物件。
1. 檢索已撤銷PDF文檔的許可證標識符。
1. 恢復對已撤銷PDF文檔的訪問。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Document Security用戶端API物件**

在以寫程式方式執行Document Security服務操作之前，必須建立Document Security服務客戶端對象。 如果您使用Java API，請建立 `DocumentSecurityClient` 物件。 如果您使用Document Security Web服務API，請建立 `DocumentSecurityServiceService` 物件。

**檢索已撤銷的PDF文檔的許可證標識符**

您必須檢索已撤銷PDF文檔的許可證標識符，才能恢復已撤銷的PDF文檔。 獲取許可證標識符值後，可以恢復已撤銷的文檔。 如果嘗試恢復未撤銷的文檔，將導致異常。

**恢復對已撤銷PDF文檔的訪問**

要恢復對已撤銷PDF文檔的訪問，必須指定已撤銷文檔的許可證標識符。 如果嘗試恢復未撤銷的PDF文檔的訪問權，將導致異常。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[將策略應用於PDF文檔](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[撤消對文檔的訪問](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API恢復對撤銷文檔的訪問 {#reinstate-access-to-revoked-documents-using-the-java-api}

使用文檔安全API(Java)恢復對已撤銷文檔的訪問：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security用戶端API物件。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocumentSecurityClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 檢索已撤銷PDF文檔的許可證標識符。

   * 建立 `java.io.FileInputStream` 表示已撤銷PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。
   * 建立 `DocumentManager` 對象，方法是調用 `DocumentSecurityClient` 物件 `getDocumentManager` 方法。
   * 通過調用 `DocumentManager` 物件 `getLicenseId` 方法和傳遞 `com.adobe.idp.Document` 表示已撤銷文檔的對象。 此方法會傳回代表授權識別碼的字串值。

1. 恢復對已撤銷PDF文檔的訪問。

   * 建立 `LicenseManager` 對象，方法是調用 `DocumentSecurityClient` 物件 `getLicenseManager` 方法。
   * 通過調用 `LicenseManager` 物件 `unrevokeLicense` 方法，並傳遞已撤銷檔案的授權識別碼值。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* &quot;快速入門（SOAP模式）:使用Web服務API恢復對已撤銷文檔的訪問」

### 使用Web服務API恢復對已撤銷文檔的訪問 {#reinstate-access-to-revoked-documents-using-the-web-service-api}

使用文檔安全API（Web服務）恢復對已撤銷文檔的訪問：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立Document Security用戶端API物件。

   * 建立 `DocumentSecurityServiceClient` 物件，使用其預設建構函式。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DocumentSecurityServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 檢索已撤銷PDF文檔的許可證標識符。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存撤消的PDF文檔，該文檔將恢復訪問。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示已撤銷PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 位元組陣列內容的欄位。

1. 恢復對已撤銷PDF文檔的訪問。

   * 通過調用 `DocumentSecurityServiceClient` 物件 `getLicenseID` 方法和傳遞 `BLOB` 表示已撤銷文檔的對象。 此方法會傳回代表授權識別碼的字串值。
   * 通過調用 `DocumentSecurityServiceClient` 物件 `unrevokeLicense` 方法，並傳遞字串值，該字串值指定已撤銷PDF文檔的許可標識符值(傳遞 `DocumentSecurityServiceClient` 物件 `getLicenseId` 方法)。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* 「快速入門(MTOM):使用Web服務API恢復對已撤銷文檔的訪問」
* 「快速入門(SwaRef):使用Web服務API恢復對已撤銷文檔的訪問」

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 檢查受策略保護的PDF文檔 {#inspecting-policy-protected-pdf-documents}

您可以使用Document Security Service API（Java和Web服務）來檢查受原則保護的PDF檔案。 檢查受策略保護的PDF文檔時，返回有關受策略保護的PDF文檔的資訊。 例如，您可以確定用於保護文檔的策略以及保護文檔的日期。

如果您的LiveCycle版本為8.x或更早版本，則無法執行此任務。 AEM Forms中新增了檢查受原則保護檔案的支援。 如果嘗試使用LiveCycle8.x（或更早版本）檢查受策略保護的文檔，則會引發異常。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-7}

要檢查受策略保護的PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security用戶端API物件。
1. 檢索要檢查的受策略保護的文檔。
1. 獲取有關受策略保護文檔的資訊。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security用戶端API物件**

在以寫程式方式執行Document Security服務操作之前，請建立Document Security服務客戶端對象。 如果您使用Java API，請建立 `RightsManagementClient` 物件。 如果您使用Document Security Web服務API，請建立 `RightsManagementServiceService` 物件。

**檢索受策略保護的文檔以檢查**

要檢查受策略保護的文檔，請檢索它。 如果嘗試檢查未通過策略進行保護或被撤銷的文檔，則會引發異常。

**Inspect檔案**

檢索受策略保護的文檔後，可以檢查它。

**獲取有關受策略保護文檔的資訊**

檢查受策略保護的PDF文檔後，可以獲取有關該文檔的資訊。 例如，您可以確定用於保護文檔的策略。

如果您使用屬於「我的策略」的策略保護文檔，然後調用 `RMInspectResult.getPolicysetName` 或 `RMInspectResult.getPolicysetId`，則會傳回null。

如果使用包含在策略集（「我的策略」除外）中的策略保護文檔，則 `RMInspectResult.getPolicysetName` 和 `RMInspectResult.getPolicysetId` 傳回有效的字串。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Inspect使用Java API的受策略保護的PDF文檔 {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspect是受原則保護的PDF檔案，使用檔案安全性服務API(Java):

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。 如需這些檔案的位置資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. 建立Document Security用戶端API物件。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 建立 `RightsManagementClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 檢索要檢查的受策略保護的文檔。

   * 建立 `java.io.FileInputStream` 使用其建構子表示受策略保護的PDF文檔的對象。 傳遞指定PDF文檔位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. Inspect檔案。

   * 建立 `DocumentManager` 對象，方法是調用 `RightsManagementClient` 物件 `getDocumentManager` 方法。
   * Inspect通過調用 `LicenseManager` 物件 `inspectDocument` 方法。 傳遞 `com.adobe.idp.Document` 包含受策略保護的PDF文檔的對象。 此方法會傳回 `RMInspectResult` 包含有關受策略保護文檔的資訊的對象。

1. 獲取有關受策略保護文檔的資訊。

   要獲取有關受策略保護文檔的資訊，請調用相應的方法 `RMInspectResult` 物件。 例如，要檢索策略名稱，請調用 `RMInspectResult` 物件 `getPolicyName` 方法。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* &quot;快速入門（SOAP模式）:使用Java API檢查受策略保護的PDF文檔」

### Inspect使用Web服務API的受策略保護的PDF文檔 {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspect是受政策保護的PDF檔案，使用檔案安全服務API（web服務）:

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立Document Security用戶端API物件。

   * 建立 `RightsManagementServiceClient` 物件，使用其預設建構函式。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `RightsManagementServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 檢索要檢查的受策略保護的文檔。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存要檢查的PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞一個字串值，該字串值表示PDF文檔的檔案位置，以及在中開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 位元組陣列內容的欄位。

1. Inspect檔案。

   Inspect通過調用 `RightsManagementServiceClient` 物件 `inspectDocument` 方法。 傳遞 `BLOB` 包含受策略保護的PDF文檔的對象。 此方法會傳回 `RMInspectResult` 包含有關受策略保護文檔的資訊的對象。

1. 獲取有關受策略保護文檔的資訊。

   要獲取有關受策略保護文檔的資訊，請獲取屬於的相應欄位的值 `RMInspectResult` 物件。 例如，要檢索策略名稱，請獲取 `RMInspectResult` 物件 `policyName` 欄位。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* 「快速入門(MTOM):使用Web服務API檢查受策略保護的PDF文檔」
* 「快速入門(SwaRef):使用Web服務API檢查受策略保護的PDF文檔」

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 建立水印 {#creating-watermarks}

水印通過唯一地識別文檔和控製版權侵權來幫助確保文檔的安全。 例如，您可以建立並放置一個水印，該水印在文檔的所有頁面上聲明「機密」。 建立浮水印後，您可以將其納入策略。 也就是說，可以使用新建立的水印來設定策略的水印屬性。 將包含水印的策略應用到文檔後，該水印將出現在受策略保護的文檔中。

>[!NOTE]
>
>只有具有Document Security管理權限的用戶才能建立水印。 也就是說，在定義建立Document Security服務客戶端對象所需的連接設定時，必須指定這樣的用戶。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-8}

要建立水印，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security用戶端API物件。
1. 設定水印屬性。
1. 向Document Security服務註冊水印。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Document Security用戶端API物件**

在以寫程式方式執行Document Security服務操作之前，必須建立Document Security服務客戶端對象。 如果您使用Java API，請建立 `RightsManagementClient` 物件。 如果您使用Document Security Web服務API，請建立 `RightsManagementServiceService` 物件。

**設定水印屬性**

要建立新水印，必須設定水印屬性。 必須始終定義name屬性。 除了name屬性之外，您至少必須設定以下屬性之一：

* 自訂文字
* DateIncluded
* UserIdIncluded
* UserNameIncluded

下表列出使用網站服務建立浮水印時所需的索引鍵和值組。

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
   <td><p>指定開啟文檔的用戶的用戶名是否屬於水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>指定開啟文檔的用戶的標識是否屬於水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>指定當前日期是否是水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>如果此值為true，則必須使用 <code>WaterBackCmd:SRCTEXT</code>.</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>指定水印的不透明度。 如果未指定，則預設值為0.5。</p></td>
   <td><p>介於0.0和1.0之間的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>指定水印的旋轉。 預設值為0度。</p></td>
   <td><p>介於0到359之間的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>若已指定此值，則 <code>WaterBackCmd:IS_SIZE_ENABLED</code> 必須存在，且值必須為true。 如果未指定此屬性，則預設行為適合頁面。</p></td>
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
   <td><p>頂部、中間或底部</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>指定水印是否為背景。 預設值為false。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>如果指定自訂比例，則為true。 如果此值為true，則還必須指定SCALE。 如果此值為false，則預設值適合頁面大小。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>指定浮水印的自定義文本。 如果此值存在，則 <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> 也必須存在且設為true。</p></td>
   <td><p>True或False</p></td>
  </tr>
 </tbody>
</table>

所有水印都必須定義以下屬性之一：

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

所有其他屬性均為選用。

**註冊水印**

必須先向Document Security服務註冊新水印，才能使用。 註冊水印後，可以在策略中使用它。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[將策略應用於PDF文檔](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API建立水印 {#create-watermarks-using-the-java-api}

使用Document Security API(Java)建立浮水印：

1. 包含專案檔案。

   包括客戶端JAR檔案，如 `adobe-rightsmanagement-client.jar`，位於Java專案的類別路徑中。

1. 建立Document Security用戶端API物件。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `RightsManagementClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 設定浮水印屬性

   * 建立 `Watermark` 對象，方法是調用 `InfomodelObjectFactory` 對象的靜態 `createWatermark` 方法。 此方法會傳回 `Watermark` 物件。
   * 通過調用 `Watermark` 物件 `setName` 方法，並傳遞指定策略名稱的字串值。
   * 調用 `Watermark` 物件 `setBackground` 方法與傳遞 `true`. 通過設定此屬性，水印將出現在文檔的背景中。
   * 調用 `Watermark` 物件 `setCustomText` 方法，並傳遞代表浮水印文字的字串值。
   * 調用 `Watermark` 物件 `setOpacity` 方法，並傳遞指定不透明度級別的整數值。 值100表示水印完全不透明，值0表示水印完全透明。

1. 註冊水印。

   * 建立 `WatermarkManager` 對象，方法是調用 `RightsManagementClient` 物件 `getWatermarkManager` 方法。 此方法會傳回 `WatermarkManager` 物件。
   * 通過調用 `WatermarkManager` 物件 `registerWatermark` 方法和傳遞 `Watermark` 表示要註冊的水印的對象。 此方法會傳回一個字串值，代表浮水印的識別值。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* &quot;快速入門（SOAP模式）:使用Java API建立浮水印&quot;

### 使用Web服務API建立水印 {#create-watermarks-using-the-web-service-api}

使用Document Security API（web服務）建立浮水印：

1. 建立Document Security用戶端API物件。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立Document Security用戶端API物件。

   * 建立 `RightsManagementServiceClient` 物件，使用其預設建構函式。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `RightsManagementServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 設定浮水印屬性。

   * 建立 `WatermarkSpec` 對象，方法是調用 `WatermarkSpec` 建構子。
   * 通過為 `WatermarkSpec` 物件 `name` 資料成員。
   * 設定浮水印的 `id` 屬性，將字串值指派給 `WatermarkSpec` 物件 `id` 資料成員。
   * 對於要設定的每個水印屬性，建立一個單獨的 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 為 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `key` 資料成員(例如， `WaterBackCmd:OPACITY)`.
   * 將值指派給 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `value` 資料成員(例如， `.25`)。
   * 建立 `MyArrayOf_xsd_anyType` 物件。 針對每個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象，調用 `MyArrayOf_xsd_anyType` 物件 `Add` 方法。 傳遞 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 指派 `MyArrayOf_xsd_anyType` 物件 `WatermarkSpec` 物件 `values` 資料成員。

1. 註冊水印。

   通過調用 `RightsManagementServiceClient` 物件 `registerWatermark` 方法和傳遞 `WatermarkSpec` 表示要註冊的水印的對象。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* 「快速入門(MTOM):使用網站服務API建立浮水印」
* 「快速入門(SwaRef):使用網站服務API建立浮水印」

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改水印 {#modifying-watermarks}

您可以使用Document Security Java API或Web服務API修改現有水印。 要對現有水印進行更改，可以檢索水印，修改其屬性，然後在伺服器上更新它。 例如，假設您檢索水印並修改其不透明度屬性。 在更改生效之前，必須更新水印。

當您修改水印時，此更改將影響應用了水印的將來文檔。 即，包含水印的現有PDF文檔不受影響。

>[!NOTE]
>
>只有具有Document Security管理權限的用戶才能修改水印。 也就是說，在定義建立Document Security服務客戶端對象所需的連接設定時，必須指定這樣的用戶。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-9}

要修改水印，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security用戶端API物件。
1. 檢索要修改的水印。
1. 設定水印屬性。
1. 更新浮水印。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Document Security用戶端API物件**

在以寫程式方式執行Document Security服務操作之前，必須建立Document Security服務客戶端對象。 如果您使用Java API，請建立 `DocumentSecurityClient` 物件。 如果您使用Document Security Web服務API，請建立 `DocumentSecurityServiceService` 物件。

**檢索要修改的水印**

要修改水印，必須檢索現有水印。 可以通過指定水印的名稱或通過指定水印的標識符值來檢索水印。

**設定水印屬性**

要修改現有水印，請更改一個或多個水印屬性的值。 當使用Web服務以寫程式方式更新水印時，必須設定最初設定的所有屬性，即使值未更改。 例如，假設已設定以下水印屬性： `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY`，和 `WaterBackCmd:SRCTEXT`. 雖然您唯一要修改的屬性是 `WaterBackCmd:OPACITY`，您必須將其他值設為正常。

>[!NOTE]
>
>使用Java API修改浮水印時，不需要指定所有屬性。 設定要修改的水印屬性。

>[!NOTE]
>
>有關水印屬性名稱的資訊，請參見 [建立水印](protecting-documents-policies.md#creating-watermarks).

**更新浮水印**

修改水印的屬性後，必須更新水印。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[建立水印](protecting-documents-policies.md#creating-watermarks)

### 使用Java API修改水印 {#modify-watermarks-using-the-java-api}

使用Document Security API(Java)修改浮水印：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security用戶端API物件。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocumentSecurityClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 檢索要修改的水印。

   建立 `WatermarkManager` 對象，方法是調用 `DocumentSecurityClient` 物件 `getWatermarkManager` 方法，並傳遞指定水印名稱的字串值。 此方法會傳回 `Watermark` 表示要修改的水印的對象。

1. 設定浮水印屬性。

   調用 `Watermark` 物件 `setOpacity` 方法，並傳遞指定不透明度級別的整數值。 值100表示水印完全不透明，值0表示水印完全透明。

   >[!NOTE]
   >
   >此示例僅修改不透明度屬性。

1. 更新浮水印。

   * 通過調用 `WatermarkManager` 物件 `updateWatermark` 方法並傳遞 `Watermark` 已修改其屬性的對象。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱快速入門（SOAP模式）:使用Java API部分修改水印。

### 使用Web服務API修改水印 {#modify-watermarks-using-the-web-service-api}

使用Document Security API（web服務）修改浮水印：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立Document Security用戶端API物件。

   * 建立 `DocumentSecurityServiceClient` 物件，使用其預設建構函式。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DocumentSecurityServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 檢索要修改的水印。

   通過調用 `DocumentSecurityServiceClient` 物件 `getWatermarkByName` 方法。 傳遞指定浮水印名稱的字串值。 此方法會傳回 `WatermarkSpec` 表示要修改的水印的對象。

1. 設定浮水印屬性。

   * 對於要更新的每個水印屬性，建立單獨的 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 為 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `key` 資料成員(例如， `WaterBackCmd:OPACITY)`.
   * 將值指派給 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `value` 資料成員(例如， `.50`)。
   * 建立 `MyArrayOf_xsd_anyType` 物件。 針對每個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象，調用 `MyArrayOf_xsd_anyType` 物件 `Add` 方法。 傳遞 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 指派 `MyArrayOf_xsd_anyType` 物件 `WatermarkSpec` 物件 `values` 資料成員。

1. 更新浮水印。

   通過調用 `DocumentSecurityServiceClient` 物件 `updateWatermark` 方法和傳遞 `WatermarkSpec` 表示要修改的水印的對象。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* 「快速入門(MTOM):使用Web服務API修改水印&quot;

## 搜尋事件 {#searching-for-events}

Rights Management服務會在發生特定操作時跟蹤這些操作，例如將策略應用到文檔、開啟受策略保護的文檔以及撤消對文檔的訪問。 必須為Rights Management服務啟用事件審核，否則不會追蹤事件。

事件分為下列其中一類：

* 管理員事件是與管理員相關的操作，如建立新的管理員帳戶。
* 文檔事件是與文檔相關的操作，如關閉受策略保護的文檔。
* 策略事件是與策略相關的操作，如建立新策略。
* 服務事件是與Rights Management服務相關的操作，如與用戶目錄同步。

您可以使用Rights ManagementJava API或網站服務API來搜尋指定的事件。 通過搜索事件，您可以執行任務，例如建立某些事件的日誌檔案。

>[!NOTE]
>
>如需Rights Management服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-10}

要搜索Rights Management事件，請執行以下步驟：

1. 包含專案檔案。
1. 建立Rights Management用戶端API物件。
1. 指定要搜尋的事件。
1. 搜尋事件。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Rights Management用戶端API物件**

在以寫程式方式執行Rights Management服務操作之前，必須建立Rights Management服務客戶端對象。 如果您使用Java API，請建立 `DocumentSecurityClient` 物件。 如果您使用Rights Management網站服務API，請建立 `DocumentSecurityServiceService` 物件。

**指定要搜尋的事件**

必須指定要搜索的事件。 例如，可以搜索策略建立事件，該事件在建立新策略時發生。

**搜尋事件**

指定要搜尋的事件後，您可以使用Rights ManagementJava API或Rights Management網站服務API來搜尋事件。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API搜尋事件 {#search-for-events-using-the-java-api}

使用Rights ManagementAPI(Java)搜尋事件：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Rights Management用戶端API物件

   建立 `DocumentSecurityClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定要搜尋的事件

   * 建立 `EventManager` 對象，方法是調用 `DocumentSecurityClient` 物件 `getEventManager` 方法。 此方法會傳回 `EventManager` 物件。
   * 建立 `EventSearchFilter` 對象，方法是調用其建構子。
   * 叫用 `EventSearchFilter` 物件 `setEventCode` 傳遞屬於靜態資料成員的方法 `EventManager` 代表要搜尋的事件的類別。 例如，要搜索策略建立事件，請傳遞 `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >您可以叫用 `EventSearchFilter` 物件方法。 例如，叫用 `setUserName` 方法來指定與事件相關聯的使用者。

1. 搜尋事件

   叫用 `EventManager` 物件 `searchForEvents` 方法和傳遞 `EventSearchFilter` 定義事件搜尋准則的物件。 此方法會傳回陣列 `Event` 對象。

**程式碼範例**

如需使用Rights Management服務的程式碼範例，請參閱下列快速入門：

* &quot;快速入門(SOAP):使用Java API搜尋事件」

### 使用網站服務API搜尋事件 {#search-for-events-using-the-web-service-api}

使用Rights ManagementAPI（網站服務）搜尋事件：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立Rights Management用戶端API物件

   * 建立 `DocumentSecurityServiceClient` 物件，使用其預設建構函式。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DocumentSecurityServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 指定要搜尋的事件

   * 建立 `EventSpec` 物件，使用其建構子。
   * 透過設定 `EventSpec` 物件 `firstTime.date` 資料成員 `DataTime` 代表事件發生日期範圍開始的例項。
   * 指派值 `true` 到 `EventSpec` 物件 `firstTime.dateSpecified` 資料成員。
   * 透過設定 `EventSpec` 物件 `lastTime.date` 資料成員 `DataTime` 代表事件發生日期範圍結尾的例項。
   * 指派值 `true` 到 `EventSpec` 物件 `lastTime.dateSpecified` 資料成員。
   * 將字串值指派給 `EventSpec` 物件 `eventCode` 資料成員。 下表列出您可指派給此屬性的數值：

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

1. 搜尋事件

   叫用 `DocumentSecurityServiceClient` 物件 `searchForEvents` 方法和傳遞 `EventSpec` 代表要搜尋的事件和結果數上限的物件。 此方法會傳回 `MyArrayOf_xsd_anyType` 其中每個元素都是 `AuditSpec` 例項。 使用 `AuditSpec` 例項，您可以取得事件的相關資訊，例如發生的時間。 此 `AuditSpec` 例項包含 `timestamp` 指定此資訊的資料成員。

**程式碼範例**

如需使用Rights Management服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM):使用Web服務API搜索事件」
* 「快速入門(SwaRef):使用Web服務API搜索事件」

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 對Word文檔應用策略 {#applying-policies-to-word-documents}

除PDF文檔外，權限管理服務還支援其他文檔格式，如Microsoft Word文檔（DOC檔案）和其他Micosoft Office檔案格式。 例如，您可以將策略應用於Word文檔以保護它。 通過將策略應用於Word文檔，可以限制對文檔的訪問。 如果文檔已使用策略進行了保護，則無法將策略應用到文檔。

在分發受策略保護的Word文檔後，可以監視其使用情況。 也就是說，您可以看到檔案的使用方式，以及使用者。 例如，您可以找出有人何時開啟檔案。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-11}

要將策略應用於Word文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security用戶端API物件。
1. 檢索應用策略的Word文檔。
1. 將現有策略應用於Word文檔。
1. 保存受策略保護的Word文檔。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Document Security Client API對象**

在以寫程式方式執行Document Security服務操作之前，必須建立Document Security服務客戶端對象。

**檢索Word文檔**

必須檢索Word文檔才能應用策略。 將策略應用到Word文檔後，在使用該文檔時，用戶將受到限制。 例如，如果策略不允許離線時開啟文檔，則用戶必須聯機才能開啟文檔。

**將現有策略應用於Word文檔**

要將策略應用於Word文檔，必須引用現有策略並指定該策略所屬的策略集。 設定連接屬性的用戶必須具有對指定策略的訪問權限。 否則會發生例外。

**保存Word文檔**

在Document Security服務將策略應用於Word文檔後，可以將受策略保護的Word文檔另存為DOC檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[撤消對文檔的訪問](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API將策略應用到Word文檔 {#apply-a-policy-to-a-word-document-using-the-java-api}

使用Document Security API(Java)將策略應用到Word文檔：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security用戶端API物件。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DocumentSecurityClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 檢索Word文檔。

   * 建立 `java.io.FileInputStream` 使用其建構子並傳遞指定Word文檔位置的字串值來表示Word文檔的對象。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 將現有策略應用於Word文檔。

   * 建立 `DocumentManager` 對象，方法是調用 `DocumentSecurityClient` 物件 `getDocumentManager` 方法。
   * 通過調用 `DocumentManager` 物件 `protectDocument` 方法並傳遞下列值：

      * 此 `com.adobe.idp.Document` 包含策略應用到的Word文檔的對象。
      * 指定文檔名稱的字串值。
      * 一個字串值，它指定策略所屬的策略集的名稱。 您可以指定 `null` 產生 `MyPolicies` 正在使用的策略集。
      * 指定策略名稱的字串值。
      * 一個字串值，它表示作為文檔發佈者的用戶的用戶管理域的名稱。 此參數值為可選值，可為null（如果此參數為null，則下一個參數值必須為null）。
      * 一個字串值，它表示作為文檔發佈者的用戶管理器用戶的規範名稱的名稱。 此參數值為選用值，可以是 `null` (如果此參數為 `null`，則上一個參數值必須是 `null`)。
      * A `com.adobe.livecycle.rightsmanagement.Locale` 表示用於選擇MS Office模板的區域設定。 此參數值為選用值，您可以指定 `null`.

      此 `protectDocument` 方法傳回 `RMSecureDocumentResult` 包含受策略保護的Word文檔的對象。


1. 保存Word文檔。

   * 叫用 `RMSecureDocumentResult` 物件 `getProtectedDoc` 獲取受策略保護的Word文檔的方法。 此方法會傳回 `com.adobe.idp.Document` 物件。
   * 建立 `java.io.File` 對象，並確保檔案副檔名為DOC。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 複製內容的方法 `Document` 物件(請確定您使用 `Document` 由傳回的物件 `getProtectedDoc` 方法)。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* &quot;快速入門（SOAP模式）:使用Java API將策略應用到Word文檔」

### 使用Web服務API將策略應用到Word文檔 {#apply-a-policy-to-a-word-document-using-the-web-service-api}

使用Document Security API（web服務）將策略應用到Word文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立Document Security用戶端API物件。

   * 建立 `DocumentSecurityServiceClient` 物件，使用其預設建構函式。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DocumentSecurityServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 檢索Word文檔。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存應用策略的Word文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示Word文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 透過取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 位元組陣列內容的欄位。

1. 將現有策略應用於Word文檔。

   通過調用 `DocumentSecurityServiceClient` 物件 `protectDocument` 方法並傳遞下列值：

   * 此 `BLOB` 包含策略應用到的Word文檔的對象。
   * 指定文檔名稱的字串值。
   * 一個字串值，它指定策略所屬的策略集的名稱。 您可以指定 `null` 產生 `MyPolicies` 正在使用的策略集。
   * 指定策略名稱的字串值。
   * 一個字串值，它表示作為文檔發佈者的用戶的用戶管理域的名稱。 此參數值為選用值，且可為null(如果此參數為null，則下一個參數值必須為 `null`)。
   * 一個字串值，它表示作為文檔發佈者的用戶管理器用戶的規範名稱的名稱。 此參數值為選用值，且可為null(如果此參數為null，則上一個參數值必須為 `null`)。
   * A `RMLocale` 指定地區設定值的值(例如 `RMLocale.en`)。
   * 用於儲存策略標識符值的字串輸出參數。
   * 用於儲存受策略保護的標識符值的字串輸出參數。
   * 用於儲存mime類型的字串輸出參數(例如， `application/doc`)。

   此 `protectDocument` 方法傳回 `BLOB` 包含受策略保護的Word文檔的對象。

1. 保存Word文檔。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示受策略保護的Word文檔的檔案位置。
   * 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `protectDocument` 方法。 取得 `BLOB` 物件 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* 「快速入門(MTOM):使用Web服務API將策略應用到Word文檔「

## 從Word文檔中刪除策略 {#removing-policies-from-word-documents}

可以從受策略保護的Word文檔中刪除策略，以便從文檔中刪除安全性。 也就是說，如果您不再希望該文檔受策略保護。 如果要使用較新的策略更新受策略保護的Word文檔，則切換該策略比刪除該策略和添加更新的策略更有效。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-12}

要從受策略保護的Word文檔中刪除策略，請執行以下步驟：

1. 包含項目檔案
1. 建立Document Security用戶端API物件。
1. 檢索受策略保護的Word文檔。
1. 從Word文檔中刪除策略。
1. 保存不安全的Word文檔。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Document Security用戶端API物件**

在以寫程式方式執行Document Security服務操作之前，請建立Document Security服務客戶端對象。

**檢索受策略保護的Word文檔**

必須檢索受策略保護的Word文檔才能刪除策略。 如果嘗試從未受策略保護的Word文檔中刪除策略，將導致異常。

**從Word文檔中刪除策略**

如果在連接設定中指定了管理員，則可以從受策略保護的Word文檔中刪除策略。 否則，用於保護文檔的策略必須包含 `SWITCH_POLICY` 從Word文檔中刪除策略的權限。 此外，在AEM Forms連線設定中指定的使用者也必須擁有該權限。 否則，會擲回例外。

**保存不安全的Word文檔**

在Document Security服務從Word文檔中刪除策略後，可以將不安全的Word文檔另存為DOC檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[對Word文檔應用策略](protecting-documents-policies.md#applying-policies-to-word-documents)

### 使用Java API從Word文檔中刪除策略 {#remove-a-policy-from-a-word-document-using-the-java-api}

使用Document Security API(Java)從受策略保護的Word文檔中刪除策略：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security用戶端API物件

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `RightsManagementClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 檢索受策略保護的Word文檔

   * 建立 `java.io.FileInputStream` 表示受策略保護的Word文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定Word文檔的位置。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 從Word文檔中刪除策略

   * 建立 `DocumentManager` 對象，方法是調用 `RightsManagementClient` 物件 `getDocumentManager` 方法。
   * 通過調用 `DocumentManager` 物件 `removeSecurity` 方法和傳遞 `com.adobe.idp.Document` 包含受策略保護的Word文檔的對象。 此方法會傳回 `com.adobe.idp.Document` 包含不安全Word文檔的對象。

1. 保存不安全的Word文檔

   * 建立 `java.io.File` 對象，並確保檔案副檔名為DOC。
   * 叫用 `Document` 物件 `copyToFile` 複製內容的方法 `Document` 物件(請確定您使用 `Document` 由傳回的物件 `removeSecurity` 方法)。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* &quot;快速入門（SOAP模式）:使用Java API從Word文檔中刪除策略「

### 使用Web服務API從Word文檔中刪除策略 {#remove-a-policy-from-a-word-document-using-the-web-service-api}

使用Document Security API（Web服務）從受策略保護的Word文檔中刪除策略：

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立Document Security用戶端API物件

   * 建立 `RightsManagementServiceClient` 物件，使用其預設建構函式。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `RightsManagementServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 檢索受策略保護的Word文檔

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存從中刪除策略的受策略保護的Word文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示Word文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 位元組陣列內容的欄位。

1. 從Word文檔中刪除策略

   調用 `RightsManagementServiceClient` 物件 `removePolicySecurity` 方法和傳遞 `BLOB` 包含受策略保護的Word文檔的對象。 此方法會傳回 `BLOB` 包含不安全Word文檔的對象。

1. 保存不安全的Word文檔

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示不安全Word文檔的檔案位置。
   * 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `removePolicySecurity` 方法。 取得 `BLOB` 物件 `MTOM` 欄位。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。

**程式碼範例**

有關使用Document Security服務的代碼示例，請參閱以下快速入門：

* 「快速入門(MTOM):使用Web服務API從Word文檔中刪除策略」

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
