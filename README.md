# flint-maven

Public Maven repository hosting the **Flint AntiCheat** developer API.

This repo contains only the thin, dependency-free `flint-api` artifact — the interfaces, events
and enum that a plugin compiles against to integrate with Flint. No plugin source, no plugin jar.

## Usage

Add the repository and the dependency. It's compile-time only, so use `provided` (Maven) /
`compileOnly` (Gradle) — the real classes come from the Flint plugin at runtime.

### Maven

```xml
<repositories>
    <repository>
        <id>flint</id>
        <url>https://raw.githubusercontent.com/Abood8001/flint-maven/main/</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>dev.abood8001</groupId>
        <artifactId>flint-api</artifactId>
        <version>1.0</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```

### Gradle

```groovy
repositories {
    maven { url 'https://raw.githubusercontent.com/Abood8001/flint-maven/main/' }
}
dependencies {
    compileOnly 'dev.abood8001:flint-api:1.0'
}
```

## Quick start

Depend on Flint in your `plugin.yml` (`depend: [FlintAC]`), then grab the API singleton:

```java
if (FlintAPIProvider.isAvailable()) {
    FlintAPI flint = FlintAPIProvider.getAPI();
    int vl = flint.getViolations(player, "Reach");
}
```

The full developer guide — events (`FlintViolationEvent`, `FlintPunishmentEvent`), every method,
the check-name reference and a complete example plugin — ships with the plugin as `FLINT-API.md`.

## Versions

| Version | Notes |
|---|---|
| `1.0` | Initial public API. |
