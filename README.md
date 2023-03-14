[1]: https://en.wikipedia.org/wiki/Fox
# Android DeeplinkSdk
[![Maven-Central - 1.0.6](https://img.shields.io/badge/Maven--Central-1.0.6-2ea44f)](https://central.sonatype.com/artifact/com.provisionpay/android-deeplink-sdk/1.0.6)

A fast entegration library for deeplink Softpos apps.

# Installation

### Gradle
``` kotlin
implementation 'com.provisionpay:android-deeplink-sdk:latest-version'
``` 
# Get Started

### initialize
You have to use initalize method to be integrated into the project.
 ``` kotlin
val privateKey = "your private key" 
val activity   = "your activity"
val softposUrl = "your softpos url"
SoftposDeeplinkSdk.initialize(InitializeConfig(privateKey = privateKey ,activity = activity ,softposUrl = softposUrl))
``` 
Throws: NullArgumentException, ArgumentLengthException

### startPayment
This method starts your payment and provides you to softpos application. The method takes paymentSessionToken as parameter. This token must be 16 character.
 ``` kotlin
 SoftposDeeplinkSdk.startPayment(paymentSessionToken)
 ``` 
 Throws: MissingArgumentException, NullArgumentException, ArgumentLengthException
 
### handleDeeplinkTransaction
This method is used onNewIntent() method on MainActivity. The method provides categorize response status codes that comes Softpos applications.
 ``` kotlin
 override fun onNewIntent(intent: Intent?) {
        super.onNewIntent(intent)
        setIntent(intent)
        SoftposDeeplinkSdk.handleDeeplinkTransaction()
    }
 ``` 
Throws: InvalidInitializeMethod, NullArgumentException, NullSubscribeParameterException  

### subscribe
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

                override fun onIntentDataNotFound(intentDataError: IntentDataError) {
                   //TODO

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
### registerBroadcastReceiver
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
 
 ### setDebugMode
Optionally this method is used to specify debug mode is on.
 ``` kotlin
  SoftposDeeplinkSdk.setDebugMode(true)
 ``` 

 ### Sample projects
* Semple kotlin project [ demo](https://github.com/ProvisionPay/android-demo-kotlin).
* Semple java project [ demo](https://github.com/ProvisionPay/android-demo-java).

