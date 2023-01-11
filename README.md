
# Android DeeplinkSdk
This library make esaier entegration softpos applications to your app.


# Download
Add the dependency below to your module's build.gradle file:

```kotlin
implementation com.provisionpay:deeplink-integrationsdk:1.0.0.75
```
# Getting Started
1.Add implemantation to your gradle.
2.Add this import line to your activity or fragment class ###### import com.provisionpay.deeplink.integrationsdk.*
3.Call initialize method and give your private key, softpos url, and activity for first.
4.Then call handlePaymentSessionToken method for take override methods. This override methods return you if you finish your payment or get you an error at anytime.

