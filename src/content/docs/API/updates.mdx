---
title: Updaters
description: Our Update API

---

### api.transcendbinary.co.uk/updates

## Overview

we have two types of update API: .TXT and .JSON. In both cases, Every app we have has its own file inside 'updates'. each file contains both the number of the latest version and a direct link to download from our CDN.

## .TXT Updaters

.TXT Updaters are used by ActualInstaller for our Windows apps. An Example of a TXT update file is:

```plaintext
1.1.1
cdn.transcendbinary.co.uk/gamesApps/app/windows/TBDesktopApp_v1.1.1.exe
```

The first line is the latest version release number (without the `v` prefix)

the second line is a direct link to download the app from our CDN. Notice the version number *in* the URL as opposed to using the `TBDesktopApp_Latest.exe` format; This is to combat caching and ensure the version download is, in fact, the latest version. 

## .JSON Updaters

.JSON Updaters are used for custom update systems such as our Android app

The JSON Format is largely the same as the TXT format except it uses JSON Keys to store information. Since every app has its own file, there is no need for a Class. An example is:

```json
{
  "latestVersion": "0.1.1",
  "url": "https://cdn.transcendbinary.co.uk/gamesApps/app/android/TBAndroidApp_v0.1.1.apk"
}
```

`latestVersion` contains the version number (again, without the `v` prefix)
`url` contains a link to download the latest version from the CDN

### Usage

see an example of how this is used:

The `checkForUpdate()` requests an update manifest from the API which sends back the JSON containing the latest version number and download URL.

```kotlin
suspend fun checkForUpdate(context: Context) {
    withContext(Dispatchers.IO) {
        try {
            val connection = URL(UPDATE_URL).openConnection() as HttpURLConnection
            connection.connectTimeout = 5000
            connection.readTimeout = 5000

            if (connection.responseCode != 200) return@withContext

            val json = JSONObject(
                connection.inputStream.bufferedReader().use { it.readText() }
            )
            connection.disconnect()

            val latestVersion = json.getString("version")
            val downloadUrl = json.getString("url")

            if (isVersionNewer(latestVersion)) {
                downloadUpdate(context, downloadUrl)
            }
        } catch (_: Exception) {
            // Handle errors
        }
    }
}
```

`isVersionNewer()` compares the currently installed version to the version listed in the update manifest. If a newer version is available, the application can notify the user and provide the download URL.

```kotlin
private fun isVersionNewer(latest: String): Boolean {
    val currentParts = CURRENT_VERSION.split(".").map { it.toInt() }
    val latestParts = latest.split(".").map { it.toInt() }

    for (i in 0 until maxOf(currentParts.size, latestParts.size)) {
        val current = currentParts.getOrElse(i) { 0 }
        val newest = latestParts.getOrElse(i) { 0 }

        if (newest > current) return true
        if (newest < current) return false
    }

    return false
}
```

If the user chooses to update, `downloadUpdate()` is called and Android's `DownloadManager` downloads the APK to the device's Downloads folder. The user can then install the downloaded APK manually.

```kotlin
private fun downloadUpdate(context: Context, url: String) {
    val request = DownloadManager.Request(Uri.parse(url))
        .setNotificationVisibility(
            DownloadManager.Request.VISIBILITY_VISIBLE_NOTIFY_COMPLETED
        )
        .setDestinationInExternalPublicDir(
            Environment.DIRECTORY_DOWNLOADS,
            "update.apk"
        )

    val manager = context.getSystemService(
        Context.DOWNLOAD_SERVICE
    ) as DownloadManager

    manager.enqueue(request)

    context.startActivity(
        Intent(DownloadManager.ACTION_VIEW_DOWNLOADS).apply {
            if (context !is Activity) {
                addFlags(Intent.FLAG_ACTIVITY_NEW_TASK)
            }
        }
    )
}
```