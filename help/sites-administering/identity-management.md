---
title: Identity Management
seo-title: Identity Management
description: 了解AEM中的身分管理。
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
ht-degree: 1%

---

# Identity Management{#identity-management}

只有在您提供登入功能時，才能識別您網站的個別訪客。 您可能想提供登入功能的原因有多種：

* [AEM Communities](/help/communities/overview.md)網站訪客必須登入才能將內容張貼至社群。
* [已關閉的用戶組](/help/sites-administering/cug.md)

   您可能需要限制特定訪客對您網站（或其區段）的存取。

* [個人化](/help/sites-administering/personalization.md) 可讓訪客設定存取您網站的特定方面。

登入（和退出）功能由 [帳戶 **設定檔**](#profiles-and-user-accounts)，其中包含註冊訪客（使用者）的其他資訊。 註冊和授權的實際過程可能不同：

* 從網站自行註冊

   A [社群網站](/help/communities/sites-console.md) 可設定為允許訪客以其Facebook或Twitter帳戶自行註冊或登入。

* 從網站申請註冊

   對於封閉的使用者群組，您可以允許訪客要求註冊，但透過工作流程強制授權。

* 從製作環境註冊每個帳戶

   如果您有少量設定檔，無論如何都需要授權，您可以決定直接註冊每個設定檔。

為了讓訪客註冊，您可以使用一系列元件和表單來收集所需的識別資訊，然後收集其他（通常為選用）的設定檔資訊。 註冊後，還應能檢查並更新已提交的詳細資訊。

可以配置或開發其他功能：

* 配置所需的任何反向複製。
* 透過與工作流程一起開發表單，允許使用者移除其設定檔。

>[!NOTE]
>
>設定檔中指定的資訊也可用來透過 [區段](/help/sites-administering/campaign-segmentation.md) 和 [行銷活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

## 註冊Forms {#registration-forms}

A [表單](/help/sites-authoring/default-components.md#form-component) 可用來收集註冊資訊，然後產生新帳戶和設定檔。

例如，使用者可以使用「Geometrixx」頁面來請求新的設定檔
`http://localhost:4502/content/geometrixx-outdoors/en/user/register.html`

![註冊表](assets/registerform.png)

提交請求時，設定檔頁面會開啟，使用者可在其中提供個人詳細資訊。

![profilepage](assets/profilepage.png)

新帳戶也會顯示在 [使用者主控台](/help/sites-administering/security.md).

## 登入 {#login}

登入元件可用來收集登入資訊，然後啟動登入程式。

這可為訪客提供 **使用者名稱** 和 **密碼**，具有 **登入** 按鈕，以在輸入憑據時啟動登入程式。

例如，使用者可以登入，或使用 **登入** 選項，此工具欄使用頁面：

`http://localhost:4502/content/geometrixx-outdoors/en/user/sign-in.html`

![登入](assets/login.png)

## 登出 {#logging-out}

由於存在登錄機制，因此也需要註銷機制。 這可作為 **登出** 選項。

## 檢視和更新設定檔 {#viewing-and-updating-a-profile}

視您的註冊表而定，訪客的設定檔中可能有註冊資訊。 他們應該能在稍後階段檢視和/或更新此項目。 這可以用類似的形式完成；例如，在Geometrixx中：

```
http://localhost:4502/content/geometrixx-outdoors/en/user/profile.html
```

若要查看設定檔的詳細資訊，請按一下 **我的設定檔** 位於任何頁面的右上角；例如，搭配 `admin` 帳戶：
`http://localhost:4502/home/users/a/admin/profile.form.html/content/geometrixx-outdoors/en/user/profile.html.`

您可以使用 [用戶上下文](/help/sites-administering/client-context.md) （在製作環境上，且具有足夠的權限）:

1. 開啟頁面；例如「Geometrixx」頁面：

   `http://localhost:4502/cf#/content/geometrixx/en.html`

1. 按一下 **我的設定檔** 在右上角。 您會看到您經常帳戶的設定檔；例如管理員。
1. Press **control-alt-C** 以開啟用戶端內容。
1. 在用戶端內容的左上角，按一下 **載入設定檔** 按鈕。

   ![](do-not-localize/loadprofile.png)

1. 從對話框窗口的下拉清單中選擇另一個配置檔案；例如， **艾莉森·帕克**.
1. 按一下&#x200B;**「確定」**。
1. 再按一下 **我的設定檔**. 表單將更新Alison的詳細資訊。

   ![profilealison](assets/profilealison.png)

1. 您現在可以使用 **編輯個人資料** 或 **更改密碼** 以更新詳細資訊。

## 新增欄位至設定檔定義 {#adding-fields-to-the-profile-definition}

您可以新增欄位至設定檔定義。 例如，若要將「最喜愛的顏色」欄位新增至Geometrixx設定檔：

1. 從網站控制台導覽至Geometrixx Outdoors網站>英文>使用者>我的設定檔。
1. 按兩下 **我的設定檔** 頁面以開啟它進行編輯。
1. 在 **元件** sidekick的標籤展開 **表單** 區段。
1. 拖曳 **下拉式清單** 從sidekick到表格，就在 **關於我** 欄位。
1. 按兩下 **下拉式清單** 要開啟配置對話框的元件，請輸入：

   * **元素名稱** - `favoriteColor`
   * **標題** - `Favorite Color`
   * **項目**  — 添加數種顏色作為項

   按一下 **確定** 儲存。

1. 關閉頁面並返回 **網站** 控制台並啟動「我的個人資料」頁面。

   下次檢視設定檔時，您可以選取最喜愛的顏色：

   ![阿帕夫科爾](assets/aparkerfavcolour.png)

   欄位將儲存在 **設定檔** 相關用戶帳戶的部分：

   ![阿爾克克斯德利特](assets/aparkercrxdelite.png)

## 設定檔狀態 {#profile-states}

有許多使用案例需要知道使用者（或其設定檔）是否位於 *特定狀態* 或否。

這包括在使用者設定檔中定義適當的屬性，其方式為：

* 可供使用者檢視和存取
* 為每個屬性定義兩個狀態
* 允許在定義的兩種狀態之間切換

這是透過：

* [狀態提供程式](#state-providers)

   管理特定屬性的兩種狀態，以及兩者之間的轉變。

* [工作流程](#workflows)

   管理與狀態相關的動作。

可定義多個狀態；例如，在Geometrixx中，這些包括：

* 訂閱（或取消訂閱）電子報或評論執行緒上的通知
* 添加和刪除與好友的連接

### 狀態提供程式 {#state-providers}

狀態提供者會管理相關屬性的目前狀態，以及兩個可能狀態之間的轉變。

狀態提供者會實作為元件，因此可針對您的專案自訂。 在Geometrixx中，這些包括：

* 取消訂閱/訂閱論壇主題
* 添加/刪除好友

### 工作流程 {#workflows}

狀態提供者會管理設定檔屬性及其狀態。

需要工作流程來實施與狀態相關的動作。 例如，訂閱通知時，工作流程將處理實際的訂閱動作；從通知取消訂閱時，工作流程將處理從訂閱清單中移除使用者的作業。

## 設定檔和使用者帳戶 {#profiles-and-user-accounts}

設定檔會儲存在內容存放庫中，作為[使用者帳戶](/help/sites-administering/user-group-ac-admin.md).

可在下方找到設定檔 `/home/users/geometrixx`:

![chlimage_1-138](assets/chlimage_1-138.png)

在標準安裝（製作或發佈）上，每個人都可讀取所有使用者的整個設定檔資訊。 每個人都是「*內建群組會自動包含所有現有的使用者和群組。 無法編輯成員清單*」。

這些訪問權限由以下通配符ACL定義：

/home每個人都允許jcr:read rep:glob = &#42;/profile&#42;

這可以：

* 論壇、留言或部落格貼文，以顯示適當設定檔中的資訊（例如圖示或全名）
* geometrixx設定檔頁面的連結

如果此類訪問權限不適合您的安裝，您可以更改這些預設設定。

您可以使用 **[存取控制](/help/sites-administering/user-group-ac-admin.md#access-right-management)** 標籤：

![aclmanager](assets/aclmanager.png)

## 設定檔元件 {#profile-components}

定義您網站的設定檔需求時，也可使用一系列設定檔元件。

### 已檢查密碼欄位 {#checked-password-field}

此元件提供下列兩個欄位：

* 密碼的輸入
* 檢查以確認密碼已正確輸入。

使用預設設定時，元件將顯示如下：

![dc_profiles_checkedpassword](assets/dc_profiles_checkedpassword.png)

### 設定檔頭像相片 {#profile-avatar-photo}

此元件提供使用者選取和上傳頭像像片檔案的機制。

![dc_profiles_avatarphoto](assets/dc_profiles_avatarphoto.png)

### 設定檔詳細名稱 {#profile-detailed-name}

此元件可讓使用者輸入詳細名稱。

![dc_profiles_detailedname](assets/dc_profiles_detailedname.png)

### 設定檔性別 {#profile-gender}

此元件可讓使用者輸入其性別。

![dc_profiles_gender](assets/dc_profiles_gender.png)
