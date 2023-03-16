[1]: https://en.wikipedia.org/wiki/Fox
# Android DeeplinkSdk
[![Maven version (android-deeplink-sdk)](https://img.shields.io/maven-metadata/v.svg?label=maven-central&metadataUrl=https%3A%2F%2Frepo1.maven.org%2Fmaven2%2Fcom%2Fprovisionpay%2Fandroid-deeplink-sdk%2Fmaven-metadata.xml)](https://central.sonatype.com/artifact/com.provisionpay/android-deeplink-sdk)

A fast entegration library for deeplink Softpos apps.

# Installation

### Gradle
``` kotlin
implementation 'com.provisionpay:android-deeplink-sdk:latest-version'
``` 

# 1. Initialize
You have to use initalize method to be integrated into the project.
 ``` kotlin
val privateKey = "your private key" 
val activity   = "your activity"
val softposUrl = "your softpos url"
SoftposDeeplinkSdk.initialize(InitializeConfig(privateKey = privateKey ,activity = activity ,softposUrl = softposUrl))
``` 
Throws: NullArgumentException, ArgumentLengthException

# 2. Start Payment
This method starts your payment and provides you to softpos application. The method takes paymentSessionToken as parameter. This token must be 16 character.
 ``` kotlin
 SoftposDeeplinkSdk.startPayment(paymentSessionToken)
 ``` 
 Throws: MissingArgumentException, NullArgumentException, ArgumentLengthException
 
# 3. OnNewIntent Method
This method is used onNewIntent() method on MainActivity. The method provides categorize response status codes that comes Softpos applications.
 ``` kotlin
 override fun onNewIntent(intent: Intent?) {
        super.onNewIntent(intent)
        setIntent(intent)
        SoftposDeeplinkSdk.handleDeeplinkTransaction()
    }
 ``` 
Throws: InvalidInitializeMethod, NullArgumentException, NullSubscribeParameterException  

# 4. Handle Softpos Events
Subscribe method gives status codes responses.
``` kotlin
SoftposDeeplinkSdk.subscribe {
            object : SoftposDeeplinkSdkListener {
                override fun onPaymentDone(transaction: Transaction, isApproved: Boolean) {
                   //TODO
                }

                override fun onCancel() {
                    //TODO
                }

                override fun onIntentData(dataFlow: IntentDataFlow, data : String) {
                   when(e){
                     dataFlow.DataDecrypted -> {
                        //TODO
                    }
                     dataFlow.DataFound -> {
                        //TODO
                    }
                     dataFlow.ActivityIntentDataIsNull -> {
                        //TODO
                    }
                     dataFlow.ActivityIntentParameterDataIsNull -> {
                        //TODO
                    }
                }
                override fun onTimeOut() {
                   //TODO()
                }

                override fun onError(e: Throwable) {
                   //TODO
                }

                override fun onOfflineDecline(paymentFailedResult: PaymentFailedResult?) {
                   //TODO
                }

                override fun onSoftposError(errorType: SoftposErrorType,description:String?) {
                    when (errorType) {
                        SoftposErrorType.TerminalNotFound -> {
                           //TODO
                        }
                        SoftposErrorType.UserHashNotFound -> {
                           //TODO
                        }
                        SoftposErrorType.ActivationNotFound -> {
                           //TODO
                        }
                       SoftposErrorType.HostError -> {
                          //TODO
                       }
                        else -> {}
                    }
                }
            }
        }
```
# 5. Broadcast Receiver Support
This method takes your softpos url and gives BroadcastReceiverListener object. With this method you can listen eventType , evenTypeMessage and paymentSessionToken. 

``` kotlin
val packageId = "package id of softpos app"
SoftposDeeplinkSdk.registerBroadcastReceiver(packageId, {
            object : BroadcastReceiverListener {
                override fun onSoftposBroadcastReceived(
                    eventType: Int,
                    eventTypeMessage: String,
                    paymentSessionToken: String
                ) {
                   //TODO
                }
            }
        }
 ```       
 Throws: NullArgumentException
 
# 6. Debug Mode Setting
Optionally this method is used to specify debug mode is on.
 ``` kotlin
  SoftposDeeplinkSdk.setDebugMode(true)
 ``` 

 # 7. Sample projects
 | Platform  | Language |                                                           |
|------------|--------------|--------------------------------------------------------------|
| Android   |Kotlin           | [android-demo-kotlin](https://github.com/ProvisionPay/android-demo-kotlin)    |
| Android   |Java       | [android-demo-java](https://github.com/ProvisionPay/android-demo-java) |




