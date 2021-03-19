---
title: 通過Dynamic Media使CDN快取失效
description: 停用您的CDN（內容傳送網路）快取內容可讓您快速更新由Dynamic Media傳送的資產，而不需等待快取過期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
role: 業務從業人員、管理員
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 1%

---


# 透過Dynamic Media{#invalidating-cdn-cache-for-dm-assets}使CDN快取失效

Dynamic Media資產由CDN（內容傳送網路）快取，以便快速傳送給客戶。 不過，當您更新這些資產時，您會希望這些變更立即在您的網站上生效。 清除或停用CDN快取可讓您快速更新由Dynamic Media傳送的資產。 您不必等待快取使用TTL（存留時間）值（預設值為10小時）過期，而是可從Dynamic Media傳送要求，讓快取在數分鐘內過期。

>[!NOTE]
>
>此功能需要您使用隨附於Adobe Experience Manager·Dynamic Media的現成可用CDN。 此功能不支援任何其他自訂CDN。

>[!IMPORTANT]
>
>以下步驟僅適用於Dynamic Media-Scene7模式(在Adobe Experience Manager6.5、Service Pack 6(Experience Manager6.5.6)或更高版本)。 此CDN失效功能也要求您使用隨附於Experience ManagerDynamic Media的現成可用CDN;不支援任何其他自訂CDN。<br>如果您在Dynamic Media6.5、Service Pack 5(Experience Manager6.5.5)或更舊版本中使用Experience Manager，請依照使用Dynamic Media·Classic讓CDN快取失效中的步驟進行。 [](/help/assets/invalidate-cdn-cache-dm-classic.md)

另請參閱「Dynamic Media的快取概觀」中的「a0/>快取概觀」。[](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)

**若要使您的CDN快取內容無效用於Dynamic Media資產：**

*第1部分（共2部分）:建立CDN失效範本*

1. 在Experience Manager6.5.6或更新版本中，點選「**[!UICONTROL 工具>資產> CDN失效」。]**

   ![CDN驗證功能](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. 在&#x200B;**[!UICONTROL CDN失效範本]**&#x200B;頁面上，根據您的藍本執行下列其中一個選項：

   | 藍本 | 選項 |
   | --- | --- |
   | 我過去已使用Dynamic Media經典建立CDN失效範本。 | **[!UICONTROL 建立範本]**&#x200B;文字欄位已預先填入範本資料。 在這種情況下，您可以編輯範本，或繼續下一步驟。 |
   | 我必須建立範本。 我要輸入什麼？ | 在&#x200B;**[!UICONTROL 建立範本]**&#x200B;文字欄位中，輸入參照`<ID>`的影像URL（包括影像預設集或修飾元），而非下列範例中的特定影像ID:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>如果範本僅包含`<ID>`，則Dynamic Media會填入`https://<publishserver_name>/is/image/<company_name>/<ID>`，其中`<publishserver_name>`是Publish Server中定義的名稱《Dynamic Media經典》中的一般設定。 `<company_name>`是與此Experience Manager實例關聯的公司根目錄的名稱，而`<ID>`是通過要失效的資產選擇器選擇的資產。<br>任何預設集／修飾 `<ID>` 元貼文都會如同在URL定義中複製。<br>只有影像——即， `/is/image` -才能根據範本自動形成。<br>對於 `/is/content/`而言，使用資產選擇器新增資產（例如影片或PDF）並不會自動產生URL。您必須改為在「CDN失效」範本中指定此類資產，或者您可以在&#x200B;*第2部分中手動將URL新增至此類資產：設定CDN失效選項*。<br>**範例：**<br>&#x200B;在第一個範例中，失效範本包含 `<ID>` 與資產URL一起包含 `/is/content`。例如，`http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`。 Dynamic Media會根據此路徑來建立URL，其中`<ID>`是您要使其失效的資產選擇器中選取的資產。<br>在第二個範例中，失效範本包含Web屬性中使用之資產的完整URL，且 `/is/content` 與資產選擇器無關。例如，`http://my.publishserver.com:8080/is/content/dms7snapshot/backpack`其中背包是資產ID。<br>Dynamic Media支援的資產格式可失效。*not*&#x200B;支援的CDN失效資產檔案類型包括PostScript®、封裝PostScript®、Adobe Illustrator、Adobe InDesign、Microsoft Powerpoint、Microsoft Excel、Microsoft Word和Rich Text格式。<br>建立範本時，請務必注意語法和錯字；Dynamic Media不進行任何範本驗證。<br>在此CDN失效範本或第2部分的「新增URL」文字欄位中，為影像智慧裁切指 ****  *定URL:設定CDN失效選項。*<br>**重要：**CDN失效範本中的每個項目都必須位於自己的行上。<br>*以下範本範例僅供圖例之用。* |

   ![CDN失效範本——建立](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. 在&#x200B;**[!UICONTROL CDN失效範本]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 儲存]**，然後點選&#x200B;**[!UICONTROL 確定。]**<br>

   *第2部分（共2部分）:設定CDN失效選項*
   <br>

1. 在Experience Manager為Cloud Service時，點選「**[!UICONTROL 工具>資產> CDN失效」。]**

   ![CDN驗證功能](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. 在&#x200B;**[!UICONTROL CDN失效——新增詳細資料]**&#x200B;頁面上，選取CDN失效的資產。

   ![CDN失效——新增詳細資料](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >如果您決定保留選項&#x200B;**[!UICONTROL 使CDN]** *和* **[!UICONTROL 中與資產相關的影像預設無效，則選定資產的基本URL會形成為無效。]**&#x200B;此選項僅用於影像。


   | 選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 使 CDN 中與影像預設集相關聯的資產失效]** | （可選）勾選此選項時，選取的資產及其所有相關的影像預設集URL都會自動形成，以便快取失效。<br>資產及其相關的預先定義預設URL會自動形成為無效。此選項僅適用於影像資產。 |
   | **[!UICONTROL 基於模板的失效]** | （可選）勾選此選項，僅使用已定義的URL建立範本。 |
   | **[!UICONTROL 新增資產]** | 使用「資產選擇器」來選擇您要廢止的資產。 您可以選取已發佈或未發佈的資產。<br>CDN的快取是以URL為基礎，而非以資產為基礎。因此，您必須注意您網站上的完整URL。 在您決定這些URL後，您可以將它們新增至範本。 然後，您可以選取並新增這些資產，並在單一步驟中使URL無效。 <br>將此選項與CDN中與 **[!UICONTROL 資產相關的影像預設集搭配使用]**，或 **[!UICONTROL 是與範本或兩者搭配使用]**「失效」。 |
   | **[!UICONTROL 新增 URL]** | 手動新增或貼上完整URL路徑至您要使其CDN快取失效的Dynamic Media資產。 如果您未在&#x200B;***第1部分（共2部分）中建立CDN失效範本，請使用此選項：建立CDN失效範本***，且只有少數資產可失效。<br>**重要：** 您新增的每個URL都必須位於自己的行上。<br>您一次最多可以使1000個URL失效。如果&#x200B;**[!UICONTROL 「新增URL]**」文字欄位中的URL數大於1000，則無法點選&#x200B;**[!UICONTROL Next]**。 在這種情況下，您必須點選所選資產右側的&#x200B;**[!UICONTROL X]**&#x200B;或手動新增的URL，才能將其從失效清單中刪除。<br>在「CDN失效」範本或此「新增URL」文字欄位中，指定影像智慧裁切 **[!UICONTROL 的]** URL。 |

1. 在頁面的右上角附近，點選&#x200B;**[!UICONTROL Next.]**
1. 在&#x200B;**[!UICONTROL CDN失效——確認]**&#x200B;頁面上，在&#x200B;**[!UICONTROL URL]**&#x200B;清單方塊中，您會看到您先前建立的CDN失效範本以及您剛新增的資產所產生的一或多個URL清單。

   例如，使用先前步驟中顯示的CDN失效範本範例，假設您新增了名為`spinset`的單一資產。 當您點選「**[!UICONTROL 工具>資產> CDN失效]**」時，會在&#x200B;**[!UICONTROL CDN失效——確認]**&#x200B;使用者介面中產生下列五個產生的URL:

   ![CDN失效——確認](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   如有必要，請點選URL右側的&#x200B;**X**，將其從失效程式中刪除。

1. 在頁面的右上角，點選&#x200B;**[!UICONTROL Submit]**&#x200B;以開始CDN失效程式。

## 疑難排解CDN失效錯誤

在所有情況下，處理整個批以進行失效處理，或處理整個批失敗。

| 錯誤 | 說明 |
| --- | --- |
| *無法擷取選取資產的URL。* | 如果符合下列任一情形，則發生：<br>-找不到Dynamic Media配置。<br>-檢索通過讀取Dynamic Media配置的服務用戶時有例外。<br>-用於形成URL的發佈伺服器或公司根目錄在Dynamic Media組態中遺失。 |
| *有些URL未定義正確。更正並重新提交。* | 發生於IPS CDN快取失效API傳回錯誤，指出URL轉介給其他公司時。 或者，如果URL無效，請依照IPS `cdnCacheInvalidation` API所完成的驗證。 |
| *無法使CDN快取失效。* | 發生於CDN快取失效要求因任何其他原因而失敗時。 |
| *未輸入URL，因此無效。* | 發生於&#x200B;**[!UICONTROL CDN失效——確認]**&#x200B;頁面中沒有URL，且您點選&#x200B;**[!UICONTROL 提交。]** |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
