---
title: 透過Dynamic Media使內容傳遞網路快取失效
description: 使CDN （內容傳遞網路）快取內容失效，可讓您快速更新Dynamic Media所傳遞的資產，而非等候快取過期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
feature: CDN Cache
exl-id: 23d3c274-0736-49f7-8d44-a56a55cfd06d
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 1%

---


# 透過 Dynamic Media 使 CDN 快取失效 {#invalidating-cdn-cache-for-dm-assets}

CDN （內容遞送網路）會快取Dynamic Media資產，以快速遞送給您的客戶。 不過，當您更新這些資產時，希望這些變更立即在您的網站上生效。 清除或使CDN快取失效，可讓您快速更新Dynamic Media傳送的資產。 您不必使用TTL （存留時間）值（預設為10小時）來等待快取過期，而是可以從Dynamic Media中傳送請求，讓快取在幾分鐘內過期。



>[!IMPORTANT]
>
>下列步驟僅適用於Adobe Experience Manager 6.5、Service Pack 6 (Experience Manager 6.5.6)或更新版本中的Dynamic Media - Scene7模式。 此CDN失效功能還需要您使用Adobe Experience Manager - Dynamic Media隨附的現成可用CDN。 此功能不支援任何其他自訂CDN。<br>如果您在Experience Manager6.5、Service Pack 5 (Experience Manager6.5.5)或更舊版本中使用Dynamic Media，請依照[透過Dynamic Media Classic使CDN快取失效](/help/assets/invalidate-cdn-cache-dm-classic.md)中的步驟操作。

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Caching overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**若要使Dynamic Media資產的CDN快取內容失效：**

*第1部分（共2部分）：建立CDN失效範本*

1. 在Experience Manager6.5.6或更新版本中，導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL CDN失效]**。

   ![CDN驗證功能](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. 在&#x200B;**[!UICONTROL CDN失效範本]**&#x200B;頁面上，根據您的情境執行下列其中一個選項：

   | 情境 | 選項 |
   | --- | --- |
   | 我過去曾使用Dynamic Media Classic建立CDN失效範本。 | **[!UICONTROL 建立範本]**&#x200B;文字欄位已預先填入您的範本資料。 在這種情況下，您可以編輯範本，或繼續下一步驟。 |
   | 我必須建立範本。 我該輸入什麼？ | 在&#x200B;**[!UICONTROL 建立範本]**&#x200B;文字欄位中，輸入參考`<ID>`的影像URL （包括影像預設集或修飾元），而不是如下列範例所示的特定影像ID：<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>如果範本僅包含`<ID>`，則Dynamic Media會填入`https://<publishserver_name>/is/image/<company_name>/<ID>`，其中`<publishserver_name>`是在Dynamic Media Classic的「一般設定」中定義的Publish伺服器名稱。 `<company_name>`是與此Experience Manager執行個體相關聯之公司根的名稱，而`<ID>`是透過要失效的資產選擇器選取的資產。<br>任何張貼`<ID>`的預設集/修飾詞都會照原樣在URL定義中複製。<br>只有影像（亦即`/is/image`）可根據範本自動形成。<br>若為`/is/content/`，使用資產選擇器新增視訊或PDF等資產不會自動產生URL。 反之，您必須在CDN失效範本中指定這類資產，或者可以在&#x200B;*第2部分（共2部分）：設定CDN失效選項*&#x200B;中手動將URL新增到這類資產。<br>**範例：**<br>&#x200B;在第一個範例中，失效範本包含`<ID>`以及具有`/is/content`的資產URL。 例如 `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`。Dynamic Media會根據此路徑建立URL，`<ID>`為透過您要失效的資產選擇器選取的資產。<br>在第二個範例中，失效範本包含您Web屬性中所使用之資產的完整URL，其中包含`/is/content` （不依存於資產選擇器）。 例如，`http://my.publishserver.com:8080/is/content/dms7snapshot/backpack`，其中揹包是資產識別碼。<br>Dynamic Media支援的資產格式符合失效資格。 *不*&#x200B;支援CDN失效的資產檔案型別包括PostScript®、EncapsulatedPostScript®、Adobe Illustrator、Adobe InDesign、Microsoft®Powerpoint、Microsoft®Excel、Microsoft®Word和RTF格式。<br><br>·當您建立範本時，請務必留意語法和拼寫錯誤；Dynamic Media不會進行任何範本驗證。<br>· CDN失效範本最多可儲存2500個字元的文字。<br>·在此CDN失效範本，或在&#x200B;*第2部分：設定CDN失效選項的&#x200B;**[!UICONTROL 新增URL]**&#x200B;文字欄位中，指定影像智慧型裁切的URL。*<br>· CDN失效範本中的每個專案都必須位於其自己的行。<br>·下列CDN失效範本範例僅供示範之用。 |

   ![CDN失效範本 — 建立](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >CDN失效範本最多可儲存2500個字元的文字。

1. 在&#x200B;**[!UICONTROL CDN失效範本]**&#x200B;頁面的右上角，選取&#x200B;**[!UICONTROL 儲存]**，然後選取&#x200B;**[!UICONTROL 確定]**。<br>
   *第2部分（共2部分）：設定CDN失效選項*
   <br>

1. 在Experience Manageras a Cloud Service中，選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL CDN失效]**。

   ![CDN驗證功能](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. 在「**[!UICONTROL CDN失效 — 新增詳細資料]**」頁面上，選取CDN失效的資產。

   ![CDN失效 — 新增詳細資料](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >如果您決定保留&#x200B;**[!UICONTROL 使CDN中與影像預設集相關聯的資產失效]** *和* **[!UICONTROL 根據範本]**&#x200B;失效的選項未勾選，則所選資產的基底URL會形成為失效。 僅針對影像使用此選項排列。


   | 選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 使CDN]**&#x200B;中與影像預設集相關聯的資產失效 | （可選）當您核取此選項時，選取的資產及其所有關聯的影像預設集URL會自動形成，以供快取失效。<br>Assets及其相關之預先定義的預設URL會自動形成以失效。 此選項僅適用於影像資產。 |
   | **[!UICONTROL 依據範本失效]** | （選擇性）核取此選項以僅使用定義的範本來形成URL。 |
   | **[!UICONTROL 新增Assets]** | 使用資產選擇器來選取您要失效的資產。 您可以選取已發佈或未發佈的資產。<br>在CDN的快取是以URL為基礎，而非以資產為基礎。 因此，您必須注意您網站上的完整URL。 決定這些URL後，您就可以將它們新增至範本。 然後，您可以選取並新增這些資產，並在單一步驟中使URL失效。 <br>使用此選項搭配&#x200B;**[!UICONTROL 使CDN]**&#x200B;中與影像預設集相關聯的資產失效&#x200B;**[!UICONTROL 、或根據範本]**&#x200B;失效（或兩者）。 |
   | **[!UICONTROL 新增URL]** | 手動將完整URL路徑新增或貼到您想要讓CDN快取失效的Dynamic Media資產。 如果您未在&#x200B;***第1部分（共2部分）：建立CDN失效範本***&#x200B;中建立CDN失效範本，而且只有少數資產要失效，請使用此選項。<br>**重要：**&#x200B;您新增的每個URL都必須在其自己的行上。<br>您一次最多可以使1000個URL失效。 如果&#x200B;**[!UICONTROL 新增URL]**&#x200B;文字欄位中的URL數目大於1000，則無法選取&#x200B;**[!UICONTROL 下一步]**。 在這種情況下，您必須選取所選資產右側的&#x200B;**[!UICONTROL X]**，或選取手動新增的URL，將其從失效清單中刪除。<br>在CDN失效範本或此&#x200B;**[!UICONTROL 新增URL]**&#x200B;文字欄位中，指定影像智慧型裁切的URL。 |

1. 在頁面的右上角附近，選取&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL CDN失效 — 確認]**&#x200B;頁面的&#x200B;**[!UICONTROL URL]**&#x200B;清單方塊中，您可以看到一或多個從您先前建立的CDN失效範本產生的URL清單以及您剛才新增的資產。

   例如，使用先前步驟中顯示的CDN失效範本範例，假設您新增了名為`spinset`的單一資產。 當您導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL CDN失效]**&#x200B;時，會在&#x200B;**[!UICONTROL CDN失效 — 確認]**&#x200B;使用者介面中產生下列五個已產生的URL：

   ![CDN失效 — 確認](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   必要時，選取URL右側的&#x200B;**X**，將其從失效程式中刪除。

1. 在頁面的右上角附近，選取&#x200B;**[!UICONTROL 提交]**&#x200B;以開始CDN失效程式。

## 疑難排解CDN失效錯誤

在所有情況下，要麼處理整個批次以使其失效，要麼處理整個批次以使其失敗。

| 錯誤 | 解釋 |
| --- | --- |
| *無法擷取所選資產的URL。* | 符合下列任一情況時發生： <br> — 找不到Dynamic Media設定。<br> — 擷取讀取Dynamic Media設定的服務使用者時發生例外狀況。<br>- Dynamic Media設定中遺失Publish伺服器或用來組成URL的公司根目錄。 |
| *部分URL未正確定義。 更正並重新提交。* | 當IPS CDN快取失效API傳回URL參考其他公司的錯誤時發生。 或者，如果URL根據IPS `cdnCacheInvalidation` API完成的驗證無效。 |
| *無法使CDN快取失效。* | 當CDN快取失效請求因任何其他原因而失敗時發生。 |
| *沒有輸入要失效的URL。* | 如果&#x200B;**[!UICONTROL CDN失效 — 確認]**&#x200B;頁面中沒有URL，而且您選取&#x200B;**[!UICONTROL 提交]**，就會發生。 |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
