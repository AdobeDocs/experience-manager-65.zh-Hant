---
title: 建立或配置監視資料夾
seo-title: Create or Configure a watched folder
description: 瞭解如何建立或刪除受監視資料夾，或修改現有受監視資料夾的屬性。
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

# 建立或配置監視資料夾 {#create-or-configure-a-watched-folder}

管理員可以配置網路資料夾，稱為 *監視資料夾*&#x200B;這樣，當用戶將檔案(如PDF檔案)放在監視資料夾中時，就會啟動預配置的操作並操作該檔案。 執行指定操作後，該操作會將修改的檔案保存到指定的輸出資料夾中。 有關管理受監視資料夾的詳細資訊，請參見 [管理幫助](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)。

可以使用監視資料夾用戶介面執行以下操作：

* 建立受監視資料夾
* 修改現有監視資料夾的屬性
* 刪除受監視資料夾

## 建立受監視資料夾 {#create-a-watched-folder}

在配置監視資料夾之前，請確保：

* 受監視資料夾是表單的AEM高級功能。 它需AEM要窗體載入項包才能運行。 確保已安裝並配置相應的AEM Forms附加軟體包。
* 可以在共用或本地儲存上建立監視資料夾。 確保配置AEM為運行監視資料夾的表單用戶對監視資料夾具有讀寫權限。
* 您可以使用服務、工作流或指令碼自動執行使用受監視資料夾的操作。 確保已建立相應的服務、工作流或指令碼並準備運行。 有關建立服務、工作流和指令碼的資訊，請參見 [處理檔案的各種方法](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files)。
* 受監視的資料夾具有各種屬性，請參見 [受監視資料夾屬性](watched-folder-in-aem-forms.md#watchedfolderproperties)。

執行以下步驟建立監視資料夾：

1. 點擊 **Adobe Experience Manager** 表徵圖。
1. 點擊 **工具** > **Forms** > **配置監視資料夾。** 將顯示已配置的監視資料夾的清單。
1. 點擊 **新建**。 將顯示建立監視資料夾所需欄位的清單：

   * **名稱**:標識受監視的資料夾。 名稱僅使用字母數字字元。
   * **路徑**:指定監視的資料夾位置。 在群集環境中，此設定必須指向一個共用網路資料夾，該資料夾可供運行在群集不同節AEM點上的每個用戶訪問。
   * **處理檔案使用**:要啟動的進程的類型。 可以指定工作流、指令碼或服務。
   * **服務名稱/指令碼路徑/工作流路徑**:欄位的行為基於為 **處理檔案使用** 的子菜單。 可以指定以下值：

      * 對於工作流，指定要執行的工作流模型。 例如，/etc/workflow/models/&lt;workflow_name>/jcr：內容/模型
      * 對於指令碼，指定要執行的指令碼的JCR路徑。 例如，/etc/watchfolder/test/testScript.ecma
      * 對於服務，指定用於查找OSGi服務的篩選器。 該服務註冊為com.adobe.aemfd.watchfolder.service.api.ContentProcessor Interface的實現。 例如，以下代碼是具有自定義(foo=bar)屬性的ContentProcessor介面的自定義實現。

   >[!NOTE]
   >
   >如果已選擇 **服務** 為 **處理檔案使用** 欄位中，「服務名稱」(inputProcessorType)欄位的值必須括在括弧中。 例如(foo=bar)。

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **輸出檔案模式**:指定分號(;)分隔的模式清單，監視資料夾使用該清單來確定輸出檔案和資料夾的名稱和位置。 有關檔案模式的詳細資訊，請參見 [關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)。


1. 點擊 **高級**。 高級頁籤包含更多欄位。 這些欄位中的大多數都包含預設值。

   * **負載映射器篩選器：** 建立受監視資料夾時，它會在正被監視的資料夾中建立資料夾結構。 資料夾結構具有階段、結果、保留、輸入和失敗資料夾。 該資料夾結構可以用作工作流的輸入負載並接受來自工作流的輸出。 它還可列出故障點（如果有）。 負載的結構不同於監視資料夾的結構。 您可以編寫自定義指令碼，將受監視資料夾的結構映射到負載。 這種指令碼稱為負載映射器篩選器。 有兩個現成的負載映射器實現。 如果你沒有 [自定義實現](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter)，使用一個現成實現：

      * **預設映射器：** 使用預設負載映射器將受監視資料夾的輸入和輸出內容保留在負載中單獨的輸入和輸出資料夾中。
      * **基於檔案的簡單負載映射器：** 使用基於簡單檔案的負載映射器將輸入和輸出內容直接保留在負載資料夾中。 它不會建立任何額外的層次結構，如預設映射器。
   * **運行模式**:指定用於工作流執行的允許運行模式的逗號分隔清單。
   * **超時轉移檔案**:指定等待的秒數，然後將已被拾取用於處理的輸入檔案/資料夾視為已超時並標籤為失敗。 僅當此屬性的值為正數時，超時機制才激活。
   * **當限制時刪除超時暫存檔案**:如果啟用， **超時轉移檔案** 僅當為監視資料夾開啟限制時才激活機制。
   * **每次掃描一次輸入資料夾：** 指定掃描監視資料夾以獲取輸入的時間間隔（秒）。 除非啟用「限制」設定，否則輪詢間隔應長於處理平均作業的時間；否則，系統可能會過載。 間隔的值必須大於或等於1。
   * **排除檔案模式**:指定分號(;)分隔的模式清單，監視資料夾使用該清單來確定要掃描和拾取的檔案和資料夾。 不掃描具有指定模式的任何檔案或資料夾進行處理。 有關檔案模式的詳細資訊，請參見 [關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)。
   * **包括檔案模式**:指定分號(;)分隔的模式清單，監視資料夾使用該清單來確定要掃描和拾取的資料夾和檔案。 例如，如果「包括檔案模式」為input&amp;ast;，則匹配input&amp;ast的所有檔案和資料夾；被選中。 預設值為&amp;ast;並指示所有檔案和資料夾。 有關檔案模式的詳細資訊，請參見 [關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)。
   * **等待時間：** 指定在建立資料夾或檔案後掃描之前等待的時間（以毫秒為單位）。 例如，如果等待時間為3,600,000毫秒（一小時），且檔案是在一分鐘前建立的，則該檔案將在59分鐘或更長時間後被拾取。 預設值為 0。

      此設定對確保將檔案或資料夾的所有內容複製到輸入資料夾非常有用。 例如，如果要處理一個大檔案，並且該檔案下載需要10分鐘，請將等待時間設定為10&amp;ast;60 &amp;ast;1000毫秒。 如果檔案未保存10分鐘，則此間隔將阻止監視資料夾掃描該檔案。

   * **刪除早於以下時間的結果：** 指定在刪除早於指定值的檔案和資料夾之前等待的時間（以天為單位）。 此設定在確保結果資料夾未滿時非常有用。 值為–1天表示從不刪除結果資料夾。 預設值為–1。
   * **結果資料夾名稱：** 指定儲存結果的資料夾的名稱。 如果結果未顯示在此資料夾中，請檢查失敗資料夾。 不處理只讀檔案並將其保存在故障資料夾中。 可將絕對路徑或相對路徑與下列檔案模式一起使用：

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
      * 例如，如果2009年7月17日晚上8點，並且您指定C:/Test/WF0/failure/%Y/%M/%D/%H/，則結果資料夾為C:/Test/WF0/failure/2009/07/17/20。
      * 如果路徑不是絕對的，而是相對的，則會在監視資料夾內建立資料夾。 預設值是result/%Y/%M/%D/，它是受監視資料夾內的「結果」資料夾。 有關檔案模式的詳細資訊，請參見 [關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)。
   * **失敗資料夾名稱：** 指定保存失敗檔案的資料夾。 此位置始終相對於監視的資料夾。 可以使用檔案模式，如「結果資料夾」中所述。
   * **保留資料夾名稱：** 指定成功掃描和拾取後儲存檔案的資料夾。 路徑可以是絕對目錄、相對目錄或空目錄。 可以使用檔案模式，如「結果資料夾」中所述。 預設值為preserve/%Y/%M/%D/。
   * **批大小：** 指定每次掃描要拾取的檔案或資料夾數。 它防止了系統過載；一次掃描過多檔案可能會導致崩潰。 預設值為 2。

      如果掃描間隔較小，則線程會經常掃描輸入資料夾。 如果檔案經常被丟棄到受監視的資料夾中，則應將掃描間隔保持在較小。 如果檔案不常被刪除，請使用更大的掃描間隔，以便其他服務可以使用線程。

   * **限制開啟：** 啟用此選項後，它將限制表單在任意給定時間處AEM理的受監視資料夾作業數。 「批大小」值確定作業的最大數量。 有關詳細資訊，請參見 [限制](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **覆蓋具有相似名稱的現有檔案**:設定為True時，結果資料夾和保留資料夾中的檔案將被覆蓋。 如果設定為False，則名稱將使用帶數字索引尾碼的檔案和資料夾。 預設值為False。
   * **失敗時保留檔案：** 如果設定為True，則在出現故障時保留輸入檔案。 預設值為true。
   * **包括具有模式的檔案：** 指定分號(;)分隔的模式清單，監視資料夾使用該清單來確定要掃描和拾取的資料夾和檔案。 例如，如果輸入了「包括檔案模式」，則會拾取所有與輸入匹配的檔案和資料夾。 有關詳細資訊，請參見 [管理幫助](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **非同步調用監視資料夾：** 將調用類型標識為非同步或同步。 預設值為非同步。 建議對長壽命進程使用非同步，而對暫時或短壽命進程建議使用同步。
   * **啟用監視資料夾：** 啟用此選項後，將啟用監視資料夾。 預設值為True。



## 修改現有監視資料夾的屬性 {#modify-properties-of-an-existing-watched-folder}

除了更改受監視資料夾的名稱外，您還可以修改現有受監視資料夾的所有屬性。 執行以下步驟以修改現有監視資料夾的屬性：

1. 點擊 **Adobe Experience Manager** 表徵圖。
1. 點擊 **工具** > **Forms** > **配置監視資料夾。** 將顯示已配置的監視資料夾的清單。
1. 在「監視資料夾」螢幕的左側，選擇監視資料夾，然後點擊 **編輯。** 將顯示建立監視資料夾所需的欄位清單。 中列出的欄位 **基本** Tab是必填項。 高級頁籤包含更多欄位。 這些欄位中的大多數都包含預設值。 您可以根據您的要求修改這些屬性。
1. 修改屬性後，點擊 **更新**。 將保存修改的屬性。
