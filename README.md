# 🌈 Cocoapods: Bug in 1.6.0.rc.2 breaks build

## Example Project

### Configuration

* MacOS 10.14.2
* Xcode 10.1
* Cocoapods 1.6.0.rc.2 (failing)
* Cocoapods 1.6.0.beta.2 (working)

### Steps to reproduce

1. In the terminal, check that you are using Cocoapods 1.6.0.rc.2.

```
$ pod --version
1.6.0.rc.2
```

2. Clone this repo.
3. In the terminal, `cd` to the repo's directory.
4. Run `pod install` then open the generated workspace.

```
$ pod install
$ open CryptoWallet.xcworkspace/
```

⚠️ DO NOT build the default CryptoWallet target— all its files have been removed. We're going to attempt to build one of the dependencies.

5. From the target menu, select “Manage Schemas...” and turn **ON** the "LifeHash" target.
6. Set the menu to be something like “LifeHash > iPhone XR”.
7. Build the target.

🛑 All of LifeHash‘s dependencies will build, but LifeHash itself will fail to build, apparently because the compiler cannot find its dependencies at compile time.

8. Install Cocoapods 1.6.0.beta.2 and verify it's the active version.

```
$ pod --version
1.6.0.beta.2
```

9. Repeat steps 2-7.

✅ Note that this time the LifeHash target builds correctly.

### Expected Behavior

The example should build correctly under Cocoapods 1.6.0.rc.2.

### Output of project-diff

```
$ xcodeproj project-diff LifeHashBuildTest_1.6.0.beta.2/CryptoWallet.xcodeproj LifeHashBuildTest_1.6.0.rc.2/CryptoWallet.xcodeproj
--- 
...

$ xcodeproj project-diff LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj
---
rootObject:
  targets:
    ExtensibleEnumeratedName:
      buildConfigurationList:
        buildConfigurations:
          Debug:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
          Release:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
    LifeHash:
      buildConfigurationList:
        buildConfigurations:
          Debug:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
          Release:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
    Pods-CryptoWallet:
      buildConfigurationList:
        buildConfigurations:
          Debug:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
          Release:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
    WolfColor:
      buildConfigurationList:
        buildConfigurations:
          Debug:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
          Release:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
    WolfFoundation:
      buildConfigurationList:
        buildConfigurations:
          Debug:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
          Release:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
    WolfGeometry:
      buildConfigurationList:
        buildConfigurations:
          Debug:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
          Release:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
    WolfImage:
      buildConfigurationList:
        buildConfigurations:
          Debug:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
          Release:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
    WolfNumerics:
      buildConfigurationList:
        buildConfigurations:
          Debug:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
          Release:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
    WolfOSBridge:
      buildConfigurationList:
        buildConfigurations:
          Debug:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
          Release:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
    WolfPipe:
      buildConfigurationList:
        buildConfigurations:
          Debug:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
          Release:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
    WolfStrings:
      buildConfigurationList:
        buildConfigurations:
          Debug:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
          Release:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
    WolfWith:
      buildConfigurationList:
        buildConfigurations:
          Debug:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
          Release:
            buildSettings:
              ARCHS:
                LifeHashBuildTest_1.6.0.beta.2/Pods/Pods.xcodeproj: "$(ARCHS_STANDARD_64_BIT)"
                LifeHashBuildTest_1.6.0.rc.2/Pods/Pods.xcodeproj: 
Wolfs-Mac-Pro:Dropbox ironwolf$ 
```