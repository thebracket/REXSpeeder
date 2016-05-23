# REXSpeeder

A C++ library for loading and saving [REXPaint](http://www.gridsagegames.com/rexpaint/) files quickly. Think of REXSpeeder as the glue between REXPaint and your project. 

### Features:
 * Really fast.
 * Simple API.
 * Supports re-saving valid .xp files

## Installation

See `INSTALL` for instructions on how to use REXSpeeder for your project. 


## Usage


All of REXSpeeder is contained in the `xp` namespace, which you get with `#include <REXSpeeder.h>`. From there,

##### Open an image: 

`xp::RexFile file("hello.xp")`

##### Get a tile from the first layer:
`xp::RexTile* tile = nyan.getTile(0, x, y)`

##### Set a tile in the first layer:
````
xp::RexTile myTile;
(...)
file.setTile(0,x,y,mytile)
````

##### Save the image:

`file.save("goodbye.xp")`

REXSpeeder also comes with a few utility functions, like image flattening, and all the image queries you'd expect. Functions are documented in `include/REXSpeeder.h`. 

## Example

Say we have an image in REXPaint, "nyan.xp":

![](https://github.com/pyridine/REXSpeeder/raw/master/example/before.png)

Then, with

````
xp::RexFile nyan("nyan.xp");

nyan.flatten();

for (int x = 0; x < nyan.getWidth(); x++) {
	for (int y = 0; y < nyan.getHeight(); y++) {
		xp::RexTile original = *nyan.getTile(0, x, y);
		xp::RexTile modified = original;

		modified.fore_red = original.fore_blue;
		modified.fore_blue = original.fore_green;
		modified.fore_green = original.fore_red;

		nyan.setTile(0, x, y, modified);
	}
}
nyan.save("cat.xp");
````

we have a new file, "cat.xp", which can be loaded in REXPaint:

![](https://github.com/pyridine/REXSpeeder/raw/master/example/after.png)


(See `example/` for the source code and Visual Studio project.)


I am technically and inspirationally indebted to GamePopper's REXPaint library, which can be found [here](https://github.com/gamepopper/REXReader-CPlusPlus).