---
title: 查看系統資訊
seo-title: View system information
description: 了解如何檢視資源監控圖表，以及執行AEM表單之伺服器的相關資訊。
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

「系統」頁簽顯示資源監視圖表和運行AEM表單的伺服器的相關資訊。 若要存取此資訊，請在管理控制台中，按一下頁面右上角的「健康狀態監視器」 。 如果您在群集環境中運行AEM表單，則顯示的資訊是從伺服器清單中選擇的節點。

要將當前系統資訊另存為屬性檔案，請按一下「保存」。

「系統」頁簽的右窗格顯示以下資訊的圖形表示：

* 工作和工作計數項
* 堆和提交的堆使用
* 非堆和提交的非堆使用

您可以沿著時間軸拖曳指標，以取得特定時間點的值。

>[!NOTE]
>
>圖表資料、伺服器資訊值和時鐘時間每10分鐘更新一次。 資訊不會即時顯示。

「系統」頁簽的左窗格顯示有關伺服器或節點的以下資訊：

**虛擬機：** 伺服器上的Java虛擬機(JVM)版本。

**虛擬機供應商：** JVM的製造商。

**虛擬機版本：** JVM版本號

**電腦名稱：** 安裝AEM表單之伺服器的主機名稱。

**啟動時間：** 伺服器運行的時間（以小時和分鐘為單位）。

**即時編譯器：** 使用的編譯器的名稱。

**編譯時間：** 編譯所花費的時間。

**即時線程數：** AEM表單系統中目前存在的執行緒總數。

**線程數峰值：** 系統上記錄的最大即時線程數。

**載入的類數：** 載入到JVM的類數。

**卸載的類數：** 從JVM卸載的類數。

**最小堆：** 已使用的堆的最小數量。

**最大堆：** 已使用的堆的最大數量。

**作業系統名稱：** AEM表單伺服器上執行的作業系統名稱。

**作業系統版本：** AEM表單伺服器上執行的作業系統版本號。

**作業系統拱：** 運行JVM的作業系統體系結構。

**處理器數：** 系統上的處理器數。

**虛擬機參數：** JVM使用的參數。

**類路徑：** JVM使用的類路徑。

**程式庫路徑：** JVM使用的庫路徑。

**引導類路徑：** JVM使用的引導類路徑。

**應用程式伺服器類型：** 用於運行AEM表單的應用程式伺服器類型。

**應用程式伺服器版本：** 用於運行AEM表單的應用程式伺服器的版本號。

**應用程式伺服器供應商：** 用於運行AEM表單的應用程式伺服器的製造商。

**安裝日期：** 安裝AEM表單的日期（yyyy-mm-dd格式）。

**AEM forms版本：** 已安裝的AEM表單版本。

**修補程式版本：** AEM forms修補程式號。

**資料庫名稱：** AEM表單使用的資料庫類型。

**資料庫版本：** AEM表單使用的資料庫版本號。

**資料庫驅動器名稱：** JVM用於連接到資料庫的驅動程式的名稱。

**資料庫驅動程式版本：** JVM用於連接到資料庫的驅動程式的版本。

此 **儲存** 按鈕可將此系統資訊保存在屬性檔案中。
