
# Insider
Insider is a .Net Core package exporting application state and metrics. 

UI is a simple web page with `state` and `metrics` tables. 

Insider supports integration with [Profiler](https://github.com/r-alekseev/Profiler) for collecting metrics.

## Design

### Local Library

Insider library opens `ui-web` and `ui-streaming` channels.

Browser connects to application's `ui-web` channel and opens `Insider-UI` page. 
Page connects to application's `ui-streaming` channel and starting to receive data.

![Local Library Design](https://github.com/r-alekseev/Insider/blob/assets/diagrams/v0.1/Insider-Local.png?raw=true)

## Protocol

### ui-streaming

`ui-streaming` channel accepting `WebSockets` connections and sending notifications in `JSON-RPC` format.

#### Example
```json
--> {"jsonrpc": "2.0", "method": "state-set", "params": {"key": "version", "value": "0.1"}}
--> {"jsonrpc": "2.0", "method": "state-set", "params": {"key": "health", "value": "green"}}
--> {"jsonrpc": "2.0", "method": "metric-set", "params": {"key": "calc-stats", "count": 44, "duration": 731}}
```

#### Schema

See [Schema](https://github.com/r-alekseev/Insider/blob/master/Versions/0.1/Schemas/ui-streaming.json) in [OpenRpc](https://open-rpc.org/) format.

## Installation

```
Install-Package Insider.Local
```

## Configuration

```csharp
var insider = new LocalInsiderConfiguration()
    .ConfigureDefault()
    .CreateInsider();
```

```csharp
insider.Run();
```

### Profiler Integration

```csharp
var profiler = new ProfilerConfiguration()
    .UseInsiderReportWriter(insider)
    .CreateProfiler();
```

## Usage

### State

```csharp
insider.SetState("version", "0.1");
insider.SetState("health", "Green");
```

### Metrics

```csharp
insider.SetMetric("calc-stats", count: 44, duration: TimeSpan.FromMilliseconds(731));
```

### Metrics with Profiler

```csharp
using (profiler.Section("calc-stats"))
{
    // doing calculations
}
```

```csharp
profiler.WriteReport();
```