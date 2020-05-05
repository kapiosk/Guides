# Cache

## Implementing a new cache

Sample implementation

```vbnet
Imports SpiderNet.eBooking.CacheManagement

Public Class SampleCache
    Inherits CacheManager

    Protected Overrides ReadOnly Property Provider As ProviderBase = GetProvider(CacheProviderCode.LOCALMEMORY, Region)

    Private Shared ReadOnly c As New SampleCache()
    Public Overrides ReadOnly Property Region As String = "Sample"

    Public Overrides Sub Init()
    End Sub
End Class
```

Our system currently supports:

- LOCAL, uses HttpContext.Current
- WINCACHE, shared Hashtable
- REDIS, interfaces with external redis server
- LOCALMEMORY, implements System.Runtime.Caching.MemoryCache

## Methods

### Legacy

GetExample

```vbnet
Public Shared Function GetExample() As String
    Dim key As String = $"{c.Region}:Sample"
    Return c.GetFromCache(key)
End Function
```

SetExample

```vbnet
Public Sub SetToCache(Of T)()
    Dim key As String = $"{c.Region}:Sample"
    c.SetToCache(Of T)(key)
End Sub
```

### Single Item

GetExample

```vbnet
Public Shared Function GetExample() As String
    Dim key As String = $"{c.Region}:Sample"
    Return c.GetFromCache(key,
                          Function() "ThisIsSampla",
                          Date.UtcNow.AddDays(1),
                          Common.CacheDependencyManager.GetFileName(Common.CacheDependencyManager.TypeCode.Sample))
End Function
```

ResetExample

```vbnet
Friend Shared Sub ClearAndResetSample()
    Dim key As String = $"{c.Region}:Sample"
    c.ResetCache(key,
                 Function() "ThisIsSampla",
                 Date.UtcNow.AddDays(1),
                 Common.CacheDependencyManager.GetFileName(Common.CacheDependencyManager.TypeCode.Sample))
End Sub
```

### Dictionary

GetDictionaryExample

```vbnet
Public Shared Function GetExcursionRestrictionsByExcursionId(sampleId As Integer) As String
    Dim key As String = $"{c.Region}:SampleDictionary"
    Dim obj As String = c.GetFromDictionaryCache(key,
                                                 Function() GetAllSamples.GroupBy(Function(x) x.sampleId).ToDictionary(Function(x) x.Key, x.ToArray.First),
                                                 Date.UtcNow.AddHours(6),
                                                 sampleId,
                                                 Common.CacheDependencyManager.GetFileName(Common.CacheDependencyManager.TypeCode.SampleDictionary))
    If obj Is Nothing Then Return $"No Sample With Id {sampleId}"
    Return obj
End Function
```

ResetDictionaryExample

```vbnet
Friend Shared Sub ResetSample(sampleId As Integer)
    Dim key As String = $"{c.Region}:SampleDictionary"
    c.ResetDictionaryCache(key, Function() GetSampleById(sampleId), sampleId)
End Sub
```

## Lock

To keep things thread safe please use Locks.vb when possible

Sample code

```vbnet
Dim obj = GetFromCache(key)
If obj Is Nothing Then
    SyncLock Locks.GetLock(key)
        obj = GetFromCache(key)
        If obj Is Nothing Then
            obj = GetFromDB(key)
            SetToCache(key, obj)
        End If
    End SyncLock
End If
```
