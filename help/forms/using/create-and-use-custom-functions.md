---
title: 在最適化表單中建立及新增自訂函式
description: AEM Forms支援自訂函式，可讓使用者在規則編輯器中建立並使用自己的函式。
keywords: 新增自訂函式、使用自訂函式、建立自訂函式，以及在規則編輯器中使用自訂函式。
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: a328b4a8-e8dd-42a0-b73b-94e76c7692a8
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 5%

---


# 最適化Forms中的自訂函式（核心元件）

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/create-and-use-custom-functions) |
| AEM 6.5 | 本文章 |

## 簡介

AEM Forms 6.5匯入定義JavaScript函式的功能，以在使用規則編輯器定義複雜商業規則時使用這些函式。 AEM Forms提供許多立即可用的自訂函式，但您需要定義自己的自訂函式，並在多個表單中使用這些函式。

自訂函式可協助處理輸入的資料，以符合指定的需求，進而擴充表單的功能。 它們還可以根據預先定義的條件來啟用表單行為的動態變更。
在調適型Forms中，您可以在中使用自訂函式 [最適化表單的規則編輯器](/help/forms/using/rule-editor.md) 以建立表單欄位的特定驗證規則。
讓我們瞭解自訂功能的使用方式，使用者可在其中輸入電子郵件地址，而您想要確保輸入的電子郵件地址遵循特定格式（其中包含「@」符號和網域名稱）。 將自訂函式建立為「ValidateEmail」，此函式會以電子郵件地址作為輸入，並在有效時傳回true，否則傳回false。

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

在上述範例中，當使用者嘗試提交表單時，會叫用自訂函式「ValidateEmail」以檢查輸入的電子郵件地址是否有效。

## 使用自訂函式 {#uses-of-custom-function}

在最適化Forms中使用自訂函式的優點包括：

* **資料操控**：自訂函式會操控及處理輸入至表單欄位中的資料。
* **資料驗證**：自訂函式可讓您對表單輸入執行自訂檢查，並提供指定的錯誤訊息。
* **動態行為**：自訂函式可讓您根據特定條件控制表單的動態行為。 例如，您可以顯示/隱藏欄位、修改欄位值或動態調整表單邏輯。
* **整合**：您可以使用自訂函式與外部API或服務整合。 它有助於從外部來源擷取資料、傳送資料至外部Rest端點，或根據外部事件執行自訂動作。

## 支援的JS註解

確認您撰寫的自訂函式會附帶 `jsdoc` 在其上方，如果您需要自訂設定和說明。 有許多方式可以在中宣告函式 `JavaScript,` 和註解可讓您追蹤函式。 如需詳細資訊，請參閱 [usejsdoc.org](https://jsdoc.app/).

支援 `jsdoc` 標籤：

* **私人**
語法： `@private`
私人函式不會納入為自訂函式。

* **名稱**
語法： `@name funcName <Function Name>`
或者 `,` 您可以使用： `@function funcName <Function Name>` **或** `@func` `funcName <Function Name>`.
  `funcName` 是函式的名稱（不允許空格）。
  `<Function Name>` 是函式的顯示名稱。

* **會員**
語法： `@memberof namespace`
將名稱空間附加至函式。

* **引數**
語法： `@param {type} name <Parameter Description>`
或者，您可以使用： `@argument` `{type} name <Parameter Description>` **或** `@arg` `{type}` `name <Parameter Description>`.
顯示函式使用的引數。 一個函式可以有多個引數標籤，每個引數會依發生順序各一個標籤。
  `{type}` 代表引數型別。 允許的引數型別為：

   1. 字串
   2. 數字
   3. 布林值
   4. 範圍

  範圍是用來反向連結最適化表單的欄位。 表單使用緩慢載入時，您可以使用 `scope` 以存取其欄位。 您可以在載入欄位時存取欄位，或者如果欄位標示為全域。

  所有其他引數型別則歸類於上述其中一種。 不支援任何專案。 請確定您選取以上任一型別。 型別不區分大小寫。 引數中不允許空格 `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **傳回型別**
語法： `@return {type}`
或者，您可以使用 `@returns {type}`.
新增函式的相關資訊，例如其目標。
{type} 代表函式的傳回型別。 允許的傳回型別為：

   1. 字串
   1. 數字
   1. 布林值

  所有其他回訪型別則會歸類到上述任一型別下。 不支援任何專案。 請確定您選取以上任一型別。 傳回型別不區分大小寫。

* **這個**
語法： `@this currentComponent`

  使用@this可參照寫入規則的最適化表單元件。

  以下範例是根據欄位值。 在以下範例中，規則會隱藏表單中的欄位。 此 `this` 部分 `this.value` 是指寫入規則的基礎調適型表單元件。

  ```
     /**
     * @function myTestFunction
     * @this currentComponent
     * @param {scope} scope in which code inside function will be executed.
     */
     myTestFunction = function (scope) {
        if(this.value == "O"){
              scope.age.visible = true;
        } else {
           scope.age.visible = false;
        }
     }
  ```

  >[!NOTE]
  >
  >使用自訂函式之前的註解作為摘要。 摘要可以延伸至多行，直到遇到標籤為止。 將大小限製為單一，以在規則產生器中提供簡要說明。

## 函式宣告支援的型別 {#function-declaration-supported-types}

**函式陳述式**

```javascript
function area(len) {
    return len*len;
}
```

此函式包含但不包含 `jsdoc` 評論。

**函式運算式**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**函式運算式和陳述式**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**函式宣告為變數**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

限制：自訂函式只會從變數清單中挑選第一個函式宣告（如果同時挑選）。 您可以對每個宣告的函式使用函式運算式。

**函式宣告為物件**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

## 建立自訂函式 {#create-custom-function}

若要建立自訂函式，請執行下列步驟：

1. 登入 `http://server:port/crx/de/index.jsp#`.
1. 在 `/apps` 檔案夾中建立一個檔案夾。例如，建立名為的資料夾 `experience-league`.
1. 儲存您的變更。
1. 導覽至建立的資料夾並建立型別節點 `cq:ClientLibraryFolder` 作為 `clientlibs`.
1. 導覽至新建立的 `clientlibs` 資料夾並新增 `allowProxy` 和 `categories` 屬性：

   ![自訂程式庫節點屬性](/help/forms/using/assets/customlibrary-catproperties.png)

   >[!NOTE]
   >
   > 您可以提供任何名稱來取代 `customfunctionsdemo`.

1. 儲存您的變更。

1. 建立名為的資料夾 `js` 在 `clientlibs` 資料夾。
1. 建立名為的JavaScript檔案 `functions.js` 在 `js` 資料夾
1. 建立名為的檔案 `js.txt` 在 `clientlibs` 資料夾。
1. 儲存您的變更。
已建立的檔案夾結構如下所示：

   ![已建立的用戶端資料庫檔案夾結構](/help/forms/using/assets/clientlibrary_folderstructure.png)
1. 按兩下 `functions.js` 檔案以開啟編輯器。 此檔案包含自訂函式的程式碼。
將下列程式碼新增至JavaScript檔案，以根據出生日期計算年齡(YYYY-MM-DD)。

   ```javascript
       /**
            * Calculates Age
            * @name calculateAge 
            * @return {string} 
       */
   
       function calculateAge(dateOfBirthString) {
       var dob = new Date(dateOfBirthString);
       var now = new Date();
   
       var age = now.getFullYear() - dob.getFullYear();
       var monthDiff = now.getMonth() - dob.getMonth();
   
       if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
       age--;
       }
   
       return age;
       }
   ```

1. 儲存 `function.js`.
1. 瀏覽至 `js.txt` 並新增下列程式碼：

   ```javascript
       #base=js
       functions.js
   ```

1. 儲存 `js.txt` 檔案。

您可參考以下內容 [自訂函式](/help/forms/using/assets/customfunction.zip) 資料夾。 下載並在您的AEM執行個體中安裝此資料夾。

現在，您可以新增使用者端程式庫，以在最適化表單中使用自訂函式。

## 在最適化表單中新增使用者端程式庫{#use-custom-function}

將使用者端程式庫部署到Forms CS環境後，請在最適化表單中使用其功能。 若要在最適化表單中新增使用者端程式庫

1. 在編輯模式中開啟您的表單。 若要以編輯模式開啟表單，請選取表單並選取 **[!UICONTROL 編輯]**.
1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「參考線容器」屬性圖示。 此時會開啟「最適化表單容器」對話框。
1. 開啟 **[!UICONTROL 基本]** 標籤並選取 **[!UICONTROL 使用者端資料庫類別]** 從下拉式清單（在此例中為「選取」） `customfunctionscategory`)。

   ![新增自訂函式使用者端程式庫](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. 按一下 **[!UICONTROL 完成]** .

現在，您可以建立規則，以在規則編輯器中使用自訂函式：

![新增自訂函式使用者端程式庫](/help/forms/using//assets/calculateage-customfunction.png)

現在，讓我們來瞭解如何使用 [AEM Forms中的規則編輯器的叫用服務](/help//forms/using/rule-editor.md).
