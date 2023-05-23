---
title: 使用媒體處理程式和工作流處理資產
description: 瞭解媒體處理程式以及如何使用工作流對數字資產執行任務。
mini-toc-levels: 1
contentOwner: AG
role: User
feature: Workflow,Renditions
exl-id: cfd6c981-1a35-4327-82d7-cf373d842cc3
source-git-commit: acc4b78f551e0e0694f41149fff7e24d855f504f
workflow-type: tm+mt
source-wordcount: '2161'
ht-degree: 3%

---

# 使用媒體處理程式和工作流處理資產 {#processing-assets-using-media-handlers-and-workflows}

[!DNL Adobe Experience Manager Assets] 帶有一組預設工作流和媒體處理程式來處理資產。 工作流定義要在資產上執行的任務，然後將特定任務委派給媒體處理程式，例如縮略圖生成或元資料提取。

可以將工作流配置為在上載特定MIME類型的資產時自動執行。 這些處理步驟根據一系列 [!DNL Assets] 媒體處理程式。 [!DNL Experience Manager] 提供 [內置的處理程式，](#default-media-handlers) 另外的可以 [自定義開發](#creating-a-new-media-handler) 或通過將進程委託給 [命令行工具](#command-line-based-media-handler)。

媒體處理程式是 [!DNL Assets] 對資產執行特定操作。 例如，當MP3音頻檔案上載到 [!DNL Experience Manager]，工作流將觸發提取元資料並生成縮略圖的MP3處理程式。 媒體處理程式通常與工作流結合使用。 在中支援最常見的MIME類型 [!DNL Experience Manager]。 通過擴展/建立工作流、擴展/建立媒體處理程式或禁用/啟用媒體處理程式，可以對資產執行特定任務。

>[!NOTE]
>
>查看 [資產支援的格式](assets-formats.md) 的子目錄 [!DNL Assets] 以及每種格式支援的功能。

## 預設媒體處理程式 {#default-media-handlers}

以下媒體處理程式在 [!DNL Assets] 並處理最常見的MIME類型：

<!-- TBD: Java versions shouldn't be set to 1.5. Must be updated.
-->

| 處理程式名稱 | 服務名稱（在系統控制台中） | 支援的MIME類型 |
|--------------|--------------------------------------|----------------------|
| [!UICONTROL 文本處理程式] | com.day.cq.dam.core.impl.handler.TextHandler | text/plain |
| [!UICONTROL Pdf處理程式] | com.day.cq.dam.handler.standard.pdf.PdfHandler | <ul><li>application/pdf</li><li>應用程式/illustrator</li></ul> |
| [!UICONTROL Jpeg處理程式] | com.day.cq.dam.core.impl.handler.JpegHandler | image/jpeg |
| [!UICONTROL Mp3Handler] | com.day.cq.dam.handler.standard.mp3.Mp3Handler | 音頻/mpeg<br><b>重要</b>  — 上載MP3檔案時， [使用第三方庫處理](https://www.zxdr.it/programmi/SistEvolBDD/LibJava/doc/de/vdheide/mp3/MP3File.html)。 如果MP3具有可變比特率(VBR)，則庫計算非精確的近似長度。 |
| [!UICONTROL Zip處理程式] | com.day.cq.dam.handler.standard.zip.ZipHandler | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL Pict處理程式] | com.day.cq.dam.handler.standard.pict.PictHandler | 影像/圖片 |
| [!UICONTROL 標準影像處理程式] | com.day.cq.dam.core.impl.handler.StandardImageHandler | <ul><li>image/gif </li><li> image/png </li> <li>應用程式/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>影像/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler | application/msword |
| [!UICONTROL MSPowerPointHandler] | com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | com.day.cq.dam.handler.standard.epub.EPubHandler | 應用程式/epub+zip |
| [!UICONTROL 泛型資產處理程式] | com.day.cq.dam.core.impl.handler.GenericAssetHandler | 回退，以防找不到其他處理程式從資產中提取資料 |

{style="table-layout:auto"}

所有處理程式都執行以下任務：

* 從資產中提取所有可用元資料。
* 建立資產的縮略圖。

要查看活動媒體處理程式，請執行以下操作：

1. 在瀏覽器中，導航到 `https://localhost:4502/system/console/components`。
1. 按一下 `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. 將顯示包含所有活動媒體處理程式的清單。 例如：

![chlimage_1-437](assets/chlimage_1-437.png)

## 在工作流中使用媒體處理程式對資產執行任務 {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

媒體處理程式是通常與工作流結合使用的服務。

[!DNL Experience Manager] 具有一些預設工作流來處理資產。 要查看它們，請開啟工作流控制台，然後按一下 **[!UICONTROL 模型]** 頁籤：以開始的工作流標題 [!DNL Assets] 是特定資產。

可以擴展現有工作流，並可以建立新工作流，以根據特定要求處理資產。

下列範例說明如何增強 **[!UICONTROL AEM Assets Synchronization]**  (AEM Assets同步化) 工作流程，以便為除PDF檔案外的所有資產產生子資產。

### 禁用或啟用媒體處理程式 {#disabling-enabling-a-media-handler}

可以通過Apache Felix Web管理控制台禁用或啟用媒體處理程式。 禁用媒體處理程式後，不會對資產執行其任務。

啟用/禁用媒體處理程式：

1. 在瀏覽器中，導航到 `https://<host>:<port>/system/console/components`。
1. 按一下 **[!UICONTROL 禁用]** 媒體處理程式的名稱旁邊。 例如：`com.day.cq.dam.handler.standard.mp3.Mp3Handler`。
1. 刷新頁面：在媒體處理程式旁顯示一個表徵圖，表示它已禁用。
1. 要啟用媒體處理程式，請按一下 **[!UICONTROL 啟用]** 媒體處理程式的名稱旁邊。

### 建立新媒體處理程式 {#creating-a-new-media-handler}

要支援新媒體類型或執行資產上的特定任務，必須建立新媒體處理程式。 本節介紹如何繼續。

#### 重要類和介面 {#important-classes-and-interfaces}

啟動實施的最佳方法是從提供的抽象實施中繼承，該實施會處理大多數事務，並提供合理的預設行為：這樣 `com.day.cq.dam.core.AbstractAssetHandler` 類。

此類已提供抽象服務描述符。 因此，如果從此類繼承並使用maven-sling-plugin，請確保將inherit標誌設定為 `true`。

實現以下方法：

* `extractMetadata()`:提取所有可用元資料。
* `getThumbnailImage()`:從傳遞的資產中建立縮略圖。
* `getMimeTypes()`:返回資產MIME類型。

下面是一個示例模板：

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

介面和類包括：

* `com.day.cq.dam.api.handler.AssetHandler` 介面：此介面描述為特定MIME類型添加支援的服務。 添加新MIME類型需要實現此介面。 該介麵包含用於導入和導出特定文檔、用於建立縮略圖和提取元資料的方法。
* `com.day.cq.dam.core.AbstractAssetHandler` 類：此類用作所有其他資產處理程式實現的基礎，並提供常用功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler` 類別：
   * 此類用作所有其他資產處理程式實現的基礎，並提供常用功能以及用於子資產提取的常用功能。
   * 啟動實施的最佳方法是從提供的抽象實施中繼承，該實施會處理大多數事務，並提供合理的預設行為：com.day.cq.dam.core.AbstractAssetHandler類。
   * 此類已提供抽象服務描述符。 因此，如果從此類繼承並使用maven-sling-plugin，請確保將inherit標誌設定為true。

需要實施以下方法：

* `extractMetadata()`:此方法提取所有可用元資料。
* `getThumbnailImage()`:此方法會從傳遞的資產中建立縮略圖。
* `getMimeTypes()`:此方法返回資產MIME類型。

下面是一個示例模板：

打包my.own.stup;/&amp;ast;&amp;ast;&amp;ast;@scr.component inherit=&quot;true&quot; &amp;ast@scr.service &amp;ast;/公用類MyMediaHandler擴展了com.day.cq.dam.core.AbstractAssetHandler { //實現相關部分}

介面和類包括：

* `com.day.cq.dam.api.handler.AssetHandler` 介面：此介面描述為特定MIME類型添加支援的服務。 添加新MIME類型需要實現此介面。 該介麵包含用於導入和導出特定文檔、用於建立縮略圖和提取元資料的方法。
* `com.day.cq.dam.core.AbstractAssetHandler` 類：此類用作所有其他資產處理程式實現的基礎，並提供常用功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler` 類：此類用作所有其他資產處理程式實現的基礎，並為子集抽取提供常用功能和常用功能。

#### 示例：建立特定文本處理程式 {#example-create-a-specific-text-handler}

在本節中，您將建立一個特定的文本處理程式，該處理程式將生成帶有水印的縮略圖。

按如下方式繼續：

請參閱 [開發工具](../sites-developing/dev-tools.md) 安裝和設定 [!DNL Maven] 插件和用於設定 [!DNL Maven] 項目。

執行以下步驟後，將TXT檔案上載到 [!DNL Experience Manager]，提取檔案的元資料並生成兩個帶水印的縮略圖。

1. 在Eclipse中，建立 `myBundle` [!DNL Maven] 項目：

   1. 在菜單欄中，按一下 **[!UICONTROL 檔案]** > **[!UICONTROL 新建]** > **[!UICONTROL 其他]**。
   1. 在對話框中，展開 [!DNL Maven] 資料夾，選擇 [!DNL Maven] 按一下 **[!UICONTROL 下一個]**。
   1. 選中「建立簡單項目」(Create a simple project)框和「使用預設工作區」(Use default Workspace)位置框，然後按一下 **[!UICONTROL 下一個]**。
   1. 定義 [!DNL Maven] 項目：

      * 組ID: `com.day.cq5.myhandler`。
      * 項目ID:我的捆綁包。
      * 名稱：我的 [!DNL Experience Manager] 捆綁。
      * 描述：這是我的 [!DNL Experience Manager] 捆綁。
   1. 按一下 **[!UICONTROL 完成]**。


1. 設定 [!DNL Java] 編譯到1.5版：

   1. 按一下右鍵 `myBundle` 項目，選擇 [!UICONTROL 屬性]。
   1. 選擇 [!UICONTROL Java編譯器] 並將以下屬性設定為1.5。

      * 編譯器符合性級別
      * 生成的.class檔案相容性
      * 源相容性
   1. 按一下&#x200B;**[!UICONTROL 「確定」]**。在對話框窗口中，按一下 **[!UICONTROL 是]**。


1. 替換 `pom.xml` 檔案，其代碼如下：

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!-- ====================================================================== -->
    <!-- P A R E N T P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <parent>
     <groupId>com.day.cq.dam</groupId>
     <artifactId>dam</artifactId>
     <version>5.2.14</version>
     <relativePath>../parent</relativePath>
    </parent>
    <!-- ====================================================================== -->
    <!-- P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <groupId>com.day.cq5.myhandler</groupId>
    <artifactId>myBundle</artifactId>
    <name>My CQ5 bundle</name>
    <version>0.0.1-SNAPSHOT</version>
    <description>This is my CQ5 bundle</description>
    <packaging>bundle</packaging>
    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
     <plugins>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-scr-plugin</artifactId>
      </plugin>
      <plugin>
       <groupId>org.apache.sling</groupId>
       <artifactId>maven-sling-plugin</artifactId>
       <configuration>
        <slingUrlSuffix>/libs/dam/install/</slingUrlSuffix>
       </configuration>
      </plugin>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-bundle-plugin</artifactId>
       <extensions>true</extensions>
       <configuration>
        <instructions>
         <Bundle-Category>cq5</Bundle-Category>
         <Export-Package> com.day.cq5.myhandler </Export-Package>
        </instructions>
       </configuration>
      </plugin>
     </plugins>
    </build>
    <!-- ====================================================================== -->
    <!-- D E P E N D E N C I E S -->
    <!-- ====================================================================== -->
    <dependencies>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-api</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-core</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq</groupId>
      <artifactId>cq-commons</artifactId>
     </dependency>
     <dependency>
      <groupId>javax.jcr</groupId>
      <artifactId>jcr</artifactId>
     </dependency>
     <dependency>
      <groupId>org.apache.felix</groupId>
      <artifactId>org.osgi.compendium</artifactId>
     </dependency>
     <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-lang</groupId>
      <artifactId>commons-lang</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-gfx</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-text</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.workflow</groupId>
      <artifactId>cq-workflow-api</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.wcm</groupId>
      <artifactId>cq-wcm-foundation</artifactId>
      <version>5.2.22</version>
     </dependency>
    </dependencies>
   ```

1. 建立包 `com.day.cq5.myhandler` 包含 [!DNL Java] 類 `myBundle/src/main/java`:

   1. 在myBundle下，按一下右鍵 `src/main/java`，選擇新建，然後選擇包。
   1. 命名它 `com.day.cq5.myhandler` 然後按一下「完成」。

1. 建立 [!DNL Java] 類 `MyHandler`:

   1. 在 [!DNL Eclipse]下 `myBundle/src/main/java`，按一下右鍵 `com.day.cq5.myhandler` 檔案。 選擇 [!UICONTROL 新建]，則 [!UICONTROL 類]。
   1. 在對話框窗口中，將 [!DNL Java] 類 `MyHandler` 按一下 [!UICONTROL 完成]。 [!DNL Eclipse] 建立並開啟檔案 `MyHandler.java`。
   1. 在 `MyHandler.java` 將現有代碼替換為以下代碼，然後保存更改：

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;
   
   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/
   
   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }
   
    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/we-retail/en/products/apparel/gloves/Gloves.jpg");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two whitespaces in a row we don't want to double count.
     // The starting of the document is always a whitespace.
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a whitespace then we need to add one extra word.
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. 編譯 [!DNL Java] 類並建立包：

   1. 按一下右鍵 `myBundle` 項目，選擇 **[!UICONTROL 運行方式]**，則 **[!UICONTROL Maven安裝]**。
   1. 捆綁 `myBundle-0.0.1-SNAPSHOT.jar` （包含編譯的類） `myBundle/target`。

1. 在CRX資源管理器中，在 `/apps/myApp`。 名稱= `install`，類型= `nt:folder`。
1. 複製捆綁包 `myBundle-0.0.1-SNAPSHOT.jar` 把它放下 `/apps/myApp/install` （例如WebDAV）。 新文本處理程式現在在中處於活動狀態 [!DNL Experience Manager]。
1. 在瀏覽器中，開啟 [!UICONTROL Apache Felix Web管理控制台]。 選擇 [!UICONTROL 元件] 頁籤並禁用預設文本處理程式 `com.day.cq.dam.core.impl.handler.TextHandler`。

## 基於命令行的媒體處理程式 {#command-line-based-media-handler}

[!DNL Experience Manager] 使您能夠在工作流中運行任何命令行工具以轉換資產(例如 [!DNL ImageMagick])，並將新格式副本添加到資產中。 您只需在托管命令的磁碟上安裝命令行工具 [!DNL Experience Manager] 添加和配置工作流的進程步驟。 調用的進程，稱為 `CommandLineProcess`，還可以根據特定MIME類型進行篩選，並基於新格式副本建立多個縮略圖。

以下轉換可自動運行並儲存在 [!DNL Assets]:

* EPS與AI轉化 [影像馬吉克](https://www.imagemagick.org/script/index.php) 和 [重影指令碼](https://www.ghostscript.com/)。
* 使用FLV視頻轉碼 [FFmpeg](https://ffmpeg.org/)。
* MP3編碼 [爛](https://lame.sourceforge.io/)。
* 使用音頻處理 [紅襪隊](https://sox.sourceforge.io/)。

>[!NOTE]
>
>在非Windows系統上，FFmpeg工具在為檔案名中包含單引號(&#39;)的視頻資產生成格式副本時返回錯誤。 如果視頻檔案的名稱包含單引號，請在上載到 [!DNL Experience Manager]。

的 `CommandLineProcess` 進程按列出順序執行以下操作：

* 根據指定的特定MIME類型篩選檔案。
* 在托管的磁碟上建立臨時目錄 [!DNL Experience Manager] 伺服器。
* 將原始檔案流式傳輸到臨時目錄。
* 執行由步驟的參數定義的命令。 該命令正在臨時目錄內執行，用戶的權限正在運行 [!DNL Experience Manager]。
* 將結果流回到的格式副本資料夾中 [!DNL Experience Manager] 伺服器。
* 刪除臨時目錄。
* 根據這些格式副本建立縮略圖（如果指定）。 縮略圖的編號和尺寸由步驟的參數定義。

### 使用 [!DNL ImageMagick] {#an-example-using-imagemagick}

以下示例說明如何設定命令行進程步驟，以便每次將具有miMIME e-typeGIF或TIFF的資產添加到 `/content/dam` 的 [!DNL Experience Manager] 伺服器中，將建立原影像的翻轉影像，同時建立三個附加縮略圖（140x100、48x48和10x250）。

要執行此操作，請使用 [!DNL ImageMagick]。 [!DNL ImageMagick] 是用於建立、編輯和合成點陣圖影像的免費命令行軟體。

安裝 [!DNL ImageMagick] 在承載 [!DNL Experience Manager] 伺服器：

1. 安裝 [!DNL ImageMagick]:請參閱 [ImageMagick文檔](https://www.imagemagick.org/script/download.php)。
1. 設定該工具，以便在命令行上運行「轉換」。
1. 要查看工具是否正確安裝，請運行以下命令 `convert -h` 命令行上。

   它顯示包含轉換工具所有可能選項的幫助螢幕。

   >[!NOTE]
   >
   >在某些Windows版本中，轉換命令可能無法運行，因為它與屬於 [!DNL Windows] 安裝。 在本例中，請提及 [!DNL ImageMagick] 用於將影像檔案轉換為縮略圖的軟體。 比如說， `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`。

1. 要查看工具是否正確運行，請向工作目錄中添加JPG映像並運行命令convert `<image-name>.jpg -flip <image-name>-flipped.jpg` 命令行上。 將翻轉的映像添加到目錄。 然後，將命令行進程步驟添加到 **[!UICONTROL DAM更新資產]** 工作流。
1. 轉到 **[!UICONTROL 工作流]** 控制台。
1. 在 **[!UICONTROL 模型]** 頁籤 **[!UICONTROL DAM更新資產]** 模型。
1. 更改 [!UICONTROL 參數] 的 **[!UICONTROL 啟用Web的格式副本]** 步驟： `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`。
1. 保存工作流。

要test修改的工作流，請將資產添加到 `/content/dam`。

1. 在檔案系統中，獲取您選擇的TIFF影像。 將其更名為 `myImage.tiff` 然後複製到 `/content/dam`，例如使用WebDAV。
1. 轉到 **[!UICONTROL CQ5水壩]** 控制台，例如 `https://localhost:4502/libs/wcm/core/content/damadmin.html`。
1. 開啟資產 **[!UICONTROL myImage.tiff]** 並驗證已建立翻轉的影像和三個縮略圖。

#### 配置CommandLineProcess進程步驟 {#configuring-the-commandlineprocess-process-step}

本節介紹如何設定 [!UICONTROL CommandLineProcess的Process][!UICONTROL 參數]。

分隔 [!UICONTROL 進程參數] 使用逗號，但不要用空格開頭。

| 參數格式 | 說明 |
|---|---|
| mime:&lt;mime-type> | 可選參數。 如果資產的MIME類型與參數之一相同，則應用該進程。 <br>可以定義多種MIME類型。 |
| tn:&lt;width>:&lt;height> | 可選參數。 該過程建立具有參數中定義的尺寸的縮略圖。 <br>可以定義多個縮略圖。 |
| cmd: &lt;command> | 定義執行的命令。 語法取決於命令行工具。 只能定義一個命令。 <br>以下變數可用於建立命令：<br>`${filename}`:輸入檔案的名稱，例如original.jpg <br> `${file}`:輸入檔案的完整路徑名，例如 `/tmp/cqdam0816.tmp/original.jpg` <br> `${directory}`:輸入檔案的目錄，例如 `/tmp/cqdam0816.tmp` <br>`${basename}`:不帶副檔名的輸入檔案的名稱，例如原始 <br>`${extension}`:輸入檔案的副檔名，例如JPG。 |

例如，如果 [!DNL ImageMagick] 安裝在承載 [!DNL Experience Manager] 伺服器，如果您使用 [!UICONTROL 命令行進程] 作為實施，以下值作為 [!UICONTROL 進程參數]:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

然後，當工作流運行時，該步驟僅適用於具有 `image/gif` 或 `mime:image/tiff` 如 `mime-types`，它建立原圖的翻轉影像，將其轉換為JPG，並建立三個具有尺寸的縮略圖：140x100、48x48和10x250。

使用以下 [!UICONTROL 進程參數] 使用 [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

使用以下 [!UICONTROL 進程參數] 使用 [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>的 [!UICONTROL 命令行進程] 步驟僅適用於資產（類型的節點） `dam:Asset`)或資產的後代。

>[!MORELIKETHIS]
>
>* [處理資產](assets-workflow.md)

