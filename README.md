# HA Sidebar Shortcuts

**English** | [Ελληνικά](README.el.md)

Puts the admin pages you use every day back in the Home Assistant sidebar, one click away:

| Item | Opens |
|---|---|
| Developer Tools | `/developer-tools/yaml` |
| Devices & Services | `/config/integrations/dashboard` |
| Automations & Scenes | `/config/automation/dashboard` |
| Apps | `/config/apps/installed` |
| Marketplace | `/marketplace` |

It is one configuration file for [Custom Sidebar](https://github.com/elchininet/custom-sidebar) that adapts by itself:

- **Admins only.** Administrators see the shortcuts. Other users keep their normal sidebar.
- **Automatic language.** Names follow each user's profile language. English and Greek are included, and [adding yours](#add-your-language) is one line per item. Missing languages fall back to English.
- **Only what exists.** "Apps" hides itself on installs without apps (Container/Core). "Marketplace" hides itself before Home Assistant 2026.11.

## Requirements

Check these before you install:

| Requirement | Why |
|---|---|
| Home Assistant **2026.8 or newer** (2026.11+ recommended) | Custom Sidebar v17 needs 2026.8+. The Marketplace item needs 2026.11+. |
| An **administrator** account | Only admins can install from the Marketplace and edit `configuration.yaml`. |
| **[Custom Sidebar](https://github.com/elchininet/custom-sidebar) v17 or newer** | This file is a configuration for that plugin. Without it nothing happens. |
| A way to **edit files** in `/config` | For example the File editor, Studio Code Server, Samba share or Terminal & SSH apps. |
| One **restart** of Home Assistant | The plugin is loaded with `extra_module_url`, which is only read at startup. |

## Install

### Step 1: Install Custom Sidebar

[![Open Custom Sidebar in your Home Assistant](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=elchininet&repository=custom-sidebar&category=plugin)

The button opens Custom Sidebar in your Marketplace (on Home Assistant 2026.10 or older, in HACS). Select **Install**.

Skip this step if Custom Sidebar is already installed.

### Step 2: Load Custom Sidebar on every page

Add this to `configuration.yaml`. If you already have a `frontend:` section, add only the `extra_module_url` part to it:

```yaml
frontend:
  extra_module_url:
    - /local/community/custom-sidebar/custom-sidebar-plugin.js
```

On Home Assistant 2026.10 or older with HACS, use `/hacsfiles/custom-sidebar/custom-sidebar-plugin.js` instead.

The Marketplace may also add Custom Sidebar as a dashboard resource. That alone is not enough: dashboard resources load only when a dashboard opens, while the sidebar needs the plugin on every page.

### Step 3: Download the configuration

[![Download custom-sidebar-config.yaml](https://img.shields.io/badge/Download-custom--sidebar--config.yaml-41BDF5?style=for-the-badge&logo=homeassistant&logoColor=white)](https://github.com/VeZReVouLiS/ha-sidebar-shortcuts/releases/latest/download/custom-sidebar-config.yaml)

Save it as **`/config/www/custom-sidebar-config.yaml`**. The name and folder must be exactly these, because Custom Sidebar only reads that path.

Already have a `custom-sidebar-config.yaml`? Don't overwrite it. Copy the items under `order:` from the downloaded file into your own.

### Step 4: Restart and refresh

1. Restart Home Assistant (**Settings** > the three dots menu > **Restart Home Assistant**).
2. Hard-refresh your browser (**Ctrl+F5**, or **Cmd+Shift+R** on Mac). In the companion app, use **Settings** > **Companion app** > **Debugging** > **Reset frontend cache**.

If the `www` folder did not exist before step 3, the restart in step 4 is what makes Home Assistant serve it.

## Add your language

All names are in one place at the top of the file, under `js_variables` > `trans`. Add one line with your language code under each item. For example, French:

```yaml
    developer_tools:
      en: 'Developer Tools'
      el: 'Εργαλεία προγραμματιστή'
      fr: 'Outils de développement'
```

The code is the first part of the language in your profile (`fr` for French, `de` for German, `pt` for both Portuguese variants). Items without your language show in English. Pull requests with new languages are welcome.

## Updates

This is a configuration file, so it doesn't update itself. To hear about new versions, select **Watch** > **Custom** > **Releases** at the top of this page. To update, download the file again (step 3) and refresh your browser. No restart is needed for updates.

The version you have is in the first line of the file.

## Uninstall

Delete `/config/www/custom-sidebar-config.yaml` and refresh your browser. To remove Custom Sidebar too, remove the `extra_module_url` line, uninstall it from the Marketplace and restart.

## Troubleshooting

| Problem | Fix |
|---|---|
| Nothing changes | Check that Custom Sidebar is in `extra_module_url` (step 2), then restart and hard-refresh. |
| Shortcuts missing for one user | They are for administrators only. Check the user under **Settings** > **People**. |
| Names are in English | The language comes from the user's profile (**Profile** > **Language**). Only languages listed in the file have their own names, see [Add your language](#add-your-language). |
| "Apps" is missing | Your installation has no apps (Home Assistant Container or Core). This is expected. |
| "Marketplace" is missing | Your Home Assistant is older than 2026.11. HACS still has its own sidebar item there. |

## Credits

Thanks to [elchininet](https://github.com/elchininet) for Custom Sidebar and for the idea of keeping all translations in one place.

## License

[MIT](LICENSE)
