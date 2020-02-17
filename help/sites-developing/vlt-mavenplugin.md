---
title: 使用Maven管理包
seo-title: 使用Maven管理包
description: 使用Content Package Maven增效模組，將套件管理工作整合至您的Maven專案
seo-description: 使用Content Package Maven增效模組，將套件管理工作整合至您的Maven專案
uuid: fa73f0d6-8848-4911-9b96-311c875b45be
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 943de371-0149-4307-be3a-b11c590b3451
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 使用Maven管理包{#managing-packages-using-maven}

使用Content Package Maven增效模組，將套件管理工作整合至您的Maven專案。 外掛程式目標和參數可讓您自動執行許多通常使用「套件管理員」頁面或FileVault命令列執行的工作：

* 從檔案系統中的檔案建立新包。
* 在CRX或CQ伺服器上安裝和解除安裝套件。
* 生成已在伺服器上定義的包。
* 獲取伺服器上安裝的軟體包清單。
* 從伺服器中刪除包。

## 將內容包Maven插件添加到POM檔案 {#adding-the-content-package-maven-plugin-to-the-pom-file}

要使用Content Package Maven Plugin，請在POM檔案的構建元素中添加以下插件元素：

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>0.0.24</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

若要啟用Maven下載外掛程式，請使用本頁「取得內容套件Maven外掛程式 [」區段中提供的描述檔](#obtaining-the-content-package-maven-plugin) 。

## Content Package Maven Plugin的目標 {#goals-of-the-content-package-maven-plugin}

「內容套件」外掛程式提供的目標和目標參數在後面的章節中有說明。 「常用參數」(Common Parameters)部分中描述的參數可用於大多數目標。 適用於一個目標的參數在該目標的一節中有說明。

**外掛程式首碼**

外掛程式首碼是content-package。 使用此前置詞從命令行執行目標，如下例所示：

```shell
mvn content-package:build
```

**參數首碼**

除非另有說明，外掛程式目標和參數會使用Vault首碼，如下列範例所示：

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

**Proxy**

使用CRX或CQ伺服器之Proxy的目標會使用Maven設定中找到的第一個有效Proxy設定。 如果未找到代理配置，則不使用代理。 請參閱「常用設定」區段中的useProxy參數。

### 通用參數 {#common-parameters}

下表中的參數是所有目標的通用參數，除非在「目標」列中注明。

<table>
 <tbody>
  <tr>
   <th>名稱</th>
   <th>類型</th>
   <th>必要</th>
   <th>預設值</th>
   <th>說明</th>
   <th>目標</th>
  </tr>
  <tr>
   <td>failOnError</td>
   <td>布林值</td>
   <td>否</td>
   <td>false</td>
   <td>值的值會 <code>true</code> 在發生錯誤時導致構建失敗。 值使生 <code>false</code> 成忽略錯誤。</td>
   <td>除包外的所有目標。</td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>字串</td>
   <td>構建：是安裝<br /> :無<br /> rm:是</td>
   <td>構建：沒有預設值。<br /> 安裝：Maven項目的artifactId屬性的值。</td>
   <td>要操作的包的名稱。</td>
   <td>除ls以外的所有目標。</td>
  </tr>
  <tr>
   <td>密碼</td>
   <td>字串</td>
   <td>是</td>
   <td>管理員</td>
   <td>用於CRX伺服器驗證的口令。</td>
   <td>除包外的所有目標。</td>
  </tr>
  <tr>
   <td>serverId</td>
   <td>字串</td>
   <td>否</td>
   <td></td>
   <td>要從中檢索用戶名和口令以進行驗證的伺服器ID。</td>
   <td>除包外的所有目標。</td>
  </tr>
  <tr>
   <td>targetURL</td>
   <td>字串</td>
   <td>是</td>
   <td>http://localhost:4502/<br /> crx/packmgr/<br /> service.jsp</td>
   <td>CRX套件管理員的HTTP服務API URL。</td>
   <td>除包外的所有目標。</td>
  </tr>
  <tr>
   <td>超時</td>
   <td>int</td>
   <td>否</td>
   <td>5</td>
   <td>與包管理器服務通信的連接超時（以秒為單位）。</td>
   <td>除包外的所有目標。</td>
  </tr>
  <tr>
   <td>useProxy</td>
   <td>布林值</td>
   <td>否</td>
   <td>true</td>
   <td>確定是否從Maven設定檔案使用代理配置。 值使用 <code>true</code> 找到的第一個活動代理配置來代理對包管理器的請求。 值false會導致不使用任何代理。</td>
   <td>除包外的所有目標。</td>
  </tr>
  <tr>
   <td>userId</td>
   <td>字串</td>
   <td>是</td>
   <td>管理員</td>
   <td>要向CRX伺服器驗證的用戶名。</td>
   <td>除包外的所有目標。</td>
  </tr>
  <tr>
   <td>verbose</td>
   <td>布林值</td>
   <td>否</td>
   <td>false</td>
   <td>啟用或禁用詳細記錄。 值啟用詳 <code>true</code> 細記錄。</td>
   <td>除包外的所有目標。</td>
  </tr>
 </tbody>
</table>

### build {#build}

建立已在AEM例項上定義的內容套件。

>[!NOTE]
>
>此目標不需要在Maven專案中執行。

#### 參數 {#parameters}

構建目標的所有參數都在「常用參數」 [部分中說明](#common-parameters) 。

#### 例如 {#example}

下列範例會建置AEM例項上安裝的workflow-mbean套件，其IP位址為10.36.79.223。目標使用以下命令執行：

```shell
mvn content-package:build
```

以下POM檔案位於命令行工具的當前目錄中。 POM指定包名和包服務的URL。

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### install {#install}

在儲存庫中安裝軟體包。 執行此目標不需要Maven項目。 其目標將綁定到Maven構建生命週期的「安裝」階段。

#### 參數 {#parameters-1}

除了下列參數外，請參閱「公用參數」( [Common Parameters)部分中的說](#common-parameters) 明。

<table>
 <tbody>
  <tr>
   <th>名稱</th>
   <th>類型</th>
   <th>必要</th>
   <th>預設值</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>藏物</td>
   <td>字串</td>
   <td>否</td>
   <td>Maven項目的artifactId屬性的值。</td>
   <td>格式groupId:artifactId:version[:packaging]的字串。</td>
  </tr>
  <tr>
   <td>artifactId</td>
   <td>字串</td>
   <td>否</td>
   <td></td>
   <td>要安裝的對象的ID</td>
  </tr>
  <tr>
   <td>groupId</td>
   <td>字串</td>
   <td>否</td>
   <td></td>
   <td>要安裝的對象的groupId</td>
  </tr>
  <tr>
   <td>安裝</td>
   <td>布林值</td>
   <td>否</td>
   <td>true</td>
   <td>確定是否在上載包時自動解壓縮包。 值true會解除封裝套件，而false則不會解除封裝套件的包裝。</td>
  </tr>
  <tr>
   <td>localRepository</td>
   <td>org.apache.maven。<br /> 藏物。 儲存庫。<br /> ArtifactRepository</td>
   <td>否</td>
   <td>localRepository系統變數的值。</td>
   <td>本地Maven儲存庫。 您無法使用外掛程式設定來設定此參數。 系統屬性一律使用。</td>
  </tr>
  <tr>
   <td>packageFile</td>
   <td>java.io.File</td>
   <td>否</td>
   <td>為Maven項目定義的主對象。</td>
   <td>要安裝的軟體包檔案的名稱。</td>
  </tr>
  <tr>
   <td>包裝</td>
   <td>字串</td>
   <td>否</td>
   <td>ZIP</td>
   <td>要安裝的對象的封裝類型</td>
  </tr>
  <tr>
   <td>pomRemoteRepositories</td>
   <td>java.util.list</td>
   <td>是</td>
   <td>為Maven項目定義的remoteAtifactRepositories屬性的值。</td>
   <td>此值無法使用外掛程式設定來設定。 必須在專案中指定值。 </td>
  </tr>
  <tr>
   <td>project</td>
   <td>org.apache.maven。<br /> project.MavenProject</td>
   <td>是</td>
   <td>為其配置插件的項目。</td>
   <td>馬文的專案。 專案是隱式的，因為專案包含外掛程式設定。</td>
  </tr>
  <tr>
   <td>repositoryId <i>(POM)</i><br /> repoID <i>（命令行）</i></td>
   <td>字串</td>
   <td>否</td>
   <td>溫度</td>
   <td>從中檢索對象的儲存庫的ID。 在POM中，使用repositoryID。 在命令行中，使用repoID。</td>
  </tr>
  <tr>
   <td>repositoryUrl <i>(POM)</i><br /> repoURL <i>（命令行）</i></td>
   <td>字串</td>
   <td>否</td>
   <td></td>
   <td>從中檢索對象的儲存庫的URL。 在POM中，使用repositoryURL。 在命令行中，使用repoURL。</td>
  </tr>
  <tr>
   <td>版本</td>
   <td>字串</td>
   <td>否</td>
   <td></td>
   <td>要安裝的對象版本。</td>
  </tr>
 </tbody>
</table>

#### 例如 {#example-1}

以下範例會建立包含workflow-mbean OSGi套件的套件(請參閱 [build](#build) goal的範例)，然後安裝此套件。 由於安裝目標綁定到軟體包安裝階段，因此以下命令將執行安裝目標：

```shell
mvn install
```

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

### ls {#ls}

列出部署到包管理器的包。

#### 參數 {#parameters-2}

ls目標的所有參數都在「公用參數」( [Common Parameters)部分中](#common-parameters) 。

#### 例如 {#example-2}

下列範例列出AEM例項中安裝的套件，其IP位址為10.36.79.223。目標使用以下命令執行：

```shell
mvn content-package:ls
```

以下POM檔案位於命令行工具的當前目錄中。 POM指定包服務的URL。

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### rm {#rm}

從包管理器中刪除包。

#### 參數 {#parameters-3}

rm目標的所有參數都在「公用參數」( [Common Parameters)部分中](#common-parameters) 。

#### 例如 {#example-3}

下列範例會移除AEM例項上安裝的IP位址為10.36.79.223的workfow-mbean套件。目標使用以下命令執行：

```shell
mvn content-package:rm
```

以下POM檔案位於命令行工具的當前目錄中。 POM指定包服務的URL和包的名稱。

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
                    <name>workflow-mbean</name>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### uninstall {#uninstall}

卸載軟體包。 該軟體包仍處於卸載狀態。

#### 參數 {#parameters-4}

卸載目標的所有參數都在「常用參數」( [Common Parameters)部分中](#common-parameters) 。

#### 例如 {#example-4}

下列範例會解除安裝IP位址為10.36.79.223之AEM例項上所安裝的workflow-mbean套件。目標使用以下命令執行：

```shell
mvn content-package:uninstall
```

以下POM檔案位於命令行工具的當前目錄中。 POM指定包名和包服務的URL。

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### package {#package}

建立內容套件。 軟體包目標的預設配置包括保存已編譯檔案的目錄的內容。 執行軟體包目標需要編譯構建階段完成。 軟體包目標綁定到Maven構建生命週期的軟體包階段。

#### 參數 {#parameters-5}

除了下列參數外，請參閱「公用參數」( `name` Common Parameters)部分中 [的參數說明](#common-parameters) 。

<table>
 <tbody>
  <tr>
   <th>名稱</th>
   <th>類型</th>
   <th>必要</th>
   <th>預設值</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>封存</td>
   <td>org.apache.maven。<br /> archiver。<br /> MavenArchiveConfiguration</td>
   <td>否</td>
   <td></td>
   <td>要使用的存檔配置。 請參 <a href="https://maven.apache.org/shared/maven-archiver/index.html">閱Maven Archiver的檔案</a>。</td>
  </tr>
  <tr>
   <td>builtContentDirectory</td>
   <td>java.io.File</td>
   <td>是</td>
   <td>Maven組建版本的輸出目錄的值。</td>
   <td>包含要包含在包中的內容的目錄。</td>
  </tr>
  <tr>
   <td>依賴性</td>
   <td>java.util.list</td>
   <td>否</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>embeddedTarget</td>
   <td>java.lang.String</td>
   <td>否</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>嵌入式</td>
   <td>java.util.list</td>
   <td>否</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>failOnMissingEmbed</td>
   <td>布林值</td>
   <td>是</td>
   <td>false</td>
   <td>如果值為true，則當在項目相關性中找不到嵌入對象時，生成會失敗。 值offalse會導致組建忽略錯誤。</td>
  </tr>
  <tr>
   <td>filterSource</td>
   <td>java.io.File</td>
   <td>否</td>
   <td></td>
   <td>指定工作區篩選器源的檔案。 在配置中指定並通過嵌入式或子包插入的過濾器與檔案內容合併。</td>
  </tr>
  <tr>
   <td>篩選器</td>
   <td>com.day.jcr。<br /> vault.maven.pack.impl<br /> DefaultWorkspaceFilter</td>
   <td>否</td>
   <td></td>
   <td>包含定義套件內容的篩選元素。 執行時，篩選器會包含在filter.xml檔案中。 請參閱下方的「使用篩選」區段。</td>
  </tr>
  <tr>
   <td>finalName</td>
   <td>java.lang.String</td>
   <td>是</td>
   <td>maven項目（構建階段）中定義的finalName。</td>
   <td>生成的包ZIP檔案的名稱，不帶。zip檔案副檔名。</td>
  </tr>
  <tr>
   <td>群組</td>
   <td>java.lang.String</td>
   <td>是</td>
   <td>Maven專案中定義的groupID。</td>
   <td>產生的內容套件的groupId。 此值是內容套件的目標安裝路徑的一部分。</td>
  </tr>
  <tr>
   <td>outputDirectory</td>
   <td>java.io.File</td>
   <td>是</td>
   <td>在Maven項目中定義的構建目錄。</td>
   <td>保存內容包的本地目錄。</td>
  </tr>
  <tr>
   <td>前置詞</td>
   <td>java.lang.String</td>
   <td>否</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>project</td>
   <td>org.apache.maven。<br /> project.MavenProject</td>
   <td>是</td>
   <td></td>
   <td>馬文的專案。</td>
  </tr>
  <tr>
   <td>屬性</td>
   <td>java.util.Map</td>
   <td>否</td>
   <td></td>
   <td>您可在properties.xml檔案中設定的其他屬性。 這些屬性無法覆寫下列預先定義的屬性：
    <ul>
     <li>群組：使用群組參數來設定</li>
     <li>名稱：使用name參數來設定</li>
     <li>版本：使用版本參數來設定</li>
     <li>說明：從專案說明設定</li>
     <li>groupId:maven項目描述符的groupId</li>
     <li>artifactId:maven項目描述符的artifactId</li>
     <li>相關性：使用相依性參數來設定</li>
     <li>createdBy:user.name系統屬性的值</li>
     <li>已建立：當前系統時間</li>
     <li>requiresRoot:使用requiresRoot參數來設定</li>
     <li>packagePath:自動從組和包名稱生成</li>
    </ul> </td>
  </tr>
  <tr>
   <td>requiresRoot</td>
   <td>布林值</td>
   <td>是</td>
   <td>false</td>
   <td>定義軟體包是否需要root。 這會成為properties.xml檔案的&lt;code&gt;requiresRoot&lt;/code&gt;屬性。</td>
  </tr>
  <tr>
   <td>subPackages</td>
   <td>java.util.list</td>
   <td>否</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>版本</td>
   <td>java.lang.String</td>
   <td>是</td>
   <td>Maven專案中定義的版本</td>
   <td>內容套件的版本。</td>
  </tr>
  <tr>
   <td>workDirectory</td>
   <td>java.io.File</td>
   <td>是</td>
   <td>在Maven項目（構建階段）中定義的目錄。</td>
   <td>包含要包含在包中的內容的目錄。</td>
  </tr>
 </tbody>
</table>

#### 使用濾鏡 {#using-filters}

使用篩選元素來定義套件內容。 篩選器會新增至套件檔案中的 `META-INF/vault/filter.xml` workspaceFilter元素。

以下篩選器示例顯示要使用的XML結構：

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

**匯入模式**

元 `mode` 素定義導入包時對儲存庫的影響。 可使用下列值：

* **** 合併：將添加包中尚未在儲存庫中的內容。 包和儲存庫中的內容保持不變。 系統不會從儲存庫中刪除任何內容。
* **** 取代：不在儲存庫中的包中的內容將添加到儲存庫中。 儲存庫中的內容將替換為包中的匹配內容。 當內容不存在於包中時，內容將從儲存庫中刪除。
* **** 更新：不在儲存庫中的包中的內容將添加到儲存庫中。 儲存庫中的內容將替換為包中的匹配內容。 現有內容從儲存庫中刪除。

當篩選器不含元 `mode` 素時，會使用預 `replace` 設值。

#### 例如 {#example-5}

下面的示例建立包含workflow-mbean OSGi包的包。 POM檔案將jcr_root目錄標識為builtContentDirectory屬性的值。 jcr_root目錄包含映射儲存庫的目錄結構中的包JAR檔案：

`jcr_root/apps/myapp/install/workflow-mbean-0.03-SNAPSHOT.jar`

由於目標綁定到包構建階段，因此以下命令將執行包目標：

`mvn package`

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

您不必在外掛 `package` 程式區段中表 `executions` 達目標，而 `content-package` 是可以用作專案元素的 `packaging` 值：

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
  <packaging>content-package</packaging>
  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

### 說明 {#help}

#### 參數 {#parameters-6}

| 名稱 | 類型 | 必要 | 預設值 | 說明 |
|---|---|---|---|---|
| detail | 布林值 | 否 | false | 確定是否顯示每個目標的所有可設定屬性。 值true會顯示所有可設定的屬性。 |
| 目標 | 字串 | 否 |  | 要顯示幫助的目標名稱。 如果未指定任何值，則會顯示所有目標的說明。 |
| indentSize | int | 否 | 2 | 用於每個級別縮排的空格數。 如果您指定值，該值應為正數。 |
| lineLength | int | 否 | 80 | 顯示線的最大長度。 如果您指定值，該值應為正數。 |

## 取得Content Package Maven Plugin {#obtaining-the-content-package-maven-plugin}

外掛程式可從公用Adobe儲存庫取得。 若要下載外掛程式，請將下列Maven描述檔新增至您的Maven設定檔，然後加以啟動。 當您使用Maven命令時，外掛程式會視需要下載到您的本機儲存庫。

>[!NOTE]
>
>Adobe Public Releases儲存庫不可瀏覽，因此使用Web瀏覽器瀏覽到儲存庫URL會導致「找不到」錯誤。 但是， Maven可以訪問儲存庫目錄。

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

## 將OSGi Bundles內嵌在內容套件中 {#embedding-osgi-bundles-in-a-content-package}

使用Content Package Maven Plugin將OSGi bundles內嵌至內容套件。 若要嵌入套件，請實作下列組態：

* 必須將包聲明為Maven項目的從屬關係。
* 外掛程式設定會使用套件中所需的套件路徑來參照套件。

下列範例POM會建立包含Apache Sling JCR UserManager套件的套件。 在包中，包JAR位於以下文 `jcr_root/apps/myapp/install` 件夾：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
             https://maven.apache.org/maven-v4_0_0.xsd">
 <modelVersion>4.0.0</modelVersion>
   <groupId>com.adobe.example.myapp</groupId>
 <artifactId>embedded-example</artifactId>
 <packaging>content-package</packaging>
 <version>1.0.0-SNAPSHOT</version>

   <build>
 <plugins>
     <plugin>
        <groupId>com.day.jcr.vault</groupId>
      <artifactId>content-package-maven-plugin</artifactId>
      <version>0.0.24</version>
      <extensions>true</extensions>
      <configuration>
   <filters>
       <filter>
    <root>/apps/myapp</root>
       </filter>
    </filters>
    <embeddeds>
       <embedded>
    <groupId>org.apache.sling</groupId>
    <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
    <target>/apps/myproject/install</target>
        </embedded>
    </embeddeds>
       </configuration>
  </plugin>
    </plugins>
    </build>
    <dependencies>
 <dependency>
      <groupId>org.apache.sling</groupId>
      <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
      <version>2.2.0</version>
 </dependency>
    </dependencies>
</project>
```

## 在包中包括縮圖影像或屬性檔案 {#including-a-thumbnail-image-or-properties-file-in-the-package}

替換預設包配置檔案以自定義包屬性。 例如，在「套件管理員」和「套件共用」中加入縮圖影像以區分套件。

在包中，FileVault特定檔案位於/META-INF/vault資料夾中。 源檔案可以位於檔案系統中的任意位置。 在POM檔案中，定義構建資源，將源檔案複製到目標/vault-work/META-INF，以便包含在包中。

以下POM代碼將項目源的META-INF資料夾中的檔案添加到包中：

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

以下POM代碼僅將縮圖影像添加到包中。 縮圖影像必須命名為thumbnail.png，且必須位於套件的META-INF/vault/definition資料夾中。 在此示例中，源檔案位於項目的/src/main/content/META-INF/vault/definition資料夾中：

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## 使用原型產生AEM專案 {#using-archetypes-to-generate-aem-projects}

有數種Maven原型可供產生AEM專案。 使用符合您發展目標的原型：

* 安裝AEM應用程式資源的內容套件：簡 [單內容包原型](#simple-content-package-archetype)
* 包含協力廠商對象的內容套件： [simple-content-package-with-embedded-archetype](#simple-content-package-with-embedded-archetype)。
* 一種多模組應用程式，它適合Java類和單元測試的開發： [multimodule-content-package-archetype](#multimodule-content-package-archetype)。

>[!NOTE]
>
>Apache Sling專案也提供適用於AEM開發的原型。 這些檔案記錄在 [https://sling.apache.org/site/maven-archetypes.html](https://sling.apache.org/documentation/development/maven-archetypes.html)。

每個原型都生成以下項目：

* 項目資料夾結構。
* POM檔案。
* FileVault配置檔案。

Adobe公用Maven儲存庫提供原型文物。 要下載並執行原型，請使用Maven原型：generate命令的參數來標識原型和Adobe儲存庫：

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId={id_of_archetype} -DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

Maven原型外掛程式在shell或命令提示中使用互動模式來收集您專案的相關資訊。 您提供的資訊可用來設定各種專案屬性，例如檔案夾名稱和物件ID。

**POM檔案**

產生的POM檔案包含指令，可用來編譯程式碼、建立組合，以及將它們部署在封裝中的AEM。 Maven專 `groupID`案的 `artifactId`、 `version`和屬性會使用您提供給Maven互動式提示的值自動 `name``archetype:generate` 填入。

您可能希望更改生成的pom.xml檔案中的以下預設值：

* CQ伺服器名稱或IP位址：預設值為 `localhost`。 下方 `crx.host` 的元 `project/properties` 素包含此值。

* CQ伺服器的埠號：預設值為 `4502`。 下方 `crx.port` 的元 `project/properties` 素包含此值。

* Content Package Maven Plugin的版本：使用最新版本作為外掛程式 `version` 的元素內容， `artifactId` 包含 `content-package-maven-plugin`。 預設值為 `0.0.24`。

**使用原型**

1. 在shell窗口或命令提示符下，輸入Maven命 `archetype:generate` 令。 出現提示時，請提供其餘參數的值。

   有關每個參數的資訊，請參閱您所用原型的章節。

1. 使用文本編輯器開啟pom.xml檔案，並根據您的要求編輯預設值。
1. 將資源填入產生的檔案夾。
1. 輸入命 `mvn clean install` 令。

### 簡單內容包——原型 {#simple-content-package-archetype}

建立適合為簡單AEM應用程式安裝資源的大型專案。 檔案夾結構是使用在AEM存放庫 `/apps` 檔案夾下方的檔案夾結構。 POM定義了用於封裝您放置在資料夾中的資源以及在AEM實例上安裝包的命令。

**原型藏物屬性：**

* 群組ID: `com.day.jcr.vault`
* 對象ID: `simple-content-package-archetype`
* 版本: `1.0.2`
* 存放庫: `adobe-public-releases`

**Maven命令：**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**原型參數：**

* groupId:Maven所產生的內容套件的groupId。 該值將自動用於POM檔案。
* artifactId:內容套件的名稱。 該值也用作項目資料夾的名稱。
* 版本：內容套件的版本。
* 套件：此值不用於simple-content-package-archetype。
* appsFolderName:/apps下方的資料夾名稱。
* artifactName:內容套件的說明。
* packageGroup:內容套件群組的名稱。 此值會為Content Package Maven Plugin的Package目標設定群組參數。

**資料夾結構：**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                               |- .content.xml
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
                        |- .content.xml
```

### 簡單內容——包含嵌入——原型 {#simple-content-package-with-embedded-archetype}

執行與simple-content-package-archetype相同的任務，還從公共Maven儲存庫下載並包含對象。

**原型包屬性：**

* 群組ID: `com.day.jcr.vault`
* 對象ID: `simple-content-package-with-embedded-archetype`
* 版本: `1.0.2`
* 存放庫: `adobe-public-releases`

**Maven命令：**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-with-embedded-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**原型參數：**

* groupId:Maven所產生的內容套件的groupId。 該值將自動用於POM檔案。
* artifactId:內容套件的名稱。 該值也用作項目資料夾的名稱。
* 版本：內容套件的版本。
* 套件：此參數不被使用。
* appsFolderName:/apps下方的資料夾名稱。
* artifactName:內容套件的說明。
* embeddedArtifactId:要嵌入內容包中的對象的ID。
* embeddedGroupId:要嵌入的對象的組ID。
* 嵌入式版本：要嵌入的對象版本。
* packageGroup:內容套件群組的名稱。 此值會為Content Package Maven Plugin的Package目標設定群組參數。

**資料夾結構：**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
```

### 多模組——內容——包——原型 {#multimodule-content-package-archetype}

建立包含檔案夾結構的大型專案，以開發AEM應用程式並將資源安裝至伺服器。

文 `bundle` 件夾包含儲存您開發的Java和JUnit源檔案的資料夾結構。 此資料夾中的pom.xml檔案將建立OSGi包。 POM中的以下值標識對象和包：

* artifactID: `${artifactID}-bundle`。
* Bundle-SymbolicName: `${groupId}.${artifactId}-bundle`。

`${artifactID}` 和 `${groupId}` 執行原型時為這些參數提供的值。

資 `content` 料夾包含安裝至AEM例項的資源。 artifactID的值為 `${artifactID}multimodule-bundle`。

父資料夾包含管理Maven插件和依賴項的父POM。

**原型包屬性：**

* 群組ID: `com.day.jcr.vault`
* 對象ID: `multimodule-content-package-archetype`
* 版本: `1.0.2`
* 存放庫: `adobe-public-releases`

**Maven命令：**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=multimodule-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**原型參數：**

* groupId:Maven所產生的內容套件的groupId。 該值將自動用於POM檔案。
* artifactId:內容套件的名稱。 該值也用作項目資料夾的名稱。
* 版本：內容套件的版本。
* 套件：此值不用於multimodule-content-package-archetype。
* appsFolderName:/apps下方的資料夾名稱。
* artifactName:內容套件的說明。
* packageGroup:內容套件群組的名稱。 此值會為Content Package Maven Plugin的Package目標設定群組參數。

**資料夾結構：**

```xml
${artifactId}
   |- pom.xml
   |- bundle
      |- pom.xml
      |- src
         |- main
            |- java
               |- ${groupId}
                  |- SimpleDSComponent.java
         |- test
            |- java
               |- ${groupId}
                  |- SimpleUnitTest.java
   |- content
      |- pom.xml
      |- src
         |- main
            |- content
               |- jcr_root
                  |- apps
                     |- ${appsFolderName}
                            |- config
                            |- install
                  |- META-INF
                      |- vault
                         |- config.xml
                         |- filter.xml
                         |- nodetypes.cnd
                         |- properties.xml
                         |- definition
                            |- .content.xml
```

