# Vanguard — WotLK AutoLogin

A minimal GlueXML modification for **World of Warcraft 3.3.5a** that lets you define a preferred character order on the character selection screen and cleans up the login UI by removing unused buttons.

## Features

- **Character order** — define your preferred character order in a simple config file; the first character in the list is automatically selected on login
- **UI cleanup** — removes Manage Account, Community Site, Credits, and Terms of Use buttons; repositions Options and Cinematics above Quit
- **No SavedVariables, no dependencies** — everything is controlled through a single `Config.lua` file
- **Credentials untouched** — login and password are handled normally by the client via `WTF/Config.wtf`

## Compatibility

- World of Warcraft **3.3.5a** (Wrath of the Lich King)
- Any private server running this client version

## Installation

> ⚠️ This mod replaces core GlueXML files. Back up the originals before installing.

1. Navigate to your WoW client folder
2. Create the folder `Data/Interface/GlueXML/`
3. Copy the following files with the ones from this repository:
   - `AccountLogin.lua`
   - `AccountLogin.xml`
4. Create the folder `Data/Interface/GlueXML/AutoLogin/`
5. Place `AutoLogin/Config.lua` inside it

Final structure:
```
Data/
  Interface/
    GlueXML/
      AccountLogin.lua
      AccountLogin.xml
      AutoLogin/
        Config.lua
```

## Configuration

Open `Data/Interface/GlueXML/AutoLogin/Config.lua` in any text editor:

```lua
AUTOLOGIN_CHAR_ORDER = {
    "CharacterOne",
    "CharacterTwo",
    "CharacterThree",
}
```

- Use **exact** character names (case-sensitive)
- The **first** character in the list is automatically selected on login
- Characters not listed appear at the end in their original order
- Set to `{}` to disable ordering

## How it works

Vanguard hooks into `UpdateCharacterList` and `UpdateCharacterSelection` — the native WoW functions responsible for rendering the character selection screen. When the character list loads, it reads `AUTOLOGIN_CHAR_ORDER` from the config file, sorts the display accordingly, and remaps button clicks to the correct real character indices on the server.

Because the WoW 3.3.5a Glue environment has no file write API (unlike SuperWoW on 1.12), the character order cannot be saved automatically from within the game. The config file must be edited manually.

## Uninstalling

Restore the original `AccountLogin.lua` and `AccountLogin.xml` from your client backup and delete the `AutoLogin/` folder.

## License

MIT
