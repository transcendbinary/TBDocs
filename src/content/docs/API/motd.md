---
title: MOTD
description: Our MOTD API

---

### api.transcendbinary.co.uk/app/motd.json

## Overview

Our MOTD API stores a list of MOTDs used in our apps and across services. 

```json
{
  "generic": [
    "Miles is Watching..."
  ],
  "special": {
    "2026-12-25": "Merry Christmas!"
  }
}
```

The root object has two properties: 

`generic`, which contains an array of Standard, Cycled MOTDs
`special`, which contains an object with dated keys for special MOTDs which will override the default on it's specified date

## Usage

### SetMOTD()

Use a `SetMOTD()` function to check the system is online and then run `FetchMOTD()`

```csharp
if (!IsOnline())
    {
        //handle the error
    }
else if (IsOnline())
    {
        await fetchMOTD();
    }
lblMOTD.Text = motd;
```
### FetchMOTD()

Use a `FetchMOTD()` function to first download and parse the JSON file

```csharp
using var client = new HttpClient();

string json = await client.GetStringAsync(
    "https://api.transcendbinary.co.uk/app/motd.json"
);

JsonDocument doc = JsonDocument.Parse(json);
```
Check if todays date is listed as a `Special` Key and set `motd`
```csharp
string today = DateTime.Today.ToString("yyyy-MM-dd");

if (doc.RootElement.GetProperty("special").TryGetProperty(today, out JsonElement special))
    {
        motd = special.GetString();
    }                                
```
then if not, use the `generic` array to select a MOTD based on the current day of the year and `return` to `SetMOTD()` set the MOTD text in the UI.
```csharp
else
    {
        string[] generic = doc.RootElement
            .GetProperty("generic")
            .Deserialize<string[]>();

        int index = DateTime.Today.DayOfYear % generic.Length;
        motd = generic[index];
    }
return;
```

the formula used for choosing a `generic` MOTD is `int index = DateTime.Today.DayOfYear % generic.Length;`. This ensures the MOTD is always the same across every app and service that uses it.
