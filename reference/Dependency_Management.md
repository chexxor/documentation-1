
# Purescript Dependency Management

## What is dependency management?

Manually including open-source, community-maintained libraries from the PureScript ecosystem into your project can be rather time-consuming and error-prone, as these libraries are small, can have their own dependencies, and may only build with certain versions of their dependent libraries and PureScript compiler version. There are multiple ways to manage this and several tools which can help solve this problem, each of them having different presumptions and goals.


## Overview of tool options

Following is a list of these tools accompanied by an introduction. Feel free to make a pull request to add missing tools or update existing ones.

### Git and custom dependency manager

It's possible to use Git as a dependency management tool. You'll need to find the PureScript library code repositories yourself, find the release tag you want, and clone them into a directory in your PureScript project. Then, pass the paths to these Purescript libraries to the compiler when building your project.

More information: [guides/Dependency-Management/Git.md](guides/Dependency_Management/Git.md)


### Bower

Bower is a dependency manager whose differentiating features are its supports for soley a flat dependency tree and its ability to refer either to "registered" packages or to other package identifiers like Git URLs. A flat dependency tree is in contrast to NPM, which supports dependencies of arbitrary depth.

Here, a flat dependency tree refers to the location a dependency's dependencies are installed: in child directories within that dependency, or in sibling directories to that dependency. This distinction becomes relevant when considering how to handle two direct dependencies which have on the same dependency. Should you have one copy of that common, transitive dependency installed, or two, one for each direct dependency. The latter is convenient when the direct dependencies require incompatible versions of the third dependency, while the former is convenient for reducing the size of the resulting build artifact, as it doesn't include duplicate libraries.

More information: [guides/Dependency-Management/Bower.md](guides/Dependency_Management/Bower.md)

### NPM

NPM is a dependency manager whose differentiating features are its history with the NodeJS ecosystem and its support for a dependency tree of arbitrary depth, which is a feature of the NodeJS module system, CommonJS. It's important to note that NPM has recently added support for "deduping" an application's dependency tree, but only as a storage space optimization. PureScript requires a flat dependency tree, as the compiler will fail when it is given two modules having the same name, which means a single PureScript project can't have two versions of the same module. In addition to modules, a data type in a module must have only one implementation, i.e. `Foo` from `MyModule.Foo#v1.0.0` cannot coexist with `Foo` from `MyModule.Foo#v2.0.0`. This prevents a library giving you a `Foo` from v1 and passing it to a function which accepts a `Foo` from v2. For more information, see [Harry Garrood's "Why the PureScript community uses Bower"](http://harry.garrood.me/blog/purescript-why-bower/) blog post.


### Yarn

Yarn is an alternative implementation of the NPM package's dependency resolution algorithm, which aims to be faster and more user-friendly. In addition, it claims to support [declaring a flat package](https://yarnpkg.com/en/docs/package-json#flat-), but there are currently no reports of this satisfying the requirements of a PureScript dependency manager.


### PSC-Package

!!! to do

### Purcell

??? too soon?