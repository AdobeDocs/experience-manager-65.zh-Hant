---
title: 將AEM Forms與Adobe LiveCycle連結
seo-title: 將AEM Forms與Adobe LiveCycle連結
description: AEM liveCycle Connector可讓您從AEM應用程式和工作流程中啟動LiveCycle ES4 Document Services。
seo-description: AEM liveCycle Connector可讓您從AEM應用程式和工作流程中啟動LiveCycle ES4 Document Services。
uuid: 7dc9d5ec-7b19-4d93-936d-81ceb45dfffa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 7e404b45-1302-4dd1-b3c9-3f47fedb5f94
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 將AEM Forms與Adobe LiveCycle連結 {#connecting-aem-forms-with-adobe-livecycle}

Adobe Experience Manager(AEM)LiveCycle連接器可讓您從AEM網頁應用程式和工作流程中順暢地呼叫Adobe LiveCycle ES4 Document Services。 LiveCycle提供rich client SDK，可讓用戶端應用程式使用Java API啟動LiveCycle服務。 AEM LiveCycle Connector可簡化在OSGi環境中使用這些API的作業。

## 將AEM伺服器連線至Adobe LiveCycle {#connecting-aem-server-to-adobe-livecycle}

AEM LiveCycle Connector是 [AEM Forms附加套件的一部分](/help/forms/using/installing-configuring-aem-forms-osgi.md)。 安裝AEM Forms附加元件套件後，請執行下列步驟，將LiveCycle伺服器的詳細資訊新增至AEM Web Console。

1. 在AEM網頁主控台組態管理器中，找出Adobe LiveCycle Client SDK組態元件。
1. 按一下元件可編輯配置伺服器URL、用戶名和口令。
1. 檢閱設定，然後按一下「 **儲存**」。

雖然屬性是自解釋的，但重要的是：

* **伺服器URL** —— 指定LiveCycle伺服器的URL。 如果您想要LiveCycle和AEM透過https通訊，請使用下列JVM啟動AEM

   ```
   argument
    -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
   ```

   的雙曲餘切值。

* **Username**—— 指定用來建立AEM與LiveCycle通訊之帳戶的使用者名稱。 此帳戶是LiveCycle使用者帳戶，具有啟動Document services的權限。
* **密碼**-指定密碼。
* **服務名稱** -指定使用「用戶名」和「密碼」欄位中提供的用戶憑據啟動的服務。 依預設，啟動LiveCycle服務時不會傳遞任何認證。

## 啟動檔案服務 {#starting-document-services}

用戶端應用程式可使用Java API、Web Services、Remoting和REST，以程式設計方式啟動LiveCycle服務。 對於Java用戶端，應用程式可使用LiveCycle SDK。 LiveCycle SDK提供Java API，以遠端啟動這些服務。 例如，若要將Microsoft word檔案轉換為PDF，用戶端會啟動GeneratePDFervice。 調用流由以下步驟組成：

1. 建立ServiceClientFactory實例。
1. 每個服務都提供一個客戶機類。 要啟動服務，請建立服務的客戶端實例。
1. 啟動服務並處理結果。

AEM LiveCycle Connector可將這些用戶端例項公開為OSGi服務，讓您使用標準OSGi來存取，以簡化流程。 LiveCycle連接器提供下列功能：

* 作為OSGi服務的客戶端實例：打包為OSGI捆綁包的客戶端列在「文檔服 [務」清單部分](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p) 。 每個客戶端jar都將客戶端實例註冊為OSGi服務註冊表。
* 用戶憑據傳播：連線至LiveCycle伺服器所需的連線詳細資訊會集中管理。
* ServiceClientFactory服務：要啟動進程，客戶端應用程式可以訪問ServiceClientFactory實例。

### 從OSGi服務註冊通過服務引用啟動 {#starting-via-service-references-from-osgi-service-registry}

若要從AEM中啟動公開的服務，請執行下列步驟：

1. 確定主要依賴項。 在maven pom.xml檔案中將相依性添加到所需的客戶端jar。 至少要將相依性新增至adobe-livecycle-client和adobe-usermanager-clientJar。

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

   要啟動服務，請為服務添加相應的Maven依賴關係。 有關依賴項的清單，請參 [閱Document Service List](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p)。 例如，對於「生成PDF」服務，添加以下相關性：

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. 獲取服務參考。 獲取服務實例的句柄。 如果您正在編寫Java類，則可以使用Declative services注釋。

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

   上述程式碼片段會啟動GeneratePdfServiceClient的createPDF API，將檔案轉換為PDF。 您可以使用下列代碼在JSP中執行類似的調用。 主要差異在於下列程式碼使用Sling ScriptHelper存取GeneratePdfServiceClient。

   ```java
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

在某些情況下， serviceClientFactory類是必需的。 例如，您需要ServiceClientFactory來呼叫進程。

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

LiveCycle中幾乎每個檔案服務都需要驗證。 您可以使用下列任一選項來啟動這些服務，而不需在程式碼中提供明確的憑證：

### 白名單配置 {#whitelist-configuration}

LiveCycle Client SDK組態包含有關服務名稱的設定。 此配置是服務清單，調用邏輯將立即使用管理員憑據。 例如，如果您將DirectoryManager服務（User Management API的一部分）新增至此清單，任何用戶端程式碼都可直接使用服務，而呼叫層會自動傳遞已設定的認證，作為傳送至LiveCycle伺服器之請求的一部分

### RunAsManager {#runasmanager}

作為整合的一部分，提供了新的服務RunAsManager。 它可讓您以程式設計方式控制呼叫LiveCycle伺服器時使用的憑證。

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

如果要傳遞不同的憑證，可以使用採用PasswordCredential實例的過載方法。

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

## 檔案服務清單 {#document-services-list}

### Adobe LiveCycle Client SDK API套件 {#adobe-livecycle-client-sdk-api-bundle}

提供下列服務：

* com.adobe.idp.um.api.AuthenticationManager
* com.adobe.idp.um.api.DirectoryManager
* com.adobe.idp.um.api.AuthorizationManager
* com.adobe.idp.dsc.registry.service.ServiceRegistry
* com.adobe.idp.dsc.registry.component.ComponentRegistry

#### Maven依賴項 {#maven-dependencies}

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

### Adobe LiveCycle Client SDK套件 {#adobe-livecycle-client-sdk-bundle}

提供下列服務：

* com.adobe.livecycle.dsc.clientsdk.security.RunAsManager
* com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider

#### Maven依賴項 {#maven-dependencies-1}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-cq-integration-api</artifactId>
  <version>1.1.10</version>
</dependency>
```

### Adobe LiveCycle TaskManager Client套件 {#adobe-livecycle-taskmanager-client-bundle}

提供下列服務：

* com.adobe.idp.taskmanager.dsc.client.task.TaskManager
* com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService
* com.adobe.idp.taskmanager.dsc.client.queuemanager.QueueManager
* com.adobe.idp.taskmanager.dsc.client.emailsettings.EmailSettingService
* com.adobe.idp.taskmanager.dsc.client.endpoint.TaskManagerEndpointClient
* com.adobe.idp.taskmanager.dsc.client.userlist.UserlistService

#### Maven依賴項 {#maven-dependencies-2}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-taskmanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Workflow Client Bundle {#adobe-livecycle-workflow-client-bundle}

提供下列服務：

* com.adobe.idp.workflow.client.WorkflowServiceClient

#### Maven依賴項 {#maven-dependencies-3}

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

#### Maven依賴項 {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Application Manager Client套件 {#adobe-livecycle-application-manager-client-bundle}

提供下列服務：

* com.adobe.idp.applicationmanager.service.ApplicationManager
* com.adobe.livecycle.applicationmanager.client.ApplicationManager
* com.adobe.livecycle.design.service.DesigntimeService

#### Maven依賴項 {#maven-dependencies-5}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-applicationmanager-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Assembler Client套件 {#adobe-livecycle-assembler-client-bundle}

提供下列服務：

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### Maven依賴項 {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Form Data Integration Client套件 {#adobe-livecycle-form-data-integration-client-bundle}

提供下列服務：

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### Maven依賴項 {#maven-dependencies-7}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-formdataintegration-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Forms Client套件 {#adobe-livecycle-forms-client-bundle}

提供下列服務：

* com.adobe.livecycle.formsservice.client.FormsServiceClient

#### Maven依賴項 {#maven-dependencies-8}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-forms-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Output Client套件 {#adobe-livecycle-output-client-bundle}

提供下列服務：

* com.adobe.livecycle.output.client.OutputClient

#### Maven依賴項 {#maven-dependencies-9}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-output-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Reader Extensions Client套件 {#adobe-livecycle-reader-extensions-client-bundle}

提供下列服務：

* com.adobe.livecycle.readerextensions.client.ReaderExtensionsServiceClient

#### Maven依賴項 {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Rights Manager Client套件 {#adobe-livecycle-rights-manager-client-bundle}

提供下列服務：

* com.adobe.livecycle.rightsmanagement.client.DocumentManager
* com.adobe.livecycle.rightsmanagement.client.EventManager
* com.adobe.livecycle.rightsmanagement.client.ExternalUserManager
* com.adobe.livecycle.rightsmanagement.client.LicenseManager
* com.adobe.livecycle.rightsmanagement.client.WatermarkManager
* com.adobe.livecycle.rightsmanagement.client.PolicyManager
* com.adobe.livecycle.rightsmanagement.client.AbstractPolicyManager

#### Maven依賴項 {#maven-dependencies-11}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-rightsmanagement-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Signatures Client套件 {#adobe-livecycle-signatures-client-bundle}

提供下列服務：

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### Maven依賴項 {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Truststore Client套件 {#adobe-livecycle-truststore-client-bundle}

提供下列服務：

* com.adobe.truststore.dsc.TrustConfigurationService
* com.adobe.truststore.dsc.CRLService
* com.adobe.truststore.dsc.CredentialService
* com.adobe.truststore.dsc.CertificateService

#### Maven依賴項 {#maven-dependencies-13}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-truststore-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Repository用戶端套件 {#adobe-livecycle-repository-client-bundle}

提供下列服務：

* com.adobe.repository.bindings.ResourceRepository
* com.adobe.repository.bindings.ResourceSynchronizer

#### Maven依賴項 {#maven-dependencies-14}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-repository-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
