---
title: Safety = Freedom
subtitle: Worse is Faster, Safe is Better
---

I have long held the belief that in programming, unlike politics,
*safety = freedom* (but I only 
[recently](https://www.reddit.com/r/rust/comments/3mofy0/when_rust_makes_sense_or_the_state_of_typed/cvgpwke) 
found this succinct formulation). If you feel safe doing something, you're free 
to do it. Conversely, your fears of doing something will at least slow you 
down, if not stop you in your tracks completely.

I think this is also at least one big underlying reason of the 
[Worse is Better](http://www.dreamsongs.com/RiseOfWorseIsBetter.html)
phenomenon: The New Jersey cowboy coders, who have no qualms doing things in 
their code that would make Bjarne Stroustrup go a little pale around the nose, 
are simply faster to the finish line, with programs that work, mostly.

## Cowboys and AOLiens

This worked beautifully during the advent of the Internet. We were all a big 
family, no one tried to attack anyone else (except for AOLers, but they were 
mostly left to their own devices), and code that mostly ran was Good Enough™. 
Alas! The Times They Are A-Changin' and before you can say knife we have a 
plethora of unpatched security holes in the wild. The cowboys are now riding 
ticking time bombs and wonder *when*, not *if* they'll blow up.

So if you're now feeling like you're standing on a minefield and wonder how you 
got there, this is the reason (As an aside, this also fuels the hate some 
harbor against C and C++). I'm not telling this to sow hate. I've been there 
and done that personally, so I share at least some of the blame. Also let's not
forget that those languages brought us a wealth of useful software, and their
contribution, averaged out over about four decades, is very probably positive.

The New Jersey style also could be related to the big differences in 
productivity between programmers: Our measurements are by definition imprecise 
and as usual, taking risks awards big payoffs, if all goes according to plan. 
Perhaps the 10× guys really are just romanticized cowboy coders after all (Then 
again, I *do* know people who can only code a tenth of what I do at a time – am 
I secretly a cowboy after all?).

Meanwhile us normal (some would say mediocre) programmers slave away on our 
keyboards to write something that works in all cases, without too many crashes 
or security holes. Of course we go slower than the cowboys, because we care 
about more stuff while they ride the open range on their time bombs. To an
uninformed outsider it looks like they are coding circles around us.

The better of us are trying to push out of their comfort zone, do some HPC
stuff, learn a few more languages. And let me tell you, C/C++ are scary places.
It's dangerous to go there alone. Here, take this `shared_ptr`.

## Enter Rust

Here comes a language that promises fast, safe, concurrent. Isn't
that three things at once? It is. Does that sound too good to be true? Of 
course. Is it? Well, not really. There's a catch, though; the compiler is the
strictest I've ever had the pleasure to work with, and the learning curve is
quite steep. However, the compiler is at least as helpful as it is strict, and
the community is, in the immortal words of Bill&Ted, excellent to each other.

The language has some rough edges, being just a few months since it's 
much-publicized 1.0.0 release. There are traits defined for arrays of size zero 
to 32, and zero- to 32-sized tuples. Want a clone of a 33-element tuple? Sorry, 
I cannot do that, Dave. About half of the thing is "unstable" scaffolding, just 
there to build the compiler (and off-limits to all but users of the "nightly" 
version, which gives the "unstable" its meaning). The whole thing screams "you 
haven't even seen my final form", and having learned it for the last months, 
I'm optimistic about the future.

Rust gets its **safety** from a few features working together. The type system 
lets us encode certain things about ownership and lifetimes of objects – things 
which C++ programmers have to keep in their heads. The Borrow Checker ensures 
that no two parts of the code can change a state within the same scope, whether 
concurrently or serially (it also ensures that no code can mutate it while 
another one is looking at it). This is sometimes just a bit cumbersome because 
of course the checks are sometimes overbroad, but mostly you don't notice it at 
all until it politely tells you when you're doing something stupid.

Some parts of the standard library purposefully cut holes into that safety 
blanket to let low-level things go fast, yet supply a safe interface on top of 
that. I sure hope this stuff gets a thorough audit every now and then, but 
mostly it looks quite sensible.

Ok, so it's safe, but is it **fast**? That very much depends on what you're 
doing with it (and of course your mileage may vary), but the measurements I've 
made so far paint a very hopeful picture. In 
[certain benchmarks](http://benchmarksgame.alioth.debian.org/u64q/rust.html), 
Rust shows very competitive results, which would be surprising for such a young 
language were it not for the fact that the compiler builds on the mature LLVM 
backend, which gives it a great optimizer which Rust relies on quite heavily.

On the **concurrency** side, Rust frees us from data races. The runtime is 
based on native threads, which sounds curious for a high-performance language, 
until one learns that green threads actually were part of the runtime until 
they were ripped out because they apparently weren't lean enough for the 
embedded folks who wanted to use Rust. Some may lament the loss, but it mostly 
works OK. Some coroutine-using libraries have already emerged to fill the gap.

The first IDEs are appearing, a few web frameworks have sprung up, and
apparently there's a very active game developer community around Rust. Judging
from my experience with Lua (which has seen a similar uptake by game devs),
this is a good sign.

## No Risk, Have Fun!

Rust lets me code at a low level without fear of breaking things. I'm not a
irredeemable bomb-jockey after all; I have kids to feed. When programming
Rust, I *feel* like a great coder, even if I have just graduated from newbie to 
someone who mostly knows his stuff.
