---
title: Tracing .NET Applications
kind: Documentation
aliases:
- /tracing/dotnet
- /tracing/languages/dotnet
further_reading:
- link: "https://github.com/DataDog/dd-trace-csharp"
  tag: "Github"
  text: Source code
- link: "tracing/visualization/"
  tag: "Documentation"
  text: "Explore your services, resources and traces"
- link: "tracing/advanced_usage/?tab=net"
  tag: "Advanced Usage"
  text: "Advanced Usage"
---

<div class="alert alert-warning">
.NET Tracing is in an open Public Beta and will be Generally Available in October 2018.
</div>

## Installation and Getting Started

To begin tracing applications written in any language, first [install and configure the Datadog Agent][1].

### Windows

To use automatic instrumentation on Windows, download the latest MSI installer for Windows from the public [GitHub repository][3]. To instrument Windows services (including web applications running on IIS), reboot the host after running the installer so these services can pick up the required environment variables added by the installer.

[Download MSI installer for Windows][3]

### Linux

Automatic instrumention for .NET Core on Linux is coming soon.

## Automatic Instrumentation

Automatic instrumentation uses the Profiling API provided by .NET Framework and .NET Core to modify IL instructions at run time and inject instrumentation code. With zero code changes or configuration, the .NET tracer automatically instruments all supported libraries out of the box.

Automatic instrumentation captures:

* Method execution time
* Relevant trace data such as URL and status response codes for web requests or SQL query for database access
* Unhandled exceptions, including stacktrace if available
* A total count of traces (requests) flowing through the system

### Runtime Compatibility

The .NET tracer supports automatic instrumentation on the following .NET runtimes:

| .NET Runtime   | Versions | OS      | Support Type      |
| :------------- | :------- | :------ | :---------------- |
| .NET Framework | 4.5+     | Windows | Public Beta       |
| .NET Core      | 2.0.x    | Windows | Public Beta       |
| .NET Core      | 2.0.x    | Linux   | Coming soon       |
| .NET Core      | 2.1.3+   |         | Coming soon       |

**Note**: Libraries that target .NET Standard 2.0 are supported when running on either .NET Framework 4.6.1+ or .NET Core 2.0.x.

Don’t see your desired frameworks? We’re continually adding additional support. [Check with the Datadog team][5] to see if we can help.

### Web Framework Integrations

The .NET tracer can instrument the following web frameworks automatically:

| Web framework    | Versions | Runtime             | OS      | Support Type      |
| :--------------- | :------- | :------------------ | :------ | :---------------- |
| ASP.NET MVC      | 5.2.x    | .NET Framework 4.5+ | Windows | Public Beta       |
| ASP.NET Web API  | 2.2.x    | .NET Framework 4.5+ | Windows | Public Beta       |
| ASP.NET Core MVC | 2.0+     | .NET Framework 4.5+ | Windows | Public Beta       |
| ASP.NET Core MVC | 2.0+     | .NET Core 2.0.x     | Windows | Public Beta       |
| ASP.NET Core MVC | 2.0+     | .NET Core 2.0.x     | Linux   | Coming soon       |

Don’t see your desired web frameworks? We’re continually adding additional support. [Check with the Datadog team][5] to see if we can help.

### Data Store Integrations

The .NET tracer's ability to automatically instrument data store access depends on the client libraries used:

| Data store    | Library or NuGet package            | Versions | Support type    |
| :---------    | :---------------------------------- | :------- | :-------------- |
| MS SQL Server | Built-in .NET Framework `SqlClient` |          | Public Beta     |
| MS SQL Server | `System.Data.SqlClient`             | 4.1+     | Public Beta     |
| Redis         | `StackExchange.Redis`               |          | Coming soon     |
| Elasticsearch | `NEST` / `Elasticsearch.Net`        |          | Coming soon     |
| MongoDB       | `MongoDB.Driver`                    |          | Coming soon     |
| PostgreSQL    | `Npgsql`                            |          | Coming soon     |

Don’t see your desired data store libraries? We’re continually adding additional support. [Check with the Datadog team][5] to see if we can help.

## Manual Instrumentation

To manually instrument your code, add the [`Datadog.Tracing`][6] NuGet package to your application. Then wrap any code in a tracer scope and set the span's type, resource name, and tags:

```csharp
using(var scope = Datadog.Tracing.Tracer.Instance.StartActive("operation_name"))
{
  var span = scope.Span;
  span.Type = "custom";
  span.ResourceName = "resource_name"
  span.SetTag("tag_name", "tag_value");

  // do work...
}
```

For more details, see [Advanced Usage][2].

## Further Reading

{{< partial name="whats-next/whats-next.html" >}}

[1]: https://docs.datadoghq.com/tracing/setup
[2]: /tracing/advanced_usage/?tab=net
[3]: https://github.com/DataDog/dd-trace-csharp/releases
[4]: https://www.nuget.org/packages/Datadog.Trace/
[5]: /help
[6]: https://www.nuget.org/packages/Datadog.Trace/
