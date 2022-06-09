---
title: 在AEM Forms監視資料夾
seo-title: Watched folder in AEM Forms
description: 管理員可以將資料夾置於監視狀態，並在將檔案置於監視的資料夾中時啟動工作流、服務或指令碼操作。
seo-description: An administrator can put a folder on watch and start a workflow, service, or script operation when a file is placed in the folder being watched.
uuid: 39eac0fd-8212-46ff-b75d-8b4320d448a9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: db38972c-be3f-49fd-8cc1-45b16ed244af
docset: aem65
exl-id: fbf5c7c3-cb01-4fda-8e5d-11d56792d4bf
source-git-commit: 44f866e1435bd98f7dbe3f4ba8500830075db001
workflow-type: tm+mt
source-wordcount: '7149'
ht-degree: 0%

---

# 在AEM Forms監視資料夾{#watched-folder-in-aem-forms}

管理員可以配置網路資料夾（稱為監視資料夾），以便當用戶將檔案(如PDF檔案)放在監視資料夾中時，會啟動預先配置的工作流、服務或指令碼操作以處理添加的檔案。 在服務執行指定操作後，它將結果檔案保存在指定的輸出資料夾中。 有關工作流、服務和指令碼的詳細資訊，請參見 [處理檔案的各種方法](#variousmethodsforprocessingfiles)。

## 建立監視資料夾 {#create-a-watched-folder}

可以使用以下方法之一在檔案系統上建立「監視資料夾」：

* 配置「監視資料夾」配置節點的屬性時，在folderPath屬性中鍵入父目錄的完整路徑，並附加要建立的監視資料夾的名稱，如下例所示： `C:/MyPDFs/MyWatchedFolder`
的 
`MyWatchedFolder`資料夾不存在，AEM Forms嘗試在指定路徑上建立該資料夾。

* 在配置「監視資料夾」終結點之前，在檔案系統上建立資料夾，然後在folderPath屬性中提供完整路徑。 有關folderPath屬性的詳細資訊，請參見 [監視的資料夾屬性](#watchedfolderproperties)。

>[!NOTE]
>
>在群集環境中，用作監視資料夾的資料夾必須可訪問、可寫和在檔案系統或網路上共用。 群集的每個應用程式伺服器實例必須具有訪問同一共用資料夾的權限。 在Windows上，在所有伺服器上建立映射網路驅動器，並在folderPath屬性中指定映射網路驅動器的路徑。

## 建立「監視資料夾」配置節點 {#create-watched-folder-configuration-node}

要配置「監視資料夾」，請建立「監視資料夾」配置節點。 執行以下步驟建立配置節點：

1. 以管理員身份登錄到CRX-DE Lite，然後導航到/etc/fd/watchfolder/config資料夾。

1. 建立類型的節點 `nt:unstructured`。 例如，監視資料夾

   >[!NOTE]
   >
   >「監視資料夾」節點名稱不能包含空格和特殊字元。

1. 將以下屬性添加到節點：

   * `folderPath`
   * `inputProcessorType`
   * `inputProcessorId`
   * `outputFilePattern`

   有關受支援屬性的完整清單，請參見 [監視的資料夾屬性](#watchedfolderproperties)。

1. 按一下 **全部保存**。 建立節點並保存屬性後。 的 `input`。 `result`。 `failure`。 `preserve`, `stage`資料夾是在 `folderPath` 屬性。

   掃描作業將以定義的時間間隔開始掃描監視資料夾。

## 監視的資料夾屬性 {#watchedfolderproperties}

可以為「監視資料夾」配置以下屬性。

* **folderPath（字串）**:要按定義的時間間隔掃描的資料夾的路徑。 對於群集環境，資料夾必須位於對伺服器具有完全訪問權限的所有伺服器的共用位置。 這是強制屬性。
* **inputProcessorType（字串）**:要啟動的進程的類型。 可以指定工作流、指令碼或服務。 這是強制屬性。
* **inputProcessorId（字串）**:inputProcessorId屬性的行為基於為inputProcessorType屬性指定的值。 這是強制屬性。 以下清單詳細列出了inputProcessorType屬性的所有可能值以及inputProcessorType屬性的相應必需項：

   * 對於工作流，指定要執行的工作流模型。 例如，/etc/workflow/models/&lt;workflow_name>/jcr：內容/模型
   * 對於指令碼，指定要執行的指令碼的JCR路徑。 例如，/etc/fd/watchfolder/test/testScript.ecma
   * 對於服務，指定用於查找OSGi服務的篩選器。 該服務註冊為com.adobe.aemfd.watchfolder.service.api.ContentProcessor Interface的實現。

* **runModes（字串）**:以逗號分隔的允許工作流執行運行模式的清單。 以下幾個例子：

   * 作者

   * 發佈

   * author,publish

   * 發佈，作者

>[!NOTE]
>
>如果承載監視資料夾的伺服器沒有任何指定的運行模式，則無論伺服器上的運行模式如何，監視資料夾都始終激活。

* **outputFilePattern（字串）**:輸出檔案的模式。 可以指定資料夾或檔案模式。 如果指定了資料夾模式，則輸出檔案的名稱將如工作流中所述。 如果指定了檔案模式，則輸出檔案的名稱如檔案模式中所述。 [檔案和資料夾模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) 也可以為輸出檔案指定目錄結構。 這是強制屬性。

* **stageFileExpirationDuration（長，預設–1）**:等待的秒數，應將已被拾取用於處理的輸入檔案/資料夾視為已超時並標籤為失敗。 僅當此屬性的值為正數時，才激活此過期機制。

>[!NOTE]
>
>即使當使用此機制將輸入標籤為已超時時，它仍可能在後台處理，但只是需要比預期的時間多。 如果輸入內容在超時機制啟動之前已被使用，則處理可能會在以後繼續完成，並將輸出轉儲到結果資料夾中。 如果在超時之前未使用內容，則稍後在嘗試使用內容時，處理很可能會出錯，並且此錯誤也將記錄在失敗資料夾中，用於同一輸入。 另一方面，如果由於間歇性作業/工作流失火而未激活輸入的處理（這是到期機制要解決的情形），則當然這兩種情況都不會發生。 因此，對於因超時而標籤為失敗的失敗資料夾中的任何條目(查找「長時間後未處理檔案，標籤為失敗！」格式的消息。 在失敗日誌中)，建議掃描結果資料夾（以及失敗資料夾本身以查找相同輸入的其他條目），以檢查是否確實發生了以前描述的任何意外情況。

* **deleteExpiredStageFileOnlyWhenThrotled（布爾值，預設為true）:** 是否僅在監視資料夾被限制時才激活過期機制。 該機制對於限制的監視資料夾更相關，因為在未處理狀態（由於間歇性作業/工作流失火）中徘徊的少量檔案在啟用限制時有可能阻塞整個批的處理。 如果此屬性保持為true（預設），則過期機制將不會為未限制的監視資料夾激活。 如果該屬性保持為false，則只要stageFileExpirationDuration屬性為正數，機制將始終激活。

* **pollInterval（長）**:掃描監視資料夾以進行輸入的間隔（秒）。 除非啟用「限制」設定，否則輪詢間隔應長於處理平均作業的時間；否則，系統可能會過載。 預設值為 5。有關其它資訊，請參閱批大小的說明。 輪詢間隔的值必須大於或等於1。
* **excludeFilePattern（字串）**:用分號(;)分隔的模式清單，「受監視資料夾」用於確定要掃描和拾取的檔案和資料夾。 不掃描任何具有此模式的檔案或資料夾進行處理。 當輸入是包含多個檔案的資料夾時，此設定非常有用。 可以將資料夾的內容複製到一個名稱由「監視資料夾」選取的資料夾中。 這將防止「監視資料夾」在將資料夾完全複製到輸入資料夾之前提取要處理的資料夾。 預設值為null。
您可以使用 [檔案模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) 要排除：

   * 具有特定檔案副檔名的檔案；比如說， &#42;.dat, &#42;.xml, .pdf, &#42;。&#42;
   * 具有特定名稱的檔案；例如，資料&#42; 將排除名為data1、data2等的檔案和資料夾。
   * 名稱和副檔名中包含複合表達式的檔案，如下例所示：

      * 資料[0-9][0-9][0-9]。[dD][aA]「port」
      * &#42;。[dD][Aa]「port」
      * &#42;。[Xx][毫米][Ll]

有關檔案模式的詳細資訊，請參見 [關於檔案模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)。

* **includeFilePattern（字串）**:用分號(;)分隔的模式清單，「監視資料夾」用於確定要掃描和拾取的資料夾和檔案。 例如，如果輸入IncludeFilePattern&#42;，所有與輸入匹配的檔案和資料夾&#42; 被選中。 這包括名為input1、input2等的檔案和資料夾。 預設值為 &#42; 並指示所有檔案和資料夾。 可以使用檔案模式包括：

   * 具有特定檔案副檔名的檔案；比如說， &#42;.dat, &#42;.xml, .pdf, &#42;。&#42;
   * 具有特定名稱的檔案；例如，資料。&#42; 將包括名為data1、data2等的檔案和資料夾。

* 名稱和副檔名中包含複合表達式的檔案，如下例所示：

   * 資料[0-9][0-9][0-9]。[dD][aA]「port」

      * &#42;。[dD][Aa]「port」
      * &#42;。[Xx][毫米][Ll]

有關檔案模式的詳細資訊，請參見 [關於檔案模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)

* **waitTime（長）**:建立資料夾或檔案後掃描檔案之前等待的時間（毫秒）。 例如，如果等待時間為3,600,000毫秒（一小時），且檔案是在一分鐘前建立的，則該檔案將在59分鐘或更長時間後被拾取。 預設值為 0。此設定對於確保將檔案或資料夾完全複製到輸入資料夾非常有用。 例如，如果要處理一個大檔案，而該檔案需要10分鐘才能下載，則將等待時間設定為10&#42;60 &#42;1000毫秒。 如果檔案未保存10分鐘，則禁止「監視資料夾」掃描該檔案。
* **purgeDuration（長）**:結果資料夾中的檔案和資料夾在早於此值時被清除。 此值以天計。 此設定在確保結果資料夾未滿時非常有用。 值為–1天表示從不刪除結果資料夾。 預設值為–1。
* **resultFolderName（字串）**:儲存保存結果的資料夾。 如果結果未顯示在此資料夾中，請檢查失敗資料夾。 不處理只讀檔案並將其保存在故障資料夾中。 此值可以是具有以下檔案模式的絕對路徑或相對路徑：

   * %F =檔案名前置詞
   * %E =檔案副檔名
   * %Y =年（滿）
   * %y =年（最後兩位）
   * %M =月
   * %D =每月的某天
   * %d =一年中的某天
   * %H =小時（24小時制）
   * %h =小時（12小時制）
   * %m =分鐘
   * %s =秒
   * %l =毫秒
   * %R =隨機數（介於0和9之間）
   * %P =進程或作業ID

   例如，如果2009年7月17日晚上8點，並且您指定C:/Test/WF0/failure/%Y/%M/%D/%H/，則結果資料夾為C:/Test/WF0/failure/2009/07/17/20

   如果路徑不是絕對的，而是相對的，則會在「監視資料夾」內建立該資料夾。 預設值為result/%Y/%M/%D/，它是「監視」資料夾內的「結果」資料夾。 有關檔案模式的詳細資訊，請參見 [關於檔案模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)。

>[!NOTE]
>
>結果資料夾的大小越小，「受監視資料夾」的效能就越好。 例如，如果監視資料夾的估計負載是每小時1000個檔案，請嘗試類似結果/%Y%M%D%H的模式，以便每小時建立新的子資料夾。 如果負載較小（例如，每天1000個檔案），則可以使用類似結果/%Y%M%D的模式。

* **failureFolderName（字串）**:保存故障檔案的資料夾。 此位置始終相對於監視資料夾。 可以使用檔案模式，如「結果資料夾」中所述。 不處理只讀檔案並將其保存在故障資料夾中。 預設值為failure/%Y/%M/%D/。
* **preserveFolderName（字串）:** 成功處理後儲存檔案的位置。 路徑可以是絕對路徑、相對路徑或空目錄路徑。 可以使用檔案模式，如「結果資料夾」中所述。 預設值為preserve/%Y/%M/%D/。
* **batchSize（長）**:每次掃描要拾取的檔案或資料夾數。 用於防止系統過載；一次掃描過多檔案可能會導致崩潰。 預設值為 2。

   「輪詢間隔」和「批處理大小」設定確定每個掃描中「監視資料夾」拾取的檔案數。 監視資料夾使用Quartz線程池掃描輸入資料夾。 線程池與其他服務共用。 如果掃描間隔較小，則線程會經常掃描輸入資料夾。 如果檔案經常被放入「監視資料夾」中，則應保持掃描間隔較小。 如果檔案不常被刪除，請使用更大的掃描間隔，以便其他服務可以使用線程。

   如果正在刪除大量檔案，請使批大小變大。 例如，如果受監視資料夾終結點啟動的服務每分鐘可處理700個檔案，並且用戶以相同的速率將檔案放入輸入資料夾中，則將「批處理大小」設定為350，將「輪詢間隔」設定為30秒，幫助受監視資料夾效能，而不會導致過多掃描受監視資料夾的成本。

   將檔案拖放到「監視資料夾」中時，它會列出輸入中的檔案，如果每秒都進行掃描，則會降低效能。 增加掃描間隔可以改善效能。 如果要刪除的檔案數量較小，請相應調整「批大小」和「輪詢間隔」。 例如，如果每秒丟棄10個檔案，請嘗試將pollInterval設定為1秒，將批大小設定為10

* **throttleOn（布爾值）**:選擇此選項後，它將限制AEM Forms在任何給定時間處理的監視資料夾作業的數量。 最大作業數由「批大小」值確定。 預設值為true。 (請參閱 [關於限制](../../forms/using/watched-folder-in-aem-forms.md#p-about-throttling-p)。)

* **overwriteDuplicateFilename（布爾型）**:設定為True時，結果資料夾和保留資料夾中的檔案將被覆蓋。 如果設定為False，則名稱將使用帶數字索引尾碼的檔案和資料夾。 預設值為False。
* **preserveOnFailure（布爾型）**:在無法對服務執行操作時保留輸入檔案。 預設值為true。
* **inputFilePattern（字串）**:指定受監視資料夾的輸入檔案的模式。 建立檔案的允許清單。
* **非同步（布爾型）**:將調用類型標識為非同步或同步。 預設值為true（非同步）。 檔案處理是一項消耗資源的任務，將非同步標誌的值保持為true，以防止阻塞掃描作業的主線程。 在群集環境中，保持標誌為true對於在可用伺服器上處理的檔案啟用負載平衡至關重要。 如果該標誌為false，則掃描作業嘗試在其自己的線程內按順序對每個頂級檔案/資料夾執行處理。 不要在沒有特定原因的情況下將標誌設定為false，例如，在單伺服器設定上基於工作流的處理。

>[!NOTE]
>
>根據設計，工作流是非同步的。 即使將值設定為false，工作流也會以非同步模式啟動。

* **已啟用（布爾型）**:停用並激活監視資料夾的掃描。 設定為「已啟用」，開始掃描「監視資料夾」。 預設值為true。
* **payloadMapperFilter:** 將資料夾配置為監視資料夾時，會在監視資料夾中建立資料夾結構。 該結構具有資料夾，用於提供輸入、接收輸出（結果）、為故障保存資料、為長壽命進程保留資料以及為不同階段保存資料。 監視資料夾的資料夾結構可以用作以Forms為中心的工作流的負載。 負載映射器允許您定義使用「監視資料夾」進行輸入、輸出和處理的負載結構。 例如，如果使用預設映射器，它將監視資料夾的內容與 [負載]\輸入和 [負載]\output資料夾。 有兩個現成的負載映射器實現。 如果你沒有 [自定義實現](../../forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter)，使用一個現成實現：

   * **預設映射器：** 使用預設負載映射器將受監視資料夾的輸入和輸出內容保留在負載中單獨的輸入和輸出資料夾中。 此外，在工作流的負載路徑中，使用 [負載]/input/和 [負載]/output路徑以檢索和保存內容。

   * **基於檔案的簡單負載映射器：** 使用基於簡單檔案的負載映射器將輸入和輸出內容直接保留在負載資料夾中。 它不會建立任何額外的層次結構，如預設映射器。

### 自定義配置參數 {#custom-configuration-parameters}

除了上面列出的「監視資料夾」配置屬性外，您還可以指定自定義配置參數。 自定義參數將傳遞給檔案處理代碼。 它使代碼能夠根據參數值更改其行為。 要指定參數：

1. 登錄到CRXDE-Lite並導航到「監視資料夾」配置節點。
1. 添加屬性參數。&lt;property_name> 到「監視資料夾」配置節點。 屬性的類型只能是Boolean、Date、Decimal、Double、Long和String。 可以指定單值和多值屬性。

>[!NOTE]
>
>如果屬性的資料類型為Double，則在此類屬性的值中指定小數點。 對於所有屬性，其中資料類型為Double且在值中未指定小數點，類型將轉換為Long。

這些屬性作為Map類型的不可變映射傳遞&lt;string object=&quot;&quot;> 到處理代碼。 處理代碼可以是ECMAScript、Workflow或Service。 為屬性提供的值在映射中可用作鍵值對。 Key是屬性的名稱，value是屬性的值。 有關自定義配置參數的詳細資訊，請參閱以下影像：

![包含強制屬性、幾個可選屬性、幾個配置參數的監視資料夾配置節點示例](assets/custom-configuration-parameters.png)

包含強制屬性、幾個可選屬性、幾個配置參數的示例watch-folder配置節點。

#### 工作流程的可變變數 {#mutable-variables-for-workflows}

可以為基於工作流的檔案處理方法建立可變變數。 這些變數用作工作流步驟之間流動資料的容器。 要建立此類變數：

1. 登錄到CRXDE-Lite並導航到「監視資料夾」配置節點。

1. 添加屬性workflow.var。&lt;variable_name> 到「監視資料夾」配置節點。

   屬性的類型只能是Boolean、Date、Decimal、Double、Long和String。 還支援多值屬性。 對於多值屬性，工作流步驟的可用值是指定類型的陣列。

   >[!NOTE]
   >
   >如果屬性的資料類型為Double，則在此類屬性的值中指定小數點。 對於所有屬性，其中資料類型為Double且在值中未指定小數點，類型將轉換為Long。

>[!NOTE]
>
>JCR規範要求屬性的預設值。 預設值可用於工作流的步驟進行處理。 因此，請指定正確的預設值。

![自定義配置參數2](assets/custom-configuration-parameters2.png)

## 處理檔案的各種方法 {#variousmethodsforprocessingfiles}

您可以啟動工作流、服務或指令碼來處理監視資料夾中的文檔位置。

### 使用服務處理受監視資料夾的檔案   {#using-a-service-to-process-files-of-a-watched-folder-nbsp}

服務是 `com.adobe.aemfd.watchfolder.service.api.ContentProcessor` 。 它已與OSGi一起註冊，並附帶一些自定義屬性。 實現的自定義屬性使其獨一無二，並有助於確定實現。

#### ContentProcessor介面的自定義實現 {#custom-implementation-of-the-contentprocessor-interface}

自定義實現接受處理上下文（com.adobe.aemfd.watchfolder.service.api.ProcessorContext類型的對象），從上下文中讀取輸入文檔和配置參數，處理輸入，並將輸出添加回上下文。 ProcessorContext具有以下API:

* **getWatchFolderId**:返回「監視資料夾」的ID。
* **getInputMap**:返回映射類型的映射。 映射的鍵是輸入檔案的檔案名和包含檔案內容的文檔對象。 使用getinputMap API讀取輸入檔案。
* **getConfigParameters**:返回類型為「映射」的不可變映射。 映射包含受監視資料夾的配置參數。

* **setResult**:ContentProcessor實現使用API將輸出文檔寫入結果資料夾。 可以為setResult API提供輸出檔案的名稱。 API可能會根據指定的輸出資料夾/檔案模式選擇使用或忽略提供的檔案。 如果指定了資料夾模式，則輸出檔案的名稱將如工作流中所述。 如果指定了檔案模式，則輸出檔案的名稱如檔案模式中所述。

例如，以下代碼是具有custom foo=bar屬性的ContentProcessor介面的自定義實現。

```java
@Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
@Service(value = {OutputWriter.class, ContentProcessor.class})
@Property(name = "foo", value = "bar")
public class OutputWriter implements ContentProcessor {
```

同時 [配置監視資料夾](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p)，如果將inputProcessorId屬性指定為(foo=bar)，將inputProcessorType屬性指定為Service，則上述服務（自定義實現）將用於處理受監視資料夾的輸入檔案。

以下示例還是ContentProcessor介面的自定義實現。 在示例中，服務接受輸入檔案，將檔案複製到臨時位置，並返回包含檔案內容的文檔對象。 文檔對象的內容將保存到結果資料夾。 結果資料夾的物理路徑在 [「監視資料夾」配置節點](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p)。

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

指令碼是ECMAScript投訴自定義代碼，它寫入到處理放置在「監視資料夾」中的文檔。 指令碼表示為JCR節點。 除了標準ECMAScript變數（日誌、sling等）之外，指令碼還具有變數processorContext。 變數的類型為ProcessorContext。 ProcessorContext具有以下API:

* **getWatchFolderId**:返回「監視資料夾」的ID。
* **getInputMap**:返回映射類型的映射。 映射的鍵是輸入檔案的檔案名和包含檔案內容的文檔對象。 使用getinputMap API讀取輸入檔案。
* **getConfigParameters**:返回類型為「映射」的不可變映射。 映射包含受監視資料夾的配置參數。
* **setResult**:ContentProcessor實現使用API將輸出文檔寫入結果資料夾。 可以為setResult API提供輸出檔案的名稱。 API可能會根據指定的輸出資料夾/檔案模式選擇使用或忽略提供的檔案。 如果指定了資料夾模式，則輸出檔案的名稱將如工作流中所述。 如果指定了檔案模式，則輸出檔案的名稱如檔案模式中所述。

以下代碼是ECMAScript示例。 它接受輸入檔案，將檔案複製到臨時位置，並返回包含檔案內容的文檔對象。 文檔對象的內容將保存到結果資料夾。 結果資料夾的物理路徑在 [「監視資料夾」配置節點](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p)。

>[!NOTE]
>
>輸出資料夾和檔案名前置詞是根據「監視資料夾」配置參數決定的。

```java
var inputMap = processorContext.getInputMap();
var params = processorContext.getConfigParameters();
var entry = inputMap.entrySet().iterator().next();
var tempFile = new Packages.java.io.File(params.get("tempDir"), params.get("outPrefix") + entry.getKey());
entry.getValue().copyToFile(tempFile);
processorContext.setResult(tempFile.getName(), new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true));
```

#### 指令碼的位置和安全注意事項 {#location-of-scripts-and-security-considerations}

預設情況下，提供容器資料夾(/etc/fd/watchfolder/scripts)，客戶可以放置其指令碼，而watch-folder框架使用的預設service-user具有從此位置讀取指令碼的必要權限。

如果您計畫將指令碼放置在自定義位置，則預設服務用戶可能沒有對自定義位置的讀取權限。 對於此類情形，請執行以下步驟來為自定義位置提供必要的權限：

1. 以寫程式方式或通過控制台https://&#39;建立系統用戶[伺服器]:[埠]「/crx/explorer。 您也可以使用現有系統用戶。 與這裡的系統用戶而不是普通用戶一起工作非常重要。
1. 為新建立或現有系統用戶提供對儲存指令碼的自定義位置的讀取權限。 您可以有多個自定義位置。 至少為所有自定義位置提供讀取權限。
1. 在Felix配置控制台(/system/console/configMgr)中，找到監視資料夾的服務用戶映射。 此映射類似於「映射：adobe-aems-core-watch-folder=...」
1. 按一下映射。 對於「adobe-aemds-core-watch-folder:scripts=fd-service」項，請將fd-service更改為自定義系統用戶的ID。 按一下「儲存」。

現在，您可以使用配置的自定義位置來保存指令碼。

### 使用工作流處理受監視資料夾的檔案 {#using-a-workflow-to-process-files-of-a-watched-folder}

工作流使您能夠自動執行Experience Manager活動。 工作流由一系列按特定順序執行的步驟組成。 每個步驟都執行不同的活動，如激活頁面或發送電子郵件。 工作流可以與儲存庫、用戶帳戶和Experience Manager服務中的資產交互。 因此，工作流可以協調複雜的工作。

* 在建立工作流之前，請考慮以下幾點：
* 步驟的輸出必須可用於所有後續步驟。
這些步驟必須能夠更新（甚至刪除）前面步驟生成的現有輸出。
* 可變變數用於在步驟之間流動自定義動態資料。

執行以下步驟以使用工作流處理檔案：

1. 建立 `com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextProcessor` 。 它類似於為服務建立的實現。

   >[!NOTE]
   >
   >可以在ECMAScript中完全建立完整的實現。

1. 在工作流的步驟中，找到com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService類型的OSGi服務，並使用以下參數調用該服務的execute()方法。

   * 您對WorkflowContextProcessor介面的自定義實現
   * 工作項
   * 工作流會話
   * 中繼資料

如果使用Java寫程式語言來實現工作流，則AEM工作流引擎會為workItem、workflowSession和元資料變數提供值。 這些變數作為參數傳遞給自定義WorkflowProcess實現的execute()方法。

如果使用ECMAScript來實現工作流，則AEM工作流引擎會為graniteWorkItem、graniteWorkflowSession和元資料變數提供值。 這些變數作為參數傳遞給WorkflowContextService.execute()方法。

processWorkflowContext()的參數是com.adobe.aemfd.watchfolder.workflow.api.WorkflowContext類型的對象。 WorkflowContext介面具有以下API，可方便執行上述特定於工作流的注意事項：

* getWorkItem:返回WorkItem變數的值。 變數將傳遞給WorkflowContextService.execute()方法。
* getWorkflowSession:返回WorkflowSession變數的值。 變數將傳遞給WorkflowContextService.execute()方法。
* getMetadata:返回元資料變數的值…… 變數將傳遞給WorkflowContextService.execute()方法。
* getCommittedVariables:返回表示由前面步驟設定的變數的只讀對象映射。 如果在前面的任何步驟中未修改變數，則返回配置「監視資料夾」期間指定的預設值。
* getCommittedResults:返回只讀文檔映射。 映射表示由前面的步驟生成的輸出檔案。
* setVariable:WorkflowContextProcessor實現使用變數來處理表示在步驟之間流動的自定義動態資料的變數。 變數的名稱和類型與在 [配置監視資料夾](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)。 要更改變數的值，請使用非空值調用setVariable API。 要刪除變數，請使用空值調用setVariable()。

還提供以下ProcessorContext API:

* getWatchFolderId:返回「監視資料夾」的ID。
* getInputMap:返回映射類型的映射&lt;string document=&quot;&quot;>。 映射的鍵是輸入檔案的檔案名和包含檔案內容的文檔對象。 使用getinputMap API讀取輸入檔案。
* getConfigParameters:返回類型為「映射」的不可變映射&lt;string object=&quot;&quot;>。 映射包含受監視資料夾的配置參數。
* setResult:ContentProcessor實現使用API將輸出文檔寫入結果資料夾。 可以為setResult API提供輸出檔案的名稱。 API可能會根據指定的輸出資料夾/檔案模式選擇使用或忽略提供的檔案。 如果指定了資料夾模式，則輸出檔案的名稱將如工作流中所述。 如果指定了檔案模式，則輸出檔案的名稱如檔案模式中所述

在工作流中使用setResult API時的考慮：

* 要添加有助於整個工作流輸出的新輸出文檔，請調用setResult API，該檔案名在前面任何步驟中都未用作輸出檔案名。
* 要更新由上一步生成的輸出，請調用setResult API，該API的檔案名已由上一步使用。
* 要刪除由上一步生成的輸出，請調用setResult，其檔案名已被上一步使用，而空值作為內容。

>[!NOTE]
>
>在任何其他方案中調用包含空內容的setResult API將導致錯誤。

以下示例作為工作流步驟實現。 在示例中，ECMAscript使用變數stepCount跟蹤在當前工作流實例中調用步驟的次數。
輸出資料夾的名稱是當前步驟號、原始檔案名和在outPrefix參數中指定的前置詞的組合。

ECMAScript獲取工作流上下文服務的引用並建立WorkflowContextProcessor介面的實現。 WorkflowContextProcessor實現接受輸入檔案，將檔案複製到臨時位置，並返回表示複製檔案的文檔。 根據布爾變數purgePrevious的值，當前步驟將刪除上次在當前工作流實例中啟動該步驟時由同一步驟生成的輸出。 最後，調用wfSvc.execute方法執行WorkflowContextProcessor實現。 輸出文檔的內容將保存到結果資料夾中「監視資料夾」配置節點中提到的物理路徑。

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

### 建立負載映射器篩選器以將受監視資料夾的結構映射到工作流的負載 {#create-payload-mapper-filter-to-map-structure-of-a-watched-folder-to-the-payload-of-a-workflow}

建立受監視資料夾時，它會在正被監視的資料夾中建立資料夾結構。 資料夾結構具有階段、結果、保留、輸入和失敗資料夾。 該資料夾結構可以用作工作流的輸入負載並接受來自工作流的輸出。 它還可列出故障點（如果有）。

如果負載的結構與監視資料夾的結構不同，則可以編寫自定義指令碼以將監視資料夾的結構映射到負載。 這種指令碼稱為負載映射器篩選器。 現成，AEM Forms提供了一個負載映射器過濾器，將受監視資料夾的結構映射到負載。

#### 建立自定義負載映射器篩選器 {#creating-a-custom-payload-mapper-filter}

1. 下載 [Adobe客戶端SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)。
1. 在基於Maven的項目的生成路徑中設定客戶端SDK。 要開始，可以下載並開啟所選IDE中的以下基於Maven的項目。
1. 編輯示例包中可用的負載映射器篩選器代碼，以滿足您的要求。
1. 使用maven建立自定義負載映射器篩選器的捆綁包。
1. 使用 [捆綁式控制台](https://localhost:4502/system/console/bundles) 安裝包。

   現在，自定義負載映射器篩選器已列AEM在監視資料夾UI中。 您可以將其與工作流一起使用。

   以下示例代碼為相對於負載保存的檔案實現了一個基於檔案的簡單映射器。 你可以用它開始。

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

## 用戶如何與受監視資料夾交互 {#how-users-interact-with-a-watched-folder}

對於受監視資料夾終結點，用戶可以通過將輸入檔案或資料夾從案頭複製或拖動到受監視資料夾來啟動檔案處理操作。 檔案按到達順序處理。

對於受監視資料夾終結點，如果作業只需要一個輸入檔案，則用戶可以將該檔案複製到受監視資料夾的根目錄。

如果作業包含多個輸入檔案，則用戶必須在「監視資料夾」層次結構外建立一個包含所有必需檔案的資料夾。 此新資料夾應包括輸入檔案（如果進程需要，還可選擇包含DDX檔案）。 構建作業資料夾後，用戶將其複製到「監視資料夾」的輸入資料夾中。

>[!NOTE]
>
>確保應用伺服器已刪除對監視資料夾中檔案的訪問權限。 如果AEM Forms在掃描後無法從輸入資料夾中刪除這些檔案，則關聯進程將無限期地啟動。

## 有關受監視資料夾的其他資訊 {#additional-information-about-the-watched-folders}

### 關於限制 {#about-throttling}

為監視資料夾終結點啟用限制時，它會限制在任何給定時間處理的監視資料夾作業的數量。 最大作業數由批大小值確定，該值也可在「監視資料夾」終結點中配置。 達到限制限制時，不會輪詢「監視資料夾」輸入目錄中的傳入文檔。 在完成其他「已監視資料夾」作業並進行另一輪輪詢嘗試之前，文檔還會保留在輸入目錄中。 對於同步處理，在單個輪詢中處理的所有作業都被計算到限制限制，即使這些作業在單個線程中連續處理。

>[!NOTE]
>
>限制不隨群集擴展。 啟用限制後，集群作為一個整體將不會處理超過「批大小」中在任何給定時間指定的作業數。 此限制是群集範圍的，不特定於群集中的每個節點。 例如，如果批大小為2，則單個節點處理兩個作業時可以達到限制限制，並且在完成其中一個作業之前，沒有其他節點會輪詢輸入目錄。

#### 限制工作原理 {#how-throttling-works}

「受監視的資料夾」在每個pollInterval上掃描輸入資料夾，提取批大小中指定的檔案數，並為這些檔案中的每個檔案調用目標服務。 例如，如果批大小為4，則每次掃描時，「監視資料夾」將拾取四個檔案，建立四個調用請求並調用目標服務。 在完成這些請求之前，如果調用了「受監視資料夾」，則它將再次啟動四個作業，而不管前四個作業是否已完成。

限制阻止監視資料夾在上一個作業未完成時調用新作業。 「已監視資料夾」檢測正在進行的作業並根據批處理大小減去正在進行的作業來處理新作業。 例如，在第二次調用中，如果已完成的作業數僅為三個，而一個作業仍在進行中，則「監視資料夾」僅調用另外三個作業。

* 「已監視資料夾」依靠階段資料夾中存在的檔案數來確定正在執行的作業數。 如果檔案在階段資料夾中仍未處理，則「監視資料夾」將不再調用任何作業。 例如，如果批處理大小為4，並且停止了3個作業，則「監視資料夾」在後續調用中只調用一個作業。 存在多種情形，可導致檔案在階段資料夾中保持未處理。 當作業停止時，管理員可以終止「進程管理」管理頁上的進程，以便「監視資料夾」將檔案移出舞台資料夾。
* 如果AEM Forms伺服器在「監視資料夾」調用作業之前關閉，則管理員可以將檔案移出舞台資料夾。 有關資訊，請參見 [故障點和恢復](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p)。
* 如果AEM Forms伺服器正在運行，但當作業管理器服務回叫時，監視資料夾未運行，當服務未按順序啟動時，管理員可以將檔案移出舞台資料夾。 有關資訊，請參見 [故障點和恢復](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p)。

### 故障點和恢復故障點和恢復 {#failure-points-and-recoveryfailure-points-and-recovery}

在每個輪詢事件中，「監視資料夾」會鎖定輸入資料夾，將與包含檔案模式匹配的檔案移動到階段資料夾，然後解鎖輸入資料夾。 需要鎖定，以便兩個線程不會拾取同一組檔案並處理它們兩次。 發生此情況的可能性隨著pollInterval的小和批處理的大而增加。 將檔案移動到舞台資料夾後，將解鎖輸入資料夾，以便其他線程可以掃描該資料夾。 此步驟有助於提供高吞吐量，因為在一個線程處理檔案時，其他線程可以掃描。

將檔案移動到階段資料夾後，為每個檔案建立調用請求，並調用目標服務。 可能存在「受監視資料夾」無法恢復階段資料夾中的檔案的情況：

* 如果伺服器在「監視資料夾」可以建立調用請求之前關閉，則舞台資料夾中的檔案將保留在舞台資料夾中，並且不會恢復。

* 如果「監視資料夾」已成功為舞台資料夾中的每個檔案建立調用請求，並且伺服器崩潰，則基於調用類型有兩種行為：

   * **同步**:如果將「監視資料夾」配置為同步調用服務，則舞台資料夾中的所有檔案在舞台資料夾中仍未處理。
   * **非同步**:在這種情況下，「監視資料夾」依賴於「作業管理器」服務。 如果作業管理器服務回叫「監視資料夾」，則根據調用結果將階段資料夾中的檔案移動到保留或失敗資料夾。 如果作業管理器服務未回叫「監視資料夾」，則這些檔案將在階段資料夾中保持未處理。 當作業管理器回叫時，當「監視資料夾」未運行時，會發生這種情況。

#### 恢復階段資料夾中的未處理源檔案 {#recover-unprocessed-source-files-in-the-stage-folder}

當「監視資料夾」無法處理階段資料夾中的源檔案時，可以恢復未處理的檔案。

1. 重新啟動應用程式伺服器或節點。

1. 停止監視資料夾處理新輸入檔案。 如果跳過此步驟，則很難確定在階段資料夾中未處理哪些檔案。 要阻止監視資料夾處理新輸入檔案，請執行以下任務之一：

   * 將「監視資料夾」的includeFilePattern屬性更改為與任何新輸入檔案都不匹配的內容（例如，輸入NOMATCH）。
   * 暫停正在建立新輸入檔案的進程。

   等待AEM Forms恢復並處理所有檔案。 大部分檔案應恢復，並且所有新輸入檔案都應正確處理。 等待「監視資料夾」恢復和處理檔案的時間長度取決於要調用的操作的長度和要恢復的檔案數量。

1. 確定無法處理的檔案。 如果您等待了適當的時間並完成了上一步，並且在階段資料夾中仍保留未處理的檔案，請轉到下一步。

   >[!NOTE]
   >
   >您可以查看階段目錄中檔案的日期和時間戳。 根據檔案數和正常處理時間，可以確定哪些檔案已足夠老，可以認為是卡住的檔案。

1. 將未處理檔案從階段目錄複製到輸入目錄。

1. 如果在步驟2中阻止「監視資料夾」處理新輸入檔案，請將「包括檔案模式」更改為其上一個值，或重新啟用您禁用的進程。

### 將受監視資料夾連結在一起 {#chain-watched-folders-together}

可以將受監視資料夾連結在一起，以便一個受監視資料夾的結果文檔是下一個受監視資料夾的輸入文檔。 每個受監視資料夾都可以調用不同的服務。 通過以此方式配置「監視資料夾」，可以調用多個服務。 例如，一個受監視資料夾可以將PDF檔案轉換為Adobe PostScript®，另一個受監視資料夾可以將PostScript檔案轉換為PDF/A格式。 為此，只需將第一個終結點定義的監視資料夾的結果資料夾設定為指向第二個終結點定義的監視資料夾的輸入資料夾即可。

第一次轉換的輸出將轉到\path\result。 第二次轉換的輸入為\path\result，第二次轉換的輸出將轉到\path\result\result （或第二次轉換的結果資料夾框中定義的目錄）。

### 檔案和資料夾模式 {#file-and-folder-patterns}

管理員可以指定可以調用服務的檔案類型。 可為每個「監視資料夾」建立多個檔案模式。 檔案模式可以是下列檔案屬性之一：

* 具有特定檔案名副檔名的檔案；比如說， &#42;.dat, &#42;.xml, .pdf, &#42;。&#42;
* 具有特定名稱的檔案；例如，資料。&#42;
* 名稱和副檔名中包含複合表達式的檔案，如下例所示：

   * 資料[0-9][0-9][0-9]。[dD][aA]「port」
   * &#42;。[dD][Aa]「port」
   * &#42;。[Xx][毫米][Ll]

* 管理員可以定義輸出資料夾的檔案模式，以在其中儲存結果。 對於輸出資料夾（結果、保留和失敗），管理員可以指定以下任何檔案模式：
* %Y =年（滿）
* %y =年（最後兩位）
* %M =月，
* %D =月日，
* %d =一年中的某天，
* %h =小時，
* %m =分鐘，
* %s =秒，
* %R = 0-9之間的隨機數
* %J =作業名稱

例如，結果資料夾的路徑可能是C:\Adobe\Adobe LiveCycle ES4\BarcodedForms\%y\%m\%d。

輸出參數映射還可以指定其他模式，如：

* %F =源檔案名
* %E =源檔案名副檔名

如果輸出參數映射模式以「File.separator」（即路徑分隔符）結尾，則會建立一個資料夾，並將內容複製到該資料夾中。 如果模式不以「File.separator」結尾，則使用該名稱建立內容（結果檔案或資料夾）。

## 將PDF生成器與監視資料夾一起使用 {#using-pdf-generator-with-a-watched-folder}

您可以配置「監視資料夾」以啟動工作流、服務或指令碼以處理輸入檔案。 在以下部分中，我們將配置一個「監視資料夾」(Stated Folder)以啟動ECMAScript。 ECMAScript將使用PDF生成器將MicrosoftWord(.docx)文檔轉換為PDF文檔。

執行以下步驟以配置帶PDF生成器的監視資料夾：

1. [建立ECMAScript](../../forms/using/watched-folder-in-aem-forms.md#p-create-an-ecmascript-p)
1. [建立工作流](../../forms/using/watched-folder-in-aem-forms.md#p-create-a-workflow-p)
1. [配置監視資料夾](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)

### 建立ECMAScript {#create-an-ecmascript}

ECMAScript將使用PDF生成器的createPDF API將MicrosoftWord(.docx)文檔轉換為PDF文檔。 執行以下步驟建立指令碼：

1. 在瀏覽器窗口中開啟CRXDE lite。 URL為https://&#39;[伺服器]:[埠]「/crx/de」。

1. 導航到/etc/workflow/scripts並建立名為PDFG的資料夾。

1. 在PDFG資料夾中，建立名為pdfg-openOffice-sample.ecma的檔案，並將以下代碼添加到該檔案：

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

1. 保存並關閉檔案。

### 建立工作流 {#create-a-workflow}

1. 在瀏覽AEM器窗口中開啟「工作流UI」。
   <https://[servername>]:&#39;埠/工作流&#39;

1. 在「模型」(Models)視圖中，按一下 **新建**。 在「新建工作流」對話框中，指定 **標題**，然後按一下 **確定**。

   ![建立工作流 — pdf](assets/create-a-workflow-pdf.png)

1. 選擇新建立的工作流，然後按一下 **編輯**。 工作流將在新窗口中開啟。

1. 刪除預設工作流步驟。 將「流程步驟」從「側腳」拖放到「工作流」。

   ![建立工作流 — pdf2](assets/create-a-workflow-pdf2.png)

1. 按一下右鍵「處理步驟」(Process Step)，然後選擇 **編輯**。 出現「Step Properties（步驟屬性）」窗口。

1. 在「進程」(Process)頁籤中，選擇ECMAScript。 例如，在中建立的pdfg-openOffice-sample.ecma指令碼 [建立ECMAScript](#p-create-an-ecmascript-p)。 啟用 **處理程式高級** 選項 **確定**。

   ![建立 — 工作流3-pdf](assets/create-a-workflow3-pdf.png)

### 配置監視資料夾 {#configure-the-watched-folder}

1. 在瀏覽器窗口中開啟CRXDE lite。 https://&#39;[伺服器]:[埠]&#39;/crx/de/

1. 導航到/etc/fd/watchfolder/config/資料夾，然後建立nt:antrograble類型的節點。

   ![configure-the-watch-folder-pdf](assets/configure-the-watched-folder-pdf.png)

1. 將以下屬性添加到節點：

   * folderPath（字串）:要按定義的時間間隔掃描的資料夾的路徑。 該資料夾必須位於所有具有對伺服器完全訪問權限的伺服器的共用位置。
inputProcessorType（字串）:要啟動的進程的類型。 在本教程中，指定工作流。

   * inputProcessorId（字串）:inputProcessorId屬性的行為基於為inputProcessorType屬性指定的值。 在本示例中，inputProcessorType屬性的值是workflow。 因此，對於inputProcessorId屬性，請指定PDFG工作流的以下路徑：/etc/workflow/models/pdfg/jcr：內容/模型

   * outputFilePattern（字串）:輸出檔案的模式。 可以指定資料夾或檔案模式。 如果指定了資料夾模式，則輸出檔案的名稱將如工作流中所述。 如果指定了檔案模式，則輸出檔案的名稱如檔案模式中所述。
   除了上述強制屬性外，「受監視資料夾」還支援一些可選屬性。 有關可選屬性的完整清單和說明，請參見 [監視的資料夾屬性](#watchedfolderproperties)。

## 已知問題 {#watched-folder-known-issues}

在JEE上啟AEM動6.5Forms時，在JBoss完全啟動和檔案無法處理之前，檔案將開始處理。 為避免這種情況，在啟動JBoss之前，請清除所有「已監視資料夾」。
