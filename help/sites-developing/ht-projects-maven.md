---
title: 如何使用Apache Maven建立AEM專案
seo-title: 如何使用Apache Maven建立AEM專案
description: 本檔案說明如何設定以Apache Maven為基礎的AEM專案
seo-description: 本檔案說明如何設定以Apache Maven為基礎的AEM專案
uuid: 5db68639-7393-48b7-9d81-5b19b596ff21
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 3ebc1d22-a7a2-4375-9aa5-a18a7ceb446a
docset: aem65
translation-type: tm+mt
source-git-commit: 9d42526ff4c7b7d8a31690ebfb8b45d0e951ebac

---


# 如何使用Apache Maven建立AEM專案{#how-to-build-aem-projects-using-apache-maven}

## 概覽 {#overview}

本檔案說明如何設定以 [Apache Maven為基礎的AEM專案](https://maven.apache.org/)。

Apache Maven是開放原始碼工具，可自動建立並提供高品質專案資訊，以管理軟體專案。 這是AEM專案的建議建置管理工具。

以Maven為基礎建立AEM專案可為您提供多項好處：

* 不受IDE限制的開發環境
* Adobe提供的Maven原型和文物使用
* 使用Apache Sling和Apache Felix工具集進行Maven開發設定
* 輕鬆匯入IDE;例如，Eclipse和／或IntelliJ
* 輕鬆與持續整合系統整合

### Maven Project Archetypes {#maven-project-archetypes}

Adobe提供兩種Maven原型，可做為AEM專案的基準。 請參閱下列連結的詳細資訊：

* [AEM專案原型](https://github.com/adobe/aem-project-archetype)
* [Maven archetype for Single Page Applications Starter Kit](https://github.com/adobe/aem-spa-project-archetype)

## Experience Manager API相依性 {#experience-manager-api-dependencies}

### 什麼是UberJar? {#what-is-the-uberjar}

「UberJar」是Adobe提供之特殊Java封存(JAR)檔案的非正式名稱。 這些JAR檔案包含Adobe Experience manager公開的所有公開Java API。 它們也包含有限的外部程式庫，尤其是AEM中所有可用的公開API，這些API來自Apache Sling、Apache Jackrabbit、Apache Lucene、Google Guava，以及兩個用於影像處理的程式庫（Werner Randelshofer的CYMK JPEG ImageIO程式庫和TweleveWek Muxines影像庫）。 UberJar僅包含API介面和類別，這表示它們僅包含由AEM中的OSGi套件匯出的介面和類別。 它們也包含 *MANIFEST.MF* 檔案，其中包含所有這些匯出封裝的正確封裝匯出版本，因此可確保以UberJar建立的專案具有正確的封裝匯入範圍。

### 為什麼Adobe會建立UberJar? {#why-did-adobe-create-the-uberjars}

過去，開發人員必須管理相對較多的個別相依性，以至於不同AEM程式庫，而且當使用每個新API時，必須將一或多個個別相依性新增至專案。 在一個項目中，UberJar的引入導致30個單獨的依賴項被從項目中刪除。

從AEM 6.5開始，Adobe提供兩個UberJar:一個包含過時的介面，另一個包含刪除那些過時的介面。 透過在建置時明確參照某個程式碼，客戶一定會瞭解他們是否對不建議使用的程式碼有依賴性。

第二個Uber jar會移除任何已過時的類別、方法和屬性，讓客戶可以編譯並瞭解自訂代碼是否是未來證明。

### 使用哪個UberJar? {#which-uberjar-to-use}

AEM 6.5提供兩種Uber Jar:

1. Uber Jar —— 僅包含未標示為取代的公用介面。 這是建議 **使用的** UberJar，因為它可協助防範未來的程式碼基底，避免依賴已過時的API。
1. Uber Jar含過時的API —— 包含所有公用介面，包括未來AEM版本中標示為淘汰的介面。

### 我如何使用UberJar? {#how-to-i-use-the-uberjars}

如果您使用Apache Maven做為組建系統（大部分的AEM java專案都是如此），您將需要新增一或兩個元素至 *pom.xml* 檔案。 第一種是相依 *性元素* ，將實際相依性添加到項目中：

**Uber jar相依&#x200B;*性（不含已過時的API）***

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

**使用已過時的API的Uber jar依賴性**

>[!CAUTION]
>
>Adobe建議針對**不包含已過時&#x200B;*的* **API的Uber Jar進行部署，以確保您的應用程式在未來的AEM版本上正常執行。
>
>只有在依賴已過時API的代碼無法修改以隨附變更時，才能使用含已過時API支援的Uber Jar。

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis-with-deprecations</classifier>
    <scope>provided</scope>
</dependency>
```

如果您的公司已使用Maven Repository Manager（如Sonatype Nexus、Apache Archiva或JFrog Artifactory），請將適當的配置添加到項目中以引用此儲存庫管理器，並將Adobe的Maven儲存庫([https://repo.adobe.com/nexus/content/groups/public/](https://repo.adobe.com/nexus/content/groups/public/))添加到儲存庫管理器。

如果您不使用儲存庫管理器，則需要將儲存庫元 *素添加* 到 ** pom.xml檔案中：

```xml
<repositories>
    <repository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.adobe.com/nexus/content/groups/public/</url>
        <layout>default</layout>
    </repository>
</repositories>
<pluginRepositories>
    <pluginRepository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.adobe.com/nexus/content/groups/public/</url>
        <layout>default</layout>
    </pluginRepository>
</pluginRepositories>
```

### UberJar有什麼用？ {#what-can-i-do-with-the-uberjar}

使用UberJar，您可以編譯專案程式碼，此程式碼需仰賴AEM API（以及上述專案所使用的API）。 您也可以產生OSGi服務元件執行階段(SCR)和OSGi Metatype資訊。 有了一些限制，您還可以編寫和執行單元測試。

### UberJar怎麼辦？ {#what-can-t-i-do-with-the-uberjar}

由於UberJar僅包 **含** API，因此無法執行，且無法用 **於執行** Adobe Experience Manager。 若要執行AEM，您需要AEM Quickstart(單機版或Web應用程式封存(WAR)表單)。

### 您提到單元測試的限制。 請進一步說明。 {#you-mentioned-limitations-on-unit-tests-please-explain-further}

單位測試通常以三種不同的方式與產品API互動，每種方式受UberJar的影響都略有不同。

#### 使用案例#1 —— 呼叫API介面的自訂代碼 {#use-case-custom-code-which-calls-a-api-interface}

此案例最常見，涉及一些在AEM API所定義的Java介面上執行方法的自訂程式碼。 此介面的實現可以直接提供，也可以使用相關性插入模式插入。 **此使用案例可由UberJar處理。**

前者的例子是：

```java
public class ClassWhichHasAEMInterfacePassedIn {
    /**
     * Get the first length characters of the page title.
     */
    public String getTrimmedTitle(Page page, int length) {
         String title = page.getTitle();
         return StringUtils.left(title, length);
    }
}
```

後者的例子是：

```java
@Component
@Service
public class ComponentWhichHasAEMInterfaceInjected implements TitleTrimmer {
    @Reference
    private PageManagerFactory pageManagerFactory;

    /**
     * Get the first length characters of the title of the page containing the provided Resource.
     */
    public String getTrimmedTitle(Resource resource, int length) {
        PageManager pageManager = pageManagerFactory.getPageManager(resource.getResourceResolver());
        Page page = pageManager.getContainingPage(resource);
        if (page == null) {
           return null;
        }
        String title = page.getTitle();
        return StringUtils.left(title, length);
    }
}
```

若要對這些方法進行單元測試，開發人員會使用模仿架構(例如 [JMockit](http://jmockit.github.io)、 [Mockito](https://mockito.org/)、 [JMock](https://www.jmock.org/)或 [](https://easymock.org/) Easymock)，為參考的AEM API建立模擬物件。 這些樣本使用JMockit，但是對於這個特定使用案例，這些框架之間的差異基本上是同步的。

```java
@RunWith(JMockit.class)
public class ClassWhichHasAEMInterfacePassedInTest {

    @Tested
    private ClassWhichHasAEMInterfacePassedIn instance;

    @Mocked
    private Page page;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(page, 8));
    }
}
```

```java
@RunWith(JMockit.class)
public class ComponentWhichHasAEMInterfaceInjectedTest {

    @Tested
    private ComponentWhichHasAEMInterfaceInjected instance;

    @Mocked
    private Page page;

    @Mocked
    private PageManager pageManager;

    @Injectable
    private PageManagerFactory pageManagerFactory;

    @Mocked
    private Resource resource;

    @Mocked
    private ResourceResolver resourceResolver;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            resource.getResourceResolver();
            result = resourceResolver;
            pageManagerFactory.getPageManager(resourceResolver);
            result = pageManager;
            pageManager.getContainingPage(resource);
            result = page;
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(resource, 8));
    }
}
```

#### 使用案例#2 —— 呼叫API實作類別的自訂代碼 {#use-case-custom-code-which-calls-an-api-implementation-class}

這個使用案例包括呼叫AEM API中您要參照具體類別的類別的靜態或例項方法，而不是使用案例#1中的介面。

```java
public class ClassWhichUsesAStaticMethodFromAPI {

    /**
     * Get a map of asset titles to asset objects.
     *
     * @param resource either an asset resource or a folder containing assets.
     * @return an map of titles to assets. if an asset doesn't have a title, the name is used instead.
     */
    public Map<String, Asset> getAssetTitles(Resource resource) {
        Iterator<Asset> assets = DamUtil.getAssets(resource);
        Map<String, Asset> result = new HashMap<String, Asset>();
        while (assets.hasNext()) {
            Asset asset = assets.next();
            String title = asset.getMetadataValue(DamConstants.DC_TITLE);
            if (title == null) {
                title = asset.getName();
            }
            result.put(title, asset);
        }
        return result;
    }
}
```

```java
public class ClassWhichUsesAnInstanceMethodFromAPI {

    /**
     * Count the number of paragraphs in a parsys.
     *
     * @param resource the parsys resource
     * @return the count
     */
    public int countParagraphs(Resource resource) {
        return new ParagraphSystem(resource).paragraphs().size();
    }
}
```

**此使用案例可由UberJar處理**。 不過，仍建議在可能的情況下嘲笑API以進行效能測試。

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAStaticMethodFromAPITest {

    @Tested
    private ClassWhichUsesAStaticMethodFromAPI instance;

    @Mocked(stubOutClassInitialization = true)
    private DamUtil unusedDamUtil = null;

    @Mocked
    private Resource resource;

    @Test
    public void test_that_empty_iterator_produces_empty_map() {
        new Expectations() {
            {
                DamUtil.getAssets(resource);
                result = Collections.<Asset> emptySet().iterator();
            }
        };
        Map<String, Asset> result = new ClassWhichUsesAStaticMethodFromAPI().getAssetTitles(resource);
        assertNotNull(result);
        assertEquals(0, result.size());
    }
    @Test
    public void test_with_reference_search() {
        assertTrue(true);
    }
}
```

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAnInstanceMethodFromAPITest {

    @Tested
    private ClassWhichUsesAnInstanceMethodFromAPI instance;

    @Mocked
    private Resource parsys;

    @Mocked
    private Paragraph firstPar;

    @Mocked
    private Paragraph secondPar;

    @Test
    public void test_empty_parsys_returns_zero() {
        new MockUp<ParagraphSystem>() {
            @Mock
            public void $init(Resource resource) {
                assertEquals(parsys, resource);
            }
            @Mock
            public List<Paragraph> paragraphs() {
                return Collections.<Paragraph> emptyList();
            }
        };
        assertEquals(0, instance.countParagraphs(parsys));
    }
}
```

#### 使用案例#3 —— 自訂程式碼，從API擴充基本類別 {#use-case-custom-code-which-extends-a-base-class-from-the-api}

和SCR產生一樣，如果您的程式碼從AEM API擴充基本類別（抽象或具體），您必須 **使** 用UberJar才能進行測試。

## 使用Maven執行常見開發任務 {#common-development-tasks-with-maven}

### 如何新增路徑至內容模組 {#how-to-add-paths-to-the-content-module}

內容模組包含檔案src/main/content/META-INF/vault/filter.xml，其中定義由Maven建立之AEM套件的篩選器。 由Maven原型建立的檔案如下所示：

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

此檔案的使用方式有許多不同：

* 決定 `content-package-maven-plugin` 要包含在套件中的內容
* 由VLT工具決定要考慮的路徑
* 如果套件已重新內建在AEM Package Manager中，這也會定義要包含的路徑

視您的應用程式需求而定，您可能想要新增至這些路徑以包含更多內容，例如：

* 轉出設定
* BluePrint
* 工作流程模型
* 設計頁面
* 範例內容

若要新增至路徑，請新增更多 `<filter>` 元素：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
    <filter root="/etc/msm/rolloutconfigs/myrolloutconfig"/>
    <filter root="/etc/blueprints/mysite/globalsite"/>
    <filter root="/etc/workflow/models/myproject"/>
    <filter root="/etc/designs/myproject"/>
    <filter root="/content/myproject/sample-content"/>
</workspaceFilter>
```

#### 新增路徑至套件，但不同步路徑 {#adding-paths-to-the-package-without-syncing-them}

如果檔案應添加到由content-package-maven-plugin構建的包中，但不應在檔案系統和儲存庫之間同步，則可以使用文 `.vltignore` 件。 這些檔案的語法與。gitignore [檔案相同](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html) 。

例如，原型使用文 `.vltignore` 件來防止作為包的一部分安裝的JAR檔案同步回檔案系統：

#### src/main/content/jcr_root/apps/myproject/install/vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore}

```xml
*.jar
```

#### 同步路徑而不將其新增至套件 {#syncing-paths-without-adding-them-to-the-package}

在某些情況下，您可能會想要讓檔案系統和儲存庫之間的特定路徑保持同步，但是無法將這些路徑包含在內建以安裝至AEM的套件中。

典型的例子是 `/libs/foundation` 路徑。 為了進行開發，您可能希望在檔案系統中提供此路徑的內容，以便（例如，IDE）解析包含JSP的JSP包含 `/libs`。 不過，您不想將該部件包含在您建立的套件中，因為該部 `/libs` 件包含自訂實作不得修改的產品代碼。

若要達成此目的，您可以提供檔案 `src/main/content/META-INF/vault/filter-vlt.xml`。 如果此檔案存在，則它將由VLT工具使用，例如，在執行和 `vlt up``vlt ci`或設定時 `vlt sync` 使用。 content-package-maven-plugin將在建立套件時繼續 `src/main/content/META-INF/vault/filter.xml` 使用檔案。

例如，若要在本 `/libs/foundation` 機提供開發，但只要包 `/apps/myproject` 含在套件中，請使用下列兩個檔案。

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml-1}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

#### src/main/content/META-INF/vault/filter-vlt.xml {#src-main-content-meta-inf-vault-filter-vlt-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/libs/foundation"/>
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

您還需要將maven-resources-plugin重新配置為不將這些檔案包含在包中：filter.xml檔案不會在安裝套件時套用，但只有在使用套件管理員重新建立套件時才會套用。

依此方 `<resources>` 式變更內容中的區段：

#### src/main/content/pom.xml {#src-main-content-pom-xml}

```xml
<!-- ... -->
<resources>
 <resource>
  <directory>src/main/content/jcr_root</directory>
  <filtering>false</filtering>
  <excludes>
   <exclude>**/.vlt</exclude>
   <exclude>**/.vltignore</exclude>
   <exclude>libs/</exclude>
  </excludes>
 </resource>
</resources>
<!-- ... -->
```

### 如何使用JSP {#how-to-work-with-jsps}

目前所述的Maven設定會建立內容套件，其中也可包含元件及其對應的JSP。 不過，Maven會將它們視為屬於內容套件的任何其他檔案，甚至不會將它們辨識為JSP。

產生的元件在AEM中都能運作，但讓Maven知道JSP有兩個主要優點

* 如果JSP包含錯誤，則Maven會失敗，因此這些錯誤會在建立時呈現，而非在AEM中第一次編譯時呈現
* 對於可以導入Maven項目的IDE，這還可以在JSP中啟用代碼完成和標籤庫支援

啟用此設定需要兩項：

1. 添加標籤庫依賴項
1. 將JSP編譯為Maven編譯過程的一部分

#### 添加標籤庫相關性 {#adding-tag-library-dependencies}

需要將以下相關性添加 `content` 到模組的POM中。

>[!NOTE]
>
>除非您要匯入上述「匯入 [AEM產品相依性」中所述的產品相依性](#importingaemproductdependencies) ，否則還需要將這些相依性新增至父POM，以及與您的AEM設定相符的版本，如上述「新增相依性 [](#addingdependencies) 」中所述。 下面每個條目中的注釋顯示要在「相依性查找器」中搜索的包。

>[!NOTE]
>
>對 `com.adobe.granite.xssprotection` 像不包含在cq-quickstart-product-dependencies POM中，並且需要從Dependency finder中獲得的完整Maven坐標。

#### 將JSP編譯為Maven編譯階段的一部分 {#compiling-jsps-as-part-of-the-maven-compile-phase}

若要在Maven的階段編譯JSP `compile` ，我們使用Apache Sling&#39;s [Maven JspC Plugin](https://sling.apache.org/documentation/development/jspc.html) ，如下所示：

* 我們為目標設定了 `jspc` 執行(預設會將目標系結至 `compile` 階段，因此我們不需要明確指定階段)

* 我們告訴它要編譯 `${project.build.directory}/jsps-to-compile`
* 並將結果輸 `${project.build.directory}/ignoredjspc` 出至 `myproject/content/target/ignoredjspc`(

* 我們設定maven-resources-plugin，將JSP複製到 `${project.build.directory}/jsps-to-compile``libs/` generate-sources階段，並設定它不複製資料夾(因為這是AEM產品程式碼，我們不想產生我們專案編譯的相依性，也不需要驗證它是否編譯。

如上所述，我們的主要目標是驗證JSP，並確保如果JSP包含錯誤，則生成過程會失敗。 這就是為什麼我們將它們編譯到一個單獨的目錄中，而這個目錄會被忽略（事實上，隨後會立即刪除，如您稍後所見）。

Maven JspC Plugin的結果也可以隨OSGi Bundle一起打包和部署，但這有其他影響和副作用，超出了我們驗證JSP的目標。

為了刪除從JSP編譯的類，我們設定了Maven Clean插件，如下所示。 如果要檢查Maven JspC插件的結果，請在中 `mvn compile` 運 `myproject/content` 行——之後，您將在中找到結果 `myproject/content/target/ignoredjspc`)。

#### myproject/content/pom.xml {#myproject-content-pom-xml}

```xml
<build>
  <!-- ... -->
  <plugins>
    <!-- ... -->
    <plugin>
      <artifactId>maven-resources-plugin</artifactId>
      <executions>
        <execution>
          <id>copy-resources</id>
          <phase>generate-sources</phase>
          <goals>
            <goal>copy-resources</goal>
          </goals>
          <configuration>
            <outputDirectory>${project.build.directory}/jsps-to-compile</outputDirectory>
            <resources>
              <resource>
                <directory>src/main/content/jcr_root</directory>
                <excludes>
                  <exclude>libs/**</exclude>
                </excludes>
              </resource>
            </resources>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <groupId>org.apache.sling</groupId>
      <artifactId>maven-jspc-plugin</artifactId>
      <version>2.0.6</version>
      <executions>
        <execution>
          <id>compile-jsp</id>
          <goals>
            <goal>jspc</goal>
          </goals>
          <configuration>
            <jasperClassDebugInfo>false</jasperClassDebugInfo>
            <sourceDirectory>${project.build.directory}/jsps-to-compile</sourceDirectory>
            <outputDirectory>${project.build.directory}/ignoredjspc</outputDirectory>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <artifactId>maven-clean-plugin</artifactId>
      <executions>
        <execution>
          <id>remove-compiled-jsps</id>
          <goals>
            <goal>clean</goal>
          </goals>
          <phase>process-classes</phase>
          <configuration>
            <excludeDefaultDirectories>true</excludeDefaultDirectories>
            <filesets>
              <fileset>
                <directory>${project.build.directory}/jsps-to-compile</directory>
                <directory>${project.build.directory}/ignoredjspc</directory>
              </fileset>
            </filesets>
          </configuration>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

>[!NOTE]
>
>視您是否實際在中使用JSP程 `/libs` 式碼（亦即從中加入JSP）而定，您需要調整要複製哪些JSP以進行編譯。
>
>例如，如果您包 `/libs/foundation/global.jsp`括，則可以對下列配置進行 `maven-resources-plugin` 操作，而非完全跳過的配置 `/libs`。
>
>```
> <resource>  
>           <directory>src/main/content/jcr_root</directory>  
>           <includes>  
>                   <include>apps/**</include>  
>                   <include>libs/foundation/global.jsp</include>
>       </includes>  
>   </resource>  
>```
>

### 如何與SCM系統搭配使用 {#how-to-work-with-scm-systems}

使用「源配置管理」(SCM)時，您需要確保

* VCS忽略檔案系統中的非源對象
* VLT忽略VCS的對象，不將其簽入儲存庫

>[!NOTE]
>
>本說明不涵蓋如何將Maven配置為與您的SCM搭配使用， [Maven POM參考和](https://maven.apache.org/pom.html#SCM) Maven SCM Plugin的說明檔案中已詳盡說明 [](https://maven.apache.org/scm/)。

#### 要從SCM中排除的模式 {#patterns-to-exclude-from-scm}

以下是SCM中要包含的典型模式清單。 例如，如果您使用git，則可將這些項目新增至專案的檔 `.gitignore` 案。

#### 示例。gitignore {#sample-gitignore}

```shell
# Ignore VLT files
.vlt
.vlt-sync.log
.vlt-sync-config.properties

# Ignore Quickstart launches in the source tree
license.properties
crx-quickstart

# Ignore compilation results
target

# Ignore IDE and Operating System artifacts
.idea
.classpath
.metadata
.project
.settings
maven-eclipse.xml
*.iml
*.ipr
*.iws
.DS_Store
```

#### VLT中忽略單片機控制檔案 {#ignoring-scm-control-files-in-vlt}

在某些情況下，您的內容源樹中可能有SCM控制檔案，您不希望將其簽入儲存庫。

請考慮以下情況：

原型已建立。vltignore檔案，以防止已安裝的bundle jar檔案同步回檔案系統：

#### src/main/content/jcr_root/apps/myproject/install/vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-1}

```shell
*.jar
```

顯然，您也不希望此檔案出現在您的SCM中，因此，如果您使用git，您會新增對應的檔案。 `gitignore` 檔案：

#### src/main/content/jcr_root/apps/myproject/install/.gitignore {#src-main-content-jcr-root-apps-myproject-install-gitignore}

```shell
*.jar
```

作為。 `gitignore` 檔案也不應進入儲存庫。 `vltignore` 需要擴充檔案才能包含。 `gitignore` 檔案：

#### src/main/content/jcr_root/apps/myproject/install/vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-2}

```shell
*.jar
.gitignore
```

### 如何使用部署設定檔 {#how-to-work-with-deployment-profiles}

如果您的建立程式是大型開發生命週期管理設定的一部分，例如持續整合程式，則您通常需要部署至其他電腦，而不只是開發人員的本機執行個體。

對於這類情況，您可以輕鬆將新 [的Maven Build Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) 添加到項目的POM中。

以下範例新增了描述檔 `integrationServer`，可重新定義作者和發佈例項的主機名稱和埠。 您可以從專案根目錄執行maven，如下所示，部署至這些伺服器。

```shell
# install on integration test author
$ mvn -PautoInstallPackage -PintegrationServer install

# install on integration test publisher
$ mvn -PautoInstallPackagePublish -PintegrationServer install
```

#### myproject/pom.xml {#myproject-pom-xml}

```xml
<profiles>

    <!-- ... -->

    <profile>
        <id>integrationServer</id>
        <properties>
            <crx.host>dev-author.intranet</crx.host>
            <crx.port>5502</crx.port>
            <publish.crx.host>dev-publish.intranet</publish.crx.host>
            <publish.crx.port>5503</publish.crx.port>
        </properties>
    </profile>
</profiles>
```

### 如何與AEM Communities搭配使用 {#how-to-work-with-aem-communities}

取得AEM Communities功能授權時，需要額外的APIjar。

如需詳細資訊，請參 [閱「使用Maven for Communities」](/help/communities/maven.md)
