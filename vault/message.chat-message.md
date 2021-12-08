---
id: TC2DDp9795LJS0wkf4GkZ
title: Chat Message
desc: ''
updated: 1638909139469
created: 1638905264133
---

A **chat message** is a [[message]] sent in a [[chat]].

## API/JSON Representation
```ts
export interface APIChatMessage {
    attachments: APIAttachment[]; // See [1]
    avatar_url: string | null;
    created_at: number;
    favorited_by: [];
    conversation_id: string;
    id: string;
    name: string;
    sender_id: string;
    sender_type: "service" | "system" | "user";
    source_guid: string;
    recipient_id: string;
    text: string | null;
    user_id: string;
    event?: APIGroupEvent; // See [2]
    deleted_at?: number;
    deletion_actor?: "sender" | "system";
}
```
1. [[attachment]]
2. [[group.event]]

## Representation in `node-groupme`
