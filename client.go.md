# Client.go

Client 会是 Kafka-go 的一个新 API。

{% hint style="info" %}
这仍然是一个实验性质的 API。
{% endhint %}

brokers 是所有 brokers 的编号列表。这里多了一个 Dialer 对象列表。

```go
type Client struct {
    brokers []string
    dailer *Dialer
}
```

