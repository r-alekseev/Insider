# Insider

Insider is a library or dedicated server exporting you application state and metrics.

## Design

### Local Library

Insider library opens `ui-web`, `ui-streaming`, and `ui-control` channels.

Browser connects to application's `ui-web` channel and opens `Insider-UI` page. 
Page connects to application's `ui-streaming` channel and starting to receive data.
Page can control data flow by sending requests to application's `ui-control` channel.

Insider library stores data in your application's process memory. 

![Local Library Design](https://github.com/r-alekseev/Insider/blob/assets/diagrams/Insider-Local.png?raw=true)

### Dedicated Server

Insider dedicated server opens `ui-web`, `ui-streaming`, `ui-control`, and `app-streaming` channels.

Insider in-app client connects to server's `app-streaming` channel and starting to stream data.

Browser connects to server's `ui-web` channel and opens `Insider-UI` page. 
Page connects to server's `ui-streaming` channel and starting to receive data.
Page can control data flow by sending requests to server's `ui-control` channel.

Insider dedicated server stores data in some external storage.

![Dedicated Server Design](https://github.com/r-alekseev/Insider/blob/assets/diagrams/Insider-Remote.png?raw=true)

## Versions

|Version|Implementations|
|-------|---------------|
|[v0.1](https://github.com/r-alekseev/Insider/blob/master/Versions/0.1/README.md)|-|

## Integrations

[Insider.NetCore](https://github.com/r-alekseev/Insider.NetCore) support integration with [Profiler](https://github.com/r-alekseev/Profiler) - Minimalistic and fast profiling library.