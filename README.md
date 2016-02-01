# library-config-test
Presents a configuration situation that I can't figure out how to test.

My scenario
====

What I'm trying to do is conceptually simple.  I want to be able to declare a particular class in a library project, meaning not a spring boot app.  This library will then become a library for other projects; meaning application B (a spring boot app) declares a dependency on library A.

The dependent application will then want to configure multiple instances of this class via application.properties (or yaml).

What I'm having trouble with
====

I can't seem to figure out how to test this scenario in the library application.  The test package contains a single test case that attempts to autowire a @Component and verify the contents of it, which is an instance of a pojo (Car for this sample).  The instance should be configured from the yml file found in the test/resources folder.

When I run the test case...

```
gradlew -Dspring.profiles.active=ci test
```

...the test case fails, saying one of the properties is null.  You can browse the test report at:

```
./build/reports/tests/index.html
```

Click into the details of the failed test, and then click the **Standard Output** link.  It shows the gory detail of the test run.  You'll notice that it finds the yml file and even prints the full contents of it in the debug log.  It also shows that it finds the **DanCarProperties** component.

What's missing in the test is that it is not properly loading the data from the yaml file into the autowired instance.

What I'm missing is what I'm doing wrong.



The challenge
====


I challenge you guys to figure out what I'm doing wrong.  I'll buy your first (and likely more) beer when you solve this seemingly simple problem.

The goal is to get the one test case to pass.
