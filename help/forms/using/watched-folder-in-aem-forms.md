---
title: 在AEM Forms中觀看資料夾
seo-title: Watched folder in AEM Forms
description: 管理員可以將資料夾置於監視資料夾中，並在檔案置於監視資料夾中時啟動工作流程、服務或指令碼操作。
seo-description: An administrator can put a folder on watch and start a workflow, service, or script operation when a file is placed in the folder being watched.
uuid: 39eac0fd-8212-46ff-b75d-8b4320d448a9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: db38972c-be3f-49fd-8cc1-45b16ed244af
docset: aem65
exl-id: fbf5c7c3-cb01-4fda-8e5d-11d56792d4bf
source-git-commit: 79dcba8e14eac39467510416bf31737ac721b07f
workflow-type: tm+mt
source-wordcount: '7118'
ht-degree: 0%

---

# 在AEM Forms中觀看資料夾{#watched-folder-in-aem-forms}

管理員可以配置網路資料夾（稱為「觀看資料夾」），以便當用戶將檔案(如PDF檔案)放入「觀看資料夾」時，將啟動預先配置的工作流、服務或指令碼操作以處理添加的檔案。 服務執行指定操作後，會將結果檔案保存在指定的輸出資料夾中。 有關工作流、服務和指令碼的詳細資訊，請參閱[處理檔案的各種方法](#variousmethodsforprocessingfiles)。

## 建立監看資料夾 {#create-a-watched-folder}

您可以使用下列其中一種方法，在檔案系統上建立「監看資料夾」：

* 在配置「監看資料夾」配置節點的屬性時，在folderPath屬性中鍵入父目錄的完整路徑，並附加要建立的「監看資料夾」的名稱，如以下示例所示：`C:/MyPDFs/MyWatchedFolder`
`MyWatchedFolder`資料夾不存在，AEM Forms會嘗試在指定路徑上建立資料夾。

* 在配置「監視的資料夾」端點之前，在檔案系統上建立資料夾，然後在folderPath屬性中提供完整路徑。 有關folderPath屬性的詳細資訊，請參閱[Watched Folder屬性](#watchedfolderproperties)。

>[!NOTE]
>
>在群集環境中，用作監視資料夾的資料夾必須在檔案系統或網路上可訪問、可寫和共用。 群集的每個應用程式伺服器實例必須具有對同一共用資料夾的訪問權限。 在Windows上，在所有伺服器上建立映射的網路驅動器，並在folderPath屬性中指定映射的網路驅動器的路徑。

## 建立監看資料夾配置節點 {#create-watched-folder-configuration-node}

若要設定「觀看資料夾」，請建立「觀看資料夾」設定節點。 執行下列步驟以建立設定節點：

1. 以管理員身分登入CRX-DE lite，並導覽至/etc/fd/watchfolder/config資料夾。

1. 建立`nt:unstructured`類型的節點。 例如，watchedfolder

   >[!NOTE]
   >
   >「觀看的資料夾」節點名稱不能包含空格和特殊字元。

1. 將下列屬性新增至節點：

   * `folderPath`
   * `inputProcessorType`
   * `inputProcessorId`
   * `outputFilePattern`
   如需支援屬性的完整清單，請參閱[監看資料夾屬性](#watchedfolderproperties)。

1. 按一下「**全部保存**」。 建立節點並儲存屬性後。 `input`、`result`、`failure`、`preserve`和`stage`資料夾是在`folderPath`屬性中指定的路徑上建立的。

   掃描作業會以定義的時間間隔開始掃描「監看的資料夾」。

## 監看的資料夾屬性 {#watchedfolderproperties}

您可以為「觀看的資料夾」配置以下屬性。

* **folderPath（字串）**:要以定義的時間間隔掃描的資料夾路徑。對於群集環境，資料夾必須位於共用位置，所有伺服器都具有對伺服器的完全訪問權限。 這是強制屬性。
* **inputProcessorType（字串）**:要啟動的進程類型。您可以指定工作流程、指令碼或服務。 這是強制屬性。
* **inputProcessorId（字串）**:inputProcessorId屬性的行為基於為inputProcessorType屬性指定的值。這是強制屬性。 以下清單詳細說明inputProcessorType屬性的所有可能值以及inputProcessorType屬性的相應必需項：

   * 對於工作流，指定要執行的工作流模型。 例如， /etc/workflow/models/&lt;workflow_name>/jcr:content/model
   * 對於指令碼，指定要執行的指令碼的JCR路徑。 例如， /etc/fd/watchfolder/test/testScript.ecma
   * 對於服務，請指定用於查找OSGi服務的篩選器。 此服務已註冊為com.adobe.aemfd.watchfolder.service.api.ContentProcessor介面的實作。

* **runModes（字串）**:用於工作流執行的允許運行模式的逗號分隔清單。以下是幾個範例：

   * 作者

   * 發佈

   * author,publish

   * 發佈，作者

>[!NOTE]
>
>如果托管「觀看」資料夾的伺服器沒有任何指定的運行模式，則無論伺服器上的運行模式如何，「觀看」資料夾都始終被激活。

* **outputFilePattern（字串）**:輸出檔案的模式。您可以指定資料夾或檔案模式。 如果指定了資料夾模式，則輸出檔案的名稱如工作流中所述。 如果指定了檔案模式，則輸出檔案的名稱如檔案模式中所述。 [檔案和資料](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) 夾模式還可以指定輸出檔案的目錄結構。這是強制屬性。

* **stageFileExpirationDuration(Long, default -1)**:已擷取以進行處理的輸入檔案/資料夾之前等待的秒數，應視為已逾時，並標示為失敗。此屬性的值為正數時，才會啟動此過期機制。

>[!NOTE]
>
>即使使用此機制將輸入標籤為已超時，它仍可能在後台處理，但所花的時間比預期的要長。 如果逾時機制啟動前已使用輸入內容，處理甚至可能稍後繼續完成，並將輸出傾棄至結果資料夾。 如果逾時前未使用內容，稍後嘗試使用內容時，處理很可能會發生錯誤，而此錯誤也會記錄在相同輸入的失敗資料夾中。 另一方面，如果因間歇性作業/工作流程失火而未啟動輸入處理（過期機制旨在解決的案例），則當然，這兩種情況都不會發生。 因此，對於因超時而標籤為失敗的失敗資料夾中的任何條目(查找「長時間後未處理的檔案，標籤為失敗！」形式的消息！ 在故障日誌中)，建議掃描結果資料夾（以及同一輸入的另一個條目的故障資料夾本身），以檢查是否實際發生了先前描述的任何情況。

* **deleteExpiredStageFileOnlyWhenThrotled（布林值，預設為true）:** 過期機制是否應僅在Watch資料夾被限制時激活。該機制與已調節的監看資料夾更相關，因為在未處理狀態中停留的少量檔案（由於間歇性作業/工作流失火）在啟用節流時有可能阻塞整個批的處理。 如果此屬性保持為true（預設值），則過期機制將不會對未限制的監看資料夾啟用。 如果屬性保持為false，只要stageFileExpirationDuration屬性為正數，機制將始終激活。

* **pollInterval(Long)**:掃描「監看」資料夾以進行輸入的間隔（秒）。除非啟用「調節」設定，否則輪詢間隔應比處理平均作業的時間長；否則，系統可能會變得過載。 預設值為 5。如需詳細資訊，請參閱批次大小說明。 pollinterval的值必須大於或等於1。
* **excludeFilePattern（字串）**:分號(;)分隔的模式清單，「觀看的資料夾」會使用該清單來判斷要掃描和擷取的檔案和資料夾。系統不會掃描任何具有此模式的檔案或資料夾以進行處理。 如果輸入是包含多個檔案的資料夾，此設定就十分實用。 資料夾的內容可以複製到名稱由「已觀看」資料夾擷取的資料夾中。 這樣，在資料夾完全複製到輸入資料夾之前，「觀看的資料夾」就無法擷取資料夾以進行處理。 預設值為null。
您可以使用[檔案模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)來排除：

   * 具有特定副檔名的檔案；例如*.dat、*.xml、.pdf、*。*
   * 具有特定名稱的檔案；例如， data*會排除名為data1、data2等的檔案和資料夾。
   * 名稱和副檔名中包含複合運算式的檔案，如下列範例所示：

      * Data[0-9][0-9][0-9]。[dD][aA]&#39;port&#39;
      * *.[dD][Aa]&#39;port&#39;
      * *.[Xx][Mm][Ll]

有關檔案模式的詳細資訊，請參閱[關於檔案模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)。

* **includeFilePattern（字串）**:分號(;)分隔的模式清單，「觀看的資料夾」會使用該清單來判斷要掃描和擷取的資料夾和檔案。例如，如果輸入* IncludeFilePattern，則會拾取所有與輸入*匹配的檔案和資料夾。 這包括名為input1、input2等的檔案和資料夾。 預設值為* ，表示所有檔案和資料夾。 您可以使用檔案模式來包括：

   * 具有特定副檔名的檔案；例如*.dat、*.xml、.pdf、*。*
   * 具有特定名稱的檔案；例如，資料。*會包含名為data1、data2等的檔案和資料夾。

* 名稱和副檔名中包含複合運算式的檔案，如下列範例所示：

   * Data[0-9][0-9][0-9]。[dD][aA]&#39;port&#39;

      * *.[dD][Aa]&#39;port&#39;
      * *.[Xx][Mm][Ll]

有關檔案模式的詳細資訊，請參閱[關於檔案模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)

* **waitTime(Long)**:建立資料夾或檔案後，在掃描資料夾或檔案之前等待的時間（以毫秒為單位）。例如，如果等待時間為3,600,000毫秒（一小時），而檔案是在一分鐘前建立的，則此檔案將在59分鐘或更長時間過後擷取。 預設值為 0。此設定對於確保將檔案或資料夾完全複製到輸入資料夾非常有用。 例如，如果要處理大型檔案，而要下載該檔案需要10分鐘，請將等待時間設定為10*60*1000毫秒。 如果檔案未保存10分鐘，則阻止「監視的資料夾」掃描該檔案。
* **purgeDuration(Long)**:結果資料夾中的檔案和資料夾早於此值時將被清除。此值以天計量。 此設定有助於確保結果資料夾不會填滿。 值為–1天表示絕不刪除結果資料夾。 預設值為–1。
* **resultFolderName（字串）**:儲儲存存結果的資料夾。如果結果未出現在此資料夾中，請檢查失敗資料夾。 不會處理唯讀檔案，且會將其儲存在失敗資料夾中。 此值可以是具有下列檔案模式的絕對或相對路徑：

   * %F =檔案名首碼
   * %E =副檔名
   * %Y =年（已滿）
   * %y =年（最後兩位）
   * %M =月
   * %D =月中的第幾天
   * %d =年
   * %H =小時（24小時時鐘）
   * %h =小時（12小時時鐘）
   * %m =分鐘
   * %s =秒
   * %l =毫秒
   * %R =隨機數（介於0到9之間）
   * %P =進程或作業ID
   例如，如果它是2009年7月17日的晚上8點，並且您指定C:/Test/WF0/failure/%Y/%M/%D/%H/，則結果資料夾為C:/Test/WF0/failure/2009/07/17/20

   如果路徑不是絕對路徑，而是相對路徑，則資料夾會建立在「監看」資料夾內。 預設值為result/%Y/%M/%D/，即「監視」資料夾內的「結果」資料夾。 有關檔案模式的詳細資訊，請參閱[關於檔案模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)。

>[!NOTE]
>
>結果資料夾的大小越小，「觀看的資料夾」的執行效能就越好。 例如，如果「監看資料夾」的預計負載每小時為1000個檔案，請嘗試類似結果/%Y%M%D%H的模式，以便每小時建立一個新子資料夾。 如果負載較小（例如，每天1000個檔案），則可以使用結果/%Y%M%D之類的模式。

* **failureFolderName（字串）**:保存故障檔案的資料夾。此位置一律與「已觀看」資料夾相對。 可以使用檔案模式，如「結果資料夾」中所述。 不會處理唯讀檔案，且會將其儲存在失敗資料夾中。 預設值為failure/%Y/%M/%D/。
* **preserveFolderName（字串）:** 成功處理後儲存檔案的位置。路徑可以是絕對、相對或空目錄路徑。 可以使用檔案模式，如「結果資料夾」中所述。 預設值為preserve/%Y/%M/%D/。
* **batchSize(Long)**:每次掃描要提取的檔案或資料夾數。用於防止系統過載；一次掃描太多檔案可能會造成當機。 預設值為 2。

   「民調問答間隔」和「批次大小」設定決定每個掃描中「監看資料夾」擷取的檔案數。 「監視資料夾」使用Quartz線程池掃描輸入資料夾。 線程池與其他服務共用。 如果掃描間隔較小，線程會經常掃描輸入資料夾。 如果檔案經常被拖放到「觀看的資料夾」中，則應將掃描間隔保持在較小。 如果檔案不常被刪除，請使用較大的掃描間隔，以便其他服務可以使用線程。

   如果要刪除的檔案量很大，請使批處理大小較大。 例如，如果「監看資料夾」端點啟動的服務每分鐘可處理700個檔案，且使用者以相同的速率將檔案拖放至輸入資料夾，則將「批次大小」設為350，「民調問答間隔」設為30秒，可協助「監看資料夾」執行，而不會造成太頻繁地掃描「監看資料夾」的成本。

   當檔案放入「觀看的資料夾」時，會列出輸入中的檔案，如果每秒都發生掃描，會降低效能。 增加掃描間隔可以提高效能。 如果要刪除的檔案量較小，請相應調整批大小和輪詢間隔。 例如，如果每秒丟棄10個檔案，請嘗試將pollInterval設定為1秒，將批次大小設定為10

* **throttleOn（布林值）**:選取此選項時，會限制AEM Forms在任何指定時間處理的「已觀看資料夾」作業數。作業的最大數量由批大小值確定。 預設值為true。 （請參閱[關於節流](../../forms/using/watched-folder-in-aem-forms.md#p-about-throttling-p)。）

* **overwriteDuplicateFilename（布林值）**:設為True時，會覆寫結果資料夾和保留資料夾中的檔案。設為False時，名稱使用帶有數值索引尾碼的檔案和資料夾。 預設值為False。
* **preserveOnFailure（布林值）**:如果無法對服務執行操作，則保留輸入檔案。預設值為true。
* **inputFilePattern（字串）**:指定「監視」資料夾的輸入檔案的模式。建立檔案的允許清單。
* **asynch（布林值）**:將調用類型標識為非同步或同步。預設值為true（非同步）。 檔案處理是一項耗用資源的任務，請將非同步標誌的值保持為true，以防止阻塞掃描作業的主線程。 在群集環境中，保持標幟為true對於在可用伺服器上處理的檔案進行負載平衡至關重要。 如果標幟為false，則掃描作業會嘗試在其自身線程內按順序對每個頂級檔案/資料夾執行處理。 若沒有特定原因（例如單一伺服器設定上以工作流程為基礎的處理），請勿將標幟設為false。

>[!NOTE]
>
>根據設計，工作流程為非同步。 即使您將值設為false，工作流程也會以非同步模式啟動。

* **已啟用（布林值）**:停用並啟動「已觀看」資料夾的掃描。設為true ，以開始掃描「已監視」資料夾。 預設值為true。
* **payloadMapperFilter:** 將資料夾設為監看資料夾時，會在監看資料夾內建立資料夾結構。該結構具有資料夾，用於提供輸入、接收輸出（結果）、為故障保存資料、為長期進程保留資料以及為各階段保存資料。 「已觀看」資料夾的資料夾結構可作為以Forms為中心的工作流程的裝載。 有效負載映射器可讓您定義使用「監看」資料夾進行輸入、輸出及處理之有效負載的結構。 例如，如果您使用預設映射器，它會將「監看資料夾」的內容與[payload]\input和[payload]\output資料夾對應。 提供兩種現成可用的裝載映射器實施。 如果您沒有[自訂實作](../../forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter)，請使用其中一個現成可用的實作：

   * **預設對應器：** 使用預設裝載對應器，將已監視資料夾的輸入和輸出內容保留在裝載中個別的輸入和輸出資料夾中。此外，在工作流的有效負載路徑中，使用[有效負載]/input/和[有效負載]/output路徑來檢索和保存內容。

   * **簡單檔案式裝載對應器：** 使用簡單檔案式裝載對應器，將輸入和輸出內容直接保留在裝載資料夾中。它不會建立任何額外的階層，例如預設映射器。

### 自訂設定參數 {#custom-configuration-parameters}

除了上述「監看資料夾」配置屬性外，您還可以指定自定義配置參數。 自訂參數會傳遞至檔案處理程式碼。 它可讓程式碼根據參數的值來變更其行為。 若要指定參數：

1. 登入CRXDE-Lite，並導覽至「監看資料夾」設定節點。
1. 新增屬性參數。&lt;property_name> 到「監視的資料夾」配置節點。屬性的類型只能是Boolean、Date、Decimal、Double、Long和String。 您可以指定單一和多值屬性。

>[!NOTE]
>
>如果屬性的資料類型為Double，請在此類屬性的值中指定小數點。 對於資料類型為Double且值中未指定小數點的所有屬性，類型將轉換為Long。

這些屬性會作為Map&lt;String, Object>類型的不可變映射傳遞至處理代碼。 處理程式碼可以是ECMAScript、工作流程或服務。 為屬性提供的值在對映中可作為索引鍵值配對使用。 索引鍵是屬性的名稱，值是屬性的值。 如需自訂設定參數的詳細資訊，請參閱下列影像：

![包含強制屬性的監看資料夾配置節點示例、一些可選屬性、一些配置參數](assets/custom-configuration-parameters.png)

包含強制屬性的監看資料夾配置節點示例、一些可選屬性、一些配置參數。

#### 工作流程的可變變數 {#mutable-variables-for-workflows}

您可以為以工作流程為基礎的檔案處理方法建立可變變數。 這些變數可做為資料在工作流程步驟之間流動的容器。 若要建立此類變數：

1. 登入CRXDE-Lite，並導覽至「監看資料夾」設定節點。

1. 新增屬性workflow.var。&lt;variable_name> 到「監視的資料夾」配置節點。

   屬性的類型只能是Boolean、Date、Decimal、Double、Long和String。 也支援多值屬性。 對於多值屬性，工作流步驟可用的值是指定類型的陣列。

   >[!NOTE]
   >
   >如果屬性的資料類型為Double，請在此類屬性的值中指定小數點。 對於資料類型為Double且值中未指定小數點的所有屬性，類型將轉換為Long。

>[!NOTE]
>
>JCR規範要求屬性的預設值。 預設值可用於工作流程的步驟以進行處理。 因此，請指定適當的預設值。

![custom-configuration-parameters2](assets/custom-configuration-parameters2.png)

## 處理檔案的各種方法 {#variousmethodsforprocessingfiles}

您可以啟動工作流、服務或指令碼，以處理文檔放在監視資料夾中。

### 使用服務處理受監視資料夾的檔案   {#using-a-service-to-process-files-of-a-watched-folder-nbsp}

服務是`com.adobe.aemfd.watchfolder.service.api.ContentProcessor`介面的自訂實作。 已透過OSGi註冊，並附上一些自訂屬性。 實作的自訂屬性使其獨一無二，有助於識別實作。

#### ContentProcessor介面的自定義實現 {#custom-implementation-of-the-contentprocessor-interface}

自訂實作接受處理內容（com.adobe.aemfd.watchfolder.service.api.ProcessorContext類型的物件）、從內容讀取輸入檔案和設定參數、處理輸入，並將輸出新增至
內容。 ProcessorContext具有以下API:

* **getWatchFolderId**:傳回已監看資料夾的ID。
* **getInputMap**:傳回地圖類型。地圖的鍵是輸入檔案的檔案名和包含檔案內容的文檔對象。 使用getinputMap API讀取輸入檔案。
* **getConfigParameters**:傳回不可變的Map類型地圖。地圖包含
監看資料夾的設定參數。

* **setResult**:ContentProcessor實施使用API將輸出文檔寫入結果資料夾。您可以為setResult API提供輸出檔案的名稱。 API可能會根據指定的輸出資料夾/檔案模式，選擇使用或忽略提供的檔案。 如果指定了資料夾模式，則輸出檔案的名稱如工作流中所述。 如果指定了檔案模式，則輸出檔案的名稱如檔案模式中所述。

例如，以下代碼是ContentProcessor介面的自定義實現，具有自定義foo=bar屬性。

```java
@Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
@Service(value = {OutputWriter.class, ContentProcessor.class})
@Property(name = "foo", value = "bar")
public class OutputWriter implements ContentProcessor {
```

在[配置監視資料夾](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p)時，如果將inputProcessorId屬性指定為(foo=bar)，將inputProcessorType屬性指定為Service，則上述服務（自定義實施）用於處理監視資料夾的輸入檔案。

以下範例也是ContentProcessor介面的自訂實作。 在該示例中，服務接受輸入檔案，將檔案複製到臨時位置，並返回帶有檔案內容的文檔對象。 文檔對象的內容將保存到結果資料夾。 結果資料夾的物理路徑配置在[Watched資料夾配置節點](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p)中。

```java
@Component(immediate = true)
@Service(value = ContentProcessor.class)
@Property(name = "serviceSelector", value = "testProcessor1")
public class TestContentProcessor1 implements ContentProcessor {
    @Override
    public void processInputs(ProcessorContext context) throws Exception {
        Map.Entry<String, Document> e = context.getInputMap().entrySet().iterator().next();
        File f = new File((String) context.getConfigParameters().get("tempDir"),
                context.getConfigParameters().get("outPrefix") + e.getKey());
        e.getValue().copyToFile(f);
        context.setResult(f.getName(), new Document(f, true));
    }
}
```

### 使用指令碼處理受監視資料夾的檔案 {#using-scripts-to-process-files-of-a-watched-folder}

指令碼是寫入到處理置於「觀看」資料夾中的檔案的ECMAScript投訴自訂程式碼。 指令碼以JCR節點表示。 除了標準ECMAScript變數（記錄、Sling等），指令碼還包含變數processorContext。 變數的類型為ProcessorContext。 ProcessorContext具有以下API:

* **getWatchFolderId**:傳回已監看資料夾的ID。
* **getInputMap**:傳回地圖類型。地圖的鍵是輸入檔案的檔案名和包含檔案內容的文檔對象。 使用getinputMap API讀取輸入檔案。
* **getConfigParameters**:傳回不可變的Map類型地圖。地圖包含監看資料夾的設定參數。
* **setResult**:ContentProcessor實施使用API將輸出文檔寫入結果資料夾。您可以為setResult API提供輸出檔案的名稱。 API可能會根據指定的輸出資料夾/檔案模式，選擇使用或忽略提供的檔案。 如果指定了資料夾模式，則輸出檔案的名稱如工作流中所述。 如果指定了檔案模式，則輸出檔案的名稱如檔案模式中所述。

以下程式碼是ECMAScript的範例。 它接受輸入檔案，將檔案複製到臨時位置，並返回帶有檔案內容的文檔對象。 文檔對象的內容將保存到結果資料夾。 結果資料夾的物理路徑配置在[Watched資料夾配置節點](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p)中。

>[!NOTE]
>
>輸出資料夾和檔案名稱首碼是根據Watched Folder設定參數決定。

```java
var inputMap = processorContext.getInputMap();
var params = processorContext.getConfigParameters();
var entry = inputMap.entrySet().iterator().next();
var tempFile = new Packages.java.io.File(params.get("tempDir"), params.get("outPrefix") + entry.getKey());
entry.getValue().copyToFile(tempFile);
processorContext.setResult(tempFile.getName(), new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true));
```

#### 指令碼的位置和安全考量 {#location-of-scripts-and-security-considerations}

依預設，會提供容器資料夾(/etc/fd/watchfolder/scripts)，客戶可放置其指令碼，且watch-folder架構使用的預設服務使用者具有從此位置讀取指令碼的必要權限。

如果您打算將指令碼放置在自訂位置，則預設服務使用者可能沒有自訂位置的讀取權限。 對於這種情況，請執行下列步驟以提供自訂位置的必要權限：

1. 以寫程式方式或通過控制台https://&#39;[server]:[port]&#39;/crx/explorer建立系統用戶。 您也可以使用現有的系統使用者。 請務必與這裡的系統使用者合作，而非與一般使用者合作。
1. 在儲存指令碼的自定義位置上，為新建立的或現有的系統用戶提供讀取權限。 您可以有多個自訂位置。 為所有自訂位置提供至少讀取權限。
1. 在Felix配置控制台(/system/console/configMgr)中，找到watch資料夾的服務用戶映射。 此對應類似「對應：adobe-aemds-core-watch-folder=...」
1. 按一下對應。 對於「adobe-aemds-core-watch-folder:scripts=fd-service」項目，將fd-service變更為自訂系統使用者的ID。 按一下「儲存」。

現在，您可以使用已設定的自訂位置來儲存指令碼。

### 使用工作流程處理受監視資料夾的檔案 {#using-a-workflow-to-process-files-of-a-watched-folder}

工作流程可讓您自動執行Experience Manager活動。 工作流程包含以特定順序執行的一系列步驟。 每個步驟都會執行不同的活動，例如啟動頁面或傳送電子郵件訊息。 工作流程可與存放庫、使用者帳戶和Experience Manager服務中的資產互動。 因此，工作流程可以協調複雜。

* 建立工作流程之前，請考慮下列幾點：
* 步驟的輸出必須可用於所有後續步驟。
這些步驟必須能夠更新（甚至刪除）前述步驟產生的現有輸出。
* 可變變數可用來在步驟之間流動自訂動態資料。

執行下列步驟以使用工作流程處理檔案：

1. 建立`com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextProcessor`介面的實作。 其類似於為服務建立的實作。

   >[!NOTE]
   >
   >您可以在ECMAScript中完全建立完整實作。

1. 在工作流程的步驟中，找到com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService類型的OSGi服務，並使用下列引數呼叫服務的execute()方法。

   * WorkflowContextProcessor介面的自定義實施
   * workItem
   * workflowSession
   * 中繼資料

如果您使用Java寫程式語言來實作工作流程，AEM工作流程引擎會為workItem、workflowSession和中繼資料變數提供值。 這些變數會作為引數傳遞至自訂WorkflowProcess實作的execute()方法。

如果您使用ECMAScript來實作工作流程，AEM工作流程引擎會為graniteWorkItem、graniteWorkflowSession和中繼資料變數提供值。 這些變數會以引數的形式傳遞至WorkflowContextService.execute()方法。

processWorkflowContext()的引數是類型com.adobe.aemfd.watchfolder.workflow.api.WorkflowContext的對象。 WorkflowContext介面有下列API，以方便執行上述工作流程特定考量事項：

* getWorkItem:返回WorkItem變數的值。 變數會傳遞至WorkflowContextService.execute()方法。
* getWorkflowSession:傳回WorkflowSession變數的值。 變數會傳遞至WorkflowContextService.execute()方法。
* getMetadata:傳回中繼資料變數的值。 變數會傳遞至WorkflowContextService.execute()方法。
* getCommittedVariables:傳回唯讀物件映射，代表先前步驟設定的變數。 如果在先前的任何步驟中未修改變數，則會傳回在設定「監看資料夾」期間指定的預設值。
* getCommittedResults:返回只讀文檔映射。 地圖代表由先前步驟產生的輸出檔案。
* setVariable:WorkflowContextProcessor實施使用變數來操控代表在步驟之間流動的自訂動態資料的變數。 變數的名稱和類型與在[設定「監看資料夾」](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)期間指定的變數名稱相同。 若要變更變數的值，請使用非空值呼叫setVariable API。 若要移除變數，請使用null值呼叫setVariable()。

也提供下列ProcessorContext API:

* getWatchFolderId:傳回已監看資料夾的ID。
* getInputMap:返回Map&lt;String, Document>類型的映射。 地圖的鍵是輸入檔案的檔案名和包含檔案內容的文檔對象。 使用getinputMap API讀取輸入檔案。
* getConfigParameters:傳回Map&lt;String, Object>類型的不可變映射。 地圖包含監看資料夾的設定參數。
* setResult:ContentProcessor實施使用API將輸出文檔寫入結果資料夾。 您可以為setResult API提供輸出檔案的名稱。 API可能會根據指定的輸出資料夾/檔案模式，選擇使用或忽略提供的檔案。 如果指定了資料夾模式，則輸出檔案的名稱如工作流中所述。 如果指定了檔案模式，則輸出檔案的名稱如檔案模式中所述

在工作流程中使用setResult API時的考量事項：

* 若要新增有助於整體工作流程輸出的新輸出檔案，請呼叫具有先前任何步驟未用作輸出檔案名稱的setResult API。
* 若要更新上一步驟產生的輸出，請使用上一步驟已使用的檔案名稱呼叫setResult API。
* 要刪除前一個步驟生成的輸出，請調用setResult，其檔案名已被前一個步驟使用，而空作為內容。

>[!NOTE]
>
>在任何其他案例中以null內容呼叫setResult API會導致錯誤。

以下範例是以工作流程步驟的形式實作。 在此範例中，ECMAscript使用變數stepCount來追蹤目前工作流程例項中呼叫步驟的次數。
輸出資料夾的名稱是當前步驟號、原始檔案名和outPrefix參數中指定的前置詞的組合。

ECMAScript獲取工作流上下文服務的參考，並建立WorkflowContextProcessor介面的實現。 WorkflowContextProcessor實施接受輸入檔案，將檔案複製到臨時位置，並返回表示複製檔案的文檔。 根據Boolean變數purgePrevious的值，當前步驟將刪除上次生成的輸出，該輸出與在當前工作流實例中啟動該步驟時的相同步驟相同。 最後，調用wfSvc.execute方法以執行WorkflowContextProcessor實施。 輸出文檔的內容將保存到結果資料夾，位於「監視資料夾」配置節點中提及的物理路徑。

```javascript
log.error("Watch-folder workflow script called for step: " + graniteWorkItem.getNode().getTitle());
var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
// Custom WorkflowContextProcessor implementation which defines the processWorkflowContext() method purely in JS
var impl = { processWorkflowContext: function (wfContext) {
    var wfId = wfContext.getWatchFolderId();
    var inputMap = wfContext.getInputMap();
    var paramMap = wfContext.getConfigParameters();
    var preResults = wfContext.getCommittedResults();
    var preVars = wfContext.getCommittedVariables();
    log.info("WF ID: " + wfId); // workflowId of type String
    log.info("Inputs: " + inputMap); // Input map of type Map<String, Document>
    log.info("Params: " + paramMap); // Config params of type Map<String, Object>
    log.info("Old results: " + preResults);
    log.info("Old variables: " + preVars);
    var currStepNumber = new Packages.java.lang.Long(new Packages.java.lang.Long(preVars.get("stepCount")).longValue() + 1);
    log.info("Current step number: " + currStepNumber);
    wfContext.setVariable("stepCount", currStepNumber);
    var entry = inputMap.entrySet().iterator().next();
    var tempFile = new Packages.java.io.File(paramMap.get("tempDir"), paramMap.get("outPrefix") + "STEP-" + currStepNumber + "-" + entry.getKey());
    entry.getValue().copyToFile(tempFile);
    var fName = tempFile.getName();
    var outDoc = new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true);
    wfContext.setResult(tempFile.getName(), outDoc);
    var prevStepOutName = paramMap.get("outPrefix") + "STEP-" + (currStepNumber - 1) + "-" + entry.getKey();
    if (preResults.containsKey(prevStepOutName) && paramMap.get("purgePrevious").booleanValue()) {
        log.info("Purging previous step output " + prevStepOutName);
        wfContext.setResult(prevStepOutName, null);
    }
} }
wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
log.info("Exiting workflow script!")
```

### 建立裝載對應器篩選器，將已監看資料夾的結構對應至工作流程的裝載 {#create-payload-mapper-filter-to-map-structure-of-a-watched-folder-to-the-payload-of-a-workflow}

建立已觀看的資料夾時，會在正在觀看的資料夾內建立資料夾結構。 資料夾結構具有階段、結果、保留、輸入和失敗資料夾。 資料夾結構可作為工作流的輸入裝載，並接受來自工作流的輸出。 它也可以列出故障點（如果有）。

如果裝載的結構與已觀看資料夾的結構不同，您可以撰寫自訂指令碼，將已觀看資料夾的結構對應至裝載。 這類指令碼稱為裝載映射器篩選器。 AEM Forms提供裝載對應器篩選器，可將已觀看資料夾的結構對應至裝載。

#### 建立自訂裝載對應器篩選器 {#creating-a-custom-payload-mapper-filter}

1. 下載[Adobe用戶端SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)。
1. 在Maven型專案的建置路徑中設定用戶端SDK。 若要開始，您可以下載並在所選IDE中開啟以下基於Maven的項目。
1. 編輯範例套件中可用的裝載對應器篩選程式程式碼，以符合您的需求。
1. 使用maven建立自訂裝載映射器篩選器的套件組合。
1. 使用[AEM套件組合控制台](https://localhost:4502/system/console/bundles)來安裝套件組合。

   現在，自訂裝載映射器篩選器會列在AEM Watched資料夾UI中。 您可以將其用於工作流程。

   下列范常式式碼會針對相對於裝載而儲存的檔案，實作簡單的檔案型對應程式。 您可以使用它開始使用。

   ```java
   package com.adobe.aemfd.watchfolder.workflow;
   import com.adobe.aemfd.docmanager.Document;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.PayloadMapper;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowExecutionContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowInitializationContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowVariable;
   import com.adobe.granite.workflow.exec.Workflow;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.ResourceResolver;
   import javax.jcr.Binary;
   import javax.jcr.Node;
   import java.util.Collection;
   import java.util.HashMap;
   import java.util.Map;
   @Component(immediate = true)
   @Service(value = PayloadMapper.class)
   public class SimpleFileBasedPayloadMapper implements PayloadMapper {
   @Override
   public Node createPayload(WorkflowInitializationContext wfInitCtxt, Node stagingFolder, String uniquePayloadName,
   Map<String, Binary> inputs, Collection<WorkflowVariable> variableDefs) throws Exception {
   Node dirNode = stagingFolder.addNode(uniquePayloadName, "sling:Folder");
   for (Map.Entry<String, Binary> bins: inputs.entrySet()) {
   Node fileNode = dirNode.addNode(bins.getKey(), "nt:file");
   Node resNode = fileNode.addNode ("jcr:content", "nt:resource");
   resNode.setProperty("jcr:data", bins.getValue());
   }
   return dirNode;
   }
   @Override
   public Map<String, Document> getInputs(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload, ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public void setOutput(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   String fileName, Binary contents, int outputMode) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getIntermediateOutputs(WorkflowInitializationContext wfInitCtxt,
   WorkflowExecutionContext wfExecCtxt, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getFinalOutputs(WorkflowInitializationContext wfInitCtxt, Workflow workflow, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   Map<String, Object> params = wfInitCtxt.getConfigParameters();
   Map<String, Document> result = new HashMap<String, Document>();
   for (Map.Entry<String, Object> me: params.entrySet()) {
   String key = me.getKey();
   if (key.startsWith("pm.outfile.")) {
   String fName = (String) me.getValue();
   Document d = new Document(payload.getPath() + "/" + fName, resourceResolver);
   result.put(fName, d);
   }
   }
   return result;
   }
   @Override
   public void setVariable(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   WorkflowVariable variable) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Object> getVariables(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   }
   ```

## 使用者與已觀看資料夾互動的方式 {#how-users-interact-with-a-watched-folder}

對於「觀看資料夾」端點，使用者可從案頭複製或拖曳輸入檔案或資料夾至「觀看資料夾」，以開始檔案處理作業。 檔案會依到達順序處理。

對於「觀看資料夾」端點，如果作業僅需要一個輸入檔案，則用戶可將該檔案複製到「觀看資料夾」的根目錄。

如果作業包含多個輸入檔案，則用戶必須在「監看資料夾」層次結構外建立一個資料夾，該層次結構包含所有必需檔案。 此新資料夾應包含輸入檔案（若處理程式需要，還可選擇使用DDX檔案）。 建立作業資料夾後，使用者會將其複製至「監看資料夾」的輸入資料夾。

>[!NOTE]
>
>請確定應用程式伺服器已刪除對「觀看資料夾」中檔案的存取權。 如果AEM Forms在掃描後無法從輸入資料夾中刪除檔案，則相關程式將無限期啟動。

## 有關已監視資料夾的其他資訊 {#additional-information-about-the-watched-folders}

### 關於節流 {#about-throttling}

為監看資料夾端點啟用限制時，它會限制在任何指定時間處理的監視資料夾作業數。 作業的最大數量由「批大小」值確定，也可在「監視資料夾」端點中配置。 達到限制限制時，不會輪詢「監視資料夾」輸入目錄中的傳入文檔。 該文檔還保留在輸入目錄中，直到完成其他「已監視資料夾」作業並進行另一輪輪詢嘗試。 對於同步處理，即使在單個線程中連續處理作業，在單個輪詢中處理的所有作業都將計入限制。

>[!NOTE]
>
>限制不會隨群集擴展。 啟用限制時，群集作為一個整體在任何給定時間處理的作業數都不超過批大小中指定的作業數。 此限制為群集範圍，不特定於群集中的每個節點。 例如，批大小為2時，單個節點處理兩個作業時可以達到限制限制，在完成其中一個作業之前，其他節點不會輪詢輸入目錄。

#### 節流如何運作 {#how-throttling-works}

Watched Folder在每個pollInterval掃描輸入資料夾，提取批大小中指定的檔案數，並為每個檔案調用目標服務。 例如，如果批大小為4，則在每次掃描時，「監看資料夾」會拾取4個檔案，建立4個調用請求，並調用目標服務。 在完成這些請求之前，如果調用了「監視的資料夾」，則無論前四個作業是否已完成，它都會再次啟動四個作業。

當前的作業未完成時，限制阻止「監視的資料夾」調用新作業。 「監看的資料夾」可偵測進行中的作業，並根據批次大小減去進行中的作業來處理新作業。 例如，在第二個調用中，如果已完成的作業數僅為三個，並且一個作業仍在進行中，則「監視的資料夾」僅調用另外三個作業。

* 「觀看的資料夾」依賴於階段資料夾中存在的檔案數，以找出正在進行的作業數。 如果檔案在階段資料夾中仍未處理，則「監看資料夾」不會調用任何更多作業。 例如，如果批處理大小為4個，且3個作業被停止，則「監視資料夾」在後續調用中只調用一個作業。 有多種情況會導致檔案在階段資料夾中保持未處理。 作業停止時，管理員可以終止「進程管理」頁上的進程，以便「監視的資料夾」將檔案移出舞台資料夾。
* 如果AEM Forms伺服器在「監視的資料夾」調用作業之前關閉，則管理員可以將檔案移出舞台資料夾。 有關資訊，請參閱[故障點和恢復](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p)。
* 如果AEM Forms伺服器正在運行，但當作業管理器服務回叫時（服務未按順序啟動時），監視資料夾未運行，則管理員可以將檔案移出舞台資料夾。 有關資訊，請參閱[故障點和恢復](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p)。

### 故障點和恢復故障點和恢復 {#failure-points-and-recoveryfailure-points-and-recovery}

在每個民調問答事件中，「觀看的資料夾」都會鎖定輸入資料夾、將符合包含檔案模式的檔案移動到階段資料夾，然後解鎖輸入資料夾。 需要鎖定，這樣兩個線程就不會提取同一組檔案並處理兩次。 發生此情況的機率會隨著小pollInterval和大批次大小而增加。 將檔案移到舞台資料夾後，輸入資料夾將解除鎖定，以便其他線程可以掃描資料夾。 此步驟有助於提供高吞吐量，因為其他線程可以在一個線程處理檔案時掃描。

將檔案移到階段資料夾後，會為每個檔案建立調用請求，並調用目標服務。 有時候，「監視的資料夾」無法恢復階段資料夾中的檔案：

* 如果伺服器在「監視的資料夾」可以建立調用請求之前關閉，則階段資料夾中的檔案將保留在階段資料夾中，並且無法恢復。

* 如果「監視的資料夾」已成功建立階段資料夾中每個檔案的調用請求，並且伺服器崩潰，則基於調用類型有兩種行為：

   * **同步**:如果「監看資料夾」配置為同步調用服務，則舞台資料夾中的所有檔案在舞台資料夾中都將保留為未處理。
   * **非同步**:在這種情況下，「觀看的資料夾」需仰賴「工作管理員」服務。如果作業管理器服務回叫「監看資料夾」，則階段資料夾中的檔案會根據調用的結果移動到「保留」或「失敗」資料夾。 如果作業管理器服務未回叫「已監看資料夾」，則檔案在預備資料夾中將保留未處理。 當工作管理員回呼時，「已監看資料夾」未執行時，就會發生此情況。

#### 恢復階段資料夾中未處理的源檔案 {#recover-unprocessed-source-files-in-the-stage-folder}

當「監看資料夾」無法處理階段資料夾中的源檔案時，您可以恢復未處理的檔案。

1. 重新啟動應用程式伺服器或節點。

1. 停止「觀看的資料夾」處理新的輸入檔案。 如果跳過此步驟，將更難以確定哪些檔案在舞台資料夾中未處理。 要阻止「監視的資料夾」處理新的輸入檔案，請執行以下任一操作：

   * 將「監看」資料夾的includeFilePattern屬性更改為與任何新輸入檔案不匹配的屬性（例如，輸入NOMATCH）。
   * 暫停建立新輸入檔案的過程。
   等到AEM Forms恢復並處理所有檔案。 大多數檔案應被恢復，任何新的輸入檔案都應被正確處理。 等待監看資料夾恢復和處理檔案的時間長度取決於要調用的操作長度和要恢復的檔案數。

1. 確定無法處理的檔案。 如果您等了適當的時間並完成了上一步，並且階段資料夾中仍有未處理的檔案，請轉到下一步。

   >[!NOTE]
   >
   >您可以查看階段目錄中檔案的日期和時間戳。 您可以根據檔案數和正常處理時間，判斷哪些檔案的存留時間夠久，足以被視為卡住。

1. 將未處理的檔案從階段目錄複製到輸入目錄。

1. 如果您在步驟2中阻止「監看的資料夾」處理新的輸入檔案，請將「包含檔案模式」更改為其上一個值，或重新啟用您禁用的進程。

### 將監看的資料夾連結在一起 {#chain-watched-folders-together}

監視資料夾可以連結在一起，以便一個監視資料夾的結果文檔是下一個監視資料夾的輸入文檔。 每個「已觀看資料夾」都可叫用不同的服務。 以此方式配置「監視的資料夾」，可以叫用多個服務。 例如，一個「觀看」資料夾可將PDF檔案轉換為Adobe PostScript®，另一個「觀看」資料夾可將PostScript檔案轉換為PDF/A格式。 要執行此操作，只需將第一個端點定義的「觀看資料夾」的結果資料夾設定為指向第二個端點定義的「觀看資料夾」的輸入資料夾。

第一次轉換的輸出將轉至\path\result。 第二次轉換的輸入為\path\result，第二次轉換的輸出將轉至\path\result\result （或您在第二次轉換的「結果資料夾」方塊中定義的目錄）。

### 檔案和資料夾模式 {#file-and-folder-patterns}

管理員可以指定可叫用服務的檔案類型。 可為每個「觀看的資料夾」建立多個檔案模式。 檔案模式可以是下列檔案屬性之一：

* 具有特定檔案名副檔名的檔案；例如*.dat、*.xml、.pdf、*。*
* 具有特定名稱的檔案；例如，資料。*
* 名稱和副檔名中包含複合運算式的檔案，如下列範例所示：

   * Data[0-9][0-9][0-9]。[dD][aA]&#39;port&#39;
   * *.[dD][Aa]&#39;port&#39;
   * *.[Xx][Mm][Ll]

* 管理員可以定義要儲存結果的輸出資料夾的檔案模式。 對於輸出資料夾（結果、保留和失敗），管理員可以指定以下任一檔案模式：
* %Y =年（已滿）
* %y =年（最後兩位）
* %M =月，
* %D =月中的第幾天，
* %d =年，
* %h =小時，
* %m =分鐘，
* %s =秒，
* %R = 0-9之間的隨機數
* %J =作業名稱

例如，結果資料夾的路徑可能是C:\Adobe\Adobe LiveCycle ES4\BarcodedForms\%y\%m\%d。

輸出參數映射也可以指定其他模式，例如：

* %F =源檔案名
* %E =源檔案名副檔名

如果輸出參數映射模式以「File.separator」（路徑分隔符）結尾，則會建立資料夾並將內容複製到該資料夾中。 如果模式的結尾不是「File.separator」，則會以該名稱建立內容（結果檔案或資料夾）。

## 將PDF產生器與監看資料夾搭配使用 {#using-pdf-generator-with-a-watched-folder}

您可以設定「監看資料夾」以起始工作流程、服務或指令碼以處理輸入檔案。 在下節中，我們將配置「監視資料夾」以啟動ECMAScript。 ECMAScript將使用PDF產生器，將Microsoft Word(.docx)檔案轉換為PDF檔案。

執行下列步驟以使用「PDF產生器」設定「監看資料夾」：

1. [建立ECMAScript](../../forms/using/watched-folder-in-aem-forms.md#p-create-an-ecmascript-p)
1. [建立工作流程](../../forms/using/watched-folder-in-aem-forms.md#p-create-a-workflow-p)
1. [配置「監視」資料夾](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)

### 建立ECMAScript {#create-an-ecmascript}

ECMAScript會使用PDF產生器的createPDF API，將Microsoft Word(.docx)檔案轉換為PDF檔案。 執行下列步驟以建立指令碼：

1. 在瀏覽器視窗中開啟CRXDE lite。 URL為https://&#39;[server]:[port]&#39;/crx/de。

1. 導覽至/etc/workflow/scripts並建立名為PDFG的資料夾。

1. 在PDFG資料夾中，建立名為pdfg-openOffice-sample.ecma的檔案，並將下列程式碼新增至檔案中：

   ```javascript
   var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
   // Custom ContentProcessor implementation which defines the processInputs() method purely in JS
   var impl = { processWorkflowContext: function (wrkfContext) {
   
     //  var logger = Packages.org.slf4j.LoggerFactory.getLogger("cmb-mergeandprint-sample.ecma");
                   var inputMap=wrkfContext.getInputMap();
   
                   var distiller = sling.getService(com.adobe.pdfg.service.api.DistillerService);
                   var generatePDF = sling.getService(com.adobe.pdfg.service.api.GeneratePDFService);
                   var pdfgConfig = sling.getService(com.adobe.pdfg.service.api.PDFGConfigService);
       var result = new Packages.java.util.HashMap();
       var entry = inputMap.entrySet().iterator().next();
       var pdfgOut = generatePDF.createPDF(entry.getValue(), ".docx", "Standard OpenOffice", "Standard", "No Security", null, null);
                   var convertedDoc = pdfgOut.get("ConvertedDoc");
   //   logger.info("SuccessFully saved the document to Ouput Node");
       wrkfContext.setResult(entry.getKey().substring(0, entry.getKey().lastIndexOf('.'))+".pdf",convertedDoc); // Ownership flag set to true for auto temp-file deletion.
   
   } }
   
   wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
   ```

1. 儲存並關閉檔案。

### 建立工作流程 {#create-a-workflow}

1. 在瀏覽器視窗中開啟AEM Workflow UI。
https://[伺服器名稱]:&#39;port&#39;/workflow

1. 在「模型」視圖中，按一下「**新建**」。 在「新建工作流」對話框中，指定&#x200B;**標題**，然後按一下&#x200B;**確定**。

   ![create-a-workflow-pdf](assets/create-a-workflow-pdf.png)

1. 選擇新建立的工作流，然後按一下「**編輯**」。 工作流程會在新視窗中開啟。

1. 刪除預設的工作流程步驟。 將「處理步驟」從Sidekick拖放至「工作流程」。

   ![create-a-workflow-pdf2](assets/create-a-workflow-pdf2.png)

1. 按一下右鍵「Process Step（處理步驟）」 ，然後選擇&#x200B;**Edit**。 此時將出現「步驟屬性」窗口。

1. 在「進程」(Process)頁簽中，選擇ECMAScript。 例如，在[建立ECMAScript](#p-create-an-ecmascript-p)中建立的pdfg-openOffice-sample.ecma指令碼。 啟用&#x200B;**Handler Advance**&#x200B;選項，然後按一下&#x200B;**OK**。

   ![create-a-workflow3-pdf](assets/create-a-workflow3-pdf.png)

### 配置「監視」資料夾 {#configure-the-watched-folder}

1. 在瀏覽器視窗中開啟CRXDE lite。 https://&#39;[server]:[port]&#39;/crx/de/

1. 導航到/etc/fd/watchfolder/config/資料夾，然後建立nt:unstructured類型的節點。

   ![configure-the-watched-folder-pdf](assets/configure-the-watched-folder-pdf.png)

1. 將下列屬性新增至節點：

   * folderPath（字串）:要以定義的時間間隔掃描的資料夾路徑。 該資料夾必須位於共用位置，所有伺服器都具有對該伺服器的完全訪問權限。
inputProcessorType（字串）:要啟動的進程類型。 在本教學課程中，指定工作流程。

   * inputProcessorId（字串）:inputProcessorId屬性的行為基於為inputProcessorType屬性指定的值。 在此示例中，inputProcessorType屬性的值為工作流。 因此，對於inputProcessorId屬性，請指定PDFG工作流的以下路徑：/etc/workflow/models/pdfg/jcr:content/model

   * outputFilePattern（字串）:輸出檔案的模式。 您可以指定資料夾或檔案模式。 如果指定了資料夾模式，則輸出檔案的名稱如工作流中所述。 如果指定了檔案模式，則輸出檔案的名稱如檔案模式中所述。
   除了上述的強制屬性外，「觀看的資料夾」也支援一些選用屬性。 如需選用屬性的完整清單和說明，請參閱[監看資料夾屬性](#watchedfolderproperties)。
