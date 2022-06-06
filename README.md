# Compose UI

### This is a simple tutorial for UI testing in Jetpack Compose (Desktop)

---

### The project can have JUnit5 as primary testing library

### Add the following dependencies to a build.gradle.kts

```kotlin
testImplementation(kotlin("test"))

@OptIn(org.jetbrains.compose.ExperimentalComposeLibrary::class)
testImplementation(compose.uiTestJUnit4)

implementation(compose.desktop.currentOs)

testImplementation("junit:junit:4.13.1")
testImplementation("org.junit.vintage:junit-vintage-engine:5.8.0")
```

### Run this code with JUnit4 settings (in JetBrains Idea a test could be created via *generate* → *test* → *with JUnit4 library*)

```kotlin
class MainKtTest {

    @get:Rule
    val composeTestRule = createComposeRule()
    
    @Before // JUnit4 Before Import
    fun setUp(){
        composeTestRule.setContent {
            App()
        }
        composeTestRule.waitForIdle()
    }

    @Test // JUnit4 Test Import
    fun `Should show Hello, Desktop`() {
        composeTestRule.onNodeWithText("Hello, World!").performClick()
        composeTestRule.waitForIdle()
        composeTestRule.onNodeWithText("Hello, Desktop!").assertExists()

    }
}
```
