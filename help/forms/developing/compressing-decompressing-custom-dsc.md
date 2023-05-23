---
title: 在JEE自定義DSC上使用AEM Forms壓縮和解壓縮檔案
description: 瞭解如何在JEE自定義DSC上使用AEM Forms壓縮和解壓縮檔案
exl-id: 1b950d8f-6b54-452a-831b-f5644370691d
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# 在JEE自定義DSC上使用AEM Forms壓縮和解壓縮檔案 {#compressing-decompressing-files}

## 先決知識 {#prerequisites}

AEM Forms在JEE流程管理、基本Java寫程式和建立自定義元件方面的經驗。

**其他所需的其他產品**

Java編輯器，如 [日蝕](https://www.eclipse.org/) 或 [NetBeans IDE](https://netbeans.apache.org/)

## 用戶級別 {#user-level}

中間

AEM FormsJEE使開發人員能夠建立自定義DSC（文檔服務容器），以便從包裝盒功能中建立豐富的功能。 建立這些元件可以在JEE運行時環境上插入AEM Forms，並滿足預期目的。 本文介紹如何建立自定義ZIP服務，該服務可用於將檔案清單壓縮到.zip檔案中，並將.zip解壓縮到文檔清單。

## 建立自定義DSC元件 {#create-custom-dsc-component}

建立具有兩個服務操作的自定義DSC元件以壓縮和解壓縮文檔清單。 此元件使用java.util.zip包進行壓縮和解壓縮。 按照以下步驟建立自定義元件：

1. 將adobe-liveccycle-client.jar檔案添加到庫
1. 添加所需的表徵圖
1. 建立公共類
1. 建立兩個名為UnzipDocument和ZipDocuments的公用方法
1. 編寫用於壓縮和解壓縮的邏輯

代碼可在以下位置找到：

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

必須在定義服務操作及其參數的包的根資料夾中建立component.xml檔案。

component.xml檔案如下所示：

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

## 打包和部署元件 {#packaging-deploying-component}

1. 編譯java項目並建立.JAR檔案。
1. 通過Workbench將元件（.JAR檔案）部署到JEE運行時的AEM Forms。
1. 從Workbench啟動服務（請參閱下圖）。

![流程設計](assets/process-design.jpg)

## 在工作流中使用ZIP服務 {#using-zip-service-in-workflows}

自定義服務的UnzipDocument操作現在可以接受文檔變數作為輸入，並返回文檔變數清單作為輸出。

![解壓縮文檔](assets/unzip-doc.jpg)

同樣，自定義元件的ZipDocuments操作可以接受文檔清單作為輸入，將其壓縮為壓縮檔案並返回壓縮文檔。

![Zip文檔](assets/zip-doc.jpg)

以下工作流業務流程說明了如何解壓縮給定的ZIP檔案，將其壓縮回另一個ZIP檔案，並返回輸出（請參見下圖）。

![解壓縮Zip工作流](assets/unzip-zip-process.jpg)

## 某些業務使用案例 {#business-use-cases}

您可以將此ZIP服務用於以下使用案例：

* 查找給定資料夾中的所有檔案，並將檔案作為壓縮文檔返回。

* 提供包含多個PDF文檔的ZIP檔案，這些文檔在解壓縮後可以進行讀取擴展。 這需要AEM Forms的JEEReader擴展模組。

* 提供包含異構類型的文檔的ZIP檔案，這些文檔可以使用「生成PDF」服務解壓縮並轉換為PDF文檔。

* 策略保護文檔清單並作為ZIP檔案返回。

* 允許用戶將進程實例的所有附件作為單個ZIP檔案下載。
