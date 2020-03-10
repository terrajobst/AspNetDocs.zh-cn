> 如果应用使用 SQLite 作为标识数据存储，则不支持某些命令。 由于数据库引擎的限制，`Alter` 命令将引发以下异常：
>
> "NotSupportedException： SQLite 不支持此迁移操作。" 
>
> 解决方法是，对数据库运行 Code First 迁移，以更改表。
