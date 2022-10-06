---
title: 啟用多線程檔案轉換
seo-title: Enabling multi-threaded file conversions
description: 了解如何啟用多執行緒檔案轉換。
seo-description: Learn how to enable multi-threaded file conversions.
uuid: 830c78aa-4f68-4e01-8b24-69a0275689c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 85d655bb-1b6b-4b4d-ae39-eca3ef9b7fd7
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# 啟用多線程檔案轉換 {#enabling-multi-threaded-file-conversions}

PDF生成器為某些類型的檔案啟用多線程檔案轉換。 多執行緒檔案轉換可讓PDF產生器同時執行多次轉換，進而改善其效能。

## 為OpenOffice、Word和PowerPoint文檔啟用多線程檔案轉換 {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

預設情況下，PDF生成器一次只能轉換一個OpenOffice、Microsoft Word或PowerPoint文檔。 如果啟用多線程轉換，PDF生成器可以同時轉換多個文檔。 PDF生成器將啟動多個OpenOffice或PDFMaker實例（用於執行Word和PowerPoint轉換）。

>[!NOTE]
>
>Microsoft Word 2003和PowerPoint 2003不支援多線程檔案轉換。 要啟用多線程檔案轉換，請升級到Microsoft Word 2007和PowerPoint 2007或Microsoft Word 2010和PowerPoint 2010。

>[!NOTE]
>
>Microsoft Excel、Microsoft Visio、Microsoft Project或Microsoft Publisher不支援多線程檔案轉換。

OpenOffice或PDFMaker的每個實例都使用單獨的用戶帳戶啟動。 您添加的每個用戶帳戶必須是在表單伺服器電腦上具有管理權限的有效用戶。 在群集環境中，同一組用戶必須對群集的所有節點有效。

在管理控制台的「用戶帳戶」頁上，您可以指定用於多線程檔案轉換的用戶帳戶。 您可以新增帳戶、刪除帳戶或變更帳戶密碼。 如果您在Windows Server 2003或Windows Server 2008上運行PDF生成器，請至少添加三個具有管理員權限的用戶帳戶。

在Windows Server 2003或2008上添加OpenOffice、Microsoft Word或Microsoft PowerPoint的用戶，或在Linux或Sun™ Solaris™上添加OpenOffice的用戶時，請關閉所有用戶的初始激活對話框。

### 新增取代程式層級代號的權限 {#add-the-right-to-replace-the-process-level-token}

在Windows作業系統上，用於PDF轉換（PDFG用戶）的管理員用戶帳戶將需要替換進程級別令牌權限。 可以使用組策略編輯器添加此權限：

1. 在Windows「開始」菜單中，按一下「運行」，然後輸入gpedit.msc。
1. 按一下「本地電腦策略」>「電腦配置」>「Windows設定」>「安全設定」>「本地策略」>「用戶權限分配」。 編輯 *取代處理層級代號* 包含管理員組的策略。
1. 將使用者新增至取代處理層級代號項目。

### Windows Server 2008上的OpenOffice、Microsoft Word和Microsoft PowerPoint所需的其他配置 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

如果您在Windows Server 2008上運行OpenOffice、Microsoft Word或Microsoft PowerPoint，請為每個添加的用戶禁用UAC。

1. 按一下「控制面板>使用者帳戶>開啟或關閉使用者帳戶控制項」 。
1. 取消選中「Use User Account Control(UAC)to help protect your computer(使用用戶帳戶控制(UAC)幫助保護電腦)」框，然後按一下「OK（確定）」。
1. 重新啟動電腦，使設定生效。

### Linux或Solaris上的OpenOffice所需的其他配置 {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. 新增使用者帳戶。 (請參閱 [新增使用者帳戶](enabling-multi-threaded-file-conversions.md#add-a-user-account).)
1. 接下來，您將對/etc/sudoers檔案進行更改。 此檔案的預設權限為440。 將此檔案的權限更改為可寫。
1. 在/etc/sudoers檔案中為其他用戶（運行表單伺服器的管理員除外）添加項。 例如，如果您以名為lcadm的用戶和名為myhost的伺服器運行AEM表單，並且要模擬user1和user2，請將以下條目添加到/etc/sudoers中：

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   通過此配置，lcadm可以在主機「myhost」上以「user1」或「user2」運行任何命令，而不提示輸入密碼。

   >[!NOTE]
   >
   >請確定您已將系統使用者和PDFG使用者角色指派給「user1」和「user2」。 若要將PDFG角色指派給使用者，請參閱 [新增使用者帳戶](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. 另外，在/etc/sudoers檔案中，通過在行的開頭添加數字元號(#)來找到此行並加註：

   ```shell
   Defaults requiretty
   ```

   這可讓您新增Linux使用者。

1. 將etc/sudoers檔案的權限變回440。
1. 允許您透過 [新增使用者帳戶](enabling-multi-threaded-file-conversions.md#add-a-user-account) 連線至表單伺服器。 例如，要允許名為user1的本地用戶有權連接到表單伺服器，請使用以下命令

   `xhost +local:user1@`

   如需詳細資訊，請參閱xhost命令檔案。

1. 重新啟動伺服器。

>[!NOTE]
>
>必須將OpenOffice安裝在所有PDFG用戶都可以訪問的目錄位置中。 您可以以PDFG用戶身份登錄並檢查是否可以啟動OpenOffice而無問題，以驗證這一點。

### 新增使用者帳戶 {#add-a-user-account}

1. 在管理控制台中，按一下「服務>PDF產生器>使用者帳戶」。
1. 按一下「添加」 ，然後輸入在表單伺服器上具有管理權限的用戶的用戶名和密碼。 如果您正在配置OpenOffice的用戶，請關閉初始的OpenOffice激活對話框。

   >[!NOTE]
   >
   >如果您正在為OpenOffice配置用戶，則OpenOffice實例的數量不能大於此步驟中指定的用戶帳戶數量。

1. 重新啟動表單伺服器。

### 從用於多線程檔案轉換的清單中刪除用戶 {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. 在管理控制台中，按一下「服務>PDF產生器>使用者帳戶」。
1. 按一下要刪除的用戶旁邊的複選框，然後按一下刪除。
1. 在確認頁面上，按一下「刪除」 。
1. 重新啟動表單伺服器。

### 更改帳戶的密碼 {#change-the-password-for-an-account}

1. 在管理控制台中，按一下「服務>PDF產生器>使用者帳戶」。
1. 按一下用戶名，然後輸入並確認新密碼。 此密碼必須與用戶的系統密碼匹配。
