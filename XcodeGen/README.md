# XcodeGen - A better way to manage Xcode Projects
## Generating xcodeproj’s with Xcodegen
Get rid of unreadable xcodeproj files and say hello to readable project configuration files

# **The problem**
1. .xcodeproj files suck
2. They aren’t human readable
3. When merge conflicts do occur this makes them pretty impossible to resolve

# **The Current “Solution”**
**Adding this line to your .gitAttributes**
```
*.pbxproj merge=union
```
This attribute tells git that whenever there is a merge conflict with any .pbxproj file then **merge automatically** and take **both sides**.
Nine times out of ten this will work fine. However when it dosen’t things go south real quickly.
Depending on the size of your project you can end up with hundreds of seemingly insolvable conflicts where blocks of code end up where they shouldn’t. If you have ever experienced this you know it can quickly become a nightmare.

# XcodeGen

XcodeGen is a command line tool that generates your Xcode project using your folder structure and a simple project spec.

With XcodeGen you create Project Specs which can either be in **JSON** or **YML**. These specs contain all the information to generate a project. Targets, Schemes, Settings, Dependencies.

Xcodegen allows you to store your project configuration in a YAML formatted file. Xcodegen then generates the xcodeproj files based from the YAML file.
[full specification for the YML file](https://github.com/yonaskolb/XcodeGen/blob/master/Docs/ProjectSpec.md#options)

After creating the Spec you simply run:
```
xcodegen
```

**Remember to tell git to ignore the xcodeproj files once you ready to use Xcodegen.**

## Summary 
✅ Xcodegen simplifies complicated to read xcodeproj files in project configuration YAML files. \
✅ Pull Requests/Merge Request are easier to read and follow. \
✅ Conflicts in the project.yml are easier to resolve. \
✅ Generate projects on demand and remove your .xcodeproj from git, which means **no more merge conflicts!** \
✅ Groups and files in Xcode are always **synced** to your directories on disk. \
✅ Easy **configuration** of projects which is human readable and git friendly. \
✅ Easily copy and paste **files and directories** without having to edit anything in Xcode. \
✅ Share build settings across multiple targets with **build setting groups**. \
✅ Automatically generate Schemes for **different environments** like test and production. \
✅ Easily **create new projects** with complicated setups on demand without messing around with Xcode. \
✅ Generate from anywhere including on **CI**. \
✅ Distribute your spec amongst multiple files for easy **sharing** and overriding. \
✅ Easily create **multi-platform** frameworks. \
✅ Integrate **Carthage** frameworks without any work. \
✅ Export **Dependency Diagrams** to view in [Graphviz](https://www.graphviz.org/). \

[ProjectSpec](https://github.com/yonaskolb/XcodeGen/blob/master/Docs/ProjectSpec.md)


## How to add Swift Packages using Xcodegen

One of the most popular dependencies managers used in iOS development is **Swift Package Manager**.
In this section, I will show you how to import a popular open-source library used in iOS development: **Alamofire.**
Open **project.yml** at the top level after options: section add the following:

```
packages:
  Alamofire:
    url: https://github.com/Alamofire/Alamofire
    majorVersion: 5.5.0
```
Above we added the package at a project level. However, we haven’t linked Alamofire to our SaladMaker app target. Let’s do that next. Under the SaladMaker target add the following:

```
dependencies:
  - package: Alamofire
```
Next, run xcodegen and then open SampleApp.xcodeproj in Xcode. In terminal run the following commands:
```
xcodegen && open SampleApp.xcodeproj
```

## How to change build settings
```
settings:
  ENABLE_BITCODE: NO
```

## Another way to run
```
xcodegen generate --spec project.yml
```

## References:-

https://medium.com/freelancer-engineering/xcodegen-a-better-way-to-manage-xcode-projects-3359d2a31d86

https://swiftpackageindex.com/yonaskolb/XcodeGen

https://github.com/yonaskolb/XcodeGen

https://betterprogramming.pub/generating-xcodeprojs-with-xcodegen-7d291cfc2f46
