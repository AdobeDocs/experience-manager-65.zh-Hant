---
title: 使用Assembler Service
seo-title: 使用Assembler Service
description: Assembler服務可讓您合併、重新排列和增強PDF和XDP檔案，並取得PDF檔案的相關資訊。
seo-description: Assembler服務可讓您合併、重新排列和增強PDF和XDP檔案，並取得PDF檔案的相關資訊。
uuid: 1efce50b-2d98-408e-aa43-ac4999de41a8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 6a99042f-79c7-494b-bca0-73f2b5725b58
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 使用Assembler Service{#using-assembler-service}

Assembler服務可讓您合併、重新排列和增強PDF和XDP檔案，並取得PDF檔案的相關資訊。 提交到Assembler服務的每個作業都包括文檔描述XML(DDX)文檔、源文檔和外部資源（字串和圖形）。 有關匯編器服務的詳細資訊，請參 [閱匯編器服務概述](../../forms/using/overview-aem-document-services.md#p-assembler-service-p)。

您可以對以下操作使用裝配服務：

## 匯整PDF檔案 {#assemble-pdf-documents}

您可以使用Assembler服務，將兩份或多份PDF檔案組合為單一PDF檔案或PDF資料夾。 您也可以將有助於導覽或增強安全性的功能套用至PDF檔案。 以下是您組合PDF檔案的一些方式：

### 匯整簡單的PDF檔案 {#assemble-a-simple-pdf-document}

下圖顯示三個源文檔要合併到單個合成文檔中。

![從多份PDF檔案組合簡單的PDF檔案](assets/as_document_assembly.png)

從多份PDF檔案組合簡單的PDF檔案

以下示例是用於組合文檔的簡單DDX文檔。 它指定用於生成合成文檔的源文檔的名稱以及合成文檔的名稱：

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
* 每個來源檔案的全部或部分書籤，已針對組合的結果檔案進行標準化
* 基本文檔(Doc1)中採用的其他特性，包括元資料、頁標籤和頁面大小
* 可選地，合成文檔包括從源文檔中的書籤構造的目錄

### 建立PDF資料夾 {#create-a-pdf-portfolio}

Assembler服務可以建立包含檔案集合和獨立使用者介面的PDF資料夾。 此介面稱為「PDF資料夾版面」或「PDF資料夾導覽器」（導覽器）。 PDF資料夾新增導覽器、檔案夾和歡迎頁面，以擴充PDF套件的功能。 此介面可運用本地化的文字字串、自訂的色彩配置和圖形資源來增強使用者體驗。 PDF資料夾也可以包含資料夾，用於組織資料夾中的檔案。

當Assembler服務解譯下列DDX檔案時，它會組合PDF資料夾，其中包含PDF資料夾導覽器和兩個檔案的套件。 服務從myNavigator源指定的位置獲取導航器。 它會將導覽器的預設色彩配置變更為pinkScheme色彩配置。

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

### 組合加密的檔案 {#assemble-encrypted-documents}

當您組合檔案時，也可以使用密碼來加密PDF檔案。 使用密碼加密PDF檔案後，使用者必須指定密碼才能在Adobe Reader或Acrobat中檢視PDF檔案。 要使用密碼加密PDF文檔，DDX文檔必須包含加密PDF文檔所需的加密元素值。

Encryption服務不必是LiveCycle安裝的一部分，就能使用密碼來加密PDF檔案。

如果一個或多個輸入文檔被加密，請提供密碼以作為DDX的一部分開啟該文檔。

### 使用Bates編號來組合檔案 {#assemble-documents-using-bates-numbering}

在組合文檔時，可以使用Bates編號將唯一的頁面標識符應用於每個頁面。 當您使用Bates編號時，檔案（或檔案集）中的每個頁面都會指派一個唯一識別頁面的編號。 例如，包含物料清單資訊並與元件生產關聯的製造文檔可以包含標識符。 Bates數字包含循序遞增的數值，以及選用的首碼和字尾。 前置詞+數值+尾碼稱為bates模式。

下圖顯示PDF檔案，其中包含位於檔案標題中的唯一識別碼。

![PDF檔案包含位於檔案標題中的唯一識別碼](do-not-localize/as_batesnumber.png)

PDF檔案包含位於檔案標題中的唯一識別碼

### 平面化及組合檔案 {#flatten-and-assemble-documents}

您可以使用Assembler服務將互動式PDF檔案（例如表單）轉換為非互動式PDF檔案。 互動式PDF檔案可讓使用者輸入或修改PDF檔案欄位中的資料。 將互動式PDF檔案轉換為非互動式PDF檔案的程式稱為平面化。 平面化PDF檔案時，表單欄位會保留其圖形外觀，但不再具互動性。 平面化PDF檔案的一個原因是為了確保資料無法修改。 此外，與欄位相關聯的指令碼不再起作用。

當您從互動式PDF檔案建立PDF檔案時，Assembler服務會先將這些表單平面化，再將它們組合為結果檔案。

>[!NOTE]
>
>Assembler服務使用Output服務來平面化動態XFA表單。 如果Assembler服務處理要求其平面化XFA動態表單的DDX，且Output服務不可用，則會拋出異常。 Assembler服務可平面化Acrobat表格或靜態XFA表格，而不需使用Output服務。

## 匯整XDP檔案 {#assemble-xdp-documents}

您可以使用Assembler服務將多個XDP檔案組合為單一XDP檔案或PDF檔案。 對於包含插入點的源XDP檔案，可以指定要插入的片段。

以下是組合XDP檔案的一些方式：

### 組合簡單的XDP檔案 {#assemble-a-simple-xdp-document}

下圖顯示了將三個源XDP文檔組裝成單一合成的XDP文檔。 生成的XDP文檔包含三個源XDP文檔，包括其關聯資料。 生成的文檔從作為第一源XDP文檔的基本文檔獲得基本屬性。

![從多個XDP檔案組合簡單的XDP檔案](assets/as_assembler_xdpassembly.png)

從多個XDP檔案組合簡單的XDP檔案

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

### 在元件期間解析參照 {#resolving-references-during-assembly}

通常，XDP文檔可以包含通過絕對或相對參照引用的影像。 預設情況下，匯編器服務會保留合成XDP文檔中對影像的引用。

可以指定Assembler服務在組裝時如何通過XDP檔案中的絕對或相對參照來處理源XDP文檔中引用的影像。 您可以選擇將所有影像嵌入到結果中，使其不包含相對或絕對參照。 您可以通過設定resolveAssets標籤的值來定義此標籤，該標籤可採用以下任何選項。 預設情況下，結果文檔中不解析任何參照。

<table>
 <tbody> 
  <tr> 
   <th>值</th> 
   <th>說明</th> 
  </tr> 
  <tr> 
   <td>無</td> 
   <td>不解析任何參照。</td> 
  </tr> 
  <tr> 
   <td>全部</td> 
   <td>將所有參考影像內嵌在來源XDP檔案中。</td> 
  </tr> 
  <tr> 
   <td>相對值</td> 
   <td>嵌入源XDP文檔中通過相對引用引用引用的所有影像<br /> 。</td> 
  </tr> 
  <tr> 
   <td>絕對值</td> 
   <td>嵌入源XDP文檔中通過絕對引用引用引用的所有影像<br /> 。</td> 
  </tr> 
 </tbody> 
</table>

您可以在XDP源標籤或父XDP結果標籤中指定resolveAssets屬性的值。 如果將屬性指定給XDP結果標籤，則屬性將由所有XDP源元素繼承，這些元素是XDP結果的子元素。 但是，顯式指定源元素的屬性將覆蓋該源文檔的結果元素的設定。

#### 解析XDP文檔中的所有源引用 {#resolve-all-source-references-in-an-xdp-document}

要解析源XDP文檔中的所有引用，請為\
合成文檔到所有文檔，如下例所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
<XDP source="input3.xdp" />
</XDP>
</DDX
```

您也可以單獨指定所有來源XDP檔案的屬性，以取得相同的\
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

通過為源引用指定resolveAssets屬性，可以有選擇地指定要解析的源引用。 個別來源檔案的屬性會覆寫產生的XDP檔案設定。 在此範例中，也會解決包含的片段。

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

#### 選擇性解析絕對或相對參照 {#selectively-resolve-absolute-or-relative-references}

您可以選擇性地解析所有或部分源文檔中的絕對或相對參照，如下例所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="absolute">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
</XDP>
</DDX
```

### 動態將表單片段插入XFA表單 {#dynamically-insert-form-fragments-into-an-xfa-form}

您可以使用Assembler服務建立從插入片段的另一個XFA表單建立的XFA表單。 使用此功能，您可以使用片段來建立多個表單。

支援動態插入表單片段，支援單一來源控制。 您會維護單一常用元件來源。 例如，您可以為公司橫幅建立片段。 如果橫幅變更，您只需修改片段即可。 包含片段的其他表格則保持不變。

表單設計人員使用LiveCycle Designer來建立表單片段。 這些片段在XFA表單中具有唯一的命名子表單。 表單設計人員也使用設計人員來建立具有唯一命名插入點的XFA表單。 您（程式設計人員）可編寫DDX檔案，以指定片段插入XFA表單的方式。

下圖顯示兩個XML表單（XFA範本）。 左側的表單包含一個名為myInsertionPoint的插入點。 右側的表格包含名為myFragment的片段。

![將表單片段插入XFA表單](assets/as_assembler_fragment_assy_assembled.png)

將表單片段插入XFA表單

當Assembler服務解譯下列DDX文檔時，它將建立包含另一個XML表單的XML表單。 myFragmentSource文檔中的myFragment子表單將插入myFormSource文檔的myInsertionPoint。

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

您可以使用Assembler服務將XDP文檔封裝為PDF文檔，如本DDX文檔所示。

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

## 反匯編PDF檔案 {#disassemble-pdf-documents}

您可以使用Assembler服務來反匯編PDF文檔。 服務可以從源文檔中提取頁面或基於書籤劃分源文檔。 通常，如果PDF檔案最初是由許多個別檔案（例如陳述式集合）建立，則此工作很有用。

### 從來源檔案擷取頁面 {#extract-pages-from-a-source-document}

在下圖中，頁面1-3是從來源檔案擷取，並放入新的合成檔案中。

![從源文檔中提取特定頁面](assets/as_intro_page_extraction.png)

從源文檔中提取特定頁面

以下示例是用於拆解文檔的DDX文檔。

```xml
<PDF result="Doc4">
<PDF source="Doc2" pages="1-3"/>
</PDF>
```

### 根據書籤劃分來源檔案 {#divide-a-source-document-based-on-bookmarks}

在下圖中，DocA被分為多個生成的文檔。 頁面上的第1級書籤可識別新結果檔案的開頭。

![將以書籤為基礎的來源檔案分割為多個檔案](assets/as_intro_pdfsfrombookmarks.png)

將以書籤為基礎的來源檔案分割為多個檔案

以下範例是DDX檔案，它使用書籤來拆解來源檔案。

```xml
<PDFsFromBookmarks prefix="A">
<PDF source="DocA"/>
</PDFsFromBookmarks>
```

## 判斷檔案是否與PDF/A相容 {#determine-whether-documents-are-pdf-a-compliant}

您可以使用Assembler服務來判斷PDF檔案是否與PDF/A相容。 PDF/A是一種封存格式，用於長期保存檔案內容。 字型會內嵌在檔案中，檔案會解壓縮。 因此，PDF/A檔案通常比標準PDF檔案大。 此外，PDF/A檔案不包含音訊和視訊內容。

## 取得PDF檔案的相關資訊 {#obtain-information-about-a-pdf-document}

您可以使用Assembler服務獲得有關PDF文檔的以下資訊：

* 文字資訊。

   * 檔案每頁的字詞
   * 每個單字在檔案每頁的位置
   * 檔案每頁各段的句子

* 書籤，包括頁碼、標題、目的地和外觀。 您可以匯出此\
   將資料從PDF檔案匯入PDF檔案。

* 檔案附件，包括檔案資訊。 對於頁面層級的附件，它也包含\
   檔案附件注釋的位置。 您可以從PDF檔案匯出此資料，\
   將它匯入PDF檔案。

* 封裝檔案，包括檔案資訊、檔案夾、封裝、架構和欄位資料。 您可以從PDF檔案匯出此資料，並將它匯入PDF檔案。

## 驗證DDX檔案 {#validate-ddx-documents}

您可以使用Assembler服務來確定DDX文檔是否有效。 例如，如果您從舊版LiveCycle升級，驗證會確保DDX檔案有效。

## 呼叫其他服務 {#call-other-services}

您可以使用DDX檔案，讓Assembler服務呼叫下列LiveCycle服務。 Assembler服務只能呼叫與LiveCycle一起安裝的服務。

**Reader Extensions服務**:讓Adobe Reader使用者數位簽署產生的PDF檔案。

**Forms服務**:合併XDP檔案和XML資料檔案，以產生包含已填寫互動式表單的PDF檔案。

**輸出服務**:將動態XML表單轉換為包含非互動表單（平面化表單）的PDF檔案。 Assembler服務可平面化靜態XML表單和Acrobat表單，而不需呼叫Output服務。

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

使用DDX和Assembler服務來呼叫其他LiveCycle服務，可簡化您的程式圖。 它甚至可以降低您自訂工作流程所花費的心力。 (另請參閱
