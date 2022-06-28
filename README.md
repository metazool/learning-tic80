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

----

This morning I made a graceless thing that worked! by pastiching together some of blinry's simpler examples and referring to the [TIC-80 cheatsheet](https://zenithsal.com/assets/documents/tic-80_cheatsheet.pdf) which makes a little bit more sense each time.

```
function TIC()
  map()
  mx, my = mouse()
  x = 116
  y = 61
  circ(x,y,mx/4,15) 
  print(mx,180,4,12)
  print(my,210,4,12)
end
```

This grabs the x and y coordinates of the mouse pointer, prints them out in the top right and draws a grey circle that resizes itself relative to where you are on the x axis. Unsure what the color value of the last parameter to `circ` is, or what language this is (lua?). What would be nice here is a sort of trombone effect where the sound gets sharper and more emphatic as the circle resizes but this is enough for now.

The most effort here is _not_ using vim muscle memory in the built-in code editor inside `tic80`! Save it from the CLI with `save zool01.tic` to then be able to Ctrl-S in the editor.

----

Looking to understand the colour values, the TIC-80 has a palette of 16 colours [with a pleasant default](https://github.com/nesbox/TIC-80/wiki/palette) but you can [overwrite the part of its memory](https://github.com/nesbox/TIC-80/wiki/ram#palette) that holds the palette and define your own. You could do this per "scanline" calling the `BDR` function and get more to display at once [wiki example showing this grayscale](https://github.com/nesbox/TIC-80/wiki/BDR). It's hard to see too much colour but the default palette has three greys at indices 13, 14, 15, it's fine.

Added an outline to the circle by writing slightly larger ones first like you'd do a label outline. A hole in the centre it would be nice to get a pulsing effect for. A counter outside the `TIC` function which you can increment per frame to keep track of relatively when you are, and consider what can be done with that, or a call to the [time() function](https://github.com/nesbox/TIC-80/wiki/time) that returns milliseconds since the cart started.

Kindly linked to this [fab looking set of tips for "byte battles"](https://github.com/vsariola/battletricks) (e.g. compressing code size to make it fit arbitrary competition weights) the gut response was "byte battles are well out of my league" but skimming back over it, there are tips for things like a ["motion blur"](https://github.com/vsariola/battletricks#motion-blur) which could make for a pulse effect. 

