# FMHY-Bridge

Glue for bridging FMHY-Indexer to FMHY-Downloader. It exposes a clean HTTP API
that resolves movie and series streams from a set of supported sources.

> [!WARNING]
> This software is currently in alpha stages, there may be bugs and breaking
> changes to the API.

## Why is the code repository private?

The source code for FMHY-Bridge is **not public** and lives in a private
repository. This documentation repository only contains the public-facing
docs it deliberately contains none of the actual implementation.

The reasons are:

- **Reverse-engineered code.** The bridge contains original, reverse-engineered
  implementations of the internal protocols, request flows, and stream-resolution
  logic of various piracy/streaming websites. This code is not documented or
  published anywhere else.
- **DMCA exposure.** Publishing reverse-engineered code that interacts with
  copyright-infringing services invites DMCA takedown notices, repository
  strikes, and account-level consequences on the hosting platform. Keeping the
  implementation private avoids handing a ready-made target to rightsholders and
  keeps the project from being taken down.
- **Not open-source.** The code is intellectual property of the author. It is
  **not licensed** for distribution, redistribution, modification, or reuse. The
  absence of a license means all rights are reserved by default.

This public repository exists so that the API can be documented and consumed
without exposing the sensitive implementation.

## Documentation

- [ENDPOINTS.md](./ENDPOINTS.md), every HTTP endpoint, its query parameters,
  and response shapes.
- [CONFIGURATION.md](./CONFIGURATION.md), every variable you can use to
  configure the Docker container.

## Distribution

Only the prebuilt Docker image is distributed publicly:

```
ghcr.io/ggjorven/fmhy-bridge:latest
```

The image runs the compiled binary; no source is shipped inside it that would
constitute publishing the reverse-engineered logic.

## License

This project is **not licensed**. The code is the author's intellectual
property and is **not** to be distributed, shared, or reused.
