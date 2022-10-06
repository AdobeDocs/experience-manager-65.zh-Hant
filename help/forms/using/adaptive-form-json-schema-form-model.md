---
title: 如何使用JSON結構描述建立適用性Forms?
description: 了解如何使用JSON結構描述作為表單模型來建立最適化表單。 您可以使用現有的JSON結構來建立最適化表單。 深入了解JSON結構描述的範例、JSON結構描述定義中的預先設定欄位、限制最適化表單元件的可接受值，以及了解不支援的建構。
feature: Adaptive Forms
role: User, Developer
level: Beginner, Intermediate
exl-id: 1b402aef-a319-4d32-8ada-cadc86f5c872
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 4%

---

# 使用JSON結構建立最適化表單 {#creating-adaptive-forms-using-json-schema}

## 必備條件 {#prerequisites}

使用JSON結構描述製作最適化表單模型，需要基本了解JSON結構描述。 建議在本文之前閱讀下列內容。

* [建立最適化表單](creating-adaptive-form.md)
* [JSON結構](https://json-schema.org/)

## 使用JSON結構描述作為表單模型  {#using-a-json-schema-as-form-model}

[!DNL Adobe Experience Manager Forms] 支援使用現有的JSON結構描述作為表單模型來建立最適化表單。 此JSON結構表示組織中後端系統產生或使用資料的結構。 您使用的JSON結構應符合 [v4規格](https://json-schema.org/draft-04/schema).

使用JSON結構描述的主要功能為：

* JSON的結構在最適化表單的製作模式中，會顯示為「內容尋找器」索引標籤中的樹狀結構。 您可以將元素從JSON階層拖曳並新增至最適化表單。
* 您可以使用符合相關結構的JSON預先填入表單。
* 提交時，使用者輸入的資料會以符合相關結構的JSON提交。

JSON結構包含簡單且複雜的元素類型。 元素具有將規則新增至元素的屬性。 將這些元素和屬性拖曳至最適化表單時，會自動對應至對應的最適化表單元件。

此JSON元素與最適化表單元件的對應如下：

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
   <th><strong>最適化表單元件</strong></th>
  </tr>
  <tr>
   <td><p>具有enum和enumNames約束的字串屬性。</p> <p>語法，</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>下拉元件：</p>
    <ul>
     <li>enumNames中列出的值將顯示在下拉框中。</li>
     <li>列舉中列出的值會用於計算。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>具有格式約束的字串屬性。 例如，電子郵件和日期。</p> <p>語法，</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>類型為字串且格式為電子郵件時，會對應電子郵件元件。</li>
     <li>類型為字串且格式為主機名時，會對應具有驗證的TextBox元件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> 文字欄位<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>數字屬性<br /> </td>
   <td>子類型設定為float的數值欄位<br /> </td>
  </tr>
  <tr>
   <td>整數屬性<br /> </td>
   <td>子類型設為整數的數值欄位<br /> </td>
  </tr>
  <tr>
   <td>布林屬性<br /> </td>
   <td>切換<br /> </td>
  </tr>
  <tr>
   <td>物件屬性<br /> </td>
   <td>面板<br /> </td>
  </tr>
  <tr>
   <td>陣列屬性</td>
   <td>最小值和最大值分別等於minItems和maxItems的可重複面板。 僅支援同質陣列。 因此，項約束必須是對象而不是陣列。<br /> </td>
  </tr>
 </tbody>
</table>

### 公用架構屬性 {#common-schema-properties}

適用性表單使用JSON結構描述中的可用資訊來對應每個產生的欄位。 特別是：

* 此 `title` 屬性可作為最適化表單元件的標籤。
* 此 `description` 屬性會設定為適用性表單元件的長說明。
* 此 `default` 屬性可作為最適化表單欄位的初始值。
* 此 `maxLength` 屬性設為 `maxlength` 屬性。
* 此 `minimum`, `maximum`, `exclusiveMinimum`，和 `exclusiveMaximum` 屬性用於數值框元件。
* 支援範圍 `DatePicker component` 其他JSON結構屬性 `minDate` 和 `maxDate` 已提供……
* 此 `minItems` 和 `maxItems` 屬性可用來限制可從面板元件新增或移除的項目/欄位數。
* 此 `readOnly` 屬性設定 `readonly` 適用性表單元件的屬性。
* 此 `required` 屬性會將適用性表單欄位標示為必填欄位，但在面板中（其中type為object），最終提交的JSON資料中的欄位會包含與該物件對應之空白值。
* 此 `pattern` 屬性在適用性表單中設為驗證模式（規則運算式）。
* JSON結構描述檔案的副檔名必須保留為.schema.json。 例如， &lt;filename>.schema.json。

## 範例JSON結構描述 {#sample-json-schema}

以下是JSON結構描述的範例。

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

### 可重複使用的架構定義 {#reusable-schema-definitions}

定義索引鍵可用來識別可重複使用的結構描述。 可重複使用的架構定義用於建立片段。 這類似於在XSD中識別複雜類型。 以下提供定義的範例JSON結構描述：

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

上例定義了客戶記錄，其中每個客戶都有發運和計費地址。 地址的結構相同（地址具有街道地址、城市地址和州地址），因此最好不要複製地址。 此外，欄位的新增和刪除也方便您日後進行任何變更。

## JSON結構定義中的預先設定欄位 {#pre-configuring-fields-in-json-schema-definition}

您可以使用 **aem:afProperties** 屬性來預先設定JSON結構描述欄位，以對應至自訂最適化表單元件。 以下列出範例：

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

## 配置表單對象的指令碼或表達式  {#configure-scripts-or-expressions-for-form-objects}

JavaScript是最適化表單的運算式語言。 所有運算式都是有效的JavaScript運算式，且會使用最適化表單指令碼模型API。 您可以將表單物件預先設定為 [評估運算式](adaptive-form-expressions.md) 在表單事件上。

使用aem:afproperties屬性來預先設定最適化表單元件的最適化表單運算式或指令碼。 例如，觸發初始化事件時，以下程式碼會設定電話欄位的值，並列印值至記錄檔：

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

您應是 [forms-power-user組](forms-groups-privileges-tasks.md) 配置表單對象的指令碼或表達式。 下表列出最適化表單元件支援的所有指令碼事件。

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
   <td>數值欄位</td>
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

在JSON中使用事件的一些範例是，在初始化事件時隱藏欄位，並在值提交事件時設定其他欄位的值。 如需為指令碼事件建立運算式的詳細資訊，請參閱 [適用性表單運算式](adaptive-form-expressions.md).

以下是先前提及範例的範例JSON程式碼。

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

#### 在值提交事件時配置另一個欄位的值 {#configure-value-of-another-field-on-value-commit-event}

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

## 限制最適化表單元件的可接受值 {#limit-acceptable-values-for-an-adaptive-form-component}

您可以將下列限制新增至JSON結構描述元素，以限制最適化表單元件可接受的值：

<table>
 <tbody>
  <tr>
   <td><p><strong> 結構屬性</strong></p> </td>
   <td><p><strong>資料類型</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
   <td><p><strong>Component</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定數值和日期的上界。 預設會包含最大值。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器<br /> </li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定數值和日期的下限。 預設會包含最小值。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>布林值</p> </td>
   <td><p>如果為true，則表單元件中指定的數值或日期必須小於為maximum屬性指定的數值或日期。</p> <p>如果為false，則表單元件中指定的數值或日期必須小於或等於為最大屬性指定的數值或日期。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>布林值</p> </td>
   <td><p>如果為true，則表單元件中指定的數值或日期必須大於為最小屬性指定的數值或日期。</p> <p>如果為false，則表單元件中指定的數值或日期必須大於或等於為最小屬性指定的數值或日期。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定元件中允許的字元數量最小。 最小長度必須等於或大於零。</p> </td>
   <td>
    <ul>
     <li>文字方塊</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>字串</td>
   <td>指定元件中允許的字元數上限。 最大長度必須等於或大於零。</td>
   <td>
    <ul>
     <li>文字方塊</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定字元的順序。 如果字元符合指定的模式，元件將接受字元。</p> <p>模式屬性映射到相應自適應表單元件的驗證模式。</p> </td>
   <td>
    <ul>
     <li>對應至XSD架構的所有適用性表單元件 </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>字串</td>
   <td>指定陣列中的項目數上限。 最大項目必須等於或大於零。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>字串</td>
   <td>指定陣列中的最小項目數。 最小項目必須等於或大於零。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 不支援的構造  {#non-supported-constructs}

適用性表單不支援下列JSON結構：

* Null類型
* 聯合類型（如any）和
* OneOf、AnyOf、AllOf和NOT
* 僅支援同質陣列。 因此，項約束必須是對象而不是陣列。

## 常見問題 {#frequently-asked-questions}

**為什麼我無法為可重複的子表單拖曳子表單的個別元素（從任何複雜類型產生的結構）（minOccours或maxOccurs值大於1）?**

在可重複的子表單中，您必須使用完整的子表單。 如果您只想要選擇性欄位，請使用整個結構並刪除不需要的結構。

**我在「內容尋找器」中有一個長而複雜的結構。 如何尋找特定元素？**

您有兩個選項：

* 滾動瀏覽樹結構
* 使用「搜尋」方塊來尋找元素

**JSON結構描述檔案的副檔名為何？**

JSON結構描述檔案的副檔名必須為.schema.json。 例如， &lt;filename>.schema.json。
