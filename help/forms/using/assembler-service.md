---
title: 使用組合器服務
seo-title: Using Assembler Service
description: 組合器服務允許您組合、重新排列和擴展PDF和XDP文檔，並獲取有關PDF文檔的資訊。
seo-description: The Assembler service lets you combine, rearrange, and augment PDF and XDP documents and obtain information about PDF documents.
uuid: 1efce50b-2d98-408e-aa43-ac4999de41a8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 6a99042f-79c7-494b-bca0-73f2b5725b58
docset: aem65
exl-id: 2acd6b19-0fe8-4994-b0f4-c9d5b9f3fdf1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2121'
ht-degree: 0%

---

# 使用組合器服務{#using-assembler-service}

組合器服務允許您組合、重新排列和擴展PDF和XDP文檔，並獲取有關PDF文檔的資訊。 提交到組合器服務的每個作業都包括文檔描述XML(DDX)文檔、源文檔和外部資源（字串和圖形）。 有關組合器服務的詳細資訊，請參見 [組合器服務概述](../../forms/using/overview-aem-document-services.md#p-assembler-service-p).

您可以對以下操作使用裝配服務：

## 匯編PDF文檔 {#assemble-pdf-documents}

您可以使用組合器服務將兩個或多個PDF文檔組合成單個PDF文檔或PDFPortfolio。 您也可以將功能套用至PDF檔案，以輔助導覽或增強安全性。 以下是匯編PDF文檔的一些方法：

### 組合簡單的PDF文檔 {#assemble-a-simple-pdf-document}

下圖顯示三個源文檔被合併到單個合成文檔中。

![從多個PDF文檔組裝簡單的PDF文檔](assets/as_document_assembly.png)

從多個PDF文檔組裝簡單的PDF文檔

以下示例是用於組合文檔的簡單DDX文檔。 它指定用於生成結果文檔的源文檔的名稱以及結果文檔的名稱：

```xml
<PDF result="Doc4">
<PDF source="Doc1"/>
<PDF source="Doc2"/>
<PDF source="Doc3"/>
</PDF>
```

文檔元件將生成包含以下內容和\
特徵：

* 每個源文檔的全部或部分
* 來自每個源文檔的所有或部分書籤，為組合的結果文檔進行標準化
* 從基本文檔(Doc1)採用的其他特性，包括元資料、頁標籤和頁大小
* 可選地，生成的文檔包括從源文檔中的書籤構建的目錄

### 建立PDFPortfolio {#create-a-pdf-portfolio}

組合器服務可以建立包含文檔集合和自包含用戶介面的PDFPortfolio。 該介面稱為「PDFPortfolio佈局」或「PDFPortfolio導航器」（導航器）。 PDFPortfolio新增導覽器、資料夾和歡迎頁面，以擴充PDF套件的功能。 此介面可善用本地化的文字字串、自訂色彩配置和圖形資源，以增強使用者體驗。 PDFPortfolio還可以包含資料夾，用於組織產品組合中的檔案。

當組合器服務解釋以下DDX文檔時，它將組合一個PDFPortfolio，該PDF包括Portfolio導航器和兩個檔案的包。 服務從myNavigator源指定的位置獲取導航器。 它將導航器的預設顏色配置更改為pinkScheme顏色配置。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1">
<Portfolio>
<Navigator source="myNavigator"/>
<ColorScheme scheme="pinkScheme"/>
</Portfolio>
<PackageFiles>
<PDF source="sourcePDF1"/>
<PDF source="sourcePDF2"/>
</PackageFiles>
</PDF>
</DDX>
```

### 組合加密文檔 {#assemble-encrypted-documents}

在組合文檔時，還可以使用密碼加密PDF文檔。 使用密碼加密PDF檔案後，使用者必須指定密碼才能檢視Adobe Reader或Acrobat中的PDF檔案。 要使用密碼加密PDF文檔，DDX文檔必須包含加密PDF文檔所需的加密元素值。

加密服務不必是LiveCycle安裝的一部分，即可使用密碼加密PDF文檔。

如果對一個或多個輸入文檔進行加密，則提供密碼以作為DDX的一部分開啟文檔。

### 使用Bates編號來組合文檔 {#assemble-documents-using-bates-numbering}

在組合文檔時，可以使用Bates編號將唯一的頁標識符應用到每個頁。 使用Bates編號時，文檔（或文檔集）中的每個頁面都會分配一個唯一標識該頁面的編號。 例如，包含物料清單資訊且與元件生產相關聯的製造文檔可以包含標識符。 Bates數字包含循序遞增的數值以及選用的前置詞和尾碼。 前置詞+數值+尾碼稱為Bates模式。

下圖顯示的PDF文檔包含位於文檔標題中的唯一標識符。

![PDF文檔，包含位於文檔標題中的唯一標識符](do-not-localize/as_batesnumber.png)

PDF文檔，包含位於文檔標題中的唯一標識符

### 平面化和組合檔案 {#flatten-and-assemble-documents}

您可以使用組合器服務將交互PDF文檔（例如，表單）轉換為非交互PDF文檔。 互動式PDF檔案可讓使用者輸入或修改位於PDF檔案欄位中的資料。 將互動式PDF文檔轉換為非互動式PDF文檔的過程稱為拼合。 平面化PDF文檔時，表單欄位將保留其圖形外觀，但不再具有交互性。 平面化PDF檔案的一個原因是為了確保資料無法修改。 此外，與欄位相關聯的指令碼將無法繼續運作。

當您建立從互動式PDF文檔組合的PDF文檔時，組合器服務會先拼合這些表單，然後再將它們組合到生成的文檔中。

>[!NOTE]
>
>組合器服務使用輸出服務來平面化動態XFA表單。 如果組合器服務處理要求其平面化XFA動態表單的DDX，並且輸出服務不可用，則會引發異常。 組合器服務可以平面化Acrobat表單或靜態XFA表單，而不使用輸出服務。

## 匯編XDP文檔 {#assemble-xdp-documents}

您可以使用組合器服務將多個XDP文檔組合為單個XDP文檔或PDF文檔。 對於包含插入點的源XDP檔案，可以指定要插入的片段。

以下是組合XDP檔案的一些方式：

### 組合簡單的XDP檔案 {#assemble-a-simple-xdp-document}

下圖顯示了將三個源XDP文檔組合為單個生成的XDP文檔。 生成的XDP文檔包含三個源XDP文檔，包括其關聯資料。 生成的文檔從作為第一源XDP文檔的基礎文檔中獲取基本屬性。

![從多個XDP檔案組裝簡單的XDP檔案](assets/as_assembler_xdpassembly.png)

從多個XDP檔案組裝簡單的XDP檔案

以下是產生上圖結果的DDX文檔。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="MyXDPResult">
<XDP source="sourceXDP1"/>
<XDP source="sourceXDP2"/>
<XDP source="sourceXDP3"/>
</XDP>
</DDX>
```

### 在元件期間解析參照 {#resolving-references-during-assembly}

通常，XDP文檔可以包含通過絕對參照或相對參照引用的影像。 預設情況下，組合器服務會在生成的XDP文檔中保留對影像的引用。

可以指定組合器服務在組裝時如何通過XDP檔案中的絕對或相對引用處理源XDP文檔中引用的影像。 您可以選擇將所有影像嵌入到結果中，使其不包含相對或絕對參照。 您可以設定resolveAssets標籤的值來定義此值，該標籤可採用下列任一選項。 預設情況下，結果文檔中不解析任何引用。

<table>
 <tbody> 
  <tr> 
   <th>值</th> 
   <th>說明</th> 
  </tr> 
  <tr> 
   <td>無</td> 
   <td>不解析任何引用。</td> 
  </tr> 
  <tr> 
   <td>全部</td> 
   <td>在源XDP文檔中嵌入所有引用的影像。</td> 
  </tr> 
  <tr> 
   <td>相對值</td> 
   <td>在源XDP中嵌入通過相對引用引用引用的所有影像<br /> 檔案。</td> 
  </tr> 
  <tr> 
   <td>絕對值</td> 
   <td>在源XDP中嵌入通過絕對參照引用的所有影像<br /> 檔案。</td> 
  </tr> 
 </tbody> 
</table>

您可以在XDP來源標籤或父XDP結果標籤中指定resolveAssets屬性的值。 如果將屬性指定給XDP結果標籤，則屬性將由所有XDP源元素繼承，這些元素是XDP結果的子項。 但是，顯式指定源元素的屬性將覆蓋該源文檔的結果元素的設定。

#### 解析XDP文檔中的所有源引用 {#resolve-all-source-references-in-an-xdp-document}

要解析源XDP文檔中的所有引用，請為\
生成文檔全部，如下例所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
<XDP source="input3.xdp" />
</XDP>
</DDX
```

您也可以獨立指定所有來源XDP檔案的屬性，以取得相同的屬性\
個結果.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp">
<XDP source="input1.xdp" resolveAssets="all"/>
<XDP source="input2.xdp" resolveAssets="all"/>
<XDP source="input3.xdp" resolveAssets="all"/>
</XDP>
</DDX>
```

#### 解析XDP文檔中選定的源引用 {#resolve-selected-source-references-in-an-xdp-document}

通過為源引用指定resolveAssets屬性，可以選擇性地指定要解析的源引用。 單個源文檔的屬性將覆蓋生成的XDP文檔的設定。 在此範例中，也會解析包含的片段。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" >
<XDPContent source="fragment.xdp" insertionPoint="MyInsertionPoint"
fragment="myFragment"/>
</XDP>
<XDP source="input2.xdp" />
</XDP>
</DDX>
```

#### 選擇性地解析絕對參照或相對參照 {#selectively-resolve-absolute-or-relative-references}

您可以選擇性地解析所有或部分源文檔中的絕對參照或相對參照，如下例所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="absolute">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
</XDP>
</DDX
```

### 動態將表單片段插入XFA表單 {#dynamically-insert-form-fragments-into-an-xfa-form}

您可以使用組合器服務來建立從插入片段的其他XFA表單建立的XFA表單。 使用此功能，您可以使用片段來建立多個表單。

支援動態插入表單片段，支援單一來源控制。 您會維護一個常用元件的來源。 例如，您可以為公司橫幅建立片段。 如果橫幅變更，您只需修改片段即可。 包含片段的其他表單未變更。

表單設計人員使用LiveCycle設計工具來建立表單片段。 這些片段在XFA表單中是唯一命名的子表單。 表單設計人員也使用設計工具來建立具有唯一命名插入點的XFA表單。 您（程式設計師）編寫DDX文檔，以指定如何將片段插入XFA表單中。

下圖顯示兩個XML表單（XFA範本）。 左側的表單包含一個名為myInsertionPoint的插入點。 右側的表單包含名為myFragment的片段。

![將表單片段插入XFA表單](assets/as_assembler_fragment_assy_assembled.png)

將表單片段插入XFA表單

組合器服務解釋下列DDX文檔時，它將建立包含另一個XML表單的XML表單。 myFragmentSource文檔中的myFragment子表單將插入到myFormSource文檔中的myInsertionPoint。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="myFormResult">
<XDP source="myFormSource">
<XDPContent fragment="myFragment" insertionPoint="myInsertionPoint"
source="myFragmentSource"/>
</XDP>
</XDP>
</DDX
```

### 將XDP檔案封裝為PDF {#package-an-xdp-document-as-pdf}

您可以使用組合器服務將XDP文檔打包為PDF文檔，如本DDX文檔所示。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1" encryption="passEncProfile1">
<XDP>
<XDP source="sourceXDP3"/>
<XDP source="sourceXDP4"/>
</XDP>
</PDF>
</DDX>
```

## 拆解PDF文檔 {#disassemble-pdf-documents}

您可以使用組合器服務來拆解PDF文檔。 服務可從源文檔中提取頁面，或基於書籤分割源文檔。 通常，如果PDF文檔最初是從許多單個文檔（如語句集合）建立，則此任務非常有用。

### 從源文檔中提取頁面 {#extract-pages-from-a-source-document}

在下圖中，從源文檔中提取頁1-3，並將其放在新生成的文檔中。

![從源文檔中提取特定頁](assets/as_intro_page_extraction.png)

從源文檔中提取特定頁

以下示例是用於拆卸文檔的DDX文檔。

```xml
<PDF result="Doc4">
<PDF source="Doc2" pages="1-3"/>
</PDF>
```

### 根據書籤劃分源文檔 {#divide-a-source-document-based-on-bookmarks}

在下圖中，DocA被分為多個生成的文檔。 頁面上的第一級書籤標識新生成文檔的開始。

![將基於書籤的源文檔劃分為多個文檔](assets/as_intro_pdfsfrombookmarks.png)

將基於書籤的源文檔劃分為多個文檔

以下示例是使用書籤拆解源文檔的DDX文檔。

```xml
<PDFsFromBookmarks prefix="A">
<PDF source="DocA"/>
</PDFsFromBookmarks>
```

## 確定文檔是否符合PDF/A {#determine-whether-documents-are-pdf-a-compliant}

可以使用組合器服務來確定PDF文檔是否PDF/A相容。 PDF/A是一種存檔格式，用於對文檔的內容進行長期保存。 這些字型嵌入到文檔中，並且該檔案被解壓縮。 因此，PDF/A文檔通常比標準PDF文檔大。 此外，PDF/檔案不包含音訊和視訊內容。

## 獲取有關PDF文檔的資訊 {#obtain-information-about-a-pdf-document}

可以使用組合器服務獲取有關PDF文檔的以下資訊：

* 文字資訊。

   * 文檔的每個頁面上的單詞
   * 文檔每個頁面上每個單詞的位置
   * 文檔每頁的每個段落中的句子

* 書籤，包括頁碼、標題、目的地和外觀。 您可以匯出此\
   從PDF檔案中匯入資料，並匯入PDF檔案。

* 檔案附件，包括檔案資訊。 對於頁面層級的附件，也包含\
   檔案附件注釋的位置。 您可以從PDF檔案匯出此資料，並\
   將其匯入PDF檔案。

* 包檔案，包括檔案資訊、資料夾、包、架構和欄位資料。 您可以從PDF文檔導出此資料，並將其導入PDF文檔。

## 驗證DDX文檔 {#validate-ddx-documents}

可以使用組合器服務來確定DDX文檔是否有效。 例如，如果您從舊版LiveCycle升級，驗證可確保DDX文檔有效。

## 呼叫其他服務 {#call-other-services}

您可以使用DDX檔案，使組合器服務呼叫下列LiveCycle服務。 組合器服務只能調用那些與LiveCycle一起安裝的服務。

**Reader擴充功能服務**:可讓Adobe Reader使用者以數位方式簽署產生的PDF檔案。

**Forms服務**:合併XDP檔案和XML資料檔案，以生成包含已填充的交互表單的PDF文檔。

**輸出服務**:將動態XML表單轉換為包含非互動式表單的PDF文檔（拼合表單）。 組合器服務會拼合靜態的XML表單和Acrobat表單，而不調用輸出服務。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="outDoc">
<PDF source="doc1"/>
<PDF source="doc2"/>
<ReaderRights
credentialAlias="LCESCred"
digitalSignatures="true"/>
</PDF>
</DDX>
```

使用DDX和組合器服務調用其他LiveC週期服務可以簡化您的流程圖。 它甚至可以減少您自訂工作流程所花費的精力。 (另請參閱
