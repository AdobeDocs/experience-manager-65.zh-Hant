---
title: Identity Management
seo-title: Identity Management
description: 瞭解中的身份管AEM理。
seo-description: Learn about identity management in AEM.
uuid: d9b83cd7-c47a-41a5-baa4-bbf385d13bfd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 994a5751-7267-4a61-9bc7-01440a256c65
docset: aem65
exl-id: acb5b235-523e-4c01-9bd2-0cc2049f88e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 2%

---

# Identity Management{#identity-management}

只有在您提供登錄功能時，才能識別您網站的個人訪問者。 您可能希望提供登錄功能的原因有多種：

* [AEM Communities](/help/communities/overview.md)站點訪問者必須登錄才能將內容發佈到社區。
* [關閉的用戶組](/help/sites-administering/cug.md)

   您可能需要將訪問您的網站（或其部分）的權限限制為特定訪問者。

* [個性化](/help/sites-administering/personalization.md) 允許訪問者配置訪問您網站的某些方面。

登錄（和註銷）功能由 [帳戶 **配置檔案**](#profiles-and-user-accounts)，其中包含有關註冊訪問者（用戶）的其他資訊。 登記和授權的實際過程可能不同：

* 從網站自行註冊

   A [社區網站](/help/communities/sites-console.md) 可以配置為允許訪問者在其Facebook或Twitter帳戶上自行註冊或登錄。

* 從網站申請註冊

   對於關閉的用戶組，您可能允許訪問者請求註冊，但通過工作流強制授權。

* 從作者環境註冊每個帳戶

   如果您有少量配置檔案，但仍需要授權，您可能決定直接註冊每個配置檔案。

為了允許訪問者註冊，可以使用一系列元件和表單來收集所需的標識資訊，然後收集附加（通常是可選的）配置檔案資訊。 註冊後，還要能夠查看和更新自己提交的細節。

可以配置或開發其他功能：

* 配置所需的任何反向複製。
* 允許用戶通過與工作流一起開發表單來刪除其配置檔案。

>[!NOTE]
>
>在簡檔中指定的資訊也可用於通過 [段](/help/sites-administering/campaign-segmentation.md) 和 [市場活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)。

## 註冊Forms {#registration-forms}

A [表格](/help/sites-authoring/default-components.md#form-component) 可以用來收集註冊資訊，然後生成新帳戶和配置檔案。

例如，用戶可以使用「Geometrixx」頁請求新的配置檔案
`http://localhost:4502/content/geometrixx-outdoors/en/user/register.html`

![註冊表](assets/registerform.png)

在提交請求後，將開啟配置檔案頁，用戶可在其中提供個人詳細資訊。

![配置檔案頁](assets/profilepage.png)

新帳戶在 [用戶控制台](/help/sites-administering/security.md)。

## 登入 {#login}

登錄元件可用於收集登錄資訊，然後激活登錄過程。

這為訪問者提供了 **用戶名** 和 **密碼**, **登錄** 按鈕，在輸入憑據時激活登錄進程。

例如，用戶可以使用 **登錄** 的子菜單。

`http://localhost:4502/content/geometrixx-outdoors/en/user/sign-in.html`

![登錄](assets/login.png)

## 註銷 {#logging-out}

由於存在登錄機制，因此也需要註銷機制。 此選項可用於 **註銷** 的子菜單。

## 查看和更新配置檔案 {#viewing-and-updating-a-profile}

根據您的註冊表，訪問者的個人資料中可能包含註冊資訊。 他們應能在以後階段查看和/或更新此項。 可以用類似的形式來完成；例如，在Geometrixx中：

```
http://localhost:4502/content/geometrixx-outdoors/en/user/profile.html
```

要查看配置檔案的詳細資訊，請按一下 **我的個人資料** 在任何頁面的右上角；例如， `admin` 帳戶：
`http://localhost:4502/home/users/a/admin/profile.form.html/content/geometrixx-outdoors/en/user/profile.html.`

您可以使用 [客戶端上下文](/help/sites-administering/client-context.md) （在作者環境上，並具有足夠的權限）:

1. 開啟頁面；例如，「Geometrixx」頁：

   `http://localhost:4502/cf#/content/geometrixx/en.html`

1. 按一下 **我的個人資料** 在右上角。 你將看到你的經常賬戶的檔案；例如管理員。
1. 按 **控制 — Alt-C** 開啟客戶端上下文。
1. 在客戶端上下文的左上角，按一下 **載入配置檔案** 按鈕

   ![](do-not-localize/loadprofile.png)

1. 從對話框窗口的下拉清單中選擇另一個配置檔案；比如說， **艾莉森·帕克**。
1. 按一下&#x200B;**「確定」**。
1. 再次按一下 **我的個人資料**。 表格將更新艾莉森的詳細資訊。

   ![輪廓](assets/profilealison.png)

1. 你現在可以 **編輯配置檔案** 或 **更改密碼** 以更新詳細資訊。

## 將欄位添加到配置檔案定義 {#adding-fields-to-the-profile-definition}

可將欄位添加到配置檔案定義。 例如，向Geometrixx配置檔案添加「收藏夾顏色」欄位：

1. 從「網站」控制台導航至「Geometrixx Outdoors網站」>「英語」>「用戶」>「我的配置檔案」。
1. 按兩下 **我的個人資料** 的子菜單。
1. 在 **元件** 旁鍵頁籤展開 **窗體** 的子菜單。
1. 拖動 **下拉清單** 從旁邊到表格，就在 **關於我** 的子菜單。
1. 按兩下 **下拉清單** 元件，開啟配置對話框並輸入：

   * **元素名稱** - `favoriteColor`
   * **標題** - `Favorite Color`
   * **項目**  — 添加多種顏色作為項

   按一下 **確定** 來保存。

1. 關閉頁面並返回到 **網站** 控制台並激活「我的概要檔案」頁。

   下次查看配置檔案時，您可以選擇收藏夾顏色：

   ![紫色](assets/aparkerfavcolour.png)

   欄位將保存在 **輪廓** 相關用戶帳戶部分：

   ![阿帕克克斯代爾特](assets/aparkercrxdelite.png)

## 配置檔案狀態 {#profile-states}

有許多使用案例需要知道用戶（或者他們的配置檔案）是否在 *特定狀態* 或者不是。

這涉及通過以下方式在用戶配置檔案中定義適當的屬性：

* 可見且用戶可訪問
* 為每個屬性定義兩個狀態
* 允許在定義的兩個狀態之間切換

這是通過：

* [狀態提供程式](#state-providers)

   管理特定屬性的兩種狀態以及兩種屬性之間的轉換。

* [工作流程](#workflows)

   管理與狀態相關的操作。

可以定義多個狀態；例如，在Geometrixx中，這些包括：

* 訂閱（或取消訂閱）新聞通訊或評論線程上的通知
* 添加和刪除與朋友的連接

### 狀態提供程式 {#state-providers}

狀態提供程式管理有關屬性的當前狀態以及兩個可能狀態之間的轉換。

狀態提供程式是作為元件實現的，因此可以為項目自定義。 在Geometrixx中包括：

* 取消訂閱/訂閱論壇主題
* 添加/刪除朋友

### 工作流程 {#workflows}

狀態提供程式管理配置檔案屬性及其狀態。

需要一個工作流來實施與狀態相關的操作。 例如，在訂閱通知時，工作流將處理實際訂閱操作；取消訂閱通知時，工作流將處理從訂閱清單中刪除用戶。

## 配置檔案和用戶帳戶 {#profiles-and-user-accounts}

配置檔案作為Content Repository的一部分儲存在[用戶帳戶](/help/sites-administering/user-group-ac-admin.md)。

配置檔案可在 `/home/users/geometrixx`:

![chlimage_1-138](assets/chlimage_1-138.png)

在標準安裝（作者或發佈）中，每個人都具有對所有用戶的整個配置檔案資訊的讀取權限。 每個人都是&quot;*內置組自動包含所有現有用戶和組。 無法編輯成員清單*。

這些訪問權限由下列通配符ACL定義：

/home每個人都允許jcr:read rep:glob = &#42;/配置檔案&#42;

這允許：

* 論壇、評論或部落格，以顯示相應配置檔案中的資訊（如表徵圖或全名）
* 連結到geometrix配置檔案頁

如果此訪問不適合您的安裝，您可以更改這些預設設定。

可以使用 **[訪問控制](/help/sites-administering/user-group-ac-admin.md#access-right-management)** 頁籤：

![卡爾曼](assets/aclmanager.png)

## 配置檔案元件 {#profile-components}

此外，還有一系列配置檔案元件可用於定義您的站點的配置檔案要求。

### 已檢查密碼欄位 {#checked-password-field}

此元件為以下項提供兩個欄位：

* 密碼的輸入
* 檢查以確認密碼已正確輸入。

使用預設設定，元件將顯示如下：

![dc_profiles_checkedpassword](assets/dc_profiles_checkedpassword.png)

### 設定檔頭像相片 {#profile-avatar-photo}

此元件為用戶提供了選擇和上載虛擬形象照片檔案的機制。

![dc_profiles_avatarphoto](assets/dc_profiles_avatarphoto.png)

### 設定檔詳細名稱 {#profile-detailed-name}

此元件允許用戶輸入詳細名稱。

![dc_profiles_detailedname](assets/dc_profiles_detailedname.png)

### 設定檔性別 {#profile-gender}

該部分允許用戶輸入其性別。

![dc_profiles_gedern](assets/dc_profiles_gender.png)
