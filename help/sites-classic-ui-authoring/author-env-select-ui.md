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

---


# 選擇您的UI{#selecting-your-ui}

由於觸控式UI會取代傳統UI，因此AEM例項的使用者或管理員必須主動決定繼續使用傳統UI。 由於傳統UI已不再維護，因此編寫使用者無法直接從傳統UI切換至觸控式UI中的相同UI。

為方便編寫使用者，觸控式UI允許視需要切換至傳統UI。 如需詳細 [資訊，請參閱標準編寫檔案中的](/help/sites-authoring/select-ui.md) 「選取您的UI」。

>[!NOTE]
>
>從舊版升級的例項將保留用於頁面製作的傳統UI。
>
>升級後，頁面製作不會自動切換至觸控式UI，但您可以使用[WCM Authoring UI Mode Service](/help/sites-deploying/configuring-osgi.md) （服務）的OSGi組態來設 ****`AuthoringUIMode` 定此設定。 請參 [閱編輯器的UI覆蓋](#uioverridesfortheeditor)。

## 為實例配置預設UI {#configuring-the-default-ui-for-your-instance}

系統管理員可以使用根映射來配置在啟動和登錄時顯示的 [UI](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)。

用戶預設值或會話設定可以覆蓋此選項。
