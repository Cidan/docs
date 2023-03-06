Locks acquired using `SELECT ... FOR UPDATE` are lost on [lease transfers]() and [range splits and merges](). This happens because currently `SELECT ... FOR UPDATE` is implemented using [unreplicated locks]().

In most cases, this will cause the transaction that acquired the locks to fail to commit. For example, this behavior can lead to [transaction retry errors with code `40001` and the `restart transaction` error message](common-errors.html#restart-transactions).

We intend to improve the reliability of these locks. For details, see [https://github.com/cockroachdb/cockroach/issues/75456].
