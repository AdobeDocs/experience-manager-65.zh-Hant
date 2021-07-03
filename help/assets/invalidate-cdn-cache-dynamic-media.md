---
title: 透過Dynamic Media使CDN快取失效
description: 使您的CDN（內容傳遞網路）快取內容失效可讓您快速更新由Dynamic Media傳送的資產，而不必等待快取過期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
exl-id: 23d3c274-0736-49f7-8d44-a56a55cfd06d
feature: CDN快取
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 1%

---

# 透過Dynamic Media使CDN快取失效 {#invalidating-cdn-cache-for-dm-assets}

Dynamic Media資產會由CDN（內容傳遞網路）快取，以快速傳遞給客戶。 不過，當您更新這些資產時，您希望這些變更立即在您的網站上生效。 清除或使CDN快取失效，可讓您快速更新由Dynamic Media傳送的資產。 您不必等待快取透過TTL（存留時間）值（預設為10小時）過期，而是可以在Dynamic Media內傳送要求，讓快取在數分鐘內過期。

>[!NOTE]
>
>若要使用此功能，您必須使用隨Adobe Experience Manager Dynamic Media提供的現成可用CDN。 此功能不支援任何其他自訂CDN。

>[!IMPORTANT]
>
>下列步驟僅適用於Adobe Experience Manager 6.5、Service Pack 6(Experience Manager6.5.6)或更新版本中的Dynamic Media - Scene7模式。 此CDN失效功能也要求您使用隨Experience ManagerDynamic Media提供的現成可用CDN;不支援任何其他自訂CDN。<br>如果您在Experience Manager6.5、Service Pack 5(Experience Manager6.5.5)或更舊版本中使用Dynamic Media，請依照透過Dynamic Media  [Classic使CDN快取失效中的步驟](/help/assets/invalidate-cdn-cache-dm-classic.md)操作。

另請參閱[Dynamic Media中的快取概述](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)。

**若要使Dynamic Media資產的CDN快取內容無效：**

*第1部分，共2部分：建立CDN失效範本*

1. 在Experience Manager6.5.6或更新版本中，點選「 **[!UICONTROL 工具>資產> CDN失效]**」。

   ![CDN驗證功能](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. 在&#x200B;**[!UICONTROL CDN失效範本]**&#x200B;頁面上，根據您的案例執行下列其中一個選項：

   | 藍本 | 選項 |
   | --- | --- |
   | 我過去已使用Dynamic Media Classic建立CDN失效範本。 | **[!UICONTROL 建立範本]**&#x200B;文字欄位已預先填入您的範本資料。 在這種情況下，您可以編輯範本，或繼續下一個步驟。 |
   | 我必須建立一個模板。 我要輸入什麼？ | 在&#x200B;**[!UICONTROL 建立範本]**&#x200B;文字欄位中，輸入參考`<ID>`的影像URL（包括影像預設集或修飾元），而非下列範例中的特定影像ID:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>如果範本僅包含`<ID>`，則Dynamic Media會填入`https://<publishserver_name>/is/image/<company_name>/<ID>`，其中`<publishserver_name>`是Dynamic Media Classic中「一般設定」中所定義之發佈伺服器的名稱。 `<company_name>`是與此Experience Manager例項相關聯的公司根目錄名稱，而`<ID>`是透過資產選擇器選取而失效的資產。<br>任何預設集/修 `<ID>` 飾元貼文都會照原樣在URL定義中複製。<br>只有影像(即 `/is/image` )才能根據範本自動形成。<br>若為 `/is/content/`，使用資產選擇器新增視訊或PDF等資產不會自動產生URL。您必須改為在「CDN失效」範本中指定此類資產，或者您可以在&#x200B;*第2部分的手動將URL新增至這類資產：設定CDN失效選項*。<br>**範例：**<br>&#x200B;在第一個範例中，失效範本包 `<ID>` 含與具有的資產URL `/is/content`。例如， `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`。 Dynamic Media會根據此路徑來形成URL，其中`<ID>`是您要使其失效的資產選擇器中選取的資產。<br>在第二個範例中，失效範本包含Web屬性中使用之資產的完整URL，且 `/is/content` 與資產選擇器無關。例如，`http://my.publishserver.com:8080/is/content/dms7snapshot/backpack`其中背包是資產ID。<br>Dynamic Media支援的資產格式可失效。CDN失效支援的&#x200B;*not*&#x200B;資產檔案類型包括PostScript®、Encapsuled PostScript®、Adobe Illustrator、Adobe InDesign、Microsoft Powerpoint、Microsoft Excel、Microsoft Word和RTF格式。<br>建立範本時，請務必注意語法和錯字；Dynamic Media不進行任何範本驗證。<br>在此CDN失效範本或第2部分的「新增URL」文字欄位中， **[!UICONTROL 指]** 定影像智慧裁 *切的URL:設定CDN失效選項。*<br>**重要：**CDN失效範本中的每個項目必須位於各自的行上。<br>*下列範本範例僅供說明之用。* |

   ![CDN失效範本 — 建立](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. 在&#x200B;**[!UICONTROL CDN失效範本]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 儲存]**，然後點選&#x200B;**[!UICONTROL 確定]**。<br>

   *第2部分（共2部分）:設定CDN失效選項*
   <br>

1. 在Experience Manager作為Cloud Service時，點選「**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL CDN失效]**」。

   ![CDN驗證功能](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. 在「**[!UICONTROL CDN失效 — 新增詳細資料]**」頁面上，選取CDN失效的資產。

   ![CDN失效 — 新增詳細資料](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >如果您決定不勾選「使CDN ]***和***[!UICONTROL &#x200B;根據範本&#x200B;]**無效」選項，則選定資產的基本URL會形成為無效。**[!UICONTROL &#x200B;僅對影像使用此選項排列。


   | 選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 使 CDN 中與影像預設集相關聯的資產失效]** | （選用）勾選此選項時，系統會自動形成選取的資產及其所有相關的影像預設集URL，以利快取失效。<br>資產及其相關聯的預先定義預設URL會自動形成為無效。此選項僅適用於影像資產。 |
   | **[!UICONTROL 根據範本失效]** | （選用）核取此選項，僅使用已定義的範本來形成URL。 |
   | **[!UICONTROL 新增資產]** | 使用「資產選擇器」來選取您要使其無效的資產。 您可以選取已發佈或未發佈的資產。<br>CDN的快取是以URL為基礎，而非以資產為基礎。因此，您必須注意您網站上的完整URL。 在您決定這些URL後，即可將它們新增至範本。 接著，您可以選取並新增這些資產，並在單一步驟中使URL無效。 <br>此選項可搭配「使 **[!UICONTROL CDN中與資產相關聯的影像預設集無效]**」、「根 **[!UICONTROL 據範本無效]**」或兩者搭配使用。 |
   | **[!UICONTROL 新增 URL]** | 手動新增或貼上完整的URL路徑至您要使其CDN快取失效的Dynamic Media資產。 如果您未在&#x200B;***第1部分（共2部分）中建立CDN失效範本，請使用此選項：建立CDN失效範本***，且只有少數資產可使其失效。<br>**重要：** 您新增的每個URL都必須位於各自的行上。<br>您一次最多可使1000個URL無效。如果「**[!UICONTROL 新增URL]**」文字欄位中的URL數大於1000，則您無法點選「**[!UICONTROL 下一步]**」。 在這種情況下，您必須點選所選資產右側的&#x200B;**[!UICONTROL X]**，或手動新增的URL，以從失效清單中刪除該資產。<br>在「CDN失效」範本或此「新增URL」文字欄位中，指定影像智慧 **[!UICONTROL 裁]** 切的URL。 |

1. 在頁面的右上角附近，點選&#x200B;**[!UICONTROL Next]**。
1. 在&#x200B;**[!UICONTROL CDN失效 — 確認]**&#x200B;頁面的&#x200B;**[!UICONTROL URL]**&#x200B;清單方塊中，您會看到一或多個從先前建立的CDN失效範本產生的URL清單，以及您剛新增的資產。

   例如，使用先前步驟中顯示的CDN失效範本範例，假設您新增了名為`spinset`的單一資產。 當您點選「**[!UICONTROL 工具>資產> CDN失效]**」時，會在「**[!UICONTROL CDN失效 — 確認]**」使用者介面中產生下列五個URL:

   ![CDN失效 — 確認](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   如有必要，請點選URL右側的&#x200B;**X**，以將其從失效程式中刪除。

1. 在頁面的右上角附近，點選&#x200B;**[!UICONTROL Submit]**&#x200B;以開始CDN失效程式。

## 疑難排解CDN失效錯誤

在所有情況下，會處理整個批次以失效，或處理整個批次失敗。

| 錯誤 | 說明 |
| --- | --- |
| *無法擷取所選資產的URL。* | 若符合下列任一情況，則發生：<br> — 找不到Dynamic Media設定。<br> — 擷取可透過讀取Dynamic Media設定的服務使用者時發生例外狀況。<br>-Dynamic Media設定中缺少發佈伺服器或用來形成URL的公司根。 |
| *有些URL未正確定義。更正並重新提交。* | 如果IPS CDN快取失效API傳回錯誤，表示URL引用了其他公司，則會發生此情況。 或者，如果URL無法如IPS `cdnCacheInvalidation` API所完成的驗證所示有效。 |
| *無法使CDN快取失效。* | 當CDN快取失效請求因任何其他原因而失敗時發生。 |
| *輸入的URL無效。* | 如果「**[!UICONTROL CDN失效 — 確認]**」頁面中沒有URL，且您點選「**[!UICONTROL 提交]**」，即會發生。 |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
