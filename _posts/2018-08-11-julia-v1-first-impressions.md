---
layout: post
title: Julia v1.0 First Impressions
author: Diana Cai
tags:
- Julia
- programming
- misc
summary:  The Julia Programming Language has finally released version 1.0! I was still using version 0.6 when pretty much suddenly both v0.7 and v1.0 came out (thanks JuliaCon). So I didn't get to actually try out a lot of the new features until now. Here I'll document the installation process and some first impressions.
---

The [Julia Programming Language](https://julialang.org/) has finally released version 1.0!
I was still using version 0.6 when pretty much suddenly both v0.7 and v1.0 came out within a day apart (thanks JuliaCon).

<div>
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Woohoo 🎉🎉🎉 <a href="https://t.co/XL7aZNRpD7">https://t.co/XL7aZNRpD7</a></p>&mdash; Diana Cai (@dianarycai) <a href="https://twitter.com/dianarycai/status/1027301960196808709?ref_src=twsrc%5Etfw">August 8, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
<br />
</div>

As a result, I didn't get to actually try out a lot of the new features until now.
Here I'll document the installation process and some first impressions.
On the Julia website is a nice [blog post](https://julialang.org/blog/2018/08/one-point-zero) on new features of Julia 1.0.
They recommend installing v0.7 first, which contains deprecation warnings, fixing those warnings, then upgrading to 1.0.

Why is 1.0 so exciting? From the blog post linked above, it says

> The single most significant new feature in Julia 1.0, of course, is a commitment to language API stability: code you write for Julia 1.0 will continue to work in Julia 1.1, 1.2, etc. The language is “fully baked.” The core language devs and community alike can focus on packages, tools, and new features built upon this solid foundation.


## Installing Julia

I haven't been using Homebrew to install Julia since v0.5, and so I decided to
go with that again this time. The first thing I did was download and install
Julia from the website, and then create the symlink:

```bash
sudo ln -s /Applications/Julia-1.0.app/Contents/Resources/julia/bin/julia /usr/local/bin/julia
```

Now typing in ```julia``` into the command prompt brings up the 1.0 REPL. The
new REPL now starts up noticeably faster than before.

I compared the startup time: for version 1.0, we have

```bash
~ $ time julia -e ""

real    0m0.360s
user    0m0.114s
sys     0m0.153s
```

and for version 0.6, we have

```bash
~ $ time /Applications/Julia-0.6.app/Contents/Resources/julia/bin/julia -e ""

real    0m0.829s
user    0m0.306s
sys     0m0.237s
```


## Installing Packages in the REPL

Next up is installing packages that I need for work. The first thing I always do
is install IJulia, and so after trying ```Pkg.add("IJulia")```, I was
immediately reminded that there is now a new package manager.

To access [Pkg](https://docs.julialang.org/en/latest/stdlib/Pkg/), the new package manager,
press the ```]``` key in the REPL. Then we just type the package name at the
prompt, e.g.,

```bash
(v1.0) pkg> add IJulia
```
Multiple packages can be installed in each line by specifying ```add Pack1 Pack2
Pack3```. Typing ```help``` will display a list of commands. To return to the ```julia>``` prompt, press backspace on an empty prompt or Ctrl+C.


Now IJulia is installed. After starting up ```jupyter notebook``` and confirming
that the v1.0.0 kernel was present, I then proceeded to install my usual packages:

1. Distributions, StatsBase - for basic probabilistic modeling and statistics
2. Seaborn (which installs all the Python dependencies) - plotting built on PyPlot (and PyCall to Matplotlib)
3. Optim - optimization package
4. Calculus, ForwardDiff - computing derivatives
6. DataFrames, CSV - for reading data, saving and loading experimental results

The installation process was quite fast for each package. Overall, I like the
simplicity of the interface for the new package manager.

While I was able to successfully install all of the packages above, I wasn't able to
successful install a few packages that either hadn't yet upgraded to v0.7 or had
some dependency that hadn't yet upgraded.

Thus, if your work depends heavily on certain packages that have yet to be
updated, it may be worth sticking with v0.6 for a little bit longer.

### Installing packages from Github

However, it's worth checking the package online to see if you can directly download the latest
code from Github. E.g., if you go to the package's Github page and see that
there have been indeed updates for v0.7, then try installing directly from
Github.

After trying to import a few packages (PyPlot and Seaborn), I found that they had import errors during precompilation
(e.g., ```ERROR: LoadError: Failed to precompile LaTeXStrings```), which were
usually due to some issue with a dependency of that package. For example, for PyPlot, I found
that the package LaTeXStrings had indeed made fixes for 0.7, but this seemed to
not be in the latest release, and so I removed the package and added the code on
the master branch on Github:
```
(v1.0) pkg> add LaTeXStrings#master
```
This fixed the issue with both PyPlot and Seaborn immediately in that I could
now import the packages.

However, I wasn't able to get the plot function to actually work initially.
After adding PyCall#master, I was able to get PyPlot and Seaborn
both working in both the REPL and Jupyter notebooks.

As in the old package manager, we can still install unregistered packages by
adding the URL directly, which is really nice for releasing your own research code for others to use.


## Final Thoughts

While the Julia v1.0 upgrade was very exciting, because many packages that I
rely on aren't yet 1.0-ready, I'm going to hold off on transitioning
my research work and code to v1.0, and stick with v0.6 for a little longer.
Supposedly the Julia developers will release a list of 1.0-ready packages soon.

From perusing the Julia channel, it seems like many packages are become almost
ready. I plan to check back again in a month or so to see if packages I rely on are
ready for use. Overall, I'm thrilled that v1.0 is finally released, and look forward to using it soon.
