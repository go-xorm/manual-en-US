## 7.Delete one or more records
Delete one or more records

* delete by id

```Go
affected, err := engine.Id(1).Delete(&User{})
```

* delete by other conditions

```Go
affected, err := engine.Delete(&User{Name:"xlw"})
```
