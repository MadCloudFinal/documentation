# AdManager

## How to use

To get started with AdManager follow [googles tutorial](https://developers.google.com/admob/android/quick-start) on setting up the admob sdk up until the "Initialize the Google Mobile Ads SDK" section.  

After that create a new instance the of AdManager class it using it's constructor.  
```java
AdManager adManager = new AdManager(context, inProduction)
```

`context` is going to be applications current context you are calling from. You can usually get this by passing in `this` or `getApplicationContext()` from a calling activity class.  
`inProduction` is a boolean used to determine if you should be shown real ads or testing ads. This is important because using real ads during testing can lead to your google ad mob account being terminated.

### Rewarded ads

If you want to display a rewarded ad using AdManager first you will call the `loadRewardedAd` method on the AdManager object you created earlier.  
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

Once the ad has loaded we can then call the `showRewardedAd` method.
This method takes in an Activity which is where the ad will be displayed and another callback which will run after the user has finished watching the ad.
Inside this callback should be where you reward the user for completing the ad.
It is recommended to put this inside of the first callback you created for the `loadRewardedAd` method if you wish to display the ad as soon as it is loaded.
```java
adManager.showRewardedAd(myActivity, () -> System.out.println("I watched a unskippable ad and should be rewarded"));
```

### Instertitial ads (Skippable ads)

create this

## Constructors

- AdManager
