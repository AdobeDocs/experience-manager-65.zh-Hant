---
title: 選擇您的UI
seo-title: 選擇您的UI
description: 為方便編寫使用者，觸控式UI允許視需要切換至傳統UI。
seo-description: 為方便編寫使用者，觸控式UI允許視需要切換至傳統UI。
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---


# 選擇您的UI{#selecting-your-ui}

由於觸控式UI會取代傳統UI，因此AEM例項的使用者或管理員必須主動決定繼續使用傳統UI。 由於傳統UI已不再維護，因此編寫使用者無法直接從傳統UI切換至觸控式UI中的相同UI。

為方便編寫使用者，觸控式UI允許視需要切換至傳統UI。 如需詳細資訊，請參閱標準編寫檔案中的[選擇您的UI](/help/sites-authoring/select-ui.md)。

>[!NOTE]
>
>從舊版升級的例項將保留用於頁面製作的傳統UI。
>
>升級後，頁面編寫不會自動切換至觸控式UI，但您可使用&#x200B;**WCM編寫UI模式服務**（`AuthoringUIMode`服務）的[OSGi configuration](/help/sites-deploying/configuring-osgi.md)來設定此設定。 請參閱[編輯器的UI覆蓋。](#uioverridesfortheeditor)

## 為實例{#configuring-the-default-ui-for-your-instance}配置預設UI

系統管理員可以使用[根映射](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)配置在啟動和登錄時顯示的UI。

用戶預設值或會話設定可以覆蓋此選項。
