A **chat** is a unique [[conversation]] between two [[Users|user]].

A chat represents a distinct relationship between exactly two users; any two users may have only one chat between them, and any chat may not include more than two users.

## API/JSON Representation
```ts
export interface APIChat {
    last_message: APIChatMessage; // See [1]
    message_deletion_mode: [
        "creator",
        "sender",
    ];
    message_deletion_period: number;
    messages_count: number;
    other_user: {
        id: string;
        name: string;
        avatar_url: string;
    };
    created_at: number;
    updated_at: number;
}
```
1. [[message]]

## Representation in `node-groupme`
https://groupme.js.org/classes/Chat