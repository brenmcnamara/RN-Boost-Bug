# RN-Boost-Bug
This repo is for demoing the bug with the boost-for-react-native dependency in as little code as possible


### How do I re-create this?

1. `react-native init Temp`
2. Paste the following in ios/Podfile:
```
platform :ios, '9.0'

# Remove this line to see the warnings that happen when calling 'pod install'.
# Refer to this issue: https://github.com/CocoaPods/CocoaPods/issues/4370
install! 'cocoapods', :deterministic_uuids => false

target 'Temp' do

  # Dependencies for react native firebase. Refer to this documentation:
  # https://rnfirebase.io/docs/v2.2.*/installation-ios#2.1)-Add-the-required-pods
  pod 'React', :path => '../node_modules/react-native', :subspecs => [
    'Core',
    'CxxBridge', # Include this for RN >= 0.47
    'DevSupport', # Include this to enable In-App Devmenu if RN >= 0.43
    'RCTText',
    'RCTNetwork',
    'RCTWebSocket', # needed for debugging
    # Add any other subspecs you want to use in your project
  ]

  pod 'yoga', :path => '../node_modules/react-native/ReactCommon/yoga'

  # Third party deps podspec link
  pod 'DoubleConversion', :podspec => '../node_modules/react-native/third-party-podspecs/DoubleConversion.podspec'
  pod 'GLog', :podspec => '../node_modules/react-native/third-party-podspecs/GLog.podspec'
  pod 'Folly', :podspec => '../node_modules/react-native/third-party-podspecs/Folly.podspec'

  target 'TempTests' do
    inherit! :search_paths
  end

end
```
3. `cd path/to/repo/ios/ && pod install`
