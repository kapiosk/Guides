# Adding Application Insights to Project

## Adding browser insights

Add the following in a master page

```javascript
<script type="text/javascript">
var sdkInstance="appInsightsSDK";window[sdkInstance]="appInsights";var aiName=window[sdkInstance],aisdk=window[aiName]||function(e){function n(e){t[e]=function(){var n=arguments;t.queue.push(function(){t[e].apply(t,n)})}}var t={config:e};t.initialize=!0;var i=document,a=window;setTimeout(function(){var n=i.createElement("script");n.src=e.url||"https://az416426.vo.msecnd.net/scripts/b/ai.2.min.js",i.getElementsByTagName("script")[0].parentNode.appendChild(n)});try{t.cookie=i.cookie}catch(e){}t.queue=[],t.version=2;for(var r=["Event","PageView","Exception","Trace","DependencyData","Metric","PageViewPerformance"];r.length;)n("track"+r.pop());n("startTrackPage"),n("stopTrackPage");var s="Track"+r[0];if(n("start"+s),n("stop"+s),n("setAuthenticatedUserContext"),n("clearAuthenticatedUserContext"),n("flush"),!(!0===e.disableExceptionTracking||e.extensionConfig&&e.extensionConfig.ApplicationInsightsAnalytics&&!0===e.extensionConfig.ApplicationInsightsAnalytics.disableExceptionTracking)){n("_"+(r="onerror"));var o=a[r];a[r]=function(e,n,i,a,s){var c=o&&o(e,n,i,a,s);return!0!==c&&t["_"+r]({message:e,url:n,lineNumber:i,columnNumber:a,error:s}),c},e.autoExceptionInstrumented=!0}return t}(
{
  instrumentationKey:"add_instrumentationKey_here"
}
);window[aiName]=aisdk,aisdk.queue&&0===aisdk.queue.length&&aisdk.trackPageView({});
</script>
```

## Adding to application configuration (web.config or app.config)

Add the tracer

```xml
<configuration>
    <system.diagnostics>
        <trace autoflush="true" indentsize="0">
            <listeners>
                <add name="myAppInsightsListener" type="Microsoft.ApplicationInsights.TraceListener.ApplicationInsightsTraceListener, Microsoft.ApplicationInsights.TraceListener" />
            </listeners>
        </trace>
    </system.diagnostics>
</configuration>
```

Add modules in web

```xml
<configuration>
    <system.web>
        <httpModules>
            <add name="TelemetryCorrelationHttpModule" type="Microsoft.AspNet.TelemetryCorrelation.TelemetryCorrelationHttpModule, Microsoft.AspNet.TelemetryCorrelation" />
            <add name="ApplicationInsightsWebTracking" type="Microsoft.ApplicationInsights.Web.ApplicationInsightsHttpModule, Microsoft.AI.Web" />
        </httpModules>
    </system.web>
</configuration>
```

Reset modules in webServer

```xml
<configuration>
    <system.webServer>
        <validation validateIntegratedModeConfiguration="false" />
        <modules>
            <remove name="TelemetryCorrelationHttpModule" />
            <add name="TelemetryCorrelationHttpModule" type="Microsoft.AspNet.TelemetryCorrelation.TelemetryCorrelationHttpModule, Microsoft.AspNet.TelemetryCorrelation" preCondition="managedHandler" />
            <remove name="ApplicationInsightsWebTracking" />
            <add name="ApplicationInsightsWebTracking" type="Microsoft.ApplicationInsights.Web.ApplicationInsightsHttpModule, Microsoft.AI.Web" preCondition="managedHandler" />
        </modules>
    </system.webServer>
</configuration>
```

Check if you need to redirect a dll version e.g.

```xml
<configuration>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="System.Diagnostics.Tracing" publicKeyToken="31bf3856ad364e35" culture="neutral" />
                <bindingRedirect oldVersion="0.0.0.0-4.2.0.0" newVersion="4.2.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
</configuration>
```

## Using Key from web/app .config

Add to Application_Start

```vbnet
If Not Config.DisableTelemetry Then
    Microsoft.ApplicationInsights.Extensibility.TelemetryConfiguration.Active.InstrumentationKey = Config.ApplicationInsightsInstrumentationKey
End If
```

## Disabling Application Insights when debugging

Add to Application_Start

```vbnet
If Config.DisableTelemetry Then
    Microsoft.ApplicationInsights.Extensibility.Implementation.TelemetryDebugWriter.IsTracingDisabled = True
    Microsoft.ApplicationInsights.Extensibility.TelemetryConfiguration.Active.DisableTelemetry = True
End If
```
