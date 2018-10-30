# Overview
The Go Client allows you to push data to <> using [Go](https://golang.org).

## Package Documentation
```shell

```
To view package documentation, run the following `godoc` command in the cloned repo:
```shell
godoc -http=:8080
```


## Unit Tests
* Run model core unit tests
```shell

```

## Examples
### Create a Client
```go
client := api.NewClient("https://api.app.argo.com/ingest", "{api-key}")
```

### Create and Post Element
```go
element := core.NewElement("elementId", "Element Name", "SERVER", "use1a")
metric := core.NewMetric("metricId", "Metric Name", "bytes", "COUNTER", "None", core.Tag{"env", "prod"})
sample, _ := core.NewSample("metricId", time.Now(), 0.0)
element.AddAttribute("cpus", "4").AddTag("platform", "kubernetes").AddRelation("relatedElementId").AddMetric(metric).AddSample(sample)
elements := []core.Element{element}
client.PostElements(elements)
```

## Create and Post Event
```go
event := core.NewEvent("go client", "test post event", "INFO", time.Now(), core.ElementMessage{"elementId", "INFO", "test"})
event.AddTag("platform", "kubernetes")
client.PostEvents([]core.Event{event})
````

## Create and Post Check
```go
check := core.Check{"heartbeat", "elementId", 120}
client.PostCheck(check)
```