---
title: 管理影片資產
description: 在中上傳、預覽、注釋和發佈視訊資產 [!DNL Adobe Experience Manager].
contentOwner: AG
role: User
feature: Asset Management
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '5499'
ht-degree: 8%

---

# 管理影片資產 {#manage-video-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-video-assets.html?lang=en) |
| AEM 6.5 | 本文 |

視訊格式是組織數位資產的重要部分。 [!DNL Adobe Experience Manager] 提供成熟的產品和功能，可在影片資產建立後管理其整個生命週期。

了解如何在中管理和編輯視訊資產 [!DNL Adobe Experience Manager Assets]. 視頻編碼和轉碼，例如，FFmpeg轉碼，可以使用 [!DNL Dynamic Media] 整合。

## 上傳和預覽視訊資產 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 以副檔名MP4產生視訊資產的預覽。 如果資產的格式不是MP4，請安裝FFmpeg套件以產生預覽。 FFmpeg建立OGG和MP4類型的視頻轉譯。 您可以在 [!DNL Assets] 使用者介面。

1. 在數位資產資料夾或子資料夾中，導覽至您要新增數位資產的位置。
1. 若要上傳資產，請按一下 **[!UICONTROL 建立]** 從工具列中，然後選擇 **[!UICONTROL 檔案]**. 或者，在用戶介面上拖動檔案。 請參閱 [上傳資產](manage-assets.md#uploading-assets) 以取得詳細資訊。
1. 若要在「卡片」檢視中預覽影片，請按一下 **[!UICONTROL 播放]** ![播放選項](assets/do-not-localize/play.png) 選項。 您只能在卡片檢視中暫停或播放視訊。 此 [!UICONTROL 播放] 和 [!UICONTROL 暫停] 清單檢視中沒有選項可用。

1. 若要在資產詳細資訊頁面中預覽視訊，請按一下 **[!UICONTROL 編輯]** 在卡片上。 視訊會在瀏覽器的原生視訊播放器中播放。 您可以播放、暫停、控制音量，以及將視訊縮放至全螢幕。

   ![視訊播放控制項](assets/video-playback-controls.png)

## 上傳大於2 GB資產的設定 {#configuration-to-upload-assets-that-are-larger-than-gb}

依預設， [!DNL Assets] 由於檔案大小限制，不允許上傳超過2 GB的任何資產。 不過，您可以前往「 」CRXDE Lite並在「 」下建立節點，以覆寫此限制 `/apps` 目錄。 節點必須具有相同的節點名稱、目錄結構和順序的可比節點屬性。

除 [!DNL Assets] 設定時，請變更下列設定以上傳大型資產：

* 增加代號過期時間。 請參閱 [!UICONTROL AdobeGranite CSRF Servlet] 在Web主控台中() `https://[aem_server]:[port]/system/console/configMgr`. 如需詳細資訊，請參閱 [CSRF保護](/help/sites-developing/csrf-protection.md).
* 增加 `receiveTimeout` 在Dispatcher設定中。 如需詳細資訊，請參閱 [Experience ManagerDispatcher設定](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>此 [!DNL Experience Manager] 傳統用戶介面沒有2-GB檔案大小限制。 此外，大型視訊的端對端工作流程也未完全支援。

要配置更高的檔案大小限制，請在 `/apps` 目錄。

1. 在 [!DNL Experience Manager]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 在CRXDE Lite中，導覽至 `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. 要查看目錄窗口，請按一下 `>>`.
1. 在工具列中，按一下 **[!UICONTROL 覆蓋節點]**. 或者，從上 **[!UICONTROL 下文選單選取]** 「覆蓋節點」。
1. 在 **[!UICONTROL 覆蓋節點]** 對話框，按一下 **[!UICONTROL 確定]**.

   ![覆蓋節點](assets/overlay-node-path.png)

1. 重新整理瀏覽器。 覆蓋節點 `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` 中所有規則的URL。
1. 在 **[!UICONTROL 屬性]** 頁簽，以位元組為單位輸入適當值，以將大小限制增加到所需大小。 例如，若要將大小限制增加為30 GB，請輸入 `32212254720` 值。

1. 在工具列中，按一下 **[!UICONTROL 全部儲存]**.
1. 在 [!DNL Experience Manager]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web主控台]**.
1. 在 [!DNL Adobe Experience Manager] [!UICONTROL Web主控台套件組合] 頁，在表的「名稱」列下，查找並按一下 **[!UICONTROL AdobeGranite工作流程外部流程作業處理常式]**.
1. 在 [!UICONTROL AdobeGranite工作流程外部流程作業處理常式] 頁面，將秒數設定為 **[!UICONTROL 預設逾時]** 和 **[!UICONTROL 逾時上限]** 欄位 `18000` （五小時）。 按一下「**[!UICONTROL 儲存]**」。
1. 在 [!DNL Experience Manager]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 在「工作流模型」頁上，選擇 **[!UICONTROL Dynamic Media編碼視訊]**，然後按一下 **[!UICONTROL 編輯]**.
1. 在工作流程頁面上，連按兩下 **[!UICONTROL Dynamic Media視訊服務程式]** 元件。
1. 在「步 [!UICONTROL 驟屬性] 」對話框的「常用」頁籤下，展開「 **[!UICONTROL 高級設定」]******。
1. 在 **[!UICONTROL 逾時]** 欄位，指定 `18000`，然後按一下 **[!UICONTROL 確定]** 返回 **[!UICONTROL Dynamic Media編碼視訊]** 工作流程頁面。
1. 靠近頁面頂端，位於 [!UICONTROL Dynamic Media編碼視訊] 頁面標題，按一下 **[!UICONTROL 儲存]**.

## 發佈視訊資產 {#publish-video-assets}

發佈後，您可以將視訊資產以URL的形式包含在網頁中，或直接內嵌資產。 如需詳細資訊，請參閱 [發佈Dynamic Media資產](/help/assets/publishing-dynamicmedia-assets.md).

## 將影片發佈至YouTube {#publishing-videos-to-youtube}

您可以直接將內部部署的Experience Manager影片資產發佈至您先前建立的YouTube管道。

若要將影片資產發佈至YouTube，請使用標籤設定Experience Manager Assets。 將這些標籤與YouTube管道建立關聯。 如果影片資產的標籤符合YouTube頻道的標籤，則影片會發佈至YouTube。 只要使用相關標籤，發佈至YouTube就會與一般發佈視訊一起發生。

YouTube會自行編碼。 因此，上傳至Experience Manager的原始視訊檔案會發佈至YouTube，而非Dynamic Media編碼已建立的任何視訊轉譯。 雖然使用Dynamic Media處理視訊並非必要動作，但是當播放需要檢視器預設集時，應確實如此。

略過視訊處理設定檔並直接發佈至YouTube時，這只是表示您Experience Manager資產中的視訊資產沒有取得可檢視的縮圖。 也意味著如果你 `dynamicmedia` 或 `dynamicmedia_scene7` 執行模式時，未編碼的視訊無法用於任何Dynamic Media資產類型。

將視訊資產發佈至YouTube伺服器時，必須完成下列工作，以確保透過YouTube進行安全的伺服器對伺服器驗證：

1. [配置Google Cloud設定](#configuring-google-cloud-settings)
1. [建立YouTube管道](#creating-a-youtube-channel)
1. [新增發佈標籤](#adding-tags-for-publishing)
1. [啟用YouTube Publish復寫代理](#enabling-the-youtube-publish-replication-agent)
1. [在Experience Manager中設定YouTube](#setting-up-youtube-in-aem)
1. [（選用）自動設定您所上傳影片的預設YouTube屬性](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [將影片發佈至您的YouTube頻道](#publishing-videos-to-your-youtube-channel)
1. [（選用）驗證已發佈的YouTube影片](/help/assets/video.md#optional-verifying-the-published-video-on-youtube)
1. [將YouTube URL連結至您的Web應用程式](#linking-youtube-urls-to-your-web-application)

您也可以 [取消發佈影片以將其從YouTube中移除](#unpublishing-videos-to-remove-them-from-youtube).

### 配置Google Cloud設定 {#configuring-google-cloud-settings}

若要發佈至YouTube，您需要Google帳戶。 如果你有Gmail賬戶，那麼你已經有了Google賬戶；如果您沒有Google帳戶，便可輕鬆建立帳戶。 您需要帳戶，因為您需要憑證才能將影片資產發佈至YouTube。 如果已建立帳戶，請跳過此任務並直接繼續 [建立YouTube管道](#creating-a-youtube-channel).

與Google Cloud搭配使用的帳戶和用於YouTube的Google帳戶不必相同。

Google會定期變更其使用者介面。 因此，將影片發佈至YouTube的步驟可能與下文所述的略有不同。 當您嘗試檢查視訊是否已上傳至YouTube時，也會套用此警告。

>[!NOTE]
>
>在編寫本文時，以下步驟是正確的。 不過，Google會不經通知便定期更新其網站。 因此，這些步驟可能會稍有不同。

若要配置Google Cloud設定：

1. 建立Google帳戶。
   [https://accounts.google.com/SignUp?service=mail](https://accounts.google.com/SignUp?service=mail)

   如果您已有Google帳戶，請跳至下一個步驟。

1. 前往 [https://cloud.google.com/](https://cloud.google.com/).
1. 在Google cloud頁面的右上角，按一下「主控台」 ****。

   如有必要， **[!UICONTROL 登入]** 使用您的Google帳戶憑證來檢視 **[!UICONTROL 主控台]** 選項。

1. 在控制面板頁面上，位於 **[!UICONTROL Google Cloud Platform]**，按一下「專案」下拉式清單以開啟「選取專案」對話方塊。
1. 在「選取專案」對話方塊中，點選 **[!UICONTROL 新增專案]**.

   ![6_5_googleaccount-newproject](assets/6_5_googleaccount-newproject.png)

1. 在「新建項目」對話框的「項目名稱」欄位中，鍵入新項目的名稱。

   您的專案ID以您的專案名稱為基礎。 因此，請謹慎選擇專案名稱；建立後無法變更。 此外，您之後在Experience Manager中設定YouTube時，必須再次輸入相同的專案ID;考慮寫下來。

1. 按一下&#x200B;**[!UICONTROL 建立]**。

1. 執行下列任一操作：

   * 在專案的控制面板上，在「快速入門」卡片中，點選 **[!UICONTROL 探索並啟用API]**.
   * 在專案的控制面板中，在API卡片中，點選 **[!UICONTROL 前往API概述]**.

   ![6_5_googleaccount-apis-enable2](assets/6_5_googleaccount-apis-enable2.png)

1. 在「API與服務」頁面頂端附近，點選 **[!UICONTROL 啟用API與服務]**.
1. 在「API程式庫」頁面的左側，位於 **[!UICONTROL 類別]**，點選 **[!UICONTROL YouTube]**. 在頁面的右側，點選 **[!UICONTROL YouTube資料API]**.
1. 在YouTube Data API v3頁面上，點選 **[!UICONTROL 啟用]**.

   ![6_5_googleaccount-apis-enable3](assets/6_5_googleaccount-apis-enable3.png)

1. 若要使用API，您需要憑證。 如有必要，請按一下 **[!UICONTROL 建立憑證]**.

   ![6_5_googleaccount-api-createcredentials](assets/6_5_googleaccount-apis-createcredentials.png)

1. 在 **[!UICONTROL 將憑證新增至專案]** 頁面，步驟1，執行下列動作：

   * 從 **[!UICONTROL 您使用哪個API?]** 下拉清單，選擇 **[!UICONTROL YouTube資料API v3]**.

   * 從 **[!UICONTROL 您從何處呼叫API?]** 下拉清單，選擇 **[!UICONTROL Web伺服器（例如node.js、Tomcat）]**

   * 從 **[!UICONTROL 您正在存取哪些資料？]** 下拉式清單，點選 **[!UICONTROL 使用者資料]**.

   ![6_5_googleaccount-api-createcredentials2](assets/6_5_googleaccount-apis-createcredentials2.png)

1. 點選 **[!UICONTROL 我需要什麼認證？]**
1. 在「 **[!UICONTROL 新增認證至您的專案]** 」頁面的「建立OAuth 2.0用戶端ID **** 」標題下，視需要在「名稱」欄位中輸入唯一名稱。或者，您可以使用Google指定的預設名稱。
1. 在 **[!UICONTROL 授權的JavaScript原始項]** 標題，在文字欄位中輸入下列路徑，在路徑中取代您自己的網域和連接埠號，然後按 **[!UICONTROL 輸入]** 要向清單添加路徑：

   `https://<servername.domain>:<port_number>`

   例如 `https://1a2b3c.mycompany.com:4321`

   **附註**:上述路徑範例僅供示範之用。

   ![6_5_googleaccount-api-createcredentials-oauth](assets/6_5_googleaccount-apis-createcredentials-oauth.png)

1. 在 **[!UICONTROL 授權的重定向URI]** 標題，在文字欄位中輸入下列路徑，在路徑中取代您自己的網域和連接埠號，然後按 **[!UICONTROL 輸入]** 要向清單添加路徑：

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   例如 `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   **附註**:上述路徑範例僅供示範之用。

1. 按一下 **[!UICONTROL 建立OAuth用戶端ID]**.
1. 在「 **[!UICONTROL 新增認證至您的專案]****** 」頁面的「設定OAuth 2.0同意書」畫面標題下方，選取您目前使用的Gmail電子郵件地址。

   ![6_5_googleaccount-api-createcredentials-accensscreen](assets/6_5_googleaccount-apis-createcredentials-consentscreen.png)

1. 在 **[!UICONTROL 向使用者顯示的產品名稱]** 標題，在文字欄位中，輸入您要在同意畫面上顯示的內容。

   Experience Manager管理員向YouTube驗證時，會顯示同意畫面；Experience Manager聯繫YouTube以獲取權限。

1. 按一下&#x200B;**[!UICONTROL 「繼續」]**。
1. 在「新增認證至您的專案」頁面的「下載認證」標題下，點選「 **[!UICONTROL 下載]** 」 **[!UICONTROL 步驟4]**。

   ![6_5_googleaccount-api-createcredentials-downloadcredentials](assets/6_5_googleaccount-apis-createcredentials-downloadcredentials.png)

1. 儲存 `client_id.json` 檔案。

   稍後在Adobe Experience Manager中設定YouTube時，您需要此已下載的json檔案。

1. 按一下 **[!UICONTROL 完成]**.

   登出您的Google帳戶。 現在建立YouTube管道。

### 建立YouTube管道 {#creating-a-youtube-channel}

若要將影片發佈至YouTube，您必須擁有一或多個管道。 如果您已建立YouTube管道，則可略過此工作，然後前往 [新增發佈標籤](/help/assets/video.md#adding-tags-for-publishing).

>[!WARNING]
>
>請確定您已在YouTube中設定一或多個管道 *befor* 您可在「YouTube設定」下方新增管道(請參閱 [在Experience Manager中設定YouTube](#setting-up-youtube-in-aem) )。 如果您未設定一或多個管道，系統不會警告您不存在管道。 不過，新增頻道時仍會發生Google驗證，但無法選擇要傳送視訊的頻道。

**若要建立YouTube管道：**

1. 前往 [https://www.youtube.com](https://www.youtube.com/) 並使用您的Google帳戶憑證登入。
1. 在YouTube頁面的右上角，按一下您的個人資料圖片（也可以在實色圓圈內顯示為字母），然後按一下 **[!UICONTROL YouTube設定]** （圓齒輪圖示）。
1. 在「概述」頁面的「其他功能」標題下，按一下 **[!UICONTROL 查看我的所有管道或建立管道]**.
1. 在「管道」頁面上，按一下 **[!UICONTROL 建立新管道]**.
1. 在「品牌帳戶」頁面的「品牌帳戶名稱」欄位中，輸入商業名稱或您選擇要發佈影片資產的任何其他管道名稱，然後按一下 **[!UICONTROL 建立]**.

   請記住您在這裡輸入的名稱，因為當您在Experience Manager中設定YouTube時，必須再次輸入它。

1. （選用）如有必要，請新增更多管道。

   現在新增要發佈的標籤。

### 新增發佈標籤 {#adding-tags-for-publishing}

若要發佈至YouTube的影片，Experience Manager會將標籤關聯至一或多個YouTube頻道。 若要新增發佈標籤，請參閱 [管理標籤](/help/sites-administering/tags.md).

或者，如果您想在Experience Manager中使用預設標籤，則可以跳過此任務並轉到 [啟用YouTube Publish復寫代理](#enabling-the-youtube-publish-replication-agent).

### 啟用YouTube Publish復寫代理 {#enabling-the-youtube-publish-replication-agent}

啟用YouTube Publish復寫代理後，如果您想要測試與Google雲端帳戶的連線，請點選 **[!UICONTROL 測試連線]**. 瀏覽器索引標籤會顯示連線結果。 如果您已新增YouTube管道，這些管道的清單會顯示為測試的一部分。

1. 在Experience Manager的左上角，按一下Experience Manager標誌，然後在左側邊欄中，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]** > **[!UICONTROL 作者代理]**.
1. 在作者代理頁面上，按一下 **[!UICONTROL YouTube Publish]**.
1. 在工具列的「設定」右側，按一下 **[!UICONTROL 編輯]**.
1. 選取 **[!UICONTROL 已啟用]** 核取方塊，以便開啟復寫代理。
1. 按一下&#x200B;**[!UICONTROL 「確定」]**。

   現在在Experience Manager中設定YouTube。

### 在Experience Manager中設定YouTube {#setting-up-youtube-in-aem}

從Experience Manager6.4開始，引入新的觸控使用者介面方法，以在Experience Manager中設定YouTube發佈。 根據您使用的Experience Manager安裝例項，執行下列其中一項操作：

* 若要在6.4之前的Experience Manager中設定YouTube，請參閱 [在6.4之前的Experience Manager中設定YouTube](/help/assets/video.md#setting-up-youtube-in-aem-before).
* 若要在Experience Manager6.4或更新版本中設定YouTube，請參閱 [在Experience Manager6.4和更新版本中設定YouTube](#setting-up-youtube-in-aem-and-later).

#### 在Experience Manager6.4和更新版本中設定YouTube {#setting-up-youtube-in-aem-and-later}

1. 請務必以管理員身分登入您的Dynamic Media例項。
1. 在左上角，點選Experience Manager標誌，然後在左側導軌中，點選 **[!UICONTROL 工具]**（錘子表徵圖）> **[!UICONTROL Cloud Services]** > **[!UICONTROL YouTube發佈設定]**.
1. 點選 **[!UICONTROL 全球]** （請勿選取）。

1. 在全域頁面的右上角附近，點選 **[!UICONTROL 建立]**.
1. 在「建立YouTube設定」頁面的「Google cloud 平台設定」下方的「應用程式名稱」欄位 **[!UICONTROL 中]** ，輸入Google專案ID。

   您先前初次設定Google Cloud設定時，已指定專案ID。
保留建立YouTube設定頁面開啟；一會兒，你就會回到這裡。

   ![6_5_youtubepublish-createyoutubeconfiguration](assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. 使用純文字編輯器，開啟您先前在工作中下載並儲存的JSON檔案 [配置Google Cloud設定](/help/assets/video.md#configuring-google-cloud-settings).
1. 選取並複製整個JSON文字。
1. 返回YouTube帳戶設定對話方塊。在「 **[!UICONTROL JSON設定」欄位中]** ，貼上JSON文字。
1. 在頁面的右上角附近，點選 **[!UICONTROL 儲存]**.

   現在在Experience Manager中設定YouTube頻道。

1. 點選 **[!UICONTROL 新增管道]**.
1. 在「管道名稱」欄位中，輸入您在任務中建立的管道名稱 **[!UICONTROL 新增一或多個管道至YouTube]** 更早。

   您可以視需要選擇新增說明。

1. 點選 **[!UICONTROL 新增]**.
1. YouTube/Google驗證隨即顯示。 如果您尚未登入Google雲端帳戶，請略過此步驟。

   * 輸入與上述Google專案ID和JSON文字相關聯的Google使用者名稱和密碼。
   * 視您的帳戶有多少管道而定，您會看到兩個或多個項目。 選取管道。 不要選擇電子郵件地址；它不是渠道。
   * 在下一頁，點選 **[!UICONTROL 接受]** 允許存取此通道。

1. 點選 **[!UICONTROL 允許]**.

   現在設定發佈的標籤。

1. **[!UICONTROL 設定發佈的標籤]**  — 在「Cloud Services> YouTube」頁面上，點選鉛筆圖示以編輯您要使用的標籤清單。
1. 點選下拉式清單圖示（倒轉插入號），以便以Experience Manager顯示可用標籤清單。
1. 點選一或多個標籤，以便新增標籤。

   若要刪除已新增的標籤，請選取標籤，然後點選 **[!UICONTROL X]**.

1. 添加完所需標籤後，點選 **[!UICONTROL 儲存]**.

   現在您可將影片發佈至YouTube頻道。

#### 在6.4之前的Experience Manager中設定YouTube {#setting-up-youtube-in-aem-before}

1. 請務必以管理員身分登入您的Dynamic Media例項。

1. 在左上角，點選Experience Manager標誌，然後在左側導軌中，點選 **[!UICONTROL 工具]** （錘子表徵圖）> **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 在「協力廠商服務」標題下，在YouTube下方，點選 **[!UICONTROL 立即配置]**.
1. 在「建立配置」對話框中，在相應欄位中輸入標題（必填）和名稱（選填）。
1. 點選 **[!UICONTROL 建立]**.
1. 在「YouTube帳戶設定」對話方塊的「應用程式名 **[!UICONTROL 稱」欄位中]** ，輸入Google專案ID。

   您最初指定專案ID時 [配置的Google Cloud設定](/help/assets/video.md#configuring-google-cloud-settings) 更早。
讓「YouTube帳戶設定」對話方塊保持開啟；你馬上就會回來。

1. 使用純文字編輯器，開啟先前在設定Google雲端設定工作中下載並儲存的JSON檔案。
1. 選取並複製整個JSON文字。
1. 返回YouTube帳戶設定對話方塊。在「 **[!UICONTROL JSON設定」欄位中]** ，貼上JSON文字。
1. 點選 **[!UICONTROL 確定]**.

   現在在Experience Manager中設定YouTube頻道。

1. 在「可用頻道」 **[!UICONTROL 的右側]**，點 **選+**  (加號圖示)。
1. 在「YouTube頻道設定」對話方塊的「標題」欄位中，輸入您在「先前新增一或多個頻道至YouTube」工作中建立的頻道名稱 **** 。

   您可以視需要選擇新增說明。

1. 點選 **[!UICONTROL 確定]**.
1. YouTube/Google驗證隨即顯示。 如果您尚未登入Google雲端帳戶，請略過此步驟。

   * 輸入與上述Google專案ID和JSON文字相關聯的Google使用者名稱和密碼。
   * 視您的帳戶有多少管道而定，您會看到兩個或多個項目。 選取管道。 不要選擇電子郵件地址；它不是渠道。
   * 在下一頁，點選 **[!UICONTROL 接受]** 允許存取此通道。

1. 點選 **[!UICONTROL 允許]**.

   現在設定發佈的標籤。

1. **[!UICONTROL 設定發佈的標籤]**  — 在「Cloud Services> YouTube」頁面上，點選鉛筆圖示以編輯您要使用的標籤清單。
1. 點選下拉式清單圖示（倒轉插入號），以便以Experience Manager顯示可用標籤清單。
1. 點選一或多個標籤，以便新增標籤。

   若要刪除已新增的標籤，請選取標籤，然後點選 **X**.

1. 添加完所需標籤後，點選 **[!UICONTROL 確定]**.

   現在您可將影片發佈至YouTube頻道。

### （選用）自動設定您所上傳影片的預設YouTube屬性 {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

您可以在Experience Manager中建立中繼資料處理設定檔，選擇在上傳影片時自動設定YouTube屬性。

若要建立中繼資料處理設定檔，您必須先從「欄位標籤 **[!UICONTROL 」、「對應至屬性]********** 」和「選擇」欄位複製值，這些全都可在視訊的中繼資料結構中找到。接著，您可以新增這些值，以建立YouTube視訊中繼資料處理設定檔。

若要自動設定已上傳影片的預設YouTube屬性：

1. 在左上角，點選Experience Manager標誌，然後在左側導軌中，按一下 **[!UICONTROL 工具]** （錘子表徵圖）> **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料結構]**.
1. 按一下 **[!UICONTROL 預設]**. （請勿在「預設」左側的選取方塊中新增核取記號。）
1. 在 **[!UICONTROL 預設]** 頁面，核取左側的方塊 **[!UICONTROL 影片]**，然後點選 **[!UICONTROL 編輯]**.
1. 在「中繼資料結構編輯器」頁面上，點選 **[!UICONTROL 進階]** 標籤。
1. 在「YouTube發佈」標題下，按一下「 **[!UICONTROL YouTube類別」]**。
1. 在頁面的右側，在 **[!UICONTROL 設定]** 頁簽，執行下列操作：

   * 在 **[!UICONTROL 對應至屬性]** 文字欄位，選取並複製值。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 將文字編輯器保持開啟。

   * 在 **[!UICONTROL 選擇]**，選擇並複製您要使用的預設值（如「人物與部落格」或「科學與技術」）。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 將文字編輯器保持開啟。

1. 在「 YouTube Publishing 」標題下，點選 **[!UICONTROL YouTube隱私]**.
1. 在頁面的右側，在 **[!UICONTROL 設定]** 頁簽，執行下列操作：

   * 在 **[!UICONTROL 對應至屬性]** 文字欄位，選取並複製值。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 將文字編輯器保持開啟。

   * 在 **[!UICONTROL 選擇]**，請選取並複製您要使用的預設值。 請注意，「選擇」會分組為兩組。 配對中的底部欄位是您要複製的預設值，例如公用、未列出或私用。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 將文字編輯器保持開啟。

1. 在「中繼資料結構編輯器」頁面的右上角附近，按一下 **[!UICONTROL 取消]**.
1. 在Experience Manager的左上角，點選Experience Manager標誌，然後在左側導軌中，按一下 **[!UICONTROL 工具]** （錘子表徵圖）> **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料設定檔]**.

1. 在「中繼資料描述檔」頁面的右上角附近，按一下 **[!UICONTROL 建立]**.
1. 在「新增中繼資料描述檔」對話方塊的「描述檔標題 **[!UICONTROL 」文字欄位中，輸入名稱，]** 然後按一下「 `YouTube Video` 建立 ****」。
1. 在「中繼資料描述檔編輯器」頁面上，按一下 **[!UICONTROL 進階]** 標籤。
1. 執行下列動作，將複製的YouTube Publishing值新增至設定檔：

   * 在頁面右側，按一下 **[!UICONTROL 建置表單]** 標籤。
   * （可選）拖曳標示為 **[!UICONTROL 節標題]** 左邊，放在表單區域。
   * （選用）按一下 **[!UICONTROL 欄位標籤]** 來選取元件。
   * （可選）在頁面右側的「設定」標籤下方的「欄位標籤」文字欄位中，輸入 `YouTube Publishing`.
   * 按一下 **[!UICONTROL 建置表單]** 標籤，然後拖曳標示為的元件 **[!UICONTROL 多值文字]** 把它放下 **[!UICONTROL YouTube發佈]** 標題。

   * 按一下 **[!UICONTROL 欄位標籤]** 以便選取元件。
   * 在頁面右側的「設定」標籤下方，將您先前複製的YouTube發佈值（欄位標籤值和對應至屬性值）貼入表單上各自的欄位。 將選擇值貼入預設值欄位。

1. 執行下列動作，將複製的YouTube隱私權值新增至設定檔：

   * 在頁面右側，按一下 **[!UICONTROL 建置表單]** 標籤。
   * （可選）拖曳標示為 **[!UICONTROL 節標題]** 左邊，放在表單區域。
   * （選用）按一下 **[!UICONTROL 欄位標籤]** 來選取元件。
   * （可選）在頁面右側的「設定」標籤下方的「欄位標籤」文字欄位中，輸入 `YouTube Privacy`.
   * 按一下 **[!UICONTROL 建置表單]** 標籤，然後拖曳標示為的元件 **[!UICONTROL 多值文字]** 把它放下 **[!UICONTROL YouTube隱私]** 標題。

   * 按一下 **[!UICONTROL 欄位標籤]** 以便選取元件。
   * 在頁面右側的「設定」標籤下方，將您先前複製的YouTube發佈值（欄位標籤值和對應至屬性值）貼入表單上各自的欄位。 將選擇值貼入預設值欄位。

1. 在頁面的右上角附近，按一下「儲 **[!UICONTROL 存」]**。
1. 將YouTube發佈中繼資料設定檔套用至您要上傳影片的資料夾。 您必須同時設定「中繼資料描述檔」和「視訊描述檔」。

   請參 [閱中繼資料](/help/assets/metadata-config.md#metadata-profiles)[描述檔和視訊描述檔](/help/assets/video-profiles.md)。

### 將影片發佈至您的YouTube頻道 {#publishing-videos-to-your-youtube-channel}

現在，您將先前新增的標籤與視訊資產建立關聯。 此程式可讓Experience Manager知道要發佈至您的YouTube管道的資產。

>[!NOTE]
>
>在Dynamic Media - Scene7模式中執行時，立即發佈不會自動發佈至YouTube。 設定Dynamic Media - Scene7模式時，有兩個發佈選項可供選擇： **[!UICONTROL 立即]** 或 **[!UICONTROL 啟動時]**.
>
>**[!UICONTROL 立即發佈]** 表示上傳的資產（與IPS同步後）會自動發佈至傳送系統。 雖然Dynamic Media的情況確實如此，但YouTube的情況並非如此。 若要發佈至YouTube，您必須透過「Experience Manager作者」發佈。

>[!NOTE]
>
>若要從YouTube發佈內容，Experience Manager會使用 **[!UICONTROL 發佈至YouTube]** 工作流程，可讓您監控進度並檢視任何失敗資訊。
>
>請參閱 [監視視訊編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress).
>
>如需更詳細的進度資訊，您可以在復寫下監控YouTube記錄檔。 但請注意，此類監控需要管理員存取權。

**若要將影片發佈至您的YouTube頻道：**

1. 在Experience Manager中，導覽至您要發佈至YouTube管道的視訊資產。
1. 選取視訊資產（最適化視訊集）。
1. 在工具列上，按一下 **[!UICONTROL 屬性]**.
1. 在「基本」標籤的「中繼資料」標題下，按一下 **[!UICONTROL 開啟選取對話方塊]** ，在「標籤」欄位的右側。
1. 在「選取標籤」頁面上，導覽至您要使用的標籤，然後選取一或多個標籤。

   請記住，標籤必須與YouTube管道相關聯。

1. 在頁面的右上角，按一下 **[!UICONTROL 選擇]**.
1. 在影片屬性頁面的右上角，按一下 **[!UICONTROL 儲存並關閉]**.
1. 在工具列上，按一下 **[!UICONTROL 快速發佈]**.

   另請參閱 [搭配使用發佈管理Experience Manager Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html).

   您可以選擇驗證您的YouTube頻道上已發佈的視訊。

### （選用）驗證已發佈的YouTube影片 {#optional-verifying-the-published-video-on-youtube}

您可以選擇監控YouTube發佈（或取消發佈）的進度。

請參閱 [監視視訊編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress).

發佈時間可能會因許多因素而大不相同，這些因素包括主要來源視訊的格式、檔案大小和上傳流量。 發佈程式可能需要幾分鐘到數小時的時間。 另外，更高解析度的格式的呈現速度要慢得多。 例如，720p和1080p的顯示時間比480p要長。

八小時後，如果您仍看到狀態訊息，指出 **[!UICONTROL 已上載（正在處理，請稍候）]**，請嘗試從Adobe的網站移除視訊，然後再次上傳。

### 將YouTube URL連結至您的Web應用程式 {#linking-youtube-urls-to-your-web-application}

您可以取得YouTube URL字串，此字串在您發佈影片後由Dynamic Media產生。 複製YouTube URL時，剪貼簿會隨即顯示，因此您可以視需要將其貼至網站或應用程式中的頁面。

>[!NOTE]
>
>在您將視訊資產發佈至YouTube之前，無法複製YouTube URL。

**若要將YouTube URL連結至您的Web應用程式：**

1. 導覽至 *YouTube已發佈* 您要複製其URL的視訊資產，然後選取它。

   請記住，YouTube URL僅可複製 *after* 你先 *已發佈* 視訊資產傳送至YouTube。

1. 在工具列上，按一下 **[!UICONTROL 屬性]**.
1. 按一下 **[!UICONTROL 進階]** 標籤。
1. 在「YouTube發佈」標題下的「YouTube URL List」（ URL清單）中，選取URL文字，並將其複製至網頁瀏覽器，以預覽資產或新增至您的網頁內容頁面。

### 取消發佈影片，以便從YouTube中移除影片 {#unpublishing-videos-to-remove-them-from-youtube}

在Experience Manager中取消發佈視訊資產時，視訊會從YouTube移除。

>[!CAUTION]
>
>如果您直接從YouTube中移除影片，Experience Manager不會察覺，且會繼續以視訊仍發佈至YouTube的方式運作。 一律透過Experience Manager從YouTube取消發佈視訊資產。

>[!NOTE]
>
>若要從YouTube移除內容，Experience Manager會使用 **[!UICONTROL 從YouTube取消發佈]** 工作流程，可讓您監控進度並檢視任何失敗資訊。
>
>請參閱 [監視視訊編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress).

**若要取消發佈影片以從YouTube中移除影片：**

1. 導覽至您要從YouTube管道取消發佈的視訊資產。
1. 在資產選取模式中，選取一或多個已發佈的視訊資產。
1. 在工具列上，按一下 **[!UICONTROL 管理出版物]**. 點選三個點的圖示(...) 在工具列上 **[!UICONTROL 管理出版物]** 開啟。
1. 在管理出版物頁面上，點選 **[!UICONTROL 取消發佈]**.
1. 在頁面的右上角，點選 **[!UICONTROL 下一個]**.
1. 在頁面的右上角，點選 **[!UICONTROL 取消發佈]**.

## 監視視訊編碼和YouTube發佈進度 {#monitoring-video-encoding-and-youtube-publishing-progress}

將新視訊上傳至已套用視訊編碼的資料夾，或將視訊發佈至YouTube時，可以監控視訊編碼/Youtube發佈的進展情形。 實際YouTube發佈進度僅透過記錄檔提供。 但是，其失敗或成功會以下列程式中說明的其他方式列出。 此外，當YouTube發佈工作流程或視訊編碼完成或中斷時，您會收到電子郵件通知。

### 監視進度 {#monitoring-progress}

1. 在資產資料夾中檢視視訊編碼進度：

   * 在卡片檢視中，視訊編碼進度會依百分比顯示在資產上。 如果發生錯誤，此資訊也會顯示在資產上。

   ![chlimage_1-429](assets/chlimage_1-429.png)

   * 在清單檢視中，視訊編碼進度會顯示在 **[!UICONTROL 處理狀態]** 欄。 如果出現錯誤，則該欄會顯示此訊息。

   ![chlimage_1-430](assets/chlimage_1-430.png)

   預設不會顯示此欄。若要啟用欄，請從檢視下拉 **[!UICONTROL 式選單中選取「檢視設定]** 」，然後新增「處理狀態」欄，然後點選或按一下「更新」 ********。

   ![chlimage_1-431](assets/chlimage_1-431.png)

1. 在資產詳細資訊中檢視進度。 當您點選或按一下資產時，請開啟下拉式選單並選取 **[!UICONTROL 時間表]**. 若要將其縮小至編碼或YouTube發佈等工作流程活動，請選取 **[!UICONTROL 工作流程]**.

   ![chlimage_1-432](assets/chlimage_1-432.png)

   時間軸中會顯示任何工作流程資訊（例如編碼）。 針對YouTube發佈，工作流程時間軸也包含YouTube管道和YouTube影片URL的名稱。 此外，發佈完成後，您會在工作流程時間軸中看到任何失敗通知。

   >[!NOTE]
   >
   >由於上有多個工作流程設定，最終記錄失敗/錯誤訊息可能需花很長時間 **[!UICONTROL 重試]**, **[!UICONTROL 重試延遲]**，和 **[!UICONTROL 逾時]** 從 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)，例如：
   >
   >    * Apache Sling作業佇列設定
   >    * AdobeGranite工作流程外部流程作業處理常式
   >    * Granite工作流程逾時佇列

   >
   >您可以調整 **[!UICONTROL 重試]**, **[!UICONTROL 重試延遲]**，和 **[!UICONTROL 逾時]** 屬性。

1. 如需進行中的工作流程，請參閱「工具 **[!UICONTROL >工作流程]** >例項」中的「工作流程例 **[!UICONTROL 項」]******。

   >[!NOTE]
   >
   >您需要管理權限才能存取 **[!UICONTROL 工具]** 功能表。

   ![chlimage_1-433](assets/chlimage_1-433.png)

   選取執行個體並點選 **[!UICONTROL 開啟歷史記錄]**.

   ![chlimage_1-434](assets/chlimage_1-434.png)

   從「工作流實例」區域，您還可以暫停、終止或更名工作流。 請參閱 [管理工作流程](/help/sites-administering/workflows-administering.md) 以取得更多資訊。

1. 有關失敗的作業，請參閱「工具」>「工作流 **[!UICONTROL 程」]** > 「失敗 **[!UICONTROL 」中的「工]** 作流失敗 ****」。「工作 **[!UICONTROL 流失敗]** 」(Workflow Failure)列出所有失敗的工作流活動。

   >[!NOTE]
   >
   >您需要管理權限才能存取 **[!UICONTROL 工具]** 功能表。

   ![chlimage_1-435](assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >由於上有多個工作流程設定，最終記錄錯誤訊息可能需要很長時間 **[!UICONTROL 重試]**, **[!UICONTROL 重試延遲]**，和 **[!UICONTROL 逾時]** 從 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)，例如：
   >
   >
   >
   >    * Apache Sling作業佇列設定
   >    * AdobeGranite工作流程外部流程作業處理常式
   >    * Granite工作流程逾時佇列

   >
   >
   >您可以調整 **[!UICONTROL 重試]**, **[!UICONTROL 重試延遲]**，和 **[!UICONTROL 逾時]** 屬性。

1. 如需完成的工作流程，請參閱「工具 **[!UICONTROL >工作流程]** >封存 **[!UICONTROL 」中的「工作流程封存]******」。「工作 **[!UICONTROL 流程存檔]** 」會列出所有已完成的工作流活動。

   >[!NOTE]
   >
   >您需要管理權限才能存取 **[!UICONTROL 工具]** 功能表。

   ![chlimage_1-436](assets/chlimage_1-436.png)

1. 您會收到有關中止或失敗工作流程作業的電子郵件通知。 管理員可設定這些電子郵件通知。 請參閱 [設定電子郵件通知](#configuring-e-mail-notifications).

#### 配置電子郵件通知 {#configuring-e-mail-notifications}

>[!NOTE]
>
>您需要管理權限才能存取 **[!UICONTROL 工具]** 功能表。

設定通知的方式取決於您要接收編碼作業或YouTube發佈作業的通知：

* 對於編碼作業，您可以訪問所有Experience Manager工作流電子郵件通知的配置頁： **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web主控台]** 通過搜索 **[!UICONTROL Day CQ工作流程電子郵件通知服務]**. 請參閱 [在Experience Manager中設定電子郵件通知](/help/sites-administering/notification.md). 您可以選取或清除 **[!UICONTROL 中止時通知]** 或 **[!UICONTROL 完成時通知]** 因此。

* 若為YouTube發佈工作，請執行下列動作：

1. 在Experience Manager中，點選 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 在「工作流模型」頁上，選擇 **[!UICONTROL 發佈至YouTube]**，然後點選 **[!UICONTROL 編輯]** 的上界。
1. 在「發佈至YouTube」工作流程頁面的右上角附近，點選 **[!UICONTROL 編輯]**.
1. 將滑鼠指標暫留在YouTube上傳元件上，然後點選一次以顯示內嵌工具列。

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. 在內嵌工具列上，點選「設定」圖示（扳手）。 按一下 **[!UICONTROL 引數]** 標籤。

   ![6_5_publishtoyoutubeworkflow-configuration圖示](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. 在YouTube上傳程式 — 步驟屬性對話方塊中，點選 **[!UICONTROL 引數]** 標籤。

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. 您可以選取或清除下列核取方塊：

   * 發佈開始
   * 發佈失敗
   * 發佈完成 — 包含通道和URL的資訊

   清除核取方塊表示您不會從YouTube發佈工作流程接收指定的電子郵件通知。

   >[!NOTE]
   >
   >這些電子郵件是YouTube專屬的，且是一般工作流程電子郵件通知的外掛程式。 因此，您可以收到兩組電子郵件通知 — 中提供的一般通知 **[!UICONTROL Day CQ工作流程電子郵件通知服務]** 和YouTube專用欄位（視您的組態設定而定）。

1. 完成後，在對話框的右上角附近，點選 **[!UICONTROL 完成]** 表徵圖（複選標籤）。
1. 在「發佈至YouTube」工作流程頁面，靠近右上角，點選 **[!UICONTROL 同步]**.

## 為視訊資產加上注釋 {#annotate-video-assets}

1. 從 [!DNL Assets] 主控台，選取 **[!UICONTROL 編輯]** 在「資產」卡片上，以顯示「資產詳細資訊」頁面。
1. 若要播放視訊，請按一下 **[!UICONTROL 預覽]**.
1. 若要為視訊加上注釋，請按一下 **[!UICONTROL 注釋]**. 在視訊中的特定時間（幀）添加註釋。 批注時，可以在畫布上繪製，並在繪圖中包括注釋。 注釋會自動儲存。 要退出注釋嚮導，請按一下 **[!UICONTROL 關閉]**.

   ![在視訊影格上繪製和加上註解](assets/annotate-video.png)

1. 尋找視訊中的特定點，在&#x200B;**「文字」**&#x200B;欄位中指定時間 (以秒為單位)，然後按一下&#x200B;**「跳至」**。例如，若要略過前 20 秒的視訊，請在文字欄位中輸入 20。

   ![尋找視訊中要略過的時間（以指定秒為準）](assets/seek-in-video.png)

1. 要在時間軸中查看它，請按一下注釋。 要從時間軸中刪除注釋，請按一下 **[!UICONTROL 刪除]**.

   ![在時間軸中查看注釋和詳細資訊](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [在Experience Manager Assets中管理數位資產](/help/assets/manage-assets.md)
>* [在Experience Manager Assets中管理集合](/help/assets/manage-collections.md)
>* [Dynamic Media影片檔案](/help/assets/video.md).

