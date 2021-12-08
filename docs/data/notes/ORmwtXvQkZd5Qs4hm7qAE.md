A **member** is an entity representing a single relationship between a [[user]] and a [[group]].

## API/JSON Representation
```ts
export interface APIMember {
    autokicked: boolean;
    id: string;
    image_url: string | null;
    muted: boolean;
    name: string;
    nickname: string;
    roles: MemberRole[];
    user_id: string;
}

export enum MemberRole {
    Admin = "admin",
    Owner = "owner",
    User = "user",
}
```

## Representation in `node-groupme`
https://groupme.js.org/classes/Member