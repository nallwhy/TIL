## What's New in Android Support Library

https://www.youtube.com/watch?v=V6-roIeNUY0

### Support Library 26

Above API 14

Only available on google maven repo

```
repositories {
  maven {
    url "https://maven.google.com"
  }
}
```

### Font

`myfont.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>
<font-family xmlns:app="http://schemas.android.com/apk/res-auto">
  <font app:fontStyle="normal" app:fontWeight="400" app:font="@font/myfont-regular"></font>
  <font app:fontStyle="normal" app:fontWeight="800" app:font="@font/myfont-bold"></font>
</font-family>
```

```xml
<TextView ...
  android:fontFamily="@font/myfont"
  android:textStyle="bold" />
```

#### Downloadable Fonts

You can get rid of bundled fonts and just rely on a `font provider`.

```java
FontRequest request = new FontRequest(
  "com.example.fontprovider.authority",
  "com.example.fontprovider",
  "Name of font",
  R.array.certs);

FontsContractCompat.FontRequestCallback callback =
  new FontsContractCompat.FontRequestCallback() {
    @Override
    public void onTypefaceRetrieved(Typeface typeface) {}

    @Override
    public void onTypefaceRequestFailed(int reason) {}
  }

FontsContractCompat.requestFont(context, request, callback, new Handler());
```

or

```xml
<?xml version="1.0" encoding="utf-8"?>
<font-family xmlns:app="http://schemas.android.com/apk/res-auto"
  app:fontProviderAuthority="com.example.fontprovider"
  app:fontProviderPackage="com.example.fontprovider"
  app:fontProviderQuery="dancing-script"
  app:fontProviderCerts="@array/certs">
</font-family>
```

or using Design tool (The easiest way)

### TextView Autosizing

```xml
<TextView
  ...
  app:autoSizeTextType="uniform"
  app:autoSizePresetSizes="@array/autosize_sizes" />

<TextView
  ...
  app:autoSizeTextType="uniform"
  app:autoSizeMinTextSize="12sp"
  app:autoSizeMaxTextSize="100sp"
  app:autoSizeStepGranularity="2sp" />
```

### Etc

* PreferenceDataStore
* FrameMetricsAggregator
* ActionBarDrawerToggle
