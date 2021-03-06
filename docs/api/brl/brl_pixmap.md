---
id: brl.pixmap
title: BRL.Pixmap
sidebar_label: Introduction
---



Pixmaps provide storage for rectangular regions of pixels.

You can create a new pixmap using the [CreatePixmap](../../brl/brl.pixmap/#function-createpixmaptpixmap-widthheightformatalignbytes4-) command, or load a pixmap 
using [LoadPixmap](../../brl/brl.pixmap/tpixmaploader/#method-loadpixmaptpixmap-streamtstream-abstract).

Pixmaps have 5 properties: width, height, a byte pointer to the pixmap's pixels, pitch and
format.

You can retrieve a pointer to a pixmap's pixels using the [PixmapPixelPtr](../../brl/brl.pixmap/#function-pixmappixelptrbyte-ptr-pixmaptpixmapx0y0-) command.

A pixmap's pitch refers to the number of bytes between one row of pixels in the pixmap
and the next. To retrieve a pixmap's pitch, use the [PixmapPitch](../../brl/brl.pixmap/#function-pixmappitch-pixmaptpixmap-) command.

A pixmap's pixel format determines how the pixels within a pixmap are stored in memory. This 
must be taken into account if you want to access pixels directly via a pixmap's pixel pointer.
You can retrieve the format of a pixmap using the [PixmapFormat](../../brl/brl.pixmap/#function-pixmapformat-pixmaptpixmap-) command, and convert pixmaps
from one format to another using [ConvertPixmap](../../brl/brl.pixmap/#function-convertpixmaptpixmap-pixmaptpixmapformat-).

You can also use [ResizePixmap](../../brl/brl.pixmap/#function-resizepixmaptpixmap-pixmaptpixmapwidthheight-nodebug) to resize a pixmap and flip a pixmap horizontally or vertically
with [XFlipPixmap](../../brl/brl.pixmap/#function-xflippixmaptpixmap-pixmaptpixmap-nodebug) and [YFlipPixmap](../../brl/brl.pixmap/#function-yflippixmaptpixmap-pixmaptpixmap-nodebug).


## Types
| Type | Description |
|---|---|
| [TPixmap](../../brl/brl.pixmap/tpixmap) | The Pixmap type |
| [TPixmapLoader](../../brl/brl.pixmap/tpixmaploader) | Abstract base type for pixmap loaders |

## Functions

### `Function CreatePixmap:TPixmap( width,height,format,align_bytes=4 )`

Create a pixmap


<b>format</b> should be one of the following:

<table><tr><td> <b>Format</b></td><td><b>Description</b></td></tr><tr><td>  PF_A8</td><td>8 bit alpha</td></tr><tr><td>  PF_I8</td><td>8 bit intensity</td></tr><tr><td>  PF_RGB888</td><td>24 bit big endian RGB</td></tr><tr><td>  PF_BGR888</td><td>24 bit little endian RGB</td></tr><tr><td>  PF_RGBA8888</td><td>32 bit big endian RGB with alpha</td></tr><tr><td>  PF_BGRA8888</td><td>32 bit little endian RGB with alpha</td></tr></table>


Note that the newly created pixmap will contain random data. [ClearPixels](../../brl/brl.pixmap/tpixmap/#method-clearpixels-argb-) can
be used to set all pixels to a known value prior to use.


#### Returns
A new pixmap object of the specified <b>width</b> and <b>height</b>


<br/>

### `Function CreateStaticPixmap:TPixmap( pixels:Byte Ptr,width,height,pitch,format )`

Create a pixmap with existing pixel data


The memory referenced by a static pixmap is not released when the pixmap is deleted.

See [CreatePixmap](../../brl/brl.pixmap/#function-createpixmaptpixmap-widthheightformatalignbytes4-) for valid pixmap formats.


#### Returns
A new pixmap object that references an existing block of memory


<br/>

### `Function CopyPixmap:TPixmap( pixmap:TPixmap )`

Copy a pixmap

#### Returns
A new pixmap object


#### Example
```blitzmax
SuperStrict

Graphics 640 , 480

Local pix:TPixmap=LoadPixmap(blitzmaxpath()+"\samples\hitoro\gfx\boing.png")
If pix = Null Then
	RuntimeError ("Error Loading Image")
End If


Local newPix:TPixmap=CopyPixmap(pix)

Repeat
	Cls
	DrawPixmap pix, 50, 50
	DrawPixmap newPix, MouseX(), MouseY()
	Flip
Until KeyHit(key_escape) Or AppTerminate()
```
<br/>

### `Function ConvertPixmap:TPixmap( pixmap:TPixmap,format )`

Convert pixel format of a pixmap


See [CreatePixmap](../../brl/brl.pixmap/#function-createpixmaptpixmap-widthheightformatalignbytes4-) for valid pixmap formats.


#### Returns
A new pixmap object with the specified pixel format


<br/>

### `Function PixmapWidth( pixmap:TPixmap )`

Get pixmap width

#### Returns
The width, in pixels, of <b>pixmap</b>


#### Example
```blitzmax
SuperStrict

Graphics 640,480
Local pix:TPixmap=LoadPixmap(blitzmaxpath()+"\samples\hitoro\gfx\boing.png")

If pix = Null Then
	RuntimeError ("Error Loading Image")
End If

Repeat
	Cls
	' Display Information
	DrawText "Image Width:"+PixmapWidth(pix)+"  Image Height:"+PixmapHeight(pix),0,0 

	DrawPixmap pix,100,100
	Flip
Until KeyHit(key_escape) Or AppTerminate()
```
<br/>

### `Function PixmapHeight( pixmap:TPixmap )`

Get pixmap width

#### Returns
The height, in pixels, of <b>pixmap</b>


#### Example
```blitzmax
SuperStrict

Graphics 640,480

Local pix:TPixmap = LoadPixmap(blitzmaxpath()+"\samples\hitoro\gfx\boing.png")

If pix = Null Then
	RuntimeError ("Error Loading Image")
End If

Repeat
	Cls
	
	' Display Information
	DrawText "Image Width:"+PixmapWidth(pix)+"  Image Height:"+PixmapHeight(pix),0,0 

	DrawPixmap pix,100,100
	Flip
Until KeyHit(key_escape) Or AppTerminate()
```
<br/>

### `Function PixmapPitch( pixmap:TPixmap )`

Get pixmap pitch


Pitch refers to the difference, in bytes, between the start of one row of pixels and the start of the next row.


#### Returns
The pitch, in bytes, of <b>pixmap</b>


<br/>

### `Function PixmapFormat( pixmap:TPixmap )`

Get pixmap format


See [CreatePixmap](../../brl/brl.pixmap/#function-createpixmaptpixmap-widthheightformatalignbytes4-) for supported formats.


#### Returns
The format of the pixels stored in <b>pixmap</b>


<br/>

### `Function PixmapPixelPtr:Byte Ptr( pixmap:TPixmap,x=0,y=0 )`

Get pixmap pixels

#### Returns
A byte pointer to the pixels stored in <b>pixmap</b>


<br/>

### `Function PixmapWindow:TPixmap( pixmap:TPixmap,x,y,width,height )`

Create a pixmap window

[PixmapWindow](../../brl/brl.pixmap/#function-pixmapwindowtpixmap-pixmaptpixmapxywidthheight-) creates a 'virtual' window into <b>pixmap</b>.


#### Returns
A new pixmap object


<br/>

### `Function MaskPixmap:TPixmap( pixmap:TPixmap,mask_red,mask_green,mask_blue ) NoDebug`

Mask a pixmap

<b>MaskPixmap</b> builds a new pixmap with alpha components set to '0' wherever the pixel colors
in the original <b>pixmap</b> match <b>mask_red</b>, <b>mask_green</b> and <b>mask_blue</b>. <b>mask_red</b>, <b>mask_green</b> and <b>mask_blue</b>
should be in the range 0 to 255.


#### Returns
A new pixmap object


<br/>

### `Function XFlipPixmap:TPixmap( pixmap:TPixmap ) NoDebug`

Flip a pixmap horizontally

#### Returns
A new pixmap object


#### Example
```blitzmax
SuperStrict

Graphics 640,480

Local pix:TPixmap=LoadPixmap(blitzmaxpath()+"\samples\hitoro\gfx\boing.png")

If pix = Null Then
	RuntimeError ("Error Loading Image")
End If

Repeat
	Cls
	DrawText "Press Key X or Y to change Orientation" , 10 , 10
	
	' Change pixmap orientation
	If KeyHit(KEY_X) Then
		pix = XFlipPixmap(pix)
	End If
	
	If KeyHit(KEY_Y) Then
		pix = YFlipPixmap(pix)
	End If
	
	DrawPixmap pix,50,50
	Flip
Until KeyHit(key_escape) Or AppTerminate()
```
<br/>

### `Function YFlipPixmap:TPixmap( pixmap:TPixmap ) NoDebug`

Flip a pixmap vertically

#### Returns
A new pixmap object


#### Example
```blitzmax
SuperStrict

Graphics 640,480

Local pix:TPixmap=LoadPixmap(blitzmaxpath()+"\samples\hitoro\gfx\boing.png")

If pix = Null Then
	RuntimeError ("Error Loading Image")
End If

Repeat
	Cls
	DrawText "Press Key X or Y to change Orientation" , 10 , 10
	
	' Change pixmap orientation
	If KeyHit(KEY_X) Then
		pix = XFlipPixmap(pix)
	End If
	
	If KeyHit(KEY_Y) Then
		pix = YFlipPixmap(pix)
	End If
	
	DrawPixmap pix,50,50
	Flip
Until KeyHit(key_escape) Or AppTerminate()
```
<br/>

### `Function ResizePixmap:TPixmap( pixmap:TPixmap,width,height ) NoDebug`

Resize a pixmap

#### Returns
A new pixmap object of the specified <b>width</b> and <b>height</b>


#### Example
```blitzmax
SuperStrict

Graphics 640 , 480

Local pix:TPixmap=LoadPixmap(blitzmaxpath()+"\samples\hitoro\gfx\boing.png")

If pix = Null Then
	RuntimeError ("Error Loading Image")
End If

'Reduce Image by 50%
Local newPix:TPixmap=ResizePixmap(pix, Int(PixmapWidth(pix)*.5), Int(PixmapHeight(pix)*.5))

Repeat
	Cls
	DrawPixmap pix, 50, 50
	DrawPixmap newPix, MouseX() , MouseY()
	Flip
Until KeyHit(key_escape) Or AppTerminate()
```
<br/>

### `Function LoadPixmap:TPixmap( url:Object )`

Load a pixmap

#### Returns
A pixmap object


#### Example 1
```blitzmax
SuperStrict

Graphics 640,480
Local player:TPixmap=LoadPixmap(blitzmaxpath()+"\samples\hitoro\gfx\boing.png")

If player = Null Then
	RuntimeError ("Error Loading Image")
End If

Repeat
	Cls
	DrawPixmap Player,10,10
	Flip
Until KeyHit(key_escape) Or AppTerminate()
```
#### Example 2
```blitzmax
SuperStrict

Graphics 640 , 480

Local pix:TPixmap=LoadPixmap(blitzmaxpath()+"\samples\hitoro\gfx\boing.png")
'converts Pixmap to Image
'note alpha transparency
Local image:TImage=LoadImage(pix)

Repeat
	Cls
	DrawPixmap pix, 50, 50
	DrawImage image, MouseX(), MouseY()
	Flip
Until KeyHit(key_escape) Or AppTerminate()
```
<br/>

### `Function ReadPixel( pixmap:TPixmap,x,y )`

Read a pixel from a pixmap


The returned 32 bit value contains the following components:

<table><tr><td> bits 24-31</td><td>pixel alpha</td></tr><tr><td>  bits 16-23</td><td>pixel red</td></tr><tr><td>  bits 8-15</td><td>pixel green</td></tr><tr><td>  bits 0-7</td><td>pixel blue</td></tr></table>



#### Returns
A 32 bit pixel value


<br/>

### `Function WritePixel( pixmap:TPixmap,x,y,argb )`

Write a pixel to a pixmap


The 32 bit <b>argb</b> value contains the following components:

<table><tr><td> bits 24-31</td><td>pixel alpha</td></tr><tr><td>  bits 16-23</td><td>pixel red</td></tr><tr><td>  bits 8-15</td><td>pixel green</td></tr><tr><td>  bits 0-7</td><td>pixel blue</td></tr></table>



<br/>

### `Function ClearPixels( pixmap:TPixmap,argb=0 )`

Clear a pixmap


Sets all pixels in a pixmap to a 32 bit pixel value.

The 32 bit <b>argb</b> value contains the following components:

<table><tr><td> bits 24-31</td><td>pixel alpha</td></tr><tr><td>  bits 16-23</td><td>pixel red</td></tr><tr><td>  bits 8-15</td><td>pixel green</td></tr><tr><td>  bits 0-7</td><td>pixel blue</td></tr></table>



#### Example
```blitzmax
SuperStrict

Graphics 800 , 600

Local mypix:TPixmap = LoadPixmap(BlitzMaxPath()+"/samples/hitoro/gfx/boing.png")
If mypix = Null Then
	RuntimeError ("Error Loading Image")
End If

DrawPixmap mypix, 0, 0

ClearPixels(mypix, $FFFFFF)
 

DrawPixmap mypix, 300, 0

Flip

WaitKey
```
<br/>

