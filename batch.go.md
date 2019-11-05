# Buffer.go

定义一个缓存池，新建一个 sync.Pool 对象配置 New 属性即可。

这里就可以看出 var, make 和 new 的区别。

var 的话是默认初始化的

```go
var bufferPool = sync.Pool {
    New: func() interface{} {
        return new Buffer()
    },
}
```

而这里我们希望 b 是一个 buffer 指针，而不是一个 buffer 对象，因此我们要用 new。新建 buffer 对象的过程中要将 buffer grow 到 2^16 大小。

```go
func newBuffer() *byte.Buffer {
    b := new(bytes.Buffer)
    b.Grow(65536)
    return b
}
```

因为 `.get` 的类型被擦除了，因此要重新设置类型。从池中取出一个 buffer 对象。

```go
func acquireBuffer() *byte.Buffer {
    return bufferPool.Get().(*bytes.Buffer)
}
```

释放 buffer 的话首先要释放掉 buffer 中的内容，然后再将 buffer 重新放回缓冲池中。

```go
func releaseBuffer(b *bytes.Buffer) {
    if b!= nil {
        b.Reset()
        bufferPool.Put(b)
    }
}
```

