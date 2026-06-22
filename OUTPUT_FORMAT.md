# Output Format

This document describes the **Output Format** your pipeline should produce. It is a simplified, platform-agnostic structure for archived messages.

The format is a **platform-agnostic** envelope for archived messages. A "message" is the generic unit of capture: depending on the platform it might be an email, a chat message, a social media post, and so on. The same structure is intended to work across any platform, so that archived content can be treated uniformly regardless of where it came from.

Part of this exercise is working out how the platform you are capturing maps onto this generic structure. The mapping is not always one-to-one, and there is often more than one reasonable way to model it.

---

## Concepts

- A **message** is the unit of capture, represented as a top-level record.
- Messages can be related to one another. A message that responds to another references the original via `message.reply_to_id`, which holds the `message_id` of the parent.
- A **context** groups related messages together (a conversation, thread, channel, or similar).
- The **author** of a message is the `sender`. Anyone the message is directed at is a `receiver`. Identifying information about a person lives on the `Account` object.
- **Reactions** capture responses to a message that aren't themselves messages (for example a like, an emoji reaction, or a similar lightweight acknowledgement).
- **Attachments** capture any media or files associated with a message.

---

## Top-level record

| Field       | Type             | Description                                                                     |
| ----------- | ---------------- | ------------------------------------------------------------------------------- |
| `platform`  | String           | The name of the platform the message was captured from.                         |
| `context`   | Context          | Information about the conversation/thread the message belongs to (see Context). |
| `sender`    | Account          | The account that authored the message (see Account).                            |
| `receivers` | Array of Account | The accounts the message was directed at. May be empty.                         |
| `message`   | Message          | The message itself (see Message).                                               |

---

## Context

| Field  | Type   | Description                                                                |
| ------ | ------ | -------------------------------------------------------------------------- |
| `id`   | String | Unique identifier for the conversation/thread the message belongs to.      |
| `name` | String | Human-friendly name for the conversation/thread. May be a templated value. |

---

## Account

Carries identifying information about a person on the platform.

| Field          | Type   | Description                                                                                                                                                   |
| -------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`           | String | Unique, stable identifier for the user on the platform.                                                                                                       |
| `name`         | String | The user's name or handle on the platform.                                                                                                                    |
| `display_name` | String | The user's display name, if the platform supports one.                                                                                                        |
| `friendly_id`  | String | The best available human-friendly identifier (e.g. email address, phone number, handle, or display name - falling back to the platform ID in the worst case). |

---

## Message

| Field            | Type                | Description                                                                                 |
| ---------------- | ------------------- | ------------------------------------------------------------------------------------------- |
| `message_id`     | String              | The platform-specific identifier for the message.                                           |
| `reply_to_id`    | String              | The `message_id` of the message this one replies to. Empty/omitted for a top-level message. |
| `content`        | String              | The text content of the message.                                                            |
| `mime`           | String              | The MIME type of the content. Typically `"text/plain"`.                                     |
| `sent_at`        | String              | When the message was created, in **RFC 3339** format, e.g. `2023-10-26T15:30:00Z`.          |
| `deleted_time`   | String \| null      | When the message was deleted, if applicable, in RFC 3339 format. `null` if not deleted.     |
| `attachments`    | Array of Attachment | Media/files attached to the message (see Attachment).                                       |
| `system_message` | Boolean             | `true` if generated by the platform rather than a user.                                     |
| `message_type`   | String              | A platform-defined label describing the kind of message.                                    |
| `reactions`      | Array of Reaction   | Reactions on the message (see Reaction).                                                    |

---

## Attachment

| Field         | Type    | Description                                                                                       |
| ------------- | ------- | ------------------------------------------------------------------------------------------------- |
| `file_name`   | String  | A unique filename for the attachment, including its file type, e.g. `412b-be39-5a86db143300.jpg`. |
| `source_name` | String  | The original name of the file, including its file type, e.g. `report.pdf`.                        |
| `mime_type`   | String  | MIME type of the attachment content.                                                              |
| `inline`      | Boolean | Whether the content was embedded in the message or attached separately.                           |

---

## Reaction

Captures a lightweight response to a message.

| Field            | Type    | Description                                          |
| ---------------- | ------- | ---------------------------------------------------- |
| `reaction_id`    | String  | The platform-specific identifier for the reaction.   |
| `reaction_value` | String  | The value of the reaction.                           |
| `message_id`     | String  | The `message_id` of the message that was reacted to. |
| `account`        | Account | The account that made the reaction (see Account).    |
| `sent_at`        | String  | When the reaction was made, in RFC 3339 format.      |

---

## Example JSON output

A single top-level message authored by `alice`, with one reply (a separate top-level record) and reactions on each. This example is platform-neutral; how a given platform's concepts map onto these fields is part of the exercise.

```json
[
  {
    "platform": "example_platform",
    "context": {
      "id": "ctx-0001",
      "name": "Conversation ctx-0001"
    },
    "sender": {
      "id": "user-alice",
      "name": "alice",
      "display_name": "Alice Anderson",
      "friendly_id": "alice"
    },
    "receivers": [],
    "message": {
      "message_id": "msg-0001",
      "reply_to_id": "",
      "content": "Hello world - this is the original message.",
      "mime": "text/plain",
      "sent_at": "2026-06-18T09:15:00Z",
      "deleted_time": null,
      "attachments": [
        {
          "file_name": "9f2c-4a1b-be39-5a86db143300.jpg",
          "source_name": "photo.jpg",
          "mime_type": "image/jpeg",
          "inline": false
        }
      ],
      "system_message": false,
      "message_type": "post",
      "reactions": [
        {
          "reaction_id": "react-0001",
          "reaction_value": "like",
          "message_id": "msg-0001",
          "account": {
            "id": "user-bob",
            "name": "bob",
            "display_name": "Bob Brown",
            "friendly_id": "bob"
          },
          "sent_at": "2026-06-18T09:20:00Z"
        }
      ]
    }
  },
  {
    "platform": "example_platform",
    "context": {
      "id": "ctx-0001",
      "name": "Conversation ctx-0001"
    },
    "sender": {
      "id": "user-bob",
      "name": "bob",
      "display_name": "Bob Brown",
      "friendly_id": "bob"
    },
    "receivers": [
      {
        "id": "user-alice",
        "name": "alice",
        "display_name": "Alice Anderson",
        "friendly_id": "alice"
      }
    ],
    "message": {
      "message_id": "msg-0002",
      "reply_to_id": "msg-0001",
      "content": "Nice - replying to the original message.",
      "mime": "text/plain",
      "sent_at": "2026-06-18T09:25:00Z",
      "deleted_time": null,
      "attachments": [],
      "system_message": false,
      "message_type": "reply",
      "reactions": [
        {
          "reaction_id": "react-0002",
          "reaction_value": "like",
          "message_id": "msg-0002",
          "account": {
            "id": "user-alice",
            "name": "alice",
            "display_name": "Alice Anderson",
            "friendly_id": "alice"
          },
          "sent_at": "2026-06-18T09:30:00Z"
        }
      ]
    }
  }
]
```
