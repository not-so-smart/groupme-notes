An **event** describes something that happens in a [[group]]. Events are emitted in special [[Messages|message]] sent by the system.

## API/JSON Representation
```ts
export interface APIEvent {
    type: string;
    data: Object;
}
```
The `data` field is an object describing the details of the event. The structure of this object changes depending on the event type. You can find a list of known event types and their corresponding data object structures below.

## Event types
This list is by no means exhaustive. It contains only the events that were observed in my groups whenever this list was made (circa mid-2021).

### Bots
- **`bot.add`** - _emitted when a bot is added to the group_
    - `user: User` - the user who added the bot
    - `bot: string` - the name of the added bot
- **`bot.del`** - _emitted when a bot is removed from the group_
    - `user: User` - the user who removed the bot
    - `bot: string` - the name of the removed bot
### Calendar
- **`calendar.event.created`** - _emitted when a calendar event is created_
    - `event: Object`
        - `id: string` - the ID of the calendar event
        - `name: string` - the name of the calendar event
    - `url: string` - a URL link to the calendar event
    - `user: UserWeird` - the user who created the event
- **`calendar.event.starting`** - _emitted when a calendar event is starting_
    - `event_name: string` - the name of the event
    - `minutes: string` - the number of minutes until the event begins
- **`calendar.event.user.going`** - _emitted when a user RSVPs to an event as "going"_
    - `event: Object`
        - `id: string` - the ID of the calendar event
        - `name: string` - the name of the calendar event
    - `user: UserWeird` - the user who RSVP'd
- **`calendar.event.user.not_going`** - _emitted when a user RSVPs to an event as "not going"_
    - `event: Object`
        - `id: string` - the ID of the calendar event
        - `name: string` - the name of the calendar event
    - `user: UserWeird` - the user who RSVP'd
- **`calendar.event.user.undecided`** - _emitted when a user removes their RSVP from an event_
    - `event: Object`
        - `id: string` - the ID of the calendar event
        - `name: string` - the name of the calendar event
    - `user: UserWeird` - the user who RSVP'd
### Group
- **`group.added_to_directory`** - _emitted when the group is added to a university directory_
    - `user: User` - the user who added the group to the directory
    - `directory_name` - the name of the directory
- **`group.avatar_change`** - _emitted when the group avatar is updated_
    - `user: User` - the user who changed the group avatar
    - `avatar_url: string` - the URL of the new avatar
- **`group.like_icon_set`** - _emitted when the group like icon is updated_
    - `user: User` - the user who updated the like icon
    - `like_icon: Object`
        - `pack_id: number`
        - `pack_index: number`
        - `type: string`
- **`group.name_change`** - _emitted when the group name is updated_
    - `user: User` - the user who updated the group name
    - `name: string` - the new name of the group
- **`group.office_mode_disabled`** - _emitted when office mode is disabled in the group_
    - `user: User` - the user who disabled office mode
- **`group.office_mode_enabled`** - _emitted when office mode is enabled in the group_
    - `user: User` - the user who enabled office mode
- **`group.role_change_admin`** - _emitted when the owner promotes a member to the admin role_
    - `user: User` - the user who initiated the change (the owner of the group)
    - `role: "admin"` - the role which was given (admin)
    - `member: User` - the member who received the role
- **`group.theme_change`** - _emitted when the group theme is updated_
    - `user: User` - the user who changed the theme
    - `theme_name` - the name of the new theme
- **`group.topic_change`** - _emitted when the group topic is updated_
    - `user: User` - the user who changed the topic
    - `topic: string` - the new topic for the group
- **`group.type_change`** - _emitted when the group type is updated_
    - `user: User` - the user who initiated the change
    - `type: "closed" | "private"` - the new group type
### Members
- **`membership.announce.added`** - _emitted when one or more users are added to the group by an existing member_
    - `added_users: User[]` - the user(s) who were added
    - `adder_user: User` - the member who added them
- **`membership.announce.joined`** - _emitted when a user joins the group from a share URL/token_
    - `user: User` - the user who joined
- **`membership.announce.rejoined`** - _emitted when a former member who previously exited on their own, rejoins the group using the former group rejoin endpoint (or the "archive" in-app)_
    - `user: User` - the user who rejoined
- **`membership.avatar_changed`** - _emitted when a member changes their avatar._ **[DEPRECATED]**
    - `user: User` - the member who changed their avatar
    - `avatar_url: string` - the new avatar
    - **NOTE:** "avatar" here refers to a member's per-group avatar, not their "primary" user avatar which is used across all of GroupMe. This is similar to the distinction between a member's nickname in a group and their "global" user name associated with their account.
    - **NOTE:** This event is **deprecated**. It can still be found historically in old messages but is no longer used and will not be emitted in the future.
- **`membership.nickname_changed`** - _emitted when a member's nickname is updated_
    - `user: User` - the member who changed their nickname
    - `name: string` - the new nickname for the member
- **`membership.notifications.autokicked`** - _emitted when an SMS user who had previously been added by an existing member using the SMS user's phone number, is autokicked (see membership states for more info)_
    - `user: User` - the member who was autokicked
- **`membership.notifications.exited`** - _emitted when a member leaves the group on their own_
    - `removed_user: User` - the member who left the group
- **`membership.notifications.removed`** - _emitted when a member is removed from the group by another member or admin_
    - `remover_user: User` - the member who removed the other member
    - `removed_user: User` - the member who was removed
### Message
- **`message.deleted`** - _emitted when a message is deleted_
    - `message_id: string` - the ID of the message
    - `deleted_at: number` - the timestamp when the message was deleted
    - `deletion_actor: "sender" | "system"` - the type of actor who deleted the message
    - `deleter_id: string` - the ID of the user who deleted the message
    - **NOTE:** `deleter_id` is always the message author ID, even if `deletion_actor` is set to `system`.
### Polls
- **`poll.created`** - _emitted when a poll is created_
    - `conversation: Object`
        - `id: string` - the ID of the group this poll was created in
    - `poll: Object`
        - `id: string` - the ID of the poll that was created
        - `subject: string` - the question or prompt for the poll
    - `user: UserWeird` - the user who created the poll
- **`poll.reminder`** - _emitted shortly before a poll expires_
    - `conversation: Object`
        - `id: string` - the ID of the group
    - `poll: Object`
        - `expiration: number` - the timestamp at which the poll will expire
        - `id: string` - the ID of the poll
        - `subject: string` - the question or prompt
- **`poll.finished`** - _emitted when a poll is ended_
    - `conversation: Object`
        - `id: string` - the ID of the group
    - `poll: Object`
        - `id: string` - the ID of the poll
        - `subject: string` - the question or prompt
    - `options: Object[]` - an array of `option` objects, each describing one option on the poll
        - `id: string` - the ID of this option (IDs start at 1 and are sequential)
        - `title: string` - the text of this option
        - `votes?: number` - the number of votes this option received (never zero; only present if the option received at least one vote)
        - `voter_ids?: string[]` - the IDs of the users who voted for this option (never empty; only present if the option received at least vote AND the poll visibility is set to `public`)
