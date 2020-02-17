---
title: 整合服務與JMX主控台
seo-title: 整合服務與JMX主控台
description: 公開服務屬性和操作，通過建立和部署MBeans來使用JMX控制台管理服務來啟用管理任務
seo-description: 公開服務屬性和操作，通過建立和部署MBeans來使用JMX控制台管理服務來啟用管理任務
uuid: 4a489a24-af10-4505-8333-aafc0c81dd3e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 83c590e0-2e6c-4499-a6ea-216e4c7bc43c
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 整合服務與JMX主控台{#integrating-services-with-the-jmx-console}

使用JMX主控台建立和部署MBeans以管理服務。 公開服務屬性和操作，以便執行管理任務。

如需有關使用JMX主控台的詳細資訊，請參 [閱使用JMX主控台監控伺服器資源](/help/sites-administering/jmx-console.md)。

## Felix和CQ5中的JMX架構 {#the-jmx-framework-in-felix-and-cq}

在Apache Felix平台上，您可將MBean部署為OSGi服務。 在OSGi服務註冊表中註冊MBean服務時，Aries JMX白板模組將自動向MBean伺服器註冊MBean。 然後MBean便可用於JMX控制台，該控制台會顯示公共屬性和操作。

![jmxweithbijj](assets/jmxwhiteboard.png)

## 為CQ5和CRX建立MBean {#creating-mbeans-for-cq-and-crx}

您為管理CQ5或CRX資源而建立的MBeans是以javax.management.DynamicMBean介面為基礎。 要建立它們，請遵循JMX規範中規定的常規設計模式：

* 建立管理介面，包括get、set和is方法來定義屬性，以及其他方法來定義操作。
* 建立實作類別。 類必須實作DynamicMBean，或擴充DynamicMBean的實作類。
* 請遵循標準命名慣例，讓實作類別的名稱是具有MBean字尾的介面名稱。

除了定義管理介面外，該介面還定義了OSGi服務介面。 實現類實現OSGi服務。

### 使用注釋提供MBean資訊 {#using-annotations-to-provide-mbean-information}

[com.adobe.granite.jmx.annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/jmx/annotation/package-summary.html) 套件提供數個註解和類別，以輕鬆將MBean中繼資料提供至JMX主控台。 使用這些注釋和類，而不是直接向MBean的MBeanInfo對象添加資訊。

**註解**

將註解新增至管理介面，以指定MBean中繼資料。 JMX主控台會針對所部署的每個實作類別顯示資訊。 下列註解可供使用(如需完整資訊，請參 [閱com.adobe.granite.jmx.annotation JavaDocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/jmx/annotation/package-summary.html)):

* **** 說明：提供MBean類或方法的說明。 在類聲明中使用時，該說明將顯示在MBean的JMX控制台頁面上。 在方法上使用時，說明會顯示為對應屬性或操作的暫留文字。
* **** 影響：方法的影響。 有效參數值是 [javax.management.MBeanOperationInfo定義的欄位](https://docs.oracle.com/javase/1.5.0/docs/api/javax/management/MBeanOperationInfo.html)。

* **** 名稱：指定操作參數要顯示的名稱。 使用此注釋覆蓋介面中使用的方法參數的實際名稱。
* **** OpenTypeInfo:指定在JMX控制台中用於表示複合資料或表格資料的類。 用於Open MBean
* **** TabularTypeInfo:用於注釋用於表示表格資料的類。

**類別**

提供的類用於建立使用添加到其介面的注釋的動態MBean:

* **** AnnotatedStandardMBean:javax.management.StandardMBean類的子類，它自動為JMX控制台提供注釋元資料。
* **** OpenAnnotatedStandardMBean:AnnotatedStandardMBean類的子類，用於建立使用OpenTypeInfo注釋的Open Mbean。

### 開發MBean {#developing-mbeans}

通常，您的MBean是您要管理的OSGi服務的反映。 在Felix平台上，您建立MBean的方式與在其他Java伺服器平台上部署的方式相同。 主要區別是，您可以使用注釋來指定MBean資訊：

* 管理介面：使用getter、setter和is方法定義屬性。 使用任何其他公用方法定義操作。 使用注釋為BeanInfo對象提供元資料。
* MBean類：建置管理介面。 擴充AnnotatedStandardMBean類別，以便處理介面上的註解。

以下示例MBean提供了有關CRX儲存庫的資訊。 此介面使用「說明」註解來提供JMX主控台的資訊。

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

實作類別使用SlingRepository服務來擷取有關CRX存放庫的資訊。

#### MBean實施類 {#mbean-implementation-class}

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

下圖顯示JMX控制台中此MBean的頁面。

![jmxdescription](assets/jmxdescription.png)

### 註冊MBean {#registering-mbeans}

當您將MBean註冊為OSGi服務時，它們會自動向MBean伺服器註冊。 若要在CQ5上安裝MBean，請將它加入套件中，並像匯出任何其他OSGi服務一樣匯出MBean服務。

除了OSGi相關元資料外，您還必須提供Aries JMX白板模組在MBean伺服器中註冊MBean所需的元資料：

* **** DynamicMBean介面的名稱：聲明MBean服務實現 `javax.management.DynamicMBea`n介面。 此聲明通知Aries JMX白板模組該服務是MBean服務。

* **** MBean域和密鑰屬性：在Felix上，您會將此資訊提供為MBean的OSGi服務的屬性。 這與您通常在對象中向MBean伺服器提供的資訊相 `javax.management.ObjectName` 同。

當您的MBean反映單一服務時，只需要MBean服務的單個實例。 在本例中，如果您使用Felix SCR Maven增效模組，則可以使用MBean實作類別上的Apache Felix Service Component Runtime(SCR)註解來指定JMX相關元資料。 要實例化多個MBean實例，可以建立另一個類，用於執行MBean的OSGi服務的註冊。 在此例中，JMX相關中繼資料會在執行時期產生。

**單一MBean**

可在設計時為其定義所有屬性和操作的MBeans可使用MBean實現類中的SCR注釋進行部署。 在以下示例中，注 `value` 釋的屬性 `Service` 聲明服務實現了接 `DynamicMBean` 口。 注 `name` 釋的屬性指 `Property` 定JMX域和鍵屬性。

#### 具有SCR注釋的MBean實施類 {#mbean-implementation-class-with-scr-annotations}

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

**多個MBean服務實例**

要管理受管理服務的多個實例，請建立相應MBean服務的多個實例。 此外，在啟動或停止受管理的實例時，應建立或刪除MBean服務實例。 您可以建立MBean管理器類，在運行時實例化MBean服務，並管理服務生命週期。

使用BundleContext將MBean註冊為OSGi服務。 在Dictionary物件中加入JMX相關資訊，以做為BundleContext.registerService方法的引數。

在以下代碼示例中，ExampleMBean服務是以寫程式方式註冊的。 componentContext物件是ComponentContext，可提供BundleContext的存取權。

#### 程式碼片段：程式化MBean服務註冊 {#code-snippet-programmatic-mbean-service-registration}

```java
Dictionary mbeanProps = new Hashtable();
mbeanProps.put("jmx.objectname", "com.adobe.example:type=CRX");
ExampleMBeanImpl mbean = new ExampleMBeanImpl();
ServiceRegistration serviceregistration =
            componentContext.getBundleContext().registerService(DynamicMBean.class.getName(), mbean, mbeanProps);
```

下一節中的示例MBean提供了更多詳細資訊。

當服務配置儲存在儲存庫中時， MBean服務管理器很有用。 管理器可以檢索服務資訊，並使用它來配置和建立相應的MBean。 管理器類還可以監聽儲存庫更改事件並相應地更新MBean服務。

## 範例：使用JMX監控工作流模型 {#example-monitoring-workflow-models-using-jmx}

此示例中的MBean提供了有關儲存在儲存庫中的CQ5工作流模型的資訊。 MBean管理器類基於儲存在儲存庫中的工作流模型建立MBean，並在運行時註冊其OSGi服務。 此示例由包含以下成員的單個束組成：

* WorkflowMBean:管理介面。
* WorkflowMBeanImpl:MBean實施類。
* WorkflowMBeanManager:MBean管理器類的介面。
* WorkflowMBeanManagerImpl:MBean管理器的實施類。

**** 注意：為簡單起見，此範例中的程式碼不會執行記錄或回應拋出的例外。

WorkflowMBeanManagerImpl包含元件啟動方法。 在激活元件時，方法將執行以下任務：

* 獲取包的BundleContext。
* 查詢儲存庫以獲取現有工作流模型的路徑。
* 為每個工作流模型建立MBean。
* 向OSGi服務註冊表註冊MBean。

MBean中繼資料會在JMX主控台中顯示，其中包含com.adobe.example網域、workflow_model類型，而「屬性」是工作流程模型設定節點的路徑。

![jmxworkflowbean](assets/jmxworkflowmbean.png)

### 範例MBean {#the-example-mbean}

此示例要求MBean介面和實現，這是介面上的 `com.day.cq.workflow.model.WorkflowModel` 反映。 MBean非常簡單，因此示例可以專注於設計的配置和部署方面。 MBean會公開單一屬性，即模型名稱。

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

### 示例MBean管理器 {#the-example-mbean-manager}

WorkflowMBeanManager服務包含用於建立WorkflowMBean服務的元件激活方法。 服務實施包括以下方法：

* 啟用：該組分活化劑。 建立用於讀取WorkflowModel配置節點的JCR會話。 儲存模型配置的根節點在靜態欄位中定義。 配置節點的名稱也在靜態欄位中定義。 此方法調用獲取節點模型路徑並建立模型WorkflowMBeans的其他方法。
* getModelIds:遍歷根節點下的儲存庫並檢索每個模型節點的路徑。
* makeMBean:使用模型路徑建立WorkflowModel對象，為其建立WorkflowMBean，並註冊其OSGi服務。

>[!NOTE]
>
>WorkflowMBeanManager實施僅為激活元件時存在的模型配置建立MBean服務。 更強大的實施會監聽有關新模型配置和對現有模型配置的更改或刪除的儲存庫事件。 發生更改時，管理員可以建立、修改或刪除相應的WorkflowMBean服務。


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

### 示例MBean的POM檔案 {#the-pom-file-for-the-example-mbean}

為方便起見，您可以將下列XML程式碼複製並貼至您的pom.xml專案檔案，以建立元件套裝。 POM引用了幾個必需的插件和從屬關係。

**外掛程式:**

* Apache Maven Compiler Plugin:從原始碼編譯Java類。
* Apache Felix Maven Bundle Plugin:建立整合與資訊清單
* Apache Felix Maven SCR Plugin:建立元件描述符檔案並配置service-component manifest標題。

**** 注意：在編寫時，mavenscr外掛程式與Eclipse的m2e外掛程式不相容。 (請參 [閱Felix bug 3170](https://issues.apache.org/jira/browse/FELIX-3170))。若要使用Eclipse IDE，請安裝Maven並使用命令列介面來執行組建。

#### 示例POM檔案 {#example-pom-file}

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

將下列設定檔新增至您的主版設定檔案，以使用公用的Adobe儲存庫。

#### Maven Profile {#maven-profile}

```xml
<profile>
    <id>adobe-public</id>
    <activation>
         <activeByDefault>false</activeByDefault>
    </activation>
    <properties>
         <releaseRepository-Id>adobe-public-releases</releaseRepository-Id>
         <releaseRepository-Name>Adobe Public Releases</releaseRepository-Name>
         <releaseRepository-URL>https://repo.adobe.com/nexus/content/groups/public</releaseRepository-URL>
    </properties>
    <repositories>
         <repository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
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
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
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
