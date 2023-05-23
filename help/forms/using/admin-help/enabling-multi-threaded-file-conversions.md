---
title: 啟用多線程檔案轉換
seo-title: Enabling multi-threaded file conversions
description: 瞭解如何啟用多線程檔案轉換。
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

PDF生成器提供了為特定類型的檔案啟用多線程檔案轉換的功能。 多線程檔案轉換通過允許PDF生成器同時執行多次轉換而提高了其效能。

## 為OpenOffice、Word和PowerPoint文檔啟用多線程檔案轉換 {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

預設情況下，PDF生成器一次只能轉換一個OpenOffice、MicrosoftWord或PowerPoint文檔。 如果啟用多線程轉換，PDF生成器可以同時轉換多個文檔。 PDF生成器將啟動OpenOffice或PDFMaker的多個實例（用於執行Word和PowerPoint轉換）。

>[!NOTE]
>
>MicrosoftWord 2003和PowerPoint 2003不支援多線程檔案轉換。 要啟用多線程檔案轉換，請升級到MicrosoftWord 2007和PowerPoint 2007或MicrosoftWord 2010和PowerPoint 2010。

>[!NOTE]
>
>MicrosoftExcel、MicrosoftVisio、Microsoft項目或MicrosoftPublisher不支援多線程檔案轉換。

OpenOffice或PDFMaker的每個實例都使用單獨的用戶帳戶啟動。 您添加的每個用戶帳戶必須是在forms伺服器電腦上具有管理權限的有效用戶。 在群集環境中，同一組用戶對群集的所有節點都必須有效。

在管理控制台的「用戶帳戶」頁上，可以指定用於多線程檔案轉換的用戶帳戶。 您可以添加帳戶、刪除帳戶或更改帳戶密碼。 如果在Windows Server 2003或Windows Server 2008上運行PDF生成器，請至少添加三個具有管理員權限的用戶帳戶。

在Windows Server 2003或2008上為OpenOffice、MicrosoftWord或MicrosoftPowerPoint添加用戶，或在Linux或Sun™ Solaris™上為OpenOffice添加用戶時，請為所有用戶取消初始激活對話框。

### 添加替換進程級令牌的權限 {#add-the-right-to-replace-the-process-level-token}

在Windows作業系統上，用於PDF轉換（PDFG用戶）的管理員用戶帳戶將需要替換進程級令牌權限。 可以使用組策略編輯器添加此權限：

1. 在Windows「開始」菜單中，按一下「運行」，然後輸入gpedit.msc。
1. 按一下「本地電腦策略」>「電腦配置」>「Windows設定」>「安全設定」>「本地策略」>「用戶權限分配」。 編輯 *替換進程級別令牌* 策略以包括「管理員」組。
1. 將用戶添加到「替換進程級別令牌」條目。

### Windows Server 2008上的OpenOffice、MicrosoftWord和MicrosoftPowerPoint所需的其他配置 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

如果在Windows Server 2008上運行OpenOffice、MicrosoftWord或MicrosoftPowerPoint，請為添加的每個用戶禁用UAC。

1. 按一下「控制面板」>「用戶帳戶」>「開啟或關閉用戶帳戶控制」。
1. 取消選擇「使用用戶帳戶控制(UAC)幫助保護電腦」框，然後按一下「確定」。
1. 重新啟動電腦以使設定生效。

### Linux或Solaris上的OpenOffice所需的其他配置 {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. 添加用戶帳戶。 (請參閱 [添加用戶帳戶](enabling-multi-threaded-file-conversions.md#add-a-user-account)。)
1. 接下來，您將對/etc/sudoers檔案進行更改。 此檔案的預設權限為440。 將此檔案的權限更改為可寫。
1. 在/etc/sudoers檔案中為其他用戶（運行表單伺服器的管理員除外）添加項。 例如，如果您以名為AEMlcadm的用戶和名為myhost的伺服器的身份運行表單，並且要模擬user1和user2，請向/etc/sudoers添加以下條目：

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   此配置使lcadm能夠以&quot;user1&quot;或&quot;user2&quot;的身份在主機&quot;myhost&quot;上運行任何命令，而不提示輸入密碼。

   >[!NOTE]
   >
   >確保已將系統用戶和PDFG用戶角色分配給「user1」和「user2」。 要將PDFG角色分配給用戶，請參閱 [添加用戶帳戶](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. 同樣，在/etc/sudoers檔案中，通過在行的開頭添加數字元號(#)來查找並注釋掉此行：

   ```shell
   Defaults requiretty
   ```

   這使您能夠添加Linux用戶。

1. 將etc/sudoers檔案的權限更改回440。
1. 允許通過 [添加用戶帳戶](enabling-multi-threaded-file-conversions.md#add-a-user-account) 以連接表單伺服器。 例如，要允許名為user1的本地用戶具有與表單伺服器建立連接的權限，請使用以下命令

   `xhost +local:user1@`

   有關詳細資訊，請參閱xhost命令文檔。

1. 重新啟動伺服器。

>[!NOTE]
>
>OpenOffice必須安裝在所有PDFG用戶都可以訪問的目錄位置。 您可以通過以PDFG用戶身份登錄並檢查是否可以在無問題的情況下啟動OpenOffice來驗證這一點。

### 添加用戶帳戶 {#add-a-user-account}

1. 在管理控制台中，按一下「服務」>「PDF生成器」>「用戶帳戶」。
1. 按一下添加，然後輸入對表單伺服器具有管理權限的用戶的用戶名和密碼。 如果要為OpenOffice配置用戶，請關閉初始的OpenOffice激活對話框。

   >[!NOTE]
   >
   >如果為OpenOffice配置用戶，則OpenOffice實例數不能大於此步驟中指定的用戶帳戶數。

1. 重新啟動表單伺服器。

### 從用於多線程檔案轉換的清單中刪除用戶 {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. 在管理控制台中，按一下「服務」>「PDF生成器」>「用戶帳戶」。
1. 按一下要刪除的用戶旁邊的複選框，然後按一下刪除。
1. 在確認頁上，按一下刪除。
1. 重新啟動表單伺服器。

### 更改帳戶的密碼 {#change-the-password-for-an-account}

1. 在管理控制台中，按一下「服務」>「PDF生成器」>「用戶帳戶」。
1. 按一下用戶名，然後輸入並確認新密碼。 此密碼必須與用戶的系統密碼匹配。
