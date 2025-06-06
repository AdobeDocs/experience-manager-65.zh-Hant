---
title: 使用組合器服務
description: 組合器服務可讓您組合、重新排列和增加PDF和XDP檔案，並取得有關PDF檔案的資訊。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
feature: Document Services
exl-id: 84c8125d-0f16-432a-9567-63b868667537
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 2eac9acd8b92582424557222b673211b29a15185
workflow-type: tm+mt
source-wordcount: '2159'
ht-degree: 6%

---

# 使用組合器服務{#using-assembler-service}

組合器服務可讓您組合、重新排列和增加PDF和XDP檔案，並取得有關PDF檔案的資訊。 提交至組合器服務的每個工作都包含檔案描述XML (DDX)檔案、來原始檔及外部資源（字串與圖形）。 如需有關組合器服務的詳細資訊，請參閱[組合器服務概述](../../forms/using/overview-aem-document-services.md#p-assembler-service-p)。

您可以使用組裝服務進行下列操作：

## 組合 PDF 文件 {#assemble-pdf-documents}

您可以使用「組合器」服務，將兩個或多個PDF檔案組合成單一PDF檔案或PDFPortfolio。 您也可以將功能套用至PDF檔案，以協助導覽或增強安全性。 以下是一些組合 PDF 文件的方法：

### 組合一個簡單 PDF 文件 {#assemble-a-simple-pdf-document}

下圖顯示三個來原始檔正在合併為單一結果檔案。

![從多個PDF檔案組合一個簡單的PDF檔案](assets/as_document_assembly.png)

從多個PDF檔案組合簡單PDF檔案

以下範例是用於組合檔案的簡單DDX檔案。 它指定用於產生結果檔案的來原始檔的名稱，以及結果檔案的名稱：

```xml
<PDF result="Doc4">
<PDF source="Doc1"/>
<PDF source="Doc2"/>
<PDF source="Doc3"/>
</PDF>
```

檔案元件會產生一份結果檔案，其中包含以下內容和\
特性：

* 每個來原始檔的全部或部分
* 來自每個來原始檔的全部或部分書籤，針對組合結果檔案加以標準化
* 從基礎檔案(Doc1)採用的其他特性，包括中繼資料、頁面標籤和頁面大小
* 或者，產生的檔案會包括由來原始檔中的書籤建構的目錄

### 建立 PDF 組合 {#create-a-pdf-portfolio}

Assembler服務可建立包含檔案集合和自含使用者介面的PDFPortfolio。 此介面稱為「PDFPortfolio配置」或「PDFPortfolio導覽器（導覽器）」。 PDFPortfolio透過新增瀏覽器、資料夾和歡迎頁面來擴展PDF套件的功能。 此介面可運用當地語系化的文字字串、自訂色彩配置和圖形資源，提升使用者體驗。 PDFPortfolio也可以包含用於組織投資組合中檔案的資料夾。

組合器服務解譯下列DDX檔案時，會組合一個PDFPortfolio，其中包含PDFPortfolio導覽器和兩個檔案的套件。 服務會從myNavigator來源指定的位置取得瀏覽器。 它會將導覽器的預設色彩配置變更為粉紅Scheme色彩配置。

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

### 組合加密的文件 {#assemble-encrypted-documents}

當您組合檔案時，也可以使用密碼加密PDF檔案。 使用密碼加密PDF檔案後，使用者必須指定密碼，才能在Adobe Reader或Acrobat中檢視PDF檔案。 若要使用密碼加密PDF檔案，DDX檔案必須包含加密PDF檔案所需的加密元素值。

加密服務不一定要成為LiveCycle安裝的一部分，才能使用密碼加密PDF檔案。

如果一或多個輸入檔案已加密，請提供密碼以開啟檔案作為DDX的一部分。

### 使用貝茨編號 (Bates numbering) 組合文件 {#assemble-documents-using-bates-numbering}

當您組合檔案時，可以使用Bates編號來將唯一的頁面識別碼套用到每個頁面。 當您使用Bates編號時，檔案（或檔案集）中的每一頁都會指定唯一識別該頁面的編號。 例如，包含用料表資訊且與組裝料號生產相關聯的製造檔案可以包含識別碼。 Bates數字包含循序遞增的數值，以及選用的首碼和尾碼。 前置詞+數值+後置詞稱為bates模式。

下圖顯示的PDF檔案在檔案標題中包含唯一識別碼。

![在檔案的標頭中包含唯一識別碼的PDF檔案](do-not-localize/as_batesnumber.png)

在檔案標題中包含唯一識別碼的PDF檔案

### 扁平化及組合文件 {#flatten-and-assemble-documents}

您可以使用Assembler服務將互動式PDF檔案（例如表單）轉換為非互動式PDF檔案。 互動式PDF檔案可讓使用者在PDF檔案欄位中輸入或修改資料。 將互動式PDF檔案轉換為非互動式PDF檔案的程式稱為平面化。 將PDF檔案平面化時，表單欄位會保留其圖形外觀，但不再具有互動性。 平面化PDF檔案的一個原因是為了確保無法修改資料。 此外，與欄位關聯的指令碼不再運作。

當您建立由互動式PDF檔案組裝的PDF檔案時，組裝程式服務會先將表單平面化，再將其組裝成結果檔案。

>[!NOTE]
>
>組合器服務會使用Output服務來平面化動態XFA表單。 如果Assembler服務處理需要其平面化XFA動態表單的DDX，且Output服務無法使用，則會發生例外狀況。 組合器服務可平面化Acrobat表單或靜態XFA表單，而不使用輸出服務。

## 組合XDP檔案 {#assemble-xdp-documents}

您可以使用Assembler服務將多個XDP檔案組合到單個XDP檔案或PDF檔案中。 對於包含插入點的來源XDP檔案，您可以指定要插入的片段。

以下是組裝XDP檔案的一些方法：

### 組合簡單XDP檔案 {#assemble-a-simple-xdp-document}

下圖顯示三個來源XDP檔案正在組合成單一結果XDP檔案。 產生的XDP檔案包含三個來源XDP檔案及其關聯資料。 產生的檔案會從基礎檔案（第一個來源XDP檔案）取得基本屬性。

![從多個XDP檔案組合一個簡單的XDP檔案](assets/as_assembler_xdpassembly.png)

從多個XDP檔案組合一個簡單的XDP檔案

以下是產生上述結果的DDX檔案。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="MyXDPResult">
<XDP source="sourceXDP1"/>
<XDP source="sourceXDP2"/>
<XDP source="sourceXDP3"/>
</XDP>
</DDX>
```

### 在組裝期間解析參照 {#resolving-references-during-assembly}

通常，XDP檔案可以包含透過絕對或相對參照參照的影像。 組合器服務預設會保留結果XDP檔案中影像的參照。

您可以指定Assembler服務在組裝時如何透過XDP檔案中的絕對或相對參照，處理來源XDP檔案中參照的影像。 您可以選擇將所有影像嵌入結果中，使其不包含相對或絕對參照。 您可透過設定resolveAssets標籤的值來定義此專案，此值可使用下列任一選項。 依預設，結果檔案中不會解析任何參照。

<table>
 <tbody> 
  <tr> 
   <th>值</th> 
   <th>說明</th> 
  </tr> 
  <tr> 
   <td>無</td> 
   <td>不會解析任何參照。</td> 
  </tr> 
  <tr> 
   <td>全部</td> 
   <td>將所有參照的影像內嵌在來源XDP檔案中。</td> 
  </tr> 
  <tr> 
   <td>相對值</td> 
   <td>在來源XDP<br />檔案中嵌入透過相對參照參照的所有影像。</td> 
  </tr> 
  <tr> 
   <td>絕對值</td> 
   <td>在來源XDP<br />檔案中嵌入透過絕對參照參照的所有影像。</td> 
  </tr> 
 </tbody> 
</table>

您可以在XDP來源標籤或父XDP結果標籤中指定resolveAssets屬性的值。 如果將屬性指定給XDP結果標籤，則它將被作為XDP結果子項的所有XDP來源元素繼承。 但是，明確指定來源元素的屬性會覆寫該來原始檔的結果元素設定。

#### 解析XDP檔案中的所有來源參照 {#resolve-all-source-references-in-an-xdp-document}

若要解析來源XDP檔案中的所有參考，請為以下專案指定resolveAssets屬性：\
結果檔案變成全部，如下列範例所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
<XDP source="input3.xdp" />
</XDP>
</DDX
```

您也可以個別指定所有來源XDP檔案的屬性以獲得相同的屬性\
結果。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp">
<XDP source="input1.xdp" resolveAssets="all"/>
<XDP source="input2.xdp" resolveAssets="all"/>
<XDP source="input3.xdp" resolveAssets="all"/>
</XDP>
</DDX>
```

#### 解析XDP檔案中選取的來源參照 {#resolve-selected-source-references-in-an-xdp-document}

您可以透過指定來源參照的resolveAssets屬性，選擇性地指定要解析的來源參照。 個別來原始檔的屬性會覆寫結果XDP檔案的設定。 在此範例中，也解析了包含的片段。

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

#### 解析CRX存放庫上的參考 {#resolve-references-on-crx-repository}

您可以指定來源參照來解析來源參照，方法是
XDP來源中的片段參考。 在以下提供的範例中，也包含片段
已解決。

```xml
<DDX xmlns="http://ns.adobe.com/DDX/1.0/"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://ns.adobe.com/DDX/1.0/ coldfusion_ddx.xsd">
<XDP result="stitched.xdp">
<XDP source="crx:///content/dam/formsanddocuments/test-xdp/sample.xdp" />
</XDP>
</DDX>
```

#### 選擇性地解析絕對或相對參照 {#selectively-resolve-absolute-or-relative-references}

您可以選擇性地解析所有或部分來原始檔中的絕對或相對參照，如下列範例所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="absolute">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
</XDP>
</DDX
```

### 將表單片段動態插入XFA表單 {#dynamically-insert-form-fragments-into-an-xfa-form}

您可以使用Assembler服務來建立XFA表單，此表單是從其他插入片段的XFA表單建立的。 使用此功能，您可以使用片段來建立多個表單。

對表單片段動態插入的支援支援支援單一原始碼控制。 您可維護常用元件的單一來源。 例如，您可以為公司橫幅建立片段。 如果橫幅變更，您只需修改片段。 包含片段的其他表單不會變更。

表單設計人員使用LiveCycleDesigner來建立表單片段。 這些片段在XFA表單中具有獨特的名稱子表單。 表單設計人員也可以使用Designer來建立具有唯一名稱插入點的XFA表單。 您（程式設計人員）撰寫DDX檔案，指定片段插入XFA表單的方式。

下圖顯示兩個XML表單（XFA範本）。 左邊的表單包含一個名為myInsertionPoint的插入點。 右邊的表單包含一個名為myFragment的片段。

![將表單片段插入XFA表單](assets/as_assembler_fragment_assy_assembled.png)

將表單片段插入到XFA表單中

組合器服務解譯下列DDX檔案時，會建立包含其他XML表單的XML表單。 來自myFragmentSource檔案的myFragment子表單插入myFormSource檔案的myInsertionPoint中。

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

您可以使用組合器服務將XDP檔案封裝為PDF檔案，如本DDX檔案所示。

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

## 分解 PDF 文件 {#disassemble-pdf-documents}

您可以使用「組合器」服務來分解PDF檔案。 此服務可以從來原始檔中擷取頁面，或依據書籤分割來原始檔。 通常，如果 PDF 文件最初是從許多個別的文件 (例如報表集合) 建立的，則此作業很有幫助。

### 從來源文件擷取頁面 {#extract-pages-from-a-source-document}

在下圖中，頁面1-3會從來原始檔中擷取，並放置在新的結果檔案中。

![從來原始檔擷取特定頁面](assets/as_intro_page_extraction.png)

從來原始檔擷取特定頁面

以下範例是用來解組檔案的DDX檔案。

```xml
<PDF result="Doc4">
<PDF source="Doc2" pages="1-3"/>
</PDF>
```

### 根據書籤分隔來源文件 {#divide-a-source-document-based-on-bookmarks}

在下圖中，DocA會分成多個產生的檔案。 頁面上的第一個第1層書籤會識別新結果檔案的開頭。

![根據書籤將來原始檔分割成多份檔案](assets/as_intro_pdfsfrombookmarks.png)

根據書籤將來原始檔分割為多個檔案

以下範例是使用書籤來分解來原始檔的DDX檔案。

```xml
<PDFsFromBookmarks prefix="A">
<PDF source="DocA"/>
</PDFsFromBookmarks>
```

## 判斷檔案是否符合PDF/A規範 {#determine-whether-documents-are-pdf-a-compliant}

您可以使用Assembler服務來判斷PDF檔案是否符合PDF/A標準。 PDF/A 是一種用於長期保存文件內容的封存格式。字體內嵌在文件中，檔案未壓縮。因此，PDF/A 文件通常比標準 PDF 文件大。此外，PDF/A 文件不包含音訊和視訊內容。

## 取得PDF檔案的相關資訊 {#obtain-information-about-a-pdf-document}

您可以使用Assembler服務來取得有關PDF檔案的下列資訊：

* 文字資訊。

   * 檔案每一頁上的文字
   * 檔案每一頁上的每個字的位置
   * 檔案每一頁各段落中的句子

* 書籤，包括頁碼、標題、目的地和外觀。 您可以匯出此\
  PDF檔案中的資料，並將其匯入PDF檔案中。

* 檔案附件，包括檔案資訊。 對於頁面層級附件，它也會包含\
  檔案附件附註的位置。 您可以從PDF檔案中匯出此資料，並且\
  將其匯入PDF檔案中。

* 封裝檔案，包括檔案資訊、資料夾、封裝、結構描述和欄位資料。 您可以從PDF檔案匯出此資料，並將其匯入PDF檔案中。

## 驗證DDX檔案 {#validate-ddx-documents}

您可以使用組合器服務來判斷DDX檔案是否有效。 例如，如果您從先前的LiveCycle版本升級，則驗證會確保您的DDX檔案有效。

## 呼叫其他服務 {#call-other-services}

您可以使用DDX檔案，讓Assembler服務呼叫下列LiveC循環服務。 組合器服務只能呼叫隨LiveCycle安裝的那些服務。

**Reader延伸模組服務**：讓Adobe Reader使用者能以數位方式簽署產生的PDF檔案。

**Forms服務**：合併XDP檔案和XML資料檔案，以產生包含已填互動式表單的PDF檔案。

**輸出服務**：將動態XML表單轉換為包含非互動式表單的PDF檔案（將表單平面化）。 Assembler服務會平面化靜態XML表單和Acrobat表單，而不需呼叫Output服務。

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

使用DDX和Assembler服務呼叫其他LiveC週期服務可簡化您的程式圖。 這甚至可以減少您自訂工作流程所花費的時間。 （另請參閱）
