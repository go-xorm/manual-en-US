## Event
xorm supports two kinds of events. One is a method on a data model struct, another is called in session process.

Struct's event methods is below:

* `BeforeInsert()`

This method will be called before data be inserted into database on insert process.

* `BeforeUpdate()`

This method will be called before data be updated into database on update process.

* `BeforeDelete()`

This method will be called before data be deleted on delete process.

* `func BeforeSet(name string, cell xorm.Cell)`

This method will be called on  Get or Find. After data is retrieve from database and before data will be set to struct.

* `AfterInsert()`

This method will be called after data be inserted into database on insert process.

* `AfterUpdate()`

This method will be called after data be updated into database on update process.

* `AfterDelete()`

This method will be called after data be deleted on delete process.

Process temporory events is:

* `Before(beforeFunc interface{})`

This method will be called before any process. For example:

```Go
before := func(bean interface{}){
    fmt.Println("before", bean)
}
engine.Before(before).Insert(&obj)
```

* `After(afterFunc interface{})`

This method will be called after any process. For example:

```Go
after := func(bean interface{}){
    fmt.Println("after", bean)
}
engine.After(after).Insert(&obj)
```
