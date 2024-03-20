---
title: 將服務與JMX主控台整合
description: 透過建立和部署MBean以使用JMX主控台管理服務，公開服務屬性和作業，以啟用要執行的管理工作
topic-tags: extending-aem
content-type: reference
exl-id: fe727406-09cb-4516-8278-806fd78cfc12
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1621'
ht-degree: 0%

---

# 將服務與JMX主控台整合{#integrating-services-with-the-jmx-console}

使用JMX主控台建立並部署MBean以管理服務。 公開服務屬性和作業，以啟用要執行的管理工作。

如需有關使用JMX主控台的資訊，請參閱 [使用JMX主控台監控伺服器資源](/help/sites-administering/jmx-console.md).

## Felix和CQ5中的JMX框架 {#the-jmx-framework-in-felix-and-cq}

在Apache Felix平台上，您可以將MBean部署為OSGi服務。 在OSGi服務登入中註冊MBean服務時，Aries JMX白板模組會自動向MBean伺服器註冊MBean。 MBean即可供JMX主控台使用，主控台會公開公用屬性和作業。

![jmxwhiteboard](assets/jmxwhiteboard.png)

## 建立CQ5和CRX的MBean {#creating-mbeans-for-cq-and-crx}

您為管理CQ5或CRX資源而建立的MBean是以javax.management.DynamicMBean介面為基礎。 若要建立它們，請遵循JMX規格中概述的一般設計模式：

* 建立管理介面，包括get、set和is定義屬性的方法，以及其他定義作業的方法。
* 建立實作類別。 類別必須實作DynamicMBean，或擴充DynamicMBean的實作類別。
* 請遵循標準命名慣例，讓實作類別的名稱是具有MBean尾碼的介面名稱。

除了定義管理介面，該介面還定義OSGi服務介面。 實作類別實作OSGi服務。

### 使用註解提供MBean資訊 {#using-annotations-to-provide-mbean-information}

此 [com.adobe.granite.jmx.annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/jmx/annotation/package-summary.html) package提供數個註解和類別，讓您輕鬆將MBean中繼資料提供至JMX主控台。 使用這些註解和類別，而非直接將資訊新增到MBean的MBeanInfo物件。

**註解**

將註解新增至管理介面以指定MBean中繼資料。 該資訊會顯示在每個已部署的實作類別的JMX主控台中。 下列為可用的註解(如需完整資訊，請參閱 [com.adobe.granite.jmx.annotation JavaDocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/jmx/annotation/package-summary.html))：

* **說明：** 提供MBean類別或方法的說明。 在類別宣告上使用時，說明會顯示在MBean的「JMX主控台」頁面上。 在方法上使用時，說明會顯示為對應屬性或作業的暫留文字。
* **影響：** 方法的影響。 有效引數值是由定義的欄位 [javax.management.MBeanOperationInfo](https://docs.oracle.com/javase/1.5.0/docs/api/javax/management/MBeanOperationInfo.html).

* **名稱：** 指定作業引數的顯示名稱。 使用此註解來覆寫介面中使用之方法引數的實際名稱。
* **OpenTypeInfo：** 指定用來在JMX主控台中表示複合資料或表格資料的類別。 與Open MBean搭配使用
* **TabularTypeInfo：** 用於標註用來表示表格資料的類別。

**類別**

提供用來建立使用您新增至其介面的註解的動態MBean的類別：

* **AnnotatedStandardMBean：** javax.management.StandardMBean類別的子類別，可自動為JMX主控台提供註解中繼資料。
* **OpenAnnotatedStandardMBean：** AnnotatedStandardMBean類別的子類別，用於建立使用OpenTypeInfo註解的Open Mbean。

### 開發MBean {#developing-mbeans}

通常您的MBean會反映在您要管理的OSGi服務上。 在Felix平台上，您可以建立MBean，就像在其他Java伺服器平台上部署一樣。 主要差異在於您可以使用註解來指定MBean資訊：

* 管理介面：使用getter、setter和is方法定義屬性。 使用任何其他公用方法定義作業。 使用註解來提供BeanInfo物件的中繼資料。
* MBean類別：實作管理介面。 擴充AnnotatedStandardMBean類別，以便在介面上處理註解。

以下範例MBean提供有關CRX存放庫的資訊。 介面使用說明註解來向JMX主控台提供資訊。

#### 管理介面 {#management-interface}

```java
package com.adobe.example.myapp;

import com.adobe.granite.jmx.annotation.Description;

@Description("Example MBean that exposes repository properties.")
public interface ExampleMBean {

    @Description("The name of the repository.")
    String getRepositoryName();

    @Description("The vendor of the repository.")
    String   getRepositoryVendor();

    @Description("The URL of repository vendor.")
    String getVendorUrl();
}
```

實作類別使用SlingRepository服務來擷取CRX存放庫的相關資訊。

#### MBean實作類別 {#mbean-implementation-class}

```java
package com.adobe.example.myapp;

import org.apache.felix.scr.annotations.*;
import org.apache.sling.jcr.api.SlingRepository;

import com.adobe.granite.jmx.annotation.AnnotatedStandardMBean;

import javax.management.*;

public class ExampleMBeanImpl extends AnnotatedStandardMBean implements ExampleMBean {

    @Reference(cardinality = ReferenceCardinality.OPTIONAL_UNARY)
    private SlingRepository repository;

    public ExampleMBeanImpl() throws NotCompliantMBeanException {
        super(ExampleMBean.class);
    }

    public String getRepositoryName() {
        return repository.getDescriptor("jcr.repository.name");
    }

    public String getRepositoryVendor() {
        return repository.getDescriptor("jcr.repository.vendor");
    }

    public String getVendorUrl() {
        return repository.getDescriptor("jcr.repository.vendor.url");
    }
}
```

下圖顯示JMX主控台中此MBean的頁面。

![jmxdescription](assets/jmxdescription.png)

### 正在登入MBean {#registering-mbeans}

當您將MBean註冊為OSGi服務時，它們會自動向MBean伺服器註冊。 若要在CQ5上安裝MBean，請將其納入套件組合中，並像匯出任何其他OSGi服務一樣匯出MBean服務。

除了OSGi相關的中繼資料之外，您還必須提供Aries JMX白板模組在MBean伺服器註冊MBean時所需的中繼資料：

* **DynamicMBean介面的名稱：** 宣告MBean服務實作 `javax.management.DynamicMBea`n介面。 此宣告會通知Aries JMX Whiteboard模組，此服務是MBean服務。

* **MBean網域和金鑰屬性：** 在Felix上，您將此資訊當作MBean的OSGi服務的屬性來提供。 此資訊與您通常在 `javax.management.ObjectName` 物件。

當您的MBean反映為單一服務時，只需要單一MBean服務執行個體。 在這種情況下，如果您使用Felix SCR Maven外掛程式，則可以在MBean實作類別上使用Apache Felix Service Component Runtime (SCR)註解來指定JMX相關的中繼資料。 若要例項化多個MBean執行個體，您可以建立另一個類別來執行MBean的OSGi服務註冊。 在此情況下，會在執行階段產生與JMX相關的中繼資料。

**單一MBean**

您可以在設計時定義所有屬性和作業的MBean，可以使用MBean實作類別中的SCR註解進行部署。 在以下範例中， `value` 的屬性 `Service` annotation宣告服務實作 `DynamicMBean` 介面。 此 `name` 的屬性 `Property` 註解指定JMX網域和金鑰屬性。

#### 含SCR註解的MBean實作類別 {#mbean-implementation-class-with-scr-annotations}

```java
package com.adobe.example.myapp;

import org.apache.felix.scr.annotations.*;
import org.apache.sling.jcr.api.SlingRepository;

import com.adobe.granite.jmx.annotation.AnnotatedStandardMBean;

import javax.management.*;

@Component(immediate = true)
@Property(name = "jmx.objectname", value="com.adobe.example:type=CRX")
@Service(value = DynamicMBean.class)
public class ExampleMBeanImpl extends AnnotatedStandardMBean implements ExampleMBean {

    @Reference(cardinality = ReferenceCardinality.OPTIONAL_UNARY)
    private SlingRepository repository;

    public ExampleMBeanImpl() throws NotCompliantMBeanException {
        super(ExampleMBean.class);
    }

    public String getRepositoryName() {
        return repository.getDescriptor("jcr.repository.name");
    }

    public String getRepositoryVendor() {
        return repository.getDescriptor("jcr.repository.vendor");
    }

    public String getVendorUrl() {
        return repository.getDescriptor("jcr.repository.vendor.url");
    }
}
```

**多個MBean服務執行個體**

若要管理受管理服務的多個執行個體，請建立對應MBean服務的多個執行個體。 此外，啟動或停止Managed執行個體時，應建立或移除MBean服務執行個體。 您可以建立MBean管理員類別以在執行階段例項化MBean服務，並管理服務生命週期。

使用BundleContext將MBean註冊為OSGi服務。 在用作BundleContext.registerService方法引數的Dictionary物件中包含JMX相關資訊。

在以下程式碼範例中，ExampleMBean服務是以程式設計方式註冊。 componentContext物件是ComponentContext，它提供BundleContext的存取權。

#### 程式碼片段：程式化MBean服務註冊 {#code-snippet-programmatic-mbean-service-registration}

```java
Dictionary mbeanProps = new Hashtable();
mbeanProps.put("jmx.objectname", "com.adobe.example:type=CRX");
ExampleMBeanImpl mbean = new ExampleMBeanImpl();
ServiceRegistration serviceregistration =
            componentContext.getBundleContext().registerService(DynamicMBean.class.getName(), mbean, mbeanProps);
```

下一節中的範例MBean提供詳細資訊。

當服務設定儲存在存放庫時，MBean服務管理員會很有用。 管理員可以擷取服務資訊，並使用它來設定和建立對應的MBean。 管理員類別也可以監聽存放庫變更事件並相應地更新MBean服務。

## 範例：使用JMX監控工作流程模型 {#example-monitoring-workflow-models-using-jmx}

此範例中的MBean提供儲存在存放庫中CQ5工作流程模型的相關資訊。 MBean管理員類別會根據儲存在存放庫中的工作流程模型建立MBean，並在執行階段註冊其OSGi服務。 此範例由包含下列成員的單一組合組成：

* Workflowmbean：管理介面。
* WorkflowMBeanImpl： MBean實作類別。
* WorkflowMBeanManager： MBean管理員類別的介面。
* WorkflowMBeanManagerImpl： MBean管理員的實作類別。

**注意：** 為簡化起見，此範例中的程式碼不會執行記錄或對擲回的例外狀況做出反應。

WorkflowMBeanManagerImpl包含元件啟用方法。 啟動元件時，方法會執行下列工作：

* 取得該組合的BundleContext。
* 查詢存放庫以取得現有工作流程模型的路徑。
* 為每個工作流程模型建立MBean。
* 向OSGi服務登入登入MBean。

MBean中繼資料會顯示在具有com.adobe.example網域、workflow_model型別的JMX主控台中，而「屬性」是工作流程模型設定節點的路徑。

![jmxworkflowmbean](assets/jmxworkflowmbean.png)

### 範例MBean {#the-example-mbean}

此範例需要MBean介面和實作，以反映在 `com.day.cq.workflow.model.WorkflowModel` 介面。 MBean非常簡單，因此範例可以專注於設計的設定和部署方面。 MBean會顯示單一屬性，即模型名稱。

#### WorkflowMBean介面 {#workflowmbean-interface}

```java
package com.adobe.example.myapp.api;

import com.adobe.granite.jmx.annotation.Description;

@Description("Example MBean that exposes Workflow model properties.")
public interface WorkflowMBean {

 @Description("The name of the Workflow model.")
 String getModelName();
}
```

#### WorkflowMBeanImpl {#workflowmbeanimpl}

```java
package com.adobe.example.myapp.impl;

import javax.management.NotCompliantMBeanException;

import com.day.cq.workflow.model.WorkflowModel;
import com.adobe.example.myapp.api.WorkflowMBean;
import com.adobe.granite.jmx.annotation.AnnotatedStandardMBean;

public class WorkflowMBeanImpl extends AnnotatedStandardMBean implements WorkflowMBean {

 WorkflowModel model;

 protected WorkflowMBeanImpl(WorkflowModel inmodel)
   throws NotCompliantMBeanException {
  super(WorkflowMBean.class);
  model=inmodel;
 }

 public String getModelName() {
  return model.getTitle();
 }
}
```

### 範例MBean管理員 {#the-example-mbean-manager}

WorkflowMBeanManager服務包含建立WorkflowMBean服務的元件啟用方法。 服務實作包括下列方法：

* 啟動：元件啟動器。 建立JCR工作階段以讀取WorkflowModel設定節點。 儲存模型設定的根節點會定義在靜態欄位中。 設定節點的名稱也會在靜態欄位中定義。 此方法會呼叫取得節點模型路徑並建立模型WorkflowMBeans的其他方法。
* getModelIds：周遊根節點下方的存放庫，並擷取每個模型節點的路徑。
* makeMBean：使用模型路徑來建立WorkflowModel物件、為其建立WorkflowMBean並註冊其OSGi服務。

>[!NOTE]
>
>WorkflowMBeanManager實作只會為啟動元件時存在的模型設定建立MBean服務。 更強大的實作會監聽有關新模型組態以及現有模型組態變更或刪除的存放庫事件。 變更發生時，管理員可以建立、修改或移除對應的WorkflowMBean服務。
>

#### WorkflowMBeanManager介面 {#workflowmbeanmanager-interface}

```java
package com.adobe.example.myapp.api;

public interface WorkflowMBeanManager {

}
```

#### WorkflowMBeanManagerImpl {#workflowmbeanmanagerimpl}

```java
package com.adobe.example.myapp.impl;

import java.util.*;

import org.apache.felix.scr.annotations.*;

import javax.jcr.Session;
import javax.jcr.Node;
import javax.jcr.NodeIterator;
import javax.jcr.RepositoryException;
import javax.management.ObjectName;

import org.apache.sling.jcr.api.SlingRepository;
import org.osgi.framework.ServiceRegistration;
import org.osgi.service.component.ComponentContext;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.workflow.WorkflowService;
import com.day.cq.workflow.WorkflowSession;
import com.adobe.example.myapp.api.WorkflowMBean;
import com.adobe.example.myapp.api.WorkflowMBeanManager;

/**Instantiates and registers WorkflowMBean services */
@Component(immediate=true)
@Service(value=WorkflowMBeanManager.class)
public class WorkflowMBeanManagerImpl implements WorkflowMBeanManager {
 //The ComponentContext provides access to the BundleContext
 private ComponentContext componentContext;

 //Use the SlingRepository service to read model nodes
 @Reference
        private SlingRepository repository = null;

 //Use the WorkflowService service to create WorkflowModel objects
 @Reference
 private WorkflowService workflowservice = null;

  private Session session;

         //Details about model nodes
  private static final String MODEL_ROOT ="/etc/workflow/models";
  private static final String MODEL_NODE = "model";

  private Set<String> modelIds = new HashSet<String>();

        //Storage for ServiceRegistrations for MBean services
  private Collection<ServiceRegistration> mbeanRegistrations= new Vector<ServiceRegistration>(0,1);

 @Activate
        protected void activate(ComponentContext ctx) {
             //Traverse the repository and load the model nodes
             try {
                   session = repository.loginAdministrative(null);
                   // load and store model node paths
                   if (session.nodeExists(MODEL_ROOT)) {
                          getModelIds(session.getNode(MODEL_ROOT));
                   }
                   //Create MBeans for each model
                   for(String modid: modelIds){
                    makeMBean(modid);
                    }
             }catch(Exception e){ }
          }

        /**
         * Add JMX domain and key properties to a collection
         * Instantiate a WorkflowModel and its WorkflowMBeanImpl object
         * Register the MBean OSGi service
         */
 private void makeMBean(String modelId) {
             // create MBean for the model
             try {
                 Dictionary<String, String> mbeanProps = new Hashtable<String, String>();
                 //These properties appear on the JMX Console home page
                 mbeanProps.put("jmx.objectname", "com.adobe.example:type=workflow_model,id=" + ObjectName.quote(modelId));
                 WorkflowSession wfsession = workflowservice.getWorkflowSession(session);
                 WorkflowMBeanImpl mbean = new WorkflowMBeanImpl(wfsession.getModel(modelId));

                ServiceRegistration serviceregistration = componentContext.getBundleContext().registerService(WorkflowMBean.class.getName(), mbean, mbeanProps);
                //Store the ServiceRegistration objects for deactivation
                mbeanRegistrations.add(serviceregistration);
             } catch (Throwable t) {}
         }

        /**
         * Traverses the repository branch below a given Node. Stores the path of each model node.
         */
 private void getModelIds(Node node) throws RepositoryException {
  try{
                     NodeIterator iter = node.getNodes();
                     while (iter.hasNext()) {
                           Node n = iter.nextNode();
                           //Look for "jcr:content" nodes
                           if (n.getName().equals("jcr:content")) {
                                //get the path of the model node and save it
                                if(n.hasNode(MODEL_NODE)){
                                      modelIds.add(n.getNode(MODEL_NODE).getPath());
                                 }
                           } else{
                                   //Scan child nodes
                                   getModelIds(n);
                           }
                       }
  }catch(Exception e){ }
       }

        /**
         * Log out of the JCR session and unregister WorkflowMBean services
         */
        @Deactivate
        protected void deactivate() {
          session.logout();
          session=null;
          for(ServiceRegistration sr:mbeanRegistrations){
         sr.unregister();
          }
        }
}
```

### 範例MBean的POM檔案 {#the-pom-file-for-the-example-mbean}

為方便起見，您可以將下列XML程式碼複製並貼到專案pom.xml檔案中，以建立元件組合。 POM會參照數個必要的外掛程式和相依性。

**外掛程式：**

* Apache Maven編譯器外掛程式：從原始程式碼編譯Java類別。
* Apache Felix Maven套件組合外掛程式：建立套件組合和資訊清單
* Apache Felix Maven SCR外掛程式：建立元件描述元檔案並設定服務元件資訊清單標頭。

**注意：** 在撰寫時，maven scr外掛程式與適用於Eclipse的m2e外掛程式不相容。 (請參閱 [Felix錯誤3170](https://issues.apache.org/jira/browse/FELIX-3170).) 若要使用Eclipse IDE，請安裝Maven並使用命令列介面執行建置。

#### 範例POM檔案 {#example-pom-file}

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.2-SNAPSHOT</version>
  <name>mbean-simple</name>
  <url>www.adobe.com</url>
  <description>A simple MBean</description>
  <packaging>bundle</packaging>
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <build>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>1.5</source>
                <target>1.5</target>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.felix</groupId>
                <artifactId>maven-scr-plugin</artifactId>
                <version>1.7.2</version>
                <executions>
                    <execution>
                        <id>generate-scr-scrdescriptor</id>
              <goals>
                 <goal>scr</goal>
              </goals>
            </execution>
         </executions>
            </plugin>
             <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-bundle-plugin</artifactId>
            <version>1.4.3</version>
            <extensions>true</extensions>
            <configuration>
                <instructions>
                    <Export-Package>com.adobe.example.myapp.*;version=${project.version}</Export-Package>
                </instructions>
            </configuration>
        </plugin>
        </plugins>
    </build>
    <dependencies>
        <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr.annotations</artifactId>
            <version>1.6.0</version>
            <scope>provided</scope>
        </dependency>
         <dependency>
            <groupId>org.apache.sling</groupId>
            <artifactId>org.apache.sling.api</artifactId>
            <version>2.0.8</version>
            <scope>provided</scope>
        </dependency>
         <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr</artifactId>
            <version>1.6.1-R1236132</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.sling</groupId>
            <artifactId>org.apache.sling.jcr.api</artifactId>
            <version>2.0.4</version>
        </dependency>
        <dependency>
            <groupId>com.adobe.granite</groupId>
            <artifactId>com.adobe.granite.jmx</artifactId>
            <version>0.1.6</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
       <groupId>com.day.cq.wcm</groupId>
       <artifactId>cq-wcm-mobile-api</artifactId>
       <version>5.5.2</version>
       <scope>provided</scope>
      </dependency>
      <dependency>
       <groupId>com.day.cq.workflow</groupId>
       <artifactId>cq-workflow-api</artifactId>
       <version>5.5.0</version>
       <scope>provided</scope>
      </dependency>
      <dependency>
       <groupId>javax.jcr</groupId>
       <artifactId>jcr</artifactId>
       <version>2.0</version>
       <scope>provided</scope>
      </dependency>
      <dependency>
                <groupId>org.slf4j</groupId>
  <artifactId>slf4j-api</artifactId>
  <version>1.6.4</version>
  <scope>provided</scope>
 </dependency>
    </dependencies>
</project>
```

將以下設定檔新增到您的maven設定檔案，以使用公共Adobe存放庫。

#### Maven設定檔 {#maven-profile}

```xml
<profile>
    <id>adobe-public</id>
    <activation>
         <activeByDefault>false</activeByDefault>
    </activation>
    <properties>
         <releaseRepository-Id>adobe-public-releases</releaseRepository-Id>
         <releaseRepository-Name>Adobe Public Releases</releaseRepository-Name>
         <releaseRepository-URL>https://repo1.maven.org/maven2/com/adobe/</releaseRepository-URL>
    </properties>
    <repositories>
         <repository>
             <id>adobe-public-releases</id>
             <name>Adobe  Public Repository</name>
             <url>https://repo1.maven.org/maven2/com/adobe/</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </repository>
     </repositories>
     <pluginRepositories>
         <pluginRepository>
             <id>adobe-public-releases</id>
             <name>Adobe Public Repository</name>
             <url>https://repo1.maven.org/maven2/com/adobe/</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </pluginRepository>
     </pluginRepositories>
</profile>
```
