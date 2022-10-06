---
title: 將AEM Forms與AdobeLiveCycle
seo-title: Connecting AEM Forms with Adobe LiveCycle
description: AEMLiveCycle連接器可讓您從AEM應用程式和工作流程中啟動LiveCycleES4檔案服務。
seo-description: AEM LiveCycle connector allows you to start LiveCycle ES4 Document Services from within AEM apps and workflows.
uuid: 7dc9d5ec-7b19-4d93-936d-81ceb45dfffa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 7e404b45-1302-4dd1-b3c9-3f47fedb5f94
role: Admin
exl-id: 562f8a22-cbab-4915-bc0d-da9bea7d18fa
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---

# 將AEM Forms與AdobeLiveCycle {#connecting-aem-forms-with-adobe-livecycle}

Adobe Experience Manager(AEM)LiveCycle連接器可讓AdobeLiveCycleES4檔案服務從AEM網頁應用程式和工作流程內順暢地呼叫。 LiveCycle提供豐富用戶端SDK，可讓用戶端應用程式使用Java API啟動LiveCycle服務。 AEMLiveCycle連接器可簡化在OSGi環境中使用這些API的程式。

## 將AEM伺服器連接到AdobeLiveCycle {#connecting-aem-server-to-adobe-livecycle}

AEMLiveCycle連接器是 [AEM Forms附加元件套件](/help/forms/using/installing-configuring-aem-forms-osgi.md). 安裝AEM Forms附加元件套件後，請執行下列步驟，將LiveCycle伺服器的詳細資訊新增至AEM Web Console。

1. 在AEM Web主控台配置管理器中，找到AdobeLiveCycle用戶端SDK配置元件。
1. 按一下元件可編輯配置伺服器URL、用戶名和密碼。
1. 檢閱設定，然後按一下 **儲存**.

雖然這些屬性是不言自明的，但重要的是：

* **伺服器URL**  — 指定LiveCycle伺服器的URL。 如果要讓LiveCycle和AEM通過https通信，請使用以下JVM啟動AEM

   ```java
   argument
    -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
   ```

   選項。

* **使用者名稱** — 指定用於建立AEM與LiveCycle之間通信的帳戶的用戶名。 帳戶是具有啟動Document Services權限的LiveCycle使用者帳戶。
* **密碼** — 指定密碼。
* **服務名稱**  — 指定使用「用戶名」和「密碼」欄位中提供的用戶憑據啟動的服務。 依預設，啟動LiveCycle服務時不會傳遞任何憑證。

## 啟動文檔服務 {#starting-document-services}

客戶端應用程式可以使用Java API、Web服務、Remoting和REST以寫程式方式啟動LiveCycle服務。 對於Java用戶端，應用程式可使用LiveCycleSDK。 LiveCycleSDK提供Java API，可遠端啟動這些服務。 例如，要將Microsoft Word文檔轉換為PDF，客戶端將啟動GeneratePDFService。 調用流包含以下步驟：

1. 建立ServiceClientFactory實例。
1. 每個服務都提供一個客戶端類。 若要啟動服務，請建立服務的用戶端例項。
1. 啟動服務並處理結果。

AEMLiveCycle連接器會將這些用戶端例項公開為可透過標準OSGi方式存取的OSGi服務，借此簡化流程。 LiveCycle連接器提供下列功能：

* 作為OSGi服務的客戶端實例：封裝為OSGI套件組合的用戶端列於 [文檔服務清單](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p) 區段。 每個客戶端jar都將客戶端實例註冊為OSGi服務註冊表。
* 用戶憑據傳播：連接到LiveCycle伺服器所需的連接詳細資訊在中央位置進行管理。
* ServiceClientFactory服務：要啟動進程，客戶端應用程式可以訪問ServiceClientFactory實例。

### 從OSGi服務註冊表通過服務引用啟動 {#starting-via-service-references-from-osgi-service-registry}

若要從AEM內啟動公開的服務，請執行下列步驟：

1. 決定主要相依性。 將相依性新增至maven pom.xml檔案中所需的用戶端jar。 至少將相依性新增至adobe-livecycle-client和adobe-usermanager-client Jar。

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

   若要啟動服務，請為服務新增對應的Maven相依性。 如需相依性清單，請參閱 [文檔服務清單](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p). 例如，對於「生成PDF」服務，添加以下相依性：

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. 取得服務參考。 取得服務例項的控制代碼。 如果您正在寫Java類，則可以使用聲明性服務注釋。

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

   上述程式碼片段會啟動GeneratePdfServiceClient的createPDF API，將檔案轉換為PDF。 您可以使用以下代碼在JSP中執行類似的調用。 主要差異在於下列程式碼使用Sling ScriptHelper存取GeneratePdfServiceClient。

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

### 通過ServiceClientFactory啟動 {#starting-via-serviceclientfactory}

在某些情況下，需要ServiceClientFactory類。 例如，您需要ServiceClientFactory才能調用進程。

```java
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;

@Reference
ServiceClientFactoryProvider scfProvider;

...
ServiceClientFactory scf = scfProvider.getDefaultServiceClientFactory();
...
```

## 運行方式支援 {#runas-support}

LiveCycle中幾乎每個文檔服務都需要身份驗證。 您可以使用下列任一選項來啟動這些服務，而不需在程式碼中提供明確憑證：

### 允許清單配置 {#allowlist-configuration}

LiveCycle用戶端SDK設定包含有關服務名稱的設定。 此配置是服務的清單，調用邏輯會立即使用管理員憑據。 例如，如果將DirectoryManager服務（用戶管理API的一部分）添加到此清單中，則任何客戶端代碼都可以直接使用該服務，調用層作為發送到LiveCycle伺服器的請求的一部分自動在配置的憑據上傳遞

### 運行AsManager {#runasmanager}

作為整合的一部分，提供了新服務RunAsManager。 它可讓您以程式設計方式控制要在呼叫LiveCycle伺服器時使用的憑證。

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

如果要傳遞不同的憑據，可以使用採用PasswordCredential實例的重載方法。

```java
PasswordCredential credential = new PasswordCredential("administrator","password");
List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
    public List<Component> run() {
        return componentRegistry.getComponents();
    }
},credential);
```

### InvocationRequest屬性 {#invocationrequest-property}

如果調用進程或直接使用ServiceClientFactory類並建立InvocationRequest，則可以指定一個屬性以指示調用層應使用配置的憑據。

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

## 文檔服務清單 {#document-services-list}

### AdobeLiveCycle用戶端SDK API套件 {#adobe-livecycle-client-sdk-api-bundle}

提供下列服務：

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

### AdobeLiveCycle用戶端SDK套件 {#adobe-livecycle-client-sdk-bundle}

提供下列服務：

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

### AdobeLiveCycleTaskManager客戶端包 {#adobe-livecycle-taskmanager-client-bundle}

提供下列服務：

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

### AdobeLiveCycle Workflow用戶端套件 {#adobe-livecycle-workflow-client-bundle}

提供下列服務：

* com.adobe.idp.workflow.client.WorkflowServiceClient

#### Maven相依性 {#maven-dependencies-3}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-workflow-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle PDF Generator用戶端套件 {#adobe-livecycle-pdf-generator-client-bundle}

提供下列服務：

* com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient

#### Maven相依性 {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle應用程式管理器客戶端套件 {#adobe-livecycle-application-manager-client-bundle}

提供下列服務：

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

### AdobeLiveCycle組合器客戶端套件 {#adobe-livecycle-assembler-client-bundle}

提供下列服務：

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### Maven相依性 {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle表單資料整合用戶端套件 {#adobe-livecycle-form-data-integration-client-bundle}

提供下列服務：

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### Maven相依性 {#maven-dependencies-7}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-formdataintegration-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Forms用戶端套件 {#adobe-livecycle-forms-client-bundle}

提供下列服務：

* com.adobe.livecycle.formsservice.client.FormsServiceClient

#### Maven相依性 {#maven-dependencies-8}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-forms-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Output用戶端套件 {#adobe-livecycle-output-client-bundle}

提供下列服務：

* com.adobe.livecycle.output.client.OutputClient

#### Maven相依性 {#maven-dependencies-9}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-output-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Reader Extensions用戶端套件 {#adobe-livecycle-reader-extensions-client-bundle}

提供下列服務：

* com.adobe.livecycle.readerextensions.client.ReaderExtensionsServiceClient

#### Maven相依性 {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle權限管理器客戶端套件 {#adobe-livecycle-rights-manager-client-bundle}

提供下列服務：

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

### AdobeLiveCycle簽名客戶端包 {#adobe-livecycle-signatures-client-bundle}

提供下列服務：

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### Maven相依性 {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycleTruststore客戶端包 {#adobe-livecycle-truststore-client-bundle}

提供下列服務：

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

### AdobeLiveCycle儲存庫客戶端套件 {#adobe-livecycle-repository-client-bundle}

提供下列服務：

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
