---
title: 自訂文字編輯器
seo-title: 自訂文字編輯器
description: 了解如何自訂文字編輯器。
seo-description: 了解如何自訂文字編輯器。
uuid: 598246fe-8f15-49b6-b6d3-9154bebcd27e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 666fee78-a103-44dc-afe7-71b90ce219b7
docset: aem65
feature: 通信管理
exl-id: 1dd3f55c-24f7-4331-a9a3-c9223e613fec
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# 自訂文字編輯器{#customize-text-editor}

## 概覽 {#overview}

您可以在「管理資產」和「建立通信UI」中自訂文字編輯器，以新增更多字型和字型大小。 這些字型包括英文和非英文，如日文字型。

您可以自訂以在字型設定中變更下列項目：

* 字型系列和大小
* 高度和字母間距等屬性
* 字型系列和大小、高度、字母間距和日期格式的預設值
* 項目符號縮進

要執行此操作，您需要：

1. [在CRX中編輯tbxeditor-config.xml檔案以自訂字型](#customizefonts)
1. [將自定義字型添加到客戶端電腦](#addcustomfonts)

## 在CRX中編輯tbxeditor-config.xml檔案以自訂字型 {#customizefonts}

要通過編輯tbxeditor-config.xml檔案來自定義字型，請執行以下操作：

1. 前往`https://'[server]:[port]'/[ContextPath]/crx/de`並以管理員身分登入。
1. 在應用程式資料夾中，使用類似設定資料夾（位於libs/fd/cm/config）的路徑/結構，建立名為config的資料夾，步驟如下：

   1. 按一下右鍵以下路徑上的「項目」資料夾，然後選擇「覆蓋節點」**:**

      `/libs/fd/cm/config`

      ![覆蓋節點](assets/1-1.png)

   1. 確定「覆蓋節點」對話方塊有下列值：

      **路徑：** /libs/fd/cm/config

      **位置：** /apps/

      **匹配節點類型：** 已選取

      ![覆蓋節點](assets/2.png)

   1. 按一下&#x200B;**「確定」**。資料夾結構會在應用程式資料夾中建立。

   1. 按一下「**全部保存**」。

1. 使用下列步驟，在新建立的設定資料夾中建立tbxeditor-config.xml檔案的副本：

   1. 在libs/fd/cm/config按一下右鍵tbxeditor-config.xml檔案，然後選擇&#x200B;**Copy**。
   1. 按一下右鍵以下資料夾，然後選擇&#x200B;**貼上：**

      `apps/fd/cm/config`

   1. 依預設，貼上的檔案的名稱為`copy of tbxeditor-config.xml.`將檔案重新命名為`tbxeditor-config.xml` ，然後按一下&#x200B;**儲存全部**。

1. 在apps/fd/cm/config處開啟tbxeditor-config.xml檔案，然後進行所需的變更。

   1. 在apps/fd/cm/config處按兩下tbxeditor-config.xml檔案。 檔案隨即開啟。

      ```xml
      <editorConfig>
         <bulletIndent>0.25in</bulletIndent>
      
         <defaultDateFormat>DD-MM-YYYY</defaultDateFormat>
      
         <fonts>
            <default>Times New Roman</default>
            <font>_sans</font>
            <font>_serif</font>
            <font>_typewriter</font>
            <font>Arial</font>
            <font>Courier</font>
            <font>Courier New</font>
            <font>Geneva</font>
            <font>Georgia</font>
            <font>Helvetica</font>
            <font>Tahoma</font>
            <font>Times New Roman</font>
            <font>Times</font>
            <font>Verdana</font>
         </fonts>
      
         <fontSizes>
            <default>12</default>
            <fontSize>8</fontSize>
            <fontSize>9</fontSize>
            <fontSize>10</fontSize>
            <fontSize>11</fontSize>
            <fontSize>12</fontSize>
            <fontSize>14</fontSize>
            <fontSize>16</fontSize>
            <fontSize>18</fontSize>
            <fontSize>20</fontSize>
            <fontSize>22</fontSize>
            <fontSize>24</fontSize>
            <fontSize>26</fontSize>
            <fontSize>28</fontSize>
            <fontSize>36</fontSize>
            <fontSize>48</fontSize>
            <fontSize>72</fontSize>
         </fontSizes>
      
         <lineHeights>
            <default>2</default>     
            <lineHeight>2</lineHeight>
            <lineHeight>3</lineHeight>
            <lineHeight>4</lineHeight>
            <lineHeight>5</lineHeight>
            <lineHeight>6</lineHeight>
            <lineHeight>7</lineHeight>
            <lineHeight>8</lineHeight>
            <lineHeight>9</lineHeight>
            <lineHeight>10</lineHeight>
            <lineHeight>11</lineHeight>
            <lineHeight>12</lineHeight>
            <lineHeight>13</lineHeight>
            <lineHeight>14</lineHeight>
            <lineHeight>15</lineHeight>
            <lineHeight>16</lineHeight>
         </lineHeights>
      
         <letterSpacings>
            <default>0</default>
            <letterSpacing>0</letterSpacing>
            <letterSpacing>1</letterSpacing>
            <letterSpacing>2</letterSpacing>
            <letterSpacing>3</letterSpacing>
            <letterSpacing>4</letterSpacing>
            <letterSpacing>5</letterSpacing>
            <letterSpacing>6</letterSpacing>
            <letterSpacing>7</letterSpacing>
            <letterSpacing>8</letterSpacing>
            <letterSpacing>9</letterSpacing>
            <letterSpacing>10</letterSpacing>
            <letterSpacing>11</letterSpacing>
            <letterSpacing>12</letterSpacing>
            <letterSpacing>13</letterSpacing>
            <letterSpacing>14</letterSpacing>
            <letterSpacing>15</letterSpacing>
            <letterSpacing>16</letterSpacing>
         </letterSpacings>
      </editorConfig>
      ```

   1. 在檔案中進行所需的變更，以變更字型設定中的下列項目：

      * 添加或刪除字型系列和大小
      * 高度和字母間距等屬性
      * 字型系列和大小、高度、字母間距和日期格式的預設值
      * 項目符號縮進

      例如，要添加名為Sazanami Mincho Medium的日文字型，需要在XML檔案中進行以下條目：`<font>Sazanami Mincho Medium</font>`。 您還需要在用於存取和使用字型自訂的用戶端電腦上安裝此字型。 有關詳細資訊，請參閱[向客戶端電腦添加自定義字型](#addcustomfonts)。

      您也可以更改文本各個方面的預設值，並通過刪除條目，從文本編輯器中刪除字型。

   1. 按一下「**全部保存**」。


## 將自定義字型添加到客戶端電腦 {#addcustomfonts}

當您在通信管理文本編輯器中訪問字型時，字型必須存在於您用來訪問通信管理的客戶端電腦中。 若要在文字編輯器中使用自訂字型，您必須先在用戶端電腦上安裝相同的字型。

有關安裝字型的詳細資訊，請參閱以下內容：

* [在Windows上安裝或卸載字型](https://windows.microsoft.com/en-us/windows-vista/install-or-uninstall-fonts)
* [Mac基本介紹：字型簿](https://support.apple.com/en-us/HT201749)

## 訪問字型自定義{#access-font-customizations}

在CRX中對tbxeditor-config.xml檔案中的字型進行變更，並在用於存取AEM Forms的用戶端電腦上安裝所需字型後，變更會顯示在文字編輯器中。

例如，在[Customize fonts by editing tbxeditor-config.xml檔案（在CRX](#customizefonts)過程中）中添加的Sazanami Mincho Medium字型顯示在文本編輯器UI中，如下所示：

![sanamiminchointext](assets/sazanamiminchointext.png)

>[!NOTE]
>
>若要查看日文文字，您必須先輸入帶有日文字元的文字。 自訂日文字型的應用程式只會以特定方式格式化文字。 應用自定義日文字型不會將英文或其他字元更改為日文字元。
