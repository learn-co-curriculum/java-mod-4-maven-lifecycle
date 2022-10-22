# Lifecycles, phases, and goals

## Learning Goals

- Define the relationships between Maven Lifecycles, Phases, Goals, and Plugins

## Introduction

A Maven build follows a clearly defined process to deploy and distribute a project.  

- A **lifecycle** is defined by a list of phases. 
- A **phase** represents a stage of a lifecycle and consists of one or more goals.
- A **goal** represents a fine-grained task that may be bound to zero or more build phases.
- A **plugin** is an artifact that provides goals.

Confused? Let's explore the relationship between lifecycles, phases, plugins, and goals.

## Lifecycles

Maven has three built-in build lifecycles. Each lifecycle consists of a sequence of phases.

- default: the primary lifecycle responsible for project deployment.
- clean: removes all files generated by the previous build.
- site: creates the project's website documentation.

We will primarily focus on the default lifecycle as that is responsible for
project deployment.  

### Phases

A Maven phase represents a stage in a lifecycle.
Each phase is a sequence of goals, and each goal is responsible for a specific task.

The default life cycle consists of
[23 phases](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html#Lifecycle_Reference)

The image below shows the first 15 phases up to **test**.
The phases are executed sequentially.  If the `test` phase is
executed, all phases before it must execute.

![default life cycle phases](https://curriculum-content.s3.amazonaws.com/6002/creating-a-maven-project/defaultlifecycle.png)

Consider what must happen to run a Junit test.
The Junit test class must be compiled before we can
execute the test. The compiled code goes in a
test directory that must be generated prior to compilation.
The compiler also performs some post-compilation processing
to optimize the bytecode.
Since a Junit test class is designed to test the
methods of a source code class, the source
code must also be compiled, necessary resources
generated, and post-compilation processing performed. 

It would be tedious to do all of these steps
manually.  A build system automates
much of the process by providing a
lifecycle of clearly defined phases.

Let's explore some of this using IntelliJ's Maven Tool Window,
which can be opened either by clicking on "Maven" along
the edge of the IntelliJ window, or by selecting ** View | Tool Windows | Maven**
from the main menu.
  
![maven tool window](https://curriculum-content.s3.amazonaws.com/6002/creating-a-maven-project/maventoolwindow.png)

Expand the Lifecycle folder to see the phases available for execution. 
The *clean* and *site* phases are not part of the default lifecycle, but
rather phases from other built-in lifecycles.

### Plugins and Goals

Expand the Plugin folder to see the plugins and goals.
When we run a phase, all goals bound to the phase are executed.

For example:
- **compiler:compile** - *compile* goal from
  the *compiler* plugin is bound to the *compile* phase
- **compiler:testCompile** - *testCompile* goal from
  the *compiler* plugin is bound to the *test-compile* phase

Each plugin has a help goal.  Select the **clean:help** goal and then
press the green run button at the top of the Maven build window
to execute the goal.  The console will display documentation
about the two goals **clean:clean** and **clean:help** that are
part of the Apache Maven clean plugin.

![clean plugin help](https://curriculum-content.s3.amazonaws.com/6002/creating-a-maven-project/cleanhelp.png)

A phase may consist of multiple goals. Running a single goal
does not run the entire phase, nor does it run the goals
in the preceding phases. 
  
To execute all goals in a phase (and preceding phases),
select the phase in the LifeCycle folder and press run.

![running a phase](https://curriculum-content.s3.amazonaws.com/6002/creating-a-maven-project/runningphase.png)
 

## Building a project

Let's see how IntelliJ builds the project when we change the code
and need to recompile. 

Edit the `main` method to print "Hello" instead of "Hello World!", then:

1. Press the build icon on the bottom toolbar to display the build view.
2. Press the build icon on the top toolbar or
   select **Build | Build Project** from the main menu to build the project.  

![build](https://curriculum-content.s3.amazonaws.com/6002/life-cycles-phases-and-goals/build.png)

Building from the main menu executes the **compile** phase.
Notice all the tasks that are performed to compile!  
Running the build again results in fewer tasks if
the source code has changed since the last build.

We use the Maven tool window if we need to build a different
phase such as **install** or **deploy**.

## Running the project

Normally we don't worry about build system lifecycles,
phases, plugins, goals.  We usually just run
the program and see the output.  But behind the
scenes, IntelliJ uses a build system to make
sure the code is compiled, necessary libraries and
resources are available, etc.

Let's run the `main` method to how the build process is triggered:

1. Edit the `main` method and change the code to print "Goodbye".  
2. Press the run button on the toolbar or select **Run | Run** from the main menu.

Since we've changed the source code, the project must be rebuilt
before we can run the code. We can see in the build view the
tasks of the **compile** phase are performed prior to running
the `main` method.


## Conclusion

A Maven build follows a clearly defined process based on phases of a lifecycle.
Each phase requires one or more goals to execute.
Goals are provided by plugins.

## Resources

[Maven Life Cycle](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html)
