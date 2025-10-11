---
icon: gear-code
---

# Configuration

Welcome to the configuration guide for Dusa Hunting System. This section covers all configuration options available in the script.

## Configuration Files

The hunting system uses three main configuration files located in the `configurations/` folder:

* [**Shared Configuration**](shared.md) - `config_shared.lua`
  * Species definitions
  * Shop configuration
  * Quest system
  * Pet system
  * Vehicle rental
  * Keybinds
* [**Client Configuration**](client.md) - `config_client.lua`
  * Hunting zones
  * Animal AI settings
  * Tournament settings
  * Butchering areas
  * Vehicle carcass attachment
* [**Server Configuration**](server.md) - `config_server.lua`
  * Level system
  * Animal rewards
  * Quality-based bonuses
  * Cooking configuration

## Quick Links

* [Adding Custom Animals](client.md#adding-custom-animals)
* [Quest Configuration](shared.md#quest-configuration)
* [Shop Setup](shared.md#shop-configuration)
* [Hunting Zones](client.md#hunting-zones)
* [Reward System](server.md#animal-rewards)

## Important Notes

1. **Always backup** configuration files before making changes
2. **Test in TEST mode** first (`Shared.TEST = true`)
3. **Restart the server** after configuration changes
4. **Balance economy** carefully - consider your server economy
5. **Performance**: Limit `maxCount` in hunting zones to avoid lag

## Getting Started

Start with the [Shared Configuration](shared.md) to set up basic system settings, then move to [Client](client.md) and [Server](server.md) configurations.

***

## Database Setup

The hunting system uses the following database table:

```sql
CREATE TABLE IF NOT EXISTS `dusa_hunting` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `identifier` varchar(50) NOT NULL,
  `name` varchar(50) NOT NULL,
  `title` varchar(50) DEFAULT 'Avcı',
  `level` int(11) DEFAULT 1,
  `experience` int(11) DEFAULT 0,
  `shot` int(11) DEFAULT 0,
  `pet` varchar(50) DEFAULT NULL,
  `progress` int(11) GENERATED ALWAYS AS (`level` + `experience`) STORED,
  `created_at` timestamp NULL DEFAULT current_timestamp(),
  `updated_at` timestamp NULL DEFAULT current_timestamp() ON UPDATE current_timestamp(),
  PRIMARY KEY (`id`),
  UNIQUE KEY `identifier` (`identifier`),
  KEY `idx_identifier` (`identifier`),
  KEY `idx_progress` (`progress`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```

This table is automatically created on first resource start.

***

## Next Steps

* Review [API Reference](../api-reference.md) for integration
* Check [Common Issues](../common-issues.md) for troubleshooting
