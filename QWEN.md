# MissingPaletteFix - Minecraft Mod

## Project Overview

MissingPaletteFix is a Minecraft Forge mod designed to fix `MissingPaletteEntryException` crashes that occur when the game encounters block state IDs that don't exist in the current palette. The mod intercepts these missing entries and replaces them with a fallback block (Dragon Egg) to prevent crashes.

### Key Features
- **Mixin-based implementation**: Uses Mixin to hook into Minecraft's `HashMapPalette` class
- **Crash prevention**: Intercepts missing palette entries and provides a fallback block state
- **Targeted fix**: Specifically addresses `MissingPaletteEntryException` crashes in chunk loading

### Architecture
- **Main class**: `MissingPaletteFix.java` - Standard Forge mod entry point
- **Mixin**: `MHashMapPalette.java` - Intercepts the `valueFor` method in `HashMapPalette` to handle missing entries
- **Build system**: Gradle with ForgeGradle and MixinGradle plugins

## Project Structure

```
MissingPaletteFix/
├── build.gradle          # Gradle build configuration with Forge and Mixin setup
├── settings.gradle       # Gradle settings
├── gradle.properties     # Project properties and version definitions
├── gradle/               # Gradle wrapper
├── src/
│   └── main/
│       ├── java/
│       │   └── btpos/mcmods/missingpalettefix/
│       │       ├── MissingPaletteFix.java           # Main mod class
│       │       └── mixin/
│       │           └── MHashMapPalette.java         # Core mixin implementation
│       └── resources/
│           ├── META-INF/mods.toml                   # Mod metadata
│           └── missingpalettefix.mixins.json        # Mixin configuration
├── README.md             # Project description
└── update.json           # Update checker configuration
```

## Building and Running

### Prerequisites
- Java 17 or higher
- Minecraft 1.20.1 (target version)
- Forge 47.3.1 or compatible version

### Build Commands
```bash
# Build the mod JAR
./gradlew build

# Run Minecraft client with the mod
./gradlew runClient

# Run Minecraft server with the mod
./gradlew runServer

# Generate IDE configurations (Eclipse/IntelliJ)
./gradlew eclipse
./gradlew idea
```

### Configuration
The mod is configured through `gradle.properties`:
- `minecraft_version=1.20.1`
- `forge_version=47.3.1`
- `mod_id=missingpalettefix`
- `mod_version=1.0`

## Development Conventions

### Code Style
- Standard Java naming conventions
- Uses Minecraft Forge mod development patterns
- Mixin annotations for bytecode manipulation

### Mixin Implementation
The core fix is implemented using SpongePowered's Mixin library:
- `@Mixin(HashMapPalette.class)` - Targets the palette class
- `@Inject` - Hooks into constructor to detect block state palettes
- `@Redirect` - Intercepts value lookups to handle missing entries

### Error Handling
When a missing palette entry is detected:
1. Logs a warning message with the missing ID
2. Returns a Dragon Egg block state as a safe fallback
3. Prevents the crash that would normally occur

## Testing

The project includes Forge's standard run configurations for testing:
- Client testing with `./gradlew runClient`
- Server testing with `./gradlew runServer`
- Data generation with `./gradlew runData`

## Dependencies

- **Minecraft**: 1.20.1
- **Forge**: 47.3.1
- **Mixin**: 0.8.5
- **Mixingradle**: 0.7-SNAPSHOT

## License
MIT License as specified in gradle.properties