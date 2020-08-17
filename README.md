### 스프링부트 의존성

```
- web
- devtool
- mustache

<dependency>
    <groupId>io.sentry</groupId>
    <artifactId>sentry</artifactId>
    <version>1.7.30</version>
</dependency>

```

### sentry 문서

```
https://docs.sentry.io/clients/java/usage/
```

![image](https://user-images.githubusercontent.com/55937799/90353855-68645e80-e082-11ea-9e45-5942ed1d7634.png)

![image](https://user-images.githubusercontent.com/62128942/90354015-e1fc4c80-e082-11ea-9ae6-7e35dbad384b.png)

## 구글 에널리틱스

```js
<!-- The core Firebase JS SDK is always required and must be listed first -->
<script src="https://www.gstatic.com/firebasejs/7.18.0/firebase-app.js"></script>

<!-- TODO: Add SDKs for Firebase products that you want to use
     https://firebase.google.com/docs/web/setup#available-libraries -->
<script src="https://www.gstatic.com/firebasejs/7.18.0/firebase-analytics.js"></script>

<script>
  // Your web app's Firebase configuration
  var firebaseConfig = {
    apiKey: "",
    authDomain: "app-89b68.firebaseapp.com",
    databaseURL: "https://app-89b68.firebaseio.com",
    projectId: "app-89b68",
    storageBucket: "app-89b68.appspot.com",
    messagingSenderId: "474148405153",
    appId: "1:474148405153:web:cdefad6e442788d9d4d5e0",
    measurementId: "G-6MVSXMJB1Q"
  };
  // Initialize Firebase
  firebase.initializeApp(firebaseConfig);
  firebase.analytics();
</script>
</body>
</html>
```

## Sentry.io (로그 남기기)

- sentry.io 회원가입
- Setting - Project - 내 프로젝트 이름 - Client Keys(DSN) - DSN확인하기
- 설정

```java
package com.cos.googleapp.config;

import org.springframework.context.annotation.Configuration;

import io.sentry.Sentry;
import io.sentry.event.Event;
import io.sentry.event.EventBuilder;

@Configuration
public class SentrySupport {

	public SentrySupport() {
		System.out.println("===============================");
		Sentry.init("DSM주소");
	}


    public void logSimpleMessage(String msg) {
        // This sends an event to Sentry.
        EventBuilder eventBuilder = new EventBuilder()

                        .withMessage(msg)
                        .withLevel(Event.Level.ERROR)
                        .withLogger(SentrySupport.class.getName());

        // Note that the *unbuilt* EventBuilder instance is passed in so that
        // EventBuilderHelpers are run to add extra information to your event.
        Sentry.capture(eventBuilder); //soket통신으로 send하는 것임.
    }


}

```

- Sentry 실행방 법

```java
sentrySupport.logSimpleMessage("프로덕트 쪽 오류");
```
