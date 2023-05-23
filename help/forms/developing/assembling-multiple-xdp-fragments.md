---
title: 組裝多個XDP片段
seo-title: Assembling Multiple XDP Fragments
description: 使用Java API和Web服務API將多個XDP片段裝配到單個XDP文檔中。
seo-description: Assemble multiple XDP fragments into a single XDP document using the Java API and Web Service API.
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
role: Developer
exl-id: 54d98c69-2b2e-46cb-9f6a-7e9bdbe5c378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 0%

---

# 組裝多個XDP片段{#assembling-multiple-xdp-fragments}

可將多個XDP片段裝配到單個XDP文檔中。 例如，請考慮XDP片段，其中每個XDP檔案包含一個或多個用於建立健康表單的子表單。 下圖顯示了大綱視圖(表示在中使用的tuc018_template_flud.xdp檔案 *組裝多個XDP片段* 快速啟動):

![am_am_forma](assets/am_am_forma.png)

下圖顯示了患者節(表示在 *組裝多個XDP片段* 快速啟動):

![am_am_formb](assets/am_am_formb.png)

下圖顯示了患者健康部分(表示中使用的tuc018_patient.xdp檔案 *組裝多個XDP片段* 快速啟動):

![am_am_formc](assets/am_am_formc.png)

此片段包含名為 *subPatientPhysical* 和 *子患者健康*。 這兩個子表單都在傳遞給匯編器服務的DDX文檔中引用。 使用匯編器服務，可以將所有這些XDP片段組合為單個XDP文檔，如下圖所示。

![am_am_formd](assets/am_am_formd.png)

以下DDX文檔將多個XDP片段組合到XDP文檔中。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <XDP result="tuc018result.xdp">
            <XDP source="tuc018_template_flowed.xdp">
             <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
            </XDP>
         </XDP>
 </DDX>
```

DDX文檔包含XDP `result` 指定結果名稱的標籤。 在這種情況下，價值是 `tuc018result.xdp`。 在匯編程式服務返回結果後用於檢索XDP文檔的應用程式邏輯中引用此值。 例如，請考慮以下用於檢索已裝配的XDP文檔的Java應用程式邏輯（請注意，值是粗體）:

```java
 //Iterate through the map object to retrieve the result XDP document
 for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
     // Retrieve the Map object’s value
     Map.Entry e = (Map.Entry)i.next();
     //Get the key name as specified in the
     //DDX document
     String keyName = (String)e.getKey();
     if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                 {
         Object o = e.getValue();
         outDoc = (Document)o;
         //Save the result PDF file
         File myOutFile = new File("C:\\AssemblerResultXDP.xdp");
         outDoc.copyToFile(myOutFile);
     }
 }
```

的 `XDP source` tag指定表示完整XDP文檔的XDP檔案，該文檔可用作添加XDP片段的容器，或作為按順序追加在一起的多個文檔之一。 在這種情況下，XDP文檔僅用作容器（如中所示的第一個圖示） *組裝多個XDP片段*)。 即，其他XDP檔案被放在XDP容器中。

對於每個子窗體，可以 `XDPContent` 元素（此元素是可選的）。 在上例中，請注意有三個子表單： `subPatientContact`。 `subPatientPhysical`, `subPatientHealth`。 都 `subPatientPhysical` 子窗體和 `subPatientHealth` 子窗體位於同一XDP檔案tuc018_patient.xdp中。 片段元素指定子窗體的名稱，如Designer中所定義。

>[!NOTE]
>
>有關匯編器服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [匯編程式服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

要裝配多個XDP片段，請執行以下任務：

1. 包括項目檔案。
1. 建立PDF匯編器客戶端。
1. 引用現有DDX文檔。
1. 引用XDP文檔。
1. 設定運行時選項。
1. 組合多個XDP文檔。
1. 檢索已裝配的XDP文檔。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

**建立PDF匯編器客戶端**

在以寫程式方式執行匯編器操作之前，請建立匯編器服務客戶端。

**引用現有DDX文檔**

必須引用DDX文檔來匯編多個XDP文檔。 此DDX文檔必須包含 `XDP result`。 `XDP source`, `XDPContent` 元素。

**引用XDP文檔**

要匯編多個XDP文檔，請參考用於匯編結果XDP文檔的所有XDP檔案。 確保XDP文檔中包含的由 `source` 屬性在 `fragment` 屬性。 子窗體在設計器中定義。 例如，請考慮以下XML。

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

名為的子窗體 *subPatientContact* 必須位於名為 *tuc018_contact.xdp*。

**設定運行時選項**

您可以設定運行時選項，這些選項在匯編程式服務執行作業時控制其行為。 例如，您可以設定一個選項，指示匯編程式服務在遇到錯誤時繼續處理作業。

**匯編多個XDP文檔**

要裝配多個XDP檔案，請調用 `invokeDDX` 的下界。 匯編器服務返回集合對象中已裝配的XDP文檔。

**檢索已裝配的XDP文檔**

集合對象內返回已裝配的XDP文檔。 循環訪問集合對象並將XDP文檔另存為XDP檔案。 您還可以將XDP文檔傳遞給其他AEM Forms服務，如輸出。

**另請參閱**

[使用Java API裝配多個XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[使用Web服務API裝配多個XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式裝配PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[使用片段建立PDF文檔](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## 使用Java API裝配多個XDP片段 {#assemble-multiple-xdp-fragments-using-the-java-api}

使用匯編器服務API(Java)匯編多個XDP片段：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF匯編器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `AssemblerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用現有DDX文檔。

   * 建立 `java.io.FileInputStream` 表示DDX文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定DDX檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 引用XDP文檔。

   * 建立 `java.util.Map` 用於使用 `HashMap` 建構子。
   * 建立 `com.adobe.idp.Document` 並傳遞 `java.io.FileInputStream` 包含輸入XDP檔案的對象（對每個XDP檔案重複此任務）。
   * 向 `java.util.Map` 通過調用對象 `put` 方法並傳遞以下參數：

      * 表示鍵名稱的字串值。 此值必須與 `source` 在DDX文檔中指定的元素值（對每個XDP檔案重複此任務）。
      * A `com.adobe.idp.Document` 包含與 `source` 元素（對每個XDP檔案重複此任務）。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過調用屬於的方法來設定運行時選項以滿足業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編器服務在發生錯誤時繼續處理作業，請調用 `AssemblerOptionSpec` 對象 `setFailOnError` 方法 `false`。

1. 組合多個XDP文檔。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下所需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文檔的對象
   * A `java.util.Map` 包含輸入XDP檔案的對象
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項的對象，包括預設字型和作業日誌級別

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含已裝配的XDP文檔的對象。

1. 檢索已裝配的XDP文檔。

   要獲取已裝配的XDP文檔，請執行以下操作：

   * 調用 `AssemblerResult` 對象 `getDocuments` 的雙曲餘切值。 此方法返回 `java.util.Map` 的雙曲餘切值。
   * 迭代 `java.util.Map` 直到找到結果 `com.adobe.idp.Document` 的雙曲餘切值。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 提取XDP文檔的方法。

**另請參閱**

[組裝多個XDP片段](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[快速啟動（SOAP模式）:使用Java API組裝多個XDP片段](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API裝配多個XDP片段 {#assemble-multiple-xdp-fragments-using-the-web-service-api}

使用匯編器服務API（Web服務）匯編多個XDP片段：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 請確保在設定服務引用時使用以下WSDL定義：

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立PDF匯編器客戶端。

   * 建立 `AssemblerServiceClient` 對象。
   * 建立 `AssemblerServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務，如 `https://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `AssemblerServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給 `AssemblerServiceClient.ClientCredentials.UserName.UserName` 的子菜單。
      * 將相應的密碼值分配給 `AssemblerServiceClient.ClientCredentials.UserName.Password`的子菜單。
      * 分配 `HttpClientCredentialType.Basic` 常數值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`的子菜單。
      * 分配 `BasicHttpSecurityMode.TransportCredentialOnly` 常數值 `BasicHttpBindingSecurity.Security.Mode`的子菜單。

1. 引用現有DDX文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存DDX文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示DDX文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞位元組陣列、起始位置和流長度以進行讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。

1. 引用XDP文檔。

   * 對於每個輸入XDP檔案，建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存輸入檔案。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示輸入檔案的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞位元組陣列、起始位置和流長度以進行讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 此集合對象用於儲存建立已裝配的XDP文檔所需的輸入檔案。
   * 對於每個輸入檔案，建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的雙曲餘切值。
   * 為指定表示鍵名的字串值 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `key` 的子菜單。 此值必須與DDX文檔中指定的元素的值匹配。 （對每個輸入XDP檔案執行此任務。）
   * 分配 `BLOB` 將輸入檔案儲存到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `value` 的子菜單。 （對每個輸入XDP檔案執行此任務。）
   * 添加 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 調用 `MyMapOf_xsd_string_To_xsd_anyType` 對象 `Add` 方法和通過 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 （對每個輸入的XDP文檔執行此任務。）

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過將值分配給屬於的資料成員來設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編程式服務在發生錯誤時繼續處理作業，請分配 `false` 到 `AssemblerOptionSpec` 對象 `failOnError` 資料成員。

1. 組合多個XDP文檔。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下值：

   * A `BLOB` 表示DDX文檔的對象
   * 的 `MyMapOf_xsd_string_To_xsd_anyType` 包含所需檔案的對象
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含作業結果和所發生的任何異常的對象。

1. 檢索已裝配的XDP文檔。

   要獲取新建立的XDP文檔，請執行以下操作：

   * 訪問 `AssemblerResult` 對象 `documents` 欄位， `Map` 包含結果PDF文檔的對象。
   * 迭代 `Map` 對象，以獲取每個結果文檔。 然後，將該陣列成員 `value` 到 `BLOB`。
   * 通過訪問PDF文檔來提取表示該文檔的二進位資料 `BLOB` 對象 `MTOM` 屬性。 這將返回可以寫入XDP檔案的位元組陣列。

**另請參閱**

[組裝多個XDP片段](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
