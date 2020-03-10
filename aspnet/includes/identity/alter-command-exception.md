> <span data-ttu-id="42b88-101">如果应用使用 SQLite 作为标识数据存储，则不支持某些命令。</span><span class="sxs-lookup"><span data-stu-id="42b88-101">Some commands aren't supported if the app uses SQLite as its Identity data store.</span></span> <span data-ttu-id="42b88-102">由于数据库引擎的限制，`Alter` 命令将引发以下异常：</span><span class="sxs-lookup"><span data-stu-id="42b88-102">Due to limitations in the database engine, `Alter` commands throw the following exception:</span></span>
>
> <span data-ttu-id="42b88-103">"NotSupportedException： SQLite 不支持此迁移操作。"</span><span class="sxs-lookup"><span data-stu-id="42b88-103">"System.NotSupportedException: SQLite does not support this migration operation."</span></span> 
>
> <span data-ttu-id="42b88-104">解决方法是，对数据库运行 Code First 迁移，以更改表。</span><span class="sxs-lookup"><span data-stu-id="42b88-104">As a work around, run Code First migrations on the database to change the tables.</span></span>
