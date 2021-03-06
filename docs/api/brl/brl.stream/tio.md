---
id: tio
title: TIO
sidebar_label: TIO
---

Base input/output type



To create your own stream types, you should extend TStream and implement
at least these methods.

You should also make sure your stream can handle multiple calls to the Close method.


## Methods

### `Method Eof:Int()`

Get stream end of file status


For seekable streams such as file streams, Eof generally returns True if the file
position equals the file size. This means that no more bytes can be read from the
stream. However, it may still be possible to write bytes, in which case the file will
'grow'.

For communication type streams such as socket streams, Eof returns True if the stream
has been shut down for some reason - either locally or by the remote host. In this case,
no more bytes can be read from or written to the stream.


#### Returns
True for end of file reached, otherwise False


<br/>

### `Method Pos:Long()`

Get position of seekable stream

#### Returns
Stream position as a byte offset, or -1 if stream is not seekable


<br/>

### `Method Size:Long()`

Get size of seekable stream

#### Returns
Size, in bytes, of seekable stream, or 0 if stream is not seekable


<br/>

### `Method Seek:Long( pos:Long, whence:Int = SEEK_SET_ )`

Seek to position in seekable stream

#### Returns
New stream position, or -1 if stream is not seekable


<br/>

### `Method Flush()`

Flush stream


Flushes any internal stream buffers.


<br/>

### `Method Close()`

Close stream


Closes the stream after flushing any internal stream buffers.


<br/>

### `Method Read:Long( buf:Byte Ptr,count:Long )`

Read at least 1 byte from a stream


This method may 'block' if it is not possible to read at least one byte due to IO
buffering.

If this method returns 0, the stream has reached end of file.


#### Returns
Number of bytes successfully read


<br/>

### `Method Write:Long( buf:Byte Ptr,count:Long )`

Write at least 1 byte to a stream


This method may 'block' if it is not possible to write at least one byte due to IO
buffering.

If this method returns 0, the stream has reached end of file.


#### Returns
Number of bytes successfully written


<br/>

### `Method SetSize:Int(size:Long)`

Sets the size of the stream to <b>size</b> bytes.

Only a few stream types support resizing.


#### Returns
[True](../../../brl/brl.blitz/#true) if the stream was able to be resized, [False](../../../brl/brl.blitz/#false) otherwise.


<br/>

