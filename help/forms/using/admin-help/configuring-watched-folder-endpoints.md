---
title: 正在設定watched資料夾端點
description: 瞭解如何設定watched資料夾端點。 如果檔案置於watched資料夾中，則會叫用已設定的服務操作並操作檔案。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: ec169a01-a113-47eb-8803-bd783ea2c943
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '7192'
ht-degree: 0%

---

# 正在設定watched資料夾端點 {#configuring-watched-folder-endpoints}

管理員可以設定網路資料夾，稱為&#x200B;*watched資料夾*，這樣當使用者將檔案(例如PDF檔案)放入watched資料夾時，就會叫用已設定的服務作業並操作檔案。 服務執行指定的作業後，會將修改的檔案儲存在指定的輸出資料夾中。

## 正在設定Watched資料夾服務 {#configuring-the-watched-folder-service}

設定watched資料夾端點之前，請先設定Watched資料夾服務。 Watched資料夾服務的設定引數有兩個用途：

* 設定所有watched資料夾端點通用的屬性
* 為所有watched資料夾端點提供預設值

在設定Watched資料夾服務後，您為目標服務新增Watched資料夾端點。 新增端點時，您可以設定值，例如將檔案或資料夾放在已設定之Watched資料夾服務的輸入資料夾中時，要呼叫的服務名稱和作業名稱。 如需設定Watched資料夾服務的詳細資訊，請參閱[Watched資料夾服務設定](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings)。

## 正在建立watched資料夾 {#creating-a-watched-folder}

您可以透過下列兩種方式建立watched資料夾：

* 設定watched資料夾端點的設定時，請在[路徑]方塊中輸入父目錄的完整路徑，並附上要建立的watched資料夾名稱，如下列範例所示：
  `  C:\MyPDFs\MyWatchedFolder`由於MyWatchedFolder資料夾尚不存在，AEM表單會嘗試在該位置建立它。

* 在設定watched資料夾端點之前，先在檔案系統上建立資料夾，然後在[路徑]方塊中輸入完整路徑。

在叢集環境中，用來當作watched資料夾的資料夾必須在檔案系統或網路上可以存取、寫入和共用。 在此案例中，叢集的每個應用程式伺服器執行個體都必須擁有相同共用資料夾的存取權。

在Windows中，如果應用程式伺服器是以服務的形式執行，則必須透過下列其中一種方式，以適當的共用資料夾存取權來啟動應用程式伺服器：

* 設定應用程式伺服器服務[以&#x200B;**引數**&#x200B;登入]以特定使用者的身分啟動，並擁有適當的共用監看資料夾存取權。
* 將應用程式伺服器服務啟動為本機系統選項設定為允許服務與案頭互動。 這個選項要求每個人都可以存取和寫入共用的watched資料夾。

## 將watched資料夾鏈結在一起 {#chaining-together-watched-folders}

Watched資料夾可以鏈結在一起，因此一個watched資料夾的結果檔案是下一個watched資料夾的輸入檔案。 每個watched資料夾都可以叫用不同的服務。 透過以這種方式設定watched資料夾，可以叫用多項服務。 例如，一個watched資料夾可以將PDF檔案轉換為Adobe PostScript®而另一個watched資料夾可以將PostScript檔案轉換為PDF/A格式。 若要這麼做，只要將您第一個端點所定義的watched資料夾的&#x200B;*result*&#x200B;資料夾設定為指向您第二個端點所定義的watched資料夾的&#x200B;*input*&#x200B;資料夾。

第一次轉換的輸出將轉至\path\result。 第二次轉換的輸入為\path\result，而第二次轉換的輸出會移至\path\result\result （或您在第二次轉換的「結果資料夾」方塊中定義的目錄）。

## 使用者如何與watched資料夾互動 {#how-users-interact-with-watched-folders}

對於watched資料夾端點，使用者可以從案頭複製或拖曳輸入檔案或資料夾到watched資料夾，以叫用。 系統會依檔案到達的順序來處理這些檔案。

對於watched資料夾端點，如果工作只需要一個輸入檔案，使用者可以將該檔案複製到watched資料夾的根目錄。

如果作業包含多個輸入檔案，使用者必須在包含所有必要檔案的watched資料夾階層之外建立資料夾。 這個新資料夾應該包含輸入檔案（如果處理序有需要，還可以選擇包含DDX檔案）。 在建構工作資料夾後，使用者將其複製到watched資料夾的輸入資料夾中。

>[!NOTE]
>
>確定應用程式伺服器已刪除watched資料夾中檔案的存取權。 如果AEM Forms在掃描檔案後無法從輸入資料夾中刪除檔案，則會無限期叫用關聯的程式。

## Watched資料夾輸出 {#watched-folder-output}

當輸入為資料夾且輸出包含多個檔案時，AEM forms會建立與輸入資料夾同名的輸出資料夾，並將輸出檔案複製到該資料夾中。 當輸出包含包含索引鍵/值組的檔案對映時（例如輸出程式的輸出），索引鍵會用作輸出檔案名稱。

端點程式產生的輸出檔案名稱不能包含字母、數字和句點(.)以外的字元 在副檔名之前。 AEM表單會將其他字元轉換為十六進位值。

使用者端應用程式會從watched資料夾結果資料夾中擷取結果檔案。 處理程式錯誤記錄在watched資料夾失敗資料夾中。

## Watched資料夾運作方式 {#how-watched-folder-works}

Watched資料夾模組包含下列服務：

* Watched資料夾服務
* provider.file_scan_service
* provider.file_write_results_service

除了上述服務之外，Watched Folder還依賴其他服務，包括用於排程工作的排程器服務，以及支援非同步呼叫目標服務的工作管理員服務。

### Watched資料夾如何處理呼叫要求 {#how-watched-folder-processes-an-invocation-request}

Watched資料夾服務可處理端點的建立、更新及刪除。 管理員建立端點後，會根據指定的重複間隔或cron運算式，將端點排程為由「排程器」服務觸發。

此圖表說明Watched資料夾如何處理呼叫要求。

![en_watchedfolder](assets/en_watchedfolder.png)

使用watched資料夾叫用服務的程式如下：

1. 使用者端應用程式會將檔案或資料夾置於watched資料夾輸入資料夾中。
1. 當作業掃描間隔發生時，排程器服務會呼叫provider.file_scan_service來處理輸入資料夾中的檔案或資料夾。
1. provider.file_scan_service會執行下列工作：


   * 掃描輸入資料夾中符合包含檔案模式的檔案或資料夾，並排除指定排除檔案模式的檔案或資料夾。 系統會先擷取最舊的檔案或資料夾。 系統會擷取早於等待時間的檔案和資料夾。 在一次掃描中，處理的檔案或資料夾數量取決於批次大小。 如需檔案模式的資訊，請參閱[關於檔案模式](configuring-watched-folder-endpoints.md#about-file-patterns)。 如需設定批次大小的相關資訊，請參閱[觀察資料夾服務設定](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings)。
   * 挑選要處理的檔案或資料夾。 如果檔案或資料夾未完全下載，則會在下次掃描時擷取它們。 為確保資料夾完全已下載，管理員應使用排除檔案模式建立具有名稱的資料夾。 在資料夾擁有所有檔案後，必須將其重新命名為包含檔案模式中指定的模式。 此步驟可確保資料夾具有叫用服務所需的所有必要檔案。 如需確保資料夾完全下載的詳細資訊，請參閱[觀看資料夾的秘訣與技巧](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders)。
   * 選取檔案或資料夾進行處理後，將其移至舞台資料夾。
   * 根據端點輸入引數對映，將stage資料夾中的檔案或資料夾轉換為適當的輸入。 如需輸入引數對應的範例，請參閱[觀察資料夾的提示與秘訣](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders)。


1. 系統會以同步或非同步方式叫用為端點設定的目標服務。 使用為端點設定的使用者名稱和密碼叫用目標服務。

   * 同步叫用會直接呼叫目標服務並立即處理回應。
   * 針對非同步叫用，會透過「作業管理員」服務呼叫目標服務，將請求置於佇列中。 「工作管理員服務」接著會呼叫provider.file_write_results_service來處理結果。

1. provider.file_write_results_service會處理目標服務呼叫的回應或失敗。 成功後，輸出會根據端點設定儲存到結果資料夾。 如果端點設定為在成功完成時保留結果，provider.file_write_results_service也會保留來源。

   當呼叫目標服務導致失敗時，provider.file_write_results_service會將失敗的原因記錄在failure.log檔案中，並將該檔案置於失敗資料夾中。 失敗資料夾是根據為端點指定的設定引數建立的。 當管理員為端點組態設定「失敗時保留」選項時，provider.file_write_results_service也會將來源檔案複製到失敗資料夾。 如需有關從失敗資料夾復原檔案的資訊，請參閱[失敗點與復原](configuring-watched-folder-endpoints.md#failure-points-and-recovery)。


## Watched資料夾端點設定 {#watched-folder-endpoint-settings}

使用下列設定來設定watched資料夾端點。

**名稱：** （必要）識別端點。 請勿包含&lt;字元，因為這會截斷Workspace中顯示的名稱。 如果您輸入URL作為端點的名稱，請確保其符合RFC1738中指定的語法規則。

**描述：**&#x200B;端點的描述。 請勿包含&lt;字元，因為這會截斷Workspace中顯示的說明。

**路徑：** （必要）指定watched資料夾位置。 在叢集環境中，此設定必須指向可以從叢集中的每台電腦存取的共用網路資料夾。

**非同步：**&#x200B;將呼叫型別識別為非同步或同步。 預設值為非同步。 建議將非同步處理用於長效處理作業，而建議將同步處理用於暫時性或短效處理作業。

**Cron運算式：**&#x200B;如果必須使用cron運算式排程watched資料夾，請輸入cron運算式。 設定此設定時，會忽略「重複間隔」。

**重複間隔：**&#x200B;掃描watched資料夾以進行輸入的間隔（以秒為單位）。 除非啟用「節流」設定，否則「重複間隔」應比處理平均作業的時間長；否則，系統可能會變得超載。 預設值為 5。如需詳細資訊，請參閱「批次大小」的說明。

**重複計數：**&#x200B;監看資料夾掃描資料夾或目錄的次數。 值–1表示無限掃描。 預設值為 -1。

**節流：**&#x200B;選取此選項時，它會限制AEM表單在任何指定時間處理的watched資料夾工作數目。 最大作業數由「批次大小」值決定。 （請參閱關於節流）。

**使用者名稱：** （必要）從watched資料夾叫用目標服務時使用的使用者名稱。 預設值為SuperAdmin。

**網域名稱：** （必要）使用者的網域。 預設值為DefaultDom。

**批次大小：**&#x200B;每次掃描要擷取的檔案或資料夾數目。 用於防止系統過載；一次掃描太多檔案可能會導致當機。 預設值為 2。

「重複間隔」和「批次大小」設定決定了Watched Folder在每次掃描中擷取的檔案數。 Watched資料夾使用Quartz執行緒集區來掃描輸入資料夾。 執行緒集區與其他服務共用。 如果掃描間隔很小，執行緒會經常掃描輸入資料夾。 如果檔案經常被拖放到watched資料夾中，則您應該將掃描間隔維持在較小的範圍內。 如果檔案不常捨棄，請使用較大的掃描間隔，讓其他服務可以使用執行緒。

如果有大量檔案被捨棄，請讓批次大小變大。 例如，如果由watched資料夾端點叫用的服務每分鐘可以處理700個檔案，而且使用者以相同的速率將檔案放入輸入資料夾，則將「批次大小」設定為350，並將「重複間隔」設定為30秒，將有助於Watched資料夾的效能，而不會產生經常掃描watched資料夾的成本。

當檔案被放入watched資料夾時，它會列出輸入中的檔案，如果每秒都進行掃描，這會降低效能。 增加掃描間隔可以改善效能。 如果捨棄的檔案量很小，請相應地調整「批次大小」和「重複間隔」。 例如，如果每秒丟棄10個檔案，請嘗試將「重複間隔」設定為1秒，並將「批次大小」設定為10。

**等待時間：**&#x200B;建立資料夾或檔案後，在掃描資料夾或檔案之前等待的時間（毫秒）。 例如，如果等待時間為3,600,000毫秒（一小時），且檔案是在一分鐘前建立的，則系統會在59分鐘或更長時間後擷取此檔案。 預設值為 0。

此設定對於確保檔案或資料夾完全複製到輸入資料夾非常有用。 例如，如果您有大型檔案要處理，且檔案下載需要10分鐘，請將等待時間設為10&amp;amp；ast；60&amp;amp；ast；1000毫秒。 這可防止watched資料夾掃描未滿十分鐘的檔案。

**排除檔案模式：**&#x200B;分號&#x200B;**；**&#x200B;分隔的模式清單，Watched資料夾會使用這些模式來決定要掃描和擷取的檔案和資料夾。 將不會掃描任何具有此模式的檔案或資料夾以進行處理。

當輸入是具有多個檔案的資料夾時，此設定非常有用。 資料夾的內容可以複製到資料夾中，其名稱會由watched資料夾擷取。 這可防止watched資料夾在資料夾完全複製到輸入資料夾之前擷取資料夾進行處理。

您可以使用檔案模式來排除：

* 具有特定副檔名的檔案；例如，&amp;amp；ast；.dat、&amp;amp；ast；.xml、&amp;amp；ast；.pdf。
* 具有特定名稱的檔案；例如，資料。&amp;amp；ast；會排除名為&#x200B;*data1*、*data2*&#x200B;等檔案和資料夾。
* 在名稱和副檔名中有複合運算式的檔案，如下列範例所示：

   * 資料[0-9][0-9][0-9]。[d][aA]&#39;連線埠&#39;
   * &amp;amp；ast；。[d][Aa]&#39;連線埠&#39;
   * &amp;amp；ast；。[Xx][毫米][Ll]

如需檔案模式的詳細資訊，請參閱[關於檔案模式](configuring-watched-folder-endpoints.md#about-file-patterns)。

**包含檔案模式：** （必要）分號&#x200B;**；**&#x200B;分隔的模式清單，Watched資料夾會使用這些模式來決定要掃描和擷取的資料夾和檔案。 例如，如果「包含檔案模式」是input&amp;amp；ast；，則會擷取符合input&amp;amp；ast；的所有檔案和資料夾。 這包括名為input1、input2等的檔案和資料夾。

預設值為&amp;amp；ast；，表示所有檔案和資料夾。

您可以使用檔案模式來包含：

* 具有特定副檔名的檔案；例如，&amp;amp；ast；.dat、&amp;amp；ast；.xml、&amp;amp；ast；.pdf。
* 具有特定名稱的檔案；例如，資料。&amp;amp；ast；會包含名為&#x200B;*data1*、*data2*&#x200B;等等的檔案和資料夾。
* 在名稱和副檔名中有複合運算式的檔案，如下列範例所示：

   * 資料[0-9][0-9][0-9]。[d][aA]&#39;連線埠&#39;
   * &amp;amp；ast；。[d][Aa]&#39;連線埠&#39;
   * &amp;amp；ast；。[Xx][毫米][Ll]

如需檔案模式的詳細資訊，請參閱[關於檔案模式](configuring-watched-folder-endpoints.md#about-file-patterns)。


**結果資料夾：**&#x200B;儲存結果的資料夾。 如果結果未出現在此資料夾中，請檢查失敗資料夾。 唯讀檔案不會處理，且會儲存在失敗資料夾中。 此值可以是具有以下檔案模式的絕對或相對路徑：

* %F =檔案名稱前置詞
* %E =副檔名
* %Y =年（完整）
* %y =年（最後兩位數）
* %M =月
* %D =日期
* %d =一年中的第幾天
* %H =小時（24小時時鐘）
* %h =小時（12小時時鐘）
* %m =分鐘
* %s =秒
* %l =毫秒
* %R =隨機數字（介於0-9之間）
* %P =處理程式或工作識別碼

例如，如果是2009年7月17日晚上8點，而您指定`C:/Test/WF0/failure/%Y/%M/%D/%H/`，則結果資料夾為`C:/Test/WF0/failure/2009/07/17/20`。

如果路徑不是絕對路徑而是相對路徑，則會在watched資料夾內建立資料夾。 預設值為result/%Y/%M/%D/，這是watched資料夾內的Result資料夾。 如需檔案模式的詳細資訊，請參閱[關於檔案模式](configuring-watched-folder-endpoints.md#about-file-patterns)。

>[!NOTE]
>
>結果資料夾的大小越小，Watched資料夾的效能就越好。 例如，如果watched資料夾的估計負載為每小時1000個檔案，請嘗試類似`result/%Y%M%D%H`的模式，以便每小時建立新的子資料夾。 如果負載較小（例如，每天1000個檔案），您可以使用類似`result/%Y%M%D`的模式。

**保留資料夾：**&#x200B;成功掃描及擷取檔案後，儲存檔案的位置。 路徑可以是絕對、相對或Null目錄路徑。 您可以使用檔案模式，如「結果資料夾」中所述。 預設值為preserve/%Y/%M/%D/。

**失敗資料夾：**&#x200B;儲存失敗檔案的資料夾。 此位置永遠是相對於watched資料夾。 您可以使用檔案模式，如「結果資料夾」中所述。

唯讀檔案不會處理，且會儲存在失敗資料夾中。

預設值為failure/%Y/%M/%D/。

**失敗時保留：**&#x200B;如果服務執行作業失敗，則保留輸入檔案。 預設值為true。

**覆寫重複的檔案名稱：**&#x200B;設定為True時，會覆寫結果資料夾和保留資料夾中的檔案。 設定為False時，名稱會使用具有數值索引尾碼的檔案和資料夾。 預設值為False。

**清除持續時間：** （必要）結果資料夾中的檔案和資料夾早於此值時會被清除。 此值以天為單位測量。 此設定對於確保結果資料夾不會填滿非常有用。

值為–1天表示絕不刪除結果資料夾。 預設值為 -1。

**作業名稱：** （必要）可指派給watched資料夾端點的作業清單。

**輸入引數對應：**&#x200B;用來設定處理服務與作業所需的輸入。 可用的設定視使用watched資料夾端點的服務而定。 以下是兩種輸入型別：

**常值：** Watched資料夾會使用顯示在欄位中輸入的值。 支援所有基本Java型別。 例如，如果API使用字串、long、int和Boolean等輸入，則字串會轉換為正確型別並叫用服務。

**變數：**&#x200B;輸入的值是watched資料夾用來挑選輸入的檔案模式。 例如，如果存在加密密碼服務，其中輸入檔案必須是PDF檔案，則使用者可以使用&amp;amp；ast；.pdf作為檔案模式。 Watched資料夾會擷取Watched資料夾中符合此模式的所有檔案，並叫用每個檔案的服務。 使用變數時，所有輸入檔案都會轉換為檔案。 僅支援使用Document作為輸入型別的API。

**輸出引數對應：**&#x200B;用來設定服務與作業的輸出。 可用的設定視使用watched資料夾端點的服務而定。

Watched資料夾輸出可以是單一檔案、檔案清單或檔案地圖。 然後這些輸出檔案會使用「輸出引數對應」中指定的模式儲存在結果資料夾中。

>[!NOTE]
>
>指定可產生唯一輸出檔案名稱的名稱，可改善效能。 例如，假設服務傳回了一個輸出檔案，輸出引數對應將其對應到`%F.%E` （輸入檔案的檔案名稱和副檔名）。 在此案例中，如果使用者每分鐘捨棄相同名稱的檔案，且結果資料夾設定為`result/%Y/%M/%D`，且[覆寫重複檔案名稱]設定為關閉，則Watched資料夾將嘗試解析重複的檔案名稱。 解析重複檔案名稱的程式可能會影響效能。 在此情況下，將輸出引數對應變更為`%F_%h_%m_%s_%l`可將小時、分鐘、秒和毫秒新增至名稱，或確保捨棄的檔案具有唯一名稱可改善效能。

## 關於檔案模式 {#about-file-patterns}

管理員可以指定可以叫用服務的檔案型別。 可以為每個watched資料夾建立多個檔案模式。 檔案模式可以是下列其中一個檔案屬性：

* 具有特定副檔名的檔案。 例如，&amp;amp；ast；.dat，&amp;amp；ast；.xml，&amp;amp；ast；.pdf
* 具有特定名稱的檔案。 例如，資料。&amp;amp；ast；
* 在名稱和副檔名中有複合運算式的檔案，如下列範例所示：

   * 資料[0-9][0-9][0-9]。[d][aA]&#39;連線埠&#39;
   * &amp;amp；ast；。[d][Aa]&#39;連線埠&#39;
   * &amp;amp；ast；。[Xx][毫米][Ll]

管理員可以定義儲存結果的輸出資料夾的檔案模式。 對於輸出資料夾（結果、保留和失敗），管理員可以指定下列任一檔案模式：

* %Y =年（完整）
* %y =年（最後兩位數）
* %M =月，
* %D =日期，
* %d =一年中的第幾天，
* %h =小時，
* %m =分鐘，
* %s =秒，
* %R =介於0到9之間的隨機數字
* %J =工作名稱

例如，結果資料夾的路徑可能是`C:\Adobe\Adobe_Experience_Manager_forms\BarcodedForms\%y\%m\%d`。

輸出引數對應也可以指定其他模式，例如：

* %F = Source檔案名稱
* %E = Source副檔名

如果輸出引數對應模式以「File.separator」（即路徑分隔符號）結尾，則會建立資料夾並將內容複製到該資料夾。 如果模式不是以「File.separator」結尾，則會以該名稱建立內容（結果檔案或資料夾）。 如需輸出引數對應的詳細資訊，請參閱[觀察資料夾的提示與秘訣](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders)。

## 關於節流 {#about-throttling}

為監看資料夾端點啟用節流時，會限制可在任何指定時間處理的監看資料夾工作數目。 作業的最大數量由「批次大小」值決定，此值也可在Watched資料夾端點中設定。 當達到節流限制時，不會輪詢watched資料夾輸入目錄中的傳入檔案。 檔案也會保留在輸入目錄中，直到其他watched資料夾工作完成且進行另一次輪詢嘗試為止。 如果有同步處理，即使作業在單一執行緒中連續處理，在單一輪詢中處理的所有作業都將計入節流限制中。

>[!NOTE]
>
>節流不會隨叢集縮放。 啟用節流時，叢集作為一個整體不會在任何指定時間處理超過批次大小中指定的作業數。 此限制是整個叢集，並非叢集中的每個節點所特有。 例如，當批次大小為2時，單一節點處理兩個作業即可達到節流限制，而其他節點則不會輪詢輸入目錄，直到其中一個作業完成為止。

### 節流如何運作 {#how-throttling-works}

Watched Folder會以每一個「重複間隔」掃描輸入資料夾，擷取在「批次大小」中指定的檔案數目，並叫用這些檔案的目標服務。 例如，如果「批次大小」為4，則每次掃描時，Watched Folder會挑選四個檔案、建立四個呼叫請求，然後呼叫目標服務。 在完成這些要求之前，如果叫用Watched資料夾，將會再次啟動4個工作，無論前4個工作是否已完成。

節流可防止Watched資料夾在先前工作未完成時叫用新工作。 Watched資料夾會偵測進行中的工作，並根據批次大小減去進行中的工作來處理新工作。 例如，在第二個叫用中，如果完成的工作只有三個，而一個工作仍在進行中，則Watched資料夾只會叫用另外三個工作。

* Watched資料夾取決於Stage資料夾中的檔案數目，以找出正在進行的工作數目。 如果stage資料夾中的檔案仍未處理，Watched資料夾將不會叫用任何其他工作。 例如，如果批次大小為四且三個工作已停止，則Watched Folder在後續呼叫中只會叫用一個工作。 有多個情況可能會導致stage資料夾中的檔案保持未處理狀態。 當工作停止時，管理員可以終止表單工作流程管理頁面上的程式，以便Watched Folder將檔案移出stage資料夾。
* 如果Forms伺服器在Watched Folder可以叫用工作之前關閉，管理員可以將檔案移出stage資料夾。 如需詳細資訊，請參閱[失敗點與復原](configuring-watched-folder-endpoints.md#failure-points-and-recovery)。
* 如果「工作管理員」服務回撥時，Forms伺服器正在執行，但「監看資料夾」並未執行（當服務未依順序啟動時就會發生回撥），管理員可以將檔案移出stage資料夾。 如需詳細資訊，請參閱[失敗點與復原](configuring-watched-folder-endpoints.md#failure-points-and-recovery)。


## 效能與擴充性 {#performance-and-scalability}

Watched資料夾可在單一節點上提供總計100個資料夾。 Watched資料夾的效能取決於Forms伺服器的效能。 對於非同步叫用，效能更取決於系統載入和「作業管理員」佇列中的作業。

Watched資料夾效能可藉由將節點新增至叢集來改善。 Watched資料夾工作會透過Quartz排程器散佈到叢集節點，而且如果有非同步要求，則由Job Manager服務散佈。 所有工作都會保留在資料庫中。

Watched資料夾依賴排程器服務來排程、取消排程和重新排程工作。 其他服務，例如「事件管理」服務、「使用者管理員」服務，以及「電子郵件提供者」服務，都可共用排程器服務執行緒集區。 這可能會影響Watched資料夾的效能。 當所有服務都開始使用排程器服務執行緒集區時，將需要對其進行調整。

## 叢集中的Watched資料夾 {#watched-folders-in-a-cluster}

在叢集中，Watched資料夾依賴於Quartz排程器和Job Manager服務來進行負載平衡和容錯移轉。 如需Quartz叢集行為的詳細資訊，請參閱[Quartz檔案](https://www.quartz-scheduler.org/documentation)。

Watched Folder會在每次輪詢時執行以下三個主要工作：

* 掃描資料夾
* 叫用目標服務
* 處理結果

負載平衡和容錯移轉行為會依據是否將watched資料夾設定為同步或非同步呼叫而變更。

### 叢集中的同步Watched資料夾 {#synchronous-watched-folder-in-a-cluster}

對於同步叫用，Quartz負載平衡器會決定哪個節點會取得輪詢事件。 取得輪詢事件的節點會執行所有工作：掃描資料夾、呼叫目標服務及處理結果。

![en_synchwatchedfoldercluster](assets/en_synchwatchedfoldercluster.png)

對於同步叫用，當一個節點失敗時，Quartz排程器會傳送新的輪詢事件到其他節點。 在失敗節點上啟動的呼叫將會遺失。 如需有關如何復原與失敗工作關聯的檔案的詳細資訊，請參閱[失敗點和復原](configuring-watched-folder-endpoints.md#failure-points-and-recovery)。


### 叢集中的非同步Watched資料夾 {#asynchronous-watched-folder-in-a-cluster}

對於非同步呼叫，Quartz負載平衡器會決定哪個節點會取得輪詢事件。 取得輪詢事件的節點會掃描輸入資料夾，並透過將要求放入工作管理員服務佇列來叫用目標服務。 工作管理員服務負載平衡器接著負責決定哪個節點將處理呼叫請求。 即使節點A建立了叫用請求，節點B最終還是會處理請求。 或者，啟動呼叫請求的節點最終也可能處理請求。

![en_asynchwatchedfoldercluster](assets/en_asynchwatchedfoldercluster.png)

對於非同步呼叫，當一個節點失敗時，Quartz排程器會傳送新的輪詢事件給其他節點。 在失敗節點上建立的呼叫要求會位於工作管理員服務佇列中，並傳送至其他節點進行處理。 未建立叫用要求的檔案將保留在stage資料夾中。 如需有關如何復原與失敗工作關聯的檔案的詳細資訊，請參閱[失敗點和復原](configuring-watched-folder-endpoints.md#failure-points-and-recovery)。


## 失敗點和復原 {#failure-points-and-recovery}

在每個輪詢事件中，Watched Folder會鎖定輸入資料夾，將符合包含檔案模式的檔案移動到stage資料夾，然後解除鎖定輸入資料夾。 需要鎖定，這樣兩個執行緒就不會擷取相同的檔案集並處理它們兩次。 較小的重複間隔和較大的批次大小會增加發生此情形的機會。 將檔案移至stage資料夾後，輸入資料夾會解除鎖定，以便其他執行緒可以掃描該資料夾。 此步驟有助於提供高輸送量，因為其他執行緒可以在一個執行緒處理檔案時進行掃描。

將檔案移至stage資料夾後，系統會為每個檔案建立叫用請求，並叫用目標服務。 Watched資料夾可能無法復原stage資料夾中的檔案：

* 如果伺服器在Watched Folder建立呼叫要求之前停止運作，stage資料夾中的檔案會保留在stage資料夾中，而且不會復原。
* 如果Watched Folder已成功地為stage資料夾中的每個檔案建立呼叫要求，而伺服器當機，則根據呼叫型別有兩種行為：

**同步：**&#x200B;如果Watched資料夾設定為同步叫用服務，stage資料夾中的所有檔案在stage資料夾中仍維持未處理狀態。

**非同步：**&#x200B;在此案例中，Watched資料夾依賴工作管理員服務。 如果「工作管理員服務」回撥Watched資料夾，系統會根據呼叫結果，將stage資料夾中的檔案移至preserve或failure資料夾。 如果「工作管理員」服務沒有回撥Watched資料夾，則暫存資料夾中的檔案將維持未處理狀態。 當Watched資料夾未執行時，作業管理員回撥時，就會發生這種情況。

### 正在復原stage資料夾中未處理的來源檔案 {#recovering-unprocessed-source-files-in-the-stage-folder}

當Watched資料夾無法處理階段資料夾中的來源檔案時，您可以復原未處理的檔案。

1. 重新啟動應用程式伺服器或節點。
1. （選擇性）停止Watched資料夾處理新的輸入檔案。 如果您略過此步驟，將更難判斷哪些檔案會在階段資料夾中未經處理。 若要防止Watched資料夾處理新的輸入檔案，請執行下列其中一項工作：

   * 在應用程式和服務中，將watched資料夾端點的Include File Pattern引數變更為不符合任何新輸入檔案的引數（例如，輸入`NOMATCH`）。
   * 暫停建立新輸入檔案的處理。

   等候AEM表單復原並處理所有檔案。 大多數檔案應該會復原，任何新輸入檔案都會正確處理。 您等待Watched資料夾復原及處理檔案的時間長度將取決於要叫用的作業長度和要復原的檔案數目。

1. 判斷哪些檔案無法處理。 如果您已等待適當的時間且已完成上一步驟，而中繼資料夾中仍留有未處理的檔案，請前往下一步。

   >[!NOTE]
   >
   >您可以檢視階段目錄中檔案的日期和時間戳記。 根據檔案數量和正常處理時間，您可以確定哪些檔案的年齡足以被視為卡住。

1. 將未處理的檔案從stage目錄複製到輸入目錄。
1. 如果您在步驟2中阻止Watched資料夾處理新的輸入檔案，請將「包含檔案模式」變更為先前的值，或重新啟用您停用的程式。

## watched資料夾的安全性考量 {#security-considerations-for-watched-folders}

每個watched資料夾都設定了使用者名稱和密碼。 叫用服務時會使用這些認證。 Watched資料夾仰賴共用資料夾受到基礎安全性檔案系統的保護，因此只有watched資料夾的擁有者才能存取共用資料夾。

## watched資料夾的提示與秘訣 {#tips-and-tricks-for-watched-folders}

以下是設定Watched資料夾端點時的一些秘訣和技巧：

* 如果您在Windows上有處理影像檔案的watched資料夾，請為「包含檔案模式」或「排除檔案模式」選項指定值，以防止Windows自動產生的Thumbs.db檔案被watched資料夾輪詢。
* 如果指定cron運算式，則會忽略重複間隔。 cron運算式的使用是根據Quartz開放原始碼工作排程系統1.4.0版。
* 批次大小是每次掃描watched資料夾時所擷取的檔案或資料夾數目。 如果批次大小設為2個，然後將10個檔案或資料夾放入watched資料夾輸入資料夾中，則每次掃描只會擷取2個檔案或資料夾。 下次掃描（將在重複間隔中指定的時間後進行）時，將會擷取下兩個檔案。
* 對於檔案模式，管理員可以指定已新增支援萬用字元模式的規則運算式，以指定檔案模式。 Watched資料夾修改規則運算式以支援萬用字元模式，例如&amp;amp；ast；。&amp;amp；ast；或&amp;amp；ast；.pdf。 規則運算式不支援這些萬用字元模式。
* Watched Folder會掃描輸入資料夾以取得輸入，並且不知道來源檔案或資料夾是否已完整複製到輸入資料夾中，然後再開始處理檔案或資料夾。 若要確保在擷取檔案或資料夾之前，將來源檔案或資料夾完全複製到watched資料夾的輸入資料夾，請執行下列工作：

   * 使用等待時間，這是Watched資料夾從上次修改時間開始等待的時間（毫秒）。 如果您有大型檔案要處理，請使用此功能。 例如，如果檔案需要10分鐘下載，請將等待時間指定為10&amp;amp；ast；60&amp;amp；ast；1000毫秒。 這會讓Watched Folder無法擷取在10分鐘以內的檔案。
   * 使用排除檔案模式與包含檔案模式。 例如，如果排除檔案模式為`ex*`且包含檔案模式為`in*`，Watched資料夾將會挑選以「in」開頭的檔案，而不會挑選以「ex」開頭的檔案。 若要複製大型檔案或資料夾，請先重新命名檔案或資料夾，使名稱以「ex」開頭。 將名為「ex」的檔案或資料夾完整複製到watched資料夾後，將其重新命名為「in&amp;amp；ast；」。

* 使用清除持續時間保持結果資料夾乾淨。 Watched Folder會清除所有超過清除期間中提及之期間的檔案。 持續時間以天為單位。
* 新增Watched資料夾端點時，在選取作業名稱之後，會填入輸入引數對應。 對於操作的每個輸入，都會產生一個輸入引數對應欄位。 以下是輸入引數對應的範例：

   * 針對`com.adobe.idp.Document`輸入：如果服務作業具有型別`Document`的輸入，則管理員可以將對應型別指定為`Variable`。 Watched資料夾會根據指定給輸入引數的檔案模式，從watched資料夾的輸入資料夾擷取輸入。 如果管理員指定`*.pdf`作為引數，則會擷取每個副檔名為.pdf的檔案，並轉換成`com.adobe.idp.Document`，然後叫用服務。
   * 針對`java.util.Map`輸入：如果服務作業有型別`Map`的輸入，管理員可以將對應型別指定為`Variable`，並輸入模式如`*.pdf`的對應值。 例如，服務需要兩個`com.adobe.idp.Document`物件的對映，這些物件代表輸入資料夾（例如1.pdf和2.pdf）中的兩個檔案。 Watched資料夾將建立以索引鍵做為檔案名稱，且值做為為`com.adobe.idp.Document`的對應。
   * 針對`java.util.List`輸入：如果服務作業具有型別List的輸入，則管理員可以將對應型別指定為`Variable`，並輸入模式如`*.pdf`的對應值。 將PDF檔案放入輸入資料夾時，Watched Folder會建立代表這些檔案的`com.adobe.idp.Document`物件清單，並叫用目標服務。
   * 針對`java.lang.String`：管理員有兩個選項。 首先，管理員可以將對應型別指定為`Literal`，並將對應值輸入為字串，例如`hello.` Watched Folder將使用字串`hello`叫用服務。 第二，管理員可以將對應型別指定為`Variable`，並輸入模式如`*.txt`的對應值。 在後一種情況下，副檔名為.txt的檔案會讀取為檔案，並以字串形式強制來叫用服務。
   * Java基本型別：管理員可以將對應型別指定為`Literal`並提供值。 Watched資料夾會以指定的值叫用服務。

* Watched資料夾用於處理檔案。 支援的輸出為`com.adobe.idp.Document`、`org.w3c.Document`、`org.w3c.Node`，以及這些型別的清單和地圖。 任何其他型別都會導致失敗資料夾中的失敗輸出。
* 如果結果不在結果資料夾中，請驗證失敗資料夾以檢視是否發生失敗。
* Watched資料夾在非同步模式下使用時效果最佳。 在此模式中，Watched資料夾會將呼叫要求放入佇列並回撥。 然後會非同步處理佇列。 如果未設定「非同步」選項，Watched Folder會同步叫用目標服務，而Process Engine會等到服務完成要求並產生結果為止。 如果目標服務需要很長時間來處理請求，Watched資料夾可能會發生逾時錯誤。
* 建立watched資料夾以進行匯入和匯出作業時，無法擷取副檔名。 使用watched資料夾叫用Form Data Integration Service時，輸出檔案的副檔名型別可能與檔案物件型別的預期輸出格式不符。 例如，如果呼叫匯出作業之watched資料夾的輸入檔案是包含資料的XFA表單，則輸出應該是XDP資料檔案。 若要取得具有正確副檔名的輸出檔案，您可以在輸出引數對應中指定它。 在此範例中，您可以使用%F.xdp作為輸出引數對應。
* Watched Folder可能會先處理輸入檔案，然後才將其完全複製到資料夾。 在UNIX上不強制鎖定檔案，因為在Windows上也是如此。 因此，當檔案被複製到watched資料夾時，Watched資料夾可能會將檔案移動到舞台，而不等待檔案複製完成。 此行為只會造成輸入檔案的一部分被處理。 目前有兩個因應措施：

   * 因應措施1

      1. 指定「排除檔案模式」的模式，例如temp&amp;amp；ast；.ps。
      1. 將以temp開頭的檔案（例如temp1.ps）複製到watched資料夾。
      1. 將檔案完全複製到watched資料夾後，重新命名檔案以對應於「包含檔案模式」指定的模式。 Watched Folder然後將完成的檔案移至舞台。

   * 因應措施2

     如果您知道將檔案複製到watched資料夾所需的最大時間長度，請指定「等待時間」的時間（以秒為單位）。 接著，Watched資料夾會等待指定的時間長度，再將檔案移至舞台。

     這不是Windows上的檔案問題，因為Windows會在寫入執行緒時鎖定檔案。 不過，這是Windows資料夾的問題。 針對資料夾，您必須依照因應措施1中的步驟操作。

* 如果Watched資料夾的「保留資料夾名稱」端點屬性設定為Null目錄路徑，則不會清除暫存目錄。 目錄仍包含已處理的檔案和暫存資料夾。

## Watched資料夾的服務特定建議 {#service-specific-recommendations-for-watched-folders}

對於所有服務，您應該調整watched資料夾的批次大小和重複間隔，以便Watched資料夾擷取新檔案和資料夾進行處理的速率，不會超過AEM Forms伺服器可以處理的工作速率。 實際使用的引數可能會有所不同，這取決於設定的watched資料夾數目、使用之watched資料夾的服務，以及處理器上的工作強度。

### 產生PDF服務建議 {#generate-pdf-service-recommendations}

* 「產生PDF」服務一次只能轉換下列檔案型別的一個檔案： Microsoft Word、Microsoft Excel、Microsoft PowerPoint、Microsoft Project、AutoCAD、Adobe Photoshop®、Adobe FrameMaker®和AdobePageMaker®。 這些是長時間執行的工作；因此，請務必將批次大小保持在低設定。 如果叢集中有更多節點，也請增加重複間隔。
* 針對PostScript (PS)、Encapsulated PostScript (EPS)和影像檔案型別，產生PDF服務可同時處理多個檔案。 您應該根據伺服器的容量和叢集中的節點數目，仔細調整階段作業Bean集區大小（控制將同時進行的轉換數目）。 然後，將批次大小增加至一個數字，該數字等於您嘗試轉換的檔案型別的工作階段Bean池大小。 輪詢頻率應該由叢集中的節點數決定；但是，由於「產生PDF」服務處理這些型別的作業的速度相當快，因此您可以將重複間隔設定為較低的值，例如5或10。
* 即使「產生PDF」服務一次只能轉換一個OpenOffice檔案，轉換速度還是相當快。 PS、EPS和影像轉換的上述邏輯也適用於OpenOffice轉換。
* 若要在叢集中啟用均勻負載分佈，請保持批次大小為低並增加重複間隔。

### 條碼式表單服務建議 {#barcoded-forms-service-recommendations}

* 為了在處理條碼式表單（小型檔案）時獲得最佳效能，請輸入`10`作為「批次大小」，輸入`2`作為「重複間隔」。
* 將許多檔案放在輸入資料夾中時，可能會發生名為&#x200B;*thumbs.db*&#x200B;的隱藏檔案錯誤。 因此，建議您將include檔案的Include File Pattern設定為與指定給輸入變數（例如，`*.tiff`）的值相同。 這會防止Watched資料夾處理DB檔案。
* 批次大小值為`5`且重複間隔為`2`通常就足夠了，因為條碼式Forms服務通常需要約0.5秒來處理一個條碼。
* Watched Folder不會等待Process Engine完成工作，然後才挑選新的檔案或資料夾。 它會持續掃描watched資料夾並叫用目標服務。 此行為可能會導致引擎過載，造成資源問題和逾時。 請確定您使用重複間隔和批次大小來節流Watched資料夾輸入。 如果存在更多觀察資料夾或啟用端點節流功能，您可以增加重複間隔並降低批次大小。 如需節流的相關資訊，請參閱[關於節流](configuring-watched-folder-endpoints.md#about-throttling)。
* Watched資料夾模擬使用者名稱和網域名稱中指定的使用者。 如果直接叫用或處理程式是短期的，Watched資料夾會叫用此使用者身分的服務。 對於長時間的流&#39;b5&#39;7b，該流&#39;b5&#39;7b會與「系統」前後關聯一起叫用。 管理員可以設定Watched資料夾的作業系統原則，以決定允許或拒絕存取的使用者。
* 使用檔案模式來組織結果、失敗和保留資料夾。 （請參閱[關於檔案模式](configuring-watched-folder-endpoints.md#about-file-patterns)。）

* Watched資料夾依賴Quartz排程器掃描watched資料夾。 Quartz排程器有執行緒集區來掃描它們。 如果watched資料夾的重複間隔非常低（&lt; 5秒）且批次大小高(> 2)，就可能發生競爭條件。 發生這種情況時，會有兩個石英執行緒擷取一個檔案：

   * 其中一個執行緒成功找到檔案，並叫用該檔案的目標服務。
   * 第二個執行緒會看到檔案，但嘗試找出檔案是否有效時失敗（讀取或寫入檔案），這會造成錯誤失敗，指出檔案因唯讀而無法處理。 只有低重複間隔和高批次大小時才會發生這種情況。
