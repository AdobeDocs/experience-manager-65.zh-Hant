---
title: 選取您的UI
seo-title: 選取您的UI
description: 為方便編寫使用者，觸控式UI允許視需要切換至傳統UI。
seo-description: 為方便編寫使用者，觸控式UI允許視需要切換至傳統UI。
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# 選取您的UI{#selecting-your-ui}

由於觸控式UI取代傳統UI，因此AEM例項的使用者或管理員必須主動決定繼續使用傳統UI。 由於傳統UI已不再維護，因此製作使用者無法只從傳統UI切換至觸控式UI中的對等UI。

為方便編寫使用者，觸控式UI允許視需要切換至傳統UI。 如需詳細資訊，請參閱標準製作檔案中的[選取UI](/help/sites-authoring/select-ui.md) 。

>[!NOTE]
>
>從舊版升級的執行個體將保留傳統UI以進行頁面編寫。
>
>升級後，頁面製作不會自動切換至觸控式UI，但您可以使用&#x200B;**WCM製作UI模式服務**（`AuthoringUIMode`服務）的[OSGi設定](/help/sites-deploying/configuring-osgi.md)來設定此設定。 請參閱Editor](#uioverridesfortheeditor)的[ UI覆蓋。

## 配置實例{#configuring-the-default-ui-for-your-instance}的預設UI

系統管理員可以使用[根映射](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)配置在啟動和登錄時顯示的UI。

使用者預設值或工作階段設定可覆寫此值。
