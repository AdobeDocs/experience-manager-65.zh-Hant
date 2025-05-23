---
title: 將AEM Forms與AdobeLiveCycle連線
description: Adobe Experience Manager (AEM) LiveCycle聯結器可讓您從AEM應用程式和工作流程中開始LiveCycleES4 Acrobat服務。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
role: Admin,User
exl-id: 562f8a22-cbab-4915-bc0d-da9bea7d18fa
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 0%

---

# 將AEM Forms與AdobeLiveCycle連線 {#connecting-aem-forms-with-adobe-livecycle}

Adobe Experience Manager (AEM) LiveCycle聯結器可讓您從AEM網頁應用程式和工作流程中，順暢地叫用AdobeLiveCycleES4 Acrobat服務。 LiveCycle提供豐富的使用者端SDK，允許使用者端應用程式使用Java™ API啟動LiveCycle服務。 AEMLiveCycle聯結器簡化了OSGi環境中使用這些API的程式。

## 正在將AEM伺服器連線到AdobeLiveCycle {#connecting-aem-server-to-adobe-livecycle}

AEMLiveCycle聯結器是[AEM Forms附加元件套件](/help/forms/using/installing-configuring-aem-forms-osgi.md)的一部分。 安裝AEM Forms附加元件套件後，請執行以下步驟，好讓LiveCycle伺服器的詳細資訊新增至AEM Web Console。

1. 在AEM Web主控台設定管理員中，找出AdobeLiveCycle使用者端SDK設定元件。
1. 按一下元件，即可編輯組態伺服器URL、使用者名稱和密碼。
1. 檢閱設定並按一下&#x200B;**儲存**。

雖然屬性含義一目瞭然，但重要的部分如下：

* **伺服器URL** — 指定LiveCycle伺服器的URL。 如果您希望LiveCycle和AEM透過https通訊，請使用以下JVM啟動AEM

  ```java
  argument
   -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
  ```

  選項。

* **使用者名稱** — 指定用來建立AEM與LiveCycle之間通訊的帳戶使用者名稱。 帳戶是有權啟動Acrobat服務的LiveCycle使用者帳戶。
* **密碼** — 指定密碼。
* **服務名稱** — 指定使用[使用者名稱]和[密碼]欄位中提供的使用者認證啟動的服務。 依預設，啟動LiveCycle服務時不會傳遞任何認證。

## 啟動檔案服務 {#starting-document-services}

使用者端應用程式可以使用Java™ API、網站服務、遠端處理和REST，以程式設計方式啟動LiveCycle服務。 對於Java™使用者端，應用程式可使用LiveCycleSDK。 LiveCycle SDK提供Java™ API，以便從遠端啟動這些服務。 例如，若要將Microsoft® Word檔案轉換為PDF，使用者端會啟動GeneratePDFervice。 呼叫流程包含下列步驟：

1. 建立ServiceClientFactory執行個體。
1. 每個服務都會提供使用者端類別。 若要啟動服務，請建立服務的使用者端執行個體。
1. 啟動服務並處理結果。

AEMLiveCycle聯結器透過將這些使用者端執行個體公開為OSGi服務（可使用標準OSGi方式存取）來簡化流程。 LiveCycle聯結器提供下列功能：

* 作為OSGi服務的使用者端執行個體：封裝為OSGI套裝的使用者端列在[Acrobat服務清單](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p)區段中。 每個使用者端jar都會向OSGi服務登入將使用者端執行個體註冊為OSGi服務。
* 使用者證明資料傳輸：連線至LiveCycle伺服器所需的連線詳細資訊是在中央位置管理的。
* ServiceClientFactory服務：若要啟動程式，使用者端應用程式可以存取ServiceClientFactory執行個體。

### 從OSGi Service Registry透過Service References啟動 {#starting-via-service-references-from-osgi-service-registry}

若要從AEM內啟動公開的服務，請執行下列步驟：

1. 判斷maven相依性。 將相依性新增到maven pom.xml檔案中所需的使用者端jar。 至少要將相依性新增到adobe-livecycle-client和adobe-usermanager-client jar。

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-livecycle-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-usermanager-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-cq-integration-api</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

   若要啟動服務，請為該服務新增對應的Maven相依性。 如需相依性清單，請參閱[Acrobat服務清單](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p)。 例如，對於「產生PDF」服務，新增下列相依性：

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. 取得服務參考。 取得服務執行個體的控制代碼。 如果您正在撰寫Java™類別，則可以使用宣告式服務註解。

   ```java
   import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
   import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
   import com.adobe.idp.Document;
   
   @Reference
   GeneratePdfServiceClient generatePDF;
   ...
   
   Resource r = resourceResolver.getResource("/path/tp/docx");
   Document sourceDoc = new Document(r.adaptTo(InputStream.class));
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

   上述程式碼片段會啟動GeneratePdfServiceClient的createPDF API，以將檔案轉換為PDF。 您可以使用下列程式碼在JSP中執行類似的呼叫。 主要差異在於以下程式碼使用Sling ScriptHelper來存取GeneratePdfServiceClient。

   ```jsp
   <%@ page import="com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient" %>
   <%@ page import="com.adobe.livecycle.generatepdf.client.CreatePDFResult" %>
   <%@ page import="com.adobe.idp.Document" %>
   
   GeneratePdfServiceClient generatePDF = sling.getService(GeneratePdfServiceClient.class);
   Document sourceDoc = ...
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

### 透過ServiceClientFactory啟動 {#starting-via-serviceclientfactory}

有時需要ServiceClientFactory類別。 例如，您需要ServiceClientFactory來呼叫處理序。

```java
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;

@Reference
ServiceClientFactoryProvider scfProvider;

...
ServiceClientFactory scf = scfProvider.getDefaultServiceClientFactory();
...
```

## RunAs支援 {#runas-support}

LiveCycle幾乎所有Acrobat服務都需要驗證。 您可以使用下列任何選項來啟動這些服務，而不需在程式碼中提供明確的認證：

### 允許清單設定 {#allowlist-configuration}

LiveCycle使用者端SDK組態包含服務名稱的相關設定。 此設定是服務清單，叫用邏輯會立即使用管理員認證。 例如，如果您將DirectoryManager服務（User Management API的一部分）加入此清單，任何使用者端程式碼都可以直接使用服務。 此外，叫用層會在傳送給LiveCycle伺服器的要求中，自動傳遞已設定的憑證。

### RunAsManager {#runasmanager}

作為整合的一部分，提供新服務RunAsManager。 它可讓您以程式設計方式控制呼叫LiveCycle伺服器時要使用的認證。

```java
import com.adobe.livecycle.dsc.clientsdk.security.PasswordCredential;
import com.adobe.livecycle.dsc.clientsdk.security.PrivilegedAction;
import com.adobe.livecycle.dsc.clientsdk.security.RunAsManager;
import com.adobe.idp.dsc.registry.component.ComponentRegistry;

@Reference
private RunAsManager runAsManager;

List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
            public List<Component> run() {
                return componentRegistry.getComponents();
            }
        });
assertNotNull(components);
```

如果您要傳遞不同的認證，可以使用採用PasswordCredential執行個體的多載方法。

```java
PasswordCredential credential = new PasswordCredential("administrator","password");
List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
    public List<Component> run() {
        return componentRegistry.getComponents();
    }
},credential);
```

### InvocationRequest屬性 {#invocationrequest-property}

如果您呼叫處理程式或直接使用ServiceClientFactory類別，然後建立InvocationRequest，您可以指定屬性來指示呼叫層應使用已設定的認證。

```java
import com.adobe.idp.dsc.InvocationResponse
import com.adobe.idp.dsc.InvocationRequest
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory
import com.adobe.livecycle.dsc.clientsdk.InvocationProperties

ServiceClientFactoryProvider scfp = sling.getService(ServiceClientFactoryProvider.class)
ServiceClientFactory serviceClientFactory = scfp.getDefaultServiceClientFactory()
InvocationRequest ir = serviceClientFactory.createInvocationRequest("sample/LetterSubmissionProcess", "invoke", new HashMap(), true);

//Here we are invoking the request with system user
ir.setProperty(InvocationProperties.INVOKER_TYPE,InvocationProperties.INVOKER_TYPE_SYSTEM)

InvocationResponse response = serviceClientFactory.getServiceClient().invoke(ir);
```

## Acrobat服務清單 {#document-services-list}

### AdobeLiveCycle使用者端SDK API套件組合 {#adobe-livecycle-client-sdk-api-bundle}

下列服務可供使用：

* com.adobe.idp.um.api.AuthenticationManager
* com.adobe.idp.um.api.DirectoryManager
* com.adobe.idp.um.api.AuthorizationManager
* com.adobe.idp.dsc.registry.service.ServiceRegistry
* com.adobe.idp.dsc.registry.component.ComponentRegistry

#### Maven相依性 {#maven-dependencies}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-client</artifactId>
  <version>11.0.0</version>
</dependency>
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-usermanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle使用者端SDK套裝 {#adobe-livecycle-client-sdk-bundle}

下列服務可供使用：

* com.adobe.livecycle.dsc.clientsdk.security.RunAsManager
* com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider

#### Maven相依性 {#maven-dependencies-1}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-cq-integration-api</artifactId>
  <version>1.1.10</version>
</dependency>
```

### AdobeLiveCycleTaskManager使用者端套件 {#adobe-livecycle-taskmanager-client-bundle}

下列服務可供使用：

* com.adobe.idp.taskmanager.dsc.client.task.TaskManager
* com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService
* com.adobe.idp.taskmanager.dsc.client.queuemanager.QueueManager
* com.adobe.idp.taskmanager.dsc.client.emailsettings.EmailSettingService
* com.adobe.idp.taskmanager.dsc.client.endpoint.TaskManagerEndpointClient
* com.adobe.idp.taskmanager.dsc.client.userlist.UserlistService

#### Maven相依性 {#maven-dependencies-2}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-taskmanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle Workflow使用者端套裝 {#adobe-livecycle-workflow-client-bundle}

下列服務可供使用：

* com.adobe.idp.workflow.client.WorkflowServiceClient

#### Maven相依性 {#maven-dependencies-3}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-workflow-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle PDF Generator使用者端套裝 {#adobe-livecycle-pdf-generator-client-bundle}

下列服務可供使用：

* com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient

#### Maven相依性 {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle應用程式管理員使用者端套件 {#adobe-livecycle-application-manager-client-bundle}

下列服務可供使用：

* com.adobe.idp.applicationmanager.service.ApplicationManager
* com.adobe.livecycle.applicationmanager.client.ApplicationManager
* com.adobe.livecycle.design.service.DesigntimeService

#### Maven相依性 {#maven-dependencies-5}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-applicationmanager-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle組合器使用者端套件 {#adobe-livecycle-assembler-client-bundle}

下列服務可供使用：

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### Maven相依性 {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle表單資料整合使用者端套裝 {#adobe-livecycle-form-data-integration-client-bundle}

下列服務可供使用：

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### Maven相依性 {#maven-dependencies-7}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-formdataintegration-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Forms使用者端套裝 {#adobe-livecycle-forms-client-bundle}

下列服務可供使用：

* com.adobe.livecycle.formsservice.client.FormsServiceClient

#### Maven相依性 {#maven-dependencies-8}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-forms-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Output使用者端套裝 {#adobe-livecycle-output-client-bundle}

下列服務可供使用：

* com.adobe.livecycle.output.client.OutputClient

#### Maven相依性 {#maven-dependencies-9}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-output-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Reader Extensions使用者端套裝 {#adobe-livecycle-reader-extensions-client-bundle}

下列服務可供使用：

* com.adobe.livecycle.readerextensions.client.ReaderExtensionsServiceClient

#### Maven相依性 {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle許可權管理員使用者端套件 {#adobe-livecycle-rights-manager-client-bundle}

下列服務可供使用：

* com.adobe.livecycle.rightsmanagement.client.DocumentManager
* com.adobe.livecycle.rightsmanagement.client.EventManager
* com.adobe.livecycle.rightsmanagement.client.ExternalUserManager
* com.adobe.livecycle.rightsmanagement.client.LicenseManager
* com.adobe.livecycle.rightsmanagement.client.WatermarkManager
* com.adobe.livecycle.rightsmanagement.client.PolicyManager
* com.adobe.livecycle.rightsmanagement.client.AbstractPolicyManager

#### Maven相依性 {#maven-dependencies-11}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-rightsmanagement-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle簽章使用者端套件 {#adobe-livecycle-signatures-client-bundle}

下列服務可供使用：

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### Maven相依性 {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle信任存放區使用者端套裝 {#adobe-livecycle-truststore-client-bundle}

下列服務可供使用：

* com.adobe.truststore.dsc.TrustConfigurationService
* com.adobe.truststore.dsc.CRLService
* com.adobe.truststore.dsc.CredentialService
* com.adobe.truststore.dsc.CertificateService

#### Maven相依性 {#maven-dependencies-13}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-truststore-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle存放庫使用者端套件 {#adobe-livecycle-repository-client-bundle}

下列服務可供使用：

* com.adobe.repository.bindings.ResourceRepository
* com.adobe.repository.bindings.ResourceSynchronizer

#### Maven相依性 {#maven-dependencies-14}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-repository-client</artifactId>
  <version>11.0.0</version>
</dependency>
```
