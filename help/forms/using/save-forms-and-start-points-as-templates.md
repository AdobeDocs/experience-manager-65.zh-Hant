---
title: 將表單另存為範本
description: 瞭解如何從含有重複所需資料的表單建立範本。
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: b97175fd-cc3d-457a-af11-1f8c83192eb7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 將表單另存為範本 {#save-forms-as-templates}

有時，使用者填寫表單時，對幾個欄位的輸入會維持不變。 對於這類例項，您可以填寫每個例項中需要相同值的欄位，並將表單或草稿另存為範本。 現在，每次建立範本的執行個體時，指定的欄位都會填入範本中指定的值。 這有助於您節省填寫表單所需的時間和精力。

執行以下步驟來建立範本：

1. 開啟表單，然後選取或填寫每次使用時幾乎具有相同值的欄位。 您可以在範本中加入附件，您通常會在填寫表單時新增該範本。
1. 選取&#x200B;**另存為範本** ![save_as_template](assets/save_as_template.png)圖示。 會出現一個對話方塊，指定範本的名稱。
1. 指定範本的名稱，並選取&#x200B;**儲存**。 範本會顯示在範本資料夾中。

   如果存在相同名稱的範本，則會出現一個對話方塊，確認覆寫現有範本。 若要以新範本取代現有的範本，請選取[繼續]****，若要以其他名稱儲存範本，請選取[取消]****。

現在，您可以開啟已儲存的範本。 每次開啟範本時，都會建立新表單或任務，且表單會顯示儲存的資料和選項。 使用範本，您可以編輯預填的資料、新增附件、另存為草稿、提交任務或使用它建立另一個範本。 範本是行動裝置專屬且未與Adobe Experience Manager Forms伺服器同步。

如果不再需要範本，您也可以將其刪除。 若要刪除範本，請瀏覽至範本資料夾，選取省略符號，然後選取&#x200B;**刪除範本**。

>[!NOTE]
>
>範本可在本機使用，且未與伺服器同步。 清除應用程式的本機資料會刪除範本。
