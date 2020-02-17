---
title: 自訂文字編輯器
seo-title: 自訂文字編輯器
description: 瞭解如何自訂文字編輯器。
seo-description: 瞭解如何自訂文字編輯器。
uuid: 598246fe-8f15-49b6-b6d3-9154bebcd27e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 666fee78-a103-44dc-afe7-71b90ce219b7
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# 自訂文字編輯器{#customize-text-editor}

## 概覽 {#overview}

您可以在「管理資產」和「建立對應UI」中自訂文字編輯器，以新增更多字型和字型大小。 這些字型包括英文和非英文，例如日文字型。

您可以自訂以變更字型設定中的下列項目：

* 字型系列和大小
* 高度和字母間距等屬性
* 字型系列和大小、高度、字母間距和日期格式的預設值
* 項目符號縮排

若要這麼做，您必須：

1. [在CRX中編輯tbxeditor-config.xml檔案以自訂字型](#customizefonts)
1. [將自訂字型新增至用戶端電腦](#addcustomfonts)

## 在CRX中編輯tbxeditor-config.xml檔案以自訂字型 {#customizefonts}

若要透過編輯tbxeditor-config.xml檔案來自訂字型，請執行下列動作：

1. 前往並 `https://[server]:[port]/[ContextPath]/crx/de` 以管理員身分登入。
1. 在應用程式檔案夾中，使用類似設定檔案夾的路徑／結構建立名為config的檔案夾，該檔案夾位於libs/fd/cm/config中，請執行下列步驟：

   1. 以滑鼠右鍵按一下下列路徑上的items資料夾，然後選取「覆 **蓋節點」**:

      `/libs/fd/cm/config`

      ![覆蓋節點](assets/1-1.png)

   1. 請確定「覆蓋節點」對話框具有下列值：

      **** 路徑：/libs/fd/cm/config

      **** 位置：/apps/

      **** 匹配節點類型：已選取

      ![覆蓋節點](assets/2.png)

   1. 按一下 **確定**。 資料夾結構會建立在應用程式資料夾中。

   1. 按一下「 **全部儲存**」。

1. 使用以下步驟，在新建的config資料夾中建立tbxeditor-config.xml檔案的副本：

   1. 在libs/fd/cm/config處按一下右鍵tbxeditor-config.xml檔案，然後選擇「 **複製」**。
   1. 按一下右鍵以下資料夾，然後選擇「 **貼上」:**

      `apps/fd/cm/config`

   1. 預設情況下，貼上檔案的名稱為「將檔案更名為」( `copy of tbxeditor-config.xml.` Rename the file to)，然 `tbxeditor-config.xml` 後按一下「 **全部保存」(Save All)**。

1. 在apps/fd/cm/config處開啟tbxeditor-config.xml檔案，然後進行必要的變更。

   1. 連按兩下apps/fd/cm/config處的tbxeditor-config.xml檔案。 檔案隨即開啟。

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

   1. 在檔案中進行必要的變更，以變更字型設定中的下列項目：

      * 新增或移除字型系列和大小
      * 高度和字母間距等屬性
      * 字型系列和大小、高度、字母間距和日期格式的預設值
      * 項目符號縮排
      例如，若要新增名為Sazanami Mincho Medium的日文字型，您必須在XML檔案中輸入下列項目： `<font>Sazanami Mincho Medium</font>`。 您也需要將此字型安裝在用戶端機器上，以便存取及使用字型自訂。 如需詳細資訊，請參 [閱「將自訂字型新增至用戶端電腦」](#addcustomfonts)。

      您也可以變更文字各個方面的預設值，並借由移除項目，從文字編輯器移除字型。

   1. 按一下「 **全部儲存**」。


## 將自訂字型新增至用戶端電腦 {#addcustomfonts}

當您在「對應管理」文字編輯器中存取字型時，字型必須出現在您用來存取「對應管理」的用戶端機器中。 若要在文字編輯器中使用自訂字型，您必須先在用戶端機器上安裝相同的字型。

如需安裝字型的詳細資訊，請參閱下列：

* [在Windows上安裝或解除安裝字型](https://windows.microsoft.com/en-us/windows-vista/install-or-uninstall-fonts)
* [Mac基本功能：字型簿](https://support.apple.com/en-us/HT201749)

## 存取字型自訂 {#access-font-customizations}

在CRX的tbxeditor-config.xml檔案中變更字型，並在用來存取AEM Forms的用戶端機器上安裝必要的字型後，這些變更就會出現在文字編輯器中。

例如，在 [Customize fonts by editing the tbxeditor-config.xml file in CRX](#customizefonts) procedure中添加的Sazanami Mincho Medium字型會以如下方式顯示在文本編輯器用戶介面中：

![sazanaminchointext](assets/sazanamiminchointext.png)

>[!NOTE]
>
>若要查看日文文字，您必須先輸入含日文字元的文字。 自訂日文字型的應用程式只會以特定方式格式化文字。 自訂日文字型的應用程式不會將英文或其他字元變更為日文字元。

