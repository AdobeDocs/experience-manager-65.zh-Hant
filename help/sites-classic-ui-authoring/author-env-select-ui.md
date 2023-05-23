---
title: 選擇UI
description: 為方便創作用戶，啟用觸摸的UI允許在需要時切換到標準UI。
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# 選擇UI{#selecting-your-ui}

由於啟用觸摸的UI取代經典UI，因此實例的用戶或管理AEM員必須做出一個活動決定，以繼續使用經典UI。 由於不再維護標準UI，因此創作用戶無法簡單地從標準UI切換到啟用觸摸的UI中的對等UI。

為方便創作用戶，啟用觸摸的UI允許在需要時切換到標準UI。 查看 [選擇UI](/help/sites-authoring/select-ui.md) 的子菜單。

>[!NOTE]
>
>從先前版本升級的實例將保留用於頁面創作的標準用戶介面。
>
>升級後，頁面創作不會自動切換到啟用觸摸功能的UI，但您可以使用[OSGi配置](/help/sites-deploying/configuring-osgi.md) 的 **WCM創作UI模式服務** ( `AuthoringUIMode` 服務)。 請參閱 [編輯器的UI覆蓋](#uioverridesfortheeditor)。

## 配置實例的預設UI {#configuring-the-default-ui-for-your-instance}

系統管理員可以使用 [根映射](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)。

用戶預設設定或會話設定可以覆蓋此設定。
