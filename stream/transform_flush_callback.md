* `callback` {Function} A callback function (optionally with an error
  argument and data) to be called when remaining data has been flushed.

*Note*: This function MUST NOT be called by application code directly. It
should be implemented by child classes, and called by the internal Readable
class methods only.

In some cases, a transform operation may need to emit an additional bit of
data at the end of the stream. For example, a `zlib` compression stream will
store an amount of internal state used to optimally compress the output. When
the stream ends, however, that additional data needs to be flushed so that the
compressed data will be complete.

Custom [Transform][] implementations *may* implement the `transform._flush()`
method. This will be called when there is no more written data to be consumed,
but before the [`'end'`][] event is emitted signaling the end of the
[Readable][] stream.

Within the `transform._flush()` implementation, the `readable.push()` method
may be called zero or more times, as appropriate. The `callback` function must
be called when the flush operation is complete.

The `transform._flush()` method is prefixed with an underscore because it is
internal to the class that defines it, and should never be called directly by
user programs.



* `callback` {Function} 一个当剩余的数据刷新后被调用的回调函数(error参数和data可选)。

*Note*: 应用程序代码禁止直接调用这个函数。它应该由子类来实现，并且只能被内部可读流的类方法调用。

在某些情况下，转换操作需要在流的末尾发射一块额外的数据。例如，`zlib` 压缩流会存储一种优先用于压缩输出的内部状态。但是在流结束的时候，那段额外的数据需要被刷新才能完成数据压缩。

自定义的 [Transform][] 实现，可以实现`transform._flush()`方法。在没有更多的要写的数据被消耗时，会调用这个方法，但是在发射[`'end'`][] 事件之前会发出可读流结束的信号。
                          
在 `transform._flush()` 实现里，`readable.push()`方法会在适当的时候调用0次或者多次。`callback`在刷新操作完成的时候一定会被调用。

`transform._flush()` 方法前缀为下划线，因为它是在定义它的类的内部，绝不应该被用户程序直接调用。
