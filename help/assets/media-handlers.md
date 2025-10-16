---
title: 使用媒體處理常式和工作流程處理資產
description: 瞭解媒體處理常式，以及如何使用工作流程對您的數位資產執行任務。
mini-toc-levels: 1
contentOwner: AG
role: User
feature: Workflow,Renditions
exl-id: cfd6c981-1a35-4327-82d7-cf373d842cc3
solution: Experience Manager, Experience Manager Assets
source-git-commit: f8588ef353bd08b41202350072728d80ee51f565
workflow-type: tm+mt
source-wordcount: '2109'
ht-degree: 3%

---

# 使用媒體處理常式和工作流程處理資產 {#processing-assets-using-media-handlers-and-workflows}

[!DNL Adobe Experience Manager Assets]隨附一組預設工作流程和媒體處理常式，以處理資產。 工作流程會定義要在資產上執行的工作，然後將特定工作委派給媒體處理常式，例如產生縮圖或擷取中繼資料。

您可以將工作流程設定為在上傳特定MIME型別的資產時自動執行。 處理步驟是以[!DNL Assets]個媒體處理常式的系列來定義。 [!DNL Experience Manager]提供一些[內建處理常式](#default-media-handlers)，額外的處理常式可以是[自訂開發的](#creating-a-new-media-handler)，或是透過將處理程式委派給[命令列工具](#command-line-based-media-handler)來定義。

媒體處理常式是[!DNL Assets]中的服務，可對資產執行特定動作。 例如，將MP3音訊檔案上傳至[!DNL Experience Manager]時，工作流程會觸發MP3處理常式，以擷取中繼資料並產生縮圖。 媒體處理常式會與工作流程搭配使用。 [!DNL Experience Manager]支援最常見的MIME型別。 您可以透過擴充或建立工作流程、擴充或建立媒體處理常式，或停用及啟用媒體處理常式，在資產上執行特定工作。

>[!NOTE]
>
>請參閱[支援的資產格式](assets-formats.md)頁面，瞭解[!DNL Assets]支援的所有格式以及每種格式支援的功能。

## 預設媒體處理常式 {#default-media-handlers}

下列媒體處理常式可在[!DNL Assets]中使用，並處理最常見的MIME型別：

<!-- TBD: Java versions should not be set to 1.5. Must be updated.
-->

| 處理常式名稱 | 服務名稱（在系統主控台中） | 支援的MIME型別 |
|--------------|--------------------------------------|----------------------|
| [!UICONTROL 文書處理常式] | com.day.cq.dam.core.impl.handler.TextHandler | text/plain |
| [!UICONTROL PdfHandler] | com.day.cq.dam.handler.standard.pdf.PdfHandler | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | com.day.cq.dam.core.impl.handler.JpegHandler | image/jpeg |
| [!UICONTROL Mp3處理常式] | com.day.cq.dam.handler.standard.mp3.Mp3Handler | audio/mpeg<br><b>重要</b> — 已上傳的MP3檔案[是使用協力廠商程式庫](https://www.zxdr.it/programmi/SistEvolBDD/LibJava/doc/de/vdheide/mp3/MP3File.html)處理。 如果MP3有可變位元速率(VBR)，程式庫會計算不精確的近似長度。 |
| [!UICONTROL ZipHandler] | com.day.cq.dam.handler.standard.zip.ZipHandler | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | com.day.cq.dam.handler.standard.pict.PictHandler | image/pict |
| [!UICONTROL StandardImageHandler] | com.day.cq.dam.core.impl.handler.StandardImageHandler | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler | application/msword |
| [!UICONTROL MSPowerPointHandler] | com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | com.day.cq.dam.handler.standard.epub.EPubHandler | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | com.day.cq.dam.core.impl.handler.GenericAssetHandler | 若找不到其他處理常式可擷取資產中的資料，則進行遞補 |

{style="table-layout:auto"}

所有處理常式都會執行下列工作：

* 從資產擷取所有可用的中繼資料。
* 建立資產的縮圖影像。

若要檢視作用中的媒體處理常式：

1. 在您的瀏覽器中，瀏覽至`https://localhost:4502/system/console/components`。
1. 按一下「`com.day.cq.dam.core.impl.store.AssetStoreImpl`」。
1. 會顯示包含所有使用中媒體處理常式的清單。 例如：

![chlimage_1-437](assets/chlimage_1-437.png)

## 在工作流程中使用媒體處理常式，以執行資產上的工作 {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

媒體處理常式是與工作流程搭配使用的服務。

[!DNL Experience Manager]有一些處理資產的預設工作流程。 若要檢視，請開啟「工作流程」主控台，然後按一下「**[!UICONTROL 模型]**」標籤：以[!DNL Assets]開頭的工作流程標題是資產專屬的工作流程標題。

您可以擴充現有的工作流程，並建立新的工作流程，以根據特定需求處理資產。

下列範例說明如何增強 **[!UICONTROL AEM Assets Synchronization]**  (AEM Assets同步化) 工作流程，以便為除PDF檔案外的所有資產產生子資產。

### 停用或啟用媒體處理常式 {#disabling-enabling-a-media-handler}

您可以透過Apache Felix Web管理主控台停用或啟用媒體處理常式。 停用媒體處理常式時，其工作不會於資產上執行。

若要啟用/停用媒體處理常式：

1. 在您的瀏覽器中，瀏覽至`https://<host>:<port>/system/console/components`。
1. 按一下媒體處理常式名稱旁的&#x200B;**[!UICONTROL 停用]**。 例如：`com.day.cq.dam.handler.standard.mp3.Mp3Handler`。
1. 重新整理頁面：媒體處理常式旁邊會顯示圖示，指出頁面已停用。
1. 若要啟用媒體處理常式，請按一下媒體處理常式名稱旁的&#x200B;**[!UICONTROL 啟用]**。

### 建立媒體處理常式 {#creating-a-new-media-handler}

若要支援新的媒體型別或在資產上執行特定工作，必須建立媒體處理常式。 本節說明如何繼續。

#### 重要類別和介面 {#important-classes-and-interfaces}

開始實作的最佳方式是從提供的抽象實作繼承，該實作會處理大多數事情並提供合理的預設行為： `com.day.cq.dam.core.AbstractAssetHandler`類別。

此類別已經提供抽象服務描述元。 因此，如果您繼承自此類別並使用maven-sling-plugin，請務必將inherit標幟設為`true`。

實作下列方法：

* `extractMetadata()`：擷取所有可用的中繼資料。
* `getThumbnailImage()`：從傳遞的資產建立縮圖影像。
* `getMimeTypes()`：傳回資產MIME型別。

範例範本如下：

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

介面和類別包括：

* `com.day.cq.dam.api.handler.AssetHandler`介面：此介面說明新增特定MIME型別支援的服務。 新增MIME型別需要實作此介面。 介麵包含匯入和匯出特定檔案的方法、建立縮圖和擷取中繼資料的方法。
* `com.day.cq.dam.core.AbstractAssetHandler`類別：此類別可做為所有其他資產處理常式實作的基礎，並提供常用的功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler` 類別：
   * 此類別可做為所有其他資產處理常式實作的基礎，並提供常用功能以及子資產擷取的常用功能。
   * 開始實作的最佳方式是繼承自提供的抽象實作，該實作會處理大多數事情並提供合理的預設行為：com.day.cq.dam.core.AbstractAssetHandler類別。
   * 此類別已經提供抽象服務描述元。 因此，如果您繼承自此類別並使用maven-sling-plugin，請務必將inherit標幟設為true。

必須實作下列方法：

* `extractMetadata()`：此方法會擷取所有可用的中繼資料。
* `getThumbnailImage()`：此方法會從傳遞的資產建立縮圖影像。
* `getMimeTypes()`：此方法會傳回資產MIME型別。

範例範本如下：

封裝my.own.stuff； /&amp;amp；ast；&amp;amp；ast； &amp;amp；@scr.component inherit=&quot;true&quot; &amp;amp；ast； @scr.service &amp;amp；ast；/ public類別MyMediaHandler擴充com.day.cq.dam.core.AbstractAssetHandler { //實作相關部分}

介面和類別包括：

* `com.day.cq.dam.api.handler.AssetHandler`介面：此介面說明新增特定MIME型別支援的服務。 新增MIME型別需要實作此介面。 介麵包含匯入和匯出特定檔案的方法、建立縮圖和擷取中繼資料的方法。
* `com.day.cq.dam.core.AbstractAssetHandler`類別：此類別可做為所有其他資產處理常式實作的基礎，並提供常用的功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler`類別：此類別可做為所有其他資產處理常式實作的基礎，並提供常用功能以及子資產擷取的常用功能。

#### 範例：建立特定的文書處理常式 {#example-create-a-specific-text-handler}

您可以在此段落中建立特定的「文書處理常式」，以產生包含浮水印的縮圖。

請依照下列步驟進行：

請參考[開發工具](../sites-developing/dev-tools.md)以使用[!DNL Maven]外掛程式安裝和設定Eclipse，以及設定[!DNL Maven]專案所需的相依性。

執行以下程式後，當您將TXT檔案上傳到[!DNL Experience Manager]時，會擷取檔案的中繼資料，並產生兩個含有浮水印的縮圖。

1. 在Eclipse中，建立`myBundle` [!DNL Maven]專案：

   1. 在功能表列中，按一下&#x200B;**[!UICONTROL 檔案]** > **[!UICONTROL 新增]** > **[!UICONTROL 其他]**。
   1. 在對話方塊中，展開[!DNL Maven]資料夾，選取[!DNL Maven]專案，然後按一下&#x200B;**[!UICONTROL 下一步]**。
   1. 勾選「建立簡單專案」方塊和「使用預設Workspace位置」方塊，然後按一下「**[!UICONTROL 下一步]**」。
   1. 定義[!DNL Maven]專案：

      * 群組識別碼： `com.day.cq5.myhandler`。
      * 成品ID： myBundle。
      * 名稱：我的[!DNL Experience Manager]套件。
      * 說明：這是我的[!DNL Experience Manager]套件。

   1. 按一下&#x200B;**[!UICONTROL 完成]**。

1. 將[!DNL Java™]編譯器設定為1.5版：

   1. 在`myBundle`專案上按一下滑鼠右鍵，選取[!UICONTROL 屬性]。
   1. 選取[!UICONTROL Java™編譯器]，並將下列屬性設定為1.5：

      * 編譯器相容性層級
      * 產生的.class檔案相容性
      * Source相容性

   1. 按一下&#x200B;**[!UICONTROL 確定]**。 在對話視窗中，按一下&#x200B;**[!UICONTROL 是]**。

1. 將`pom.xml`檔案中的程式碼取代為下列程式碼：

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

1. 在`com.day.cq5.myhandler`下建立包含[!DNL Java™]類別的封裝`myBundle/src/main/java`：

   1. 在myBundle下，用滑鼠右鍵按一下`src/main/java`，選取新增，然後選取封裝。
   1. 將其命名為`com.day.cq5.myhandler`並按一下[完成]。

1. 建立[!DNL Java™]類別`MyHandler`：

   1. 在[!DNL Eclipse]中的`myBundle/src/main/java`下，用滑鼠右鍵按一下`com.day.cq5.myhandler`封裝。 選取[!UICONTROL 新增]，然後選取[!UICONTROL 類別]。
   1. 在對話方塊視窗中，將[!DNL Java™]類別命名為`MyHandler`並按一下[!UICONTROL 完成]。 [!DNL Eclipse]建立並開啟檔案`MyHandler.java`。
   1. 在`MyHandler.java`中，以下列專案取代現有的程式碼，然後儲存變更：

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
     // We need to keep track of the last character, if we have two whitespaces in a row we do not want to double count.
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

1. 編譯[!DNL Java™]類別並建立組合：

   1. 在`myBundle`專案上按一下滑鼠右鍵，選取&#x200B;**[!UICONTROL 執行身分]**，然後選取&#x200B;**[!UICONTROL Maven安裝]**。
   1. 已在`myBundle-0.0.1-SNAPSHOT.jar`下建立套件`myBundle/target` （包含編譯的類別）。

1. 在CRX總管中，在`/apps/myApp`下建立節點。 名稱= `install`，型別= `nt:folder`。
1. 複製組合`myBundle-0.0.1-SNAPSHOT.jar`並將其儲存在`/apps/myApp/install`下（例如，使用WebDAV）。 新文書處理常式現在在[!DNL Experience Manager]中處於使用中狀態。
1. 在瀏覽器中，開啟[!UICONTROL Apache Felix Web管理主控台]。 選取[!UICONTROL 元件]索引標籤並停用預設文書處理常式`com.day.cq.dam.core.impl.handler.TextHandler`。

## 命令列式媒體處理常式 {#command-line-based-media-handler}

[!DNL Experience Manager]可讓您在工作流程中執行任何命令列工具，以轉換資產（例如[!DNL ImageMagick]）並將新轉譯新增至資產。 請在主控[!DNL Experience Manager]伺服器的磁碟上安裝命令列工具，並新增及設定工作流程的程式步驟。 叫用的處理序（稱為`CommandLineProcess`）也會根據特定的MIME型別進行篩選，並根據新的轉譯建立多個縮圖。

下列轉換可自動執行並儲存在[!DNL Assets]中：

* 使用`https://www.imagemagick.org/script/index.php`和[Ghostscript](https://www.ghostscript.com/)的EPS和AI轉換。
* 使用[FFmpeg](https://ffmpeg.org/)的FLV視訊轉碼。
* 使用[LAME](https://lame.sourceforge.io/)的MP3編碼。
* 使用[SOX](https://sourceforge.net/projects/sox/)處理音訊。

>[!NOTE]
>
>在非Windows系統上，針對檔案名稱中包含單引號(&#39;)的視訊資產，FFmpeg工具在產生轉譯時傳回錯誤。 如果您的視訊檔案名稱包含單引號，請先移除該名稱，再上傳至[!DNL Experience Manager]。

`CommandLineProcess`處理序會依照列出的順序執行下列作業：

* 根據特定的MIME型別篩選檔案（如果指定）。
* 在裝載[!DNL Experience Manager]伺服器的磁碟上建立暫存目錄。
* 將原始檔案串流至暫存目錄。
* 執行由步驟的引數定義的命令。 命令正在暫存目錄中執行，且使用者執行[!DNL Experience Manager]的許可權。
* 將結果串流回[!DNL Experience Manager]伺服器的轉譯資料夾。
* 刪除暫存目錄。
* 如果指定，會根據這些轉譯建立縮圖。 縮圖的編號和尺寸由步驟的引數定義。

### 使用[!DNL ImageMagick]的範例 {#an-example-using-imagemagick}

下列範例說明如何設定命令列處理步驟，以便每次將具有miMIME e-type GIF或TIFF的資產新增至`/content/dam`伺服器上的[!DNL Experience Manager]時，都會建立原始檔案的翻轉影像。 另外也會建立三個縮圖140x100、48x48和10x250。

若要這麼做，請使用[!DNL ImageMagick]。 [!DNL ImageMagick]是用來建立、編輯和撰寫點陣圖影像的免費命令列軟體。

在裝載[!DNL ImageMagick]伺服器的磁碟上安裝[!DNL Experience Manager]：

1. 安裝[!DNL ImageMagick]：請參閱`https://www.imagemagick.org/script/download.php`網站。
1. 設定工具，讓您可以在命令列執行`convert`。
1. 若要檢視工具是否已正確安裝，請在命令列上執行下列命令`convert -h`。

   它會顯示說明畫面，其中包含轉換工具的所有可能選項。

   >[!NOTE]
   >
   >在某些Windows版本中，轉換命令可能無法執行，因為它與[!DNL Windows]安裝中的原生轉換公用程式衝突。 在此案例中，請提及用於將影像檔案轉換為縮圖的[!DNL ImageMagick]軟體的完整路徑。 例如，`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`。

1. 若要檢視工具是否正確執行，請將JPG影像新增至工作目錄，並在命令列上執行convert `<image-name>.jpg -flip <image-name>-flipped.jpg`命令。 翻轉的影像會新增至目錄中。 然後，將命令列處理步驟新增至&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程。
1. 移至&#x200B;**[!UICONTROL 工作流程]**&#x200B;主控台。
1. 在&#x200B;**[!UICONTROL 模型]**&#x200B;標籤中，編輯&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;模型。
1. 將[!UICONTROL 啟用Web的轉譯]步驟的&#x200B;**[!UICONTROL 引數]**&#x200B;變更為： `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`。
1. 儲存工作流程。

若要測試修改的工作流程，請新增資產至`/content/dam`。

1. 在檔案系統中，取得您選擇的TIFF影像。 請將它重新命名為`myImage.tiff`，並複製到`/content/dam`，例如，使用WebDAV。
1. 移至&#x200B;**[!UICONTROL CQ5 DAM]**&#x200B;主控台，例如`https://localhost:4502/libs/wcm/core/content/damadmin.html`。
1. 開啟資產&#x200B;**[!UICONTROL myImage.tiff]**，並確認已建立反向影像和三個縮圖。

#### 設定CommandLineProcess程式步驟 {#configuring-the-commandlineprocess-process-step}

本節介紹如何設定 [!UICONTROL CommandLineProcess的Process]&#x200B;[!UICONTROL 參數]。

請使用逗號分隔[!UICONTROL 程式引數]的值，並且不要以空格開頭。

| 引數 — 格式 | 說明 |
|---|---|
| mime：&lt;mime-type> | 選用引數。 如果資產與引數中的MIME型別相同，則會套用程式。 <br>可以定義數個MIME型別。 |
| tn：&lt;寬度>：&lt;高度> | 選用引數。 此程式會使用引數中定義的尺寸建立縮圖。 <br>可以定義數個縮圖。 |
| cmd： &lt;command> | 定義執行的命令。 語法取決於命令列工具。 只能定義一個指令。 <br>下列變數可用來建立命令：<br>`${filename}`：輸入檔案的名稱，例如original.jpg <br> `${file}`：輸入檔案的完整路徑名稱，例如，`/tmp/cqdam0816.tmp/original.jpg` <br> `${directory}`：輸入檔案的目錄，例如，`/tmp/cqdam0816.tmp` <br>`${basename}`：沒有副檔名的輸入檔案名稱，例如，原始的<br>`${extension}`：輸入檔案的副檔名，例如JPG。 |

例如，若在裝載[!DNL ImageMagick]伺服器的磁碟上安裝[!DNL Experience Manager]，且您使用[!UICONTROL CommandLineProcess]做為實作，以及下列值做為[!UICONTROL Process Arguments]來建立處理序步驟：

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

然後，當工作流程執行時，該步驟僅適用於具有`image/gif`或`mime:image/tiff`作為`mime-types`的資產。 它會建立原始影像的翻轉影像、將其轉換為JPG，然後建立三個尺寸分別為140x100、48x48和10x250的縮圖。

使用下列[!UICONTROL 處理程式引數]，使用[!DNL ImageMagick]建立三個標準縮圖：

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

使用下列[!UICONTROL 處理程式引數]來建立啟用Web的轉譯，使用[!DNL ImageMagick]：

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>[!UICONTROL CommandLineProcess]步驟僅適用於資產（型別`dam:Asset`的節點）或資產的子代。

>[!MORELIKETHIS]
>
>* [處理資產](assets-workflow.md)
