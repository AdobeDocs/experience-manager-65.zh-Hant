---
title: 使用原則保護檔案
seo-title: 使用原則保護檔案
description: 'null'
seo-description: 'null'
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# 使用原則保護檔案 {#protecting-documents-with-policies}

**關於Document Security Service**

Document security服務可讓使用者動態地將機密設定套用至Adobe PDF檔案，而且不論檔案的散布範圍有多廣，都能保有檔案的控制權。

Document Security服務可讓使用者控制收件者使用受原則保護PDF檔案的方式，防止資訊擴散到使用者的觸及範圍以外。 使用者可以指定誰可以開啟檔案、限制其使用方式，以及在檔案發佈後監控檔案。 使用者也可以動態控制對受原則保護檔案的存取，甚至可以動態撤銷對檔案的存取。

Document Security服務也可保護其他檔案類型，例如Microsoft Word檔案（DOC檔案）。 您可以使用Document Security Client API來處理這些檔案類型。 支援下列版本：

* Microsoft Office 2003檔案（DOC、XLS、PPT檔案）
* Microsoft Office 2007檔案（DOCX、XLSX、PPTX檔案）
* PTC Pro/E檔案

為避免疑義，以下兩節將討論如何使用Word檔案：

* [將原則套用至Word檔案](protecting-documents-policies.md#applying-policies-to-word-documents)
* [從Word檔案移除原則](protecting-documents-policies.md#removing-policies-from-word-documents)

您可以使用Document Security服務完成下列工作：

* 建立原則。 有關資訊，請參 [閱建立策略](protecting-documents-policies.md#creating-policies)。
* 修改策略。 有關資訊，請參 [閱修改策略](protecting-documents-policies.md#modifying-policies)。
* 刪除原則。 有關資訊，請參 [閱刪除策略](protecting-documents-policies.md#deleting-policies)。
* 套用原則至PDF檔案。 如需詳細資訊，請 [參閱套用原則至PDF檔案](protecting-documents-policies.md#applying-policies-to-pdf-documents)。
* 從PDF檔案移除原則。 如需詳細資訊，請 [參閱從PDF檔案移除原則](protecting-documents-policies.md#removing-policies-from-pdf-documents)。
* 檢查受原則保護的檔案。 如需詳細資訊，請參 [閱檢查受原則保護的PDF檔案](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)。
* 撤銷PDF檔案的存取權。 如需詳細資訊，請 [參閱廢止檔案存取權](protecting-documents-policies.md#revoking-access-to-documents)。
* 恢復對已撤銷文檔的訪問。 有關資訊，請參 [閱恢復對已撤銷文檔的訪問](protecting-documents-policies.md#reinstating-access-to-revoked-documents)。
* 建立浮水印。 如需詳細資訊，請參 [閱建立浮水印](protecting-documents-policies.md#creating-watermarks)。
* 搜尋事件。 如需詳細資訊，請 [參閱搜尋事件](protecting-documents-policies.md#searching-for-events)。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

## 建立策略 {#creating-policies}

您可以使用Document Security Java API或web service API，以程式設計方式建立原則。 原 *則* 是包含檔案安全性設定、授權使用者和使用權限的資訊集合。 您可以使用適合不同情況和使用者的安全性設定，來建立和儲存任何數量的原則。

策略允許您執行以下任務：

* 指定可開啟檔案的個人。 收件者可以屬於您的組織，也可以是您組織外部的。
* 指定收件者如何使用檔案。 您可以限制存取不同的Acrobat和Adobe Reader功能。 這些功能包括列印和複製文字、新增簽名，以及在檔案中新增註解的功能。
* 隨時變更存取權與安全性設定，即使在您散發受原則保護的檔案後亦然。
* 在您散發檔案後，請監控檔案的使用情況。 您可以看到檔案的使用方式以及使用者。 例如，您可以瞭解某人何時開啟檔案。

### 使用web services建立原則 {#creating-a-policy-using-web-services}

使用web service API建立原則時，請參考描述該原則的現有可攜式檔案權限語言(PDRL)XML檔案。 策略權限和承擔者在PDRL文檔中定義。 以下XML文檔是PDRL文檔的示例。

```as3
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
>如需Document Security服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要建立策略，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 設定原則的屬性。
1. 建立策略條目。
1. 註冊原則。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-rightsmanagement-client.jar
* namespace.jar（如果AEM Forms部署在JBoss上）
* jaxb-api.jar（如果AEM Forms部署在JBoss上）
* jaxb-impl.jar（如果AEM Forms部署在JBoss上）
* jaxb-libs.jar（如果AEM Forms部署在JBoss上）
* jaxb-xjc.jar（如果AEM Forms部署在JBoss上）
* relanchingDatatype.jar（如果AEM Forms部署在JBoss上）
* xsdlib.jar（如果AEM Forms部署在JBoss上）
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar（如果AEM Forms未部署在JBoss上，請使用不同的JAR檔案）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立Document Security Client API物件**

在以程式設計方式執行Document Security服務操作之前，請先建立Document Security服務用戶端物件。

**設定原則的屬性**

要建立策略，請設定策略屬性。 強制屬性是策略名稱。 每個策略集的策略名稱必須是唯一的。 策略集只是策略的集合。 如果策略屬於不同的策略集，則可能有兩個具有相同名稱的策略。 但是，單個策略集中的兩個策略不能具有相同的策略名稱。

另一個要設定的實用屬性是有效期。 有效期是授權收件人可存取受原則保護檔案的時段。 如果未設定此屬性，則策略始終有效。

有效期間可設為下列其中一個選項：

* 從發佈檔案開始，檔案可存取的固定天數
* 文檔無法訪問的結束日期
* 可存取檔案的特定日期範圍
* 始終有效

您只能指定開始日期，這會導致原則在開始日期之後有效。 如果您只指定結束日期，則原則在結束日期之前有效。 但是，如果未定義開始日期和結束日期，則會引發例外。

設定屬於策略的屬性時，還可以設定加密設定。 這些加密設定會在原則套用至檔案時生效。 您可以指定下列加密值：

* **AES256**:表示使用256位元金鑰的AES加密演算法。
* **AES128**:以128位元金鑰表示AES加密演算法。
* **** 無加密：不表示加密。

指定選 `NoEncryption` 項時，不能將選 `PlaintextMetadata` 項設定為 `false`。 如果您嘗試這麼做，則會擲回例外。

>[!NOTE]
>
>如需您可設定之其他屬性的詳細資訊，請參閱 `Policy` 「 [AEM Forms API參考」中的介面說明](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**建立策略條目**

策略條目會將承擔者（即組和用戶）和權限附加到策略。 策略至少必須有一個策略條目。 例如，假設您執行下列工作：

* 建立並註冊原則項目，讓群組只能線上上檢視檔案，並禁止收件者複製檔案。
* 將策略條目附加到策略。
* 使用Acrobat以原則保護檔案。

這些動作會導致收件者只能線上檢視檔案，而無法複製檔案。 在檔案移除安全性之前，檔案仍保有安全性。

**註冊原則**

必須先註冊新策略，才能使用新策略。 在註冊原則後，您就可以使用它來保護檔案。

### 使用Java API建立原則 {#create-a-policy-using-the-java-api}

使用Document Security API(Java)建立原則：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `DocumentSecurityClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 設定原則的屬性。

   * 調用 `Policy` 物件的靜態方 `InfomodelObjectFactory` 法來建立物 `createPolicy` 件。 此方法返回對 `Policy` 像。
   * 調用物件的方法並傳遞指定原則名 `Policy` 稱的字串值， `setName` 以設定原則的名稱屬性。
   * 調用物件的方法並傳 `Policy` 遞指定原則 `setDescription` 說明的字串值，以設定原則的說明。
   * 通過調用對象的方法並傳遞指定策略集名 `Policy` 稱的字 `setPolicySetName` 符串值，設定新策略所屬的策略集。 (可以為此 `null` 參數值指定，這會導致將策略添加到「我的策 *略* 」策略集。)
   * 調用物件的靜態方法，以建立 `InfomodelObjectFactory` 原則的有效 `createValidityPeriod` 期。 此方法返回對 `ValidityPeriod` 像。
   * 調用物件的方法，並傳遞指定天數的整數值，以設定受原則保護 `ValidityPeriod` 檔案 `setRelativeExpirationDays` 可存取的天數。
   * 調用物件的方法並傳遞物件，以 `Policy` 設定原則的 `setValidityPeriod` 有效期 `ValidityPeriod` 間。

1. 建立策略條目。

   * 調用物件的靜態方 `InfomodelObjectFactory` 法以建立原則 `createPolicyEntry` 項目。 此方法返回對 `PolicyEntry` 像。
   * 呼叫物件的靜態方法，以指 `InfomodelObjectFactory` 定原則的權 `createPermission` 限。 傳遞屬於表示權限的介面 `Permission` 的靜態資料成員。 此方法返回對 `Permission` 像。 例如，若要新增允許使用者從受原則保護的PDF檔案複製資料的權限，請傳遞 `Permission.COPY`。 （對要添加的每個權限重複此步驟）。
   * 調用物件的方法並傳遞物件，將權 `PolicyEntry` 限新增 `addPermission` 至原則項 `Permission` 目。 (請對您建立的每個 `Permission` 物件重複此步驟)。
   * 調用物件的靜態方 `InfomodelObjectFactory` 法，以建立原則主 `createSpecialPrincipal` 體。 傳遞屬於表示承擔者 `InfomodelObjectFactory` 的對象的資料成員。 此方法返回對 `Principal` 像。 例如，要將文檔的發佈者添加為承擔者，請通過 `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`。
   * 調用物件的方法並傳遞物件，將承擔者 `PolicyEntry` 新增 `setPrincipal`至原則項目 `Principal` 中。
   * 調用物件的方法並傳遞物件，將原 `Policy` 則項目新 `addPolicyEntry` 增至原 `PolicyEntry` 則。

1. 註冊原則。

   * 調用 `PolicyManager` 物件的方 `DocumentSecurityClient` 法以建立物 `getPolicyManager` 件。
   * 呼叫物件的方法並傳 `PolicyManager` 遞下列值， `registerPolicy` 以註冊原則：

      * 代 `Policy` 表要註冊的策略的對象。
   * 一個字串值，它表示策略所屬的策略集。
   如果您在連線設定中使用AEM Forms管理員帳戶來建立物 `DocumentSecurityClient` 件，請在呼叫方法時指定原則集名 `registerPolicy` 稱。 如果為策略集 `null` 傳遞值，則會在管理員「我的策略」策略集 *中建立策略* 。

   如果您在連線設定中使用Document Security使用者，則可以叫用只接受原則 `registerPolicy` 的多載方法。 也就是說，您不需要指定原則集名稱。 但是，策略將添加到名為「我的策略」的 *策略集中*。 如果不想將新策略添加到此策略集，則在調用該方法時指定策略集名 `registerPolicy` 稱。

   >[!NOTE]
   >
   >建立策略時，請參考現有策略集。 如果指定不存在的策略集，則會拋出異常。

如需使用Document Security服務的程式碼範例，請參閱下列：

* &quot;快速啟動（SOAP模式）:使用Java API建立原則」

### 使用web service API建立原則 {#create-a-policy-using-the-web-service-api}

使用Document Security API(web service)建立原則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Document Security Client API物件。

   * 使用其 `DocumentSecurityServiceClient` 預設建構函式建立物件。
   * 使用建 `DocumentSecurityServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `RightsManagementServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。


1. 設定原則的屬性。

   * 使用其 `PolicySpec` 建構函式建立物件。
   * 為物件的資料成員指派字串值，以設 `PolicySpec` 定原則的 `name` 名稱。
   * 將字串值指派給物件的資料成員，以設定 `PolicySpec` 原則的 `description` 說明。
   * 為物件的資料成員指派字串值，以設定原則所屬的 `PolicySpec` 原則 `policySetName` 集。 必須指定現有策略集名稱。 (您可以為 `null` 此參數值指定，使策略被添加到「我的 *策略*」)。
   * 將整數值指派給物件的資料成員，以設定原則的離 `PolicySpec` 線租用 `offlineLeasePeriod` 期間。
   * 使用表 `PolicySpec` 示PDRL XML資料 `policyXml` 的字串值來設定物件的資料成員。 要執行此任務，請使用。NET對 `StreamReader` 像的建構子建立。 將表示策略的PDRL XML檔案的位置傳遞給建構子 `StreamReader` 。 接著，叫用 `StreamReader` 物件的方 `ReadLine` 法，並將傳回值指派給字串變數。 重複該對 `StreamReader` 像，直到 `ReadLine` 方法返回null。 將字串變數指派給 `PolicySpec` 物件的資 `policyXml` 料成員。

1. 建立策略條目。

   使用Document Security web service API建立原則時，不需要建立原則項目。 策略條目在PDRL文檔中定義。

1. 註冊原則。

   呼叫物件的方法並傳 `DocumentSecurityServiceClient` 遞下列值， `registerPolicy` 以註冊原則：

   * 代 `PolicySpec` 表要註冊的策略的對象。
   * 一個字串值，它表示策略所屬的策略集。 您可以指定 `null` 導致策略被添加到 ** MyPolices策略集的值。
   如果您在連線設定中使用AEM Forms管理員帳戶來建立物 `DocumentSecurityClient` 件，請在呼叫方法時指定原則集 `registerPolicy` 名稱。

   如果您在連線設定中使用Document SecurityDocument Security使用者，則可以叫用只接受原則 `registerPolicy` 的多載方法。 也就是說，您不需要指定原則集名稱。 但是，策略將添加到名為「我的策略」的 *策略集中*。 如果不想將新策略添加到此策略集，則在調用該方法時指定策略集名 `registerPolicy` 稱。

   >[!NOTE]
   >
   >建立策略並指定策略集時，請確保指定現有策略集。 如果指定不存在的策略集，則會拋出異常。

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM):使用web service API建立原則」
* 「快速入門(SwaRef):使用web service API建立原則」

## 修改策略 {#modifying-policies}

您可以使用Document Security Java API或web service API修改現有原則。 要更改現有策略，請檢索該策略、修改該策略，然後更新伺服器上的策略。 例如，假設您檢索現有策略並延長其有效期。 在更改生效之前，您必須更新策略。

當業務需求變更且政策不再反映這些需求時，您可以修改政策。 您不必建立新策略，只需更新現有策略即可。

要使用Web服務修改策略屬性（例如，使用使用JAX-WS建立的Java代理類），必須確保策略已向Document Security服務註冊。 然後，可以使用方法引用現有策略， `PolicySpec.getPolicyXml` 並使用適用的方法修改策略屬性。 例如，您可以叫用方法來修改離線租用 `PolicySpec.setOfflineLeasePeriod` 期間。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要修改現有策略，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 檢索現有策略。
1. 更改策略屬性。
1. 更新原則。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Document Security Client API物件**

在以程式設計方式執行Document Securityservice作業之前，您必須先建立Document Security服務用戶端物件。 如果您使用Java API，請建立物 `RightsManagementClient` 件。 如果您使用Document Security web service API，請建立物 `RightsManagementServiceService` 件。

**檢索現有策略**

您必須檢索現有策略才能對其進行修改。 要檢索策略，請指定策略名稱和策略所屬的策略集。 如果為策略 `null` 集名稱指定值，則會從「我的策略」策 ** 略集檢索策略。

**設定原則的屬性**

要修改策略，請修改策略屬性的值。 唯一不能更改的策略屬性是name屬性。 例如，若要變更原則的離線租用期間，您可以修改原則的離線租用期間屬性值。

使用web service修改原則的離線租用期間時，介 `offlineLeasePeriod` 面上的欄 `PolicySpec` 位會被忽略。 要更新離線租用期間，請修改PDRL `OfflineLeasePeriod` XML文檔中的元素。 然後，使用介面的資料成員，參考更 `PolicySpec` 新的PDRL `policyXML` XML檔案。

>[!NOTE]
>
>如需您可設定之其他屬性的詳細資訊，請參閱 `Policy` 「 [AEM Forms API參考」中的介面說明](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**更新原則**

在您對原則所做的變更生效之前，您必須使用Document Security服務更新原則。 在下次將受原則保護的檔案與Document Security服務同步時，會更新保護檔案的原則變更。

### 使用Java API修改現有策略 {#modify-existing-policies-using-the-java-api}

使用Document Security API(Java)修改現有原則：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `RightsManagementClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 檢索現有策略。

   * 調用 `PolicyManager` 物件的方 `RightsManagementClient` 法以建立物 `getPolicyManager` 件。
   * 建立 `Policy` 代表要更新之原則的物件，方法 `PolicyManager` 是叫用物 `getPolicy` 件的方法並傳遞下列值。」

      * 一個字串值，它表示策略所屬的策略集名稱。 您可以指 `null` 定導致使用 `MyPolicies` 策略集的結果。
      * 代表原則名稱的字串值。

1. 設定原則的屬性。

   變更政策屬性以符合您的業務需求。 例如，若要變更原則的離線租用期間，請叫 `Policy` 用物件的方 `setOfflineLeasePeriod` 法。

1. 更新原則。

   調用物件的方 `PolicyManager` 法以更新原 `updatePolicy` 則。 傳遞代 `Policy` 表要更新的策略的對象。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱快速啟動（SOAP模式）:使用Java API部分修改策略。

### 使用web service API修改現有策略 {#modify-existing-policies-using-the-web-service-api}

使用Document Security API(web service)修改現有原則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Document Security Client API物件。

   * 使用其 `RightsManagementServiceClient` 預設建構函式建立物件。
   * 使用建 `RightsManagementServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `RightsManagementServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。


1. 檢索現有策略。

   通過調 `PolicySpec` 用對象的方法並傳遞以下值，建立表示要修 `RightsManagementServiceClient` 改的 `getPolicy` 策略的對象：

   * 一個字串值，它指定策略所屬的策略集名稱。 您可以指 `null` 定導致使用 `MyPolicies` 策略集的結果。
   * 指定策略名稱的字串值。

1. 設定原則的屬性。

   變更政策屬性以符合您的業務需求。

1. 更新原則。

   調用物件的方 `RightsManagementServiceClient` 法並傳遞 `updatePolicyFromSDK` 代表要更 `PolicySpec` 新之原則的物件，以更新原則。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM):使用web service API修改原則&quot;
* 「快速入門(SwaRef):使用web service API修改原則&quot;

## 刪除策略 {#deleting-policies}

您可以使用Document Security Java API或web service API刪除現有原則。 刪除原則後，便無法再用來保護檔案。 不過，使用原則的現有受原則保護檔案仍受到保護。 當有較新的策略可用時，可以刪除策略。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

要刪除現有策略，請執行以下步驟：

1. 包含專案檔案
1. 建立Document Security Client API物件。
1. 刪除原則。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Document Security Client API物件**

您必須先建立Document Security服務用戶端物件，才能以程式設計方式執行Document Security服務作業。 如果您使用Java API，請建立物 `RightsManagementClient` 件。 如果您使用Document Security web service API，請建立物 `RightsManagementServiceService` 件。

**刪除原則**

要刪除策略，請指定要刪除的策略和策略所屬的策略集。 使用其設定來叫用AEM Forms的使用者必須擁有刪除原則的權限；否則會發生異常。 同樣地，如果您嘗試刪除不存在的策略，則會出現例外。

### 使用Java API刪除原則 {#delete-policies-using-the-java-api}

使用Document Security API(Java)刪除原則：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `RightsManagementClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 刪除原則。

   * 調用 `PolicyManager` 物件的方 `RightsManagementClient` 法以建立物 `getPolicyManager` 件。
   * 叫用物件的方 `PolicyManager` 法並傳 `deletePolicy` 遞下列值，以刪除原則：

      * 一個字串值，它指定策略所屬的策略集名稱。 您可以指 `null` 定導致使用 `MyPolicies` 策略集的結果。
      * 一個字串值，它指定要刪除的策略的名稱。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* &quot;快速啟動（SOAP模式）:使用Java API刪除策略」

### 使用web service API刪除原則 {#delete-policies-using-the-web-service-api}

使用Document Security API(web service)刪除原則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Document Security Client API物件。

   * 使用其 `RightsManagementServiceClient` 預設建構函式建立物件。
   * 使用建 `RightsManagementServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `RightsManagementServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。


1. 刪除原則。

   調用物件的方法並傳 `RightsManagementServiceClient` 遞下列值， `deletePolicy` 以刪除原則：

   * 一個字串值，它指定策略所屬的策略集名稱。 您可以指 `null` 定導致使用 `MyPolicies` 策略集的結果。
   * 一個字串值，它指定要刪除的策略的名稱。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM):使用web service API刪除策略&quot;
* 「快速入門(SwaRef):使用web service API刪除策略&quot;

## 套用原則至PDF檔案 {#applying-policies-to-pdf-documents}

您可以套用原則至PDF檔案，以保護檔案的安全。 將原則套用至PDF檔案，即可限制對檔案的存取。 如果文檔已使用策略保護，則不能將策略應用於文檔。

當檔案開啟時，您也可以限制對Acrobat和Adobe Reader功能的存取，包括列印和複製文字、進行變更，以及在檔案中新增簽名和註解的功能。 此外，當您不再希望使用者存取受原則保護的PDF檔案時，也可以撤銷該檔案。

在分發受原則保護的檔案後，您可以監控檔案的使用情況。 也就是說，您可以看到檔案的使用方式以及使用者。 例如，您可以瞭解某人何時開啟檔案。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-3}

若要將原則套用至PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 擷取套用原則的PDF檔案。
1. 將現有原則套用至PDF檔案。
1. 儲存受原則保護的PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Document Security用戶端API物件**

在以程式設計方式執行Document Security服務操作之前，請先建立Document Security服務用戶端物件。 如果您使用Java API，請建立物 `DocumentSecurityClient` 件。 如果您使用Document Security web service API，請建立物 `DocumentSecurityServiceService` 件。

**擷取PDF檔案**

您可以擷取PDF檔案以套用原則。 將原則套用至PDF檔案後，使用者在使用檔案時會受到限制。 例如，如果原則未讓檔案在離線時開啟，則使用者必須線上上才能開啟檔案。

**將現有原則套用至PDF檔案**

若要將原則套用至PDF檔案，請參考現有原則並指定原則所屬的原則集。 設定連接屬性的用戶必須有權訪問指定的策略。 否則，會發生例外。

**儲存PDF檔案**

在Document Security服務將原則套用至PDF檔案後，您就可以將受原則保護的PDF檔案儲存為PDF檔案。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[廢止檔案存取權](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API將原則套用至PDF檔案 {#apply-a-policy-to-a-pdf-document-using-the-java-api}

使用Document Security API(Java)將原則套用至PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `RightsManagementClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 擷取PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式建立代表PDF檔案的物件。 傳遞指定PDF檔案位置的字串值。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 將現有原則套用至PDF檔案。

   * 調用 `DocumentManager` 物件的方 `RightsManagementClient` 法以建立物 `getDocumentManager` 件。
   * 調用物件的方法並傳遞下列值，以套 `DocumentManager` 用原則 `protectDocument` 至PDF檔案：

      * 包 `com.adobe.idp.Document` 含套用原則之PDF檔案的物件。
      * 指定文檔名稱的字串值。
      * 一個字串值，它指定策略所屬的策略集的名稱。 您可以指定 `null` 導致使用策略 `MyPolicies` 集的值。
      * 指定策略名稱的字串值。
      * 一個字串值，它表示作為文檔發佈者的用戶的用戶管理域的名稱。 此參數值是可選的，可以是null（如果此參數為null，則下一個參數值必須為null）。
      * 一個字串值，它表示作為文檔發佈者的用戶管理器用戶的標準名稱的名稱。 此參數值是可選的，可 `null` 以是(如果此參數為null，則上一個參數值必須 `null`是)。
      * 表 `com.adobe.livecycle.rightsmanagement.Locale` 示用於選擇MS office模板的區域設定。 此參數值是可選的，不用於PDF文檔。 若要保護PDF檔案，請指定 `null`。
      此方 `protectDocument` 法會傳回包 `RMSecureDocumentResult` 含受原則保護PDF檔案的物件。


1. 儲存PDF檔案。

   * 叫用物 `RMSecureDocumentResult` 件的方 `getProtectedDoc` 法以取得受原則保護的PDF檔案。 此方法返回對 `com.adobe.idp.Document` 像。
   * 建立物 `java.io.File` 件，並確定副檔名為PDF。
   * 叫用 `com.adobe.idp.Document` 物件的方 `copyToFile` 法，將物件的內容複製至檔案(請確定您使用 `Document` 由方法傳回的物 `Document``getProtectedDoc` 件)。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* &quot;快速啟動（EJB模式）:使用Java API將原則套用至PDF檔案」
* &quot;快速啟動（SOAP模式）:使用Java API將原則套用至PDF檔案」

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API將原則套用至PDF檔案 {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

使用Document Security API(web service)將原則套用至PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Document Security Client API物件。

   * 使用其 `RightsManagementServiceClient` 預設建構函式建立物件。
   * 使用建 `RightsManagementServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `RightsManagementServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。


1. 擷取PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。 對 `BLOB` 像用於儲存應用策略的PDF文檔。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 透過取得物件的屬性，來 `System.IO.FileStream` 判斷位元組陣列 `Length` 大小。
   * 調用物件的方法，以串流資料填 `System.IO.FileStream` 入位元組 `Read` 陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 將現有原則套用至PDF檔案。

   調用物件的方法並傳遞下列值，以套 `RightsManagementServiceClient` 用原則 `protectDocument` 至PDF檔案：

   * 包 `BLOB` 含套用原則之PDF檔案的物件。
   * 指定文檔名稱的字串值。
   * 一個字串值，它指定策略所屬的策略集的名稱。 您可以指定 `null` 導致使用策略 `MyPolicies` 集的值。
   * 指定策略名稱的字串值。
   * 一個字串值，它表示作為文檔發佈者的用戶的用戶管理域的名稱。 此參數值是可選的，可以是null(如果此參數為null，則下一個參數值必須 `null`為)。
   * 一個字串值，它表示作為文檔發佈者的用戶管理器用戶的標準名稱的名稱。 此參數值是可選的，可以是空值(如果此參數為空值，則上一個參數值必須 `null`為)。
   * 指 `RMLocale` 定地區值(例如 `RMLocale.en`)的值。
   * 用於儲存策略標識符值的字串輸出參數。
   * 用來儲存受原則保護識別碼值的字串輸出參數。
   * 用於儲存MIME類型(例如， `application/pdf`)的字串輸出參數。
   此方 `protectDocument` 法會傳回包 `BLOB` 含受原則保護PDF檔案的物件。

1. 儲存PDF檔案。

   * 叫用 `System.IO.FileStream` 其建構函式並傳遞字串值來建立物件，此字串值代表受原則保護PDF檔案的檔案位置。
   * 建立一個位元組陣列，該陣列儲存由方 `BLOB` 法返回的對象的資料內 `protectDocument` 容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `MTOM` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM):使用web service API將原則套用至PDF檔案」
* 「快速入門(SwaRef):使用web service API將原則套用至PDF檔案」

## 從PDF檔案移除原則 {#removing-policies-from-pdf-documents}

您可以從受原則保護的檔案中移除原則，以便從檔案中移除安全性。 也就是說，如果您不想讓檔案受到原則的保護。 如果您想要使用較新的原則更新受原則保護的檔案，則切換原則會更有效率，而不是移除原則並新增更新的原則。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-4}

若要從受原則保護的PDF檔案移除原則，請執行下列步驟：

1. 包含專案檔案
1. 建立Document Security Client API物件。
1. 擷取受原則保護的PDF檔案。
1. 從PDF檔案移除原則。
1. 儲存不安全的PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Document Security Client API物件**

在以程式設計方式執行Document Security服務操作之前，請先建立Document Security服務用戶端物件。

**擷取受原則保護的PDF檔案**

您可以擷取受原則保護的PDF檔案，以移除原則。 如果您嘗試從未受原則保護的PDF檔案移除原則，將會造成例外。

**從PDF檔案移除原則**

只要在連線設定中指定管理員，您就可以從受原則保護的PDF檔案中移除原則。 否則，用於保護文檔的策略必須包含權 `SWITCH_POLICY` 限，才能從PDF文檔中刪除策略。 此外，在AEM Forms連線設定中指定的使用者也必須擁有該權限。 否則，會拋出異常。

**儲存不安全的PDF檔案**

在Document Security服務從PDF檔案移除原則後，您就可以將不安全的PDF檔案儲存為PDF檔案。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[套用原則至PDF檔案](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API從PDF檔案移除原則 {#remove-a-policy-from-a-pdf-document-using-the-java-api}

使用Document Security API(Java)，從受原則保護的PDF檔案移除原則：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `DocumentSecurityClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 擷取受原則保護的PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，建立代表受原則保護PDF檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 從PDF檔案移除原則。

   * 調用 `DocumentManager` 物件的方 `DocumentSecurityClient` 法以建立物 `getDocumentManager` 件。
   * 叫用物件的方法並傳遞包含受原則保 `DocumentManager` 護的PDF檔案的 `removeSecurity` 物件， `com.adobe.idp.Document` 從PDF檔案中移除原則。 此方法傳回包 `com.adobe.idp.Document` 含不安全PDF檔案的物件。

1. 儲存不安全的PDF檔案。

   * 建立物 `java.io.File` 件，並確定副檔名為PDF。
   * 叫用 `Document` 物件的方 `copyToFile` 法，將物件的內容複製至檔案(請確定您使用 `Document` 由方法傳回的物 `Document``removeSecurity` 件)。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* &quot;快速啟動（SOAP模式）:使用Java API從PDF檔案移除原則」

### 使用web service API移除原則 {#remove-a-policy-using-the-web-service-api}

使用Document Security API(web service)從受原則保護的PDF檔案移除原則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Document Security Client API物件。

   * 使用其 `DocumentSecurityServiceClient` 預設建構函式建立物件。
   * 使用建 `DocumentSecurityServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `DocumentSecurityServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。


1. 擷取受原則保護的PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。 此物 `BLOB` 件用來儲存受原則保護的PDF檔案，從中移除原則。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 從PDF檔案移除原則。

   叫用物件的方法並傳遞包含受原則保 `DocumentSecurityServiceClient` 護的PDF檔案的 `removePolicySecurity` 物件， `BLOB` 從PDF檔案移除原則。 此方法傳回包 `BLOB` 含不安全PDF檔案的物件。

1. 儲存不安全的PDF檔案。

   * 調用 `System.IO.FileStream` 其建構函式並傳遞字串值，以建立物件，此字串值代表不安全PDF檔案的檔案位置。
   * 建立一個位元組陣列，該陣列儲存由方 `BLOB` 法返回的對象的資料內 `removePolicySecurity` 容。 取得物件欄位的值，以填入 `BLOB` 位元組陣 `MTOM` 列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM):使用web service API從PDF檔案移除原則」
* 「快速入門(SwaRef):使用web service API從PDF檔案移除原則」

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 廢止檔案存取權 {#revoking-access-to-documents}

您可以撤銷對受原則保護PDF檔案的存取權，使用者無法存取該檔案的所有副本。 當使用者嘗試開啟已撤銷的PDF檔案時，會將其重新導向至可檢視修訂檔案的指定URL。 必須以程式設計方式指定使用者重新導向的URL。 當您廢止檔案的存取權時，這項變更會在使用者下次透過線上開啟受原則保護的檔案與Document Security服務同步時生效。

廢止檔案存取權的能力提供額外的安全性。 例如，假設有較新版本的檔案可供使用，而您不再希望任何人檢視過時版本。 在這種情況下，對舊文檔的訪問權可以被撤銷，除非恢復訪問權，否則沒有人可以查看該文檔。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-5}

要撤銷受原則保護的檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 擷取受原則保護的PDF檔案。
1. 撤銷受原則保護的檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Document Security Client API物件**

您必須先建立Document Security服務用戶端物件，才能以程式設計方式執行Document Security服務作業。

**擷取受原則保護的PDF檔案**

您必須擷取受原則保護的PDF檔案，才能將其廢止。 您無法撤銷已撤銷或非受原則保護之檔案的檔案。

如果您知道受原則保護檔案的授權識別碼值，則不需要擷取受原則保護的PDF檔案。 不過，在大多數情況下，您必須擷取PDF檔案，才能取得授權識別碼值。

**撤銷受原則保護的檔案**

若要撤銷受原則保護的檔案，請指定受原則保護檔案的授權識別碼。 此外，您還可以指定當使用者嘗試開啟已撤銷的檔案時，可以檢視的檔案URL。 即假設已過時的檔案被撤銷。 當使用者嘗試開啟已撤銷的檔案時，他們會看到已更新的檔案，而非已撤銷的檔案。

>[!NOTE]
>
>如果您嘗試撤銷已撤銷的檔案，則會擲回例外。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[套用原則至PDF檔案](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[恢復對已撤銷文檔的訪問](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### 使用Java API撤銷檔案的存取權 {#revoke-access-to-documents-using-the-java-api}

使用Document Security API(Java)撤銷對受原則保護PDF檔案的存取權：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `DocumentSecurityClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 擷取受原則保護的PDF檔案

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，以建立代表受原則保護PDF檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 撤銷受原則保護的檔案

   * 調用 `DocumentManager` 物件的方 `DocumentSecurityClient` 法以建立物 `getDocumentManager` 件。
   * 叫用物件的方法，以擷取受原則保護檔案的 `DocumentManager` 授權識別 `getLicenseId` 碼值。 傳遞代 `com.adobe.idp.Document` 表受原則保護檔案的物件。 此方法會傳回代表授權識別碼值的字串值。
   * 調用 `LicenseManager` 物件的方 `DocumentSecurityClient` 法以建立物 `getLicenseManager` 件。
   * 調用物件的方法並傳遞下 `LicenseManager` 列值，以撤 `revokeLicense` 銷受原則保護的檔案：

      * 一個字串值，指定受原則保護檔案的授權識別碼值(指定物件方法 `DocumentManager` 的傳回 `getLicenseId` 值)。
      * 介面的靜態資料成 `License` 員，它指定撤銷文檔的原因。 例如，您可以指定 `License.DOCUMENT_REVISED`。
      * 一 `java.net.URL` 個值，它指定修訂文檔所在的位置。 如果您不想將使用者重新導向至其他URL，則可以傳遞 `null`。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* &quot;快速啟動（SOAP模式）:使用Java API廢止檔案」

### 使用web service API撤銷檔案的存取權 {#revoke-access-to-documents-using-the-web-service-api}

使用Document Security API(web service)撤銷對受原則保護PDF檔案的存取權：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Document Security Client API物件

   * 使用其 `DocumentSecurityServiceClient` 預設建構函式建立物件。
   * 使用建 `DocumentSecurityServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `DocumentSecurityServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。


1. 擷取受原則保護的PDF檔案

   * 使用其 `BLOB` 建構函式建立物件。 此物 `BLOB` 件用來儲存已撤銷受原則保護的PDF檔案。
   * 呼叫 `System.IO.FileStream` 其建構函式並傳遞字串值來建立物件，此字串值代表要廢止之受原則保護PDF檔案的檔案位置，以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 撤銷受原則保護的檔案

   * 借由叫用物件的方法並傳遞代表受原則保護 `DocumentSecurityServiceClient` 檔案的物件， `getLicenseID` 擷取受 `BLOB` 原則保護檔案的授權識別碼值。 此方法會傳回代表授權識別碼的字串值。
   * 調用物件的方法並傳遞下 `DocumentSecurityServiceClient` 列值，以撤 `revokeLicense` 銷受原則保護的檔案：

      * 一個字串值，指定受原則保護檔案的授權識別碼值(指定物件方法 `DocumentSecurityServiceService` 的傳回 `getLicenseId` 值)。
      * 枚舉的靜態資料成 `Reason` 員，它指定撤銷文檔的原因。 例如，您可以指定 `Reason.DOCUMENT_REVISED`。
      * 一 `string` 個值，它指定修訂文檔所在的URL位置。 如果您不想將使用者重新導向至其他URL，則可以傳遞 `null`。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM):使用web service API廢止檔案」
* 「快速入門(SwaRef):使用web service API廢止檔案」

**另請參閱**

[從Word檔案移除原則](protecting-documents-policies.md#removing-policies-from-word-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 恢復對已撤銷文檔的訪問 {#reinstating-access-to-revoked-documents}

您可以恢復對已撤銷PDF檔案的存取權，讓使用者可存取已撤銷檔案的所有副本。 當使用者開啟已撤銷的復原檔案時，使用者可以檢視該檔案。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-6}

要恢復對已撤銷的PDF文檔的訪問權，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 擷取已撤銷PDF檔案的授權識別碼。
1. 恢復對已撤銷PDF檔案的存取權。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Document Security Client API物件**

您必須先建立Document Security服務用戶端物件，才能以程式設計方式執行Document Security服務作業。 如果您使用Java API，請建立物 `DocumentSecurityClient` 件。 如果您使用Document Security web service API，請建立物 `DocumentSecurityServiceService` 件。

**擷取已撤銷PDF檔案的授權識別碼**

您必須擷取已撤銷PDF檔案的授權識別碼，才能重新建立已撤銷的PDF檔案。 取得授權識別碼值後，您可以重建已撤銷的檔案。 如果嘗試恢復未撤銷的文檔，將導致異常。

**恢復對已撤銷PDF檔案的存取權**

若要恢復對已撤銷PDF檔案的存取權，您必須指定已撤銷檔案的授權識別碼。 如果您嘗試重新建立未撤銷的PDF檔案存取權，將會造成例外。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[套用原則至PDF檔案](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[廢止檔案存取權](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API恢復對已撤銷文檔的訪問 {#reinstate-access-to-revoked-documents-using-the-java-api}

使用Document Security API(Java)重新建立對已撤銷檔案的存取權：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `DocumentSecurityClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 擷取已撤銷PDF檔案的授權識別碼。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，建立代表已撤銷PDF檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。
   * 調用 `DocumentManager` 物件的方 `DocumentSecurityClient` 法以建立物 `getDocumentManager` 件。
   * 叫用物件的方法並傳遞代表已撤銷檔案的物 `DocumentManager` 件，以擷取已 `getLicenseId` 撤銷 `com.adobe.idp.Document` 檔案的授權識別碼值。 此方法會傳回代表授權識別碼的字串值。

1. 恢復對已撤銷PDF檔案的存取權。

   * 調用 `LicenseManager` 物件的方 `DocumentSecurityClient` 法以建立物 `getLicenseManager` 件。
   * 叫用物件的方法並傳遞已撤銷檔案的授 `LicenseManager` 權識別碼值， `unrevokeLicense` 以重新建立對已撤銷PDF檔案的存取權。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* &quot;快速啟動（SOAP模式）:使用web service API恢復對已撤銷文檔的訪問權&quot;

### 使用Web服務API恢復對已撤銷檔案的存取權 {#reinstate-access-to-revoked-documents-using-the-web-service-api}

使用Document Security API(web service)重新建立對已撤銷檔案的存取權：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Document Security Client API物件。

   * 使用其 `DocumentSecurityServiceClient` 預設建構函式建立物件。
   * 使用建 `DocumentSecurityServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `DocumentSecurityServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。


1. 擷取已撤銷PDF檔案的授權識別碼。

   * 使用其 `BLOB` 建構函式建立物件。 對 `BLOB` 像用於儲存撤消的PDF文檔，恢復其訪問權。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示已撤銷的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 恢復對已撤銷PDF檔案的存取權。

   * 叫用物件的方法並傳遞代表已撤銷檔案的物 `DocumentSecurityServiceClient` 件，以擷取已 `getLicenseID` 撤銷 `BLOB` 檔案的授權識別碼值。 此方法會傳回代表授權識別碼的字串值。
   * 調用物件的方法，並傳遞 `DocumentSecurityServiceClient` 指定已撤銷PDF檔案之授權識別碼值的字串值（傳遞物件方法的傳回值），以重新建立對已撤銷 `unrevokeLicense` PDF檔案的 `DocumentSecurityServiceClient``getLicenseId` 存取。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM):使用web service API恢復對已撤銷文檔的訪問權&quot;
* 「快速入門(SwaRef):使用web service API恢復對已撤銷文檔的訪問權&quot;

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 檢查受原則保護的PDF檔案 {#inspecting-policy-protected-pdf-documents}

您可以使用Document Security Service API（Java和web service）來檢查受原則保護的PDF檔案。 檢查受原則保護的PDF檔案會傳回受原則保護的PDF檔案的相關資訊。 例如，您可以確定用於保護文檔的策略以及保護文檔的日期。

如果您的LiveCycle版本為8.x或舊版，則無法執行此工作。 AEM Forms中新增了檢查受原則保護檔案的支援。 如果您嘗試使用LiveCycle 8.x（或更早版本）檢查受原則保護的檔案，則會擲回例外。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-7}

若要檢查受原則保護的PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 擷取受原則保護的檔案以進行檢查。
1. 取得受原則保護檔案的相關資訊。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Document Security Client API物件**

在以程式設計方式執行Document Security服務操作之前，請先建立Document Security服務用戶端物件。 如果您使用Java API，請建立物 `RightsManagementClient` 件。 如果您使用Document Security web service API，請建立物 `RightsManagementServiceService` 件。

**擷取受原則保護的檔案以進行檢查**

若要檢查受原則保護的檔案，請擷取它。 如果您嘗試檢查未使用策略保護或已撤銷的文檔，則會拋出例外。

**檢查檔案**

擷取受原則保護的檔案後，即可加以檢查。

**取得受原則保護檔案的相關資訊**

在檢查受原則保護的PDF檔案後，您可以取得相關資訊。 例如，您可以決定用於保護檔案的原則。

如果您使用屬於「我的策略」的策略保護文檔，然後調用或 `RMInspectResult.getPolicysetName` ，則 `RMInspectResult.getPolicysetId`返回null。

如果文檔使用包含在策略集（「我的策略」除外）中的策略進行保護，則返回 `RMInspectResult.getPolicysetName` 有效 `RMInspectResult.getPolicysetId` 的字串。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API檢查受原則保護的PDF檔案 {#inspect-policy-protected-pdf-documents-using-the-java-api}

使用Document Security Service API(Java)檢查受原則保護的PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。 如需這些檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 建立Document Security Client API物件。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。 (請參 [閱設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 使用其 `RightsManagementClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 擷取受原則保護的檔案以進行檢查。

   * 使用 `java.io.FileInputStream` 其建構函式建立代表受原則保護PDF檔案的物件。 傳遞指定PDF檔案位置的字串值。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 檢查檔案。

   * 調用 `DocumentManager` 物件的方 `RightsManagementClient` 法以建立物 `getDocumentManager` 件。
   * 調用物件的方法，以檢查受原 `LicenseManager` 則保護的 `inspectDocument` 檔案。 傳遞包 `com.adobe.idp.Document` 含受原則保護PDF檔案的物件。 此方法傳回 `RMInspectResult` 包含受原則保護檔案資訊的物件。

1. 取得受原則保護檔案的相關資訊。

   若要取得受原則保護檔案的相關資訊，請叫用屬於物件的適當 `RMInspectResult` 方法。 例如，若要擷取原則名稱，請叫 `RMInspectResult` 用物件的方 `getPolicyName` 法。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* &quot;快速啟動（SOAP模式）:使用Java API檢查受原則保護的PDF檔案」

### 使用web service API檢查受原則保護的PDF檔案 {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

使用Document Security Service API(web service)檢查受原則保護的PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Document Security Client API物件。

   * 使用其 `RightsManagementServiceClient` 預設建構函式建立物件。
   * 使用建 `RightsManagementServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `RightsManagementServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。


1. 擷取受原則保護的檔案以進行檢查。

   * 使用其 `BLOB` 建構函式建立物件。 此物 `BLOB` 件用來儲存要檢查的PDF檔案。
   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，代表PDF檔案的檔案位置，以及在中開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法，以串流資料填 `System.IO.FileStream` 入位元組 `Read` 陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 檢查檔案。

   調用物件的方法，以檢查受原 `RightsManagementServiceClient` 則保護的 `inspectDocument` 檔案。 傳遞包 `BLOB` 含受原則保護PDF檔案的物件。 此方法傳回 `RMInspectResult` 包含受原則保護檔案資訊的物件。

1. 取得受原則保護檔案的相關資訊。

   若要取得受原則保護檔案的相關資訊，請取得屬於物件的適當欄位 `RMInspectResult` 值。 例如，若要擷取原則名稱，請取得物件欄 `RMInspectResult` 位的值 `policyName` 。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM):使用web service API檢查受原則保護的PDF檔案」
* 「快速入門(SwaRef):使用web service API檢查受原則保護的PDF檔案」

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 建立浮水印 {#creating-watermarks}

浮水印可以透過唯一識別檔案並控製版權侵權來確保檔案的安全性。 例如，您可以建立水印，並將該水印標示為檔案的所有頁面上的機密。 在建立浮水印後，您可以將它加入原則中。 也就是說，您可以使用新建立的浮水印來設定原則的浮水印屬性。 將包含浮水印的原則套用至檔案後，浮水印就會出現在受原則保護的檔案中。

>[!NOTE]
>
>只有具有Document Security管理權限的使用者才能建立浮水印。 也就是說，在定義建立Document Security服務客戶端對象所需的連接設定時，必須指定此類用戶。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-8}

要建立水印，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 設定浮水印屬性。
1. 向Document Security服務註冊浮水印。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Document Security Client API物件**

您必須先建立Document Security服務用戶端物件，才能以程式設計方式執行Document Security服務作業。 如果您使用Java API，請建立物 `RightsManagementClient` 件。 如果您使用Document Security web service API，請建立物 `RightsManagementServiceService` 件。

**設定浮水印屬性**

要建立新水印，必須設定水印屬性。 必須始終定義name屬性。 除了name屬性外，您至少必須設定以下屬性之一：

* 自訂文字
* DateIncluded
* UserIdIncluded
* UserNameIncluded

下表列出使用web services建立浮水印時所需的索引鍵和值配對。

<table>
 <thead>
  <tr>
   <th><p>密鑰名稱</p></th>
   <th><p>說明</p></th>
   <th><p>值</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERNAME_ENABLED</code></p></td>
   <td><p>指定開啟文檔的用戶的用戶名是否屬於水印。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>指定開啟文檔的用戶的標識是否屬於水印。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>指定當前日期是否屬於水印。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>如果此值為true，則必須使用指定自訂文字的值 <code>WaterBackCmd:SRCTEXT</code>。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>指定浮水印的不透明度。 如果未指定，則預設值為0.5。</p></td>
   <td><p>介於0.0和1.0之間的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>指定水印的旋轉。 預設值為0度。</p></td>
   <td><p>介於0和359之間的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>如果指定此值，則 <code>WaterBackCmd:IS_SIZE_ENABLED</code> 必須存在且值必須為true。 如果未指定此屬性，則預設行為符合頁面大小。</p></td>
   <td><p>大於0.0且小於或等於1.0的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>指定水印的水準對齊方式。 預設值為中心。</p></td>
   <td><p>左、中或右</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>指定浮水印的垂直對齊方式。 預設值為中心。</p></td>
   <td><p>上、中或下</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>指定水印是否為背景。 預設值為false。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>如果指定自訂比例，則為true。 如果此值為true，則還必須指定SCALE。 如果此值為false，則預設值會符合頁面大小。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>指定浮水印的自訂文字。 如果此值存在，則 <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> 也必須存在並設定為true。</p></td>
   <td><p>True或False</p></td>
  </tr>
 </tbody>
</table>

所有水印都必須定義下列其中一個屬性：

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

所有其他屬性都是選用的。

**註冊水印**

必須先在Document Security服務中註冊新的浮水印，才能使用。 在註冊水印後，您可以在原則中使用水印。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[套用原則至PDF檔案](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API建立浮水印 {#create-watermarks-using-the-java-api}

使用Document Security API(Java)建立浮水印：

1. 包含專案檔案。

   在Java專案的類別路徑中 `adobe-rightsmanagement-client.jar`包含用戶端JAR檔案，例如。

1. 建立Document Security Client API物件。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `RightsManagementClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 設定水印屬性

   * 調用 `Watermark` 物件的靜態方 `InfomodelObjectFactory` 法來建立物 `createWatermark` 件。 此方法返回對 `Watermark` 像。
   * 調用物件的方法並傳遞指定原則 `Watermark` 名稱的字 `setName` 串值，以設定浮水印的名稱屬性。
   * 調用物件的方法並傳遞，以設定 `Watermark` 水印的 `setBackground` 背景屬性 `true`。 通過設定此屬性，水印將出現在文檔的背景中。
   * 調用物件的方法並傳遞代表浮水印 `Watermark` 文字的字串值， `setCustomText` 以設定浮水印的自訂文字屬性。
   * 調用物件的方法並傳遞指定不 `Watermark` 透明度等級的 `setOpacity` 整數值，以設定浮水印的不透明度屬性。 值100表示水印完全不透明，值0表示水印完全透明。

1. 註冊水印。

   * 調用 `WatermarkManager` 物件的方 `RightsManagementClient` 法以建立物 `getWatermarkManager` 件。 此方法返回對 `WatermarkManager` 像。
   * 調用物件的方 `WatermarkManager` 法並將代 `registerWatermark` 表水印的物 `Watermark` 件傳遞至註冊，以註冊水印。 此方法會傳回代表浮水印識別值的字串值。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* &quot;快速啟動（SOAP模式）:使用Java API建立浮水印&quot;

### 使用web service API建立浮水印 {#create-watermarks-using-the-web-service-api}

使用Document Security API(web service)建立浮水印：

1. 建立Document Security Client API物件。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Document Security Client API物件。

   * 使用其 `RightsManagementServiceClient` 預設建構函式建立物件。
   * 使用建 `RightsManagementServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `RightsManagementServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。


1. 設定水印屬性。

   * 通過調 `WatermarkSpec` 用建構子建立對 `WatermarkSpec` 像。
   * 為物件的資料成員指派字串值，以設定浮 `WatermarkSpec` 水印的 `name` 名稱。
   * 將字串值指派 `id` 給物件的資料成員，以設 `WatermarkSpec` 定浮水印的 `id` 屬性。
   * 對於要設定的每個水印屬性，請建立一個單獨的 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象。
   * 將值指派給物件的資料成 `MyMapOf_xsd_string_To_xsd_anyType_Item` 員以設 `key` 定索引鍵值(例如 `WaterBackCmd:OPACITY)`。
   * 將值指派給物件的資 `MyMapOf_xsd_string_To_xsd_anyType_Item` 料成員 `value` (例如 `.25`)。
   * 建立對 `MyArrayOf_xsd_anyType` 像。 對於每 `MyMapOf_xsd_string_To_xsd_anyType_Item` 個物件，請叫 `MyArrayOf_xsd_anyType` 用物件的方 `Add` 法。 傳遞物 `MyMapOf_xsd_string_To_xsd_anyType_Item` 件。
   * 將物 `MyArrayOf_xsd_anyType` 件指派給物 `WatermarkSpec` 件的資料 `values` 成員。

1. 註冊水印。

   調用物件的方 `RightsManagementServiceClient` 法並將代 `registerWatermark` 表水印的物 `WatermarkSpec` 件傳遞至註冊，以註冊水印。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM):使用web service API建立浮水印&quot;
* 「快速入門(SwaRef):使用web service API建立浮水印&quot;

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改浮水印 {#modifying-watermarks}

您可以使用Document Security Java API或web service API修改現有的浮水印。 要更改現有水印，可以檢索它、修改其屬性，然後在伺服器上更新它。 例如，假設您檢索水印並修改其不透明度屬性。 在更改生效之前，您必須更新水印。

當您修改水印時，此變更會影響套用水印的未來檔案。 也就是說，包含浮水印的現有PDF檔案不受影響。

>[!NOTE]
>
>只有具有Document Security管理權限的使用者才能修改浮水印。 也就是說，在定義建立Document Security服務客戶端對象所需的連接設定時，必須指定此類用戶。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-9}

要修改水印，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 檢索要修改的水印。
1. 設定浮水印屬性。
1. 更新浮水印。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Document Security Client API物件**

您必須先建立Document Security服務用戶端物件，才能以程式設計方式執行Document Security服務作業。 如果您使用Java API，請建立物 `DocumentSecurityClient` 件。 如果您使用Document Security web service API，請建立物 `DocumentSecurityServiceService` 件。

**檢索要修改的水印**

要修改水印，必須檢索現有水印。 可以通過指定水印的名稱或通過指定水印的標識符值來檢索水印。

**設定浮水印屬性**

要修改現有水印，請更改一個或多個水印屬性的值。 當使用Web服務以程式設計方式更新水印時，您必須設定所有原本設定的屬性，即使值未變更亦然。 例如，假設已設定以下水印屬性： `WaterBackCmd:IS_USERID_ENABLED`、 `WaterBackCmd:IS_CUSTOMTEXT_ENABLED``WaterBackCmd:OPACITY`和 `WaterBackCmd:SRCTEXT`。 雖然您要修改的唯一屬性是 `WaterBackCmd:OPACITY`，但您必須將其他值設定為正確。

>[!NOTE]
>
>使用Java API修改浮水印時，您不需要指定所有屬性。 設定要修改的水印屬性。

>[!NOTE]
>
>有關水印屬性名稱的資訊，請參 [閱建立水印](protecting-documents-policies.md#creating-watermarks)。

**更新浮水印**

修改水印的屬性後，您必須更新水印。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[建立浮水印](protecting-documents-policies.md#creating-watermarks)

### 使用Java API修改浮水印 {#modify-watermarks-using-the-java-api}

使用Document Security API(Java)修改浮水印：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `DocumentSecurityClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 檢索要修改的水印。

   調用物 `WatermarkManager` 件的方法，並 `DocumentSecurityClient` 傳遞指定浮 `getWatermarkManager` 水印名稱的字串值，以建立物件。 此方法返回 `Watermark` 表示要修改的水印的對象。

1. 設定水印屬性。

   調用物件的方法並傳遞指定不 `Watermark` 透明度等級的 `setOpacity` 整數值，以設定浮水印的不透明度屬性。 值100表示水印完全不透明，值0表示水印完全透明。

   >[!NOTE]
   >
   >此範例僅修改不透明屬性。

1. 更新浮水印。

   * 調用物件的方 `WatermarkManager` 法並傳 `updateWatermark` 遞屬性已修 `Watermark` 改的物件，以更新水印。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱快速入門（SOAP模式）:使用Java API部分修改水印。

### 使用web service API修改浮水印 {#modify-watermarks-using-the-web-service-api}

使用Document Security API(web service)修改浮水印：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Document Security Client API物件。

   * 使用其 `DocumentSecurityServiceClient` 預設建構函式建立物件。
   * 使用建 `RightsManagementServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `DocumentSecurityServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。


1. 檢索要修改的水印。

   調用物件的方法來擷取要修 `DocumentSecurityServiceClient` 改的浮水印 `getWatermarkByName` 。 傳遞指定浮水印名稱的字串值。 此方法返回 `WatermarkSpec` 表示要修改的水印的對象。

1. 設定水印屬性。

   * 對於要更新的每個水印屬性，請建立一個單獨的 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象。
   * 將值指派給物件的資料成 `MyMapOf_xsd_string_To_xsd_anyType_Item` 員以設 `key` 定索引鍵值(例如 `WaterBackCmd:OPACITY)`。
   * 將值指派給物件的資 `MyMapOf_xsd_string_To_xsd_anyType_Item` 料成員 `value` (例如 `.50`)。
   * 建立對 `MyArrayOf_xsd_anyType` 像。 對於每 `MyMapOf_xsd_string_To_xsd_anyType_Item` 個物件，請叫 `MyArrayOf_xsd_anyType` 用物件的方 `Add` 法。 傳遞物 `MyMapOf_xsd_string_To_xsd_anyType_Item` 件。
   * 將物 `MyArrayOf_xsd_anyType` 件指派給物 `WatermarkSpec` 件的資料 `values` 成員。

1. 更新浮水印。

   調用物件的方 `DocumentSecurityServiceClient` 法並傳遞 `updateWatermark` 代表要修 `WatermarkSpec` 改的物件，以更新水印。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM):使用web service API修改水印&quot;

## 搜尋事件 {#searching-for-events}

Rights Management服務會在特定動作發生時追蹤這些動作，例如將原則套用至檔案、開啟受原則保護的檔案，以及廢止檔案存取權。 必須為Rights Management服務啟用事件審核，否則不會追蹤事件。

事件分為下列類別：

* 管理員事件是與管理員相關的操作，如建立新管理員帳戶。
* 檔案事件是與檔案相關的動作，例如關閉受原則保護的檔案。
* 策略事件是與策略相關的操作，如建立新策略。
* 服務事件是與Rights Management服務相關的操作，如與用戶目錄同步。

您可以使用Rights Management Java API或web service API來搜尋指定的事件。 通過搜索事件，您可以執行任務，如建立某些事件的日誌檔案。

>[!NOTE]
>
>如需Rights Management服務的詳細資訊，請參閱「AEM [表格的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-10}

要搜索Rights Management事件，請執行以下步驟：

1. 包含專案檔案。
1. 建立Rights Management用戶端API物件。
1. 指定要搜尋的事件。
1. 搜尋事件。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Rights Management用戶端API物件**

在以寫程式方式執行Rights Management服務操作之前，必須建立Rights Management服務客戶端對象。 如果您使用Java API，請建立物 `DocumentSecurityClient` 件。 如果您使用Rights Management web service API，請建立物 `DocumentSecurityServiceService` 件。

**指定要搜尋的事件**

您必須指定要搜尋的事件。 例如，您可以搜索策略建立事件，該事件在建立新策略時發生。

**搜尋事件**

指定要搜尋的事件後，您可以使用Rights Management Java API或Rights Management web service API來搜尋事件。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API搜尋事件 {#search-for-events-using-the-java-api}

使用Rights Management API(Java)搜尋事件：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Rights Management用戶端API物件

   使用其 `DocumentSecurityClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 指定要搜尋的事件

   * 調用 `EventManager` 物件的方 `DocumentSecurityClient` 法以建立物 `getEventManager` 件。 此方法返回對 `EventManager` 像。
   * 通過調用 `EventSearchFilter` 其建構子建立對象。
   * 通過調用對象的方法並傳遞屬於表示要搜索的 `EventSearchFilter` 事件的類的 `setEventCode` 靜態資料成員，指定要搜索的 `EventManager` 事件。 例如，要搜索策略建立事件，請傳遞 `EventManager.POLICY_CREATE_EVENT`。
   >[!NOTE]
   >
   >您可以叫用物件方法來定義其他 `EventSearchFilter` 搜尋准則。 例如，叫用方 `setUserName` 法以指定與事件關聯的使用者。

1. 搜尋事件

   調用物件的方法並傳 `EventManager` 遞定義事件搜 `searchForEvents` 尋准則的 `EventSearchFilter` 物件，以搜尋事件。 此方法會傳回物件 `Event` 陣列。

**程式碼範例**

如需使用Rights Management服務的程式碼範例，請參閱下列快速入門：

* &quot;快速入門(SOAP):使用Java API搜尋事件&quot;

### 使用網站服務API搜尋事件 {#search-for-events-using-the-web-service-api}

使用Rights Management API(web service)搜尋事件：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Rights Management用戶端API物件

   * 使用其 `DocumentSecurityServiceClient` 預設建構函式建立物件。
   * 使用建 `DocumentSecurityServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `DocumentSecurityServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。


1. 指定要搜尋的事件

   * 使用其 `EventSpec` 建構函式建立物件。
   * 透過設定物件的資料成員，以例項來指 `EventSpec` 定事件發生的 `firstTime.date` 時 `DataTime` 段開始時間，例項代表事件發生時的日期範圍開始時間。
   * 將值指 `true` 派給物 `EventSpec` 件的資料 `firstTime.dateSpecified` 成員。
   * 透過使用例項設定物件的資料成員，以 `EventSpec` 指定事件發生 `lastTime.date``DataTime` 的時段結束時間，此例項代表事件發生時的日期範圍結束時間。
   * 將值指 `true` 派給物 `EventSpec` 件的資料 `lastTime.dateSpecified` 成員。
   * 將字串值指派給物件的資料成員，以設定要 `EventSpec` 搜尋的 `eventCode` 事件。 下表列出了可分配給此屬性的數值：
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

   調用物件的方法並傳 `DocumentSecurityServiceClient` 遞代表要搜尋之事 `searchForEvents` 件的物 `EventSpec` 件，以及結果的最大數目，以搜尋事件。 此方法會傳回 `MyArrayOf_xsd_anyType` 每個元素都是例項的 `AuditSpec` 系列。 使用例 `AuditSpec` 項，您可以取得事件的相關資訊，例如事件發生的時間。 實 `AuditSpec` 例包含指定 `timestamp` 此資訊的資料成員。

**程式碼範例**

如需使用Rights Management服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM):使用web service API搜尋事件&quot;
* 「快速入門(SwaRef):使用web service API搜尋事件&quot;

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將原則套用至Word檔案 {#applying-policies-to-word-documents}

除了PDF檔案外，Rights Management服務還支援其他檔案格式，例如Microsoft Word檔案（DOC檔案）和其他Microsoft Office檔案格式。 例如，您可以將原則套用至Word檔案，以保護其安全。 將原則套用至Word檔案，即可限制對檔案的存取。 如果文檔已使用策略保護，則不能將策略應用於文檔。

您可以在分發受原則保護的Word檔案後，監控檔案的使用情況。 也就是說，您可以看到檔案的使用方式以及使用者。 例如，您可以瞭解某人何時開啟檔案。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-11}

要將策略應用於Word文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 擷取套用原則的Word檔案。
1. 將現有原則套用至Word檔案。
1. 儲存受原則保護的Word檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Document Security用戶端API物件**

您必須先建立Document Security服務用戶端物件，才能以程式設計方式執行Document Security服務作業。

**擷取Word檔案**

您必須檢索Word文檔才能應用策略。 將原則套用至Word檔案後，使用者在使用檔案時會受到限制。 例如，如果原則未讓檔案在離線時開啟，則使用者必須線上上才能開啟檔案。

**將現有原則套用至Word檔案**

要將策略應用於Word文檔，必須引用現有策略並指定策略所屬的策略集。 設定連接屬性的用戶必須有權訪問指定的策略。 否則，會發生例外。

**儲存Word檔案**

在Document Security服務將原則套用至Word檔案後，您就可以將受原則保護的Word檔案儲存為DOC檔案。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[廢止檔案存取權](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API將原則套用至Word檔案 {#apply-a-policy-to-a-word-document-using-the-java-api}

使用Document Security API(Java)將原則套用至Word檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `DocumentSecurityClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 擷取Word檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定Word檔案位置的字串值，以建立代表Word檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 將現有原則套用至Word檔案。

   * 調用 `DocumentManager` 物件的方 `DocumentSecurityClient` 法以建立物 `getDocumentManager` 件。
   * 調用物件的方法並傳遞下列值，以套 `DocumentManager` 用原則 `protectDocument` 至Word檔案：

      * 包 `com.adobe.idp.Document` 含套用原則之Word檔案的物件。
      * 指定文檔名稱的字串值。
      * 一個字串值，它指定策略所屬的策略集的名稱。 您可以指定 `null` 導致使用策略 `MyPolicies` 集的值。
      * 指定策略名稱的字串值。
      * 一個字串值，它表示作為文檔發佈者的用戶的用戶管理域的名稱。 此參數值是可選的，可以是null（如果此參數為null，則下一個參數值必須為null）。
      * 一個字串值，它表示作為文檔發佈者的用戶管理器用戶的標準名稱的名稱。 此參數值是可選的，可 `null` 以是(如果此參數 `null`為，則前一個參數值必須 `null`是)。
      * 表 `com.adobe.livecycle.rightsmanagement.Locale` 示用於選擇MS office模板的區域設定。 此參數值是可選的，您可以指定 `null`。
      此方 `protectDocument` 法會傳回包 `RMSecureDocumentResult` 含受原則保護Word檔案的物件。


1. 儲存Word檔案。

   * 叫用物 `RMSecureDocumentResult` 件的方 `getProtectedDoc` 法以取得受原則保護的Word檔案。 此方法返回對 `com.adobe.idp.Document` 像。
   * 建立對 `java.io.File` 像並確保檔案副檔名為DOC。
   * 叫用 `com.adobe.idp.Document` 物件的方 `copyToFile` 法，將物件的內容複製至檔案(請確定您使用 `Document` 由方法傳回的物 `Document``getProtectedDoc` 件)。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* &quot;快速啟動（SOAP模式）:使用Java API將原則套用至Word檔案」

### 使用web service API將原則套用至Word檔案 {#apply-a-policy-to-a-word-document-using-the-web-service-api}

使用Document Security API(web service)將原則套用至Word檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Document Security Client API物件。

   * 使用其 `DocumentSecurityServiceClient` 預設建構函式建立物件。
   * 使用建 `DocumentSecurityServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `DocumentSecurityServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。


1. 擷取Word檔案。

   * 使用其 `BLOB` 建構函式建立物件。 對 `BLOB` 像用於儲存應用策略的Word文檔。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示Word文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 透過取得物件的屬性，來 `System.IO.FileStream` 判斷位元組陣列 `Length` 大小。
   * 調用物件的方法，以串流資料填 `System.IO.FileStream` 入位元組 `Read` 陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 將現有原則套用至Word檔案。

   調用物件的方法並傳遞下列值，以套 `DocumentSecurityServiceClient` 用原則 `protectDocument` 至Word檔案：

   * 包 `BLOB` 含套用原則之Word檔案的物件。
   * 指定文檔名稱的字串值。
   * 一個字串值，它指定策略所屬的策略集的名稱。 您可以指定 `null` 導致使用策略 `MyPolicies` 集的值。
   * 指定策略名稱的字串值。
   * 一個字串值，它表示作為文檔發佈者的用戶的用戶管理域的名稱。 此參數值是可選的，可以是null(如果此參數為null，則下一個參數值必須 `null`為)。
   * 一個字串值，它表示作為文檔發佈者的用戶管理器用戶的標準名稱的名稱。 此參數值是可選的，可以是空值(如果此參數為空值，則上一個參數值必須 `null`為)。
   * 指 `RMLocale` 定地區值(例如 `RMLocale.en`)的值。
   * 用於儲存策略標識符值的字串輸出參數。
   * 用來儲存受原則保護識別碼值的字串輸出參數。
   * 用於儲存MIME類型(例如， `application/doc`)的字串輸出參數。
   此方 `protectDocument` 法會傳回包 `BLOB` 含受原則保護Word檔案的物件。

1. 儲存Word檔案。

   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示受原則保護Word文檔的檔案位置。
   * 建立一個位元組陣列，該陣列儲存由方 `BLOB` 法返回的對象的資料內 `protectDocument` 容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `MTOM` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入Word檔案。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM):使用web service API將原則套用至Word檔案」

## 從Word檔案移除原則 {#removing-policies-from-word-documents}

您可以從受原則保護的Word檔案移除原則，以移除檔案的安全性。 也就是說，如果您不想讓檔案受到原則的保護。 如果您想要使用較新的原則更新受原則保護的Word檔案，則切換原則會更有效率，而不是移除原則並新增更新的原則。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-12}

若要從受原則保護的Word檔案移除原則，請執行下列步驟：

1. 包含專案檔案
1. 建立Document Security Client API物件。
1. 擷取受原則保護的Word檔案。
1. 從Word檔案移除原則。
1. 儲存不安全的Word檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Document Security Client API物件**

在以程式設計方式執行Document Security服務操作之前，請先建立Document Security服務用戶端物件。

**擷取受原則保護的Word檔案**

您必須擷取受原則保護的Word檔案，才能移除原則。 如果您嘗試從未受原則保護的Word檔案移除原則，將會造成例外。

**從Word檔案移除原則**

只要在連線設定中指定管理員，您就可以從受原則保護的Word檔案移除原則。 否則，用於保護文檔的策略必須包含權限， `SWITCH_POLICY` 才能從Word文檔中刪除策略。 此外，在AEM Forms連線設定中指定的使用者也必須擁有該權限。 否則，會拋出異常。

**儲存不安全的Word檔案**

在Document Security服務從Word檔案移除原則後，您可以將不安全的Word檔案儲存為DOC檔案。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[將原則套用至Word檔案](protecting-documents-policies.md#applying-policies-to-word-documents)

### 使用Java API從Word檔案移除原則 {#remove-a-policy-from-a-word-document-using-the-java-api}

使用Document Security API(Java)，從受原則保護的Word檔案移除原則：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `RightsManagementClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 擷取受原則保護的Word檔案

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定Word檔案位置的字串值，建立代表受原則保護Word檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 從Word檔案移除原則

   * 調用 `DocumentManager` 物件的方 `RightsManagementClient` 法以建立物 `getDocumentManager` 件。
   * 調用物件的方法並傳遞包含受原則保 `DocumentManager` 護之Word文 `removeSecurity` 件的物 `com.adobe.idp.Document` 件，以移除Word檔案中的原則。 此方法傳回包 `com.adobe.idp.Document` 含不安全Word檔案的物件。

1. 儲存不安全的Word檔案

   * 建立對 `java.io.File` 像並確保檔案副檔名為DOC。
   * 叫用 `Document` 物件的方 `copyToFile` 法，將物件的內容複製至檔案(請確定您使用 `Document` 由方法傳回的物 `Document``removeSecurity` 件)。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* &quot;快速啟動（SOAP模式）:使用Java API從Word檔案移除原則」

### 使用web service API從Word檔案移除原則 {#remove-a-policy-from-a-word-document-using-the-web-service-api}

使用Document Security API(web service)，從受原則保護的Word檔案移除原則：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Document Security Client API物件

   * 使用其 `RightsManagementServiceClient` 預設建構函式建立物件。
   * 使用建 `RightsManagementServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/RightsManagementService?WSDL`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `RightsManagementServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。


1. 擷取受原則保護的Word檔案

   * 使用其 `BLOB` 建構函式建立物件。 對 `BLOB` 像用於儲存從中刪除策略的受策略保護Word文檔。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示Word文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 從Word檔案移除原則

   調用物件的方法並傳遞包含受原則保 `RightsManagementServiceClient` 護之Word文 `removePolicySecurity` 件的物 `BLOB` 件，從Word檔案移除原則。 此方法傳回包 `BLOB` 含不安全Word檔案的物件。

1. 儲存不安全的Word檔案

   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示不安全Word文檔的檔案位置。
   * 建立一個位元組陣列，該陣列儲存由方 `BLOB` 法返回的對象的資料內 `removePolicySecurity` 容。 取得物件欄位的值，以填入 `BLOB` 位元組陣 `MTOM` 列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM):使用web service API從Word檔案移除原則」

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
