# The Commands API

The most common and familiar way to interact with bots in Discord is through bot commands. These commands are sent by users to text channels and usually consist of a prefix, root command, and arguments. The most common prefixes include `!`, `/` and `=`. Modis also supports auxiliary arguments that modify the root argument, which are prefixed with `-`. A command with all four elements may look like `!play -loop despacito`.

Modis' internal commands API is designed to streamline the module code by collating the handling of bot commands into one central module (`!core`). The `!core` module then distributes the commands to their respective modules.

With the internal commands API, you don't need to worry about implementing parsing, permissions, or auxiliary arguments into your code. You only need to define what commands and arguments your module can receive (and their default permission levels if you want) in the `__info.py` file, which acts like a header file of sorts for your module. Then, you can use an `on_command.py` event handler the same way you would use any of the discord.py event handlers.

## Commands

Just like a header file, `__info.py` defines what methods your module is able to execute (commands), what variables it can take (auxiliary arguments), and what variables and constants it stores (database structure).

The internal commands API uses the `__info.py` file to add your module's commands to the list against which it will check each message received from Discord. The API will then call the `on_command.py` event handler in your module.

### Registering root commands
[text here]

### Receiving root commands
[text here]

## Auxiliary arguments

[text here]

### Registering aux arguments
[text here]

### Receiving aux arguments
[text here]

## Permissions

[text here]

### Registering default permissions
[text here]

#### Permission integers
Below is a table detailing how the permission integer affects the accessibility of that command:

| Integer | Accessible by                             |
| ------: | :---------------------------------------- |
|    `-1` | @everyone                                 |
|     `0` | Server owner only                         |
|     `1` | Server owner + highest role               |
|     `2` | Server owner + 2nd highest role and above |
|     `3` | Server owner + 3rd highest role and above |
|    `4+` | etc.                                      |

#### Permission strings
Below is a list of all the permission strings you can use to define what Discord permission a user needs to have to use a command:

| General Permissions     | Text Permissions       | Voice Permissions      |
| :---------------------- | :--------------------- | :--------------------- |
| `administrator`         | `send_messages`        | `connect`              |
| `view_audit_log`        | `send_tts_messages`    | `speak`                |
| `manage_server`         | `manage_messages`      | `mute_members`         |
| `manage_roles`          | `embed_links`          | `deafen_members`       |
| `manage_channels`       | `attach_files`         | `use_members`          |
| `kick_members`          | `read_message_history` | `use_voice_activity`   |
| `ban_members`           | `mention_everyone`     | `priority_speaker`     |
| `create_instant_invite` | `use_external_emojis`  |                        |
| `change_nickname`       | `add_reactions`        |                        |
| `manage_nicknames`      |                        |                        |
| `manage_emojis`         |                        |                        |
| `manage_webhooks`       |                        |                        |
| `view_channels`         |                        |                        |

## Upcoming features

We're always looking to improve Modis, and we have a couple things lined up for the commands API in the future:

* Auto-deleting of commands - specify for your module whether you want a command message to be auto-deleted once it's sent to keep the text channel clean, like the music module does.
    * The manager module will have functionality that lets you turn this on and off for modules through commands.
    * In the future we may add the ability to specify the option per-command and per-aux, in a similar fashion to permissions.
* Emoji button support like the music module; this would get a little more complex as we would need to work out the process involved in letting your module ask to have buttons created on a specific message. Join our [Discord](http://discord.gg/z83UGvK) to stay updated or suggest something!
