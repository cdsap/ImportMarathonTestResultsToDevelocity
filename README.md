## Importing Marathon test results to Develocity
Example repository showing how to import Marathon test results in a Build Scan.

### Usage
Configure the Develocity API `ImportJUnitXmlReports` in the `build.gradle.kts` where Marathon is applied:
```kotlin
afterEvaluate {
    ImportJUnitXmlReports.register(
        tasks,
        tasks.named("marathonDebugAndroidTest"),
        JUnitXmlDialect.GENERIC,
    )
        .configure {
            reports.from(
                fileTree("${layout.buildDirectory.get()}/reports/marathon") {
                    include("**/marathon_junit_report.xml")
                }
            )
        }
}
```
Assuming that the test task is `marathonDebugAndroidTest`, the test results will be imported in the build scan:
https://ge.solutions-team.gradle.com/s/3rsxjvvrvxep4/tests/overview
