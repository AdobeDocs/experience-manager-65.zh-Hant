---
title: 啟用多執行緒檔案轉換
seo-title: 啟用多執行緒檔案轉換
description: 瞭解如何啟用多執行緒檔案轉換。
seo-description: 瞭解如何啟用多執行緒檔案轉換。
uuid: 830c78aa-4f68-4e01-8b24-69a0275689c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 85d655bb-1b6b-4b4d-ae39-eca3ef9b7fd7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 啟用多執行緒檔案轉換 {#enabling-multi-threaded-file-conversions}

PDF產生器可針對特定類型的檔案啟用多執行緒檔案轉換。 多執行緒檔案轉換可讓PDF產生器同時執行多個轉換，進而改善其效能。

## 為OpenOffice、Word和PowerPoint檔案啟用多執行緒檔案轉換 {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

依預設，PDF產生器一次只能轉換一份OpenOffice、Microsoft word或PowerPoint檔案。 如果您啟用多執行緒轉換，PDF產生器可同時轉換多個檔案。 PDF產生器將啟動多個OpenOffice或PDFMaker執行個體（用於執行Word和PowerPoint轉換）。

>[!NOTE]
>
>Microsoft Word 2003和PowerPoint 2003不支援多執行緒檔案轉換。 若要啟用多執行緒檔案轉換，請升級至Microsoft Word 2007和PowerPoint 2007或Microsoft Word 2010和PowerPoint 2010。

>[!NOTE]
>
>Microsoft Excel、Microsoft Visio、Microsoft project或Microsoft Publisher不支援多執行緒檔案轉換。

每個OpenOffice或PDFMaker例項都是使用個別的使用者帳戶啟動。 您新增的每個使用者帳戶都必須是具有Forms伺服器電腦管理權限的有效使用者。 在群集環境中，同一組用戶對群集的所有節點都必須有效。

在管理控制台的「使用者帳戶」頁面上，您可以指定用於多執行緒檔案轉換的使用者帳戶。 您可以新增帳戶、刪除帳戶或變更帳戶密碼。 如果您在Windows Server 2003或Windows Server 2008上執行PDF產生器，請新增至少三個具有管理員權限的使用者帳戶。

在Windows Server 2003或2008上新增OpenOffice、Microsoft word或Microsoft powerPoint的使用者，或在Linux或Sun™ Solaris™上新增OpenOffice的使用者時，請關閉所有使用者的初始啟動對話方塊。

### 新增取代程式層級Token的權限 {#add-the-right-to-replace-the-process-level-token}

在Windows作業系統上，用於PDF轉換（PDF使用者）的管理員使用者帳戶將需要取代處理層級的Token權限。 您可以使用群組原則編輯器來新增此項：

1. 在Windows的「開始」菜單中，按一下「運行」，然後輸入gpedit.msc。
1. 按一下「本機電腦原則>電腦設定> windows設定>安全性設定>本機原則>使用者權限分配」。 編輯「取 *代處理層級Token* 」原則以包含「管理員」群組。
1. 將使用者新增至「取代處理層級Token」項目。

### Windows Server 2008上的OpenOffice、Microsoft word和Microsoft powerPoint需要額外的設定 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

如果您在Windows Server 2008上執行OpenOffice、Microsoft word或Microsoft powerPoint，請針對新增的每個使用者停用UAC。

1. 按一下「控制面板>使用者帳戶>開啟或關閉使用者帳戶控制」。
1. 取消選取「使用使用者帳戶控制(UAC)協助保護您的電腦」方塊，然後按一下「確定」。
1. 重新啟動電腦以使設定生效。

### Linux或Solaris上的OpenOffice需要其他配置 {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. 新增使用者帳戶。 (請參 [閱新增使用者帳戶](enabling-multi-threaded-file-conversions.md#add-a-user-account)。)
1. 接下來，您將對/etc/sudoers檔案進行更改。 此檔案的預設權限為440。 將此檔案的權限更改為可寫。
1. 在/etc/sudoers檔案中新增其他使用者（執行表單伺服器的管理員除外）的項目。 例如，如果您以名為lcadm的使用者和名為myhost的伺服器身分執行AEM表單，而您想要模擬user1和user2，請將下列項目新增至/etc/sudoers:

   ```as3
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   此配置使lcadm能夠以「user1」或「user2」身份在主機「myhost」上運行任何命令，而不提示輸入密碼。

   >[!NOTE]
   >
   >請確定您已將系統使用者和PDFG使用者角色指派給「user1」和「user2」。 若要將PDFG角色指派給使用者，請參 [閱新增使用者帳戶](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. 此外，在/etc/sudoers檔案中，在行的開頭加上數字元號(#)，找出此行並加上註解：

   ```as3
   Defaults requiretty
   ```

   這可讓您新增Linux使用者。

1. 將etc/sudoers檔案的權限變更回440。
1. 允許您透過「新增使用者帳戶 [」新增的所有使用者](enabling-multi-threaded-file-conversions.md#add-a-user-account) ，以連線至表單伺服器。 例如，要允許名為user1的本地用戶訪問Forms伺服器的連接權限，請使用以下命令

   `xhost +local:user1@`

   有關詳細資訊，請參閱xhost命令文檔。

1. 重新啟動伺服器。

>[!NOTE]
>
>OpenOffice必須安裝在所有PDFG使用者皆可存取的目錄位置。 您可以以PDFG使用者身分登入並檢查是否可以無問題地啟動OpenOffice來驗證此點。

### 新增使用者帳戶 {#add-a-user-account}

1. 在管理控制台中，按一下「服務> PDF產生器>使用者帳戶」。
1. 按一下「新增」，然後輸入對表單伺服器具有管理權限的使用者的使用者名稱和密碼。 如果您要設定OpenOffice的使用者，請關閉初始的OpenOffice啟動對話方塊。

   >[!NOTE]
   >
   >如果您正在為OpenOffice配置用戶，則OpenOffice實例數不能大於此步驟中指定的用戶帳戶數。

1. 重新啟動表單伺服器。

### 從用於多線程檔案轉換的清單中刪除用戶 {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. 在管理控制台中，按一下「服務> PDF產生器>使用者帳戶」。
1. 按一下您要移除之使用者旁的核取方塊，然後按一下「刪除」。
1. 在確認頁面上，按一下「刪除」。
1. 重新啟動表單伺服器。

### 變更帳戶的密碼 {#change-the-password-for-an-account}

1. 在管理控制台中，按一下「服務> PDF產生器>使用者帳戶」。
1. 按一下用戶名，然後輸入並確認新密碼。 此密碼必須符合使用者的系統密碼。

