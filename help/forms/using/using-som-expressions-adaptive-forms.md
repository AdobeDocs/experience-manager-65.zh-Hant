---
title: 在最適化表單中使用SOM表達式
seo-title: 在最適化表單中使用SOM表達式
description: 瞭解如何擷取最適化表單面板的SOM運算式。
seo-description: 瞭解如何擷取最適化表單面板的SOM運算式。
uuid: c5d55aff-fb69-4a1c-96ea-fb3f9322cbb0
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# 在最適化表單中使用SOM表達式{#using-som-expressions-in-adaptive-forms}

最適化表單會建模為AEM頁面，在AEM儲存庫中會以JCR內容結構表示。 內容結構的關鍵元素為guideContainer節點。 在guideContainer下方，有rootPanel，其中可能包含巢狀面板和欄位。

可以使用指令碼對象模型(SOM)來引用特定文檔對象模型(DOM)中的值、屬性和方法。 DOM將記憶體對象和屬性組織在樹層次中。 SOM表達式引用欄位／繪製元素和面板。

下圖描述了在向表單添加元件時，自適應表單轉換為的節點結構。 例如，您可以新增面板至根面板，並在面板中新增選項按鈕，在執行時期轉換為DOM。 自適應格式的單選按鈕欄位的SOM表達式指定為 `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`。

![DOM樹](assets/hierarchy.png)

DOM樹

自適應形式中任何元素的SOM表達式都以前置詞 `guide[0].guide1[0]`。 元件在節點結構層次中的位置用於導出其SOM表達式。

![具有兩個單選按鈕的DOM樹](assets/hierarchy_radio_button.png)

具有兩個單選按鈕的DOM樹

當您在最適化表單中變更選項按鈕的位置時，SOM運算式會變更。 在編寫模式中，您可以使用「檢視SOM運算式」選項，檢視AEM Forms中欄位或元素的SOM運算式。 當您以滑鼠右鍵按一下欄位或元素時，該選項就會出現在面板上。

![在自適應形式中提取SOM表達式](assets/som-expressions.png)

在自適應形式中提取SOM表達式

在面板中，您可以從面板工具列存取功能。 此功能可協助自適應表單作者編寫指令碼。

![使用面板工具列擷取SOM運算式](assets/som-expression.png)

使用面板工具列擷取SOM運算式

GuideBridge中列出的 [某些API](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.md) ，會使用元素的SOM運算式。 例如，若要以最適化形式將焦點放在特定欄位，請將對應的SOM運算式傳遞至 `getFocus`API `guideBridge`。

