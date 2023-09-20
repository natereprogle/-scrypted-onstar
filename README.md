# Scrypted OnStar

A Scrypted plugin to control OnStar enabled vehicles.

This plugin was tested using a `2024 Chevrolet Trax 1RS`. Other vehicle features may vary.

I recommend, if possible, creating a secondary OnStar account and connecting this plugin to it. You can share vehicles with these second OnStar accounts, and it protects your main account as well.

This plugin uses an **UNOFFICIAL** API, [OnStarJS](https://github.com/samrum/OnStarJS). OnStar refuses to provide developers with a publicly available API. They claim to have commercial development APIs available, but also refuse to respond to development requests. Therefore, the community has had to resort to workarounds and reverse engineering the OnStar API. **USE THIS AT YOUR OWN RISK**.

**<u>Help Wanted</u>**! If you know how to make this plugin better, or want to contribute, please submit a pull request 😄

## Usage

Once installed, you will need four things:

1. The VIN of primary vehicle
2. Your OnStar Username
3. Your OnStar Password
4. Your OnStar Account PIN

Enter those items in the settings pane of the @natereprogle/onstar plugin, and save. Then, reload the plugin. Your vehicles should appear momentarily. You may also add them to the HomeKit plugin for control of them via Siri, Shortcuts, or other automations. And, in iOS 17, since widgets are interactable, this means you can finally use a widget (Home or Shortcuts) to start your vehicle instead of having to open the official app for your vehicle. See the below screenshot as an example! (Ignore the updating outlets 😜)

<div align="center">
    <img src="https://github.com/natereprogle/scrypted-onstar/blob/5cd970082449123baac1bd1a9ce180ce4e8d4310/assets/HomeKit.PNG?raw=true" alt="Screenshot of HomeKit app showing vehicle controls" width="50%" height="50%">
</div>

## Current Features

1. Remote Lock / Unlock
2. Remote Start
3. Activate Horn / Lights
4. Model, Manufacturer, Serial Number, and Firmware Version in the HomeKit device settings all match your vehicle information. Serial Number maps to VIN, and Firmware Version maps to vehicle year. Feel free to brag about your firmware version being 2024.0, if you so choose 😎

## Planned Features

1. Add support for EV-specific functionality (Will need assistance, as my vehicle is an ICE).
2. Add the ability to check diagnostic information from HomeKit. This can be achieved by creating sensors and setting them based on diagnostic levels.

## Workarounds

As it is currently not possible to query a vehicle's status (See "Current Limitations" below), the plugin will do two things automatically

1. The doors will automatically lock after 5 minutes, if not locked from HomeKit. The same applies to the horn and lights, if they are on.
2. The engine switch will automatically be flipped to off after 15 minutes (On my car, the timeout is 15 minutes. Not sure if this is the same for EVs or other GM vehicles). I am tempted to make this flip back to off automatically once the vehicle is running, that way you, as the driver, are aware your vehicle started, but for now it's just a 15 minute timeout, just like the myChevy app.

## Current Limitations

1. As far as I'm aware, the OnStar API does not _send_ data on its own, it only sends replies to requests. Therefore, vehicles cannot currently be queried for their status's. You can query diagnostic info, but that does not include things like lights, lock, engine status, or panic.
2. This is an unofficial API. At any time OnStar can block the usage of this API, or even ban your account, if they so chose. Since OnStarJS uses the "official" key from the Android APK, and you are using legitimate credentials, I don't see why they would, but they are the "boss", so-to-speak, regarding their product. So, use this with caution.
3. Each feature is its own "device". Unlike HomeBridge, where you can create devices with multiple properties on them (For example, the [Hatch Baby Rest plugin](https://github.com/dgreif/homebridge-hatch-baby-rest/blob/main/packages/homebridge-hatch-baby-rest/README.md) from dgrief, which allows you to set brightness, power, and volume (using a fan speed control) all within the same device), I was not able to figure out how to create a single device with multiple properties. So, for each vehicle you own, you will have at least 4 (for now) devices associated with it.
