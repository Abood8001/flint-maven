# flint-maven

Public Maven repository hosting the **Flint AntiCheat** developer API.

This repo contains only the thin, dependency-free `flint-api` artifact — the interfaces, events
and enum that a plugin compiles against to integrate with Flint. No plugin source, no plugin jar.

> ### ⚠️ The repository URL is not a web page — a 404 in your browser is normal
>
> Pasting `https://raw.githubusercontent.com/Abood8001/flint-maven/main/` into a browser returns
> **`404: Not Found`**. That is expected and does **not** mean the repo is down.
> `raw.githubusercontent.com` serves individual *files*, not directory listings, so the base path
> has nothing to show. Maven and Gradle never request that path — they request specific artifact
> files, which resolve normally. See for yourself:
>
> [`.../dev/abood8001/flint-api/1.0/flint-api-1.0.jar`](https://raw.githubusercontent.com/Abood8001/flint-maven/main/dev/abood8001/flint-api/1.0/flint-api-1.0.jar)
> → downloads fine.
>
> To *browse* what's published, use the GitHub file view instead:
> [dev/abood8001/flint-api](https://github.com/Abood8001/flint-maven/tree/main/dev/abood8001/flint-api)

## Usage

Add the repository and the dependency. It's compile-time only, so use `provided` (Maven) /
`compileOnly` (Gradle) — the real classes come from the Flint plugin at runtime.

> **This jar is not a plugin.** It contains interfaces only — no `plugin.yml`, no implementation.
> Putting it in a server's `plugins/` folder will fail to load ("does not contain a plugin.yml").
> It belongs on your *compile* classpath; the server gets the real classes from `FlintAC.jar`.

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
