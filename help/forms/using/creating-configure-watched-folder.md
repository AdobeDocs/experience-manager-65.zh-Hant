---
title: 建立或設定已觀看的資料夾
seo-title: Create or Configure a watched folder
description: 了解如何建立或刪除已觀看的資料夾，或修改現有已觀看資料夾的屬性。
seo-description: Learn how to create or delete a watched folder, or modify the properties of an existing watched folder.
uuid: 659d4d8c-99b8-40dd-b884-bfee4d476fe1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 0ce7b338-6686-49b3-b58b-e7ab6b670708
exl-id: b15d8d3b-5e47-4c33-95fe-440fcf96be83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---

# 建立或設定已觀看的資料夾 {#create-or-configure-a-watched-folder}

管理員可以配置網路資料夾，稱為 *已觀看的資料夾*，以便當使用者將檔案(例如PDF檔案)放入觀看的資料夾時，會啟動預先設定的操作並操作檔案。 執行指定操作後，操作會將修改的檔案保存到指定的輸出資料夾中。 如需管理已觀看資料夾的詳細資訊，請參閱 [管理說明](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

您可以使用觀看的資料夾使用者介面來：

* 建立已觀看的資料夾
* 修改現有監視資料夾的屬性
* 刪除已監視的資料夾

## 建立已觀看的資料夾 {#create-a-watched-folder}

設定已監看資料夾之前，請確定下列事項：

* 監看資料夾是AEM表單的進階功能。 需要AEM Forms附加套件才能運作。 請確定已安裝並設定適當的AEM Forms附加元件套件。
* 您可以在共用或本機儲存空間中建立已觀看的資料夾。 確保配置為運行觀看資料夾的AEM Forms用戶具有觀看資料夾的讀寫權限。
* 您可以使用服務、工作流程或指令碼，以自動執行有已觀看資料夾的操作。 請確定已建立對應的服務、工作流程或指令碼，並準備好執行。 如需建立服務、工作流程和指令碼的相關資訊，請參閱 [處理檔案的各種方法](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files).
* 已監看的資料夾有各種屬性，請參閱 [監視的資料夾屬性](watched-folder-in-aem-forms.md#watchedfolderproperties).

執行下列步驟以建立已觀看的資料夾：

1. 點選 **Adobe Experience Manager** 圖示。
1. 點選 **工具** > **Forms** > **配置「監視」資料夾。** 將顯示已配置的監視資料夾清單。
1. 點選 **新增**. 此時會顯示建立觀看資料夾所需的欄位清單：

   * **名稱**:識別已觀看的資料夾。 名稱僅使用英數字元。
   * **路徑**:指定已監視的資料夾位置。 在群集環境中，此設定必須指向一個共用網路資料夾，該資料夾可供在群集的不同節點上運行AEM的每個用戶訪問。
   * **處理檔案使用**:要啟動的進程類型。 您可以指定工作流程、指令碼或服務。
   * **服務名稱/指令碼路徑/工作流路徑**:欄位的行為是根據 **處理檔案使用** 欄位。 您可以指定下列值：

      * 對於「工作流」，指定要執行的工作流模型。 例如， /etc/workflow/models/&lt;workflow_name>/jcr:content/model
      * 對於指令碼，指定要執行的指令碼的JCR路徑。 例如， /etc/watchfolder/test/testScript.ecma
      * 針對服務，指定用於找到OSGi服務的篩選器。 此服務已註冊為com.adobe.aemfd.watchfolder.service.api.ContentProcessor介面的實作。 例如，以下代碼是ContentProcessor介面的自定義實現，該介面具有自定義(foo=bar)屬性。

   >[!NOTE]
   >
   >如果您已選取 **服務** 針對 **處理檔案使用** 欄位中，服務名稱(inputProcessorType)欄位的值必須括在括弧中。 例如(foo=bar)。

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **輸出檔案模式**:指定分號(;)分隔的模式清單，監視資料夾會使用該清單來判斷輸出檔案和資料夾的名稱和位置。 如需檔案模式的詳細資訊，請參閱 [關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).


1. 點選 **進階**. 進階標籤包含更多欄位。 這些欄位大多包含預設值。

   * **裝載映射器篩選器：** 建立已觀看的資料夾時，會在正在觀看的資料夾內建立資料夾結構。 資料夾結構具有階段、結果、保留、輸入和失敗資料夾。 資料夾結構可作為工作流的輸入裝載，並接受來自工作流的輸出。 它也可以列出故障點（如果有）。 有效負載的結構與已觀看資料夾的結構不同。 您可以撰寫自訂指令碼，將已觀看資料夾的結構對應至裝載。 這類指令碼稱為裝載映射器篩選器。 提供兩種現成可用的裝載映射器實施。 如果您沒有 [自訂實作](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter)，請使用其中一個現成可用的實作：

      * **預設映射器：** 使用預設有效負載映射器，將已監視資料夾的輸入和輸出內容保留在有效負載中的單獨輸入和輸出資料夾中。
      * **簡單的檔案式裝載對應器：** 使用簡單檔案式裝載映射器，將輸入和輸出內容直接保留在裝載資料夾中。 它不會建立任何額外的階層，例如預設映射器。
   * **運行模式**:指定以逗號分隔的允許執行模式清單以執行工作流程。
   * **在之後超時分段檔案**:指定在已擷取以進行處理的輸入檔案/資料夾被視為已逾時並標示為失敗之前，要等候的秒數。 超時機制僅在此屬性的值為正數時激活。
   * **在限制時刪除超時分段檔案**:若已啟用，則 **在之後超時分段檔案** 僅當為觀看的資料夾開啟節流時，才激活機制。
   * **在以下時間後掃描輸入資料夾：** 指定掃描觀看的資料夾以獲取輸入的時間間隔（以秒為單位）。 除非啟用「調節」設定，否則輪詢間隔應比處理平均作業的時間長；否則，系統可能會超載。 間隔的值必須大於或等於1。
   * **排除檔案模式**:指定分號(;)分隔的模式清單，監視資料夾會使用該清單來判斷要掃描和擷取的檔案和資料夾。 系統不會掃描具有指定模式的任何檔案或資料夾以進行處理。 如需檔案模式的詳細資訊，請參閱 [關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **包含檔案模式**:指定分號(;)分隔的模式清單，監視資料夾會使用該清單來判斷要掃描和擷取的資料夾和檔案。 例如，如果「包含檔案模式」為input&amp;ast;，則所有與input&amp;ast匹配的檔案和資料夾；被撿起。 預設值為&amp;ast;並指示所有檔案和資料夾。 如需檔案模式的詳細資訊，請參閱 [關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **等待時間：** 指定在建立資料夾或檔案後，在掃描資料夾或檔案之前等待的時間（以毫秒為單位）。 例如，如果等待時間為3,600,000毫秒（一小時），而檔案是在一分鐘前建立的，則此檔案將在59分鐘或更長時間過後擷取。 預設值為 0。

      此設定非常實用，可確保檔案或資料夾的所有內容都複製到輸入資料夾。 例如，如果要處理大型檔案，而要下載該檔案需要10分鐘，請將等待時間設定為10&amp;ast;60&amp;ast;1000毫秒。 如果檔案未保存10分鐘，此間隔將阻止監視的資料夾掃描該檔案。

   * **刪除早於以下時間的結果：** 指定在刪除早於指定值的檔案和資料夾之前等待的時間（以天為單位）。 此設定有助於確保結果資料夾不會填滿。 值為–1天表示絕不刪除結果資料夾。 預設值為–1。
   * **結果資料夾名稱：** 指定要儲存結果的資料夾名稱。 如果結果未出現在此資料夾中，請檢查失敗資料夾。 不會處理唯讀檔案，且會將其儲存在失敗資料夾中。 您可以使用具有下列檔案模式的絕對或相對路徑：

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
      * 例如，如果它是2009年7月17日的晚上8點，並且您指定C:/Test/WF0/failure/%Y/%M/%D/%H/，則結果資料夾為C:/Test/WF0/failure/2009/07/17/20。
      * 如果路徑不是絕對路徑，而是相對路徑，則會在觀看的資料夾內建立資料夾。 預設值為result/%Y/%M/%D/，即監視資料夾內的「結果」資料夾。 如需檔案模式的詳細資訊，請參閱 [關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **失敗資料夾名稱：** 指定保存失敗檔案的資料夾。 此位置一律與已觀看的資料夾相對。 可以使用檔案模式，如「結果資料夾」中所述。
   * **保留資料夾名稱：** 指定成功掃描和拾取後儲存檔案的資料夾。 路徑可以是絕對目錄、相對目錄或空目錄。 可以使用檔案模式，如「結果資料夾」中所述。 預設值為preserve/%Y/%M/%D/。
   * **批大小：** 指定每次掃描要提取的檔案或資料夾數量。 它防止了系統過載；一次掃描太多檔案可能會造成當機。 預設值為 2。

      如果掃描間隔較小，線程會經常掃描輸入資料夾。 如果檔案經常被拖放到監看的資料夾中，則應將掃描間隔保持在較小。 如果檔案不常被刪除，請使用較大的掃描間隔，以便其他服務可以使用線程。

   * **調節開：** 啟用此選項後，它會限制AEM表單在任何指定時間處理的已觀看資料夾作業數。 「批大小」值確定作業的最大數量。 如需詳細資訊，請參閱 [節流](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **以類似名稱覆寫現有檔案**:設為True時，會覆寫結果資料夾和保留資料夾中的檔案。 設為False時，名稱使用帶有數值索引尾碼的檔案和資料夾。 預設值為False。
   * **失敗時保留檔案：** 設為True時，會保留輸入檔案以防失敗。 預設值為true。
   * **包含具有模式的檔案：** 指定分號(;)分隔的模式清單，監視資料夾會使用該清單來判斷要掃描和擷取的資料夾和檔案。 例如，如果輸入了「包含檔案模式」，則會拾取所有與輸入匹配的檔案和資料夾。 如需詳細資訊，請參閱 [管理說明](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **非同步叫用監看資料夾：** 將調用類型標識為非同步或同步。 預設值為非同步。 對於長期進程，建議使用非同步，而對於暫時進程或短期進程，建議使用同步。
   * **啟用「觀看的資料夾」：** 啟用此選項後，將啟用監看資料夾。 預設值為True。



## 修改現有監視資料夾的屬性 {#modify-properties-of-an-existing-watched-folder}

除了更改監視資料夾的名稱外，您還可以修改現有監視資料夾的所有屬性。 執行以下步驟修改現有監視資料夾的屬性：

1. 點選 **Adobe Experience Manager** 圖示。
1. 點選 **工具** > **Forms** > **配置「監視」資料夾。** 將顯示已配置的監視資料夾清單。
1. 在「觀看資料夾」畫面的左側，選取觀看資料夾並點選 **編輯。** 隨即顯示建立觀看資料夾所需的欄位清單。 列於 **基本** 標籤是必填的。 進階標籤包含更多欄位。 這些欄位大多包含預設值。 您可以根據需求修改這些屬性。
1. 修改屬性後，點選 **更新**. 已修改的屬性將被保存。
