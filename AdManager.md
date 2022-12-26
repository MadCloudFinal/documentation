# AdManager

- [Getting started](#getting-started)
- [Rewarded ads](#rewarded-ads-unskippable-ads)
- [Interstitial ads](#interstitial-ads-skippable-ads)
- [Reference](#reference)


### Getting started

To get started with AdManager follow [googles tutorial](https://developers.google.com/admob/android/quick-start) on setting up the admob sdk up until the "Initialize the Google Mobile Ads SDK" section.  

After that create a new instance the of AdManager class it using it's constructor.  
```java
AdManager adManager = new AdManager(context, inProduction)
```

`context` is going to be the applications current context you are calling from. You can usually get this by passing in `this` or `getApplicationContext()` from a calling activity class.  
`inProduction` is a boolean used to determine if you should be shown real ads or testing ads. This is important because using real ads during testing can lead to your google ad mob account being terminated.

### Rewarded ads (Unskippable ads)

If you want to display a rewarded ad using AdManager first call the `loadRewardedAd` method on the AdManager object you created earlier.  
This method takes in a callback and will run that callback once the ad has finished loading.  
Using lambdas:
```java
adManager.loadRewardedAd(() -> System.out.println("The ad has loaded"));
```
Using an anonymous function:   
```java
adManager.loadRewardedAd(new Runnable() 
{
  @Override
  public void run()
  {
    System.out.println("The ad has loaded");
  }
});
```
Using a method reference:  
```java
adManager.loadRewardedAd(this::showAd);

private void showAd()
{
  System.out.println("The ad has loaded");
}
```

Once the ad has loaded we can then call the `showRewardedAd` method.
This method takes in an Activity which is where the ad will be displayed and another callback function which will run after the user has finished watching the ad.
Inside this callback should be where you reward the user for completing the ad.
It is recommended to put this inside of the first callback you created for the `loadRewardedAd` method if you wish to display the ad as soon as it is loaded.
```java
adManager.showRewardedAd(myActivity, () -> System.out.println("I watched an unskippable ad and should be rewarded"));
```

### Interstitial ads (Skippable ads)
To display insterstitial ads using AdManager you will first need to load an ad. This can be done by calling the `loadInterstitialAd` method on an AdManager object.
This method takes in a callback function that will run after the ad has loaded.
```java
adManager.loadInterstitialAd(() -> System.out.println("The ad has loaded"));
```
Once the ad has loaded the `showInterstitialAd` method can be called to show the ad. This method takes an Activity that will be used to determine where to display the ad. It is recommended to put this method call inside of the callback created in the `loadInterstitialAd` method if you would like to show the ad immediately after it it loaded.
```java
adManager.showInterstitialAd(myActivity);
```

## Reference


### Constructors

```java
public AdManager (Context context, boolean inProduction)
```
Creates a new instance of `AdManager`. The `inProduction` variable determines which ad unit ids are used.  

### Public Methods

```java
public void loadRewardedAd(Runnable adLoadCallback)
```
Loads a rewarded ad and runs the `adLoadCallback` once it is loaded.  
<br/>

```java
public void showRewardedAd(Activity activity, Runnable userEarnedRewardCallback)
```
Shows a rewarded ad over the `activity` and runs the `userEarnedRewardCallback` once the ad has finished playing.  
<br/>

```java
public void loadInterstitialAd(Runnable adLoadCallback)
```
Loads a interstitial ad and runs the `adLoadCallback` once it is loaded.  
<br/>

```java
public void showInterstitialAd(Activity activity)
```
Shows a interstitial ad over the `activity`
