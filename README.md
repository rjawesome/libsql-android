# Rebuilt stuff
- Follow the instructions from CONTRIBUTING.md to build yourself (or I also built it for you!)
- If you want to use my build, copy the file "libsql-release.aar" to your project's "apps/libs" directory
- Add the line `protobufJava = "4.28.2"` under dependencies and `protobuf-java = { module = "com.google.protobuf:protobuf-java", version.ref = "protobufJava" }` under libraries in your gradle/libs.versons.toml file
- Add the lines `implementation(files("libs/libsql-release.aar"))` and `implementation(libs.protobuf.java)` to your app's build.gradle (the one in app directory) file under dependencies (and remove any existing libsql/tursodb dependencies)
- You should be good to go!

<p align="center">
  <a href="https://tur.so/turso-android">
    <picture>
      <img src="/.github/cover.png" alt="libSQL Android" />
    </picture>
  </a>
  <h1 align="center">libSQL Android</h1>
</p>

<p align="center">
  Databases for Android multi-tenant AI Apps.
</p>

<p align="center">
  <a href="https://tur.so/turso-android"><strong>Turso</strong></a> ·
  <a href="https://docs.turso.tech"><strong>Docs</strong></a> ·
  <a href="https://docs.turso.tech/sdk/kotlin/quickstart"><strong>Quickstart</strong></a> ·
  <a href="https://docs.turso.tech/sdk/kotlin/reference"><strong>SDK Reference</strong></a> ·
  <a href="https://turso.tech/blog"><strong>Blog &amp; Tutorials</strong></a>
</p>

<p align="center">
  <a href="LICENSE">
    <picture>
      <img src="https://img.shields.io/github/license/tursodatabase/libsql-android?color=0F624B" alt="MIT License" />
    </picture>
  </a>
  <a href="https://tur.so/discord-android">
    <picture>
      <img src="https://img.shields.io/discord/933071162680958986?color=0F624B" alt="Discord" />
    </picture>
  </a>
  <a href="#contributors">
    <picture>
      <img src="https://img.shields.io/github/contributors/tursodatabase/libsql-android?color=0F624B" alt="Contributors" />
    </picture>
  </a>
  <a href="https://packagist.org/packages/turso/libsql">
    <picture>
      <img src="https://img.shields.io/packagist/dt/turso/libsql?color=0F624B" alt="Total downloads" />
    </picture>
  </a>
  <a href="/examples">
    <picture>
      <img src="https://img.shields.io/badge/browse-examples-0F624B" alt="Examples" />
    </picture>
  </a>
</p>

## Features

- 🔌 Works offline with [Embedded Replicas](https://docs.turso.tech/features/embedded-replicas/introduction)
- 🌎 Works with remote Turso databases
- ✨ Works with Turso [AI & Vector Search](https://docs.turso.tech/features/ai-and-embeddings)

> [!WARNING]
> This SDK is currently in technical preview. <a href="https://tur.so/discord-android">Join us in Discord</a> to report any issues.

## Install

Add `libsql` to your Gradle dependencies:

```kotlin
dependencies {
    implementation("tech.turso.libsql:libsql:0.1.0")
}
```

> [!NOTE]
> This will only work with the Android Gradle Plugin for now.

## Quickstart

The example below uses Embedded Replicas and syncs data every 1000ms from Turso.

```kotlin
import tech.turso.libsql.Libsql

val db = Libsql.open(
    path = "./local.db",
    url = "TURSO_DATABASE_URL",,
    authToken = "TURSO_AUTH_TOKEN",
    syncInterval: 1000
)

val conn = db.connect()

db.connect().use {
    it.execute_batch("
      CREATE TABLE IF NOT EXISTS users (
          id INTEGER PRIMARY KEY AUTOINCREMENT,
          name TEXT
      );

      INSERT INTO users (name) VALUES ('Iku');
    ")
}

db.connect().use {
    it.query("SELECT * FROM users WHERE id = ?", 1)
}
```

## Documentation

Visit our [official documentation](https://docs.turso.tech/sdk/kotlin).

## Support

Join us [on Discord](https://tur.so/discord-android) to get help using this SDK. Report security issues [via email](mailto:security@turso.tech).

## Contributors

See the [contributing guide](CONTRIBUTING.md) to learn how to get involved.

![Contributors](https://contrib.nn.ci/api?repo=tursodatabase/libsql-android)

<a href="https://github.com/tursodatabase/libsql-android/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22">
  <picture>
    <img src="https://img.shields.io/github/issues-search/tursodatabase/libsql-android?label=good%20first%20issue&query=label%3A%22good%20first%20issue%22%20&color=0F624B" alt="good first issue" />
  </picture>
</a>
