---
title: 使用媒體處理常式和工作流程處理資產
description: 瞭解媒體處理常式以及如何使用工作流程對您的數位資產執行工作。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '2108'
ht-degree: 3%

---


# 使用媒體處理常式和工作流程處理資產 {#processing-assets-using-media-handlers-and-workflows}

[!DNL Adobe Experience Manager Assets] 隨附一組預設工作流程和媒體處理常式來處理資產。 工作流程會定義要在資產上執行的工作，然後將特定工作委派給媒體處理常式，例如縮圖產生或中繼資料擷取。

工作流程可設定為在上傳特定MIME類型的資產時自動執行。 這些處理步驟是根據一系列媒體處理常式來 [!DNL Assets] 定義的。 [!DNL Experience Manager] 提供一些 [內置處理程式](#default-media-handlers) ，並可通過將進程委派到命令行工具來自 [定義開發或定](#creating-a-new-media-handler) 義其它處理程式 [](#command-line-based-media-handler)。

媒體處理常式是對資 [!DNL Assets] 產執行特定動作的服務。 例如，當MP3音訊檔案上傳到中時 [!DNL Experience Manager]，工作流程會觸發MP3處理常式，以擷取中繼資料並產生縮圖。 媒體處理常常與工作流程搭配使用。 Most most recompont MIME types are supported within. Comport. Comport. Comport. Comport. Comport. Comport. Comport. Compor. Compop. Comp. Compon. [!DNL Experience Manager]. 特定工作可透過擴充／建立工作流程、擴充／建立媒體處理常式或停用／啟用媒體處理常式，對資產執行。

>[!NOTE]
>
>如需各 [種格式支援之格式](assets-formats.md) ，請參閱「資產支援的格式」頁面，以 [!DNL Assets] 取得各格式支援之功能的說明。

## 預設媒體處理常式 {#default-media-handlers}

下列媒體處理常式可用於 [!DNL Assets] 和處理最常見的MIME類型：

<!-- TBD: Java versions shouldn't be set to 1.5. Must be updated.
-->

| 處理常式名稱 | 服務名（在系統控制台中） | 支援的MIME類型 |
|--------------|--------------------------------------|----------------------|
| [!UICONTROL TextHandler] | `com.day.cq.dam.core.impl.handler.TextHandler` | text/plain |
| [!UICONTROL PdfHandler] | `com.day.cq.dam.handler.standard.pdf.PdfHandler` | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | `com.day.cq.dam.core.impl.handler.JpegHandler` | image/jpeg |
| [!UICONTROL Mp3Handler] | `com.day.cq.dam.handler.standard.mp3.Mp3Handler` | audio/mpeg |
| [!UICONTROL ZipHandler] | `com.day.cq.dam.handler.standard.zip.ZipHandler` | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | `com.day.cq.dam.handler.standard.pict.PictHandler` | image/pict |
| [!UICONTROL StandardImageHandler] | `com.day.cq.dam.core.impl.handler.StandardImageHandler` | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | `com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler` | application/msword |
| [!UICONTROL MSPowerPointHandler] | `com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler` | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | `com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler` | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | `com.day.cq.dam.handler.standard.epub.EPubHandler` | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | `com.day.cq.dam.core.impl.handler.GenericAssetHandler` | 回退，以備找不到其他處理常式來擷取資產的資料 |

所有處理程式都執行下列任務：

* 從資產擷取所有可用的中繼資料。
* 建立資產的縮圖影像。

要查看活動媒體處理程式：

1. 在瀏覽器中，導覽至 `http://localhost:4502/system/console/components`。
1. 按一下 `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. 將顯示包含所有活動媒體處理程式的清單。 例如：

![chlimage_1-437](assets/chlimage_1-437.png)

## 在工作流程中使用媒體處理常式，對資產執行工作 {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

媒體處理常式是通常與工作流程結合使用的服務。

[!DNL Experience Manager] 有一些預設的工作流程來處理資產。 要查看它們，請開啟「工作流」(Workflow)控制台，然後按一下「模 **[!UICONTROL 型」(Models]** )頁籤：以開頭的工作流程標題 [!DNL Assets] 是資產特定的標題。

可擴充現有的工作流程，並建立新的工作流程，以根據特定需求處理資產。

下列範例說明如何增強 **[!UICONTROL AEM Assets Synchronization]**  (AEM Assets同步化) 工作流程，以便為除PDF檔案外的所有資產產生子資產。

### 停用或啟用媒體處理常式 {#disabling-enabling-a-media-handler}

媒體處理常式可以透過Apache Felix Web Management Console停用或啟用。 停用媒體處理常式時，不會對資產執行其工作。

要啟用／禁用媒體處理程式：

1. 在瀏覽器中，導覽至 `https://<host>:<port>/system/console/components`。
1. 按一下 **[!UICONTROL 媒體處理程式名稱旁邊的「禁用]** 」。 For example: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. 重新整理頁面：媒體處理常式旁會顯示圖示，指出其已停用。
1. 若要啟用媒體處理常式，請按一 **[!UICONTROL 下媒體處理常式]** 名稱旁的「啟用」。

### 建立新的媒體處理常式 {#creating-a-new-media-handler}

要支援新介質類型或對資產執行特定任務，必須建立新介質處理程式。 本節說明如何繼續。

#### 重要類別和介面 {#important-classes-and-interfaces}

開始實施的最佳方式是繼承所提供的抽象實施，以處理大部分事物並提供合理的預設行為：班 `com.day.cq.dam.core.AbstractAssetHandler` 級。

此類已提供抽象服務描述符。 因此，如果您繼承此類別並使用maven-sling-plugin，請確定您將inherit標幟設為 `true`。

實施下列方法：

* `extractMetadata()`:擷取所有可用的中繼資料。
* `getThumbnailImage()`:在傳遞的資產中建立縮圖影像。
* `getMimeTypes()`:傳回資產MIME類型。

以下是範例範本：

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

介面和類包括：

* `com.day.cq.dam.api.handler.AssetHandler` 介面：此介面說明新增支援特定MIME類型的服務。 要添加新的MIME類型，必須實施此介面。 介麵包含匯入和匯出特定檔案、建立縮圖和擷取中繼資料的方法。
* `com.day.cq.dam.core.AbstractAssetHandler` 類別：此類別可做為所有其他資產處理常式實作的基礎，並提供常用的功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler` 類別：
   * 此類別可做為所有其他資產處理常式實作的基礎，並提供常用功能以及子資產擷取常用功能。
   * 開始實施的最佳方式是繼承所提供的抽象實施，以處理大部分事物並提供合理的預設行為：com.day.cq.dam.core.AbstractAssetHandler類別。
   * 此類已提供抽象服務描述符。 因此，如果您繼承此類別並使用maven-sling-plugin，請確定您將inherit標幟設為true。

需要實施下列方法：

* `extractMetadata()`:此方法會擷取所有可用的中繼資料。
* `getThumbnailImage()`:此方法會從傳遞的資產中建立縮圖影像。
* `getMimeTypes()`:此方法會傳回資產MIME類型。

以下是範例範本：

封裝my.own.stuff;/&amp;ast;&amp;ast;&amp;ast;@scr.component inherit=&quot;true&quot; &amp;ast;@scr.service &amp;ast;/ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement relevant parts }

介面和類包括：

* `com.day.cq.dam.api.handler.AssetHandler` 介面：此介面說明新增支援特定MIME類型的服務。 要添加新的MIME類型，必須實施此介面。 介麵包含匯入和匯出特定檔案、建立縮圖和擷取中繼資料的方法。
* `com.day.cq.dam.core.AbstractAssetHandler` 類別：此類別可做為所有其他資產處理常式實作的基礎，並提供常用的功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler` 類別：此類別可做為所有其他資產處理常式實作的基礎，並提供常用功能以及子資產擷取的常用功能。

#### 範例：建立特定文字處理常式 {#example-create-a-specific-text-handler}

在本節中，您將建立特定的文字處理常式，以產生含浮水印的縮圖。

按如下步驟進行：

請參閱 [開發工具](../sites-developing/dev-tools.md) ，以安裝並設定包含外掛程式的Eclipse [!DNL Maven] ，以及設定專案所需的相依 [!DNL Maven] 性。

執行以下過程後，將TXT檔案上載到 [!DNL Experience Manager]中時，將提取檔案的元資料並生成兩個帶有水印的縮略圖。

1. 在Eclipse中，建立 `myBundle` 專 [!DNL Maven] 案：

   1. 在功能表列中，按一下「 **[!UICONTROL 檔案]** >新 **[!UICONTROL 增]** >其 **[!UICONTROL 他]**」。
   1. 在對話框中，展開檔案 [!DNL Maven] 夾，選擇 [!DNL Maven] 項目並按一下 **[!UICONTROL 下一步]**。
   1. 選中「建立簡單項目」框和「使用預設工作區位置」框，然後按一下「下 **[!UICONTROL 一步]**」。
   1. 定義專 [!DNL Maven] 案：

      * 群組ID: `com.day.cq5.myhandler`.
      * 對象ID:myBundle。
      * 名稱：我的 [!DNL Experience Manager] 包裹。
      * 說明：這是我的 [!DNL Experience Manager] 包裹。
   1. 按一 **[!UICONTROL 下完成]**。


1. 將編譯 [!DNL Java] 器設定為1.5版：

   1. 按一下右鍵項 `myBundle` 目，選擇 [!UICONTROL 屬性]。
   1. 選擇 [!UICONTROL Java編譯器] ，並將下列屬性設定為1.5:

      * 編譯器合規性級別
      * 生成的。class檔案相容性
      * 原始碼相容性
   1. 按一下&#x200B;**[!UICONTROL 「確定」]**。在對話框窗口中，按一下「 **[!UICONTROL 是」]**。


1. 將檔案中的程式 `pom.xml` 碼取代為下列程式碼：

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

1. 建立包 `com.day.cq5.myhandler` 含以下類 [!DNL Java] 的包 `myBundle/src/main/java`:

   1. 在myBundle下，按一下右鍵， `src/main/java`選擇新建，然後選擇包。
   1. 將其命名 `com.day.cq5.myhandler` 並按一下「完成」。

1. 建立 [!DNL Java] 類 `MyHandler`:

   1. 在 [!DNL Eclipse]的下 `myBundle/src/main/java`面，按一下右鍵包 `com.day.cq5.myhandler` 。 依次選擇 [!UICONTROL 新建]、 [!UICONTROL 類]。
   1. 在對話框窗口中，為類命 [!DNL Java] 名並 `MyHandler` 按一下 [!UICONTROL Finish]。 [!DNL Eclipse] 建立並開啟檔案 `MyHandler.java`。
   1. 在以 `MyHandler.java` 下方式取代現有程式碼，然後儲存變更：

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
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/geometrixx/icons/certificate.png");
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

1. 編譯類 [!DNL Java] 並建立包：

   1. 按一下右鍵項 `myBundle` 目，選 **[!UICONTROL 擇Run As]**, Maven Install ****。
   1. 在下 `myBundle-0.0.1-SNAPSHOT.jar` 建立包（包含編譯類） `myBundle/target`。

1. 在CRX檔案總管中，在下方建立新節點 `/apps/myApp`。 名稱= `install`，類型= `nt:folder`。
1. 複製套件 `myBundle-0.0.1-SNAPSHOT.jar` 並將它儲存 `/apps/myApp/install` 在下方（例如WebDAV）。 新的文字處理常式現在在中處於作用中 [!DNL Experience Manager]。
1. 在您的瀏覽器中，開啟 [!UICONTROL Apache Felix Web Management Console]。 選取「元 [!UICONTROL 件] 」標籤，並停用預設文字處理常式 `com.day.cq.dam.core.impl.handler.TextHandler`。

## 基於命令行的媒體處理程式 {#command-line-based-media-handler}

[!DNL Experience Manager] 可讓您在工作流程中執行任何命令列工具，以轉換資產( [!DNL ImageMagick]例如)，並將新的轉譯新增至資產。 您只需要在托管伺服器的磁碟上安裝命令行工具， [!DNL Experience Manager] 並向工作流中添加和配置流程步驟。 調用的程式( `CommandLineProcess`稱為)也可以根據特定MIME類型進行篩選，並根據新轉譯建立多個縮圖。

下列轉換可自動執行並儲存在 [!DNL Assets]:

* 使用ImageMagick和 [Ghostscript進行EPS](https://www.imagemagick.org/script/index.php)[和AI轉換](https://www.ghostscript.com/)。
* 使用FFmpeg進行FLV視 [訊轉碼](https://ffmpeg.org/)。
* 使用 [LAME進行MP3編碼](http://lame.sourceforge.net/)。
* 使用 [SOX處理音訊](http://sox.sourceforge.net/)。

>[!NOTE]
>
>在非Windows系統上，FFmpeg工具會傳回錯誤，因為其檔案名稱中包含單引號(&#39;)的視訊資產會產生轉譯。 如果視訊檔案的名稱包含單引號，請先將其移除，然後再上傳至 [!DNL Experience Manager]。

該 `CommandLineProcess` 進程按列出順序執行以下操作：

* 根據特定MIME類型（如果已指定）篩選檔案。
* 在托管伺服器的磁碟上建立臨時 [!DNL Experience Manager] 目錄。
* 將原始檔案流到臨時目錄。
* 執行由步驟的參數定義的命令。 該命令正在臨時目錄內執行，並具有用戶的運行權限 [!DNL Experience Manager]。
* 將結果串流回伺服器的轉譯資 [!DNL Experience Manager] 料夾。
* 刪除臨時目錄。
* 根據這些轉譯（如果已指定）建立縮圖。 縮圖的編號和尺寸由步驟的參數定義。

### 使用 [!DNL ImageMagick] {#an-example-using-imagemagick}

以下示例說明如何設定命令行處理步驟，以便每次在伺服器上將具有miMIME e-type GIF或TIFF的資產添加到伺服器時，都會建立原始影像的翻轉影像，並同時建立另外三個縮略圖（140x100、48x48和10x250）。 `/content/dam`[!DNL Experience Manager]

若要這麼做，請使用 [!DNL ImageMagick]。 [!DNL ImageMagick] 是免費的命令列軟體，用來建立、編輯和合成點陣圖影像。

安裝 [!DNL ImageMagick] 在托管伺服器的磁 [!DNL Experience Manager] 盤上：

1. 安裝 [!DNL ImageMagick]:請參 [閱ImageMagick檔案](https://www.imagemagick.org/script/download.php)。
1. 設定工具，以便在命令行上運行轉換。
1. 要查看工具是否已正確安裝，請在命令行上運 `convert -h` 行以下命令。

   它會顯示說明畫面，內含轉換工具的所有可能選項。

   >[!NOTE]
   >
   >在某些Windows版本中，轉換命令可能無法運行，因為它與作為安裝一部分的本地轉換實用程式 [!DNL Windows] 衝突。 在此例中，請提及將影像檔案轉換為縮圖 [!DNL ImageMagick] 所用軟體的完整路徑。 For example, `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. 若要查看工具是否正常運行，請將JPG影像添加到工作目錄並在命令行上運行 `<image-name>.jpg -flip <image-name>-flipped.jpg` 命令convert。 翻轉的影像會新增至目錄。 Then, add the command line process step to the **[!UICONTROL DAM Update Asset]** workflow.
1. 前往「工作 **[!UICONTROL 流程]** 」主控台。
1. 在「模 **[!UICONTROL 型]** 」標籤中，編 **[!UICONTROL 輯「DAM更新資產模型]** 」。
1. 將啟用 [!UICONTROL Web] 的轉譯步 **[!UICONTROL 驟的「參數]** 」更改為： `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`.
1. 儲存工作流程。

若要測試修改後的工作流程，請新增資產至 `/content/dam`。

1. 在檔案系統中，取得您選擇的TIFF影像。 例如， `myImage.tiff` 使用WebDAV將其重 `/content/dam`新命名並複製至。
1. 例如， **[!UICONTROL 前往CQ5 DAM]** Console `http://localhost:4502/libs/wcm/core/content/damadmin.html`。
1. 開啟資產 **[!UICONTROL myImage.tiff]** ，並確認已建立翻轉的影像和三個縮圖。

#### 配置CommandLineProcess進程步驟 {#configuring-the-commandlineprocess-process-step}

本節介紹如何設定 [!UICONTROL CommandLineProcess的Process][!UICONTROL 參數]。

使用逗號分隔 [!UICONTROL 「進程參數] 」的值，不要以空格開頭。

| 參數格式 | 說明 |
|---|---|
| mime:&lt;mime-type> | 可選引數。 如果資產與其中一個引數的MIME類型相同，則會套用此程式。 <br>可定義數種MIME類型。 |
| tn:&lt;width>:&lt;height> | 可選引數。 該過程建立具有在參數中定義的尺寸的縮略圖。 <br>可定義數個縮圖。 |
| cmd:&lt;command> | 定義所執行的命令。 語法取決於命令行工具。 只能定義一個命令。 <br>以下變數可用來建立命令：<br>`${filename}`:輸入檔案的名稱，例如original.jpg <br> `${file}`:輸入檔案的完整路徑名稱，例如 `/tmp/cqdam0816.tmp/original.jpg` <br> `${directory}`:目錄，例如 `/tmp/cqdam0816.tmp`<br>`${basename}`:輸入檔案的名稱（不帶副檔名），例如原始檔案 <br>`${extension}`:輸入檔案的副檔名，例如JPG。 |

例如，如果 [!DNL ImageMagick] 安裝在托管伺服器的磁碟上，並且 [!DNL Experience Manager] 使用 [!UICONTROL CommandLineProcess] as Implementation和以下值作為Process Arguments建立進程步驟 :

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

然後，當工作流程執行時，此步驟僅會套用至具有或作為 `image/gif``mime:image/tiff``mime-types`，它會建立原始影像的翻轉影像，並將其轉換為JPG，並建立三個尺寸縮圖：140x100、48x48和10x250。

使用下列 [!UICONTROL Process Arguments] （進程參數）建立三個標準縮圖 [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

使用下列 [!UICONTROL 「處理參數] 」建立啟用Web的轉譯，使用 [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>CommandLineProcess [!UICONTROL 步驟僅適用於資產(類型的節]`dam:Asset`點)或資產的後代。

>[!MORELIKETHIS]
>
>* [處理資產](assets-workflow.md)

