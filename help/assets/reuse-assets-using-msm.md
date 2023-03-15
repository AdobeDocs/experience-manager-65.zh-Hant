---
title: 使用 MSM 重複使用資產
description: 在衍生自父資產並連結至父資產的多個頁面/資料夾中使用資產。 資產會與主要副本保持同步，只要按幾下，就會從父資產接收更新。
contentOwner: AG
mini-toc-levels: 1
role: User, Admin, Architect
feature: Asset Management,Multi Site Manager
exl-id: 4d0367c4-88aa-4aef-b23d-828609b0df09
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '3401'
ht-degree: 10%

---

# 使用MSM重複使用資產 [!DNL Assets] {#reuse-assets-using-msm-for-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/reuse-assets-using-msm.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/using/reuse-assets-using-msm.html?lang=en) |

中的Multi Site Manager(MSM)功能 [!DNL Adobe Experience Manager] 可讓使用者重複使用一次撰寫的內容，並在多個Web位置間重複使用。 數位資產與MSM之數位資產相同 [!DNL Assets] 功能。 將MSM用於 [!DNL Assets]，您可以：

* 只需建立資產一次，然後複製這些資產，以便在網站的其他區域重複使用。
* 保持多個副本同步，並更新一次原始主副本以將更改推送到子副本。
* 暫時或永久暫停父資產和子資產之間的連結，以進行本機變更。

## 必備條件 {#prereq}

使用MSM以 [!DNL Assets]，至少安裝 [!DNL Experience Manager] 6.5 Service Pack 1。 如需詳細資訊，請參閱 [最新service pack發行說明](/help/release-notes/release-notes.md).

## 了解優點和概念 {#concepts}

### 運作方式與優點 {#how-it-works-and-the-benefits}

若要了解在多個Web位置重複使用相同內容（文字和資產）的使用案例，請參閱 [可能的MSM情況](/help/sites-administering/msm.md). [!DNL Experience Manager] 維護原始資產與其連結副本之間的連結，稱為即時副本(LC)。 維護的連結可將集中的變更推送至多個即時副本。 這樣可以更快地更新，同時消除管理重複副本的限制。 變更的傳播是無誤的，是集中的。 此功能允許儲存受選定即時副本限制的更新空間。 使用者可以分離連結（即中斷繼承），並進行下次更新主副本並執行變更時不會覆寫的本機編輯。 您可以對一些選取的中繼資料欄位或整個資產進行分離。 它允許靈活地在本機更新原來繼承自主副本的資產。

MSM會維護來源資產與其即時副本之間的即時關係，以便：

* 對來源資產的變更也會套用（轉出）至即時副本，即即時副本會與來源同步。
* 您可以暫停即時關係以更新即時副本，或移除少數有限欄位的繼承。 對來源的修改不再套用至即時副本。

### MSM辭匯表 [!DNL Assets] 條款 {#glossary}

**來源：** 原始資產或資料夾。 從中派生即時副本的主副本。

**即時副本：** 與其來源同步的來源資產/資料夾復本。 Live Copy可以是更多Live Copy的源。 了解如何建立LC。

**繼承：** 即時副本資產/資料夾與其來源之間的連結/參考，系統會使用此連結/參考來記住要將更新傳送至何處。 中繼資料欄位的繼承存在於精細的層級。 可以為選擇性中繼資料欄位移除繼承，同時保留來源與其即時副本之間的即時關係。

**轉出：** 將對來源所做的修改推送到下游的Live Copy的動作。 可以使用轉出動作，一次更新一或多個即時副本。 請參閱轉出。

**轉出設定：** 決定要同步哪些屬性、同步方式和同步時間的規則。 建立Live Copy時會套用這些設定；可稍後編輯；子項可從其父項資產繼承轉出設定。 針對MSM [!DNL Assets]，僅使用標準轉出設定。 其他轉出設定不適用於MSM [!DNL Assets].

**同步：** 除了轉出以外，還有另一個動作，可將更新從來源傳送至即時副本，借此在來源與其即時副本之間取得平衡。 系統會起始特定即時副本的同步作業，且動作會從來源提取變更。 使用此動作，只能更新其中一個即時副本。 請參閱同步操作。

**暫停：** 暫時移除即時副本與其來源資產/資料夾之間的即時關係。 你可以恢復關係。 請參閱暫停動作。

**繼續：** 繼續即時關係，讓即時副本再次開始從來源接收更新。 請參閱繼續動作。

**重設：** 重置操作通過覆蓋任何本地更改使即時副本再次成為源的副本。 它也會移除繼承取消，並重設所有中繼資料欄位的繼承。 若要日後進行本機修改，您必須再次取消特定欄位的繼承。 請參閱LC的本機修改。

**分離：** 不可撤回地移除即時副本資產/資料夾的即時關係。 分離操作後，即時副本永遠不會接收來自源的更新，並且不再是即時副本。 請參閱刪除關係。

## 建立資產的即時副本 {#createlc}

若要從一或多個來源資產或資料夾建立即時副本，請遵循下列其中一項操作：

* 方法1:選取來源資產，然後按一下 **[!UICONTROL 建立]** > **[!UICONTROL Live Copy]** 的上界。
* 方法2:在 [!DNL Experience Manager] 使用者介面，按一下 **[!UICONTROL 建立]** > **[!UICONTROL Live Copy]** 從介面的右上角。

您可以一次建立資產或資料夾的即時副本。 您可以建立衍生自資產或即時副本本身之資料夾的即時副本。 使用案例不支援內容片段(CF)。 嘗試建立其Live Copy時，CF會照原樣複製，沒有任何關係。 複製的CF是及時的快照，在更新原始CF時不會更新。

若要使用第一個方法建立Live Copy，請執行下列步驟：

1. 選取來源資產或資料夾。 在工具列中，按一下 **[!UICONTROL 建立]** > **[!UICONTROL Live Copy]**.

   ![從建立即時副本 [!DNL Experience Manager] 介面](assets/create_lc1.png)

   *圖：從建立即時副本 [!DNL Experience Manager] 介面。*

1. 選擇目標資料夾。 按一下&#x200B;**[!UICONTROL 下一步]**。
1. 提供標題和名稱。 資產沒有子項。 建立資料夾的即時副本時，您可以選擇包含或排除子項。
1. 選取轉出設定。 按一下&#x200B;**[!UICONTROL 建立]**。

若要使用第二種方法建立即時副本，請依照下列步驟操作：

1. 在 [!DNL Experience Manager] 介面，按一下右上角 **[!UICONTROL 建立]** > **[!UICONTROL Live Copy]**.

   ![從建立即時副本 [!DNL Experience Manager] 介面](assets/create_lc2.png)

   *圖：從建立即時副本 [!DNL Experience Manager] 介面。*

1. 選取來源資產或資料夾。 按一下&#x200B;**[!UICONTROL 下一步]**。
1. 選擇目標資料夾。 按一下&#x200B;**[!UICONTROL 下一步]**。
1. 提供標題和名稱。 資產沒有子項。 建立資料夾的即時副本時，您可以選擇包含或排除子項。
1. 選取轉出設定。 按一下&#x200B;**[!UICONTROL 建立]**。

>[!NOTE]
>
>移動源或即時副本時，將保留關係。 刪除即時副本時，將刪除關係。

## 查看源副本和即時副本的各種屬性和狀態 {#properties}

您可以從 [!DNL Experience Manager] 使用者介面。

下列兩種方法適用於資產和資料夾：

* 選取即時複製資產，並在其「屬性」頁面中尋找資訊。
* 選擇源資料夾，並從 [!UICONTROL 即時副本主控台].

>[!TIP]
>
>若要檢查幾個個別即時副本的狀態，請使用第一個方法來檢查 **[!UICONTROL 屬性]** 頁面。 若要檢查多個即時副本的狀態，請使用第二個方法來檢查 **[!UICONTROL 關係狀態]** 頁面。

### 即時副本的資訊和狀態 {#statuslcasset}

若要檢查即時副本資產或資料夾的資訊和狀態，請遵循下列步驟。

1. 選取即時複製資產或資料夾。 按一下 **[!UICONTROL 屬性]** 的上界。 或者，使用鍵盤快速鍵 `p`.
1. 按一下 **[!UICONTROL Live Copy]**. 您可以檢查來源的路徑、暫停狀態、同步狀態、上次轉出日期，以及上次轉出的使用者。

   ![即時副本資訊和狀態會顯示在「屬性」的控制台中](assets/lcfolder_info_properties.png)

   *圖：即時副本資訊和狀態。*

1. 如果子資產借用即時副本設定，您可以啟用或停用。

1. 您可以選擇即時副本的選項，以繼承父項的轉出設定或變更設定。

### 資料夾所有即時副本的資訊和狀態 {#status-lc-folder}

[!DNL Experience Manager] 提供一個控制台，用於檢查源資料夾的所有即時副本的樣式。 此主控台會顯示所有子資產的狀態。

1. 選擇源資料夾。 按一下 **[!UICONTROL 屬性]** 的上界。 或者，使用鍵盤快速鍵 `p`.
1. 按一下「 **[!UICONTROL 即時複製來源」]**。若要開啟主控台，請按一下「即 **[!UICONTROL 時複製概述」]**。此控制面板提供所有子資產的頂層狀態。

   ![在源的Live Copy控制台中查看Live Copy的狀態](assets/livecopy-statuses.png)

   *圖：在中檢視即時副本的狀態 [!UICONTROL 即時副本主控台] 源。*

1. 若要檢視即時副本檔案夾中每個資產的詳細資訊，請選取資產，然後從工具列按一 **[!UICONTROL 下「關係狀態]** 」。

   ![資料夾中即時副本子資產的詳細資訊和狀態](assets/livecopy_relationship_status.png)

   資料夾中即時副本子資產的詳細資訊和狀態

>[!TIP]
>
>您可以快速查看其他資料夾的即時副本狀態，而無需瀏覽太多。 從 **[!UICONTROL 即時副本概述]** 介面。

### 從「參考」(References)邊欄為源執行快速操作 {#refrailsource}

對於來源資產或資料夾，您可以看到下列資訊，並直接從「參考」邊欄採取下列動作：

* 請參閱Live Copy的路徑。
* 在中開啟或顯示特定即時副本 [!DNL Experience Manager] 使用者介面。
* 將更新同步到特定的即時副本。
* 暫停關係或變更特定即時副本的轉出設定。
* 存取即時副本概述主控台。

選取來源資產或資料夾，開啟左側邊欄，然後按一下 **[!UICONTROL 參考]**. 或者，選取資產或檔案夾，然後使用鍵盤快速鍵 `Alt + 4`。

![「參考」(References)邊欄中所選源的可用操作和資訊](assets/referencerail_source.png)

*圖：「參考」(References)邊欄中所選源的可用操作和資訊。*

若為特定即時副本，請按一下 **[!UICONTROL 編輯即時副本]** 暫停關係或變更轉出設定。

![對於特定即時副本，選取來源資產時，可從「參考」邊欄存取暫停關係或變更轉出設定的選項](assets/referencerail_editlc_options.png)

*圖：暫停關係或變更特定即時副本的轉出設定。*

### 從「參考」邊欄快速動作即時副本 {#ref-rail-lc}

若為即時複製資產或資料夾，您可以看到下列資訊，並直接從「參考」邊欄採取下列動作：

* 查看源的路徑。
* 在中開啟或顯示特定即時副本 [!DNL Experience Manager] 使用者介面。
* 推出更新。

選取即時複製資產或資料夾，開啟左側導軌，然後按一下「參 **[!UICONTROL 考」]**。或者，選取資產或檔案夾，然後使用鍵盤快速鍵 `Alt + 4`。

![在「參考」(References)邊欄中，所選即時副本的可用動作](assets/referencerail_livecopy.png)

*圖：在「參考」(References)邊欄中，所選即時副本的可用動作。*

## 將修改從來源傳播至即時副本 {#rolloutsync}

修改來源後，變更可以透過同步動作或轉出動作傳播至即時副本。 若要了解這兩個動作之間的差異，請參閱 [字彙表](#glossary).

### 轉出動作 {#rollout}

您可以從來源資產啟動轉出動作，並更新所有或部分選取的即時副本。

1. 選取即時複製資產或資料夾。 按一下 **[!UICONTROL 屬性]** 的上界。 或者，使用鍵盤快速鍵 `p`.
1. 按一下「 **[!UICONTROL 即時複製來源」]**。按一下 **[!UICONTROL 轉出]** 的上界。
1. 選取您要更新的即時副本。 按一下 **[!UICONTROL 轉出]**.
1. 若要轉出對子資產進行的更新，請選取 **[!UICONTROL 轉出來源和所有子項]**.

   ![將來源修改轉出為幾個或所有即時副本](assets/livecopy_rollout_page.png)

   *圖：將來源修改轉出為幾個或所有即時副本。*

>[!NOTE]
>
>在來源資產中所做的修改只會推出至直接相關的即時副本。 如果即時副本衍生自另一個即時副本，則修改不會轉出至衍生的即時副本。

或者，您也可以在選取特定即時副本後，從「參考」邊欄起始轉出動作。 如需詳細資訊，請參閱 [從「參考」邊欄快速動作即時副本](#ref-rail-lc). 在此轉出方法中，只會更新選取的即時副本及其子項（選擇性）。

![將來源修改轉出至所選即時副本](assets/livecopy_rollout_dialog.png)

*圖：將來源修改轉出至所選即時副本。*

### 關於同步操作 {#about-sync}

同步操作只會將修改從源提取到所選的即時副本。 同步動作會尊重並維護取消繼承後完成的本機修改。 不會覆寫本機修改，且取消的繼承不會重新建立。 您可以透過三種方式啟動同步動作。

| 其中 [!DNL Experience Manager] 介面 | 使用時機和原因 | 如何使用 |
|---|---|---|
| [!UICONTROL 參考] 邊欄 | 已選擇源時，快速同步。 | 請參閱 [從「參考」(References)邊欄為源執行快速操作](#refrailsource) |
| 工具列 [!UICONTROL 屬性] 頁面 | 在您已開啟即時副本屬性時啟動同步。 | 請參閱 [同步即時副本](#sync-lc) |
| [!UICONTROL 即時副本概述] 主控台 | 選取來源資料夾或 [!UICONTROL 即時副本概述] 主控台已開啟。 一次會針對一個資產起始同步動作，但是這是一次就多個資產同步的更快方式。 | 請參閱 [對即時副本資料夾中的許多資產執行的動作](#bulk-actions) |

### 同步即時副本 {#sync-lc}

若要啟動同步動作，請開啟即 **[!UICONTROL 時副本的「屬性]** 」頁面，按一下「即時 **** 副本」，然後從工具列按一下所要的動作。

要查看與同步操作相關的狀態和資訊，請參 [閱即時副本的資訊和狀態](#statuslcasset)[以及資料夾所有即時副本的狀態](#status-lc-folder)。

![同步操作提取對源所做的更改](assets/livecopy_sync.png)

*圖：同步操作提取對源所做的更改。*

>[!NOTE]
>
>如果掛起關係，則工具欄中不提供同步操作。 雖然「參考」邊欄中有同步動作可用，但即使成功轉出，修改也不會傳播。

## 暫停和恢復關係 {#suspend-resume}

您可以暫時暫停關係，以防止即時副本收到對來源資產或資料夾所做的修改。 也可以恢復關係，以便即時副本開始從來源接收修改。

若要暫停或繼續，請開啟即 **[!UICONTROL 時副本的「屬性]** 」頁面，按一下「即時副本 **** 」，然後從工具列按一下所要的動作。

或者，您也可以從即時副本概述主控台，快速暫停或繼續即時副本資料夾中多 **[!UICONTROL 個資產的關係]** 。請參 [閱對即時副本資料夾中的許多資產採取動作](#bulk-actions)。

## 對即時副本進行本機修改 {#local-mods}

Live Copy是建立原始源時的副本。 即時副本的中繼資料值繼承自來源。 中繼資料欄位個別地維護與來源資產之個別欄位的繼承。

不過，您有彈性對即時副本進行本機修改，以變更一些選取的屬性。若要進行本機修改，請取消所要屬性的繼承。當取消一個或多個元資料欄位的繼承時，保留資產的即時關係和其它元資料欄位的繼承。任何同步或轉出都不會覆寫本機修改。要執行此操作，請開啟 **[!UICONTROL 屬性]** 即時副本資產的頁面，按一下 **[!UICONTROL 取消繼承]** 中繼資料欄位旁的選項。

您可以還原所有本機修改，並將資產還原為其來源狀態。 不可撤銷且立即重設動作，會覆寫所有本機修改，並重新建立所有中繼資料欄位的繼承。 若要回復，請從 **[!UICONTROL 屬性]** 即時復本資產的頁面，按一下 **[!UICONTROL 重設]** 的上界。

![「重設」動作會覆寫本機編輯內容，並將即時副本部分與其來源連結。](assets/livecopy_reset.png)

*圖：「重設」動作會覆寫本機編輯內容，並將即時副本部分與其來源連結。*

## 移除即時關係 {#detach}

您可以使用「分離」操作完全刪除源和即時副本之間的關係。 分離即時副本後，即時副本會變成獨立資產或資料夾。 它會顯示為 [!DNL Experience Manager] 介面，分離後立即執行。 要從源分離即時副本，請執行以下步驟。

1. 選取即時複製資產或資料夾。 按一下 **[!UICONTROL 屬性]** 的上界。 或者，使用鍵盤快速鍵 `p`.

1. 按一下 **[!UICONTROL Live Copy]**. 按一下 **[!UICONTROL 分離]** 的下一頁。 按一下 **[!UICONTROL 分離]** 從對話框。

   ![「分離」操作完全刪除了源副本和即時副本之間的關係](assets/livecopy_detach.png)

   *圖：「分離」操作完全刪除了源副本和即時副本之間的關係。*

   >[!CAUTION]
   >
   >當您按一下「 **[!UICONTROL 分離]** 對話框。 您無法按一下「 **[!UICONTROL 取消]** （在「屬性」頁面上）。

或者，您也可以從 **[!UICONTROL 即時副本概述]** 控制台。 請參 [閱對即時副本資料夾中的許多資產採取動作](#bulk-actions)。

## 即時副本資料夾中的大量動作 {#bulk-actions}

如果即時副本資料夾中有多個資產，對每個資產啟動動作可能會相當繁瑣。 您可以快速對許多資產啟動基本動作，方法是 [!UICONTROL 即時副本主控台]. 上述方法仍適用於個別資產。

1. 選擇源資料夾。 按一下 **[!UICONTROL 屬性]** 的上界。 或者，使用鍵盤快速鍵 `p`.
1. 按一下「 **[!UICONTROL 即時複製來源」]**。若要開啟主控台，請按一下「即 **[!UICONTROL 時複製概述」]**。
1. 在此控制面板中，從即時複製資料夾選取即時複製資產。從工具列按一下所需的動作。可用的操作有 **[!UICONTROL 同步]**、重置 **[!UICONTROL 、]**&#x200B;掛起 ****&#x200B;和 ****&#x200B;分離。您可以對與所選來源資料夾處於即時關係的任何即時副本資料夾中的任何資產快速啟動這些動作。

   ![從即時副本概述主控台輕鬆更新即時副本資料夾中的許多資產](assets/livecopyconsole_update_many_assets.png)

   *圖：輕鬆更新即時副本資料夾中的許多資產， [!UICONTROL 即時副本概述] 控制台。*

## 為 [!DNL Assets] {#extend-api}

[!DNL Experience Manager] 可讓您使用MSM Java API擴充功能。 針對 [!DNL Assets]，延伸功能與搭配MSM運作的功能相同 [!DNL Sites]. 如需詳細資訊，請參閱 [擴充MSM](/help/sites-developing/extending-msm.md) 以及下列項目，以了解特定工作的資訊：

* [API概觀](/help/sites-developing/extending-msm.md#overview-of-the-java-api)
* [建立同步動作](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)
* [建立轉出設定](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration)
* [建立和使用簡單的LiveActionFactory類](/help/sites-developing/extending-msm.md#creating-and-using-a-simple-liveactionfactory-class)

>[!NOTE]
>
>* MSM中的Blueprint [!DNL Sites] 在MSM中，稱為Live Copy來源 [!DNL Assets].
>* MSM不支援移除建立網站精靈中的章節步驟 [!DNL Assets].
>* MSM不支援在頁面屬性（觸控式UI）上設定MSM鎖， [!DNL Assets].


## 資產管理任務對Live Copy的影響 {#manage-assets}

即時副本和來源是可在一定程度上作為數位資產進行管理的資產或資料夾。 中的某些資產管理任務 [!DNL Experience Manager] 對即時副本有特定影響。

* 複製即時副本時，會建立具有與第一個即時副本相同來源的即時副本資產。
* 當您移動源或其即時副本時，將保留即時關係。
* 編輯動作無法用於即時副本資產。 如果即時副本的來源本身為即時副本，則編輯動作無法用於該副本。
* 簽出動作不適用於即時副本資產。
* 對於源資料夾，可使用建立審閱任務的選項。
* 在清單檢視和欄檢視中檢視資產清單時，即時副本資產或資料夾會對其顯示「即時副本」。 它可協助您輕鬆識別資料夾中的即時副本。

## 比較 [!DNL Assets] 和 [!DNL Sites] {#comparison}

在更多情況下， [!DNL Assets] 符合MSM for Sites功能的行為。 請注意的一些主要差異：

* MSM中的Blueprint [!DNL Sites] 在MSM中，稱為Live Copy來源 [!DNL Assets].
* 在Sites中，您可以比較Blueprint及其Live Copy，但無法在 [!DNL Assets] 來比較來源與其即時副本。
* 您無法在中編輯即時副本 [!DNL Assets].
* 網站通常有孩子，但 [!DNL Assets] 不要。 建立個別資產的即時副本時，不存在包含或排除子項的選項。
* MSM不支援移除建立網站精靈中的章節步驟 [!DNL Assets].
* MSM不支援在頁面屬性上設定MSM鎖（觸控式UI）, [!DNL Assets].
* 針對MSM [!DNL Assets]，僅使用 **[!UICONTROL 標準轉出設定]**. 其他轉出設定不適用於MSM [!DNL Assets].

## 最佳實務 {#best-practices}

MSM的一些最佳實務為：

* 開始實作前，先規劃資產和內容流的父子關係。

## MSM之限制及已知問題 [!DNL Assets] {#limitations}

以下為MSM於 [!DNL Assets].

* 使用案例不支援內容片段(CF)。 嘗試建立其Live Copy時，CF會照原樣複製，沒有任何關係。 複製的CF是及時的快照，在更新原始CF時不會更新。

* MSM無法搭配已啟用的中繼資料回寫運作。 回寫時，繼承會中斷。
