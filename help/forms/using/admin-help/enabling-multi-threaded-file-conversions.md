---
title: 啟用多執行緒檔案轉換
description: 瞭解如何啟用多執行緒檔案轉換。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# 啟用多執行緒檔案轉換 {#enabling-multi-threaded-file-conversions}

PDF Generator可讓您為特定型別的檔案啟用多執行緒檔案轉換。 多執行緒檔案轉換可讓PDF Generator同時執行多個轉換，進而提升轉換效能。

## 啟用OpenOffice、Word和PowerPoint檔案的多執行緒檔案轉換 {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

根據預設，PDF Generator一次只能轉換一個OpenOffice®Microsoft、Word或PowerPoint檔案。 如果您啟用多執行緒轉換，PDF Generator可同時轉換多個檔案。 PDF Generator會啟動多個OpenOffice或PDFMaker例項（用來執行Word和PowerPoint轉換）。

>[!NOTE]
>
>Microsoft® Word 2003和PowerPoint 2003不支援多執行緒檔案轉換。 若要啟用多執行緒檔案轉換，請升級至Microsoft® Word 2007和PowerPoint 2007或Microsoft®Word 2010和PowerPoint 2010。

>[!NOTE]
>
>Microsoft® Excel、Microsoft® Visio、Microsoft® Project或Microsoft® Publisher不支援多執行緒檔案轉換。

OpenOffice或PDFMaker的每個例項都是使用個別的使用者帳戶啟動。 您新增的每個使用者帳戶都必須是Forms Server電腦上具有系統管理許可權的有效使用者。 在叢集環境中，叢集的所有節點都必須有相同的使用者集。

您可以在管理主控台的「使用者帳戶」頁面中，指定要用於多執行緒檔案轉換的使用者帳戶。 您可以新增帳戶、刪除帳戶或變更帳戶密碼。 如果您正在Windows Server 2003或Windows Server 2008上執行PDF Generator，請至少新增三個具有系統管理員許可權的使用者帳戶。

在Windows Server 2003或2008上新增OpenOffice、Microsoft® Word或Microsoft® PowerPoint的使用者，或在Linux®或Sun™ Solaris™上新增OpenOffice的使用者時，請關閉所有使用者的初始啟動對話方塊。

### 新增取代程式層級權杖的權利 {#add-the-right-to-replace-the-process-level-token}

在Windows作業系統上，用於PDF轉換的管理員使用者帳戶（PDFG使用者）必須取代處理序層級權杖許可權。 您可以使用群組原則編輯器來新增此權利：

1. 在Windows「開始」功能表中，按一下「執行」，然後輸入gpedit.msc。
1. 按一下[本機電腦原則] > [電腦組態] > [Windows設定] > [安全性設定] > [本機原則] > [使用者許可權指派]。 編輯&#x200B;*取代處理序層級權杖*&#x200B;原則以包含Administrators群組。
1. 將使用者新增至「取代程式層級權杖」專案。

### Windows Server 2008上的OpenOffice、Microsoft®Word和Microsoft®PowerPoint需要其他設定 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

如果您在Windows Server 2008上執行OpenOffice、Microsoft®Word或Microsoft®PowerPoint，請為每個新增的使用者停用UAC。

1. 按一下「控制面板>使用者帳戶>開啟或關閉使用者帳戶控制」 。
1. 取消選取「使用使用者帳戶控制(UAC)協助保護您的電腦」方塊，然後按一下「確定」。
1. 重新啟動電腦讓設定生效。

### Linux®或Solaris™上的OpenOffice需要其他設定 {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. 新增使用者帳戶。 （請參閱[新增使用者帳戶](enabling-multi-threaded-file-conversions.md#add-a-user-account)。）
1. 接下來，您必須變更/etc/sudoers檔案。 此檔案的預設許可權為440。 將此檔案的許可權變更為可寫入。
1. 在/etc/sudoers檔案中新增其他使用者(除了執行Forms伺服器的管理員之外)的專案。 例如，如果您以名為lcadm的使用者和名為myhost的伺服器身分執行AEM表單，並且想要模擬user1和user2，請將下列專案新增到/etc/sudoers：

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   此設定可讓lcadm在主機&#39;myhost&#39;上以&#39;user1&#39;或&#39;user2&#39;執行任何命令，而不需要提示輸入密碼。

   >[!NOTE]
   >
   >確保您已為「user1」和「user2」指派系統使用者和PDFG使用者角色。 若要將PDFG角色指派給使用者，請參閱[新增使用者帳戶](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. 同樣在/etc/sudoers檔案中，找到並註解此行，方式是在行首新增數字元號(#)：

   ```shell
   Defaults requiretty
   ```

   這可讓您新增Linux®使用者。

1. 將etc/sudoers檔案的許可權變更回440。
1. 允許透過[新增使用者帳戶](enabling-multi-threaded-file-conversions.md#add-a-user-account)新增的所有使用者與Forms伺服器建立連線。 例如，若要授予名為user1的本機使用者連線Forms伺服器的許可權，請使用以下命令

   `xhost +local:user1@`

   如需詳細資訊，請參閱xhost命令檔案。

1. 重新啟動伺服器。

>[!NOTE]
>
>OpenOffice必須安裝在所有PDFG使用者都能存取的目錄位置。 您可以以PDFG使用者身分登入，並檢查您是否可以在沒有問題的情況下啟動OpenOffice，以確認這點。

### 新增使用者帳戶 {#add-a-user-account}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

1. 在管理控制檯中，按一下「服務>PDF Generator>使用者帳戶」。
1. 按一下新增，然後輸入在Forms伺服器上擁有管理許可權的使用者的使用者名稱和密碼。 如果您正在設定OpenOffice的使用者，請關閉初始OpenOffice啟用對話方塊。

   >[!NOTE]
   >
   >如果您正在設定OpenOffice的使用者，OpenOffice的執行個體數目不能大於此步驟中指定的使用者帳戶數目。

1. 重新啟動Forms伺服器。

### 從用於多執行緒檔案轉換的清單中移除使用者 {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. 在管理控制檯中，按一下「服務>PDF Generator>使用者帳戶」。
1. 按一下您要移除的使用者旁的核取方塊，然後按一下刪除。
1. 在確認頁面上，按一下刪除。
1. 重新啟動Forms伺服器。

### 變更帳戶的密碼 {#change-the-password-for-an-account}

1. 在管理控制檯中，按一下「服務>PDF Generator>使用者帳戶」。
1. 按一下使用者名稱，然後輸入並確認新密碼。 此密碼必須符合使用者的系統密碼。
