---
title: 使用匯編程式服務
seo-title: Using Assembler Service
description: 「匯編器」服務允許您組合、重新排列和增加PDF和XDP文檔，並獲取有關PDF文檔的資訊。
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
ht-degree: 6%

---

# 使用匯編程式服務{#using-assembler-service}

「匯編器」服務允許您組合、重新排列和增加PDF和XDP文檔，並獲取有關PDF文檔的資訊。 提交到匯編器服務的每個作業都包括文檔說明XML(DDX)文檔、源文檔和外部資源（字串和圖形）。 有關匯編程式服務的詳細資訊，請參見 [匯編程式服務概述](../../forms/using/overview-aem-document-services.md#p-assembler-service-p)。

可將裝配服務用於以下操作：

## 組合 PDF 文件 {#assemble-pdf-documents}

您可以使用匯編器服務將兩個或多個PDF文檔匯編為單個PDF文檔或PDFPortfolio。 您還可以將功能應用於PDF文檔，以幫助導航或增強安全性。 以下是一些組合 PDF 文件的方法：

### 組合一個簡單 PDF 文件 {#assemble-a-simple-pdf-document}

下圖顯示了三個源文檔正在合併到單個合成文檔中。

![從多個PDF文檔中組裝簡單PDF文檔](assets/as_document_assembly.png)

從多個PDF文檔中組裝簡單PDF文檔

以下示例是用於裝配文檔的簡單DDX文檔。 它指定用於生成結果文檔的源文檔的名稱以及結果文檔的名稱：

```xml
<PDF result="Doc4">
<PDF source="Doc1"/>
<PDF source="Doc2"/>
<PDF source="Doc3"/>
</PDF>
```

文檔程式集生成包含以下內容和\
特徵：

* 每個源文檔的全部或部分
* 每個源文檔的所有或部分書籤，為已裝配的合成文檔進行規範化
* 基本文檔(Doc1)中採用的其他特徵，包括元資料、頁標籤和頁面大小
* 可選地，合成文檔包括從源文檔中的書籤構建的目錄

### 建立 PDF 組合 {#create-a-pdf-portfolio}

匯編器服務可以建立PDFPortfolio，這些包含文檔集合和自包含的用戶介面。 該介面稱為PDFPortfolio佈局或PDFPortfolio導航器（導航器）。 PDFPortfolio通過添加導航器、資料夾和歡迎頁擴展了PDF包的功能。 該介面可以利用本地化的文本字串、自定義顏色方案和圖形資源來增強用戶體驗。 PDFPortfolio還可以包括資料夾，用於組織包中的檔案。

當匯編器服務解釋以下DDX文檔時，它會匯編PDFPortfolio，該PDFPortfolio包括導航器和兩個檔案的包。 該服務從myNavigator源指定的位置獲取導航器。 它將導航器的預設顏色方案更改為pinkScheme顏色方案。

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

在匯編文檔時，還可以使用密碼對PDF文檔進行加密。 使用密碼加密PDF文檔後，用戶必須指定密碼才能查看Adobe Reader或Acrobat的PDF文檔。 要使用密碼加密PDF文檔，DDX文檔必須包含加密PDF文檔所需的加密元素值。

加密服務不必是LiveCycle安裝的一部分，就可以使用密碼加密PDF文檔。

如果一個或多個輸入文檔被加密，則提供密碼以作為DDX的一部分開啟文檔。

### 使用貝茨編號 (Bates numbering) 組合文件 {#assemble-documents-using-bates-numbering}

在匯編文檔時，可以使用Bates編號將唯一的頁面標識符應用於每個頁面。 使用Bates編號時，文檔（或文檔集）中的每個頁面都會分配一個唯一標識頁面的編號。 例如，包含物料清單資訊並與元件生產相關聯的製造文檔可以包含標識符。 Bates數字包含一個按順序遞增的數字值以及一個可選前置詞和尾碼。 前置詞+數字值+尾碼稱為bates模式。

下圖顯示一個PDF文檔，該文檔包含位於文檔標題中的唯一標識符。

![包含位於文檔標題中的唯一標識符的PDF文檔](do-not-localize/as_batesnumber.png)

包含位於文檔標題中的唯一標識符的PDF文檔

### 扁平化及組合文件 {#flatten-and-assemble-documents}

您可以使用匯編器服務將互動式PDF文檔（例如，表單）轉換為非互動式PDF文檔。 互動式PDF文檔允許用戶輸入或修改位於PDF文檔欄位中的資料。 將互動式PDF文檔轉換為非互動式PDF文檔的過程稱為拼合。 當PDF文檔展平時，表單域將保留其圖形外觀，但不再交互。 展平PDF文檔的一個原因是確保資料無法修改。 此外，與欄位關聯的指令碼不再起作用。

當您建立從互動式PDF文檔裝配的PDF文檔時，「匯編器」服務會先拼合這些表單，然後再將它們裝配到合成文檔中。

>[!NOTE]
>
>匯編器服務使用輸出服務來拼合動態XFA表單。 如果匯編器服務處理要求它平整XFA動態表單的DDX，並且輸出服務不可用，則會引發異常。 匯編器服務可以拼合Acrobat表單或靜態XFA表單，而不使用輸出服務。

## 匯編XDP文檔 {#assemble-xdp-documents}

您可以使用匯編器服務將多個XDP文檔匯編為單個XDP文檔或PDF文檔。 對於包含插入點的源XDP檔案，可以指定要插入的片段。

以下是匯編XDP文檔的一些方法：

### 匯編簡單的XDP文檔 {#assemble-a-simple-xdp-document}

下圖顯示三個源XDP文檔被裝配到單個合成XDP文檔中。 生成的XDP文檔包含三個源XDP文檔，包括它們的關聯資料。 結果文檔從基礎文檔（即第一源XDP文檔）獲取基本屬性。

![從多個XDP文檔組裝簡單的XDP文檔](assets/as_assembler_xdpassembly.png)

從多個XDP文檔組裝簡單的XDP文檔

這是一個DDX文檔，它生成上面所示的結果。

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

通常，XDP文檔可以包含通過絕對或相對引用引用的影像。 預設情況下，匯編器服務會保留對結果XDP文檔中影像的引用。

可以指定匯編器服務在匯編時如何處理源XDP文檔中引用的影像，這些影像是通過XDP檔案中的絕對或相對引用進行的。 您可以選擇將所有影像嵌入到結果中，以使其不包含相對或絕對參照。 可通過設定resolveAssets標籤的值來定義此項，該標籤可以採用以下任何選項。 預設情況下，結果文檔中不解析任何引用。

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
   <td>嵌入源XDP中通過相對引用引用引用的所有影像<br /> 的子菜單。</td> 
  </tr> 
  <tr> 
   <td>絕對值</td> 
   <td>在源XDP中嵌入通過絕對引用引用引用的所有影像<br /> 的子菜單。</td> 
  </tr> 
 </tbody> 
</table>

可以在XDP源標籤或父XDP結果標籤中指定resolveAssets屬性的值。 如果將屬性指定到XDP結果標籤，則所有XDP源元素（XDP結果的子元素）將繼承該屬性。 但是，顯式指定源元素的屬性將覆蓋僅針對該源文檔的結果元素的設定。

#### 解析XDP文檔中的所有源引用 {#resolve-all-source-references-in-an-xdp-document}

要解析源XDP文檔中的所有引用，請為\
結果文檔到所有，如下例所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
<XDP source="input3.xdp" />
</XDP>
</DDX
```

您還可以單獨為所有源XDP文檔指定屬性，以獲得相同的屬性\
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

通過為源引用指定resolveAssets屬性，可以有選擇地指定要解析的源引用。 單個源文檔的屬性會覆蓋生成的XDP文檔的設定。 在本例中，還解析了包括的片段。

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

#### 有選擇地解析絕對或相對參照 {#selectively-resolve-absolute-or-relative-references}

可有選擇地解析所有或部分源文檔中的絕對或相對參照，如下例所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="absolute">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
</XDP>
</DDX
```

### 動態地將表單片段插入XFA表單 {#dynamically-insert-form-fragments-into-an-xfa-form}

可以使用匯編器服務建立XFA表單，該表單是從插入片段的另一個XFA表單建立的。 使用此功能，可以使用片段建立多個表單。

支援表單片段的動態插入支援單源控制。 維護常用元件的單個源。 例如，您可以為公司橫幅建立片段。 如果標題更改，則只需修改片段。 包含片段的其它表單保持不變。

表單設計器使用LiveCycle設計器建立表單片段。 這些片段在XFA窗體中是唯一命名的子窗體。 表單設計器還使用設計器建立具有唯一命名插入點的XFA表單。 您（程式設計師）編寫DDX文檔，指定如何將片段插入XFA表單。

下圖顯示了兩個XML表單（XFA模板）。 左側的表單包含一個名為myInsertionPoint的插入點。 右側的表單包含名為myFragment的片段。

![將表單片段插入XFA表單](assets/as_assembler_fragment_assy_assembled.png)

將表單片段插入XFA表單

匯編器服務在解釋以下DDX文檔時，會建立包含另一個XML表單的XML表單。 myFragmentSource文檔的myFragment子窗體將插入myFormSource文檔的myInsertionPoint中。

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

### 將XDP文檔打包為PDF {#package-an-xdp-document-as-pdf}

您可以使用匯編器服務將XDP文檔打包為PDF文檔，如此DDX文檔中所示。

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

可以使用匯編程式服務來拆解PDF文檔。 該服務可以從源文檔中提取頁面或基於書籤劃分源文檔。 通常，如果 PDF 文件最初是從許多個別的文件 (例如報表集合) 建立的，則此作業很有幫助。

### 從來源文件擷取頁面 {#extract-pages-from-a-source-document}

在下圖中，從源文檔中提取第1-3頁，並將其放在新合成文檔中。

![從源文檔中提取特定頁面](assets/as_intro_page_extraction.png)

從源文檔中提取特定頁面

以下示例是用於拆卸文檔的DDX文檔。

```xml
<PDF result="Doc4">
<PDF source="Doc2" pages="1-3"/>
</PDF>
```

### 根據書籤分隔來源文件 {#divide-a-source-document-based-on-bookmarks}

在下圖中，DocA分為多個結果文檔。 頁面上的第一級書籤標識新合成文檔的開始。

![將基於書籤的源文檔劃分為多個文檔](assets/as_intro_pdfsfrombookmarks.png)

將基於書籤的源文檔劃分為多個文檔

以下示例是使用書籤來拆卸源文檔的DDX文檔。

```xml
<PDFsFromBookmarks prefix="A">
<PDF source="DocA"/>
</PDFsFromBookmarks>
```

## 確定文檔是否符合PDF/A {#determine-whether-documents-are-pdf-a-compliant}

您可以使用匯編器服務來確定PDF文檔是否與PDF/A相容。 PDF/A 是一種用於長期保存文件內容的封存格式。字體內嵌在文件中，檔案未壓縮。因此，PDF/A 文件通常比標準 PDF 文件大。此外，PDF/A 文件不包含音訊和視訊內容。

## 獲取有關PDF文檔的資訊 {#obtain-information-about-a-pdf-document}

您可以使用匯編器服務獲取有關PDF文檔的以下資訊：

* 文本資訊。

   * 文檔每頁上的詞
   * 文檔每頁上每個單詞的位置
   * 文檔每頁各段中的句子

* 書籤，包括頁碼、標題、目標和外觀。 您可以導出此\
   從PDF文檔中導入資料，並將其導入PDF文檔。

* 檔案附件，包括檔案資訊。 對於頁面級附件，它還包括\
   檔案附件注釋的位置。 可以從PDF文檔導出此資料，\
   將其導入PDF文檔。

* 包檔案，包括檔案資訊、資料夾、包、架構和欄位資料。 您可以從PDF文檔導出此資料，然後將其導入PDF文檔。

## 驗證DDX文檔 {#validate-ddx-documents}

您可以使用匯編器服務來確定DDX文檔是否有效。 例如，如果從以前的LiveCycle版本升級，驗證將確保DDX文檔有效。

## 呼叫其他服務 {#call-other-services}

可以使用DDX文檔，這些文檔使匯編程式服務調用以下LiveC循環服務。 匯編程式服務只能調用那些安裝有LiveCycle的服務。

**Reader擴展服務**:使Adobe Reader用戶能夠對生成的PDF文檔進行數字簽名。

**Forms**:合併XDP檔案和XML資料檔案，以生成包含填充的互動式表單的PDF文檔。

**輸出服務**:將動態XML表單轉換為包含非交互表單（拼合表單）的PDF文檔。 匯編器服務將拼合靜態XML表單和Acrobat表單，而不調用輸出服務。

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

使用DDX和匯編程式服務調用其他LiveC循環服務可簡化流程圖。 它甚至可以減少您定制工作流所花費的工作量。 (另請參閱
