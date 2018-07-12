# cucumber-java-references
cucumber run with java and spring integration quick notes

## How to setup a cucumber test project with java
[Steve Fenton getting started with bdd intellij](https://www.stevefenton.co.uk/2015/01/getting-started-with-bdd-intellij/)

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





        
