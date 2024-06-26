---
title: 檢視系統資訊
description: 瞭解如何檢視資源監檢視表和執行AEM表單之伺服器的相關資訊。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 27a2e81c-47b0-4de8-95bd-7cb34b9450da
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# 檢視系統資訊 {#view-system-information}

「系統」標籤會顯示資源監檢視表和執行AEM表單之伺服器的相關資訊。 若要存取此資訊，請在管理主控台中，按一下頁面右上角的「健康情況監視」 。 如果您在叢集環境中執行AEM表單，顯示的資訊會針對從「伺服器」清單中選取的節點。

若要將目前系統資訊儲存為屬性檔案，請按一下「儲存」。

「系統」標籤的右窗格會顯示下列資訊的圖形表示：

* 工作與工作計數專案
* 棧積與認可的棧積使用狀況
* 非棧積與認可的非棧積使用狀況

您可以沿著時間軸拖曳指標，以取得特定時間點的值。

>[!NOTE]
>
>圖形資料、伺服器資訊值和時鐘時間每10分鐘更新一次。 此資訊不會即時顯示。

「系統」標籤的左窗格會顯示下列有關伺服器或節點的資訊：

**虛擬機器器：** 伺服器上的Java虛擬機器器(JVM)版本。

**虛擬機器器廠商：** JVM的製造商。

**虛擬機器器版本：** JVM版本號碼

**電腦名稱：** 安裝AEM表單之伺服器的主機名稱。

**運作時間：** 伺服器執行的時間，以小時和分鐘為單位。

**即時編譯器：** 使用的編譯器名稱。

**編譯時間：** 編譯所花費的時間。

**即時Threads數量：** AEM表單系統中目前存在的執行緒總數。

**Threads尖峰數量：** 系統上記錄的最大即時執行緒數量。

**載入的類別數目：** 載入至JVM的類別數目。

**未載入的類別數目：** 從JVM解除安裝的類別數。

**棧積下限：** 使用的棧積數量下限。

**棧積上限：** 使用的棧積數量上限。

**作業系統名稱：** AEM Forms伺服器上執行的作業系統名稱。

**作業系統版本：** 在AEM Forms伺服器上執行的作業系統的版本號碼。

**作業系統拱門：** JVM執行所在的作業系統架構。

**處理器數目：** 系統上的處理器數目。

**虛擬機器器引數：** JVM使用的引數。

**類別路徑：** JVM使用的類別路徑。

**程式庫路徑：** JVM使用的程式庫路徑。

**開機類別路徑：** JVM使用的開機類別路徑。

**應用程式伺服器型別：** 用來執行AEM表單的應用程式伺服器型別。

**應用程式伺服器版本：** 用來執行AEM表單的應用程式伺服器版本號碼。

**應用程式伺服器廠商：** 用來執行AEM表單的應用程式伺服器製造商。

**安裝日期：** 安裝AEM表單的日期（yyyy-mm-dd格式）。

**AEM表單版本：** 已安裝的AEM表單版本。

**修補程式版本：** AEM forms修補程式編號。

**資料庫名稱：** AEM表單使用的資料庫型別。

**資料庫版本：** AEM Forms使用的資料庫版本號碼。

**資料庫磁碟機名稱：** JVM用來連線至資料庫的驅動程式名稱。

**資料庫驅動程式版本：** JVM用來連線到資料庫的驅動程式版本。

此 **儲存** 按鈕可讓您將此系統資訊儲存在屬性檔案中。
