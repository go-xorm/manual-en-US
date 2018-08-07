# Create ORM Engine

When using xorm, you can create one or more ORM engines. XORM supports two kinds of engines, `Engine` and `EngineGroup`. An engine could operate one database and an engine group could handle Master/Slave situations. Both kinds of engines have similar APIs, so that you can easily change from one to another. We also provide an `EngineInterface` to do that.