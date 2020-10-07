# General

## Setting up ssh for Git

Go to portrait -> more options -> User settings -> SSH keys
and add public key

Create Keys:

```bash
ssh-keygen -t rsa -C "your_email@example.com"
```

## Create artifacts

### Automatic versioning for .Net Standard / dotnetcore

Use dotnet pack

In project file

```xml
  <PropertyGroup>
    <Deterministic>false</Deterministic>
    <Version>1.$([System.DateTime]::UtcNow.Date.Subtract($([System.DateTime]::Parse("2000-01-01"))).TotalDays).$([System.DateTime]::UtcNow.Hour)</Version>
  </PropertyGroup>
```

### Automatic versioning for .Net Framework

Use Nuget pack

In project file

```xml
<Deterministic>false</Deterministic>
```

In AssemblyInfo.vb

```vba
<Assembly: AssemblyVersion("1.0.*")>
<Assembly: AssemblyFileVersion("1.0")>
```
