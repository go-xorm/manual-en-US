## 6.Update

You can use `Update` to update the record. The first param of this method is the pointer of struct or `map[string]interface{}` which need to be update. When this param is the pointer of struct, only non-empty and non-zero field will be updated to database. When it is a `map[string]interface{}`, the map key is the name of the column will be updated, the map value is the content needs to be updated.

```Go
user := new(User)
user.Name = "myname"
affected, err := engine.Id(id).Update(user)
```

But if you want to update a zero value to database. There are two chosen:

1. Use `Cols` to indicate the columns will need to be update even if it is zero or empty.

```Go
affected, err := engine.Id(id).Cols("age").Update(&user)
```

2. Use `map[string]interface{}`, but you need specify the table via a pointer of struct or a string.

```Go
affected, err := engine.Table(new(User)).Id(id).Update(map[string]interface{}{"age":0})
affected, err := engine.Table("user").Id(id).Update(map[string]interface{}{"age":0})
```
