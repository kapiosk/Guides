# Config

## Creating Another Config

```vbnet
Public Class Config
    Inherits SpiderNet.eBooking.Common.Config

    Public Shared ReadOnly SampleDatabase As String = ReadConnectionString("SampleDatabase")
    Public Shared ReadOnly SampleConfig As String = ReadConfiguration("SampleConfig")

End Class
```
