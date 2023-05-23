---
title: 在中選擇您的用戶介面AEM
description: 配置要使用的介面AEM。
uuid: ab127f2f-2f8a-4398-90dd-c5d48eed9e53
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: e418d330-f234-411d-8cad-3fd9906dcbee
docset: aem65
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 1%

---

# 選擇UI{#selecting-your-ui}

儘管啟用觸摸的UI現在是標準UI，而且在站點的管理和編輯過程中幾乎達到了功能奇偶校驗，但用戶有時可能希望切換到 [經典UI](/help/sites-classic-ui-authoring/classicui.md)。 這樣做有幾種選擇。

>[!NOTE]
>
>有關與標準UI的功能奇偶校驗狀態的詳細資訊，請參見 [觸摸UI功能奇偶校驗](/help/release-notes/touch-ui-features-status.md) 的子菜單。

您可以定義要使用哪些UI的不同位置：

* [配置實例的預設UI](#configuring-the-default-ui-for-your-instance)
這將設定在用戶登錄時顯示的預設UI，儘管用戶可能可以覆蓋此UI並為其帳戶或當前會話選擇其他UI。

* [設定帳戶的經典UI創作](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
這將將UI設定為編輯頁面時的預設用戶介面，儘管用戶可以覆蓋該介面並為其帳戶或當前會話選擇不同的用戶介面。

* [切換到當前會話的經典UI](#switching-to-classic-ui-for-the-current-session)
這將切換到當前會話的經典UI。

* 對於 [頁面創作系統在與UI的關係中進行某些替代](#ui-overrides-for-the-editor)。

>[!CAUTION]
>
>切換到標準UI的各種選項不能立即開箱即用，必須為您的實例專門配置。
>
>請參閱 [啟用對經典UI的訪問](/help/sites-administering/enable-classic-ui.md) 的子菜單。

>[!NOTE]
>
>從先前版本升級的實例將保留用於頁面創作的標準用戶介面。
>
>升級後，頁面創作不會自動切換到啟用觸摸功能的UI，但您可以使用 [OSGi配置](/help/sites-deploying/configuring-osgi.md) 的 **WCM創作UI模式服務** ( `AuthoringUIMode` 服務)。 請參閱 [編輯器的UI覆蓋](#ui-overrides-for-the-editor)。

## 配置實例的預設UI {#configuring-the-default-ui-for-your-instance}

系統管理員可以使用 [根映射](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)。

用戶預設設定或會話設定可以覆蓋此設定。

## 設定帳戶的經典UI創作 {#setting-classic-ui-authoring-for-your-account}

每個用戶都可以訪問 [用戶首選項](/help/sites-authoring/user-properties.md#userpreferences) 定義他/她是否希望將傳統UI用於頁面創作（而不是預設UI）。

會話設定可以覆蓋此項。

## 切換到當前會話的經典UI {#switching-to-classic-ui-for-the-current-session}

使用啟用觸摸的UI案頭時，用戶可能希望恢復到經典（僅限案頭）UI。 有幾種方法可切換到當前會話的經典UI:

* **導航連結**

   >[!CAUTION]
   >
   >切換到標準UI的此選項不是現成的，必須為您的實例專門配置。
   >
   >
   >請參閱 [啟用對經典UI的訪問](/help/sites-administering/enable-classic-ui.md) 的子菜單。

   如果啟用此功能，則每當您在適用的控制台上安裝時，都會出現一個表徵圖（顯示器的符號），輕擊/按一下此功能將開啟標準用戶介面中的相應位置。

   例如， **站點** 至 **站點管理**:

   ![syui-01](assets/syui-01.png)

* **URL**

   可使用歡迎螢幕的URL訪問標準UI，網址為： `welcome.html`。 例如：

   `https://localhost:4502/welcome.html`

   >[!NOTE]
   >
   >可通過以下方式訪問啟用觸摸的UI: `sites.html`。 例如：
   >
   >
   >`https://localhost:4502/sites.html`

### 編輯頁面時切換到經典UI {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>切換到標準UI的此選項不是現成的，必須為您的實例專門配置。
>
>請參閱 [啟用對經典UI的訪問](/help/sites-administering/enable-classic-ui.md) 的子菜單。

如果啟用， **開啟經典UI** 的 **頁面資訊** 對話框：

![syui-02](assets/syui-02.png)

### 編輯器的UI覆蓋 {#ui-overrides-for-the-editor}

用戶或系統管理員定義的設定可以在頁面創作時由系統覆蓋。

* 創作頁面時：

   * 使用 `cf#` 的子菜單。 例如：
      `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * 使用時強制使用啟用觸摸的編輯器 `/editor.html` 的子菜單。 例如：
      `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* 任何強制都是臨時的，且僅對瀏覽器會話有效

   * 將根據是否啟用觸摸( `editor.html`)或經典( `cf#`)。

* 開啟頁面時 `siteadmin`，將檢查是否存在：

   * 餅乾
   * 用戶首選項
   * 如果兩者均不存在，則預設為 [OSGi配置](/help/sites-deploying/configuring-osgi.md) 的 **WCM創作UI模式服務** ( `AuthoringUIMode` 服務)。

>[!NOTE]
>
>如果 [用戶已定義了頁面創作首選項](#settingthedefaultauthoringuiforyouraccount)，不會通過更改OSGi屬性來覆蓋。

>[!CAUTION]
>
>由於使用了Cookie（如前所述），因此建議不要執行以下任一操作：
>
>* 手動編輯URL — 非標準URL可能導致未知情況和缺少功能。
>* 同時開啟兩個編輯器 — 例如，在單獨的窗口中。

