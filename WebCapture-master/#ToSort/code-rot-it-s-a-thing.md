# Code Rot - It's a Thing

_Captured: 2017-05-01 at 20:46 from [dzone.com](https://dzone.com/articles/code-rot-its-a-thing?edition=293882&utm_source=Daily%20Digest&utm_medium=email&utm_campaign=dd%202017-05-01)_

Reduce testing time & get feedback faster through automation. Read the [Benefits of Parallel Testing](https://dzone.com/go?i=124039&u=http%3A%2F%2Finfo.saucelabs.com%2Fpaper-benefits-of-parallel-testing.html%3Futm_campaign%3Dparalleltestingwp%26utm_medium%3Dtextlink%26utm_source%3Ddzone-agile), brought to you in partnership with [Sauce Labs](https://dzone.com/go?i=124039&u=http%3A%2F%2Finfo.saucelabs.com%2Fpaper-benefits-of-parallel-testing.html%3Futm_campaign%3Dparalleltestingwp%26utm_medium%3Dtextlink%26utm_source%3Ddzone-agile).

In my experience, code can rot in two distinct ways. The first case isn't where the code hasn't been used in a long time, but where the environment has changed so it is no longer possible to run the code. In the second case, the code still works but has gradually become complicated and hard to work with. The first case is unusual, but straightforward to fix. The second case is very common, but unfortunately hard to fix if left for too long.

![](https://henrikwarne1.files.wordpress.com/2017/04/dsc_3078.jpg?w=477&h=269)

## Type 1 - Changed Environment

One type of code rot happens when a module of code isn't used in the system for a while (typically for months or years). For example, it can be some existing functionality that isn't needed or requested anymore. So it is not included when compiling and building the software. However, suddenly it is needed again. Maybe a new customer needs the functionality that it implements. Or maybe it is needed as a basis for developing new functionality.

At this point, more often than not, there have been changes to the environment in which the module will be used. Even though** the module itself hasn't changed at all** since it was last used in production, the code has rotted, since it no longer fits in its surrounding environment. The environment can have changed in a lot of ways. The libraries it depended on may not be supported anymore, so an upgrade is necessary. Maybe the build steps have changed. Maybe the internal APIs have evolved.

This form of code rot is not that common in my experience. It is unusual to remove a module, and even more unusual to later need it again. But it does happen. When it does, it is not that difficult to fix. You just have to work through all the incompatibilities one by one, adapting the module to the new environment. Tedious, but not difficult.

## Type 2 - Gradual Decay

The more common type of code rot is the gradual decay of the code. Like type 1, it happens incrementally, but this code is actively used in the program, so it is up to date with the environment. Instead, this code rots by slowly getting worse in small details. Each individual degradation may not be cause for alarm, but taken together they have a significant impact. This type of code rot is in almost every code base to a varying degree.

A common form this problem takes is when **changes are just added on to the existing code**, without considering the bigger picture. For example, a conditional statement may have started out as a simple if-then-else case. After it has been extended many times (often by different people) it may end up like this:

This is now almost impossible to understand. Each new change only added one specific case that made sense in isolation, but the cumulative effect is disastrous. It needs to be divided up differently to be easier to understand.

Another very common way code rots by incremental changes is when you get **very large method bodies**. As more and more logic is added, a method that started out small grows and grows to become up to several pages long. Often it includes if-statements or loops that contain larger and larger chunks of logic as well. If all the necessary logic had been known from the beginning, the code would likely have been split up into several smaller methods. But because it was extended piece by piece, nobody made the effort to split it up.

A third example is **misnamed methods** (and variables and even files). As changes accumulate in what a method does, the name may no longer fit. So it is quite common with method names that are either plain wrong or that don't tell the whole truth about what the method does.

### Why Does It Happen?

I don't think any developer sets out to make the code base worse. Often it just happens as a by-product of adding or changing a feature. Unless you pay attention, it is easy to make the code rot a tiny bit in the process. I can see at least six reasons why this happens (many of them overlapping):

**Following the existing pattern.** In the example with the if-statement above, it is easy to just add on one more case to get the new desired functionality. It is more work to take a step back and see if the code needs to be restructured to better accommodate the intended change.

**Unfamiliar code.** When you don't know the code you are changing very well, you are more inclined to change as little of it as possible.

**Making the smallest possible change.** The more you change the existing working code, the greater the risk of introducing bugs (even when you know the code well). To minimize that risk, you tend to make the minimal change, which often contributes to the overall code rot.

**Time pressure.** When you feel that you have to finish a feature soon, you may opt to make the smaller and faster modification, rather than the bigger change that would also improve the overall structure of the code.

**No clear point at which it happens.** Since the code gets worse in small incremental steps, there is no clear point at which the problem must be dealt with. One more change surely will not make the code bad, will it?

**Inexperienced or indifferent developers.** Sometimes the developer making the change doesn't know better or doesn't care enough about the long term code quality.

### What Should Be Done?

Code rot is like weeds in the garden - the earlier the problem is dealt with, the easier it is to overcome. The longer you leave it, the harder it is to fix. This is especially true for parts of the code that should really be separated, but which have been mixed together in one method or one file. It is quite easy to combine things together, but it can be incredibly hard to break the separate pieces apart.

The only solution I see to the problem of code rot it to be aware of the problem, and to make regular small fixes to avoid it getting out of hand. However, code rot has a tendency to sneak up on you, so that is easier said than done. I am as guilty of contributing to code rot as the next developer. Part of the reason for writing this blog post is simply to become more aware of the problem myself.

## Conclusion

Code rot is the degradation of the code base over time. The gradual decay (type 2) is the more difficult case. It is both hard to spot and hard to combat since it happens bit by bit. However, if not dealt with in time, it is quite hard to fix. In my opinion, code rot is the most common problem with most code bases. The only solution I know of is awareness and regular small fixes. What is your experience with code rot? Do you agree it is a common problem? How do we fix it? Please let me know in the comments.

The Agile Zone is brought to you in partnership with [Sauce Labs](https://dzone.com/go?i=121022&u=http%3A%2F%2Finfo.saucelabs.com%2FHow-to-Get-the-Most-out-of-CICD-Workflow.html%3Futm_campaign%3Ddevops%2Bwp%26utm_medium%3Dtextlink%26utm_source%3Ddzone-agile). Discover how to optimize your DevOps workflows with our [cloud-based automated testing infrastructure](https://dzone.com/go?i=121022&u=http%3A%2F%2Finfo.saucelabs.com%2FHow-to-Get-the-Most-out-of-CICD-Workflow.html%3Futm_campaign%3Ddevops%2Bwp%26utm_medium%3Dtextlink%26utm_source%3Ddzone-agile).
