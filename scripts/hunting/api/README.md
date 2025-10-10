# API Reference

This section provides a comprehensive reference for all exports, events, and callbacks available in the Dusa Hunting System for developers who want to integrate or extend the script.

## API Documentation

The API is organized into three sections:

- **[Client-Side API](client.md)** - Client exports and events
  - Exports: `OpenMenu`, `UpdateQuestProgress`
  - Events: Menu, traps, binoculars, bait, laptop, license

- **[Server-Side API](server.md)** - Server exports, callbacks, and events
  - Exports: `addExperience`, `UpdateQuestProgress`, `reloadUITranslations`
  - Callbacks: Shop, selling, animals, quests, vehicles, cooking, traps
  - Events: Server-side triggers

- **[Shared Functions](shared.md)** - Shared utility functions
  - Weapon checks
  - Inventory images
  - Vehicle spawning
  - Vehicle keys

## Quick Reference

### Common Operations

**Add XP to Player** (Server):
```lua
exports['dusa_hunting']:addExperience(source, 50)
```

**Update Quest Progress** (Server):
```lua
exports['dusa_hunting']:UpdateQuestProgress(source, 'hunt', 'deer', 1)
```

**Open Hunting Shop** (Client):
```lua
exports['dusa_hunting']:OpenMenu()
```

**Get Player Level** (Server):
```lua
local level = lib.callback.await('hunting:server:getPlayerLevel', false)
```

**Sell Items** (Server):
```lua
local result = lib.callback.await('hunting:server:sellItems', false, itemsToSell)
```

## Integration Examples

See each API section for detailed integration examples:
- [Client Examples](client.md#integration-examples)
- [Server Examples](server.md#integration-examples)
- [Shared Examples](shared.md#usage-examples)

## Notes for Developers

1. **Quality System**: All meat items support quality levels (1-3)
   - Quality 1: Body shot
   - Quality 2: Leg shot
   - Quality 3: Headshot or trap kill

2. **Quest Types**:
   - `'hunt'` - Hunting animals
   - `'trap'` - Trapping animals
   - `'cook'` - Cooking meat

3. **Animal Types**: `deer`, `rabbit`, `bear`, `boar`, `coyote`, `mtlion`, `lion`, `oryx`, `antelope`, `redpanda`, `pig`

4. **Thread Safety**: All callbacks are thread-safe and can be called from any script

5. **Error Handling**: All exports and callbacks include built-in error handling - always check return values

## Support

For additional API support or feature requests, please contact the script author or join the support Discord.
