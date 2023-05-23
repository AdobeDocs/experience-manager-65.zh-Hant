---
title: AEMAEM Forms案頭應用
seo-title: AEM desktop app for AEM Forms
description: AEMAEM Forms案頭應用
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

# AEMAEM Forms案頭應用 {#aem-desktop-app-for-aem-forms}

案頭應AEM用允許您將Adobe Experience Manager(AEM)資產儲存庫和AEM Forms二進位檔案映射到系統上的網路目錄。 您可以在檔案資源管理器中查看同步的資產和二進位檔案，並根據需要使用各種應用來編輯檔案。 除了查看檔案外，還可以建立、上載和刪除二進位檔案。 您也可以直接從軟體中開啟、編輯和保存檔案。 例如，可以直接從Designer中開啟和編輯XDP檔案。 您對本地資產所做的更改將反映在AEM Assets儲存庫和AEM FormsUI中。

你可以從實例下載應AEM用。 有關下載應用的詳細資訊，請參閱 [案頭應AEM用發行說明](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html)。

## AEM Forms在案頭應用AEM中支援的資產 {#aem-forms-assets-supported-in-aem-desktop-app}

您可以使用此應用同步以下類型的AEM Forms二進位檔案：表單模板(.xdp)、PDF表單(.pdf)、文檔(.pdf)、影像、XML架構(.xsd)、樣式表(.xfs)。 應用程式將所有其他檔案（不支援的檔案）列為0位元組檔案。 將不支援的檔案列為0位元組檔案可確保用戶知道AEM Forms伺服器上存在其他可用資產。

>[!NOTE]
>
>檔案名只能包含字母數字字元、連字元或下划線。

## 為案頭應用啟AEM用AEM Forms {#enable-aem-forms-for-aem-desktop-app}

案頭應AEM用在MicrosoftWindows和MacOS X上的SMB1上使用WebDAV協定連接到AEM Forms伺服器。 開箱即用後，AEM Forms伺服器無法將二進位檔案和其他資產與WebDAV或SMB客戶端同步。 執行以下步驟以啟用AEM FormsAEM案頭應用：

1. 以管理員身份登錄到AEM Forms。
1. 在作者實例中，按一下 ![adobeexperience manager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager>工具]** ![錘](assets/hammer.png) **[!UICONTROL >部署>操作> Web控制台]**。 Web控制台將在新窗口中開啟。
1. 在Web控制台窗口中，找到並開啟 **[!UICONTROL FormsManager AddOn配置]** 的雙曲餘切值。
1. 在「FormsManager AddOn配置」對話框中，取消選擇 **[!UICONTROL 非同步同步資源]** 複選框，然後按一下 **[!UICONTROL 保存]**。
1. 重新啟動AEM Forms伺服器。 重新啟動後，AEM Forms伺服器可以接受和與案頭應用共AEM享內容。
1. 開啟應用並連接到AEM Forms伺服器。

   成功連接時，應用將填充 `content/dam` 和 `content/dam/formsanddocuments` 資料夾。 除了將檔案從上面的資料夾移動到本地資料夾，反之亦然，您還可以使用應用程式在自動填充的資料夾之間移動內容。
