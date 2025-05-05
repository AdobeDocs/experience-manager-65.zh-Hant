---
title: 選取您的UI
description: 為了方便編寫使用者，觸控式UI可讓您在必要時切換至傳統UI。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# 選取您的UI{#selecting-your-ui}

由於觸控式UI會取代傳統UI，AEM例項的使用者或管理員必須做出有效決定，才能繼續使用傳統UI。 由於傳統UI已不再進行維護，因此製作使用者無法僅從傳統UI切換為觸控式UI中的同等專案。

為了方便編寫使用者，觸控式UI可讓您在必要時切換至傳統UI。 如需詳細資訊，請參閱標準編寫檔案中的[選取您的UI](/help/sites-authoring/select-ui.md)。

>[!NOTE]
>
>從舊版升級的執行個體將保留傳統UI以進行頁面編寫。
>
>升級之後，頁面編寫將不會自動切換至觸控式UI，但您可以使用&#x200B;**WCM編寫UI模式服務** （ `AuthoringUIMode`服務）的[OSGi設定](/help/sites-deploying/configuring-osgi.md)來設定此設定。 檢視編輯器[&#128279;](#uioverridesfortheeditor)的UI覆寫。

## 為您的執行個體設定預設UI {#configuring-the-default-ui-for-your-instance}

系統管理員可以使用[根對應](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)來設定啟動時看到並登入的UI。

此可由使用者預設值或工作階段設定覆寫。
