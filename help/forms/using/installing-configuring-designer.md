---
title: 安裝和配置設計工具
seo-title: Installing and configuring Designer
description: 'Designer是獨立安裝程式，也與Workbench搭配使用。 了解如何安裝獨立設計工具。  '
seo-description: Designer is available as a stand-alone installer and is also bundled with Workbench. Learn how to install stand-alone Designer.
uuid: c5b779d1-cb6a-48f4-87d6-48464753e516
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f3a5b5ce-2262-4d5d-a8ae-d59a3a4229e7
docset: aem65
role: Admin
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
source-git-commit: a3cf926bde4a4b3a0810058e84ac01012a4a3a57
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---

# 安裝和配置設計工具{#installing-and-configuring-designer}

## 先決條件 {#pre-requisites}

AEM Forms Designer安裝程式需要32位元版本 [Visual C++可再分發運行時包2012](https://support.microsoft.com/en-us/topic/the-latest-supported-visual-c-downloads-2647da03-1eea-4433-9aff-95f26a218cc0) 和 [Visual C++可再分發運行時包2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). 開始安裝之前，請確定已安裝先前提到的可再分發的執行階段套件。

安裝或卸載Designer需要管理員權限。

## 安裝設計器 {#install-designer}

Designer作為獨立安裝程式提供，並與WorkBench捆綁。 如果您使用Designer的獨立安裝程式，請執行以下步驟：

1. 從Adobe下載設計器 [授權網站](https://licensing.adobe.com/).

   >[!NOTE]
   >
   >如果已安裝舊版Designer，請先卸載舊版，然後再繼續。

1. 按兩下setup.exe以啟動Designer安裝程式。
1. 繼續，在「個人化」畫面上提供您的詳細資訊和序號。
1. 如果您接受許可協定，請按一下「下一步」以繼續。
1. （可選）如果要在所選位置安裝Designer，請更改預設安裝路徑。 按一下下一步。
1. 按一下「上一步」以變更任何偏好設定。 要安裝設計器，請按一下「安裝」。
1. 安裝完成後，按一下「完成」。

或者，您也可以使用被動或靜默模式通過命令行安裝設計器。

* 被動命令行安裝：安裝程式將顯示進度欄，該進度欄指示安裝正在進行，但不顯示提示或錯誤消息。 啟動後，無法取消安裝。

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* 靜默命令行安裝：安裝程式會執行安裝，而不顯示使用者介面。 不顯示提示、消息或對話框。 啟動後，無法取消安裝。

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```


