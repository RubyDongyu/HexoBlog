

我们访问ContentProvider借助于ContentResolver的query，其中首先使用acquireUnstableProvider，如果发生DeadObjectException的异常就会使用acquireProvider来进行。 