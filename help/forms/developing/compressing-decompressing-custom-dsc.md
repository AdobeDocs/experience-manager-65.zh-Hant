---
title: 如何使用WS-security標頭傳遞憑據？
description: 了解如何使用WS-security標頭傳遞憑證
exl-id: 1b950d8f-6b54-452a-831b-f5644370691d
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# 在JEE自訂DSC上使用AEM Forms來壓縮和解壓縮檔案 {#compressing-decompressing-files}

## 必備知識 {#prerequisites}

在JEE流程管理、基本Java程式設計和建立自訂元件方面的AEM Forms經驗。

**其他所需產品**

Java編輯器，例如 [Eclipse](https://www.eclipse.org/) 或 [Netbeans IDE](https://netbeans.apache.org/)

## 使用者層級 {#user-level}

中間

AEM Forms on JEE可讓開發人員建立自訂DSC（檔案服務容器），以建立現成可用的功能。 建立這類元件可插入至JEE執行階段環境上的AEM Forms，並符合預期用途。 本文說明如何建立自訂ZIP服務，此服務可用來將檔案清單壓縮為.zip檔案，並將.zip解壓縮為檔案清單。

## 建立自訂DSC元件 {#create-custom-dsc-component}

建立自訂DSC元件，並執行兩個服務操作來壓縮及解壓縮檔案清單。 此元件使用java.util.zip套件進行壓縮和解壓縮。 請依照下列步驟建立自訂元件：

1. 將adobe-livecycle-client.jar檔案新增至程式庫
1. 新增所需的圖示
1. 建立公用類
1. 建立兩個名為UnzipDocument和ZipDocuments的公用方法
1. 編寫用於壓縮和解壓縮的邏輯

您可以在下列位置找到程式碼：

```java
/*
 * Custom DSC : ZIP Utility
 * Purpose: This is a LiveCycle ES2 custom component used to Compress & Decompress List of Documents
 * Author: Nithiyanandam Dharmadass
 * Organization: Ministry of Finance, Kingdom of Bahrain
 * Last modified Date: 18/Apr/2011
 */
package nith.lces2.dsc;

import java.util.zip.ZipEntry;
import java.util.zip.ZipInputStream;
import com.adobe.idp.Document;
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.List;
import java.util.zip.ZipOutputStream;

public class ZIPService {

    static final int BUFFER = 2048; // 2MB buffer size

    public java.util.List UnzipDocument(com.adobe.idp.Document zipDocument) throws Exception {
        ZipInputStream zis = new ZipInputStream(zipDocument.getInputStream());

        ZipEntry zipFile;

        List resultList = new ArrayList();

        while ((zipFile = zis.getNextEntry()) != null) {

            ByteArrayOutputStream byteArrayOutStream = new ByteArrayOutputStream();

            int count;  // an int variable to hold the number of bytes read from input stream
            byte data[] = new byte[BUFFER];
            while ((count = zis.read(data, 0, BUFFER)) != -1) {
                byteArrayOutStream.write(data, 0, count);   // write to byte array
            }

            com.adobe.idp.Document unzippedDoc = new Document(byteArrayOutStream.toByteArray());  // create an idp document
            unzippedDoc.setAttribute("file", zipFile.getName());
            unzippedDoc.setAttribute("wsfilename", zipFile.getName());  // update the wsfilename attribute
            resultList.add(unzippedDoc);
        }
        return resultList;  // List of uncompressed documents
    }

    public com.adobe.idp.Document ZipDocuments(java.util.List listOfDocuments,java.lang.String zipFileName) throws Exception {

        if (listOfDocuments == null || listOfDocuments.size() == 0) {
            return null;
        }

        ByteArrayOutputStream byteArrayOutStream = new ByteArrayOutputStream();
        ZipOutputStream zos = new ZipOutputStream(byteArrayOutStream);  // ZIP Output Stream

        for (int i = 0; i < listOfDocuments.size(); i++) {
            Document doc = (Document) listOfDocuments.get(i);
            InputStream docInputStream = doc.getInputStream();
            ZipEntry zipEntry = new ZipEntry(doc.getAttribute("file").toString());
            zos.putNextEntry(zipEntry);
            int count;
            byte data[] = new byte[BUFFER];
            while ((count = docInputStream.read(data, 0, BUFFER)) != -1) {
                zos.write(data, 0, count);  // Read document content and add to zip entry
            }
            zos.closeEntry();
        }
        zos.flush();
        zos.close();

        Document zippedDoc = new Document(byteArrayOutStream.toByteArray());
        if(zipFileName==null || zipFileName.equals(""))
        {
            zipFileName = "CompressedList.zip";
        }
        zippedDoc.setAttribute("file", zipFileName);
        return zippedDoc;
    }
}
```

## 建立Component.XML檔案 {#create-component-xml-file}

必須在定義服務操作及其參數的包的根資料夾內建立component.xml檔案。

元件.xml檔案如下所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<component xmlns="https://adobe.com/idp/dsc/component/document">
<!-- Unique id identifying this component -->
   <component-id>ZipService</component-id>

<!-- Version -->
   <version>1.0</version>

<!-- Start of the Service definition -->
   <services>
<!-- Unique name for service descriptor.
           The value is used as the default name for
           deployed services -->
      <service name="ZipService">
<!-- service implementation class definition -->
        <implementation-class>nith.lces2.dsc.ZIPService</implementation-class>

<!-- description -->
        <description>Compress or Decompress list of documents</description>

<!--  You can provide your own icons for a distinct look   -->
          <small-icon>icons/Zip_icon16.png</small-icon>
          <large-icon>icons/Zip_icon32.png</large-icon>


<!-- automatically deploys the service and starts it after installation -->
         <auto-deploy service-id="ZipService" />

         <operations>
<!-- method name in the interface setSmtpHost-->
            <operation name="UnzipDocument">
<!-- input parameters to the "send" method -->
              <input-parameter name="zipDocument" title="Input ZIP Document" type="com.adobe.idp.Document">
                    <hint>A ZIP File to be decompressed</hint>
                </input-parameter>
                <output-parameter name="resultList" title="Decompressed list of documents" type="java.util.List">
                    <hint>Decompressed ZIP list</hint>
                </output-parameter>
            </operation>
            <operation name="ZipDocuments">
<!-- input parameters to the "send" method -->
              <input-parameter name="listOfDocuments" title="List of Documents" type="java.util.List">
                    <hint>A list of documents to be Compressed</hint>
                </input-parameter>
                <input-parameter name="zipFileName" title="Result File Name" type="java.lang.String">
                    <hint>The name of compressed file (optional)</hint>
                </input-parameter>

                <output-parameter name="zippedDoc" title="Compressed Zip file" type="com.adobe.idp.Document">
                    <hint>Compressed ZIP File</hint>
                </output-parameter>
            </operation>
             </operations>
      </service>
   </services>
</component>
```

## 封裝和部署元件 {#packaging-deploying-component}

1. 編譯java項目並建立.JAR檔案。
1. 透過Workbench，在JEE執行階段將元件（.JAR檔案）部署至AEM Forms。
1. 從Workbench啟動服務（請參閱下圖）。

![流程設計](assets/process-design.jpg)

## 在工作流程中使用ZIP服務 {#using-zip-service-in-workflows}

自訂服務的UnzipDocument操作現在可以接受檔案變數作為輸入，並傳回檔案變數清單作為輸出。

![解壓縮檔案](assets/unzip-doc.jpg)

同樣地，自訂元件的ZipDocuments操作也可以接受檔案清單作為輸入，將其壓縮為zip檔案，然後傳回壓縮的檔案。

![郵遞區號檔案](assets/zip-doc.jpg)

以下工作流程協調將顯示如何解壓縮給定的ZIP檔案，將其壓縮回另一個ZIP檔案，並返回輸出（請參見下圖）。

![解壓縮郵遞區號工作流程](assets/unzip-zip-process.jpg)

## 某些業務使用案例 {#business-use-cases}

您可以將此ZIP服務用於下列使用案例：

* 查找指定資料夾中的所有檔案，並以壓縮文檔形式返回這些檔案。

* 提供包含許多PDF文檔的ZIP檔案，這些文檔在解壓縮後可以被讀取器擴展。 這需要JEE上的AEM FormsReader擴充功能模組。

* 提供包含異構類型的文檔的ZIP檔案，這些文檔可以使用「生成PDF」服務被解壓縮並轉換為PDF文檔。

* 原則會保護檔案清單，並以ZIP檔案傳回。

* 允許使用者以單一ZIP檔案的形式下載處理程式例項的所有附件。
