# Learning about the TIC-80

This repository is for notes about my slow process of getting my head around the [TIC-80](https://tic80.com) virtual retrocomputer. Thinking about using it as an exercise in a corporate code dojo, as an incentive to learn; but don't want that to become a synthetic source of pressure. I've always coded in "high level" / abstract languages useful for web / GIS / data science work, like python, Perl and R. I've never had to think about where memory is, what's in it and where it's going. It would be interesting to know!

## The TIC-80

* [TIC-80.com](https://tic80.com)
* [TIC-80 overview on sizecoding.org](http://www.sizecoding.org/wiki/TIC-80)

## Slow steps

You can run a TIC-80 in a web browser, or you can put one on your Android phone. Tried this and didn't like the keyboard affordance. Dug out the 2008-era Thinkpad, reinstalled it with a recent stable version of Debian (ISO on a US B stick) and now it is a host for a TIC-80. 

Had to build it from scratch because the packaged version is x64 specific , followed the [Ubuntu 18.04 install instructions](https://github.com/nesbox/TIC-80#ubuntu-1804) on Debian bullseye and that was ok.

Now we can run `tic80` and what is next?

Each `tic80` program / demo / whatever comes in a file called a "cart" (short for "cartridge"?), so the logical next step is to download other peoples carts and have a look at what they do.

This [collection from blinry](https://blinry.org/50-tic80-carts/) of 50 carts made in a weekend is perfect for that because each of them does a small thing slightly differently. Downloaded a couple of the audio ones and copied them into `.local/share/com.nesbox.tic/TIC-80/` as that's where the `tic80` looks by default (it has `cd` and `dir` commands but will it remember, the next time?)

Now we can tell the `tic80`'s shell 

```
load 19.tic
run
```

And it starts blatting out random bytes as noise, but it is a start! Then you can `Esc` into the editor and `F1` etc to pan about its different editing modes for maps, sprites, music and so on.

`20.tic` is a more interesting cart, it defines waveforms as hex strings and pokes them into memory with parameters, you can edit the waveform strings and then try out a sort of visual theremin that plays you the shape and shows you the effect of frequency and pitch changes as your cursor moves in 2d space.

That's about it for the day - noodling about in some other carts from [tic80.com](https://tic80.com) you can see people calling higher level `sfx()` functions which work on waveforms that must have already been put into the `tic80`s memory. There's a graphical editor for the sound effects that comes with the inbuilt interface, you can draw and shape the forms and save them, there are YouTube videos about that, if you like to watch videos and poke at graphical interfaces.
