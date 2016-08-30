---
title: Android 测试专题笔记
date: 2016-08-15 00:11:49
tags: 
- Android
---
敢为常语谈何易，百炼工纯始自然。在软件开发中，完备的测试是防御软件缺陷的第一道也是最好的一道防线。

## 1. Test Types
### 1.1. Based on Running Platform

#### 1.1.1. Local Unit Tests
Located at `module-name/src/test/java/`
These tests run on the local JVM and do not have access to functional Android framework APIs.

#### 1.1.2. Instrumented Tests
Located at `module-name/src/androidTest/java/`
These are all tests that must run on an Android hardware device or an Android emulator.

- **Instrumented Unit Test:** Build complex unit tests with Android dependencies that cannot be satisfied with mock objects.
- **User Interface Tests:** Create tests to verify that the user interface behaves correctly for user interactions within a single app or for interactions across multiple apps.
- **App Component Integrations Test:** Verify the behavior of components that users do not directly interact with, such as a Service or a Content Provider.

### 1.2. Based on Real Testing Types
#### 1.2.1. Unit Tests
- **Local Unit Tests:**  Unit tests that run locally on the Java Virtual Machine (JVM). Use these tests to minimize execution time when your tests have no Android framework dependencies or when you can mock the Android framework dependencies.
- **Instrumented Unit Tests:** Unit tests that run on an Android device or emulator. These tests have access to Instrumentation information, such as the Context of the app you are testing. Use these tests when your tests have Android dependencies that mock objects cannot satisfy.

#### 1.2.2. Integration Tests
- **Components within your app only:** This type of test verifies that the target app behaves as expected when a user performs a specific action or enters a specific input in its activities. Supported by [Espresso](https://developer.android.com/tools/testing-support-library/index.html#Espresso).
- **Cross-app Components:** This type of test verifies the correct behavior of interactions between different user apps or between user apps and system apps. Supported by [UI Automator](https://developer.android.com/topic/libraries/testing-support-library/index.html#UIAutomator).

## 2. Set Up Testing Environment
### 2.1. Local Unit Tests
In your app's top-level `build.gradle` file, you need to specify theres libraries as dependencies:
```
dependencies {
    // Required -- JUnit 4 framework
    testCompile 'junit:junit:4.12'
    // Optional -- Mockito framework
    testCompile 'org.mockito:mockito-core:1.10.19'
}
```

### 2.2. Instrumented Tests
In your app's top-level build.gradle file, you need to specify these libraries as dependencies:
```
dependencies {
    androidTestCompile 'com.android.support:support-annotations:24.0.0'
    androidTestCompile 'com.android.support.test:runner:0.5'
    androidTestCompile 'com.android.support.test:rules:0.5'
    // Optional -- Hamcrest library
    androidTestCompile 'org.hamcrest:hamcrest-library:1.3'
    // Optional -- UI testing with Espresso
    androidTestCompile 'com.android.support.test.espresso:espresso-core:2.2.2'
    // Optional -- UI testing with UI Automator
    androidTestCompile 'com.android.support.test.uiautomator:uiautomator-v18:2.1.2'
}
```
To use JUnit 4 test classes, make sure to specify AndroidJUnitRunner as the default test instrumentation runner in your project by including the following setting in your app's module-level build.gradle file:
```
android {
    defaultConfig {
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
}
```

## 3. Create Test Casese
### 3.1. Local Unit Test Class
```
import org.junit.Test;
import java.util.regex.Pattern;
import static org.junit.Assert.assertFalse;
import static org.junit.Assert.assertTrue;

public class EmailValidatorTest {

    @Test
    public void emailValidator_CorrectEmailSimple_ReturnsTrue() {
        assertThat(EmailValidator.isValidEmail("name@email.com"), is(true));
    }
    ...
}
```
To test that components in your app return the expected results, use the junit.Assert methods to perform validation checks (or assertions) to compare the state of the component under test against some expected value. To make tests more readable, you can use Hamcrest matchers (such as the is() and equalTo() methods) to match the returned result against the expected result.

**Mock Android dependencies**
You can use a mocking framework to stub out external dependencies in your code, to easily test that your component interacts with a dependency in an expected way. By substituting Android dependencies with mock objects, you can isolate your unit test from the rest of the Android system while verifying that the correct methods in those dependencies are called. 

The [Mockito](https://github.com/mockito/mockito) mocking framework for Java (version 1.9.5 and higher) offers compatibility with Android unit testing. With Mockito, you can configure mock objects to return some specific value when invoked.

Steps to add a mock object to your local unit test:
1. Include the Mockito library dependency in your build.gradle file, as described in Section 2.1.
2. At the beginning of your unit test class definition, add the `@RunWith(MockitoJUnitRunner.class)` annotation. This annotation tells the Mockito test runner to validate that your usage of the framework is correct and simplifies the initialization of your mock objects.
3. To create a mock object for an Android dependency, add the `@Mock` annotation before the field declaration.
4. To stub the behavior of the dependency, you can specify a condition and return value when the condition is met by using the `when()` and `thenReturn()` methods.

***Code Example:***
```
@RunWith(MockitoJUnitRunner.class)
public class UnitTestSample {

    private static final String FAKE_STRING = "HELLO WORLD";

    @Mock
    Context mMockContext;

    @Test
    public void readStringFromContext_LocalizedString() {
        // Given a mocked Context injected into the object under test...
        when(mMockContext.getString(R.string.hello_word))
                .thenReturn(FAKE_STRING);
        ClassUnderTest myObjectUnderTest = new ClassUnderTest(mMockContext);

        // ...when the string is returned from the object under test...
        String result = myObjectUnderTest.getHelloWorldString();

        // ...then the result should be the expected one.
        assertThat(result, is(FAKE_STRING));
    }
}
```

### 3.2.  Instrumented Unit Test Class
To create an instrumented JUnit 4 test class, add the `@RunWith(AndroidJUnit4.class)` annotation at the beginning of your test class definition. 
```
import android.os.Parcel;
import android.support.test.runner.AndroidJUnit4;
import android.util.Pair;
import org.junit.Test;
import org.junit.runner.RunWith;
import java.util.List;
import static org.hamcrest.Matchers.is;
import static org.junit.Assert.assertThat;

@RunWith(AndroidJUnit4.class)
@SmallTest
public class LogHistoryAndroidUnitTest {

    public static final String TEST_STRING = "This is a string";
    public static final long TEST_LONG = 12345678L;
    private LogHistory mLogHistory;

    @Before
    public void createLogHistory() {
        mLogHistory = new LogHistory();
    }

    @Test
    public void logHistory_ParcelableWriteRead() {
        // Set up the Parcelable object to send and receive.
        mLogHistory.addEntry(TEST_STRING, TEST_LONG);

        // Write the data.
        Parcel parcel = Parcel.obtain();
        mLogHistory.writeToParcel(parcel, mLogHistory.describeContents());

        // After you're done with writing, you need to reset the parcel for reading.
        parcel.setDataPosition(0);

        // Read the data.
        LogHistory createdFromParcel = LogHistory.CREATOR.createFromParcel(parcel);
        List<Pair<String, Long>> createdFromParcelData = createdFromParcel.getData();

        // Verify that the received data is correct.
        assertThat(createdFromParcelData.size(), is(1));
        assertThat(createdFromParcelData.get(0).first, is(TEST_STRING));
        assertThat(createdFromParcelData.get(0).second, is(TEST_LONG));
    }
}
```
### 3.3.  Create an Espresso Test Class
The following code snippet shows how your test class might invoke this basic workflow:
```
onView(withId(R.id.my_view))            // withId(R.id.my_view) is a ViewMatcher
        .perform(click())               // click() is a ViewAction
        .check(matches(isDisplayed())); // matches(isDisplayed()) is a ViewAssertion
```
#### Using Espresso with ActivityTestRule
By using ActivityTestRule, the testing framework launches the activity under test before each test method annotated with @Test and before any method annotated with @Before. The framework handles shutting down the activity after the test finishes and all methods annotated with @After are run.

```
...
@RunWith(AndroidJUnit4.class)
@LargeTest
public class ChangeTextBehaviorTest {
    public static final String STRING_TO_BE_TYPED = "Espresso";
    @Rule
    public ActivityTestRule<MainActivity> mActivityRule = new ActivityTestRule<>(
            MainActivity.class);

    @Test
    public void changeText_sameActivity() {
        // Type text and then press the button.
        onView(withId(R.id.editTextUserInput))
                .perform(typeText(STRING_TO_BE_TYPED), closeSoftKeyboard());
        onView(withId(R.id.changeTextBt)).perform(click());

        // Check that the text was changed.
        onView(withId(R.id.textToBeChanged)).check(matches(withText(STRING_TO_BE_TYPED)));
    }
...
}
```
### 3.4. Create an UI Automator Test Class
... ...

### References
- [Getting Started with Testing | Android Developers](https://developer.android.com/training/testing/start/index.html)
- [Building Effective Unit Tests | Android Developers](https://developer.android.com/training/testing/unit-testing/index.html)
- [Automating User Interface Tests | Android Developers](https://developer.android.com/training/testing/ui-testing/index.html)
- [Android Testing Patterns  - YouTube](https://www.youtube.com/playlist?list=PLWz5rJ2EKKc-6HWg_jyP0U1zrVLHn65b2)
- [Espresso Documentation](https://google.github.io/android-testing-support-library/docs/index.html)