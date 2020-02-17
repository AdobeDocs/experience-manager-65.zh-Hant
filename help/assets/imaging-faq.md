---
title: 智慧型影像處理
description: 智慧型影像處理運用每位使用者獨特的檢視特性，自動提供最適合其體驗的影像，進而提升效能和參與度。
uuid: c11e52ba-8d64-4dc5-b30a-fc10c2b704e5
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 智慧型影像 {#smart-imaging}

## 什麼是智慧影像？ {#what-is-smart-imaging}

智慧型影像處理運用每位使用者獨特的檢視特性，自動提供最適合其體驗的影像，進而提升效能和參與度。 智慧型影像功能可與您現有的影像預設集搭配使用，並在傳送時的最後一毫秒使用智慧功能，根據瀏覽器或網路連線速度進一步降低影像檔案大小。

智慧型影像處理可與同級最佳的優質CDN服務完全整合，進而大幅提升效能。 此服務在伺服器、網路和互連點之間找到最佳的Internet路由，該路由的延遲和／或資料包丟失率比Internet上的預設路由低。

## 智慧型影像的主要優點為何？ {#what-are-the-key-benefits-of-smart-imaging}

智慧型影像功能可根據使用者特性自動最佳化影像檔案大小，提供更佳的影像傳送效能。 由於影像是頁面載入時間的絕大部分，因此效能的提升會對商業KPI產生深遠影響，例如較高的轉換率、網站逗留時間、較低的網站反彈率等。 Adobe比較了不同檔案格式、瀏覽器和品質(QLT)設定的預設影像傳送效能與智慧型影像的效能。 整體而言，視您現有的影像預設集設定和特定使用者特性而定，效能可提升22-47%。

![image2017-11-14_133226](assets/image2017-11-14_133226.png)

## 智慧型影像處理是否有相關的授權成本？ {#are-there-any-licensing-costs-associated-with-smart-imaging}

否. 智慧型影像功能已隨附於您現有的Dynamic Media Classic(Scene7)或Dynamic Media授權中。 利用這項新功能不需要額外的成本。

## 智慧型影像處理如何運作？ {#how-does-smart-imaging-work}

當消費者第一次要求影像時，我們會檢查使用者的特性，並根據瀏覽器將影像轉換為適當的影像格式。 此外，我們同時建立所有格式轉換，然後在CDN中快取。 當不同瀏覽器的消費者隨後要求該影像時，會直接從CDN快取自動傳送適當的影像格式。 這些格式轉換是以無損的方式進行，不會降低視覺精確度。 智慧型影像功能可根據瀏覽器功能自動將影像轉換為不同格式，如下所示：

* 針對支援WebP格式（例如Chrome、Android和Opera）的瀏覽器，自動轉換為不失真的WebP。
* 針對支援JPEGXR格式（例如Internet Explorer 9+）的瀏覽器，自動轉換為無損JPEGXR。
* 針對支援JPEG2000格式（例如Safari）的瀏覽器，自動轉換為無損JPEG2000。
* 對於不支援這些格式的瀏覽器，會提供原本要求的影像格式。

## 支援哪些影像格式？ {#what-image-formats-are-supported}

智慧型影像支援下列影像格式：

* RGB JPEG
* RGB PNG
* RGB TIFF
* CMYK JPEG
* CMYK TIFF

## 智慧型影像處理如何與我們現有已使用的影像預設集搭配運作？ {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

智慧型影像功能可與您現有的影像預設集搭配使用，並可觀察您的所有影像設定，例如大小、品質、銳利化等等。 更改的是映像格式，或者，在網路連接速度較慢的情況下，更改質量設定。 對於格式轉換，我們會依照您的影像預設集設定所定義，維持完整的視覺完整性，但檔案大小會較小。

例如，假設影像預設集的定義為JPEG格式，大小為500x500、quality=85，而遮色片不銳利=0.1,1,5。 當我們偵測到使用者在Chrome瀏覽器上時，影像會轉換為不失真的WebP格式，大小為500x500、品質=85，遮色片=0.1,1,5。

## 我是否必須變更任何URL、影像預設集，或在我的網站上部署任何新程式碼，才能進行智慧型影像處理？ {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

否. 智慧型影像功能可與您現有的影像URL和影像預設集完美搭配運作。 此外，智慧型影像功能不需要您在網站上新增任何程式碼來偵測不同的使用者特性（瀏覽器、頻寬、裝置等）。 所有這些都由Adobe自動處理。

唯一需要的變更是更新 **[!UICONTROL 存留時間]** (TTL)設定。 此設定會定義CDN快取資產的時間長度。 為了最大化智慧型影像的效能提升，Adobe建議將TTL設為24小時或更長。 要更改此設定，請：

* 如果您使用Dynamic Media Classic，請點選「設定>應 **[!UICONTROL 用程式設定>發佈設定>影像伺服器」]**。 將「預 **[!UICONTROL 設用戶端快取時間」設為]** 24或更長的「即時」值。

* 如果您使用動態媒體，請依照指示 [設定動態媒體影像設定](config-dynamic.md)**[!UICONTROL Expiration]** （過期）值為24小時或更長。

>[!NOTE]
>
>如果設定TTL &lt;= 1小時，則智慧映像無法工作。

## 智慧型影像處理是否可與HTTPS搭配運作？ HTTP/2如何？ {#does-smart-imaging-working-with-https-how-about-http}

智慧型影像可處理透過HTTP或HTTPS傳送的影像。 此外，它也可透過HTTP/2運作。

## 我是否符合使用智慧型影像的資格？ {#am-i-eligible-to-use-smart-imaging}

若要使用智慧型影像，您公司的AEM帳戶上的Dynamic Media Classic或Dynamic Media必須符合下列需求：

* 使用Adobe搭售的CDN（內容放送網路）做為您授權的一部分。
* 使用專用網域(即 `images.company.com` 或 `mycompany.scene7.com`)，而非一般網域(即、 `s7d1.scene7.com`、 `s7d2.scene7.com`或 `s7d13.scene7.com`)。

   若要尋找您的網域，請登入您的公司帳戶或帳戶。

   點選「 **[!UICONTROL 設定>應用程式設定>一般設定」]**。 尋找標示為「已發佈伺服 **[!UICONTROL 器名稱」的欄位]**。 如果您目前使用一般網域，則可請求移至您自己的自訂網域，做為轉換的一部分。

* 請勿要求CMYK JPEG影像。 智慧型影像處理功能會將CMYK JPEG影像轉換為RGB。 如果您需要取得CMYK JPEG影像，就無法使用智慧型影像。

## 為我的帳戶啟用智慧型影像的程式為何？ {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

您必須提出使用智慧型影像的要求；不會自動啟用。

1. 啟動技術支援要求(電子郵件：s7support@adobe.com)。
1. 在您的支援要求中提供下列資訊：

   1. 主要聯絡人姓名、電子郵件、電話。
   1. 所有要啟用智慧型影像功能的網域（即images.company.com或mycompany.scene7.com）。

      若要尋找您的網域，請登入您的公司帳戶或帳戶。

      按一 **[!UICONTROL 下「設定>應用程式設定>一般設定」]**。

      尋找標示為「已發佈伺服 **[!UICONTROL 器名稱」的欄位]**。
   1. 確認您是否透過Adobe使用CDN，而且未透過直接關係進行管理。
   1. 確認您使用的是專用網域(如 `images.company.com` 或 `mycompany.scene7.com`)，而非一般網域(如、、 `s7d1.scene7.com`、) `s7d2.scene7.com``s7d13.scene7.com`。

      若要尋找您的網域，請登入您的公司帳戶或帳戶。

      按一 **[!UICONTROL 下「設定>應用程式設定>一般設定」]**。

      尋找標示為「已發佈伺服 **[!UICONTROL 器名稱」的欄位]**。 如果您目前使用一般的Dynamic Media Classic網域，則可請求移至您自己的自訂網域，做為轉換的一部分。
   1. 指出您是否也需要此功能才能透過HTTP/2運作

1. 技術支援將根據提交請求的順序將您添加到智慧映像客戶等待清單。
1. 當Adobe準備好處理您的要求時，支援人員將會聯絡您以協調並設定目標日期。
1. 可選：您可以選擇在Staging中測試智慧型影像，然後Adobe將新功能推展至生產環境。
1. 完成後，支援會通知您。
1. 為了最大化智慧型影像的效能提升，Adobe建議將「存留時間(TTL)」設為24小時或更長。 TTL會定義CDN快取資產的時間長度。 要更改此設定，請：

   1. 如果您使用Dynamic Media Classic，請按一下「 **[!UICONTROL 設定>應用程式設定>發佈設定>影像伺服器]**」。 將「預 **[!UICONTROL 設用戶端快取時間」設為]** 24或更長的「即時」值。
   1. 如果您使用動態媒體，請依照 [這些指示](config-dynamic.md)。 將「過 **[!UICONTROL 期]** 」值設為24小時或更長。

## 我何時可以期待我的帳戶啟用智慧型影像功能？ {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

請求的處理順序依技術支援部門接收的順序，依等待清單而定。

>[!NOTE]
可能需要較長的前置時間，因為啟用智慧映像需要清除快取。 因此，在任何指定時間，都只能處理少數客戶轉場。

## 改用智慧型影像處理有哪些風險？ {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

轉換為智慧型影像會清除CDN中的快取，因為它涉及在AEM上移至Dynamic Media Classic或Dynamic Media的新組態。

在初始轉換期間，非快取的影像會直接點擊Adobe的原始伺服器，直到重新建立快取為止。 因此，Adobe計劃一次處理數個客戶轉場，以便在從我們的來源提取要求時仍能維持可接受的效能。 對於大部分客戶，快取會在約1至2天內在CDN中重新完整建立。

## 如何驗證智慧型影像是否如預期般運作？  {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 在您的帳戶設定智慧型影像後，請在瀏覽器上載入Dynamic Media Classic(S7)/Dynamic Media影像URL。
1. 在瀏覽器中按一下「檢視>開 **[!UICONTROL 發人員>開發人員工具]** 」，以開啟Chrome開發人員窗格。 或選擇您選擇的任何瀏覽器開發人員工具。

1. 請確定開啟開發人員工具時已停用快取。

   1. 在Windows上，導覽至「開發人員工具」窗格中的設定，然後選取「停用快取( **[!UICONTROL 在開啟裝置工具時)」核取方塊]** 。
   1. 在Mac上，在開發人員窗格的「網路」索引標籤 **[!UICONTROL 下]** ，選取 **[!UICONTROL 停用快取]** 。

1. 在初始要求時，影像將無法最佳化。 通常，如果最佳化的影像不在CDN快取中，傳回該影像需要約15分鐘。
1. 觀察「內容類型」已轉換為適當的格式。 下列螢幕擷取顯示在Chrome上動態轉換為WebP的PNG影像。
1. 在不同的瀏覽器和使用者條件上重複此測試。

>[!NOTE]
並非所有影像都會轉換。 智慧型影像功能決定是否需要轉換來改善效能。 在某些情況下，如果沒有預期的效能提升，則不會轉換影像。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

