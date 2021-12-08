---
id: UfTK0Ggs4Dxy7lLZfveNO
title: Group
desc: ''
updated: 1638904160141
created: 1638477636926
---
Structurally, a **group** is an entity containing a single [[conversation]] and a collection of [[Members|member]].

Functionally, a **group** is a [[conversation]] between one or more [[Users|user]].

## API/JSON Representation

```ts
export interface APIGroup {
    name: string;
    id: string;
    group_id: string;
    description: string;
    image_url: string | null;
    creator_user_id: string;
    members: APIMember[] | null; // See [1]
    messages: {
        count: number;
        last_message_created_at: number | null;
        last_message_id: string | null;
        preview: {
            attachments: APIAttachment[]; // See [2]
            image_url: string | null;
            nickname: string | null;
            text: string | null;
            deleted_at?: number;
            deletion_actor?: "sender" | "system";
        };
    };
    type: "closed" | "private";
    requires_approval: boolean;
    show_join_question: boolean;
    join_question: null | {
        type: "join_reason/questions/text";
        text: string;
    };
    like_icon: null | {
        pack_id: number;
        pack_index: number;
        type: string;
    };
    message_deletion_mode?: [
        "creator",
        "sender",
    ];
    message_deletion_period?: number;
    muted_until?: number | null;
    office_mode: boolean;
    phone_number: string | null;
    share_qr_code_url: string | null;
    share_url: string | null;
    theme_name: string | null;
    max_members: number;
    max_memberships?: number;
    thread_id?: null;
    created_at: number;
    updated_at: number;
}
```
1. [[member]]
2. [[attachment]]

## Representation in `node-groupme`
https://groupme.js.org/classes/Group