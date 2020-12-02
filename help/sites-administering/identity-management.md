---
title: 身分識別管理
seo-title: 身分識別管理
description: 瞭解AEM中的身分識別管理。
seo-description: 瞭解AEM中的身分識別管理。
uuid: d9b83cd7-c47a-41a5-baa4-bbf385d13bfd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 994a5751-7267-4a61-9bc7-01440a256c65
docset: aem65
translation-type: tm+mt
source-git-commit: a268b7046430cc17c8b59b9306cf3533d73bb4a2
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 1%

---


# 身份管理{#identity-management}

只有當您提供登入功能時，才能識別您網站的個別訪客。 您可能想要提供登入功能的原因有很多：

* [AEM ](/help/communities/overview.md)CommunitiesSite訪客必須登入才能將內容張貼至社群。
* [已關閉的使用者群組](/help/sites-administering/cug.md)

   您可能需要限制對特定訪客的網站（或網站的部分）存取。

* [個](/help/sites-administering/personalization.md) 人化允許訪客設定存取您網站的特定方面。

登入（和登出）功能由[帳戶提供，**描述檔**](#profiles-and-user-accounts)&#x200B;包含有關註冊訪客（使用者）的其他資訊。 註冊和授權的實際程式可能不同：

* 從網站自行註冊

   [社群網站](/help/communities/sites-console.md)可設定為允許訪客自行註冊或登入其Facebook或Twitter帳戶。

* 從網站要求註冊

   對於已關閉的使用者群組，您可能允許訪客要求註冊，但是透過工作流程強制授權。

* 從作者環境註冊每個帳戶

   如果您有少量個人檔案，而且仍需要授權，您可以決定直接註冊每個檔案。

為了讓訪客註冊，您可使用一系列元件和表單來收集所需的識別資訊，然後再收集其他（通常為選擇性）描述檔資訊。 在註冊後，也應該能夠查看和更新，提交的細節。

可以配置或開發其他功能：

* 配置任何需要的反向複製。
* 讓使用者透過與工作流程一起開發表單，來移除其個人檔案。

>[!NOTE]
>
>設定檔中指定的資訊也可用來透過[Segments](/help/sites-administering/campaign-segmentation.md)和[Campaigns](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)提供使用者目標內容。

## 註冊表單{#registration-forms}

[form](/help/sites-authoring/default-components.md#form-component)可用來收集註冊資訊，然後生成新帳戶和配置檔案。

例如，使用者可使用Geometrixx頁面來請求新的描述檔
`http://localhost:4502/content/geometrixx-outdoors/en/user/register.html`

![註冊表](assets/registerform.png)

提交請求時，描述檔頁面隨即開啟，使用者可在其中提供個人詳細資訊。

![分析頁面](assets/profilepage.png)

新帳戶也會顯示在[使用者主控台](/help/sites-administering/security.md)中。

## 登入 {#login}

登入元件可用來收集登入資訊，然後啟動登入程式。

這為訪客提供標準欄位&#x200B;**Username**&#x200B;和&#x200B;**Password**，以及&#x200B;**登入**&#x200B;按鈕，以在輸入憑證時啟動登入程式。

例如，使用者可使用Geometrixx工具列上的&#x200B;**登入**&#x200B;選項登入或建立新帳戶，該工具列使用頁面：

`http://localhost:4502/content/geometrixx-outdoors/en/user/sign-in.html`

![登錄](assets/login.png)

## 登出{#logging-out}

由於存在登錄機制，因此也需要註銷機制。 此選項可作為Geometrixx中的&#x200B;**登出**&#x200B;選項使用。

## 查看和更新配置檔案{#viewing-and-updating-a-profile}

視您的註冊表而定，訪客的描述檔中可能包含註冊資訊。 他們應該能夠在以後階段查看和／或更新此項。 這可以用類似的形式完成；例如，在Geometrixx中：

```
http://localhost:4502/content/geometrixx-outdoors/en/user/profile.html
```

若要查看您的個人檔案詳細資訊，請按一下任何頁面右上角的&#x200B;**My Profile**;例如`admin`帳戶：
`http://localhost:4502/home/users/a/admin/profile.form.html/content/geometrixx-outdoors/en/user/profile.html.`

您可以使用[客戶端上下文](/help/sites-administering/client-context.md)（在作者環境上，並具有足夠的權限）查看另一個配置檔案：

1. 開啟頁面；例如Geometrixx頁面：

   `http://localhost:4502/cf#/content/geometrixx/en.html`

1. 按一下右上角的&#x200B;**My Profile**。 你會看到你經常帳戶的概況；例如，管理員。
1. 按&#x200B;**control-alt-C**&#x200B;鍵開啟客戶機上下文。
1. 在用戶端內容的左上角，按一下「載入描述檔&#x200B;**」按鈕。**

   ![](do-not-localize/loadprofile.png)

1. 從對話框窗口的下拉清單中選擇另一個配置檔案；例如，**Alison Parker**。
1. 按一下&#x200B;**「確定」**。
1. 再次按一下&#x200B;**My Profile**。 表格將更新Alison的詳細資訊。

   ![profilealison](assets/profilealison.png)

1. 您現在可以使用&#x200B;**編輯描述檔**&#x200B;或&#x200B;**變更密碼**&#x200B;來更新詳細資訊。

## 將欄位添加到配置檔案定義{#adding-fields-to-the-profile-definition}

您可以將欄位添加到配置檔案定義中。 例如，若要將「我的最愛色彩」欄位新增至Geometrixx描述檔：

1. 從「網站」主控台導覽至「Geometrixx Outdoors網站>英文>使用者>我的設定檔」。
1. 按兩下&#x200B;**My Profile**&#x200B;頁面以開啟它進行編輯。
1. 在側腳的「**元件**」標籤中，展開「**表單**」區段。
1. 將&#x200B;**下拉式清單**&#x200B;從側腳拖曳至表單，位於&#x200B;**關於me**&#x200B;欄位下方。
1. 按兩下&#x200B;**下拉清單**&#x200B;元件以開啟配置對話框並輸入：

   * **元素名稱** - `favoriteColor`
   * **標題** - `Favorite Color`
   * **項目** -新增數種顏色作為項目

   按一下&#x200B;**確定**&#x200B;保存。

1. 關閉頁面並返回至&#x200B;**Websites**&#x200B;主控台並啟動「我的個人資料」頁面。

   下次您檢視描述檔時，可以選取最愛的顏色：

   ![aperkafcolor](assets/aparkerfavcolour.png)

   欄位將儲存在相關使用者帳戶的&#x200B;**profile**&#x200B;區段下：

   ![aparkerxdelite](assets/aparkercrxdelite.png)

## 配置檔案狀態{#profile-states}

有許多使用案例需要知道使用者（或其描述檔）是否處於&#x200B;*特定狀態*。

這包括在使用者描述檔中定義適當的屬性，其方式為：

* 可見，用戶可以訪問
* 為每個屬性定義兩個狀態
* 允許在定義的兩個狀態之間切換

這是通過：

* [州提供者](#state-providers)

   管理特定屬性的兩種狀態，以及兩者之間的轉換。

* [工作流程](#workflows)

   管理與狀態相關的操作。

可以定義多個狀態；例如，在Geometrixx中，下列項目包括：

* 訂閱（或取消訂閱）電子報或留言執行緒上的通知
* 向朋友添加和刪除連接

### 州提供者{#state-providers}

狀態提供者管理相關屬性的目前狀態，以及兩個可能狀態之間的轉換。

州級提供者會實作為元件，因此可針對您的專案自訂。 在Geometrixx中，下列項目包括：

* 取消訂閱/訂閱論壇主題
* 添加／刪除朋友

### 工作流程 {#workflows}

州提供者管理描述檔屬性及其狀態。

需要有工作流程來實施與狀態相關的動作。 例如，在訂閱通知時，工作流程將處理實際的訂閱動作；從通知取消訂閱時，工作流程將處理從訂閱清單中移除使用者的問題。

## Profiles and User Accounts {#profiles-and-user-accounts}

配置檔案作為[用戶帳戶](/help/sites-administering/user-group-ac-admin.md)的一部分儲存在內容儲存庫中。

可在`/home/users/geometrixx`下找到配置檔案：

![chlimage_1-138](assets/chlimage_1-138.png)

在標準安裝（作者或發佈）上，每個人都可讀取所有使用者的整個描述檔資訊。 每個人都是「*內建群組」，會自動包含所有現有的使用者和群組。 成員清單不能編輯*&quot;。

這些訪問權限由以下通配符ACL定義：

/home everyone allow jcr:read rep:glob = *.profile*

這允許：

* 論壇、留言或部落格文章，以顯示適當描述檔中的資訊（例如圖示或完整名稱）
* geometrixx描述檔頁面的連結

如果此類存取不適合您的安裝，您可以變更這些預設設定。

這可以使用&#x200B;**[Access Control](/help/sites-administering/user-group-ac-admin.md#access-right-management)**&#x200B;頁籤完成：

![aclmanager](assets/aclmanager.png)

## 配置檔案元件{#profile-components}

您也可以使用一系列描述檔元件來定義您網站的描述檔需求。

### 已檢查密碼欄位 {#checked-password-field}

此元件提供兩個欄位：

* 輸入密碼
* 檢查確認密碼已正確輸入。

使用預設設定，元件將顯示如下：

![dc_profiles_checkedpassword](assets/dc_profiles_checkedpassword.png)

### 設定檔頭像相片 {#profile-avatar-photo}

此元件提供使用者選擇和上傳頭像像片檔案的機制。

![dc_profiles_avatarphoto](assets/dc_profiles_avatarphoto.png)

### 設定檔詳細名稱 {#profile-detailed-name}

此元件可讓使用者輸入詳細名稱。

![dc_profiles_detailedname](assets/dc_profiles_detailedname.png)

### 設定檔性別 {#profile-gender}

此元件可讓使用者輸入其性別。

![dc_profiles_geder](assets/dc_profiles_gender.png)

