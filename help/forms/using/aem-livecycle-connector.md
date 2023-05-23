---
title: 連接AEM Forms與AdobeLiveCycle
seo-title: Connecting AEM Forms with Adobe LiveCycle
description: AEMLiveCycle連接器允許您從應用和工作流中啟動LiveCycleES4文AEM檔服務。
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

# 連接AEM Forms與AdobeLiveCycle {#connecting-aem-forms-with-adobe-livecycle}

Adobe Experience Manager(AEM)LiveCycle連接器允許從Web應用和工作流中無縫調用AdobeLiveCycleES4文AEM檔服務。 LiveCycle提供富客戶端SDK，它允許客戶端應用程式使用Java API啟動LiveCycle服務。 AEMLiveCycle連接器簡化了在OSGi環境中使用這些API。

## 將服AEM務器連接到AdobeLiveCycle {#connecting-aem-server-to-adobe-livecycle}

AEMLiveCycle連接器是 [AEM Forms附加包](/help/forms/using/installing-configuring-aem-forms-osgi.md)。 安裝AEM Forms載入項軟體包後，請執行以下步驟將LiveCycle伺服器的詳細資訊添加AEM到Web控制台。

1. 在Web控AEM制台配置管理器中，找到AdobeLiveCycle客戶端SDK配置元件。
1. 按一下元件可編輯配置伺服器URL、用戶名和密碼。
1. 查看設定並按一下 **保存**。

雖然這些屬性是不言而喻的，但重要的是：

* **伺服器URL**  — 指定LiveCycle伺服器的URL。 如果要LiveCycle並AEM通過https通信，請從AEM以下JVM開始

   ```java
   argument
    -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
   ```

   的雙曲餘切值。

* **用戶名** — 指定用於在和LiveCycle之間建立通信的帳戶的AEM用戶名。 帳戶是具有啟動Document Services權限的LiveCycle用戶帳戶。
* **密碼** — 指定密碼。
* **服務名稱**  — 指定使用「用戶名」和「密碼」欄位中提供的用戶憑據啟動的服務。 預設情況下，啟動LiveCycle服務時不傳遞任何憑據。

## 啟動文檔服務 {#starting-document-services}

客戶端應用程式可以使用Java API、Web服務、遠程處理和REST以寫程式方式啟動LiveCycle服務。 對於Java客戶端，應用程式可以使用LiveCycleSDK。 LiveCycleSDK提供了用於遠程啟動這些服務的Java API。 例如，要將MicrosoftWord文檔轉換為PDF，客戶端將啟動GeneratePDFservice。 調用流包含以下步驟：

1. 建立ServiceClientFactory實例。
1. 每個服務都提供一個客戶端類。 要啟動服務，請建立服務的客戶端實例。
1. 啟動服務並處理結果。

通過AEM將這些客戶端實例作為OSGi服務公開，可以使用標準OSGi手段訪問這些服務，LiveCycle連接器簡化了流程。 LiveCycle連接器提供以下功能：

* 作為OSGi服務的客戶端實例：打包為OSGI捆綁包的客戶端列在 [文檔服務清單](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p) 的子菜單。 每個客戶端jar都將客戶端實例註冊為OSGi服務註冊表。
* 用戶憑據傳播：連接到LiveCycle伺服器所需的連接詳細資訊在中央位置進行管理。
* ServiceClientFactory服務：要啟動進程，客戶端應用程式可以訪問ServiceClientFactory實例。

### 通過OSGi服務註冊表中的服務引用啟動 {#starting-via-service-references-from-osgi-service-registry}

要從內部啟動外露服務AEM，請執行以下步驟：

1. 確定主依賴項。 將依賴關係添加到maven pom.xml檔案中所需的客戶端jar中。 至少，將依賴關係添加到adobe-livecycle-client和adobe-usermanager-clientjar中。

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

   要啟動服務，請為服務添加相應的Maven依賴項。 有關依賴項的清單，請參見 [文檔服務清單](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p)。 例如，對於「生成PDF」服務，添加以下依賴關係：

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. 獲取服務引用。 獲取服務實例的句柄。 如果正在編寫Java類，則可以使用聲明性服務注釋。

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

   上述代碼段將啟動GeneratePdfServiceClient的createPDF API，以將文檔轉換為PDF。 可以使用以下代碼在JSP中執行類似的調用。 主要區別在於以下代碼使用Sling ScriptHelper訪問GeneratePdfServiceClient。

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

在某些情況下，需要ServiceClientFactory類。 例如，您需要ServiceClientFactory調用進程。

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

LiveCycle中幾乎每個文檔服務都需要身份驗證。 您可以使用以下任意選項啟動這些服務，而無需在代碼中提供顯式憑據：

### 允許清單配置 {#allowlist-configuration}

LiveCycle客戶端SDK配置包含有關服務名的設定。 此配置是一個服務清單，調用邏輯將管理員憑據開箱即用。 例如，如果將DirectoryManager服務（用戶管理API的一部分）添加到此清單，則任何客戶端代碼都可以直接使用該服務，並且調用層作為發送到LiveCycle伺服器的請求的一部分自動傳遞配置的憑據

### 運行方式管理器 {#runasmanager}

作為整合的一部分，提供了新服務RunAsManager。 它允許您以寫程式方式控制在調用LiveCycle伺服器時使用的憑據。

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

### AdobeLiveCycle客戶端SDK API包 {#adobe-livecycle-client-sdk-api-bundle}

提供以下服務：

* com.adobe.idp.um.api.AuthenticationManager
* com.adobe.idp.um.api.DirectoryManager
* com.adobe.idp.um.api.AuthorizationManager
* com.adobe.idp.dsc.registry.service.ServiceRegistry
* com.adobe.idp.dsc.registry.component.ComponentRegistry

#### 馬文依賴項 {#maven-dependencies}

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

### AdobeLiveCycle客戶端SDK包 {#adobe-livecycle-client-sdk-bundle}

提供以下服務：

* com.adobe.livecycle.dsc.clientsdk.security.RunAsManager
* com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider

#### 馬文依賴項 {#maven-dependencies-1}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-cq-integration-api</artifactId>
  <version>1.1.10</version>
</dependency>
```

### AdobeLiveCycleTaskManager客戶端包 {#adobe-livecycle-taskmanager-client-bundle}

提供以下服務：

* com.adobe.idp.taskmanager.dsc.client.task.TaskManager
* com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService
* com.adobe.idp.taskmanager.dsc.client.queuemanager.QueueManager
* com.adobe.idp.taskmanager.dsc.client.emailsettings.EmailSettingService
* com.adobe.idp.taskmanager.dsc.client.endpoint.TaskManagerEndpointClient
* com.adobe.idp.taskmanager.dsc.client.userlist.UserlistService

#### 馬文依賴項 {#maven-dependencies-2}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-taskmanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle Workflow客戶端包 {#adobe-livecycle-workflow-client-bundle}

以下服務可用：

* com.adobe.idp.workflow.client.WorkflowServiceClient

#### 馬文依賴項 {#maven-dependencies-3}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-workflow-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle PDF Generator客戶捆綁 {#adobe-livecycle-pdf-generator-client-bundle}

以下服務可用：

* com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient

#### 馬文依賴項 {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle應用程式管理器客戶端包 {#adobe-livecycle-application-manager-client-bundle}

提供以下服務：

* com.adobe.idp.applicationmanager.service.ApplicationManager
* com.adobe.livecycle.applicationmanager.client.ApplicationManager
* com.adobe.livecycle.design.service.DesigntimeService

#### 馬文依賴項 {#maven-dependencies-5}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-applicationmanager-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle匯編器客戶端包 {#adobe-livecycle-assembler-client-bundle}

以下服務可用：

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### 馬文依賴項 {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle表單資料整合客戶端包 {#adobe-livecycle-form-data-integration-client-bundle}

以下服務可用：

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### 馬文依賴項 {#maven-dependencies-7}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-formdataintegration-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Forms客戶捆綁 {#adobe-livecycle-forms-client-bundle}

以下服務可用：

* com.adobe.livecycle.formsservice.client.FormsServiceClient

#### 馬文依賴項 {#maven-dependencies-8}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-forms-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Output客戶捆綁 {#adobe-livecycle-output-client-bundle}

以下服務可用：

* com.adobe.livecycle.output.client.OutputClient

#### 馬文依賴項 {#maven-dependencies-9}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-output-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Reader Extensions客戶捆綁 {#adobe-livecycle-reader-extensions-client-bundle}

以下服務可用：

* com.adobe.livecycle.readerextensions.client.ReaderExtensionsServiceClient

#### 馬文依賴項 {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle權限管理器客戶端包 {#adobe-livecycle-rights-manager-client-bundle}

提供以下服務：

* com.adobe.livecycle.rightsmanagement.client.DocumentManager
* com.adobe.livecycle.rightsmanagement.client.EventManager
* com.adobe.livecycle.rightsmanagement.client.ExternalUserManager
* com.adobe.livecycle.rightsmanagement.client.LicenseManager
* com.adobe.livecycle.rightsmanagement.client.WatermarkManager
* com.adobe.livecycle.rightsmanagement.client.PolicyManager
* com.adobe.livecycle.rightsmanagement.client.AbstractPolicyManager

#### 馬文依賴項 {#maven-dependencies-11}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-rightsmanagement-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle簽名客戶端捆綁包 {#adobe-livecycle-signatures-client-bundle}

以下服務可用：

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### 馬文依賴項 {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle信任儲存客戶端捆綁包 {#adobe-livecycle-truststore-client-bundle}

提供以下服務：

* com.adobe.truststore.dsc.TrustConfigurationService
* com.adobe.truststore.dsc.CRLService
* com.adobe.truststore.dsc.CredentialService
* com.adobe.truststore.dsc.CertificateService

#### 馬文依賴項 {#maven-dependencies-13}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-truststore-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle儲存庫客戶端包 {#adobe-livecycle-repository-client-bundle}

提供以下服務：

* com.adobe.repository.bindings.ResourceRepository
* com.adobe.repository.bindings.ResourceSynchronizer

#### 馬文依賴項 {#maven-dependencies-14}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-repository-client</artifactId>
  <version>11.0.0</version>
</dependency>
```
