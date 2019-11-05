# Client.go

Client 会是 Kafka-go 的一个新 API。

{% hint style="info" %}
这仍然是一个实验性质的 API。
{% endhint %}

我们希望 Client 这个 API 的层面比 Conn 高，比 Reader 和 Writer API 低。

brokers 是所有 brokers 的编号列表。这里多了一个 Dialer 对象列表。

```go
type Client struct {
    brokers []string
    dailer *Dialer
}
```

Client 的配置

```go
type ClientConfig struct {
    Brokers []string
    Dialer *Dialer
}
```

我们希望将 Topic 和 Group 作为一个整体作为函数参数提交给 Client API。

{% hint style="danger" %}
这个结构体未来可能会变化。
{% endhint %}

```go
type TopicAndGroup struct {
    Topic string
    GroupId string
}
```