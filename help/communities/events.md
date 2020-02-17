---
title: OSGi Events for Communities Components
seo-title: OSGi Events for Communities Components
description: 傳送OSGi事件，可觸發非同步監聽器
seo-description: 傳送OSGi事件，可觸發非同步監聽器
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# OSGi Events for Communities Components {#osgi-events-for-communities-components}

## 概覽 {#overview}

當成員與社群功能互動時，會傳送OSGi事件，可觸發非同步接聽程式，例如通知或遊戲化（計分和標籤）。

元件的 [SocialEvent例項會將](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html)`actions``topic`事件記錄為 SocialEvent包含傳回與動作相 `verb`關聯的方法。 和之 *間有* n- `actions`1關係 `verbs`。

對於發行版中提供的Communities元件，下表說明了每個可 `verbs`用元件 `topic`的定義。

## 主題和動詞 {#topics-and-verbs}

[行事歷元](calendar-basics-for-developers.md)件SocialEvent `topic`= com/adobe/cq/social/calendar

| **動詞** | **說明** |
|---|---|
| 貼文 | 成員建立日曆事件 |
| 新增 | 日曆事件上的成員注釋 |
| 更新 | 會編輯成員的日曆事件或注釋 |
| 刪除 | 會員的日曆事件或留言已刪除 |

[Comments Component](essentials-comments.md)SocialEvent `topic`= com/adobe/cq/social/comment

| **動詞** | **說明** |
|---|---|
| 貼文 | 成員建立注釋 |
| 新增 | 成員回覆評論 |
| 更新 | 已編輯成員的注釋 |
| 刪除 | 會員的注釋已刪除 |

[檔案庫元件](essentials-file-library.md)SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **動詞** | **說明** |
|---|---|
| 貼文 | 成員建立資料夾 |
| 附加 | 成員上傳檔案 |
| 更新 | 成員更新資料夾或檔案 |
| 刪除 | 成員刪除資料夾或檔案 |

[論壇元件](essentials-forum.md)SocialEvent `topic`= com/adobe/cq/social/forum

| **動詞** | **說明** |
|---|---|
| 貼文 | 成員建立論壇主題 |
| 新增 | 成員對論壇主題的回覆 |
| 更新 | 編輯成員的論壇主題或回覆 |
| 刪除 | 會員的論壇主題或回覆被刪除 |

[Journal Component](blog-developer-basics.md)SocialEvent `topic`= com/adobe/cq/social/journal

| **動詞** | **說明** |
|---|---|
| 貼文 | 成員建立部落格 |
| 新增 | 部落格文章中的成員注釋 |
| 更新 | 會編輯會員的部落格文章或留言 |
| 刪除 | 會員的部落格文章或留言已刪除 |

[QnA元件](qna-essentials.md)SocialEvent `topic` = com/adobe/cq/social/qna

| **動詞** | **說明** |
|---|---|
| 貼文 | 成員建立QnA問題 |
| 新增 | 成員建立QnA答案 |
| 更新 | 成員的QnA問題或答案已編輯 |
| 選擇 | 已選擇成員的答案 |
| 取消選擇 | 會員的答案為取消選擇 |
| 刪除 | 刪除成員的QnA問題或答案 |

[Reviews Component](reviews-basics.md)SocialEvent `topic`= com/adobe/cq/social/review

| **動詞** | **說明** |
|---|---|
| 貼文 | 成員建立審閱 |
| 更新 | 會員的審核已編輯 |
| 刪除 | 會員的審核已刪除 |

[評分元件](rating-basics.md)SocialEvent `topic`= com/adobe/cq/social/tally

| **動詞** | **說明** |
|---|---|
| 新增評分 | 會員的內容已被評級 |
| 移除評分 | 會員的內容已降級 |

[投票元件](essentials-voting.md)SocialEvent `topic`= com/adobe/cq/social/tally

| **動詞** | **說明** |
|---|---|
| 新增投票 | 會員的內容已通過投票 |
| 移除投票 | 會員的內容已被否決 |

**已啟用協調的元**&#x200B;件SocialEvent `topic`= com/adobe/cq/social/協調

| **動詞** | **說明** |
|---|---|
| 拒絕 | 會員的內容被拒絕 |
| 不適當的旗幟 | 會員的內容已標籤 |
| 取消標幟為不當 | 會員的內容已取消標幟 |
| 接受 | 會員的內容由協調者核准 |
| 關閉 | 成員關閉編輯和回覆的注釋 |
| 開啟 | 成員重新開啟注釋 |

## 自訂元件的事件 {#events-for-custom-components}

對於自訂元件， [SocialEvent抽象類別](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) ，必須加以擴充，才能將元件的事件記錄 `actions`為發生於的事件 `topic`。

自訂事件會覆寫方法， `getVerb()` 以便針對每個 `verb`事件傳回適當 `action`。 針 `verb` 對動作傳回的可能是常用(例如 `POST`)或專用於元件(例如 `ADD RATING`)。 和之 *間有* n- `actions`1關係 `verbs`。

>[!NOTE]
>
>確保自訂擴充功能的註冊排名低於產品中任何現有實作的排名。

### 自訂元件事件的偽程式碼 {#pseudo-code-for-custom-component-event}

[org.osgi.service.event.Event](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);[com.adobe.cq.sosical.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html);[com.adobe.granite.activitystreams.ObjectTypes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html);[com.adobe.granite.activitystreams.Verbs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/Verbs.html);

```java
package com.mycompany.recipe;

import org.osgi.service.event.Event;
import com.adobe.cq.social.scf.core.SocialEvent;
import com.adobe.granite.activitystreams.ObjectTypes;
import com.adobe.granite.activitystreams.Verbs;

/*
 * The Recipe type, passed to RecipeEvent(), would be a custom Recipe class
 * that extends either
 * com.adobe.cq.social.scf.SocialComponent
 * or
 * com.adobe.cq.social.scf.SocialCollectionComponent
 * See https://docs.adobe.com/docs/en/aem/6-2/develop/communities/scf/server-customize.html
 */

/**
 * Defines events that are triggered on a custom component, "Recipe".
 */
public class RecipeEvent extends SocialEvent<RecipeEvent.RecipeActions> {

    private static final long serialVersionUID = 1L;
    protected static final String PARENT_PATH = "PARENT_PATH";

    /**
     * The event topic suffix for Recipe events
     */
    public static final String RECIPE_TOPIC = "recipe";

    /**
     * @param recipe - the recipe resource on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final Recipe recipe, final String userId, final RecipeEvent.RecipeActions action) {
        String recipePath = recipe.getResource().getPath();
        String parentPath = (recipe.getParentComponent() != null) ?
                             recipe.getParentComponent().getResource().getPath() :
                             recipe.getSourceComponentId();
        this(recipePath, userId, parentPath, action);
    }

    /**
     * @param recipePath - the path to the recipe resource (jcr node) on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param parentPath - the path to the parent node of the recipe resource
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final String recipePath, final String userId, final String parentPath) {
        super(RECIPE_TOPIC, recipePath, userId, action,
              new BaseEventObject(recipePath, ObjectTypes.ARTICLE),
              new BaseEventObject(parentPath, ObjectTypes.COLLECTION),
              new HashMap<String, Object>(1) {
            private static final long serialVersionUID = 1L;
            {
                if (parentPath != null) {
                    this.put(PARENT_PATH, parentPath);
                }

            }
        });
    }

    private RecipeEvent (final Event event) {
      super(event);
    }

    /**
     * List of available recipe actions that can trigger a recipe event.
     */
    public static enum RecipeActions implements SocialEvent.SocialActions {
        RecipeAdded,
        RecipeModified,
        RecipeDeleted;

        @Override
        public String getVerb() {
            switch (this) {
                case RecipeAdded:
                    return Verbs.POST;
                case RecipeModified:
                    return Verbs.UPDATE;
                case RecipeDeleted:
                    return Verbs.DELETE;
                default:
                    throw new IllegalArgumentException("Unsupported action");
            }
        }
    }

}
```

## 篩選活動串流資料的範例EventListener {#sample-eventlistener-to-filter-activity-stream-data}

可以監聽事件，以修改活動串流中顯示的內容。

以下虛擬碼示例將從活動流中刪除「注釋」元件的DELETE事件。

### EventListener的虛擬碼 {#pseudo-code-for-eventlistener}

需要 [最新的功能套件](deploy-communities.md#latestfeaturepack)。

```java
package my.company.comments;

import java.util.Collections;
import java.util.Map;

import org.apache.commons.lang.StringUtils;
import org.apache.felix.scr.annotations.Activate;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Modified;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.osgi.PropertiesUtil;
import org.osgi.service.component.ComponentContext;

import com.adobe.cq.social.activitystreams.listener.api.ActivityStreamProviderExtension;
import com.adobe.cq.social.commons.events.CommentEvent.CommentActions;
import com.adobe.cq.social.scf.core.SocialEvent;

@Service
@Component(metatype = true, label = "My Comment Delete Event Filter",
        description = "Prevents comment DELETE events from showing up in activity streams")
public class CommentDeleteEventActivityFilter implements ActivityStreamProviderExtension {

    @Property(name = "ranking", intValue = 10)
    protected int ranking;

    @Activate
    public void activate(final ComponentContext ctx) {
        ranking = PropertiesUtil.toInteger(ctx.getProperties().get("ranking"), 10);
    }

    @Modified
    public void update(final Map<String, Object> props) {
        ranking = PropertiesUtil.toInteger(props.get("ranking"), 10);
    }

    @Override
    public boolean evaluate(final SocialEvent<?> evt, final Resource resource) {
        if (evt.getAction() != null && evt.getAction() instanceof SocialEvent.SocialActions) {
            final SocialEvent.SocialActions action = evt.getAction();
            if (StringUtils.equals(action.getVerb(), CommentActions.DELETED.getVerb())) {
                return false;
            }
        }
        return true;
    }

    @Override
    public Map<String, ? extends Object> getActivityProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public Map<String, ? extends Object> getActorProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String getName() {
        return "My Comment Delete Event Filter";
    }

    @Override
    public Map<String, ? extends Object> getObjectProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    /* Ensure a custom extension is registered with a ranking lower than any existing implementation in the product. */
    @Override
    public int getRanking() {
        return this.ranking;
    }

    @Override
    public Map<String, ? extends Object> getTargetProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String[] getStreamProviderPid() {
        return new String[]{"*"};
    }

}
```

