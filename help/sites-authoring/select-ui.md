---
title: 在AEM中選取您的使用者介面
description: 設定您要在Adobe Experience Manager 6.5中使用哪個介面。
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 1%

---

# 選取您的UI{#selecting-your-ui}

Adobe Experience Manager (AEM)觸控式UI現在是標準UI，管理和編輯網站幾乎已達功能對等性。 不過，使用者有時可能想要切換至[傳統UI](/help/sites-classic-ui-authoring/classicui.md)。 有幾個選項可以執行此操作。

>[!NOTE]
>
>如需與傳統UI功能對等狀態的詳細資訊，請參閱[Touch UI功能對等](/help/release-notes/touch-ui-features-status.md)檔案。

有許多位置可供您定義要使用的UI：

* [設定執行個體的預設UI](#configuring-the-default-ui-for-your-instance)
這會設定在使用者登入時顯示的預設UI。 使用者可以覆寫此專案，並為其帳戶或目前的工作階段選取不同的UI。

* [正在設定您帳戶的傳統UI編寫](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
這會將UI設定為編輯頁面時的預設值，但使用者可以覆寫此設定，並為其帳戶或目前工作階段選取不同的UI。

* [切換到目前工作階段的傳統UI](#switching-to-classic-ui-for-the-current-session)
切換到目前工作階段的傳統UI。

* 在[頁面編寫的情況下，系統會對UI](#ui-overrides-for-the-editor)的相關性進行某些覆寫。

>[!CAUTION]
>
>用於切換至傳統UI的各種選項無法立即使用，必須針對您的執行個體進行設定。
>
>如需詳細資訊，請參閱[啟用對傳統UI的存取](/help/sites-administering/enable-classic-ui.md)。

>[!NOTE]
>
>從舊版升級的執行個體會保留傳統UI以供編寫頁面。
>
>升級後，頁面編寫不會自動切換至觸控式UI，但您可以使用&#x200B;**WCM編寫UI模式服務** （ `AuthoringUIMode`服務）的[OSGi設定](/help/sites-deploying/configuring-osgi.md)來設定此設定。 檢視編輯器[&#128279;](#ui-overrides-for-the-editor)的UI覆寫。

## 為您的執行個體設定預設UI {#configuring-the-default-ui-for-your-instance}

系統管理員可以使用[根對應](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)來設定啟動時看到並登入的UI。

此可由使用者預設值或工作階段設定覆寫。

## 為您的帳戶設定傳統UI編寫 {#setting-classic-ui-authoring-for-your-account}

每個使用者都可以存取自己的[使用者偏好設定](/help/sites-authoring/user-properties.md#userpreferences)，以定義他們是否要使用傳統UI來編寫頁面，而不是使用預設的UI。

工作階段設定可覆寫此選項。

## 切換到目前工作階段的傳統UI {#switching-to-classic-ui-for-the-current-session}

使用觸控式UI時，桌上型電腦使用者可能想要回覆為傳統（僅限桌上型電腦） UI。 有幾種方法可切換至目前工作階段的傳統UI：

* **導覽連結**

  >[!CAUTION]
  >
  >這個用於切換至傳統UI的選項無法立即使用，必須針對您的執行個體進行設定。
  >
  >
  >如需詳細資訊，請參閱[啟用對傳統UI的存取](/help/sites-administering/enable-classic-ui.md)。

  如果啟用此功能，每當您將滑鼠移至適用的主控台時，畫面都會顯示圖示（監視器符號）。 點選/按一下此可在傳統UI中開啟適當位置。

  例如，從&#x200B;**網站**&#x200B;到&#x200B;**網站管理員**&#x200B;的連結：

  ![syui-01](assets/syui-01.png)

* **URL**

  傳統UI可使用歡迎熒幕的URL進行存取，網址為`welcome.html`。 例如：

  `https://localhost:4502/welcome.html`

  >[!NOTE]
  >
  >可透過`sites.html`存取觸控式UI。 例如：
  >
  >
  >`https://localhost:4502/sites.html`

### 編輯頁面時切換到傳統UI {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>這個用於切換至傳統UI的選項無法立即使用，必須針對您的執行個體進行設定。
>
>如需詳細資訊，請參閱[啟用對傳統UI的存取](/help/sites-administering/enable-classic-ui.md)。

如果啟用，**從**&#x200B;頁面資訊&#x200B;**對話方塊開啟Classic UI**：

![syui-02](assets/syui-02.png)

### 編輯器的UI覆寫 {#ui-overrides-for-the-editor}

如果存在頁面編寫功能，則系統可覆寫使用者或系統管理員定義的設定。

* 編寫頁面時：

   * 在URL中使用`cf#`存取頁面時，會強制使用傳統編輯器。 例如：

     `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * 在URL中使用`/editor.html`或使用觸控裝置時，會強制使用觸控式編輯器。 例如：

     `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* 任何強制都是暫時性的，只對瀏覽器工作階段有效

   * Cookie集的設定取決於是否使用觸控式( `editor.html`)或傳統式( `cf#`)。

* 透過`siteadmin`開啟頁面時，會檢查下列專案是否存在：

   * Cookie
   * 使用者偏好設定
   * 如果兩者都不存在，則預設為&#x200B;**WCM編寫UI模式服務** （ `AuthoringUIMode`服務）的[OSGi設定](/help/sites-deploying/configuring-osgi.md)中設定的定義。

>[!NOTE]
>
>如果[使用者已定義頁面編寫的偏好設定](#settingthedefaultauthoringuiforyouraccount)，則不會變更OSGi屬性來覆寫該偏好設定。

>[!CAUTION]
>
>由於使用Cookie （如前所述），不建議執行以下任一操作：
>
>* 手動編輯URL — 非標準URL可能導致未知情況並缺乏功能。
>* 讓兩個編輯器同時開啟 — 例如，在不同視窗中。
