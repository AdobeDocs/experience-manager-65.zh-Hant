---
title: 如何使用JSON架構建立自適應Forms?
description: 瞭解如何使用JSON架構作為表單模型建立自適應表單。 可以使用現有JSON架構建立自適應表單。 使用JSON架構的示例進行更深入的挖掘，在JSON架構定義中預配置欄位，限制自適應表單元件的可接受值，並學習不支援的構造。
feature: Adaptive Forms
role: User, Developer
level: Beginner, Intermediate
exl-id: 1b402aef-a319-4d32-8ada-cadc86f5c872
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 4%

---

# 使用JSON架構建立自適應表單 {#creating-adaptive-forms-using-json-schema}

## 必備條件 {#prerequisites}

使用JSON架構作為其表單模型創作自適應表單需要對JSON架構有基本的瞭解。 建議在本文之前閱讀以下內容。

* [建立自適應窗體](creating-adaptive-form.md)
* [JSON架構](https://json-schema.org/)

## 將JSON架構用作表單模型  {#using-a-json-schema-as-form-model}

[!DNL Adobe Experience Manager Forms] 支援使用現有JSON架構作為表單模型建立自適應表單。 此JSON架構表示組織中後端系統生成或使用資料的結構。 您使用的JSON架構應與 [v4規格](https://json-schema.org/draft-04/schema)。

使用JSON架構的主要功能有：

* JSON的結構在自適應表單的創作模式下的「內容查找器」頁籤中顯示為樹。 您可以將元素從JSON層次結構拖動並添加到自適應窗體。
* 可以使用與關聯架構相容的JSON預填充表單。
* 在提交時，用戶輸入的資料將作為與關聯架構對齊的JSON提交。

JSON架構由簡單和複雜的元素類型組成。 元素具有向元素添加規則的屬性。 當這些元素和屬性被拖到自適應表單上時，它們將自動映射到相應的自適應表單元件。

JSON元素與自適應表單元件的映射如下：

```json
"birthDate": {
              "type": "string",
              "format": "date",
              "pattern": "date{DD MMMM, YYYY}",
              "aem:affKeyword": [
                "DOB",
                "Date of Birth"
              ],
              "description": "Date of birth in DD MMMM, YYYY",
              "aem:afProperties": {
                "displayPictureClause": "date{DD MMMM, YYYY}",
                "displayPatternType": "date{DD MMMM, YYYY}",
                "validationPatternType": "date{DD MMMM, YYYY}",
                "validatePictureClause": "date{DD MMMM, YYYY}",
                "validatePictureClauseMessage": "Date must be in DD MMMM, YYYY format."
              }
```

<table>
 <tbody>
  <tr>
   <th><strong>JSON元素、屬性或屬性</strong></th>
   <th><strong>自適應表單元件</strong></th>
  </tr>
  <tr>
   <td><p>具有enum和enumNames約束的字串屬性。</p> <p>語法，</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>下拉元件：</p>
    <ul>
     <li>enumNames中列出的值將顯示在下拉框中。</li>
     <li>枚舉中列出的值用於計算。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>帶格式約束的字串屬性。 例如，電子郵件和日期。</p> <p>語法，</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>當類型為字串且格式為電子郵件時，將映射電子郵件元件。</li>
     <li>當類型為字串且格式為主機名時，將映射帶驗證的文本框元件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> 文本欄位<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>number屬性<br /> </td>
   <td>子類型設定為浮動的數字欄位<br /> </td>
  </tr>
  <tr>
   <td>整數屬性<br /> </td>
   <td>子類型設定為整數的數字欄位<br /> </td>
  </tr>
  <tr>
   <td>布爾型<br /> </td>
   <td>切換<br /> </td>
  </tr>
  <tr>
   <td>對象屬性<br /> </td>
   <td>面板<br /> </td>
  </tr>
  <tr>
   <td>陣列屬性</td>
   <td>最小值和最大值分別等於minItems和maxItems的可重複面板。 僅支援同構陣列。 因此項目約束必須是對象而不是陣列。<br /> </td>
  </tr>
 </tbody>
</table>

### 公用架構屬性 {#common-schema-properties}

自適應表單使用JSON架構中的可用資訊來映射每個生成的欄位。 特別是：

* 的 `title` 屬性用作自適應窗體元件的標籤。
* 的 `description` 屬性設定為自適應窗體元件的長說明。
* 的 `default` 屬性用作自適應窗體欄位的初始值。
* 的 `maxLength` 屬性設定為 `maxlength` 文本欄位元件的屬性。
* 的 `minimum`。 `maximum`。 `exclusiveMinimum`, `exclusiveMaximum` 屬性用於「數字」框元件。
* 支援範圍 `DatePicker component` 其他JSON架構屬性 `minDate` 和 `maxDate` 。
* 的 `minItems` 和 `maxItems` 屬性用於限制可從面板元件中添加或刪除的項/欄位數。
* 的 `readOnly` 屬性設定 `readonly` 屬性。
* 的 `required` 屬性將自適應表單域標籤為必需欄位，而在面板（其中type為object）中，最終提交的JSON資料具有與該對象對應的空值欄位。
* 的 `pattern` 屬性設定為自適應形式的驗證模式（規則運算式）。
* JSON架構檔案的副檔名必須保留為.schema.json。 比如說， &lt;filename>.schema.json。

## 示例JSON架構 {#sample-json-schema}

下面是JSON架構的示例。

```json
{
 "$schema": "https://json-schema.org/draft-04/schema#",
 "definitions": {
  "employee": {
   "type": "object",
   "properties": {
    "userName": {
     "type": "string"
    },
    "dateOfBirth": {
     "type": "string",
     "format": "date"
    },
    "email": {
     "type": "string",
     "format": "email"
    },
    "language": {
     "type": "string"
    },
    "personalDetails": {
     "$ref": "#/definitions/personalDetails"
    },
    "projectDetails": {
     "$ref": "#/definitions/projectDetails"
    }
   },
   "required": [
    "userName",
    "dateOfBirth",
    "language"
   ]
  },
  "personalDetails": {
   "type": "object",
   "properties": {
    "GeneralDetails": {
     "$ref": "#/definitions/GeneralDetails"
    },
    "Family": {
     "$ref": "#/definitions/Family"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "projectDetails": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projects": {
      "$ref": "#/definitions/projects"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projects": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projectsAdditional": {
      "$ref": "#/definitions/projectsAdditional"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projectsAdditional": {
   "type": "array",
   "items": {
    "properties": {
     "Additional_name": {
      "type": "string"
     },
     "Additional_areacode": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "GeneralDetails": {
   "type": "object",
   "properties": {
    "age": {
     "type": "number"
    },
    "married": {
     "type": "boolean"
    },
    "phone": {
     "type": "number",
     "aem:afProperties": {
      "sling:resourceType": "/libs/fd/af/components/guidetelephone",
      "guideNodeClass": "guideTelephone"
     }
    },
    "address": {
     "type": "string"
    }
   }
  },
  "Family": {
   "type": "object",
   "properties": {
    "spouse": {
     "$ref": "#/definitions/spouse"
    },
    "kids": {
     "$ref": "#/definitions/kids"
    }
   }
  },
  "Income": {
   "type": "object",
   "properties": {
    "monthly": {
     "type": "number"
    },
    "yearly": {
     "type": "number"
    }
   }
  },
  "spouse": {
   "type": "object",
   "properties": {
    "name": {
     "type": "string"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "kids": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  }
 },
 "type": "object",
 "properties": {
  "employee": {
   "$ref": "#/definitions/employee"
  }
 }
}
```

### 可重用架構定義 {#reusable-schema-definitions}

定義鍵用於標識可重用方案。 可重用架構定義用於建立片段。 它類似於在XSD中標識複雜類型。 下面提供了一個帶定義的示例JSON架構：

```json
{
  "$schema": "https://json-schema.org/draft-04/schema#",

  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "type": "object",

  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

上例定義了客戶記錄，其中每個客戶都有發運地址和開單地址。 兩個地址的結構相同 — 地址具有街道地址、城市地址和省/市/自治區地址 — 因此最好不要複製這些地址。 它還使添加和刪除欄位變得容易，以便將來進行任何更改。

## JSON架構定義中的預配置欄位 {#pre-configuring-fields-in-json-schema-definition}

您可以使用 **aem:afProperties** 用於預配置JSON架構欄位以映射到自定義自適應窗體元件的屬性。 下面列出了一個示例：

```json
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512,
            "aem:afProperties" : {
                 "sling:resourceType" : "/apps/fd/af/components/guideTextBox",
                 "guideNodeClass" : "guideTextBox"
             }
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}
```

## 為表單對象配置指令碼或表達式  {#configure-scripts-or-expressions-for-form-objects}

JavaScript是自適應表單的表達式語言。 所有表達式都是有效的JavaScript表達式，並使用自適應表單指令碼模型API。 可以將表單對象預配置為 [計算表達式](adaptive-form-expressions.md) 表單活動。

使用aem:afproperties屬性為自適應表單元件預配置自適應表單表達式或指令碼。 例如，當觸發初始化事件時，下面的代碼設定電話欄位的值並將值打印到日誌中：

```json
"telephone": {
  "type": "string",
  "pattern": "/\\d{10}/",
  "aem:affKeyword": ["phone", "telephone","mobile phone", "work phone", "home phone", "telephone number", "telephone no", "phone number"],
  "description": "Telephone Number",
  "aem:afProperties" : {
    "sling:resourceType" : "fd/af/components/guidetelephone",
    "guideNodeClass" : "guideTelephone",
    "events": {
      "Initialize" : "this.value = \"1234567890\"; console.log(\"ef:gh\") "
    }
  }
}
```

你應該是 [表單超級用戶組](forms-groups-privileges-tasks.md) 為窗體對象配置指令碼或表達式。 下表列出了自適應表單元件支援的所有指令碼事件。

<table>
 <tbody>
  <tr>
   <th><strong></strong>元件\事件</th>
   <th>初始化 <br /> </th>
   <td>計算</td>
   <td>可見性</td>
   <td>驗證</td>
   <td>已啟用</td>
   <td>提交值</td>
   <td>按一下 </td>
   <td>選項</td>
  </tr>
  <tr>
   <td>文字欄位</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>數字欄位</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>數值步進器</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>選項按鈕</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>電話</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>切換</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>按鈕</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>核取方塊</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>下拉式清單</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>影像選擇</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>資料輸入欄位</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>日期挑選器</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>電子郵件</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>檔案附件</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>影像</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Draw</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>面板</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

在JSON中使用事件的一些示例是在初始化事件時隱藏一個欄位，並在值提交事件時配置另一個欄位的值。 有關為指令碼事件建立表達式的詳細資訊，請參見 [自適應表單表達式](adaptive-form-expressions.md)。

下面是前面提到的示例的示例JSON代碼。

### 在初始化事件時隱藏欄位 {#hiding-a-field-on-initialize-event}

```json
"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### 配置值提交事件上其他欄位的值 {#configure-value-of-another-field-on-value-commit-event}

```json
"Income": {
    "type": "object",
    "properties": {
        "monthly": {
            "type": "number",
            "aem:afProperties": {
                "events" : {
                    "Value Commit" : "IncomeYearly.value = this.value * 12;"
                }
            }
        },
        "yearly": {
            "type": "number",
            "aem:afProperties": {
                "name": "IncomeYearly"
            }
        }
    }
}
```

## 限制自適應表單元件的可接受值 {#limit-acceptable-values-for-an-adaptive-form-component}

可以將以下限制添加到JSON架構元素，以限制自適應表單元件可接受的值：

<table>
 <tbody>
  <tr>
   <td><p><strong> 架構屬性</strong></p> </td>
   <td><p><strong>資料類型</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
   <td><p><strong>Component</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定數值和日期的上限。 預設情況下，包括最大值。</p> </td>
   <td>
    <ul>
     <li>數字框</li>
     <li>數值步進器<br /> </li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定數值和日期的下界。 預設情況下，包括最小值。</p> </td>
   <td>
    <ul>
     <li>數字框</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>布林值</p> </td>
   <td><p>如果為true，則在窗體元件中指定的數值或日期必須小於為maximum屬性指定的數值或日期。</p> <p>如果為false，則在表單元件中指定的數值或日期必須小於或等於為maximum屬性指定的數值或日期。</p> </td>
   <td>
    <ul>
     <li>數字框</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>布林值</p> </td>
   <td><p>如果為true，則在窗體元件中指定的數值或日期必須大於為minimum屬性指定的數值或日期。</p> <p>如果為false，則表單元件中指定的數值或日期必須大於或等於為最小值屬性指定的數值或日期。</p> </td>
   <td>
    <ul>
     <li>數字框</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定元件中允許的最小字元數。 最小長度必須等於或大於零。</p> </td>
   <td>
    <ul>
     <li>文本框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>字串</td>
   <td>指定元件中允許的最大字元數。 最大長度必須等於或大於零。</td>
   <td>
    <ul>
     <li>文本框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定字元的順序。 如果字元符合指定的模式，則元件將接受字元。</p> <p>該模式屬性映射到相應自適應表單元件的驗證模式。</p> </td>
   <td>
    <ul>
     <li>映射到XSD架構的所有自適應表單元件 </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>字串</td>
   <td>指定陣列中的最大項數。 最大項必須等於或大於零。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>字串</td>
   <td>指定陣列中最小項數。 最小項必須等於或大於零。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 不支援的構造  {#non-supported-constructs}

自適應表單不支援以下JSON架構構造：

* 空類型
* 聯合類型，如any和
* OneOf、AnyOf、AllOf和NOT
* 僅支援同構陣列。 因此，項目約束必須是對象而不是陣列。

## 常見問題 {#frequently-asked-questions}

**為什麼無法為可重複子表單拖動子表單（從任何複雜類型生成的結構）的單個元素（minOccours或maxOccurs值大於1）?**

在可重複的子窗體中，必須使用完整的子窗體。 如果只需要選擇欄位，請使用整個結構並刪除不需要的欄位。

**我在Content Finder中有一個很長的複雜結構。 如何找到特定元素？**

您有兩個選擇：

* 滾動瀏覽樹結構
* 使用「搜索」框查找元素

**JSON架構檔案的副檔名應是什麼？**

JSON架構檔案的副檔名必須為.schema.json。 比如說， &lt;filename>.schema.json。
