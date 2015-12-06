---
layout: post
title: Upgrading your codebase and staying fresh
---

In the first part of the mini-series (1/2) dealing with upgrading code, libraries or tools we will go over the process of upgrading your whole codebase from a general point of view, applicable to any kind of language or framework. We will discuss how to get ready for it, persuade others and what you might encounter on this journey. I will provide you with arguments, why I believe that upgrading should be a continuous process, which can reduce costs in the long run. In the second part we will take a closer look into upgrading app from  Rails 3 to Rails 4, and what to expect from Rails 5.

### Reasons to upgrade or why to upgrade?
The reasons that you want to upgrade your codebase to the latest versions of your language or framework - there are plenty of them. Maybe you would like to try out the new feature of your language/tool - websockets, lambda expressions (java 8), native json support ([mysql](https://dev.mysql.com/doc/refman/5.7/en/json.html)), fix slow performance, improve the security .. or you just want to be ready for the future.

*Lambda expressions in Java*

```java
Predicate<Integer> isOdd = n -> n % 2 != 0;
```

On a second thought, why break something that works? This might be the question that probably your management or some conservative peers will ask you. Every upgrade brings in a certain risk - is the release really stable, wouldn't it break compatibility between your dependencies?. These are risks, which the open source community and tools that are available as of today (bundler, maven, sbt) cover pretty good. Anyways, you are bringing new equipment into the battle, which flaws you might only discover in your specific production environment (the luckier ones on staging/QA). Well on the first sight, they do have a point - if your app is something where you are not expecting any major changes to be made, then there really might be no reason to do this. But think about situations like major security vulnerabilities in your language  and .. Oops! your 3 years old version is no longer supported and the fix won't be backported. What about if Heroku decides to stop supporting certain versions .. you wanted to upgrade a simple footer text, but now you are out of luck, because you cannot push with your versions. So ..

![_config.yml]({{ site.baseurl }}/images/upgrade_update_sw_dilbert.jpg)

*source: dilbert.com*

### How to sell this to your team?
I don't believe you would have a hard time persuading the developers within your team with the upgrade. Majority of us trully want to explore the latest cutting-edge technologies and features - and benefit from them. We want to make our lives easier and we are happy to dedicate a bit of time to a admitably little bit daunting task of refactoring. Bigger obstacle would be the management - if you have any. Sooner or later, they have to realize that refactoring is essential part of the development process.

### What you might gain once again?
Now let's take a more detailed look onto the benefits that upgrade can bring. Let's suppose we are upgrading a whole codebase, and not only some component like a database version in here.

#### 1. Easier upgrades in the future

This point is related to the continuity of the process. Generally, the longer you wait, the older version of software you are using, the harder will the upgrade be in the future. With the release of new versions you might encounter blog posts or tutorials dealing with the concrete upgrade. As the time goes by, these blog posts might get lost, they might be out of date or it missleading after few years. The point is, if you accept this as a some essential part of your development process - e.g. on each beginning of month, quarterly etc. check what new versions are available and how can you profit from it - it might be an easier path. The incremental approach itself here is a agile way to do it, when compared with some waterfall style of upgrading once per 3 years. It will reduce the costs of the upgrade in the long run (if you intend to keep working in this system for a longer period of time).

Another important benefit is that by using the latest versions of your language or a  framework, you are able to use the latest libraries which bring in additional functionality. You are simply staying updated with the whole ecosystem and community. This is not really obvious, but what if in 6 months you find some awesome library for implementing custom filtering of the records, exactly matching your needs. The library is utilizing the latest feature of your language (e.g. lambda expressions in the Java). And now what? Boom! You are ready to grab it and use it, because you are staying fresh with the latest versions!

#### 2. Performance boost

This might not apply to everyone, but by continous growth of the users of web and IT in general, there is a huge demand for the speed and efficiency of apps. This results in plethora of performance related upgrades in the software your development is built on. Even if the performance is not a huge factor for you, you can always save couple of bucks off the hardware or SaaS, that you can invest into other places. You can almost bet, that the new release of the language is going to be faster or even in terms of performance in the stable release. 
Majority of the changes are related to the various compiler level optimizations, garbage collector changes or utilizing some new concepts.

#### 3. Security fixes and patches

This might be the most underestimated point. Teams' budgets are tight and commonly there isn't any space for evaluating the security of applications - which is a major flaw. Lot of frameworks are working really hard in order to secure their users in areas like SQL Injections, XSS, CSRF etc. All of which nowadays we take for granted. But there are vulnerabilities which didn't go public or you are not familiar with them and you should protect yourself against. Why not to utilize these patches, if they exist? Another example from the future? What if all of sudden your app has to go through some kind of compliance security check or maintain OWASP and you are stuck on a pre historic version of your language? If you used the latest versions, you would be definitely more covered and the whole process would have been faster and easier.

#### 4. Developer hapiness and engagement, innovation

*Ruby 2.3.0 Safe operator*

```ruby
# Ruby 2.2.3
user = User.first

if user && user.profile
puts "User: #{user.profile.nickname}"
end

# Ruby 2.3.0
user = User.first

if user&.profile
puts "User: #{user.profile.nickname}"
end
```
New versions bring new features and enhancements. This adds to the developer comfort and hapiness.
I don't wanna turn this into a discussion about how or whether developers should give back to the community and contribute ot the open source, which they are actively using and relying on. Although, working on a lastest branch of a certain library and when you find a feature missing, immediately firing up a PR is certainly a nice thing and a good feeling for the developer. You suddenly find yourself among the people shaping up that certain piece of software. Instead, I want to emphasise that by using the latest technologies, you can feel secure that your are not staying behind. It is then only a short way to becoming some kind of evangelist, whether it is only internally in your company or within your local community.

### What to expect on this journey and how to prepare?

The upgrade task itself is probably not something that is going to be a popular thing to do in your team. Following some of the tips I will describe, you can make the upgrade a lot smoother and convenint for the whole team. Be prepared to google a lot, change your dependencies/libraries and face numerous obstacles along the way.

- Have a solid code coverage with your tests. If you don't have any tests, then write them first - this is really the essential part. This way even developer without domain knowledge or an external expert can perform the upgrade. Later on you can sleep happily because you know that the upgrade didn't break a thing. Recently, Justin Seals gave an awesome talk in 45mins covering the essentials of a happy test suite.

<iframe style="   display: block;margin: 0 auto;"width="560" height="315" src="https://www.youtube.com/embed/VD51AkG8EZw" frameborder="0" allowfullscreen></iframe>

- Have a clear vision against what branch are you going to be doing the upgrade. Think in the longer terms. It might take a surprisingly long time to truly finish an upgrade of an codebase.

- Choose the iterative way for an upgrade, but be flexible. Don't jump from version `1.0.2` to the latest `5.6.2`. There might be too many changes to be performed at once and you will have a hard time even making the app boot. This helps also on the mental process. Find way that suit your needs, but stick to it, so lets say, you will perform upgrades iteratively on the major versions. This a safer bet, which might take a longer time to accomplish. Is is also easier on the mind, because you will be splitting the task in to smaller subtask, which makes it easier on the progress tracking and mentally, you as a developer, will be happy because of achieving those smaller checkpoints, version by version. Other than that, you can find out that an feature you need was released on an older version, then you thought and for now, you can stay at that concrete version. If you get stuck at a certain version with some issue, try to skip it a jump to the next on the list - your issue might be solved and you are wasting your time.

### How long is it gonna take and how much is it gonna cost?

That's really hard to estimate, I would say that even worse than the esimation of new features. Some systems and applications might be so lucky, that all that you would need to do is just change the version from `2.3.1` to `3.0.0` and you are there. The other end is an application which takes weeks to fix, because you have touched the internals of the frameworks, monkey-patched them and the majority of libraries you have used are no longer supported. The latter is a situation which you can find yourself in easily if you keep pushing the upgrade and refactoring away for a longer period of time.

Sometimes there might be occasions where an external expert can help you speed up this process, which might increase (or decrease) your costs. Especially in case that your team has been working many years, only on that one certain project and they got so sucked in, that they are not aware of the new technologies or features of the language or framework. This is not their failure. If you don't provide them with opportunities to exepriment and try new technologies, then it is hard for the developers to keep up with the fancy new and niche stuff.

### Final thoughts

Now that you have seen the upsides of the upgrade process, it is up to you and your team to decise whether it is worthy of doing it. There is a high probability, that you will encounter many issues on your journey, but these won't be useless - your developers will gain more knowledge, they will be happier and eager to work with the new features provided by the language or framework. 

And what about the continuity of the upgrade process?

> Premature optimization is the root of all evil.

> (Donald Knuth)

You might find yourself thinking about this continuity like .. wait, isn't this an instance of *premature optimization* pehonemnon? Well, you might be totally right! But please, do keep an eye on the new versions of the tools you are using and listen to your developers.

In the second part of this mini-series, we will be going through an upgrade of Rails Application, and we will take a look into what will Rails 5 bring to the table.

