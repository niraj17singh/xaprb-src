---
title: "The Erlang Response Time Stretch Factor For 3 And 4 Servers"
date: 2016-12-11T15:57:16-05:00
url: /blog/erlang-stretch-factor-three-four/
description: "In which I explore the divergence between the Erlang C formula and Gunther's heuristic approximation."
credit: "https://unsplash.com/photos/_NNsOxgemgg"
image: "/media/2016/12/unsplash-photos-_NNsOxgemgg.jpg"
thumbnail: /media/2016/12/unsplash-photos-_NNsOxgemgg.tn-500x500.jpg
classes:
- feature-figcaption-visible
- feature-fignum
- feature-figlink
categories:
- Math
- Scalability
---

In a [previous post](/blog/response-time-stretch-factor/) I explored a few
variations of equations that express the M/M/m queueing theory response time
"stretch factor," and tried to indicate some areas where I wanted to dig into
the relationships between these formulas a bit more. In this post I discuss the
divergence between the official Erlang C formula and Neil Gunther's heuristic
approximation to it. I introduced this before thusly:

> At {{< math >}}m=3{{< /math >}} and above, the heuristic is only approximate. What does the Erlang
> form reduce to for the first of those cases? Does it result in the missing term
> that will extend to 4 and beyond too?

<!--more-->

Here's the Erlang form again:

{{< math >}}
R(m, \rho) = 1 + \frac{ \frac{(m \rho)^m}{m!} }{ (1-\rho) \sum_{n=0}^{m-1} \frac{(m \rho)^n}{n!} + \frac{(m \rho)^m}{m!} } \frac{1}{m(1-\rho)}
{{< /math >}}

And the equivalent heuristic by Gunther, which is exact for 1 and 2 service
channels:

{{< math >}}
R(m, \rho) \approx \frac{1}{1-\rho^m}
{{< /math >}}

Note that this is a stretch factor relative to the service time, i.e. to find
the average residence time, you must multiply by the service time.

When {{< math >}}m{{< /math >}} is 1 or 2, the Erlang formula simplifies exactly to the heuristic.
When {{< math >}}m=3{{< /math >}}, the Erlang formula simplifies to:

{{< math >}}
R(3, \rho) = 1 + \frac{3\rho^3}{(1-\rho)(3\rho^2+4\rho+2)}
{{< /math >}}

It's not immediately obvious to me how that might be related to the heuristic
form of the response time stretch factor, {{< math >}}\frac{1}{1-\rho^3}{{< /math >}}.

At {{< math >}}m=4{{< /math >}}, the Erlang formula simplifies to

{{< math >}}
R(4, \rho) = 1 + \frac{8\rho^4}{(1-\rho)(8\rho^3+24\rho^2-15\rho+15)}
{{< /math >}}

The relationship between this and {{< math >}}\frac{1}{1-\rho^4}{{< /math >}} is is no more
obvious to me. Importantly, I think, at this point the Erlang formula and the
heuristic start behaving very differently. With 3 service channels, the formulas
have essentially the same shapes (same poles, etc), but there's a slight ripple
in one that's not in the other.

![The Erlang and heuristic queueing formulae at m=3, and the error between them](/media/2016/12/erlang-vs-heuristic-m-3.png)

But with 4 service channels they're
fundamentally different over portions of their range (outside the physically
meaningful performance region of {{< math >}}0<=\rho<=1{{< /math >}}, that is).
Figure 2 shows the same graphs, but for 4 service channels.

What is the error in the heuristic for 3 and 4 service channels? I touched on
this briefly in the previous post. By subtracting the heuristic from the
Erlang formula and simplifying, I found that when there are 3 service channels,
the difference is

{{< math >}}
\frac{\rho^3}{3\rho^4+7\rho^3+9\rho^2+6\rho+2}
{{< /math >}}

But with 4 service channels, the difference between the functions isn't
expressible neatly, and is sometimes infinity, reinforcing the impression that
the coincidence between Erlang and heuristic is just that.

![The Erlang and heuristic queueing formulae at m=4, and the error between them](/media/2016/12/erlang-vs-heuristic-m-4.png)

I still feel that something useful is hiding just around the corner, because the
heuristic arises analytically but doesn't scale correctly to more than 2 service
channels, and Erlang also arises analytically but is correct. The fact that they
are exactly the same for 1 and 2 service channels just doesn't feel accidental.
But intuition has led me astray many times.

You can graph and visualize all of the above with a [Desmos
calculator](https://www.desmos.com/calculator/dx7syiudvb) that I made for you.
