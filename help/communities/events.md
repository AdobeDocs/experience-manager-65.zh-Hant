---
title: 社區元件的OSGi事件
seo-title: OSGi Events for Communities Components
description: 發送可觸發非同步偵聽器的OSGi事件
seo-description: OSGi events are sent that can trigger asynchronous listeners
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
exl-id: 8049d797-e758-44c2-a89b-51d2b2fca8dc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 4%

---

# 社區元件的OSGi事件  {#osgi-events-for-communities-components}

## 概觀 {#overview}

當成員與社區功能交互時，會發送可觸發非同步偵聽器的OSGi事件，如通知或遊戲化（計分和標籤）。

元件 [社交事件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) 實例將事件記錄為 `actions` 發生在 `topic`。 SocialEvent包括返回 `verb` 與操作關聯。 有 *n-1* 關係 `actions` 和 `verbs`。

對於在發行版中提供的社區元件，下表描述了 `verbs` 定義 `topic` 可用。

## 主題和動詞 {#topics-and-verbs}

[日曆元件](calendar-basics-for-developers.md)
社交事件 `topic`= com/adobe/cq/social/calendar

| **動詞** | **說明** |
|---|---|
| POST | 成員建立日曆事件 |
| 新增 | 日曆事件上的成員注釋 |
| 更新 | 編輯成員的日曆事件或注釋 |
| 刪除 | 已刪除成員的日曆事件或注釋 |

[注釋元件](essentials-comments.md)
社交事件 `topic`= com/adobe/cq/social/comment

| **動詞** | **說明** |
|---|---|
| POST | 成員建立注釋 |
| 新增 | 成員對注釋的答復 |
| 更新 | 已編輯成員注釋 |
| 刪除 | 已刪除成員的注釋 |

[檔案庫元件](essentials-file-library.md)
社交事件 `topic`= com/adobe/cq/social/fileLibrary

| **動詞** | **說明** |
|---|---|
| POST | 成員建立資料夾 |
| 附加 | 成員上載檔案 |
| 更新 | 成員更新資料夾或檔案 |
| 刪除 | 成員刪除資料夾或檔案 |

[論壇元件](essentials-forum.md)
社交事件 `topic`= com/adobe/cq/social/forum

| **動詞** | **說明** |
|---|---|
| POST | 成員建立論壇主題 |
| 新增 | 成員對論壇主題的答復 |
| 更新 | 已編輯成員的論壇主題或回復 |
| 刪除 | 已刪除成員的論壇主題或答復 |

[日記帳元件](blog-developer-basics.md)
社交事件 `topic`= com/adobe/cq/social/journal

| **動詞** | **說明** |
|---|---|
| POST | 成員建立部落格 |
| 新增 | 對部落格的成員評論 |
| 更新 | 編輯成員的部落格或評論 |
| 刪除 | 已刪除成員的部落格或評論 |

[QnA元件](qna-essentials.md)
社交事件 `topic` = com/adobe/cq/social/qna

| **動詞** | **說明** |
|---|---|
| POST | 成員建立QnA問題 |
| 新增 | 成員建立QnA答案 |
| 更新 | 編輯成員的QnA問題或答案 |
| 選擇 | 已選擇成員的答案 |
| 取消選擇 | 已取消選擇成員的答案 |
| 刪除 | 刪除成員的QnA問題或答案 |

[審閱元件](reviews-basics.md)
社交事件 `topic`= com/adobe/cq/social/review

| **動詞** | **說明** |
|---|---|
| POST | 成員建立審閱 |
| 更新 | 已編輯成員的審閱 |
| 刪除 | 已刪除成員的審閱 |

[評級元件](rating-basics.md)
社交事件 `topic`= com/adobe/cq/social/tally

| **動詞** | **說明** |
|---|---|
| 添加評級 | 已對成員的內容進行分級 |
| 刪除評級 | 成員的內容已降級 |

[投票元件](essentials-voting.md)
社交事件 `topic`= com/adobe/cq/social/tally

| **動詞** | **說明** |
|---|---|
| 添加投票 | 成員的內容已被投票 |
| 刪除投票 | 成員的內容已被投票否決 |

**啟用裁決的元件**
社交事件 `topic`= com/adobe/cq/social/moderation

| **動詞** | **說明** |
|---|---|
| 拒絕 | 拒絕成員的內容 |
| 標誌不恰當 | 已標籤成員的內容 |
| 取消標籤為不適當 | 成員的內容已取消標籤 |
| 接受 | 成員的內容由版主批准 |
| 關閉 | 成員關閉編輯和回復的注釋 |
| 開啟 | 成員重新開啟注釋 |

## 自定義元件的事件 {#events-for-custom-components}

對於自定義元件， [SocialEvent抽象類](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) 必須擴展d以將元件的事件記錄為 `actions`發生在 `topic`。

自定義事件將覆蓋該方法 `getVerb()` 以便 `verb`返回 `action`。 的 `verb` 返回的操作可能是常用的(例如 `POST`)或專用於元件(例如 `ADD RATING`)。 有 *n-1* 關係 `actions`和 `verbs`。

>[!NOTE]
>
>確保自定義擴展註冊的等級低於產品中任何現有實現。

### 自定義元件事件的虛擬碼 {#pseudo-code-for-custom-component-event}

[org.osgi.service.event.Event](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);
[com.adobe.cq.social.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html);
[com.adobe.granite.activitystreams.ObjectTypes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html);
[com.adobe.granite.activitystreams.verbs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/Verbs.html);

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

## 用於篩選活動流資料的示例EventListener {#sample-eventlistener-to-filter-activity-stream-data}

可以偵聽事件以修改活動流中顯示的內容。

下面的虛擬碼示例將從活動流中刪除Comments元件的DELETE事件。

### EventListener的虛擬碼 {#pseudo-code-for-eventlistener}

需要 [最新功能包](deploy-communities.md#latestfeaturepack)。

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
