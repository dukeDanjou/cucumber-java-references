# cucumber-java-references
cucumber run with java and spring integration quick notes

## How to setup a cucumber test project with java
[Steve Fenton getting started with bdd intellij](https://www.stevefenton.co.uk/2015/01/getting-started-with-bdd-intellij/)

1. Maven dependencies

*note: cucumber-java8 is not required it allows you to use lambda steps definition*

```
<dependency>
  <groupId>io.cucumber</groupId>
  <artifactId>cucumber-junit</artifactId>
  <version>${cucumber.version}</version>
  <scope>test</scope>
</dependency>
<dependency>
  <groupId>io.cucumber</groupId>
  <artifactId>cucumber-java</artifactId>
  <version>${cucumber.version}</version>
  <scope>test</scope>
</dependency>
<dependency>
  <groupId>io.cucumber</groupId>
  <artifactId>cucumber-spring</artifactId>
  <version>${cucumber.version}</version>
</dependency>
<dependency>
  <groupId>io.cucumber</groupId>
  <artifactId>cucumber-java8</artifactId>
  <version>${cucumber.version}</version>
  <scope>test</scope>
</dependency>
```
2. Define a runner 

The runner below run features in src/test/resources/features, with steps defs and hooks in com.your.company.steps.package, create an html report in target/cucumber directory and skips @wip tagged features/scenarios. 

```
@RunWith(Cucumber.class)
@CucumberOptions(
        features={"src/test/resources/features"},
        glue = {"com.your.company.steps.package"},
        plugin = {"pretty", "html:target/cucumber"},
        // skip WIP features
        tags = {"~@wip"}
)
public class RunAllFeatures {}
```

## Using cucmber with spring injection 

1. Add maven dependency 

```
<dependency>
  <groupId>io.cucumber</groupId>
  <artifactId>cucumber-spring</artifactId>
  <version>${cucumber.version}</version>
</dependency>
```
2. Declare bean context configuration on top of step class 

```
@ContextConfiguration(classes = SpringConfiguration.class)
public class YourStepdefs {
...
}
```
3. Using "World" bean/component

If you want to inject a common instance between your steps definitions class, you can declare a @component scenario scoped. ie a bean that will be instantiate at the beginning of a scenario and destroyed at the end of each scenario. You will need to use the cucumber-glue scope.

```
@Component
@Scope("cucumber-glue")
public class World {
...
}
```
## Using natural language for date 

In order to use natural language in you features like so : 

```
Scenario: Scheduling a 90-day Review
Given an employee is hired "today"
When I schedule a review
Then the review should be scheduled "in 90 days"
```
[look at natty](http://natty.joestelmach.com/)
