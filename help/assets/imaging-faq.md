---
title: 智慧型影像處理
description: 智慧型影像功能可套用每位使用者獨特的檢視特性，自動提供最適合其體驗的影像，進而提升效能與參與度。
uuid: c11e52ba-8d64-4dc5-b30a-fc10c2b704e5
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
translation-type: tm+mt
source-git-commit: 996780c3fac85f0ce0deeddd5ff4e74e01df436e
workflow-type: tm+mt
source-wordcount: '1876'
ht-degree: 1%

---


# 智慧型影像 {#smart-imaging}

## 什麼是「智慧型影像」?{#what-is-smart-imaging}

智慧型影像技術運用Adobe Sensei AI功能，並與現有的「影像預設集」搭配使用，根據用戶端瀏覽器功能自動最佳化影像格式、大小和品質，以增強影像傳送效能。

>[!NOTE]
>
>這項功能需要您使用Adobe Experience Manager Dynamic Media隨附的現成可用CDN。 此功能不支援任何其他自訂CDN。

Smart Imaging也受益於與Adobe同級最佳的優質CDN服務完全整合的額外效能提升。 此服務可在伺服器、網路和互連點之間找到最佳的Internet路由。 它查找的路由具有最低的延遲和最低的資料包丟失率，而不是使用Internet上的預設路由。

以下影像資產範例說明新增的智慧型影像最佳化：

| 影像<br>(URL) | 縮圖 | 大小<br>(JPEG) | 大小(WebP)<br>（含智慧映像） | 減少% |
|---|---|---|---|---|
| [影像1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![pictore1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [影像2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![pictore2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [影像3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [影像4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | 平均= 51% |

類似於上述，Adobe也透過即時客戶網站的7009個URL執行測試。 由於智慧型影像功能，他們平均可進一步將JPEG檔案大小最佳化38%，並將WebP格式的PNG檔案大小最佳化31%。

## 最新Smart Imaging的主要優點是什麼？{#what-are-the-key-benefits-of-smart-imaging}

由於影像是頁面載入時間的絕大部分，因此效能的提升會對業務產生深遠的影響，例如更高的轉換率、網站逗留時間以及較低的網站反彈率。

最新版Smart Imaging的增強功能：

* 立即提供最佳化內容（在執行時期）。
* 使用Adobe Sensei技術，根據影像要求中指定的品質(qlt)進行轉換。
* 智慧型影像可以使用「bfc」 URL參數關閉。
* TTL（存留時間）獨立。 以前，Smart Imaging的最低TTL為12小時。
* 以前，原始和衍生影像都會進行快取，而使快取失效的步驟是2個步驟。 在最新的智慧型影像中，只有衍生產品會被快取，允許單步驟快取失效程式。
* 在規則集中使用自訂標題的客戶。 例如，[新增自訂標頭值至影像回應|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)中建議的「允許原點計時」、「X-Robot」。 它們可以從最新的Smart Imaging中獲益，因為與舊版Smart Imaging不同，這些標頭不會被阻止。

## 智慧型影像處理是否有相關的授權成本？{#are-there-any-licensing-costs-associated-with-smart-imaging}

否. Smart Imaging隨附於您現有的Dynamic Media Classic或Adobe Experience Manager - Dynamic Media（On-prem、AMS和AEM雲端服務）授權中。

>[!NOTE]
>
>Smart Imaging不適用於Dynamic Media - Hybrid客戶。


## 智慧型影像處理如何運作？{#how-does-smart-imaging-work}

當消費者要求影像時，智慧型影像功能會檢查使用者特性，並根據使用中的瀏覽器轉換為適當的影像格式。 這些格式轉換的方式不會降低視覺精確度。 智慧型影像功能可根據瀏覽器功能，以下列方式自動將影像轉換為不同格式。

* 針對下列瀏覽器自動轉換為WebP:
   * Chrome
   * Firefox
   * Microsoft Edge
   * Safari 14.0 +
      * Safari 14僅包含iOS 14.0和更新版本，以及macOS BigSur和更新版本
   * Android
   * Opera
* 舊版瀏覽器支援：

   | 瀏覽器 | 瀏覽器／作業系統版本 | 格式 |
   | --- | --- | --- |
   | Safari | iOS 14.0或更舊版本 | JPEG2000 |
   | Edge | 18或舊版 | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* 對於不支援這些格式的瀏覽器，會提供原本要求的影像格式。

如果原始影像大小小於智慧型影像產生的大小，則會提供原始影像。

## 支援哪些影像格式？{#what-image-formats-are-supported}

智慧型影像支援下列影像格式：
* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## 智慧型影像處理如何與我現有已使用的影像預設集搭配運作？{#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

Smart Imaging可與您現有的「影像預設集」搭配使用，並在所要求的檔案格式為JPEG或PNG時，會觀察所有影像設定，但品質(qlt)和格式(fmt)除外。 對於格式轉換，智慧型影像功能可維持影像預設集設定所定義的完整視覺完整性，但檔案大小較小。 如果原始影像大小小於智慧型影像產生的大小，則會提供原始影像。

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## 我是否必須變更任何URL、影像預設集，或在我的網站上部署智慧型影像的新程式碼？{#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

如果您在現有的自訂網域上設定Smart Imaging,Smart Imaging將可與您現有的影像URL和影像預設集順暢地運作。 此外，智慧型影像功能不需要您在網站上新增任何程式碼來偵測使用者的瀏覽器。 這些都會自動處理。

如果您必須設定新的自訂網域以使用智慧型影像，則必須更新URL以反映此自訂網域。

要瞭解Smart Imaging的先決條件，請參閱[我是否有資格使用Smart Imaging?](#am-i-eligible-to-use-smart-imaging)。

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## 智慧型影像是否可與HTTPS搭配運作？ HTTP/2如何？{#does-smart-imaging-working-with-https-how-about-http}

智慧型影像可處理透過HTTP或HTTPS傳送的影像。 此外，它也可透過HTTP/2運作。

## 我是否符合使用智慧型影像的資格？{#am-i-eligible-to-use-smart-imaging}

若要使用Smart Imaging，您公司的AEM帳戶上的Dynamic Media Classic或Dynamic Media必須符合下列需求：

* 使用Adobe搭售的CDN（內容放送網路）做為您授權的一部分。
* 使用專用網域（例如`images.company.com`或`mycompany.scene7.com`），而不使用一般網域（例如`s7d1.scene7.com`、`s7d2.scene7.com`或`s7d13.scene7.com`）。

若要尋找您的網域，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或帳戶。

點選「**[!UICONTROL 設定>應用程式設定>一般設定」。]** 查找標有「已發佈伺服器 **[!UICONTROL 名稱」的欄位。]** 如果您目前使用一般網域，在提交技術支援票證時，可以請求移轉至您自己的自訂網域，做為此移轉的一部分。

您的第一個自訂網域不需額外付費，只要取得Dynamic Media授權即可。

## 為我的帳戶啟用Smart Imaging的過程是什麼？{#what-is-the-process-for-enabling-smart-imaging-for-my-account}

您會提出使用智慧型影像的要求；不會自動啟用。

1. [使用Admin Console建立支援案例。](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
1. 在您的支援案例中提供下列資訊：

   1. 主要聯絡人姓名、電子郵件、電話。
   1. 要啟用智慧映像的所有域（即`images.company.com`或`mycompany.scene7.com`）。

      若要尋找您的網域，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或帳戶。

      按一下&#x200B;**[!UICONTROL 設定>應用程式設定>常規設定。]**

      查找標有&#x200B;**[!UICONTROL 「已發佈伺服器名稱」的欄位。]**
   1. 確認您是否透過Adobe使用CDN，而且未透過直接關係進行管理。
   1. 確認您使用的是專用網域，例如`images.company.com`或`mycompany.scene7.com`，而不是通用網域，例如`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com`。

      若要尋找您的網域，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或帳戶。

      按一下&#x200B;**[!UICONTROL 設定>應用程式設定>常規設定。]**

      查找標有&#x200B;**[!UICONTROL 「已發佈伺服器名稱」的欄位。]** 如果您目前使用一般的Dynamic Media Classic網域，則可請求移至您自己的自訂網域，做為轉換的一部分。
   1. 指出它是否必須透過HTTP/2運作。

1. Adobe客戶服務會根據提交請求的順序，將您加入智慧型影像客戶等待清單。
1. 當Adobe準備好處理您的要求時，支援會聯絡您以協調並設定目標日期。
1. **可選**:您可以選擇在Staging中測試智慧型影像，然後Adobe將新功能推展至生產環境。
1. 完成後，支援會通知您。
1. 為充份提升智慧型影像處理的效能，Adobe建議將「存留時間(TTL)」設定為24小時或更長。 TTL會定義CDN快取資產的時間長度。 要更改此設定，請：

   1. 如果您使用Dynamic Media Classic，請按一下「**[!UICONTROL 設定>應用程式設定>發佈設定>影像伺服器」。]** 將「預 **[!UICONTROL 設用戶端快取時間」設]** 為「即時值」24或更長。
   1. 如果您使用動態媒體，請依照[這些指示](config-dynamic.md)進行。 將&#x200B;**[!UICONTROL Expiration]**&#x200B;值設為24小時或更長。

## 我何時可以期待我的帳戶啟用Smart Imaging?{#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

客戶服務會根據等待清單，依照收到請求的順序處理請求。

>[!NOTE]
啟用「智慧型影像」需要Adobe清除快取，因此可能需要較長的前置時間。 因此，在任何指定時間，都只能處理少數客戶轉場。

## 切換到使用Smart Imaging時有哪些風險？{#what-are-the-risks-with-switching-over-to-use-smart-imaging}

客戶網頁沒有風險。 不過，轉換至Smart Imaging會清除CDN中的快取，因為它涉及在Experience Manager上移至Dynamic Media Classic或Dynamic Media的新組態。

在初始轉換期間，非快取的影像會直接點擊Adobe的原始伺服器，直到重新建立快取為止。 因此，Adobe計劃一次處理數個客戶轉場，如此當從來源提取要求時，就能維持可接受的效能。 對於大部分客戶，快取會在約1 - 2天內在CDN中重新完整建立。

## 如何驗證智慧映像是否如預期般工作？{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 在您的帳戶設定智慧型影像後，請在瀏覽器上載入Dynamic Media Classic或Adobe Experience Manager - Dynamic Media影像URL。
1. 在瀏覽器中按一下「**[!UICONTROL 檢視>開發人員>開發人員工具]**」，以開啟Chrome開發人員窗格。 或者，選擇您選擇的任何瀏覽器開發人員工具。

1. 請確定開啟開發人員工具時已停用快取。

   * 在Windows上——導覽至「開發人員工具」窗格中的設定，然後選取「停用快取（在開啟裝置工具時）」]**核取方塊。**[!UICONTROL 
   * 在Mac上——在開發人員窗格的&#x200B;**[!UICONTROL Network]**&#x200B;標籤下，選擇&#x200B;**[!UICONTROL disable cache]**。

1. 觀察「內容類型」已轉換為適當的格式。 下列螢幕擷取顯示在Chrome上動態轉換為WebP的PNG影像。
1. 在不同的瀏覽器和使用者條件上重複此測試。

>[!NOTE]
並非所有影像都會轉換。 Smart Imaging決定轉換是否可以改善效能。 有時，若沒有預期的效能提升，或格式不是JPEG或PNG，則不會轉換影像。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## 是否可以針對任何請求關閉智慧映像？{#turning-off-smart-imaging}

是. 您可以將修飾詞`bfc=off`新增至URL，以關閉智慧型影像。

## 有哪些「調整」可用？ 是否有可定義的設定或行為？ (#tuning-settings)

目前，您可以選擇啟用或禁用智慧映像。 沒有其他調整功能可用。

## 如果「智慧映像」管理質量設定，我是否可以設定最小和最大值？ 例如，是否可設定「不低於60」和「不高於80品質」? (#minimum-maximum)

當前的Smart Imaging中沒有這種資源調配功能。

## 有時，JPEG影像會傳回至Chrome，而非WebP影像。 為什麼？ (#jpeg-webp)

智慧型影像功能可判斷轉換是否有益。 只有當轉換導致檔案大小較小且品質相當時，才會傳回新影像。
