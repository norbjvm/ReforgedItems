# ItemForge

## 🚀 Features

- **Modular Configuration**: Separate YAML files for weapons, armor, tools, and food
- **Custom Enchantment System**: Advanced enchantment effects via `enchantments.yml`
- **Event-Based Modification**: Automatic item processing on pickup, inventory changes, and spawn
- **Auto-Remodify**: Items are always updated according to the latest configuration
- **Creative Inventory Support**: Items taken from creative inventory are automatically modified
- **Command System**: Admin commands for reloading and force-remodifying items
- **Permission System**: Granular permissions for different commands

## 📋 Requirements

- **Server**: Paper 1.21.4+ (recommended)
- **Java**: Java 17 or higher
- **API Version**: 1.21

## 🛠️ Quick Start

### Installation

1. **Download**: Get the latest JAR from releases
2. **Install**: Place `itemforge-1.0.0.jar` in your `plugins/` folder
3. **Start**: Restart your server
4. **Configure**: Edit the generated YAML files in `plugins/ItemForge/`

## ⚙️ Configuration

The plugin uses modular YAML configuration files:

### Main Configuration (`config.yml`)
```yaml
general:
  enabled: true
  debug: false
  auto-save-interval: 5
  apply-on-join: true
  apply-on-pickup: true
  apply-on-inventory-click: true
  apply-on-spawn: true
  auto-remodify: true  # Always reprocess items with latest config

modifications:
  show-modification-lore: true
  lore-prefix: "&7[&bItemForge&7]"
  default-unbreakable: false
  preserve-vanilla-enchants: true
```

### Item Configuration Files

- **`weapons.yml`** - Weapon modifications (swords, axes, etc.)
- **`armor.yml`** - Armor modifications (helmet, chestplate, etc.)
- **`tools.yml`** - Tool modifications (pickaxes, shovels, etc.)
- **`food.yml`** - Food modifications (apples, golden apples, etc.)
- **`enchantments.yml`** - Custom enchantment effects and values

### Example Weapon Configuration
```yaml
weapons:
  diamond_sword:
    display_name: "&bDiamond Sword"
    lore:
      - "&7A powerful sword"
      - "&7Enhanced by ItemForge"
    attributes:
      generic_attack_damage: 8.0
      generic_attack_speed: 1.6
    enchantments:
      sharpness: 5
      unbreaking: 3
```

### Custom Enchantment System
```yaml
sharpness:
  damage_multiplier: 1.5
  special_effects:
    bleeding:
      levels:
        1:
          chance: 0.10
          duration: 40
        2:
          chance: 0.15
          duration: 60
```

## 📜 Commands

| Command | Permission | Description |
|---------|------------|-------------|
| `/itemforge reload` | `itemforge.reload` | Reload all configuration files |
| `/itemforge info` | `itemforge.info` | Show plugin information |
| `/itemforge remodifyall` | `itemforge.admin` | Force re-modify all items in all players' inventories |

## 🔐 Permissions

| Permission | Default | Description |
|------------|---------|-------------|
| `itemforge.admin` | `op` | Access to all commands |
| `itemforge.reload` | `op` | Reload configuration |
| `itemforge.info` | `true` | View plugin info |

## 🔧 Technical Details

### Event Handling
The plugin automatically modifies items on these events:
- **PlayerJoinEvent**: Process all items in player's inventory
- **EntityPickupItemEvent**: Modify items when picked up
- **InventoryClickEvent**: Modify items when moved in inventory
- **ItemSpawnEvent**: Modify items when they spawn in the world
- **InventoryCreativeEvent**: Modify items taken from creative inventory

### Data Storage
- Uses **PersistentDataContainer** for item tracking
- Maintains modification status without external databases
- Efficient memory usage with minimal overhead

### Auto-Remodify Feature
When `auto-remodify: true` is enabled:
- Items are always processed with the latest configuration
- Old modification tags are removed and reapplied
- Ensures consistency across server restarts

## 🐛 Troubleshooting
### Common Issues
**Plugin not loading:**
- Ensure you're using Paper 1.21.4+
- Check Java version (17+ required)
- Verify plugin.yml is present in JAR

**Items not modifying:**
- Check `general.enabled: true` in config.yml
- Verify item configurations in respective YAML files
- Enable debug mode for detailed logging

**Commands not working:**
- Check permissions
- Ensure you have the required permission nodes
- Try `/itemforge reload` to refresh configuration

### Debug Mode
Enable debug mode in `config.yml`:
```yaml
general:
  debug: true
```
This provides detailed logging for troubleshooting.

## 📝 Changelog
### Version 1.0.0
- Initial release
- Modular configuration system
- Custom enchantment system
- Auto-remodify feature
- Creative inventory support
- Comprehensive event handling
- Command system with permissions
