# [Application Insights](https://learn.microsoft.com/en-us/training/paths/az-204-instrument-solutions-support-monitoring-logging/)

### [Monitor](https://learn.microsoft.com/en-us/training/modules/monitor-app-performance/)

- Request rates, response times, and failure rates - Find out which pages are most popular, at what times of day, and where your users are. See which pages perform best. If your response times and failure rates go high when there are more requests, then perhaps you have a resourcing problem.
- Dependency rates, response times, and failure rates - Find out whether external services are slowing you down.
- Exceptions - Analyze the aggregated statistics, or pick specific instances and drill into the stack trace and related requests. Both server and browser exceptions are reported.
- Page views and load performance - reported by your users' browsers.
- AJAX calls from web pages - rates, response times, and failure rates.
- User and session counts.
- Performance counters from your Windows or Linux server machines, such as CPU, memory, and network usage.
- Host diagnostics from Docker or Azure.
- Diagnostic trace logs from your app - so that you can correlate trace events with requests.
- Custom events and metrics that you write yourself in the client or server code, to track business events such as items sold or games won.

There are two kinds of metrics:
- Log-based metrics behind the scene are translated into Kusto queries from stored events.
- Standard metrics are stored as pre-aggregated time series.

Auto-Instrumentation is the preferred way to collect metrics but is severly limited to the platform and language it supports.

Availability tests check various metrics of your application like response time etc. Most commonly via an URL ping. 
Custom TrackAvailability test is the long term supported solution for multi request or authentication test scenarios.
