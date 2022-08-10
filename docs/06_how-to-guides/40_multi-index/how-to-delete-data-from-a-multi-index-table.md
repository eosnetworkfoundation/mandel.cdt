---
content_title: How to delete data from a multi-index table
---

## Overview

This guide provides instructions to to delete data from a multi-index table.

## Reference

See the following code reference:

* The [`multi-index`](http://docs.eosnetwork.com/reference/mandel-cdt/classeosio_1_1multi__index.html) class.
* The [`multi-index::find(...)`](http://docs.eosnetwork.com/reference/mandel-cdt/group__multiindex.html#ga40a65cdfcc298b85e0e4ddf4c3581c1c) method.
* The [`multi-index::erase(...)`](http://docs.eosnetwork.com/reference/mandel-cdt/group__multiindex.html#gad28ac8d91e9af22cbbc12962a805d253) method.

## Before you begin

Make sure you have the following prerequisites in place:

* An EOSIO development environment, for details consult the [Binary Releases](/eosdocs/smart-contracts/mandel-cdt/binary_releases),
* A multi-index `testab` table instance which stores `user` objects indexed by the primary key which is of type `eosio::name`. Consult the section [How to instantiate a multi-index table](/eosdocs/smart-contracts/mandel-cdt/how-to-guides/multi-index/how-to-instantiate-a-multi-index-table) to learn how to set it up.

## Procedure

Complete the following steps to implement a `del` action which deletes an user object, identified by its account name, from the multi-index table.

### 1. Find The User You Want To Delete

Use the multi-index [`find(...)`](http://docs.eosnetwork.com/reference/mandel-cdt/group__multiindex.html#ga40a65cdfcc298b85e0e4ddf4c3581c1c) method to locate the user object you want to delete. The targeted user is searched based on its account name.

```cpp
[[eosio::action]] void multi_index_example::del( name user ) {
  // check if the user already exists
  auto itr = testtab.find(user.value);
}
```

### 2. Delete The User If Found

Check to see if the user exists and use [`erase`(...)](http://docs.eosnetwork.com/reference/mandel-cdt/group__multiindex.html#gad28ac8d91e9af22cbbc12962a805d253) method to delete the row from table. Otherwise print an informational message and return.

```diff
[[eosio::action]] void multi_index_example::del( name user ) {
  // check if the user already exists
  auto itr = testtab.find(user.value);
+  if ( itr == testtab.end() ) {
+    printf("User does not exist in table, nothing to delete");
+    return;
+  }

+  testtab.erase( itr );
}
```

[[info | Full example location]]
| A full example project demonstrating the instantiation and usage of multi-index table can be found [here](https://github.com/eosnetworkfoundation/mandel.cdt/tree/main/examples/multi_index_example).

## Summary

In conclusion, the above instructions show how to delete data from a multi-index table.

## Next Steps

* You can verify if the user object was deleted from the multi-index table. .

```cpp
  // check if the user was deleted
  auto itr = testtab.find(user.value);
  if ( itr == testtab.end() ) {
    printf("User was deleted successfully.");
  }
  else {
    printf("User was NOT deleted!");
  }
```
