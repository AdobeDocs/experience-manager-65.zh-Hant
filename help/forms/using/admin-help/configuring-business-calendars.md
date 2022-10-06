---
title: 配置業務日曆
seo-title: Configuring Business Calendars
description: 業務日曆定義貴組織的業務日和非業務日。 了解如何配置業務日曆。
seo-description: Business calendars define business and non-business days for your organization. Learn how to configure the business calendars.
uuid: 0ba610b8-72a8-480c-8783-70d98cbe890a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7a85e13d-4800-47c4-812a-5c6e2355298a
exl-id: 4282718a-41f1-411a-9cd7-8c470005107d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 0%

---

# 配置業務日曆 {#configuring-business-calendars}

*業務日曆* 為貴組織定義業務日和非工作日（例如法定假日、週末和公司關閉日）。 使用商業日曆時，AEM表單在執行特定日期計算時會略過非工作日。 在Workbench中，您可以指定是否對與使用者相關聯的事件（例如任務提醒、截止時間和呈報）或與使用者無關的動作（例如計時器事件和等待服務）使用商業日曆。

例如，任務提醒被配置為在任務分配給用戶後的三個工作日內發生。 任務在星期四分配。 但是，後三天不是工作日，因為星期五是全國假日，而後兩天是週末。 因此，提醒將於下週的星期三發送。

>[!NOTE]
>
>使用業務日曆計算日期和時間時，AEM表單會使用其執行所在伺服器的日期和時間，不會針對時區之間的差異進行調整。 例如，如果任務提醒計畫於上午10:00在倫敦運行的伺服器上發生，但接收提醒的用戶位於紐約市，則用戶將於當地時間凌晨5:00收到提醒。

## 使用預設業務日曆 {#using-the-default-business-calendar}

AEM forms提供預設的商務日曆(名為 *內建日曆*)將星期六和星期日指定為非工作日。 如果組織中的所有使用者有相同的非工作日，您可以更新預設的業務日曆以符合組織。 僅使用預設業務日曆時，您無需在「用戶管理」中啟用業務日曆或提供任何映射。 當未定義其他業務日曆時，AEM Forms將使用預設的業務日曆。

## 設定多個業務日曆 {#setting-up-multiple-business-calendars}

如果組織中的某些用戶具有不同的非工作日，則您可以定義多個業務日曆並配置映射，以允許用戶對業務日曆的運行時解析。

### 定義多個業務日曆 {#define-multiple-business-calendars}

1. 決定如何將適當的業務日曆與用戶關聯。 將業務日曆與用戶關聯有兩種方法：

   **群組成員資格：** 您可以根據使用者的群組成員資格，將業務日曆指派給使用者。 在這種情況下，群組中的每位使用者都會使用相同的商業行事歷。

   如果用戶是兩個不同組的成員，並且這些組被映射到兩個不同的業務日曆，則AEM表單將使用其在搜索結果中找到的第一個日曆。 在這種情況下，請考慮使用業務日曆鍵將用戶與業務日曆關聯。

   **業務日曆密鑰：** 您可以根據業務日曆鍵（在「用戶管理」中指定的設定）將業務日曆分配給用戶。 然後，在表單工作流中將業務日曆密鑰映射到業務日曆。

   將業務日曆密鑰分配給用戶的方式取決於您使用的是企業、本地還是混合域。 如需設定網域的詳細資訊，請參閱 [新增網域](/help/forms/using/admin-help/adding-domains.md#adding-domains).

   如果您使用本機或混合網域，則有關使用者的資訊只會儲存在使用者管理資料庫中。 要為這些用戶設定業務日曆鍵，請在「用戶管理」中添加或編輯用戶時，在「業務日曆鍵」欄位中輸入字串。 (請參閱 [新增和設定使用者](/help/forms/using/admin-help/adding-configuring-users.md#adding-and-configuring-users).) 然後，您可將業務日曆鍵（字串）映射到表單工作流中的業務日曆。 (請參閱 [將用戶和組映射到業務日曆](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

   如果使用的是企業域，則有關用戶的資訊駐留在第三方儲存系統中，如LDAP目錄，用戶管理會與用戶管理資料庫同步該目錄。 這允許您將業務日曆密鑰映射到LDAP目錄中的欄位。 例如，如果目錄中的每個用戶記錄都包含「國家/地區」欄位，並且要根據用戶所在的國家/地區來分配業務日曆，請在指定目錄的用戶設定時，在「業務日曆密鑰」欄位中指定「國家/地區」欄位名稱。 (請參閱 [配置目錄](/help/forms/using/admin-help/configuring-directories.md#configuring-directories).) 然後，您可以將業務日曆鍵（為LDAP目錄中的「國家/地區」欄位定義的值）映射到表單工作流中的業務日曆。 (請參閱 [將用戶和組映射到業務日曆](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

1. 在表單工作流程中，為共用相同非工作日的每組使用者定義日曆。 (請參閱 [建立或更新業務日曆](configuring-business-calendars.md#create-or-update-a-business-calendar).)
1. 在表單工作流程中，映射每個日曆的業務日曆鍵或組成員資格。 (請參閱 [將用戶和組映射到業務日曆](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)
1. 在Workbench中，流程開發人員可選擇是否使用業務日曆來提醒、截止時間和升級。 (請參閱 [Workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   如果流程開發人員選擇使用業務日曆，AEM Forms將根據User Management設定和Administration Console中定義的業務日曆映射動態選擇相應的業務日曆，或者，如果不存在映射，則使用預設日曆。

   如果流程開發人員不使用業務日曆，則事件的日期計算會將每天視為業務日。 例如，任務期限被配置為在任務分配給用戶後三天執行。 任務在星期四分配。 任務截止日期是週日，即使是週末。

## 建立或更新業務日曆 {#create-or-update-a-business-calendar}

如果您的組織包含具有不同非工作日的不同用戶集，則可以定義多個業務日曆。 您也可以變更現有日曆，包括AEM表單隨附的預設內建日曆。

>[!NOTE]
>
>如果您未建立新的業務日曆，則將使用預設日曆。

1. 在管理控制台中，按一下「服務>Forms工作流程>業務日曆」。
1. 要添加新業務日曆，請按一下 ![bus_cal_plus](assets/bus_cal_plus.png). 文字 *新日曆* 會顯示在下拉式清單中。 選取文字，然後輸入日曆的其他名稱。

   要編輯現有業務日曆，請從下拉清單中選擇該日曆。

1. 在「預設非工作天」下，選擇任何每週非工作天，如週末。
1. [可選] 選擇「使用工作時間」，並指定工作日的開始和結束時間。

   如果選擇此選項，在指定時間範圍之前發生的事件將移至時間範圍的開頭，而在時間範圍之後發生的事件將移至下一個工作日的開始時間。

   例如，假設某個情況是，某個用戶在星期二凌晨2:00被分配了任務，該任務的提醒設定為兩個工作天。 如果沒有工作時間，提醒將在週四凌晨2:00發生。 如果工作時間設為上午8:00至下午5:00，則提醒將被推送到星期四上午8:00。 在沒有營業時間的情況下，如果星期二下午6:00建立了提醒事件，則提醒將在星期四的營業時間之後發生。 營業時間設為上午8:00至下午5:00，提醒將在星期五上午8:00發生。

1. 在左側的日曆中，按兩下任何其他非工作日，例如假日。 不能選擇過去的天數。 您選取的非工作日會顯示在右側的清單中，日期會在一行中顯示兩次。 選擇左側的日期，以鍵入非工作日的名稱或說明。

   要從清單中刪除非工作日，請按一下 ![bus_cal_crash](assets/bus_cal_trash.png) 就在這裡。

1. [可選] 如果此日曆將是預設日曆，請選擇「預設日曆」。 如果與用戶關聯的事件不存在其他日曆映射，或者沒有為計時器事件或等待服務指定業務日曆，則使用預設日曆。 您無法刪除預設日曆。
1. 定義完非工作日後，選擇「已啟用日曆」使其處於活動狀態，然後按一下「保存」。

   如果要更新現有日曆，則新版本將立即生效，並用於所有業務日曆計算，包括已運行的任務。

   >[!NOTE]
   >
   >如果未啟用日曆，則將使用預設日曆。

## 將用戶和組映射到業務日曆 {#mapping-users-and-groups-to-a-business-calendar}

有兩種方法可用來將業務日曆與使用者建立關聯。 您可以根據業務日曆密鑰或根據用戶所屬的目錄組為用戶分配業務日曆。 您可以使用「映射」頁簽指定AEM表單將使用的方法，也可以將業務日曆鍵和組映射到業務日曆。 有關將業務日曆密鑰與用戶關聯的詳細資訊，請參閱 [設定多個業務日曆](configuring-business-calendars.md#setting-up-multiple-business-calendars).

### 根據業務日曆鍵將業務日曆與用戶關聯 {#associate-business-calendars-with-users-based-on-business-calendar-keys}

1. 在管理控制台中，按一下「服務」>「表單工作流」>「業務日曆」，然後按一下「映射」頁簽。
1. 在「系統將使用」清單中，選擇「用戶管理器業務日曆」鍵解析。
1. 選擇「顯示用戶管理器業務日曆密鑰」。 隨即顯示一個清單，其中包含已在「用戶管理」中定義的一組唯一的業務日曆鍵。

   對於本地和混合域，該清單顯示在「用戶管理」的「業務日曆鍵」欄位中輸入的值。 對於企業(LDAP)域，該清單顯示從LDAP域設定中配置的LDAP欄位（例如「國家/地區」）返回的唯一集。

   如果用戶管理管理員未定義任何業務日曆鍵，則清單將為空。

1. 對於UM業務日曆鍵清單中的每個項，選擇日曆。
1. 按一下「儲存」。

### 根據目錄服務組將業務日曆與用戶和組關聯 {#associate-business-calendars-with-users-and-groups-based-on-directory-service-groups}

1. 在管理控制台中，按一下「服務」>「表單工作流」>「業務日曆」，然後按一下「映射」頁簽。
1. 在「系統將使用」清單中，選擇由目錄伺服器定義的組。
1. 在「映射」頁簽上，選擇「顯示目錄服務組」。 隨即顯示一個清單，其中包含已在「使用者管理」中定義的群組。 (請參閱 [目錄設定](/help/forms/using/admin-help/configuring-directories.md#directory-settings).)

   >[!NOTE]
   >
   >在Workbench中，如果您已將使用者服務設定為使用商業日曆，且該服務已指派給群組，AEM Forms會使用此處指定的群組對應來解析群組的日曆。 AEM Forms一律使用群組對應來解析群組的日曆，即使您使用商業日曆索引鍵來解析使用者的日曆亦然。 如果未找到組映射，則使用預設業務日曆。

1. 對於「目錄服務組」清單中的每個項目，選擇一個日曆。
1. 按一下「儲存」。

## 導出和導入業務日曆 {#exporting-and-importing-business-calendars}

AEM forms可讓您將業務日曆匯出和匯入為XML檔案。 您可以使用此功能將日曆從測試系統移至生產系統。

>[!NOTE]
>
>此功能會匯出和匯入所有已定義的業務日曆，包括AEM表單提供的預設業務日曆。 與現有日曆同名的導入業務日曆將覆蓋現有日曆。

### 導出業務日曆 {#export-business-calendars}

1. 在管理控制台中，按一下「服務>表單工作流程>業務日曆」。
1. 按一下「導出」並保存XML檔案。

### 導入業務日曆 {#import-business-calendars}

1. 在管理控制台中，按一下「服務>表單工作流程>業務日曆」。
1. 按一下「匯入」。
1. 選擇包含導出的業務日曆的XML檔案，然後按一下「開啟」。

## 刪除業務日曆 {#delete-a-business-calendar}

您可以移除貴組織不再需要的任何業務日曆。 如果您刪除仍對應至使用者和群組的業務日曆，則會使用預設日曆。

1. 在管理控制台中，按一下「服務>Forms工作流程>業務日曆」。
1. 選取日曆。
1. 按一下刪除。
