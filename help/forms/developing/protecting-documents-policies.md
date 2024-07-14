---
title: 使用原則保護檔案
description: 使用Document Security服務來動態套用機密性設定至Adobe PDF檔案，並保持對檔案的控制。 Document Security服務也可讓使用者持續控制收件人使用受原則保護的PDF檔案的方式。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: ff42579e-6aaf-433d-8b5d-9e9dd0957250
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '15394'
ht-degree: 0%

---

# 使用原則保護檔案 {#protecting-documents-with-policies}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於Document Security服務**

Document Security服務可讓使用者動態地將機密性設定套用至Adobe PDF檔案，並保持對檔案的控制，無論檔案分佈範圍如何。

Document Security服務可讓使用者持續控制受原則保護的PDF檔案收件人使用方式，以防止資訊擴散到使用者觸及的範圍之外。 使用者可以指定誰可以開啟檔案、限制他們使用檔案的方式，並在檔案分發後監視檔案。 使用者也可以動態控制受原則保護檔案的存取權，甚至可以動態撤銷對檔案的存取權。

Document Security服務也會保護其他檔案型別，例如Microsoft Word檔案（DOC檔案）。 您可以使用Document Security使用者端API來處理這些檔案型別。 支援下列版本：

* Microsoft Office 2003檔案（DOC、XLS、PPT檔案）
* Microsoft Office 2007檔案（DOCX、XLSX、PPTX檔案）
* PTC Pro/E檔案

為清楚起見，以下兩個部分討論如何使用Word檔案：

* [將原則套用至Word檔案](protecting-documents-policies.md#applying-policies-to-word-documents)
* [從Word檔案移除原則](protecting-documents-policies.md#removing-policies-from-word-documents)

您可以使用Document Security服務完成這些工作：

* 建立原則。 如需詳細資訊，請參閱[建立原則](protecting-documents-policies.md#creating-policies)。
* 修改原則。 如需詳細資訊，請參閱[修改原則](protecting-documents-policies.md#modifying-policies)。
* 刪除原則。 如需詳細資訊，請參閱[刪除原則](protecting-documents-policies.md#deleting-policies)。
* 套用原則至PDF檔案。 如需詳細資訊，請參閱[套用原則至PDF檔案](protecting-documents-policies.md#applying-policies-to-pdf-documents)。
* 從PDF檔案中移除原則。 如需詳細資訊，請參閱[從PDF檔案移除原則](protecting-documents-policies.md#removing-policies-from-pdf-documents)。
* Inspect受原則保護的檔案。 如需詳細資訊，請參閱[檢查受原則保護的PDF檔案](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)。
* 撤銷PDF檔案的存取權。 如需詳細資訊，請參閱[撤銷檔案的存取權](protecting-documents-policies.md#revoking-access-to-documents)。
* 恢復對已撤銷檔案的存取權。 如需詳細資訊，請參閱[恢復撤銷檔案的存取權](protecting-documents-policies.md#reinstating-access-to-revoked-documents)。
* 建立浮水印。 如需詳細資訊，請參閱[建立浮水印](protecting-documents-policies.md#creating-watermarks)。
* 搜尋事件。 如需詳細資訊，請參閱[搜尋事件](protecting-documents-policies.md#searching-for-events)。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 建立原則 {#creating-policies}

您可以使用Document Security Java API或Web服務API，以程式設計方式建立原則。 *原則*&#x200B;是包含檔案安全性設定、授權使用者及使用許可權的資訊集合。 您可以使用適用於不同情況和使用者的安全性設定，來建立和儲存任意數量的原則。

原則可讓您執行下列工作：

* 指定可以開啟檔案的個人。 收件者可以屬於或屬於您組織。
* 指定收件者使用檔案的方式。 您可以限制存取不同的Acrobat和Adobe Reader功能。 這些功能包括列印和複製文字、新增簽名以及在檔案中新增註解的功能。
* 隨時變更存取許可權和安全性設定，即使在您分發受原則保護的檔案後亦然。
* 在分發檔案後監視檔案的使用。 您可以檢視檔案的使用方式以及誰正在使用它。 例如，您可以找出何時有人開啟了檔案。

### 使用Web服務建立原則 {#creating-a-policy-using-web-services}

使用Web服務API建立原則時，請參考說明原則的現有Portable Document Rights Language (PDRL) XML檔案。 原則許可權和主體在PDRL檔案中定義。 下列XML檔案是PDRL檔案的範例。

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
>如需Document Security服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要建立原則，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 設定原則的屬性。
1. 建立原則專案。
1. 註冊原則。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-rightsmanagement-client.jar
* namespace.jar (如果AEM Forms部署在JBoss上)
* jaxb-api.jar (如果AEM Forms部署在JBoss上)
* jaxb-impl.jar (如果AEM Forms部署在JBoss上)
* jaxb-libs.jar (如果AEM Forms部署在JBoss上)
* jaxb-xjc.jar (如果AEM Forms部署在JBoss上)
* relaxngDatatype.jar (如果AEM Forms部署在JBoss上)
* xsdlib.jar (如果AEM Forms部署在JBoss上)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar (如果AEM Forms未部署在JBoss上，請使用其他JAR檔案)

如需關於這些JAR檔案位置的資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立Document Security Client API物件**

在您以程式設計方式執行Document Security服務操作之前，請先建立Document Security服務使用者端物件。

**設定原則的屬性**

若要建立原則，請設定原則屬性。 原則名稱是強制屬性。 每個原則集的原則名稱必須是唯一的。 原則集只是原則的集合。 如果原則屬於不同的原則集，則可能會有兩個名稱相同的原則。 但是，單一原則集內的兩個原則不能有相同的原則名稱。

另一個要設定的有用屬性是有效期。 有效期間是指獲授權的收件者可存取受原則保護檔案的時間期間。 如果您未設定此屬性，則原則永遠有效。

有效期可以設定為下列選項之一：

* 從檔案發佈之時起可存取檔案的一組天數
* 無法存取檔案的結束日期
* 可存取檔案的特定日期範圍
* 永遠有效

您可以只指定開始日期，這會導致原則在開始日期之後有效。 如果您只指定結束日期，則原則會在結束日期之前有效。 但是，如果未定義開始日期和結束日期，則會擲回例外狀況。

設定屬於原則的屬性時，您也可以設定加密設定。 這些加密設定會在原則套用至檔案時生效。 您可以指定下列加密值：

* **AES256**：代表使用256位元金鑰的AES加密演演算法。
* **AES128**：代表使用128位元金鑰的AES加密演演算法。
* **NoEncryption：**&#x200B;代表未加密。

指定`NoEncryption`選項時，您無法將`PlaintextMetadata`選項設定為`false`。 如果嘗試這麼做，會發生例外狀況。

>[!NOTE]
>
>如需您可以設定的其他屬性相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`Policy`介面說明。

**建立原則專案**

原則專案會將主體（群組和使用者）和許可權附加到原則。 原則必須至少有一個原則專案。 例如，假設您執行下列工作：

* 建立並註冊原則專案，讓群組僅能線上上檢視檔案，並禁止收件者複製檔案。
* 將原則專案附加至原則。
* 使用Acrobat以原則保護檔案。

這些動作會導致收件者僅能線上上檢視檔案而無法複製檔案。 除非將安全性從檔案中移除，否則檔案會保持安全性。

**登入原則**

必須先註冊新原則才能使用。 註冊原則之後，您可以使用它來保護檔案。

### 使用Java API建立原則 {#create-a-policy-using-the-java-api}

使用Document Security API (Java)建立原則：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`DocumentSecurityClient`物件。

1. 設定原則的屬性。

   * 呼叫`InfomodelObjectFactory`物件的靜態`createPolicy`方法，以建立`Policy`物件。 此方法會傳回`Policy`物件。
   * 透過叫用`Policy`物件的`setName`方法並傳遞指定原則名稱的字串值來設定原則的name屬性。
   * 透過叫用`Policy`物件的`setDescription`方法並傳遞指定原則描述的字串值來設定原則的描述。
   * 透過叫用`Policy`物件的`setPolicySetName`方法並傳遞指定原則集名稱的字串值，來指定新原則所屬的原則集。 （您可以為此引數值指定`null`，這會使原則新增至&#x200B;*我的原則*&#x200B;原則集。）
   * 透過叫用`InfomodelObjectFactory`物件的靜態`createValidityPeriod`方法建立原則的有效期。 此方法會傳回`ValidityPeriod`物件。
   * 設定受原則保護檔案可存取的天數，方法是叫用`ValidityPeriod`物件的`setRelativeExpirationDays`方法，並傳遞指定天數的整數值。
   * 透過叫用`Policy`物件的`setValidityPeriod`方法並傳遞`ValidityPeriod`物件來設定原則的有效期。

1. 建立原則專案。

   * 透過叫用`InfomodelObjectFactory`物件的靜態`createPolicyEntry`方法建立原則專案。 此方法會傳回`PolicyEntry`物件。
   * 透過叫用`InfomodelObjectFactory`物件的靜態`createPermission`方法來指定原則的許可權。 傳遞屬於代表許可權之`Permission`介面的靜態資料成員。 此方法會傳回`Permission`物件。 例如，若要新增允許使用者從受原則保護的PDF檔案複製資料的許可權，請傳遞`Permission.COPY`。 （對每個要新增的許可權重複此步驟）。
   * 叫用`PolicyEntry`物件的`addPermission`方法並傳遞`Permission`物件，以新增許可權至原則專案。 （對您建立的每個`Permission`物件重複此步驟）。
   * 透過叫用`InfomodelObjectFactory`物件的靜態`createSpecialPrincipal`方法建立原則主體。 傳遞屬於代表主體之`InfomodelObjectFactory`物件的資料成員。 此方法會傳回`Principal`物件。 例如，若要新增檔案的發行者作為主體，請傳遞`InfomodelObjectFactory.PUBLISHER_PRINCIPAL`。
   * 叫用`PolicyEntry`物件的`setPrincipal`方法並傳遞`Principal`物件，以將主體加入原則專案。
   * 呼叫`Policy`物件的`addPolicyEntry`方法並傳遞`PolicyEntry`物件，以將原則專案新增至原則。

1. 註冊原則。

   * 呼叫`DocumentSecurityClient`物件的`getPolicyManager`方法，以建立`PolicyManager`物件。
   * 透過叫用`PolicyManager`物件的`registerPolicy`方法並傳遞下列值來登入原則：

      * 代表要註冊之原則的`Policy`物件。

   * 字串值，代表原則所屬的原則集。

   如果您在連線設定內使用AEM表單管理員帳戶來建立`DocumentSecurityClient`物件，請在叫用`registerPolicy`方法時指定原則集名稱。 如果您傳遞原則集的`null`值，原則會在管理員&#x200B;*我的原則*&#x200B;原則集中建立。

   如果您在連線設定中使用Document Security使用者，則可以叫用僅接受原則的多載`registerPolicy`方法。 也就是說，您不需要指定原則集名稱。 但是，原則已新增至名為&#x200B;*我的原則*&#x200B;的原則集。 如果您不想將新原則新增至這個原則集，請在叫用`registerPolicy`方法時指定原則集名稱。

   >[!NOTE]
   >
   >建立原則時，參考現有的原則集。 如果您指定的原則集不存在，則會擲回例外狀況。

如需使用Document Security服務的程式碼範例，請參閱以下內容：

* 「快速入門(SOAP模式)：使用Java API建立原則」

### 使用Web服務API建立原則 {#create-a-policy-using-the-web-service-api}

使用Document Security API （Web服務）建立原則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Document Security Client API物件。

   * 使用預設建構函式建立`DocumentSecurityServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`DocumentSecurityServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`RightsManagementServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 設定原則的屬性。

   * 使用物件的建構函式建立`PolicySpec`物件。
   * 將字串值指派給`PolicySpec`物件的`name`資料成員，以設定原則的名稱。
   * 將字串值指派給`PolicySpec`物件的`description`資料成員，以設定原則的描述。
   * 指定原則所屬的原則集，方法是指派字串值給`PolicySpec`物件的`policySetName`資料成員。 指定現有的原則集名稱。 （您可以為此引數值指定`null`，結果會將原則新增至&#x200B;*我的原則*。）
   * 將整數值指派給`PolicySpec`物件的`offlineLeasePeriod`資料成員，以設定原則的離線租期。
   * 使用代表PDRL XML資料的字串值設定`PolicySpec`物件的`policyXml`資料成員。 若要執行此工作，請使用它的建構函式來建立.NET `StreamReader`物件。 將代表原則的PDRL XML檔案位置傳遞給`StreamReader`建構函式。 接著，叫用`StreamReader`物件的`ReadLine`方法，並將傳回值指派給字串變數。 反複執行`StreamReader`物件，直到`ReadLine`方法傳回null。 將字串變數指派給`PolicySpec`物件的`policyXml`資料成員。

1. 建立原則專案。

   使用Document Security Web服務API建立原則時，不需要建立原則專案。 原則專案是在PDRL檔案中定義的。

1. 註冊原則。

   透過叫用`DocumentSecurityServiceClient`物件的`registerPolicy`方法並傳遞下列值來登入原則：

   * 代表要註冊之原則的`PolicySpec`物件。
   * 字串值，代表原則所屬的原則集。 您可以指定`null`值，將原則新增至&#x200B;*MyPolices*&#x200B;原則集。

   如果您在連線設定內使用AEM表單管理員帳戶來建立`DocumentSecurityClient`物件，請在叫用`registerPolicy`方法時指定原則集名稱。

   如果您在連線設定中使用Document SecurityDocument Security使用者，則可以叫用僅接受原則的多載`registerPolicy`方法。 也就是說，您不需要指定原則集名稱。 但是，原則已新增至名為&#x200B;*我的原則*&#x200B;的原則集。 如果您不想將新原則新增至這個原則集，請在叫用`registerPolicy`方法時指定原則集名稱。

   >[!NOTE]
   >
   >在建立原則並指定原則集時，請確定您指定了現有的原則集。 如果您指定的原則集不存在，則會擲回例外狀況。

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API建立原則」
* 「快速入門(SwaRef)：使用網站服務API建立原則」

## 修改原則 {#modifying-policies}

您可以使用Document Security Java API或Web服務API修改現有原則。 若要變更現有原則，您可以擷取並修改它，然後在伺服器上更新原則。 例如，假設您擷取現有原則並延長其有效期。 在變更生效之前，您必須更新原則。

當業務需求變更且原則不再反映這些需求時，您可以修改原則。 您可以更新現有的原則，而不需要建立原則。

若要使用Web服務（例如，使用以JAX-WS建立的Java Proxy類別）修改原則屬性，您必須確保該原則已向Document Security服務註冊。 然後您可以使用`PolicySpec.getPolicyXml`方法參考現有原則，並使用適用方法修改原則屬性。 例如，您可以叫用`PolicySpec.setOfflineLeasePeriod`方法來修改離線租期。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

若要修改現有原則，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 擷取現有原則。
1. 變更原則屬性。
1. 更新原則。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security Client API物件**

您必須先建立Document Security服務使用者端物件，才能以程式設計方式執行Document Security服務操作。 如果您使用Java API，請建立`RightsManagementClient`物件。 如果您使用Document Security網站服務API，請建立`RightsManagementServiceService`物件。

**擷取現有的原則**

擷取現有原則以修改它。 若要擷取原則，請指定原則名稱和原則所屬的原則集。 如果您指定原則集名稱的`null`值，則會從&#x200B;*我的原則*&#x200B;原則集擷取原則。

**設定原則的屬性**

若要修改原則，請修改原則屬性的值。 唯一不能變更的原則屬性是名稱屬性。 例如，若要變更原則的離線租賃期間，您可以修改原則的離線租賃期間屬性的值。

使用Web服務修改原則的離線租期時，`PolicySpec`介面上的`offlineLeasePeriod`欄位會被忽略。 若要更新離線租期，請修改PDRL XML檔案中的`OfflineLeasePeriod`專案。 然後使用`PolicySpec`介面的`policyXML`資料成員，參考更新的PDRL XML檔案。

>[!NOTE]
>
>如需您可以設定的其他屬性相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`Policy`介面說明。

**更新原則**

在您對原則進行的變更生效之前，必須使用Document Security服務更新原則。 保護檔案的原則變更會在下次受原則保護的檔案與Document Security服務同步時更新。

### 使用Java API修改現有原則 {#modify-existing-policies-using-the-java-api}

使用Document Security API (Java)修改現有原則：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`RightsManagementClient`物件。

1. 擷取現有原則。

   * 呼叫`RightsManagementClient`物件的`getPolicyManager`方法，以建立`PolicyManager`物件。
   * 建立`Policy`物件，代表要更新的原則，方法是叫用`PolicyManager`物件的`getPolicy`方法，並傳遞下列值

      * 字串值，代表原則所屬的原則集名稱。 您可以指定導致使用`MyPolicies`原則集的`null`。
      * 代表原則名稱的字串值。

1. 設定原則的屬性。

   變更原則的屬性以符合您的業務需求。 例如，若要變更原則的離線租期，請叫用`Policy`物件的`setOfflineLeasePeriod`方法。

1. 更新原則。

   叫用`PolicyManager`物件的`updatePolicy`方法來更新原則。 傳遞代表要更新之原則的`Policy`物件。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱快速入門(SOAP模式)：使用Java API修改原則一節。

### 使用Web服務API修改現有原則 {#modify-existing-policies-using-the-web-service-api}

使用Document Security API （Web服務）修改現有原則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Document Security Client API物件。

   * 使用預設建構函式建立`RightsManagementServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`RightsManagementServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`RightsManagementServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取現有原則。

   建立代表要修改之原則的`PolicySpec`物件，方法是叫用`RightsManagementServiceClient`物件的`getPolicy`方法，並傳遞下列值：

   * 字串值，指定原則所屬的原則集名稱。 您可以指定導致使用`MyPolicies`原則集的`null`。
   * 字串值，指定原則的名稱。

1. 設定原則的屬性。

   變更原則的屬性以符合您的業務需求。

1. 更新原則。

   透過叫用`RightsManagementServiceClient`物件的`updatePolicyFromSDK`方法並傳遞代表要更新之原則的`PolicySpec`物件來更新原則。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API修改原則」
* 「快速入門(SwaRef)：使用網站服務API修改原則」

## 刪除原則 {#deleting-policies}

您可以使用Document Security Java API或Web服務API刪除現有原則。 原則刪除後，就無法再用來保護檔案。 但是，使用此原則的現有受原則保護檔案仍受保護。 您可以在有較新的原則可用時刪除原則。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

若要刪除現有原則，請執行下列步驟：

1. 包含專案檔案
1. 建立Document Security Client API物件。
1. 刪除原則。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security Client API物件**

您必須先建立Document Security服務使用者端物件，才能以程式設計方式執行Document Security服務操作。 如果您使用Java API，請建立`RightsManagementClient`物件。 如果您使用Document Security網站服務API，請建立`RightsManagementServiceService`物件。

**刪除原則**

若要刪除原則，您可以指定要刪除的原則以及該原則所屬的原則集。 使用設定來叫用AEM Forms的使用者必須擁有刪除原則的許可權；否則會發生例外狀況。 同樣地，如果您嘗試刪除不存在的原則，則會發生例外狀況。

### 使用Java API刪除原則 {#delete-policies-using-the-java-api}

使用Document Security API (Java)刪除原則：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`RightsManagementClient`物件。

1. 刪除原則。

   * 呼叫`RightsManagementClient`物件的`getPolicyManager`方法，以建立`PolicyManager`物件。
   * 叫用`PolicyManager`物件的`deletePolicy`方法並傳遞下列值以刪除原則：

      * 字串值，指定原則所屬的原則集名稱。 您可以指定導致使用`MyPolicies`原則集的`null`。
      * 字串值，指定要刪除的原則名稱。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(SOAP模式)：使用Java API刪除原則」

### 使用Web服務API刪除原則 {#delete-policies-using-the-web-service-api}

使用Document Security API （Web服務）刪除原則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Document Security Client API物件。

   * 使用預設建構函式建立`RightsManagementServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`RightsManagementServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`RightsManagementServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 刪除原則。

   叫用`RightsManagementServiceClient`物件的`deletePolicy`方法並傳遞下列值以刪除原則：

   * 字串值，指定原則所屬的原則集名稱。 您可以指定導致使用`MyPolicies`原則集的`null`。
   * 字串值，指定要刪除的原則名稱。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API刪除原則」
* 「快速入門(SwaRef)：使用網站服務API刪除原則」

## 套用原則至PDF檔案 {#applying-policies-to-pdf-documents}

您可以將原則套用至PDF檔案以保護檔案。 透過將原則套用到PDF檔案，您可以限制對檔案的存取權。 如果檔案已受原則保護，則無法將原則套用至檔案。

檔案開啟時，您也可以限制對Acrobat和Adobe Reader功能的存取，包括列印和複製文字、進行變更以及將簽名和註解新增到檔案的功能。 此外，當您不再需要使用者存取受原則保護的PDF檔案時，也可以撤銷該檔案。

您可以在分發受原則保護的檔案後，監視其使用情況。 也就是說，您可以看到檔案的使用方式以及誰正在使用它。 例如，您可以找出何時有人開啟了檔案。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-3}

若要將原則套用至PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 擷取套用了原則的PDF檔案。
1. 將現有原則套用至PDF檔案。
1. 儲存受原則保護的PDF檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security使用者端API物件**

在您以程式設計方式執行Document Security服務操作之前，請先建立Document Security服務使用者端物件。 如果您使用Java API，請建立`DocumentSecurityClient`物件。 如果您使用Document Security網站服務API，請建立`DocumentSecurityServiceService`物件。

**擷取PDF檔案**

您可以擷取PDF檔案以套用原則。 將原則套用至PDF檔案後，使用者使用檔案時會受到限制。 例如，如果原則未允許在離線時開啟檔案，則使用者必須線上上才能開啟檔案。

**將現有原則套用至PDF檔案**

若要將原則套用至PDF檔案，請參考現有原則並指定該原則所屬的原則集。 設定連線屬性的使用者必須擁有指定原則的存取權。 如果沒有，會發生例外狀況。

**儲存PDF檔案**

Document Security服務將原則套用至PDF檔案後，您可以將受原則保護的PDF檔案儲存為PDF檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[撤銷檔案的存取權](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API將原則套用至PDF檔案 {#apply-a-policy-to-a-pdf-document-using-the-java-api}

使用Document Security API (Java)將原則套用至PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`RightsManagementClient`物件。

1. 擷取PDF檔案。

   * 使用建構函式建立代表PDF檔案的`java.io.FileInputStream`物件。 傳遞字串值，指定PDF檔案的位置。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 將現有原則套用至PDF檔案。

   * 呼叫`RightsManagementClient`物件的`getDocumentManager`方法，以建立`DocumentManager`物件。
   * 呼叫`DocumentManager`物件的`protectDocument`方法並傳遞下列值，以將原則套用至PDF檔案：

      * 包含套用原則之PDF檔案的`com.adobe.idp.Document`物件。
      * 字串值，指定檔案的名稱。
      * 字串值，指定原則所屬的原則集名稱。 您可以指定導致使用`MyPolicies`原則集的`null`值。
      * 字串值，指定原則名稱。
      * 字串值，代表作為檔案發行者的使用者的使用者管理員網域名稱。 此引數值為選用值，可為Null （若此引數為Null，則下一個引數值必須為Null）。
      * 字串值，代表作為檔案發行者的使用者管理員使用者的正式名稱名稱。 此引數值是選用的，可以是`null` （如果此引數為Null，則先前的引數值必須是`null`）。
      * `com.adobe.livecycle.rightsmanagement.Locale`代表用於選取MS Office範本的區域設定。 此引數值為選用值，不用於PDF檔案。 若要保護PDF檔案的安全，請指定`null`。

     `protectDocument`方法傳回包含受原則保護的PDF檔案的`RMSecureDocumentResult`物件。

1. 儲存PDF檔案。

   * 叫用`RMSecureDocumentResult`物件的`getProtectedDoc`方法，以取得受原則保護的PDF檔案。 此方法會傳回`com.adobe.idp.Document`物件。
   * 建立`java.io.File`物件，並確定副檔名PDF。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`Document`物件的內容複製到檔案（請確定您使用的是`getProtectedDoc`方法傳回的`Document`物件）。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門（EJB模式）：使用Java API將原則套用至PDF檔案」
* 「快速入門(SOAP模式)：使用Java API將原則套用至PDF檔案」

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API套用原則至PDF檔案 {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

使用Document Security API （Web服務）將原則套用至PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Document Security Client API物件。

   * 使用預設建構函式建立`RightsManagementServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`RightsManagementServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至Forms服務（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`RightsManagementServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取PDF檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存套用原則的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表PDF檔案檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 取得`System.IO.FileStream`物件的`Length`屬性，以決定位元組陣列大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 將現有原則套用至PDF檔案。

   呼叫`RightsManagementServiceClient`物件的`protectDocument`方法並傳遞下列值，以將原則套用至PDF檔案：

   * 包含套用原則之PDF檔案的`BLOB`物件。
   * 字串值，指定檔案的名稱。
   * 字串值，指定原則所屬的原則集名稱。 您可以指定導致使用`MyPolicies`原則集的`null`值。
   * 字串值，指定原則名稱。
   * 字串值，代表作為檔案發行者的使用者的使用者管理員網域名稱。 此引數值是選用的，可以是null （若此引數為null，則下一個引數值必須是`null`）。
   * 字串值，代表作為檔案發行者的使用者管理員使用者的正式名稱名稱。 此引數值是選用的，可以是null （若此引數為null，則前一個引數值必須是`null`）。
   * 指定地區設定值的`RMLocale`值（例如，`RMLocale.en`）。
   * 用來儲存原則識別碼值的字串輸出引數。
   * 字串輸出引數，用來儲存受原則保護的識別碼值。
   * 用來儲存mime型別的字串輸出引數（例如，`application/pdf`）。

   `protectDocument`方法傳回包含受原則保護的PDF檔案的`BLOB`物件。

1. 儲存PDF檔案。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表受原則保護之PDF檔案的檔案位置的字串值。
   * 建立位元組陣列，儲存`protectDocument`方法傳回的`BLOB`物件的資料內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API將原則套用至PDF檔案」
* 「快速入門(SwaRef)：使用網站服務API將原則套用至PDF檔案」

## 從PDF檔案中移除原則 {#removing-policies-from-pdf-documents}

您可以從受原則保護的檔案中移除原則，以從檔案移除安全性。 亦即，如果您不再希望檔案受原則保護。 如果您想要使用較新的原則更新受原則保護的檔案，則切換原則會比移除原則並新增更新後的原則更有效率。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-4}

若要從受原則保護的PDF檔案中移除原則，請執行下列步驟：

1. 包含專案檔案
1. 建立Document Security Client API物件。
1. 擷取受原則保護的PDF檔案。
1. 從PDF檔案中移除原則。
1. 儲存不安全的PDF檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security Client API物件**

在您以程式設計方式執行Document Security服務操作之前，請先建立Document Security服務使用者端物件。

**擷取受原則保護的PDF檔案**

您可以擷取受原則保護的PDF檔案來移除原則。 如果您嘗試從不受原則保護的PDF檔案中移除原則，則會造成例外狀況。

**從PDF檔案中移除原則**

只要連線設定中指定了管理員，您就可以從受原則保護的PDF檔案中移除原則。 如果沒有，則用來保護檔案的原則必須包含`SWITCH_POLICY`許可權，才能從PDF檔案中移除原則。 此外，在AEM Forms連線設定中指定的使用者也必須具有該許可權。 否則，會擲回例外狀況。

**儲存不安全的PDF檔案**

Document Security服務從PDF檔案中移除原則後，您可以將不安全的PDF檔案儲存為PDF檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[套用原則至PDF檔案](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API從PDF檔案中移除一項原則 {#remove-a-policy-from-a-pdf-document-using-the-java-api}

使用Document Security API (Java)從受原則保護的PDF檔案中移除原則：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`DocumentSecurityClient`物件。

1. 擷取受原則保護的PDF檔案。

   * 使用受原則保護的PDF檔案的建構函式，並傳遞指定PDF檔案位置的字串值，來建立代表受原則保護的檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 從PDF檔案中移除原則。

   * 呼叫`DocumentSecurityClient`物件的`getDocumentManager`方法，以建立`DocumentManager`物件。
   * 叫用`DocumentManager`物件的`removeSecurity`方法，並傳遞包含受原則保護的PDF檔案的`com.adobe.idp.Document`物件，以從PDF檔案中移除原則。 此方法傳回包含不安全PDF檔案的`com.adobe.idp.Document`物件。

1. 儲存不安全的PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名PDF。
   * 叫用`Document`物件的`copyToFile`方法，將`Document`物件的內容複製到檔案（請確定您使用的是`removeSecurity`方法傳回的`Document`物件）。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(SOAP模式)：使用Java API從PDF檔案中移除原則」

### 使用Web服務API移除原則 {#remove-a-policy-using-the-web-service-api}

使用Document Security API （Web服務），從受原則保護的PDF檔案中移除原則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Document Security Client API物件。

   * 使用預設建構函式建立`DocumentSecurityServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`DocumentSecurityServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`DocumentSecurityServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取受原則保護的PDF檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存受原則保護的PDF檔案，原則會從中移除。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表PDF檔案檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 從PDF檔案中移除原則。

   叫用`DocumentSecurityServiceClient`物件的`removePolicySecurity`方法，並傳遞包含受原則保護的PDF檔案的`BLOB`物件，以從PDF檔案中移除原則。 此方法傳回包含不安全PDF檔案的`BLOB`物件。

1. 儲存不安全的PDF檔案。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表不安全PDF檔案檔案位置的字串值。
   * 建立位元組陣列，儲存`removePolicySecurity`方法傳回的`BLOB`物件的資料內容。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API從PDF檔案中移除原則」
* 「快速入門(SwaRef)：使用網站服務API從PDF檔案中移除原則」

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 撤銷檔案的存取權 {#revoking-access-to-documents}

您可以撤銷受原則保護之PDF檔案的存取權，導致使用者無法存取該檔案的所有復本。 當使用者嘗試開啟撤銷的PDF檔案時，他們被重新導向到指定的URL，其中可檢視修訂的檔案。 必須以程式設計方式指定要將使用者重新導向到的URL。 當您撤銷對檔案的存取時，此變更會在下次使用者透過線上開啟受原則保護的檔案與Document Security服務同步時生效。

撤銷檔案存取權的功能提供額外的安全性。 例如，假設有較新版本的檔案可用，並且您不再希望任何人檢視過時的版本。 在此情況下，對舊檔案的存取權可能會被撤銷，除非恢復存取權，否則沒有人可以檢視該檔案。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-5}

若要撤銷受原則保護的檔案，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 擷取受原則保護的PDF檔案。
1. 撤銷受原則保護的檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security Client API物件**

您必須先建立Document Security服務使用者端物件，才能以程式設計方式執行Document Security服務操作。

**擷取受原則保護的PDF檔案**

擷取受原則保護的PDF檔案以將其撤銷。 您無法撤銷已撤銷或不是受原則保護檔案的檔案。

如果您知道受原則保護檔案的授權識別碼值，則不必擷取受原則保護的PDF檔案。 但是，在大多數情況下，您必須擷取PDF檔案才能取得許可證識別碼值。

**撤銷受原則保護的檔案**

若要撤銷受原則保護的檔案，請指定受原則保護檔案的授權識別碼。 此外，您可以指定當使用者嘗試開啟撤銷的檔案時，可檢視的檔案URL。 也就是說，假設過期的檔案被撤銷。 當使用者嘗試開啟撤銷的檔案時，他們會看到更新檔案，而不是撤銷的檔案。

>[!NOTE]
>
>如果您嘗試撤銷已撤銷的檔案，則會擲回例外狀況。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[套用原則至PDF檔案](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[恢復對已撤銷檔案的存取權](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### 使用Java API撤銷檔案的存取權 {#revoke-access-to-documents-using-the-java-api}

使用Document Security API (Java)撤銷受原則保護的PDF檔案存取權：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security使用者端API物件

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`DocumentSecurityClient`物件。

1. 擷取受原則保護的PDF檔案

   * 使用受原則保護的PDF檔案的建構函式，並傳遞指定PDF檔案位置的字串值，來建立代表受原則保護的檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 撤銷受原則保護的檔案

   * 呼叫`DocumentSecurityClient`物件的`getDocumentManager`方法，以建立`DocumentManager`物件。
   * 透過叫用`DocumentManager`物件的`getLicenseId`方法，擷取受原則保護檔案的授權識別碼值。 傳遞代表受原則保護檔案的`com.adobe.idp.Document`物件。 此方法會傳回代表授權識別碼值的字串值。
   * 呼叫`DocumentSecurityClient`物件的`getLicenseManager`方法，以建立`LicenseManager`物件。
   * 叫用`LicenseManager`物件的`revokeLicense`方法並傳遞下列值，以撤銷受原則保護的檔案：

      * 字串值，指定受原則保護檔案的授權識別碼值（指定`DocumentManager`物件的`getLicenseId`方法的傳回值）。
      * `License`介面的靜態資料成員，指定撤銷檔案的原因。 例如，您可以指定`License.DOCUMENT_REVISED`。
      * 指定修訂檔案所在位置的`java.net.URL`值。 如果您不想將使用者重新導向至其他URL，則可以傳遞`null`。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(SOAP模式)：使用Java API撤銷檔案」

### 使用Web服務API撤銷檔案的存取權 {#revoke-access-to-documents-using-the-web-service-api}

使用Document Security API （Web服務）撤銷受原則保護的PDF檔案存取權：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Document Security使用者端API物件

   * 使用預設建構函式建立`DocumentSecurityServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`DocumentSecurityServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`DocumentSecurityServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取受原則保護的PDF檔案

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存已撤銷的受原則PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表要撤銷之受原則保護之PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 撤銷受原則保護的檔案

   * 透過叫用`DocumentSecurityServiceClient`物件的`getLicenseID`方法並傳遞代表受原則保護檔案的`BLOB`物件來擷取受原則保護檔案的授權識別碼值。 此方法會傳回代表授權識別碼的字串值。
   * 叫用`DocumentSecurityServiceClient`物件的`revokeLicense`方法並傳遞下列值，以撤銷受原則保護的檔案：

      * 字串值，指定受原則保護檔案的授權識別碼值（指定`DocumentSecurityServiceService`物件的`getLicenseId`方法的傳回值）。
      * `Reason`列舉的靜態資料成員，指定撤銷檔案的原因。 例如，您可以指定`Reason.DOCUMENT_REVISED`。
      * `string`值，指定修訂檔案所在的URL位置。 如果您不想將使用者重新導向至其他URL，則可以傳遞`null`。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API撤銷檔案」
* 「快速入門(SwaRef)：使用網站服務API撤銷檔案」

**另請參閱**

[從Word檔案移除原則](protecting-documents-policies.md#removing-policies-from-word-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 恢復對已撤銷檔案的存取權 {#reinstating-access-to-revoked-documents}

您可以恢復對已撤銷PDF檔案的存取權，讓使用者能夠存取已撤銷檔案的所有復本。 當使用者開啟已撤銷的恢復檔案時，使用者將能夠檢視檔案。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-6}

若要恢復已撤銷PDF檔案的存取權，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 擷取撤銷PDF檔案的授權識別碼。
1. 恢復已撤銷PDF檔案的存取權。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security Client API物件**

您必須先建立Document Security服務使用者端物件，才能以程式設計方式執行Document Security服務操作。 如果您使用Java API，請建立`DocumentSecurityClient`物件。 如果您使用Document Security網站服務API，請建立`DocumentSecurityServiceService`物件。

**擷取已撤銷PDF檔案的授權識別碼**

擷取已撤銷PDF檔案的授權識別碼，以復原已撤銷PDF檔案。 取得授權識別碼值後，即可恢復撤銷的檔案。 如果您嘗試恢復未撤銷的檔案，則會造成例外狀況。

**恢復已撤銷PDF檔案的存取權**

若要恢復對已撤銷PDF檔案的存取權，您必須指定已撤銷檔案的授權識別碼。 如果您嘗試恢復未撤銷之PDF檔案的存取權，則會造成例外狀況。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[套用原則至PDF檔案](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[撤銷檔案的存取權](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API恢復對已撤銷檔案的存取權 {#reinstate-access-to-revoked-documents-using-the-java-api}

使用Document Security API (Java)恢復對已撤銷檔案的存取權：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`DocumentSecurityClient`物件。

1. 擷取撤銷PDF檔案的授權識別碼。

   * 使用物件的建構函式並傳遞指定PDF檔案位置的字串值，建立代表已撤銷PDF檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。
   * 呼叫`DocumentSecurityClient`物件的`getDocumentManager`方法，以建立`DocumentManager`物件。
   * 叫用`DocumentManager`物件的`getLicenseId`方法並傳遞代表撤銷檔案的`com.adobe.idp.Document`物件，以擷取撤銷檔案的授權識別碼值。 此方法會傳回代表授權識別碼的字串值。

1. 恢復已撤銷PDF檔案的存取權。

   * 呼叫`DocumentSecurityClient`物件的`getLicenseManager`方法，以建立`LicenseManager`物件。
   * 透過叫用`LicenseManager`物件的`unrevokeLicense`方法並傳遞撤銷檔案的授權識別碼值，恢復對已撤銷PDF檔案的存取。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(SOAP模式)：使用網站服務API恢復對已撤銷檔案的存取權」

### 使用網站服務API恢復對已撤銷檔案的存取 {#reinstate-access-to-revoked-documents-using-the-web-service-api}

使用Document Security API （網頁服務）恢復對已撤銷檔案的存取權：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Document Security Client API物件。

   * 使用預設建構函式建立`DocumentSecurityServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`DocumentSecurityServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`DocumentSecurityServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取撤銷PDF檔案的授權識別碼。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存已撤銷的PDF檔案，存取權已恢復到該檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表已撤銷PDF檔案的檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 恢復已撤銷PDF檔案的存取權。

   * 叫用`DocumentSecurityServiceClient`物件的`getLicenseID`方法並傳遞代表撤銷檔案的`BLOB`物件，以擷取撤銷檔案的授權識別碼值。 此方法會傳回代表授權識別碼的字串值。
   * 透過叫用`DocumentSecurityServiceClient`物件的`unrevokeLicense`方法並傳遞字串值來恢復對已撤銷PDF檔案的存取，該字串值指定已撤銷PDF檔案的授權識別碼值（傳遞`DocumentSecurityServiceClient`物件的`getLicenseId`方法的傳回值）。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API恢復對已撤銷檔案的存取權」
* 「快速入門(SwaRef)：使用網站服務API恢復對已撤銷檔案的存取權」

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 檢查受原則保護的PDF檔案 {#inspecting-policy-protected-pdf-documents}

您可以使用Document Security Service API （Java和Web服務）來檢查受原則保護的PDF檔案。 檢查受原則保護的PDF檔案會傳回受原則保護的PDF檔案的相關資訊。 例如，您可以決定用來保護檔案的原則以及保護檔案的日期。

如果您的LiveCycle版本是8.x或較舊的版本，則無法執行此工作。 AEM Forms已新增檢查受原則保護檔案的支援。 如果您嘗試使用LiveCycle8.x （或更早版本）檢查受原則保護的檔案，會發生例外狀況。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-7}

若要檢查受原則保護的PDF檔案，請執行以下步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 擷取受原則保護的檔案以進行檢查。
1. 取得受原則保護檔案的相關資訊。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security Client API物件**

在您以程式設計方式執行Document Security服務操作之前，請先建立Document Security服務使用者端物件。 如果您使用Java API，請建立`RightsManagementClient`物件。 如果您使用Document Security網站服務API，請建立`RightsManagementServiceService`物件。

**擷取受原則保護的檔案以檢查**

若要檢查受原則保護的檔案，請擷取該檔案。 如果您嘗試檢查未受原則保護或已撤銷的檔案，則會擲回例外狀況。

**Inspect檔案**

擷取受原則保護的檔案後，即可加以檢查。

**取得受原則保護檔案的相關資訊**

檢查受原則保護的PDF檔案後，即可取得相關資訊。 例如，您可以決定用來保護檔案的原則。

如果您使用屬於我的原則的原則來保護檔案，然後呼叫`RMInspectResult.getPolicysetName`或`RMInspectResult.getPolicysetId`，則會傳回null。

如果檔案是使用包含在原則集（除了「我的原則」）中的原則進行保護，則`RMInspectResult.getPolicysetName`和`RMInspectResult.getPolicysetId`會傳回有效的字串。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API的Inspect受原則保護的PDF檔案 {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspect使用Document Security Service API (Java)提供受原則保護的PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。 如需這些檔案位置的相關資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 建立Document Security Client API物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。 （請參閱[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`RightsManagementClient`物件。

1. 擷取受原則保護的檔案以進行檢查。

   * 使用受原則保護的PDF檔案的建構函式，建立代表該檔案的`java.io.FileInputStream`物件。 傳遞字串值，指定PDF檔案的位置。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. Inspect檔案。

   * 呼叫`RightsManagementClient`物件的`getDocumentManager`方法，以建立`DocumentManager`物件。
   * 叫用`LicenseManager`物件的`inspectDocument`方法，以Inspect受原則保護的檔案。 傳遞包含受原則保護的PDF檔案的`com.adobe.idp.Document`物件。 此方法會傳回包含受原則保護檔案相關資訊的`RMInspectResult`物件。

1. 取得受原則保護檔案的相關資訊。

   若要取得受原則保護檔案的相關資訊，請叫用屬於`RMInspectResult`物件的適當方法。 例如，若要擷取原則名稱，請叫用`RMInspectResult`物件的`getPolicyName`方法。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(SOAP模式)：使用Java API檢查受原則保護的PDF檔案」

### 使用Web服務API的Inspect受原則保護的PDF檔案 {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspect使用Document Security Service API （網頁服務）撰寫受原則保護的PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Document Security Client API物件。

   * 使用預設建構函式建立`RightsManagementServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`RightsManagementServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`RightsManagementServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取受原則保護的檔案以進行檢查。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存要檢查的PDF檔案。
   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表PDF檔案檔案位置的字串值以及開啟檔案的模式。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、開始位置和串流長度以讀取。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. Inspect檔案。

   叫用`RightsManagementServiceClient`物件的`inspectDocument`方法，以Inspect受原則保護的檔案。 傳遞包含受原則保護的PDF檔案的`BLOB`物件。 此方法會傳回包含受原則保護檔案相關資訊的`RMInspectResult`物件。

1. 取得受原則保護檔案的相關資訊。

   若要取得受原則保護檔案的相關資訊，請取得屬於`RMInspectResult`物件的適當欄位值。 例如，若要擷取原則名稱，請取得`RMInspectResult`物件的`policyName`欄位的值。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API檢查受原則保護的PDF檔案」
* 「快速入門(SwaRef)：使用網站服務API檢查受原則保護的PDF檔案」

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 建立浮水印 {#creating-watermarks}

浮水印可唯一識別檔案並控制侵犯版權，以協助確保檔案的安全性。 例如，您可以建立並放置浮水印，在檔案的所有頁面上顯示「機密」。 建立浮水印後，您可以將其納入原則中。 也就是說，您可以使用新建立的浮水印來設定原則的浮水印屬性。 將包含浮水印的原則套用至檔案後，浮水印會顯示在受原則保護的檔案中。

>[!NOTE]
>
>只有具有Document Security管理員許可權的使用者才能建立浮水印。 也就是說，在定義建立Document Security服務使用者端物件所需的連線設定時，您必須指定這類使用者。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-8}

若要建立浮水印，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 設定浮水印屬性。
1. 向Document Security服務註冊浮水印。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security Client API物件**

您必須先建立Document Security服務使用者端物件，才能以程式設計方式執行Document Security服務操作。 如果您使用Java API，請建立`RightsManagementClient`物件。 如果您使用Document Security網站服務API，請建立`RightsManagementServiceService`物件。

**設定浮水印屬性**

若要建立浮水印，您必須設定浮水印屬性。 必須一律定義name屬性。 除了name屬性之外，您至少必須設定下列其中一個屬性：

* 自訂文字
* DateInclude
* UserIdInclude
* UserNameInclude

下表列出使用Web服務建立浮水印時所需的索引鍵和值配對。

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
   <td><p>指定開啟檔案之使用者的使用者名稱是否屬於浮水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>指定開啟檔案的使用者識別碼是否為浮水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>指定目前的日期是否為浮水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>如果此值為true，則必須使用<code>WaterBackCmd:SRCTEXT</code>指定自訂文字的值。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>指定浮水印的不透明度。 若未指定，預設值為0.5。</p></td>
   <td><p>介於0.0和1.0之間的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>指定浮水印的旋轉。 預設值為0度。</p></td>
   <td><p>介於0到359的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>如果指定此值，則必須有<code>WaterBackCmd:IS_SIZE_ENABLED</code>且值必須為true。 如果未指定此屬性，預設行為會適合頁面。</p></td>
   <td><p>大於0.0且小於或等於1.0的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>指定浮水印的水準對齊方式。 預設值為center。</p></td>
   <td><p>左、中或右</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>指定浮水印的垂直對齊方式。 預設值為center。</p></td>
   <td><p>上、中或下</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>指定浮水印是否為背景。 預設值為false。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>如果指定了自訂比例，則為True。 如果此值為true，則必須指定SCALE。 如果此值為false，則預設為適合頁面。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>指定浮水印的自訂文字。 如果此值存在，則<code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code>也必須存在並設定為true。</p></td>
   <td><p>True或False</p></td>
  </tr>
 </tbody>
</table>

所有浮水印都必須定義下列其中一個屬性：

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

所有其他屬性都是選用的。

**登入浮水印**

新的浮水印必須先向Document Security服務註冊，才能使用。 註冊浮水印後，即可在原則內使用。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[套用原則至PDF檔案](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API建立浮水印 {#create-watermarks-using-the-java-api}

使用Document Security API (Java)建立浮水印：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如`adobe-rightsmanagement-client.jar`。

1. 建立Document Security Client API物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`RightsManagementClient`物件。

1. 設定浮水印屬性

   * 呼叫`InfomodelObjectFactory`物件的靜態`createWatermark`方法，以建立`Watermark`物件。 此方法會傳回`Watermark`物件。
   * 透過叫用`Watermark`物件的`setName`方法並傳遞指定原則名稱的字串值來設定浮水印的名稱屬性。
   * 透過叫用`Watermark`物件的`setBackground`方法並傳遞`true`來設定浮水印的背景屬性。 透過設定此屬性，浮水印會出現在檔案的背景中。
   * 透過叫用`Watermark`物件的`setCustomText`方法並傳遞代表浮水印文字的字串值來設定浮水印的自訂文字屬性。
   * 透過叫用`Watermark`物件的`setOpacity`方法並傳遞指定不透明度等級的整數值來設定浮水印的不透明度屬性。 值100表示浮水印完全不透明，值0表示浮水印完全透明。

1. 註冊浮水印。

   * 呼叫`RightsManagementClient`物件的`getWatermarkManager`方法，以建立`WatermarkManager`物件。 此方法會傳回`WatermarkManager`物件。
   * 透過叫用`WatermarkManager`物件的`registerWatermark`方法並傳遞代表浮水印的`Watermark`物件來登入浮水印。 此方法會傳回代表浮水印識別值的字串值。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(SOAP模式)：使用Java API建立浮水印」

### 使用網站服務API建立浮水印 {#create-watermarks-using-the-web-service-api}

使用Document Security API （網頁服務）建立浮水印：

1. 建立Document Security Client API物件。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Document Security Client API物件。

   * 使用預設建構函式建立`RightsManagementServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`RightsManagementServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`RightsManagementServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 設定浮水印屬性。

   * 呼叫`WatermarkSpec`建構函式以建立`WatermarkSpec`物件。
   * 將字串值指派給`WatermarkSpec`物件的`name`資料成員，以設定浮水印的名稱。
   * 將字串值指派給`WatermarkSpec`物件的`id`資料成員，以設定浮水印的`id`屬性。
   * 若要設定每個浮水印屬性，請建立個別的`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。
   * 將值指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`key`資料成員（例如`WaterBackCmd:OPACITY)`），以設定索引鍵值。
   * 將值指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`value`資料成員（例如`.25`）以設定值。
   * 建立`MyArrayOf_xsd_anyType`物件。 針對每個`MyMapOf_xsd_string_To_xsd_anyType_Item`物件，叫用`MyArrayOf_xsd_anyType`物件的`Add`方法。 傳遞`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。
   * 將`MyArrayOf_xsd_anyType`物件指派給`WatermarkSpec`物件的`values`資料成員。

1. 註冊浮水印。

   透過叫用`RightsManagementServiceClient`物件的`registerWatermark`方法並傳遞代表浮水印的`WatermarkSpec`物件來登入浮水印。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API建立浮水印」
* 「快速入門(SwaRef)：使用網站服務API建立浮水印」

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改浮水印 {#modifying-watermarks}

您可以使用Document Security Java API或網站服務API修改現有的浮水印。 若要變更現有的浮水印，您可以擷取浮水印、修改其屬性，然後在伺服器上更新浮水印。 例如，假設您擷取浮水印並修改其不透明度屬性。 在變更生效之前，您必須更新浮水印。

當您修改浮水印時，此變更會影響已套用浮水印的未來檔案。 也就是說，包含浮水印的現有PDF檔案不受影響。

>[!NOTE]
>
>只有具有Document Security管理員許可權的使用者才能修改浮水印。 也就是說，在定義建立Document Security服務使用者端物件所需的連線設定時，您必須指定這類使用者。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-9}

若要修改浮水印，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 擷取要修改的浮水印。
1. 設定浮水印屬性。
1. 更新浮水印。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security Client API物件**

您必須先建立Document Security服務使用者端物件，才能以程式設計方式執行Document Security服務操作。 如果您使用Java API，請建立`DocumentSecurityClient`物件。 如果您使用Document Security網站服務API，請建立`DocumentSecurityServiceService`物件。

**擷取浮水印以修改**

若要修改浮水印，您必須擷取現有的浮水印。 您可以指定浮水印名稱或指定其識別碼值來擷取浮水印。

**設定浮水印屬性**

若要修改現有的浮水印，請變更一或多個浮水印屬性的值。 使用Web服務以程式設計方式更新浮水印時，您必須設定所有最初設定的屬性，即使值未變更亦然。 例如，假設已設定下列浮水印屬性： `WaterBackCmd:IS_USERID_ENABLED`、`WaterBackCmd:IS_CUSTOMTEXT_ENABLED`、`WaterBackCmd:OPACITY`和`WaterBackCmd:SRCTEXT`。 雖然您唯一要修改的屬性是`WaterBackCmd:OPACITY`，但您必須設定其他正確的值。

>[!NOTE]
>
>使用Java API修改浮水印時，您不需要指定所有屬性。 設定您要修改的浮水印屬性。

>[!NOTE]
>
>如需有關浮水印屬性名稱的資訊，請參閱[建立浮水印](protecting-documents-policies.md#creating-watermarks)。

**更新浮水印**

修改浮水印的屬性之後，您必須更新浮水印。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[建立浮水印](protecting-documents-policies.md#creating-watermarks)

### 使用Java API修改浮水印 {#modify-watermarks-using-the-java-api}

使用Document Security API (Java)修改浮水印：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`DocumentSecurityClient`物件。

1. 擷取要修改的浮水印。

   叫用`DocumentSecurityClient`物件的`getWatermarkManager`方法建立`WatermarkManager`物件，並傳遞指定浮水印名稱的字串值。 此方法會傳回代表要修改之浮水印的`Watermark`物件。

1. 設定浮水印屬性。

   透過叫用`Watermark`物件的`setOpacity`方法並傳遞指定不透明度等級的整數值來設定浮水印的不透明度屬性。 值100表示浮水印完全不透明，值0表示浮水印完全透明。

   >[!NOTE]
   >
   >此範例只會修改不透明度屬性。

1. 更新浮水印。

   * 透過叫用`WatermarkManager`物件的`updateWatermark`方法更新浮水印，並傳遞其屬性被修改的`Watermark`物件。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱快速入門(SOAP模式)：使用Java API修改浮水印一節。

### 使用網站服務API修改浮水印 {#modify-watermarks-using-the-web-service-api}

使用Document Security API （Web服務）修改浮水印：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Document Security Client API物件。

   * 使用預設建構函式建立`DocumentSecurityServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`RightsManagementServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/DocumentSecurityService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`DocumentSecurityServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取要修改的浮水印。

   透過叫用`DocumentSecurityServiceClient`物件的`getWatermarkByName`方法擷取要修改的浮水印。 傳遞指定浮水印名稱的字串值。 此方法會傳回代表要修改之浮水印的`WatermarkSpec`物件。

1. 設定浮水印屬性。

   * 若要更新每個浮水印屬性，請建立個別的`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。
   * 將值指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`key`資料成員（例如`WaterBackCmd:OPACITY)`），以設定索引鍵值。
   * 將值指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`value`資料成員（例如`.50`）以設定值。
   * 建立`MyArrayOf_xsd_anyType`物件。 針對每個`MyMapOf_xsd_string_To_xsd_anyType_Item`物件，叫用`MyArrayOf_xsd_anyType`物件的`Add`方法。 傳遞`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。
   * 將`MyArrayOf_xsd_anyType`物件指派給`WatermarkSpec`物件的`values`資料成員。

1. 更新浮水印。

   呼叫`DocumentSecurityServiceClient`物件的`updateWatermark`方法，並傳遞代表要修改之浮水印的`WatermarkSpec`物件，以更新浮水印。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API修改浮水印」

## 搜尋事件 {#searching-for-events}

Rights Management服務會在特定動作發生時加以追蹤，例如將原則套用至檔案、開啟受原則保護的檔案，以及撤銷對檔案的存取權。 必須為Rights Management服務啟用事件稽核，否則不會追蹤事件。

事件分為下列類別之一：

* 管理員事件是與管理員相關的動作，例如建立管理員帳戶。
* 檔案事件是與檔案相關的動作，例如關閉受原則保護的檔案。
* 原則事件是與原則相關的動作，例如建立原則。
* 服務事件是與Rights Management服務相關的動作，例如與使用者目錄同步。

您可以使用Rights ManagementJava API或網站服務API來搜尋指定特定事件。 透過搜尋事件，您可以執行工作，例如建立特定事件的記錄檔。

>[!NOTE]
>
>如需Rights Management服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-10}

若要搜尋Rights Management事件，請執行下列步驟：

1. 包含專案檔案。
1. 建立Rights Management使用者端API物件。
1. 指定要搜尋的事件。
1. 搜尋事件。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Rights Management使用者端API物件**

您必須先建立Rights Management服務使用者端物件，才能以程式設計方式執行Rights Management服務作業。 如果您使用Java API，請建立`DocumentSecurityClient`物件。 如果您使用Rights ManagementWeb服務API，請建立`DocumentSecurityServiceService`物件。

**指定要搜尋的事件**

指定要搜尋的事件。 例如，您可以搜尋原則建立事件，這會在建立新原則時發生。

**搜尋事件**

指定要搜尋的事件後，您可以使用Rights ManagementJava API或Rights ManagementWeb服務API來搜尋事件。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API搜尋事件 {#search-for-events-using-the-java-api}

使用Rights Management API (Java)搜尋事件：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Rights Management使用者端API物件

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`DocumentSecurityClient`物件。

1. 指定要搜尋的事件

   * 呼叫`DocumentSecurityClient`物件的`getEventManager`方法，以建立`EventManager`物件。 此方法傳回`EventManager`物件。
   * 透過叫用它的建構函式來建立`EventSearchFilter`物件。
   * 叫用`EventSearchFilter`物件的`setEventCode`方法，並傳遞屬於代表要搜尋之事件的`EventManager`類別的靜態資料成員，以指定要搜尋的事件。 例如，若要搜尋原則建立事件，請傳遞`EventManager.POLICY_CREATE_EVENT`。

   >[!NOTE]
   >
   >您可以叫用`EventSearchFilter`物件方法來定義其他搜尋條件。 例如，叫用`setUserName`方法以指定與事件相關聯的使用者。

1. 搜尋事件

   叫用`EventManager`物件的`searchForEvents`方法並傳遞定義事件搜尋准則的`EventSearchFilter`物件來搜尋事件。 此方法傳回`Event`物件的陣列。

**程式碼範例**

如需使用Rights Management服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(SOAP)：使用Java API搜尋事件」

### 使用網站服務API搜尋事件 {#search-for-events-using-the-web-service-api}

使用Rights Management API （網站服務）搜尋事件：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Rights Management使用者端API物件

   * 使用預設建構函式建立`DocumentSecurityServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`DocumentSecurityServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`DocumentSecurityServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 指定要搜尋的事件

   * 使用物件的建構函式建立`EventSpec`物件。
   * 藉由設定`EventSpec`物件的`firstTime.date`資料成員的`DataTime`執行個體（代表事件發生時日期範圍的開始），指定事件發生期間的開始。
   * 將值`true`指派給`EventSpec`物件的`firstTime.dateSpecified`資料成員。
   * 藉由設定`EventSpec`物件的`lastTime.date`資料成員的`DataTime`執行個體（代表事件發生時日期範圍的結尾），指定事件發生期間的時間段結尾。
   * 將值`true`指派給`EventSpec`物件的`lastTime.dateSpecified`資料成員。
   * 將字串值指派給`EventSpec`物件的`eventCode`資料成員，以設定要搜尋的事件。 下表列出您可以指派給此屬性的數值：

   <table>
    <thead>
    <tr>
    <th><p>事件型別</p></th>
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

   叫用`DocumentSecurityServiceClient`物件的`searchForEvents`方法並傳遞代表要搜尋之事件和結果數目上限的`EventSpec`物件來搜尋事件。 此方法會傳回`MyArrayOf_xsd_anyType`集合，其中每個元素都是`AuditSpec`執行個體。 使用`AuditSpec`執行個體，您可以取得事件的相關資訊，例如發生時間。 `AuditSpec`執行個體包含指定此資訊的`timestamp`資料成員。

**程式碼範例**

如需使用Rights Management服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API搜尋事件」
* 「快速入門(SwaRef)：使用網站服務API搜尋事件」

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將原則套用至Word檔案 {#applying-policies-to-word-documents}

除了PDF檔案之外，Rights Management服務也支援其他檔案格式，例如Microsoft Word檔案（DOC檔案）和其他Microsoft Office檔案格式。 例如，您可以將原則套用至Word檔案來保護它。 將原則套用至Word檔案後，您就可以限制對檔案的存取權。 如果檔案已受原則保護，則無法將原則套用至檔案。

您可以在分發受原則保護的Word檔案後，監視其使用情況。 也就是說，您可以看到檔案的使用方式以及誰正在使用它。 例如，您可以找出何時有人開啟了檔案。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-11}

若要將原則套用至Word檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security Client API物件。
1. 擷取套用了原則的Word檔案。
1. 將現有原則套用至Word檔案。
1. 儲存受原則保護的Word檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security使用者端API物件**

您必須先建立Document Security服務使用者端物件，才能以程式設計方式執行Document Security服務操作。

**擷取Word檔案**

擷取Word檔案以套用原則。 將原則套用至Word檔案之後，使用者使用檔案時會受到限制。 例如，如果原則未允許在離線時開啟檔案，則使用者必須線上上才能開啟檔案。

**將現有原則套用至Word檔案**

若要將原則套用至Word檔案，您必須參考現有原則並指定該原則所屬的原則集。 設定連線屬性的使用者必須擁有指定原則的存取權。 如果沒有，會發生例外狀況。

**儲存Word檔案**

Document Security服務將原則套用至Word檔案後，您就可以將受原則保護的Word檔案儲存為DOC檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[撤銷檔案的存取權](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API將原則套用至Word檔案 {#apply-a-policy-to-a-word-document-using-the-java-api}

使用Document Security API (Java)將原則套用至Word檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security Client API物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`DocumentSecurityClient`物件。

1. 擷取Word檔案。

   * 使用它的建構函式並傳遞指定Word檔案位置的字串值，建立代表Word檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 將現有原則套用至Word檔案。

   * 呼叫`DocumentSecurityClient`物件的`getDocumentManager`方法，以建立`DocumentManager`物件。
   * 叫用`DocumentManager`物件的`protectDocument`方法並傳遞下列值，將原則套用至Word檔案：

      * 包含套用原則之Word檔案的`com.adobe.idp.Document`物件。
      * 字串值，指定檔案的名稱。
      * 字串值，指定原則所屬的原則集名稱。 您可以指定導致使用`MyPolicies`原則集的`null`值。
      * 字串值，指定原則名稱。
      * 字串值，代表作為檔案發行者的使用者的使用者管理員網域名稱。 此引數值為選用值，可為Null （若此引數為Null，則下一個引數值必須為Null）。
      * 字串值，代表作為檔案發行者的使用者管理員使用者的正式名稱名稱。 此引數值是選用的，可以是`null` （如果此引數是`null`，則前一個引數值必須是`null`）。
      * `com.adobe.livecycle.rightsmanagement.Locale`代表用於選取MS Office範本的區域設定。 此引數值是選用的，您可以指定`null`。

     `protectDocument`方法傳回包含受原則保護的Word檔案的`RMSecureDocumentResult`物件。

1. 儲存Word檔案。

   * 叫用`RMSecureDocumentResult`物件的`getProtectedDoc`方法，以取得受原則保護的Word檔案。 此方法會傳回`com.adobe.idp.Document`物件。
   * 建立`java.io.File`物件，並確定副檔名為DOC。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`Document`物件的內容複製到檔案（請確定您使用的是`getProtectedDoc`方法傳回的`Document`物件）。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(SOAP模式)：使用Java API將原則套用至Word檔案」

### 使用網站服務API將原則套用至Word檔案 {#apply-a-policy-to-a-word-document-using-the-web-service-api}

使用Document Security API （Web服務）將原則套用至Word檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Document Security Client API物件。

   * 使用預設建構函式建立`DocumentSecurityServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`DocumentSecurityServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/DocumentSecurityService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`DocumentSecurityServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取Word檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存套用原則的Word檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表Word檔案檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 取得`System.IO.FileStream`物件的`Length`屬性，以決定位元組陣列大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 將現有原則套用至Word檔案。

   叫用`DocumentSecurityServiceClient`物件的`protectDocument`方法並傳遞下列值，將原則套用至Word檔案：

   * 包含套用原則之Word檔案的`BLOB`物件。
   * 字串值，指定檔案的名稱。
   * 字串值，指定原則所屬的原則集名稱。 您可以指定導致使用`MyPolicies`原則集的`null`值。
   * 字串值，指定原則名稱。
   * 字串值，代表作為檔案發行者的使用者的使用者管理員網域名稱。 此引數值是選用的，可以是null （若此引數為null，則下一個引數值必須是`null`）。
   * 字串值，代表作為檔案發行者的使用者管理員使用者的正式名稱名稱。 此引數值是選用的，可以是null （若此引數為null，則前一個引數值必須是`null`）。
   * 指定地區設定值的`RMLocale`值（例如，`RMLocale.en`）。
   * 用來儲存原則識別碼值的字串輸出引數。
   * 字串輸出引數，用來儲存受原則保護的識別碼值。
   * 用來儲存mime型別的字串輸出引數（例如，`application/doc`）。

   `protectDocument`方法傳回包含受原則保護的Word檔案的`BLOB`物件。

1. 儲存Word檔案。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表受原則保護之Word檔案的檔案位置的字串值。
   * 建立位元組陣列，儲存`protectDocument`方法傳回的`BLOB`物件的資料內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入Word檔案。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API將原則套用至Word檔案」

## 從Word檔案移除原則 {#removing-policies-from-word-documents}

您可以從受原則保護的Word檔案中移除原則，以從檔案中移除安全性。 亦即，如果您不再希望檔案受原則保護。 如果您想要使用較新的原則更新受原則保護的Word檔案，則切換原則比移除原則並新增更新原則更有效率。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-12}

若要從受原則保護的Word檔案中移除原則，請執行下列步驟：

1. 包含專案檔案
1. 建立Document Security Client API物件。
1. 擷取受原則保護的Word檔案。
1. 從Word檔案中移除原則。
1. 儲存不安全的Word檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security Client API物件**

在您以程式設計方式執行Document Security服務操作之前，請先建立Document Security服務使用者端物件。

**擷取受原則保護的Word檔案**

擷取受原則保護的Word檔案以移除原則。 如果您嘗試從不受原則保護的Word檔案中移除原則，將會造成例外狀況。

**從Word檔案中移除原則**

只要連線設定中指定了管理員，您就可以從受原則保護的Word檔案中移除原則。 如果沒有，則用來保護檔案的原則必須包含`SWITCH_POLICY`許可權，才能從Word檔案中移除原則。 此外，在AEM Forms連線設定中指定的使用者也必須具有該許可權。 否則，會擲回例外狀況。

**儲存不安全的Word檔案**

在Document Security服務從Word檔案中移除原則後，您可以將不安全的Word檔案儲存為DOC檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[將原則套用至Word檔案](protecting-documents-policies.md#applying-policies-to-word-documents)

### 使用Java API從Word檔案中移除一項原則 {#remove-a-policy-from-a-word-document-using-the-java-api}

使用Document Security API (Java)從受原則保護的Word檔案中移除原則：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security使用者端API物件

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`RightsManagementClient`物件。

1. 擷取受原則保護的Word檔案

   * 使用受原則保護的Word檔案的建構函式，並傳遞指定Word檔案位置的字串值，以建立代表受原則保護的Word檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 從Word檔案中移除原則

   * 呼叫`RightsManagementClient`物件的`getDocumentManager`方法，以建立`DocumentManager`物件。
   * 叫用`DocumentManager`物件的`removeSecurity`方法，並傳遞包含受原則保護的Word檔案的`com.adobe.idp.Document`物件，以從Word檔案中移除原則。 此方法傳回包含不安全Word檔案的`com.adobe.idp.Document`物件。

1. 儲存不安全的Word檔案

   * 建立`java.io.File`物件，並確定副檔名為DOC。
   * 叫用`Document`物件的`copyToFile`方法，將`Document`物件的內容複製到檔案（請確定您使用的是`removeSecurity`方法傳回的`Document`物件）。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(SOAP模式)：使用Java API從Word檔案中移除原則」

### 使用網站服務API從Word檔案中移除一項原則 {#remove-a-policy-from-a-word-document-using-the-web-service-api}

使用Document Security API （Web服務），從受原則保護的Word檔案中移除原則：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Document Security使用者端API物件

   * 使用預設建構函式建立`RightsManagementServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`RightsManagementServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`RightsManagementServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取受原則保護的Word檔案

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存受原則保護的Word檔案，而原則會從中移除。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表Word檔案檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 從Word檔案中移除原則

   叫用`RightsManagementServiceClient`物件的`removePolicySecurity`方法，並傳遞包含受原則保護的Word檔案的`BLOB`物件，以從Word檔案中移除原則。 此方法傳回包含不安全Word檔案的`BLOB`物件。

1. 儲存不安全的Word檔案

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表不安全Word檔案檔案位置的字串值。
   * 建立位元組陣列，儲存`removePolicySecurity`方法傳回的`BLOB`物件的資料內容。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API從Word檔案中移除原則」

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
