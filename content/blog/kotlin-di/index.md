---
title: "Dependency injection with Kotlin Ktor"
date: 2023-10-03T14:41:09+02:00
draft: false
image: "forest_misty_wide.png"
---


## It´s been a long time...

This blogpost has been a very long time coming, over six months in fact. Not because it would take so long to write in itself, but because I have had a lot of other priorities and creating online content has been put far down the list. The longer time passes between each time I work on the post or any other projects for that matter it seems that the hurdle to overcome seems to be larger and larger every day. Getting started is often the most difficult thing; just taking that first, small step. This is something I feel every day as have side projects I want to keep working on that do not get enough of my time. To improve I need to start getting better at scheduling my time, sticking to it and deliver on the goals I set for myself to achieve. Creating a blog and a developing an online presence is part of my attempt to become something more than just a working developer, I want to share my knowledge and experiences with the world, with you. If my writing can help anyone overcome the problems they are facing or give them a shortcut to the solution they are seeking that would be wonderful. 

## Lets get back on to the business at hand
Now, on to what this post is actually about, which is dependency inversion tools in Kotlin. The reason I started to look into this was because in my current job our applications normally run on a Kubernetes based platform which provides hosting for Kafka, databases, environment variables and other dependencies the application might need to run. However the issue I faced here was that I could not easily run the application locally while programming as long as the application used Kafka. Not without setting up Kafka in testcontainers and playing around with configuration I could get this done locally. Connecting to the development environment would require multiple environment variables that were provided by the platform and those I did not have immediate access to. So the desire to run my application locally prompted the quest to find a way to separate configuration per environment, and utilize dependency injection to make sure everything the program needed to run was loaded in. 

> **Dependency Injection (DI)** is a design pattern that deals with how components or objects acquire their dependencies. The primary goal of DI is to separate the creation of objects from their use, making systems more modular and promoting the principle of inversion of control (IoC). Instead of objects creating their own dependencies or having them hardcoded, they receive the dependencies from an outside source.

The immediate solution that comes to mind is to use Spring Boot which of course is known to heavily utilize dependency injection. The Spring framework provides a container that manages the lifecycle and configuration of application objects. However, this project is using Ktor and the goal was to see how similar DI could be achieved when still using Ktor instead of Spring Boot. 

The primary DI frameworks for Kotlin as of today appears to be Koin, Dagger and Hilt, and Kotlin-inject. While Dagger and Hilt is primarily aimed at Android programming, the Kotlin-inject framework has a Dagger-like API and it provides compile time safety. Which means Kotlin-inject gives you multiplatform support and you have a compile-time dependency graph validation. Koin on the other hand does not, but offer faster build times and is very lightweight. [This comparison of Koin and Kotlin-inject highlights differences](https://infinum.com/blog/koin-vs-kotlin-inject-dependency-injection/), drawbacks and benefits of each.

### Koin

Koin is a pragmatic, lightweight dependency injection framework written in Kotlin. It's designed specifically for Kotlin, making use of its features to provide a straightforward and concise way to manage dependencies.

Here are some key features and aspects of Koin:

1. - **DSL Based:** Koin uses a Kotlin-based DSL for defining modules, making it very readable and expressive.
2. - **No Reflection:** Unlike some other DI frameworks, Koin doesn’t use reflection. This makes it faster and more predictable.
3. - **Scopes:** Koin provides different scopes (like singleton, factory, and scoped) to control the lifecycle of your instances.
4. - **Extensions for Kotlin Features:** Koin has extensions for Kotlin's coroutine support.
5. - **Integration with Popular Frameworks:** Koin offers modules for integration with popular frameworks like Android, Ktor, and Spring.


The GitHub-project can be found here: [https://github.com/InsertKoinIO/koin](https://github.com/InsertKoinIO/koin)

A Ktor quickstart guide is available: [https://insert-koin.io/docs/quickstart/ktor](https://insert-koin.io/docs/quickstart/ktor)

---


### Kotlin-inject

Kotlin-inject is a compile-time dependency injection framework for Kotlin. It aims to provide a simple and effective way to perform dependency injection while ensuring compile-time safety. Since it works at compile-time rather than runtime (like many other DI frameworks such as Dagger or Hilt in the Java world), it can be faster and have a smaller runtime footprint.

Here are some key aspects of kotlin-inject:

1. - **Compile-time Safety:** The main advantage of compile-time DI tools like kotlin-inject is that they verify your bindings at compile time. This means if you make a mistake in your DI setup, you'll be informed during the compilation rather than at runtime.
2. - **Annotation-driven:** Like many DI tools, kotlin-inject uses annotations to mark classes for injection and to define modules.
3. - **Generated Code:** Instead of relying on reflection, kotlin-inject generates code during compilation. This leads to better performance at runtime.
4. - **Kotlin-native:** As the name suggests, it's tailored for Kotlin and leverages Kotlin's features for a clean DI setup.
5. - **Integration with Popular Frameworks:** While primarily a general-purpose DI tool, there might be integrations or plugins that help in using it with popular frameworks or platforms.


The GitHub-project can be found here: [https://github.com/evant/kotlin-inject](https://github.com/evant/kotlin-inject)

This detailed blogpost about kotlin-inject is very informative: [https://proandroiddev.com/from-dagger-hilt-into-the-multiplatform-world-with-kotlin-inject-647d8e3bddd5](https://proandroiddev.com/from-dagger-hilt-into-the-multiplatform-world-with-kotlin-inject-647d8e3bddd5)

---

## So which framework to choose?

Well, it depends what is more important for you, and what you prefer. If you have  experience with Dagger from before then Kotlin-inject may be feel very familiar to you. The drawback here is that the community around the framework is much smaller than the community around Koin. In addition, Koin does have excellent support for Ktor out of the box and is quite straightforward to use. Personally I would lean against Koin as I like what i´ve read about it so far in being lightweight and simple to use. At the time of writing I have not yet had sufficient experience with either to give a hands on opinion on them, but I intend to experiment with both in the coming days. 

