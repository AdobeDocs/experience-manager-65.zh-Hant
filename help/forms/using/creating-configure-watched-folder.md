---
title: 建立或設定受監視的資料夾
seo-title: 建立或設定受監視的資料夾
description: 瞭解如何建立或刪除受監視的資料夾，或修改現有受監視資料夾的屬性。
seo-description: 瞭解如何建立或刪除受監視的資料夾，或修改現有受監視資料夾的屬性。
uuid: 659d4d8c-99b8-40dd-b884-bfee4d476fe1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 0ce7b338-6686-49b3-b58b-e7ab6b670708
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30

---


# 建立或設定受監視的資料夾 {#create-or-configure-a-watched-folder}

管理員可以配置網路資料夾(稱為 *watched資料夾*)，以便當用戶將檔案（如PDF檔案）放置到watched資料夾時，啟動預配置的操作並操作該檔案。 執行指定的操作後，操作將修改的檔案保存到指定的輸出資料夾中。 如需管理受監視資料夾的詳細資訊，請參閱管 [理說明](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)。

您可以使用監視的資料夾使用者介面來：

* 建立受監視的資料夾
* 修改現有監視資料夾的屬性
* 刪除受監視的資料夾

## 建立受監視的資料夾 {#create-a-watched-folder}

在配置監視資料夾之前，請確保以下各項：

* Watched資料夾是AEM表格的進階功能。 它需要AEM Forms附加套件才能運作。 請確定已安裝並設定適當的AEM Forms附加套件。
* 您可以在共用或本機儲存區建立受監視的資料夾。 請確定已設定為執行監看資料夾的AEM表單使用者對監看資料夾具有讀取和寫入權限。
* 您可以使用「服務」、「工作流程」或「指令碼」，自動處理受監視資料夾的作業。 請確定已建立對應的服務、工作流程或指令碼並準備執行。 如需有關建立服務、工作流程和指令碼的詳細資訊，請參 [閱各種檔案處理方法](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files)。
* 監視的資料夾具有各種屬性，請參 [閱「監視資料夾屬性」](/help/forms/using/watched-folder-in-aem-forms.md#main-pars-header-1)。

執行以下步驟以建立受監視資料夾：

1. 點 **選畫面左上角的Adobe Experience Manager** 圖示。
1. 點選「 **工具** >表 **單** >設 **定Watched資料夾」。** 將顯示已配置的監視資料夾的清單。
1. 點選 **新**。 此時將顯示建立監視資料夾所需欄位的清單：

   * **名稱**:識別受監視的資料夾。 名稱僅使用英數字元。
   * **路徑**:指定受監視的資料夾位置。 在叢集環境中，此設定必須指向可供在叢集不同節點上執行AEM的每位使用者存取的共用網路資料夾。
   * **使用**:要啟動的進程的類型。 您可以指定工作流程、指令碼或服務。
   * **服務名／指令碼路徑／工作流路徑**:欄位的行為基於為「使用進程檔案」( **Process Files Using** )欄位指定的值。 您可以指定下列值：

      * 對於「工作流」，指定要執行的工作流模型。 例如，/etc/workflow/models/&lt;workflow_name>/jcr:content/model
      * 對於指令碼，指定要執行的指令碼的JCR路徑。 例如，/etc/watchfolder/test/testScript.ecma
      * 對於服務，請指定用於查找OSGi服務的篩選器。 此服務已註冊為com.adobe.aemfd.watchfolder.service.api.ContentProcessor Interface的實作。 例如，下列程式碼是ContentProcessor介面的自訂實作，具有自訂(foo=bar)屬性。
   >[!NOTE]
   >
   >如果已為「使 **用流程檔案** 」(Process Files Using **** )欄位選擇了「服務」(Service)，則「服務名稱(inputProcessorType)」(服務名稱(inputProcessorType)欄位的值必須括在括弧中。 例如(foo=bar)。

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **輸出檔案模式**:指定分號(;)分隔的模式清單，受監視的資料夾會使用該清單來判斷輸出檔案和資料夾的名稱和位置。 有關檔案模式的詳細資訊，請參 [閱關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)。


1. 點選「 **進階**」。 進階標籤包含更多欄位。 這些欄位中，大部分都包含預設值。

   * **** 裝載映射器過濾器：當您建立受監視的檔案夾時，會在受監視的檔案夾中建立檔案夾結構。 資料夾結構具有舞台、結果、保留、輸入和失敗資料夾。 該資料夾結構可以用作工作流的輸入負載並接受來自工作流的輸出。 它還可以列出故障點（如果有）。 有效載荷的結構與監視資料夾的結構不同。 您可以編寫自訂指令碼，將受監視資料夾的結構對應至裝載。 這種指令碼稱為負載映射器過濾器。 有兩種現成可用的裝載映射器實現。 如果您沒有 [自訂實作](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter)，請使用一個現成可用的實作：

      * **** 預設映射器：使用預設裝載映射器，將受監視資料夾的輸入和輸出內容保留在裝載中單獨的輸入和輸出資料夾中。
      * **** 簡單的基於檔案的負載映射器：使用簡單檔案型裝載映射程式，將輸入和輸出內容直接保留在裝載資料夾中。 它不建立任何額外的層次，如預設映射器。
   * **運行模式**:指定以逗號分隔的工作流執行允許運行模式清單。
   * **在以下時間後暫存的檔案超時**:指定等待的秒數，然後輸入檔案／資料夾已被拾取進行處理，被視為已超時並標籤為失敗。 只有當此屬性的值為正數時，才會啟動逾時機制。
   * **在調節時刪除逾時分段檔案**:如果啟用，則 **只有在為受監視資料夾開啟頻寬限制時，才會激活「Time Out Staged Files After** 」機制。
   * **** 在每次掃描後掃描輸入資料夾：指定掃描受監視資料夾以取得輸入的時間間隔（以秒為單位）。 除非啟用「限制」設定，否則輪詢間隔應比處理平均作業的時間長；否則，系統可能會過載。 間隔的值必須大於或等於1。
   * **排除檔案模式**:指定分號(;)分隔的模式清單，該清單由受監視的資料夾用來決定要掃描和擷取哪些檔案和資料夾。 不會掃描任何具有指定模式的檔案或檔案夾以進行處理。 有關檔案模式的詳細資訊，請參 [閱關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)。
   * **包含檔案模式**:指定分號(;)分隔的模式清單，讓受監視的檔案夾用來判斷要掃描和擷取的檔案夾和檔案。 例如，如果「包含檔案模式」是input&amp;ast;，則所有與input&amp;ast匹配的檔案和資料夾；都被撿起來了。 預設值為&amp;ast;並指示所有檔案和資料夾。 有關檔案模式的詳細資訊，請參 [閱關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)。
   * **** 等待時間：指定在資料夾或檔案建立後掃描之前等待的時間（以毫秒為單位）。 例如，如果等待時間為3,600,000毫秒（1小時），而檔案是在一分鐘前建立的，則此檔案會在59分鐘或更久之後被擷取。 預設值為0。

      此設定對於確保檔案或資料夾的所有內容都複製到輸入資料夾非常有用。 例如，如果要處理大檔案，而要下載該檔案需要10分鐘，請將等待時間設定為10&amp;ast;60 &amp;ast;1000毫秒。 此間隔會阻止受監視資料夾掃描檔案（如果檔案沒有10分鐘）。

   * **** 刪除早於：指定在刪除早於指定值的檔案和資料夾之前要等待的時間（以天為單位）。 此設定在確保結果資料夾未滿時非常有用。 值為-1天表示從不刪除結果資料夾。 預設值為-1。
   * **** 結果資料夾名稱：指定要儲存結果的資料夾名稱。 如果結果未顯示在此資料夾中，請檢查失敗資料夾。 只讀檔案不會被處理，並保存在失敗資料夾中。 可以將絕對路徑或相對路徑與以下檔案模式一起使用：

      * %F =檔案名前置詞
      * %E =副檔名
      * %Y =年（已滿）
      * %y =年（最後兩位）
      * %M =月
      * %D =月中的某天
      * %d =年
      * %H =小時（24小時時鐘）
      * %h =小時（12小時時鐘）
      * %m =分鐘
      * %s =秒
      * %l =毫秒
      * %R =隨機數（介於0和9之間）
      * %P =進程或作業ID
      * 例如，如果在2009年7月17日下午8點，而您指定C:/Test/WF0/failure/%Y/%M/%D/%H/，則結果資料夾為C:/Test/WF0/failure/2009/07/17/20。
      * 如果路徑不是絕對的，而是相對的，則會在監視的資料夾內建立資料夾。 預設值為result/%Y/%M/%D/，即監視資料夾內的「結果」資料夾。 有關檔案模式的詳細資訊，請參 [閱關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)。
   * **** 故障資料夾名稱：指定保存失敗檔案的資料夾。 此位置始終相對於監視的資料夾。 可以使用檔案模式，如「結果資料夾」中所述。
   * **** 保留資料夾名稱：指定在成功掃描並擷取檔案後儲存檔案的檔案夾。 路徑可以是絕對、相對或空目錄。 可以使用檔案模式，如「結果資料夾」中所述。 預設值為preserve/%Y/%M/%D/。
   * **** 批大小：指定每次掃描要拾取的檔案或資料夾數。 它防止了系統過載；一次掃描太多檔案可能會造成當機。 預設值為2。

      如果掃描間隔較小，線程會經常掃描輸入資料夾。 如果檔案經常被丟入監視資料夾，則應將掃描間隔保持在較小。 如果檔案不常被丟棄，請使用較大的掃描間隔，以便其他服務可以使用線程。

   * **** 限制開啟：啟用此選項時，它會限制AEM表單在任何指定時間處理的受監視檔案夾工作數。 「批大小」值確定作業的最大數目。 如需詳細資訊，請參 [閱](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **以類似名稱覆寫現有檔案**:當設定為True時，將覆蓋結果資料夾和保留資料夾中的檔案。 當設定為False時，名稱將使用帶有數字索引尾碼的檔案和資料夾。 預設值為False。
   * **** 失敗時保留檔案：當設為True時，會在失敗時保留輸入檔案。 預設值為true。
   * **** 包含具有模式的檔案：指定分號(;)分隔的模式清單，讓受監視的檔案夾用來判斷要掃描和擷取的檔案夾和檔案。 例如，如果輸入「包含檔案模式」，則會擷取所有符合輸入的檔案和檔案夾。 如需詳細資訊，請參閱「管 [理說明」](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **** 非同步地叫用Watched資料夾：將調用類型標識為非同步或同步。 預設值為非同步。 建議對長壽命進程使用非同步，而對瞬態或短壽命進程則建議使用同步。
   * **** 啟用「監視資料夾」:啟用此選項後，就會啟用監看資料夾。 預設值為True。



## 修改現有監視資料夾的屬性 {#modify-properties-of-an-existing-watched-folder}

除了更改監視資料夾的名稱外，您還可以修改現有監視資料夾的所有屬性。 執行以下步驟以修改現有監視資料夾的屬性：

1. 點選 **螢幕左上角的Adobe Experience Manager** 圖示。
1. 點選「 **工具** >表 **單** >設 **定Watched資料夾」。** 將顯示已配置的監視資料夾的清單。
1. 在「Watched Folder」畫面的左側，選取Watchfolder並點選「編 **輯」。** 此時將顯示建立監視資料夾所需欄位的清單。 「基本」( **Basic** )頁籤中列出的欄位是強制的。 進階標籤包含更多欄位。 這些欄位中，大部分都包含預設值。 您可以根據需求修改這些屬性。
1. 修改屬性後，點選「 **更新」**。 將保存修改的屬性。

