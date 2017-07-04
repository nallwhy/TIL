### 2017-07-04

#### Composer

https://github.com/gojuno/composer

Reactive Android Instrumentation Test Runner.


### 2017-07-03

#### LocationServices

https://blog.stylingandroid.com/locationservices/

```java
public class LocationFragment extends Fragment {

  private FusedLocationProviderClient locationProvicerClient = null;

  void registerForLocationUpdates() {
    locationProvicerClient = LocationServices.getFusedLocationProviderClient(getActivity());
    LocationRequest locationRequest = LocationRequest.create();
    Looper looper = Looper.myLooper();
    locationProviderClient.requestLocationUpdates(locationRequest, locationCallback, looper);
  }

  void unregisterForLocationUpdates() {
    fusedLocationProviderClient.removeLocationUpdates(locationCallback);
  }

  private LocationCallback locationCallback = new LocationCallback() {
    @Override
    public void onLocationResult(LocationResult locationResult) {
      super.onLocationResult(locationResult);
      Location lastLocation = locationResult.getLastLocation();
      updatePosition(lastLocation);
    }
  };
}
```

#### RxJava — The first 3 patterns

https://medium.com/@andrew.kelly/rxjava-the-first-3-patterns-4c112a85b689

```java
Observable<List<Event>> source1 = cacheRepository.getEventsFeed(...);
Observable<List<Event>> source2 = networkRepository.getEventsFeed(...);
Maybe<List<Event>> source = Observable.concat(source1, source2).firstElement();
```

#### Device Year Class

https://github.com/facebook/device-year-class


### 2017-06-06

#### Update your app to take advantage of the larger aspect ratio on new Android flagship devices

https://android-developers.googleblog.com/2017/03/update-your-app-to-take-advantage-of.html


### 2017-05-09

#### RxLoader

https://github.com/kmdupr33/RxLoader


### 2017-05-07

#### UltimateAndroidReference

https://github.com/aritraroy/UltimateAndroidReference


### 2017-05-05

#### Interfaces for presenters in MVP are a waste of time!

http://blog.karumi.com/interfaces-for-presenters-in-mvp-are-a-waste-of-time/

#### Introduction to Automated Android Testing

https://riggaroo.co.za/introduction-automated-android-testing/


### 2017-05-04

#### Object Oriented Tricks: #4 Starter Pattern -Android Edition

https://hackernoon.com/object-oriented-tricks-4-starter-pattern-android-edition-1844e1a8522d

#### Hidden Gems of Android O

https://medium.com/@ianhlake/hidden-gems-of-android-o-7def63136629


### 2017-05-02

#### MVC vs. MVP vs. MVVM on Android

https://news.realm.io/news/eric-maxwell-mvc-mvp-and-mvvm-on-android/

#### Fragments: The Solution to (and Cause of) All of Android's Problems

https://news.realm.io/news/michael-yotive-state-of-fragments-2017

#### Dependency Injection in Android with Dagger 2

https://www.raywenderlich.com/146804/dependency-injection-dagger-2


### 2017-04-25

#### AppIntro

https://github.com/apl-devs/AppIntro

Walkthrough

#### Litho

http://fblitho.com/
https://facebook.github.io/yoga/

A declarative UI framework for Android


### 2017-04-19

#### Workcation App – Part 1. Fragment custom transition 

https://www.thedroidsonroids.com/blog/android/workcation-app-part-1-fragments-custom-transition/

There are 3 more articles in that series.

#### How We Made the ToolBar on Android Move Like Jelly: Animation in Kotlin

https://yalantis.com/blog/toolbar-jelly-animation-kotlin-android


### 2017-04-13

#### RxJava2를 도입하며

https://medium.com/rainist-engineering/migrate-from-rxjava1-to-rxjava2-3aea3ff9051c

`Observable` 대신 `Single`, `Completable`, `Maybe` 를 적극적으로 사용하자.

#### RxRelay

https://github.com/JakeWharton/RxRelay

> A Subject except without the ability to call onComplete or onError.

Relays are simply Subjects without the aforementioned property. They allow you to bridge non-Rx APIs into Rx easily, and without the worry of accidentally triggering a terminal state.


### 2017-03-22

#### From design to android, part 1

http://saulmm.github.io/from-design-to-android-part1

Good example of ConstraintLayout & Chains, DataBinding.