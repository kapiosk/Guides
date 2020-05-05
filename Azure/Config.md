# Configuration files (web.config / app.config)

## Dealing with solution configurations

Adding a key which is not in the parent config

```xml
<add key="TestKey" value="TestValue" xdt:Transform="Insert" />
```

Removing an attribute from a tag which is in the parent config and should not be in the build

```xml
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

Modifying a key

```xml
<add key="TestKey" value="TestValue" xdt:Transform="Replace" xdt:Locator="Match(key)" />
```

Changing an attribute of a tag

```xml
<add name="DBcon" connectionString="LiveServerConn" providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)" />
```
