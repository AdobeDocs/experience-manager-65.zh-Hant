---
title: AEM AEM Forms案頭應用程式
seo-title: AEM desktop app for AEM Forms
description: AEM AEM Forms案頭應用程式
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
role: Admin
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# AEM AEM Forms案頭應用程式 {#aem-desktop-app-for-aem-forms}

AEM案頭應用程式可讓您將Adobe Experience Manager(AEM)Assets存放庫和AEM Forms二進位檔案對應至系統上的網路目錄。 您可以在檔案總管中檢視同步的資產和二進位檔案，並視需要使用各種應用程式來編輯檔案。 除了檢視檔案外，您也可以建立、上傳和刪除二進位檔案。 您也可以直接從軟體開啟、編輯和儲存檔案。 例如，您可以直接從Designer開啟和編輯XDP檔案。 您在本機對資產所做的變更會反映在AEM Assets存放庫和AEM Forms UI。

您可以從AEM例項下載應用程式。 如需下載應用程式的詳細資訊，請參閱 [AEM案頭應用程式發行說明](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html).

## AEM Forms案頭應用程式支援的資產 {#aem-forms-assets-supported-in-aem-desktop-app}

您可以使用應用程式來同步以下類型的AEM Forms二進位檔案：表單模板(.xdp)、PDF表單(.pdf)、文檔(.pdf)、影像、XML架構(.xsd)、樣式表(.xfs)。 應用程式會將所有其他檔案（不支援的檔案）列為0位元組檔案。 將不支援的檔案列為0位元組檔案，可確保使用者知道AEM Forms伺服器上有其他可用資產。

>[!NOTE]
>
>檔案名只能包含英數字元、連字型大小或底線。

## 啟用AEM Forms for AEM案頭應用程式 {#enable-aem-forms-for-aem-desktop-app}

AEM案頭應用程式在Microsoft Windows上使用WebDAV通訊協定，在Mac OS X上使用SMB1連線至AEM Forms伺服器。 AEM Forms伺服器無法立即與WebDAV或SMB用戶端同步二進位檔案和其他資產。 執行下列步驟以啟用AEM案頭應用程式的AEM Forms:

1. 以管理員身分登入AEM Forms。
1. 在製作例項中，按一下 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager >工具]** ![錘](assets/hammer.png) **[!UICONTROL >部署>操作> Web控制台]**. Web控制台在新窗口中開啟。
1. 在Web控制台窗口中，找到並開啟 **[!UICONTROL FormsManager AddOn配置]** 選項。
1. 在「FormsManager AddOn配置」對話框中，取消選擇 **[!UICONTROL 非同步資源]** 複選框，然後按一下 **[!UICONTROL 儲存]**.
1. 重新啟動AEM Forms伺服器。 重新啟動後，AEM Forms伺服器可接受內容並與AEM案頭應用程式共用。
1. 開啟應用程式並連線至AEM Forms伺服器。

   成功連線時，應用程式會填入 `content/dam` 和 `content/dam/formsanddocuments` 資料夾。 除了將檔案從上述資料夾移至本機資料夾（反之亦然）之外，您還可以使用應用程式在自動填入的資料夾之間移動內容。
