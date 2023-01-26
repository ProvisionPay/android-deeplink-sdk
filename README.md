[1]: https://en.wikipedia.org/wiki/Fox
# Android DeeplinkSdk
[![Maven-Central - 1.0.1](https://img.shields.io/badge/Maven--Central-1.0.1-2ea44f)](https://central.sonatype.dev/artifact/com.provisionpay/android-deeplink-sdk/1.0.0)

A fast entegration library for deeplink Softpos apps.

# Documantation
You can find [android deeplink sdk documentation here][1] which has extended usage instructions and other useful information.

# Installation

### Gradle
``` kotlin
implementation 'com.provisionpay:android-deeplink-sdk:1.0.0'
```
### Maven
``` kotlin
<dependency>
    <groupId>com.provisionpay</groupId>
    <artifactId>android-deeplink-sdk</artifactId>
    <version>1.0.0</version>
</dependency>
```
# Get Started

### initialize
You have to use initalize method to 

### setDebugMode
Optionally this method is used to specify debug mode is on.
 ``` kotlin
  SoftposDeeplinkSdk.setDebugMode(true)
 ``` 
 
### handleDeeplinkTransaction
This method is used onNewIntent() method on MainActivity. The method provides categorize response status codes that comes Softpos applications.
 ``` kotlin
 override fun onNewIntent(intent: Intent?) {
        super.onNewIntent(intent)
        setIntent(intent)
        SoftposDeeplinkSdk.handleDeeplinkTransaction()
    }
 ``` 

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
