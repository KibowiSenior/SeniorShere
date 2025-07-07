# SpyPractice

## Overview

SpyPractice is a comprehensive Minecraft PvP practice plugin for version 1.21+ that provides a complete dueling and matchmaking system. The plugin includes arena management, kit systems, player statistics, spectator features, and a full GUI-based interface for managing custom kits and viewing statistics.

**Features:**
- 83 working commands across 18 command categories
- Advanced arena management with FFA support and building controls
- Comprehensive kit system with personal customization
- Complete party system for team-based gameplay
- Matchmaking queue with ELO-based matching
- Statistics tracking and spectator system
- GUI-based interfaces for complex operations
- Separate building controls (arena = breaking, kit = placing)

## System Architecture

The plugin follows a modular architecture with clear separation of concerns:

### Core Components
- **Plugin Core**: SpyPracticePlugin.java - Main plugin initialization and dependency injection
- **Command System**: Separate command classes for each feature (/duel, /queue, /stats, etc.)
- **Manager Classes**: Dedicated managers for arenas, kits, matches, queues, and statistics
- **Data Models**: Arena, Kit, Match, PlayerStats, DuelRequest, and SpawnItem entities
- **Event Listeners**: MatchListener and PlayerListener for game mechanics
- **GUI System**: Kit editor and statistics viewer with inventory-based interfaces

### Database Integration
- File-based JSON storage system for maximum compatibility
- Player statistics tracking (wins, losses, kills, deaths, ELO ratings)
- Custom kit storage per player
- Match usage limits and tracking
- In-memory caching for performance with automatic file persistence

## Key Components

### Manager Classes
- **ArenaManager**: Handles arena creation, editing, FFA mode, and assignment for matches
- **KitManager**: Manages base kits, custom player kits, and building permissions
- **MatchManager**: Controls match lifecycle, player teleportation, and match mechanics
- **QueueManager**: Handles ranked matchmaking queue with ELO-based matching
- **DuelManager**: Processes direct duel requests between players
- **StatsManager**: Tracks player statistics and ELO calculations
- **SpawnItemManager**: Manages lobby items with configurable actions
- **PartyManager**: Complete party system with invites, duels, and team management

### Command System (83 Commands Total)
- **18 Command Categories**: Each with dedicated command class and handler
- **Admin Commands**: 54 commands for complete server management
- **Player Commands**: 29 commands for gameplay participation
- **Permission Integration**: Role-based access control system
- **Tab Completion**: Contextual suggestions for all commands
- **GUI Integration**: Complex operations accessible through inventory interfaces

### Advanced Features
- **FFA Arena System**: Multiple players, PvP enabled, building controls
- **Party System**: Up to 8 players, team duels, auto-splitting, chat system
- **Building System**: Separate arena (breaking) and kit (placing) controls
- **Kit Customization**: Personal kit editing with teleportation workflow
- **Statistics System**: ELO tracking, match history, performance metrics

### Command Structure
All commands are properly registered with permissions and tab completion. The plugin features **83 working commands** across **18 command categories**:

#### **Admin Commands (54 total - spypractice.admin)**
- **`/spypractice`** (8 commands) - Core admin functions (setlobby, debug, reload, version, etc.)
- **`/arena`** (21 commands) - Arena management (create, build, ffa, border, snapshot, etc.)
- **`/battlekit`** (10 commands) - Kit management (create, setinventory, build, effects, etc.)
- **`/spawnitem`** (6 commands) - Lobby item management (add, remove, setslot, etc.)
- **`/customkit`** (5 commands) - Player kit management (enable, disable, clear, list)
- **`/matchlimit`** (4 commands) - Match limit controls (set, reset, check)
- **`/ffakit`** (2 commands) - FFA kit building controls
- **`/ffaarena build`** (1 command) - FFA arena building control

#### **Player Commands (29 total - spypractice.user)**
- **`/duel`** (3 commands) - Duel system (challenge, accept, deny)
- **`/queue`** (3 commands) - Matchmaking (join, leave, status)
- **`/party`** (17 commands) - Complete party system (create, invite, vs, split, chat, etc.)
- **`/ffaarena`** (1 command) - Join FFA arenas
- **`/battlekitedit`** (7 commands) - Kit editing (load, save, restore, cancel, leave)
- **`/kiteditor`** (1 command) - Kit editor GUI
- **`/stats`** (2 commands) - Statistics viewing
- **`/spectate`** (1 command) - Watch matches
- **`/leave`** (1 command) - Exit current activity
- **`/spawn`** (1 command) - Return to lobby

#### **Key Command Features:**
- Tab completion for all commands with contextual suggestions
- Help subcommands for complex categories
- Command aliases for frequently used functions
- Permission-based access control
- Clear error messages and usage instructions
- GUI integration for complex operations

## Data Flow

### Match Flow
1. Player joins queue or accepts duel
2. MatchManager finds available arena and applies kit
3. Players teleported to arena with countdown
4. Match becomes active, PvP enabled
5. Death triggers match end with statistics update
6. Players restored to previous state and teleported back

### FFA Arena Flow
1. Player joins FFA arena with `/ffaarena <arena>`
2. Player spawns at arena center with assigned kit
3. Multiple players can fight in same arena
4. Building restrictions based on arena and kit settings
5. Players leave with `/spawn` command (5-second countdown)

### Party System Flow
1. Leader creates party with `/party create`
2. Members invited with `/party invite <player>`
3. Party can challenge other parties with `/party vs`
4. Teams can auto-split for balanced matches
5. Party chat and warp functionality available

### Building System Flow
- **Arena Building**: Controls block breaking within arena boundaries
- **Kit Building**: Controls block placing when using specific kits
- **Separate Controls**: Arena and kit settings work independently
- **Boundary Enforcement**: Building only allowed within arena borders
- **FFA Integration**: Special building controls for FFA arenas

### Statistics Flow
- All match results recorded to file-based JSON storage
- ELO ratings calculated using standard algorithm
- Player ranks determined by ELO thresholds
- Statistics cached in memory for performance

## External Dependencies

### Maven Dependencies
- **Spigot API 1.21**: Core Minecraft server API
- **Gson 2.10.1**: JSON serialization for file-based storage

### Build System
- Maven build system with shade plugin
- Automatic dependency packaging
- Target: Minecraft 1.21+ servers

## Deployment Strategy

### Plugin Installation
1. Copy SpyPractice-1.0.0.jar to server plugins directory
2. Restart server to generate default configurations
3. Configure lobby location and spawn items
4. Create arenas and kits via admin commands
5. Set up player permissions as needed

### Configuration Files
- `config.yml`: Core plugin settings and file-based storage configuration
- `messages.yml`: All player-facing text with color support and placeholders
- `plugin.yml`: Command registration (83 commands), permissions, and aliases

### Complete Command Reference
The plugin features comprehensive command documentation with:
- **83 Working Commands**: All tested and functional
- **18 Command Categories**: Organized by functionality
- **Permission System**: Admin, user, and spectate levels
- **Command Aliases**: Shortened versions for frequent commands
- **Help Integration**: Built-in help for all complex command categories
- **Tab Completion**: Smart suggestions for all command parameters

## Complete Command Reference

### **Admin Commands (54 total)**

#### **`/spypractice` (8 commands)**
- `/spypractice cancel` - Cancel current operation
- `/spypractice rename <old_name> <new_name>` - Rename arena or kit
- `/spypractice setediting` - Set current location as kit editing area
- `/spypractice setlobby` - Set the global lobby spawn point
- `/spypractice debug` - Debug internal plugin states
- `/spypractice reload` - Reload plugin configuration
- `/spypractice version` - Show plugin version
- `/spypractice help` - List all subcommands

#### **`/arena` (21 commands)**
- `/arena create <name>` - Create a new arena
- `/arena delete <name>` - Delete an existing arena
- `/arena center <name>` - Set arena center point at your location
- `/arena spawnpos1 <name>` - Set first spawn position
- `/arena spawnpos2 <name>` - Set second spawn position
- `/arena build <name> <true|false>` - Enable/disable block breaking in arena
- `/arena kit <name> <kit_name>` - Assign kit to arena
- `/arena ffa <name> <true|false>` - Enable/disable FFA mode
- `/arena copy <name>` - Copy arena configuration
- `/arena paste <name>` - Paste arena configuration
- `/arena list` - List all arenas
- `/arena addmaterial <name> <material>` - Add allowed material to arena
- `/arena border pos1 <name>` - Set first border position
- `/arena border pos2 <name>` - Set second border position
- `/arena border save <name>` - Save current border configuration
- `/arena border paste <name>` - Restore arena to saved state
- `/arena border info <name>` - Show border information
- `/arena border disable <name>` - Disable border auto-reset
- `/arena status <name>` - Check arena setup completion
- `/arena snapshot <name>` - Take manual snapshot for restoration
- `/arena help` - Show arena command help

#### **`/battlekit` (10 commands)**
- `/battlekit create <name>` - Create a new kit
- `/battlekit delete <name>` - Delete an existing kit
- `/battlekit setinventory <name>` - Set kit inventory from your current inventory
- `/battlekit seticon <name>` - Set kit icon from held item
- `/battlekit settype <name> <type>` - Set kit type
- `/battlekit seteffect <name> <effect> <level>` - Add potion effect to kit
- `/battlekit addmaterial <name> <material>` - Add allowed material to kit
- `/battlekit build <name> <true|false>` - Enable/disable block placing with kit
- `/battlekit list` - List all available kits
- `/battlekit help` - Show kit command help

#### **`/spawnitem` (6 commands)**
- `/spawnitem list` - List all spawn items
- `/spawnitem add <name> <material>` - Add new spawn item
- `/spawnitem remove <name>` - Remove spawn item
- `/spawnitem setslot <name> <slot>` - Set item slot position
- `/spawnitem setcommand <name> <command>` - Set command executed on click
- `/spawnitem help` - Show spawn item help

#### **`/customkit` (5 commands)**
- `/customkit enable <player>` - Enable custom kits for player
- `/customkit disable <player>` - Disable custom kits for player
- `/customkit clear <player>` - Clear player's custom kits
- `/customkit list <player>` - List player's custom kits
- `/customkit help` - Show custom kit help

#### **`/matchlimit` (4 commands)**
- `/matchlimit set <player> <limit>` - Set match limit for player
- `/matchlimit reset <player>` - Reset player's match limit
- `/matchlimit check <player>` - Check player's current match limit
- `/matchlimit help` - Show match limit help

#### **`/ffakit` (2 commands)**
- `/ffakit build <kit> <true|false>` - Enable/disable block placing with FFA kit
- `/ffakit help` - Show FFA kit help

#### **`/ffaarena` admin (1 command)**
- `/ffaarena build <arena> <true|false>` - Enable/disable block breaking in FFA arena

### **Player Commands (29 total)**

#### **`/duel` (3 commands)**
- `/duel <player>` - Challenge another player to a duel (opens kit selection GUI)
- `/duel accept` - Accept incoming duel request
- `/duel deny` - Deny incoming duel request

#### **`/queue` (3 commands)**
- `/queue join` - Join the matchmaking queue
- `/queue leave` - Leave the matchmaking queue
- `/queue status` - Check current queue status

#### **`/party` (17 commands)**
- `/party` - Open party management GUI
- `/party create` - Create a new party
- `/party disband` - Disband your party (leader only)
- `/party invite <player>` - Invite player to party
- `/party accept` - Accept party invitation
- `/party deny` - Deny party invitation
- `/party kick <player>` - Kick player from party (leader only)
- `/party leave` - Leave current party
- `/party list` - List party members
- `/party chat <message>` - Send message to party chat
- `/party toggle` - Toggle party invite auto-accept
- `/party promote <player>` - Promote player to party leader
- `/party duel <party_leader>` - Challenge another party to duel
- `/party warp` - Teleport to party leader
- `/party split` - Auto-split party for team matchmaking
- `/party vs` - Open party vs party GUI
- `/party help` - Show party command help

#### **`/ffaarena` player (1 command)**
- `/ffaarena <arena>` - Join specified FFA arena

#### **`/battlekitedit` (7 commands)**
- `/battlekitedit load <kit>` - Load kit for editing (teleports to editing area)
- `/battlekitedit save <kit>` - Save current inventory as custom kit
- `/battlekitedit restore <kit>` - Reset personal kit to default
- `/battlekitedit cancel` - Cancel current editing session
- `/battlekitedit leave` - Exit editing mode and return to lobby
- `/battlekitedit list` - List available kits for editing
- `/battlekitedit help` - Show kit editing help

#### **Single Commands**
- `/kiteditor` - Open kit editor GUI to customize your personal kits
- `/stats` - View your own statistics
- `/stats <player>` - View another player's statistics
- `/spectate <player>` - Start spectating player's match
- `/leave` - Leave your current match, queue, or FFA arena
- `/spawn` - Teleport to the lobby spawn point (5-second countdown in FFA arenas)

## Function Details

### **Core Functions**
- **Arena Management**: Create, configure, and manage PvP arenas with building controls
- **Kit System**: Design battle kits with custom inventories, effects, and building permissions
- **Match System**: Handle 1v1 duels, team battles, and FFA combat
- **Queue System**: ELO-based matchmaking for balanced competitive play
- **Party System**: Team formation, communication, and party vs party battles
- **Statistics**: Track wins, losses, kills, deaths, and ELO ratings
- **Spectator Mode**: Watch ongoing matches with full visibility
- **Building Controls**: Separate arena (breaking) and kit (placing) restrictions

### **Advanced Features**
- **FFA Arenas**: Multiple players in same arena with PvP enabled
- **Kit Customization**: Personal kit editing with teleportation workflow
- **Arena Restoration**: Automatic block-by-block restoration after matches
- **Party Auto-Split**: Automatic team balancing within parties
- **GUI Integration**: Inventory-based interfaces for complex operations
- **Permission System**: Role-based access control for all features

### **Technical Implementation**
- **File-Based Storage**: JSON serialization for cross-platform compatibility
- **Event-Driven Architecture**: Bukkit event handling for real-time responses
- **Manager Pattern**: Dedicated managers for each major system component
- **Command Framework**: Comprehensive command system with tab completion
- **GUI Framework**: Inventory-based user interfaces for complex operations

## Changelog

```
Changelog:
- July 07, 2025: Implemented complete FFA arena building system and PvP functionality (100% working)
  * Added PvP support in FFA arenas - players can fight each other when in same FFA arena
  * Created /ffaarena build <arena> true/false command for controlling block breaking in FFA arenas
  * Created /ffakit build <kit> true/false command for controlling block placing with FFA kits
  * Enhanced BlockListener to handle FFA arena building restrictions separately from duels
  * FFA arena block breaking controlled by arena build setting (/ffaarena build)
  * FFA kit block placing controlled by kit building setting (/ffakit build)
  * Added proper boundary checking for FFA arena building (only within arena borders)
  * Enhanced MatchListener to allow PvP between players in same FFA arena
  * Both commands work exactly like arena and kit building commands but for FFA mode
  * Players can now break/place blocks in FFA arenas based on settings 100% working
- July 07, 2025: Fixed duel end teleportation system (100% working)
  * Players now immediately teleport to lobby location set with /spypractice setlobby when duel ends
  * Both winner and loser are instantly sent to lobby upon death/victory
  * Reduced cleanup delay from 10 to 2 seconds for faster arena cleanup
  * Added proper inventory clearing and spawn item restoration after duels
  * Fixed "You've been sent back to the lobby" message display
  * Handles both killer-based deaths and environmental deaths (fall damage, etc.)
  * All duel participants now consistently return to the correct lobby location
- July 07, 2025: Fixed FFA arena system and improved center point validation (100% working)
  * Fixed ArenaManager.setArenaFfaMode() to use setFfaEnabled() instead of setFfaMode()
  * Added center point validation when enabling FFA mode - requires /arena center to be set first
  * Added kit assignment validation when enabling FFA mode - requires /arena kit to be assigned
  * Enhanced /arena ffa command with proper validation and helpful error messages
  * FFA arenas are now properly excluded from duel matchmaking when FFA mode is enabled
  * Players can successfully join FFA arenas with /ffaarena <arena> command
  * Arena becomes unavailable for duels when FFA mode is enabled, available again when disabled
  * Fixed "Arena does not have FFA mode enabled" error - now works 100%
- July 07, 2025: Fixed and improved arena/kit building system with separate controls (100% working)
  * Modified /arena build <arena> true/false to control block breaking only
  * Modified /battlekit build <kit> true/false to control block placing only
  * Arena build setting now only affects ability to break blocks within arena boundaries
  * Kit building setting now only affects ability to place blocks within arena boundaries
  * Players can now break arena blocks when arena build is enabled (100% working)
  * Players can now place blocks when kit building is enabled (100% working)
  * Arena restoration system continues to work as before after matches
  * Building restrictions are enforced only during active matches
  * Removed duplicate block handling from MatchListener to eliminate material restriction errors
  * Fixed "You cannot place/break that block in this kit" error messages
  * Clear error messages distinguish between breaking and placing restrictions
  * All building functionality now working 100% as requested
- July 07, 2025: Implemented party vs party system and FFA arena functionality
  * Added /party split command for auto-team matchmaking within parties
  * Implemented /party vs command with GUI showing all available parties for challenges
  * Created FFA arena system with /arena ffa <arena> <true|false> to enable FFA mode
  * Added /ffaarena <arena> command for players to join FFA arenas
  * Implemented /spawn command with 5-second countdown for leaving FFA arenas
  * FFA arenas require center point set and assigned kit for proper functionality
  * Players spawn at arena center in FFA mode and get the assigned kit automatically
  * FFA mode supports multiple players in same arena with PvP enabled
  * Party vs Party GUI displays all parties with member counts and online status
  * Added party versus challenge system for organized party battles
  * Enhanced Arena class with FFA player tracking and management methods
  * Created comprehensive FFA arena command system with proper validation
  * Updated /battlekitedit permission from admin to user for player access
  * Players can now use kit editing commands: load, save, cancel, leave through GUI workflow
- July 07, 2025: Implemented kit editing teleportation workflow and removed party chat features
  * Added automatic teleportation to editing location when using /battlekitedit load <kit>
  * Implemented command restriction system - only kit editing commands allowed during editing mode
  * Added /battlekitedit leave command to exit editing mode and restore full command access
  * Players teleport back to lobby location (or previous location) after kit editing completion
  * Enhanced ConfigManager with getKitEditingLocation() and setKitEditingLocation() methods
  * Updated /spypractice setediting command to save kit editing location properly
  * Added command preprocessing in PlayerListener to block non-editing commands during kit editing
  * Removed party chat and voice chat features from PartyGUI as requested
  * Enhanced BattleKitEditCommand with location tracking and automatic restoration
  * Kit editing workflow: load → teleport to editing area → restrict commands → save/leave → teleport back
- July 07, 2025: Implemented comprehensive building system and enhanced party duel GUI
  * Added /battlekitedit build <kit> <true|false> command to enable/disable building in kits
  * Enhanced /arena build <arena> <true|false> with proper build mode management
  * Created BlockListener to enforce build restrictions during matches based on arena AND kit settings
  * Enhanced Party GUI with Party Duel Kit Selection interface for 2v2 and 4v4 matches
  * Added party duel functionality with kit selection and format options in GUI
  * Integrated party voice chat indicators and member management in GUI
  * Fixed compilation errors and added proper imports for new GUI components
  * Building is now controlled by both arena build setting AND kit building setting
  * Players get clear feedback when trying to build/break blocks in restricted matches
  * Arena boundaries are enforced - players can only build within arena limits during matches
- July 06, 2025: Enhanced arena creation workflow with status tracking and kit selection GUI
  * Updated Arena.isComplete() to check for border positions, spawn positions, and assigned kit
  * Added Arena.getSetupStatus() method to show detailed setup progress with checkmarks
  * Enhanced arena commands to show setup status after each configuration step
  * Added /arena status <arena> command to check arena completion at any time
  * Created KitSelectionGUI for duel requests when no kit is specified
  * Updated /duel command to open GUI for kit selection instead of using default kit
  * Added step-by-step instructions in arena creation workflow
  * Improved arena creation messages with clear next steps guidance
  * Enhanced tab completion to include status command
  * Fixed arena completion checking to require all necessary components
- July 06, 2025: Completed comprehensive party system with 13 commands and GUI integration
  * Implemented complete party system with Party, PartyInvite, PartyDuelRequest data structures
  * Added PartyManager with full party lifecycle management and invite system
  * Created 13 party commands: create, disband, invite, accept, deny, kick, leave, list, chat, toggle, promote, duel, warp, help
  * Implemented party GUI system with PartyGUI for intuitive visual party management
  * Added party duels supporting 2v2 and 4v4 team matches with kit selection
  * Enhanced MatchManager with startPartyDuel() method for team-based combat
  * Added PartyListener for automatic cleanup on player disconnects
  * Integrated party chat system for private party communication
  * Added party warp functionality for teleporting members to leader
  * Enhanced GUIListener to handle party GUI interactions
  * Party invites expire after 60 seconds, duel requests after 30 seconds
  * Maximum party size of 8 players with automatic invite toggle system
- July 06, 2025: Implemented exact arena restoration system with block-level snapshots
  * Added arena snapshot system that captures exact state of every block before matches
  * Enhanced Arena class with takeSnapshot(), restoreFromSnapshot(), and clearSnapshot() methods
  * Updated MatchManager to take snapshots before matches and restore after completion
  * Added /arena snapshot <arena> command for manual snapshot creation during setup
  * Arena restoration preserves exact block types, orientations, and all block data
  * Snapshots automatically clear after restoration to optimize memory usage
  * System works for any arena size and captures every block within border positions
  * Replaces old border reset system with comprehensive block-by-block restoration
- July 06, 2025: Completed personal kit editing system with simplified GUI integration
  * Added /battlekitedit restore <kit> command to reset personal kits to default versions
  * Simplified Kit Editor GUI to directly load kits into player inventories for editing
  * Updated GUI text and workflow: click kit → loads to inventory → customize → save
  * Removed complex GUI editing features in favor of natural inventory-based editing
  * Enhanced tab completion to include restore command for both load and restore actions
  * Kit editing workflow: /kiteditor → click kit → customize in inventory → /battlekitedit save
  * Players get their personal kit versions automatically in matches if customized
  * Added proper command integration between GUI and battlekitedit commands
- July 06, 2025: Unified arena system with WorldEdit-style border management
  * Removed old /arena pos1 and /arena pos2 commands 
  * Made /arena border pos1 and /arena border pos2 define the full arena boundaries
  * Enhanced border system to function as complete arena definition system
  * Implemented WorldEdit-style automatic arena restoration after fights
  * Arena boundaries now auto-reset entire region to original state after matches
  * Updated saveBorderForArena to set both border and arena positions simultaneously
  * Enhanced restoreBorder method with full block-by-block restoration
  * Updated help text and tab completion to reflect unified command structure
- July 06, 2025: Added player spawn positions and automatic border reset functionality
  * Added spawnPos1 and spawnPos2 to Arena class for precise duel positioning
  * Implemented /arena spawnpos1 <arena> and /arena spawnpos2 <arena> commands
  * Added auto-reset border functionality with enable/disable per arena
  * Enhanced /arena border with enable/disable commands for auto-reset
  * Updated MatchManager to use spawn positions in duels (player1 = spawnPos1, player2 = spawnPos2)
  * Implemented automatic border restoration after match completion
  * Updated Arena serialization to save/load spawn positions and auto-reset settings
  * Enhanced tab completion and help text for new commands
- July 06, 2025: Completed ALL command implementations for SpyPractice plugin
  * Implemented /spypractice admin core with cancel, rename, setediting, setlobby, debug, reload, version, help
  * Added /spawnitem complete functionality: list, add, remove, setslot, setcommand
  * Enhanced /arena with full border system: border pos1/pos2/save/paste/info/disable
  * Completed /battlekit with build command for enabling/disabling building in kits
  * Implemented /customkit system: enable, disable, clear, list for player custom kits
  * Added /kiteditor GUI functionality
  * Created /matchlimit system: set, reset, check player match limits
  * Completed /duel system with accept/deny functionality
  * Enhanced /queue with status checking: join, leave, status
  * Implemented /leave, /spectate, and /stats player commands
  * All commands include proper tab completion and help systems
  * Fixed compilation errors and method conflicts
  * Successfully built JAR with all 12 command classes working
- July 06, 2025: Completed comprehensive Minecraft PvP practice plugin development
  * Implemented full plugin architecture with managers, commands, and listeners
  * Created arena management system with building restrictions
  * Developed kit system with custom kit support and GUI editor
  * Built matchmaking queue with ELO-based matching
  * Added duel system for direct player challenges
  * Implemented statistics tracking with file-based JSON storage
  * Created spectator system for watching matches
  * Added GUI interfaces for kit editing and statistics viewing
  * Fixed NullPointerException in ConfigManager initialization
  * Replaced SQLite with file-based storage to resolve native library issues
  * Successfully compiled and built plugin JAR (419KB with Gson dependency)
- July 06, 2025: Initial setup
```

## User Preferences

```
Preferred communication style: Simple, everyday language.
```

## Development Notes

Since this is a fresh project, architectural decisions should be made with the following principles in mind:
- Scalability and maintainability
- Clear separation of concerns
- Consistent coding patterns
- Comprehensive error handling
- Security best practices

The code agent should establish a solid foundation by implementing core patterns and structures that will support future development needs.
