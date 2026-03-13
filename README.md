# UPM

**UltraPluginManager (UPM)** is a modern, safe, and advanced plugin management system for Spigot servers (1.18.2+). It serves as a robust alternative to PlugMan, featuring a clean architecture, asynchronous operations, and a user-friendly GUI.

![Java](https://img.shields.io/badge/Java-17-orange) ![Spigot](https://img.shields.io/badge/Spigot-1.18.2-yellow) ![License](https://img.shields.io/badge/License-ARR-blue)

## ✨ Features

*   **Plugin Management:** Enable, Disable, Restart, Load, and Unload plugins dynamically.
*   **Modern GUI:** A chest-based GUI to manage plugins visually with pagination and status indicators.
*   **Safety First:**
    *   Prevents disabling critical plugins (e.g., Vault, ProtocolLib, WorldGuard).
    *   Checks for dependencies before disabling.
    *   Detects circular dependencies.
*   **Async Operations:** Heavy operations (like loading/unloading) are handled asynchronously to prevent server lag.
*   **Multi-Language Support:** Built-in support for English (`en`) and Hungarian (`hu`), with the ability to add custom language files.
*   **Tab Completion:** Full tab completion for all commands and file names.
*   **Hex Color Support:** Beautiful chat and GUI formatting with Hex color codes.

## 📥 Installation

1.  Ensure your server is running **Java 17** or newer.
2.  Download the `UPM.jar`.
3.  Place the jar file into your server's `plugins` folder.
4.  Restart the server.

## 🛠 Commands & Permissions

| Command | Alias | Description | Permission |
| :--- | :--- | :--- | :--- |
| `/upm` | | Shows the help menu. | `upm.admin` |
| `/upm list` | | Lists all plugins with their status. | `upm.list` |
| `/upm enable <plugin>` | | Enables a disabled plugin. | `upm.enable` |
| `/upm disable <plugin>` | | Disables an enabled plugin. | `upm.disable` |
| `/upm reload <plugin>` | | Reloads a specific plugin. | `upm.reload` |
| `/upm reload` | `areload` | Reloads the UPM configuration. | `upm.reload` |
| `/upm load <file>` | | Loads a jar file from the plugins folder. | `upm.load` |
| `/upm unload <plugin>` | | Unloads a plugin from memory (Use with caution). | `upm.unload` |
| `/upm info <plugin>` | | Shows detailed info (version, authors, deps). | `upm.info` |
| `/upm gui` | | Opens the Plugin Manager GUI. | `upm.gui` |
| `/upm debug` | | Toggles debug mode. | `upm.debug` |

**Wildcard Permission:** `upm.admin` grants access to all commands.

## ⚙️ Configuration

The `config.yml` allows you to customize the plugin's behavior.

```yaml
# Language setting (en, hu, or custom)
language: en

# Toggle debug messages in console
debug-mode: false

# GUI Title
gui-title: "&9&lUPM &8- &bPlugin Manager"

# Plugins that cannot be disabled/unloaded via UPM
protected-plugins:
  - "Vault"
  - "ProtocolLib"
  - "LuckPerms"
  - "WorldEdit"
  - "WorldGuard"
  - "UPM"
```

### Language Support
UPM generates `lang_en.yml` and `lang_hu.yml` by default. To create a new language:
1. Copy `lang_en.yml` and rename it (e.g., `lang_it.yml`).
2. Translate the messages.
3. Set `language: it` in `config.yml`.
4. Run `/upm reload`.

## ⚠️ Warning Regarding `unload` and `reload`

While UPM uses advanced techniques to unload plugins (closing ClassLoaders, clearing references), Java's architecture makes "clean" unloading difficult without a full server restart.

*   **Use `/upm reload` for development:** It is great for testing small changes in your own plugins.
*   **Avoid reloading complex plugins:** Plugins with heavy packet usage (ProtocolLib) or complex dependency injections may not reload cleanly.
*   **Memory Leaks:** Repeatedly loading/unloading plugins *can* lead to Metaspace memory leaks over time. **Always restart your server for production changes.**
