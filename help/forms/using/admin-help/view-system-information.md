---
title: 查看系統資訊
seo-title: View system information
description: 瞭解如何查看資源監視圖表以及有關正在運行表單的伺服器AEM的資訊。
seo-description: Learn how you can view resource monitoring charts and information about the server that is running AEM forms.
uuid: 983c1cc7-a8b3-48b2-a4c8-7b28a2e32537
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d51460d9-c96c-4661-b93e-e015427878ab
exl-id: 27a2e81c-47b0-4de8-95bd-7cb34b9450da
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# 查看系統資訊 {#view-system-information}

「系統」頁籤顯示資源監視圖表和有關正在運行表單的伺服器AEM的資訊。 要訪問此資訊，請在管理控制台中按一下頁面右上角的「運行狀況監視器」。 如果您在群集AEM環境中運行表單，則顯示的資訊是從「伺服器」清單中選擇的節點的資訊。

要將當前系統資訊另存為屬性檔案，請按一下「保存」。

「系統」(System)頁籤的右窗格顯示以下資訊的圖形表示：

* 作業和工作計數項
* 堆和已提交堆使用率
* 非堆和已提交非堆使用

可沿時間軸拖動指針以獲取特定時間點的值。

>[!NOTE]
>
>圖形資料、伺服器資訊值和時鐘時間每10分鐘更新一次。 資訊不會即時顯示。

[系統]頁籤的左窗格顯示有關伺服器或節點的以下資訊：

**虛擬機：** 伺服器上的Java虛擬機(JVM)版本。

**虛擬機供應商：** JVM的製造商。

**虛擬機版本：** JVM版本號

**電腦名稱：** 安裝表單的服AEM務器的主機名。

**啟動時間：** 伺服器運行的時間（以小時和分鐘為單位）。

**即時編譯器：** 正在使用的編譯器的名稱。

**編譯時間：** 編譯所花費的時間。

**即時線程數：** 窗體系統中當前存在的線AEM程總數。

**線程數峰值：** 系統上記錄的最大即時線程數。

**載入的類數：** 載入到JVM中的類數。

**已卸載的類數：** 從JVM卸載的類數。

**最小堆：** 已使用的最小堆量。

**最大堆：** 已使用的最大堆量。

**作業系統名稱：** 在forms伺服器上運行的操作系AEM統的名稱。

**作業系統版本：** 在forms伺服器上運行的操作系AEM統的版本號。

**作業系統拱門：** 運行JVM的作業系統體系結構。

**處理器數：** 系統上的處理器數。

**虛擬機參數：** JVM使用的參數。

**類路徑：** JVM使用的類路徑。

**庫路徑：** JVM使用的庫路徑。

**引導類路徑：** JVM使用的引導類路徑。

**應用程式伺服器類型：** 用於運行表單的應用程式服AEM務器類型。

**應用程式伺服器版本：** 用於運行表單的應用程式伺服器的版AEM本號。

**應用程式伺服器供應商：** 用於運行表單的應用程式伺服器的制AEM造商。

**安裝日期：** 已安裝表單的日AEM期（yyyy-mm-dd格式）。

**表AEM單版本：** 已安裝AEM的表單版本。

**修補程式版本：** 表AEM單修補程式號。

**資料庫名稱：** 表單使用的資料AEM庫類型。

**資料庫版本：** 表單使用的資料庫的版AEM本號。

**資料庫驅動器名稱：** JVM用於連接到資料庫的驅動程式的名稱。

**資料庫驅動程式版本：** JVM用於連接到資料庫的驅動程式的版本。

的 **保存** 按鈕，將此系統資訊保存在屬性檔案中。
