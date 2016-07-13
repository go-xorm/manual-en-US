# Create ORM Engine

When using xorm, you can create multiple orm engines, an engine means a databse. So you can：

```Go
import (
    _ "github.com/go-sql-driver/mysql"
    "github.com/go-xorm/xorm"
)

var engine *xorm.Engine

func main() {
    var err error
    engine, err = xorm.NewEngine("mysql", "root:123@/test?charset=utf8")
}
```

or

```Go
import (
    _ "github.com/mattn/go-sqlite3"
    "github.com/go-xorm/xorm"
)

var engine *xorm.Engine

func main() {
    var err error
    engine, err = xorm.NewEngine("sqlite3", "./test.db")
}
```

You can create many engines for different databases.Generally, you just need to create only one engine. Engine supports run on go routines.

When you want to manually close the engine, call `engine.Close`. Generally, we don't need to do this, because engine will be closed automatically when application exits.

xorm supports four drivers now:

* Mysql: [github.com/Go-SQL-Driver/MySQL](https://github.com/Go-SQL-Driver/MySQL)

* MyMysql: [github.com/ziutek/mymysql](https://github.com/ziutek/mymysql)

* SQLite: [github.com/mattn/go-sqlite3](https://github.com/mattn/go-sqlite3)

* Postgres: [github.com/lib/pq](https://github.com/lib/pq)

* MsSql: [github.com/lunny/godbc](https://githubcom/lunny/godbc)

NewEngine's parameters are the same as `sql.Open`. So you should read the driver's document for parameter's usage.

After engine is created, you can do some settings.

## Logs

* `engine.ShowSQL(true)`, Shows SQL statement on standard output or your io.Writer;
* `engine.Logger().SetLevel(core.LOG_DEBUG)`, Shows debug and other infomations;

If you want to record infomations with another method: use `engine.SetLogger()` as `io.Writer`:

```Go
f, err := os.Create("sql.log")
if err != nil {
    println(err.Error())
    return
}
engine.SetLogger(xorm.NewSimpleLogger(f))
```

Logs also support recording to syslog, for example:

```Go
logWriter, err := syslog.New(syslog.LOG_DEBUG, "rest-xorm-example")
if err != nil {
	log.Fatalf("Fail to create xorm system logger: %v\n", err)
}

logger := xorm.NewSimpleLogger(logWriter)
logger.ShowSQL(true)
engine.SetLogger(logger)
```

## Connections pool

Engine provides DB connections pool settings.

* Use `engine.SetMaxIdleConns()` to set idle connections.
* Use `engine.SetMaxOpenConns()` to set Max connections. This methods support only Go 1.2+.
