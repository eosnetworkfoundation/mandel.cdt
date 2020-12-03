---
content_title: How-To Upsert Into Key-Value Map
link_text: "How-To Upsert Into Key-Value Map"
---

## Summary

This how-to procedure provides instructions to upsert into `Key-Value Map` (`kv map`).

## Prerequisites

Before you begin, complete the following prerequisites:

* An EOSIO development environment, for details consult the [Get Started](https://developers.eos.io/welcome/latest/getting-started/development-environment/introduction) Guide
* A smart contract, let’s call it `smrtcontract`
* A user defined type, let’s call it `person`, which defines the data which is stored in the map
* A `kv map` object which stores objects of type `person`, with unique keys of type `int`.

Refer to the following possible implementation of your starting point.

`smartcontract.hpp file`

```cpp
struct person {
  eosio::name account_name;
  std::string first_name;
  std::string last_name;
};

class [[eosio::contract]] smartcontract : public eosio::contract {

   using my_map_t = eosio::kv::map<"kvmap"_n, int, person>;

   public:
      using contract::contract;
      smartcontract(eosio::name receiver, eosio::name code, eosio::datastream<const char*> ds)
         : contract(receiver, code, ds) {}

   private:
      my_map_t my_map{};
};
```

## Procedure

Complete the following steps to insert a new `person` object with a given ID, if it doesn't exist already, or update it in the `kv map` if the `person` with the given ID already exists:

1. Create a new action in your contact, let’s call it `upsert`, which takes as input parameters the person ID, an account name, a first name and a last name.
2. Create an instance of the `person` class, named `person_upsert`, based on the input parameters: account name, first name and last name.
3. Use the `[]` operator defined for the `kv::map` type, and set the `person_upsert` as the value for the `ID` key.

Refer to the following possible implementation to insert a new `person` object, and then update it, in the `kv map`:

`smartcontract.hpp file`

```cpp
struct person {
  eosio::name account_name;
  std::string first_name;
  std::string last_name;
};

class [[eosio::contract]] smartcontract : public eosio::contract {

   using my_map_t = eosio::kv::map<"kvmap"_n, int, person>;

   public:
      using contract::contract;
      smartcontract(eosio::name receiver, eosio::name code, eosio::datastream<const char*> ds)
         : contract(receiver, code, ds) {}

      // inserts if not exists, or updates if already exists, a person
      [[eosio::action]]
      void upsert(int id,
         eosio::name account_name,
         std::string first_name,
         std::string last_name);

   private:
      my_map_t my_map{};
};
```

`smartcontract.cpp file`

```cpp
// inserts if not exists, or updates if already exists, a person
[[eosio::action]]
void smartcontract::upsert(
      int id,
      eosio::name account_name,
      std::string first_name,
      std::string last_name) {

   // create the person object which will be stored in kv::map
   const person& person_upsert = person{
      account_name = account_name,
      first_name = first_name,
      last_name = last_name};

   // upsert into kv::map
   my_map[id] = person_upsert;
}
```

## Next Steps

The following options are available when you complete the procedure:

* Verify if the newly inserted `person` actually exists in the map. To accomplish this task use the `find()` function of the `kv_map`.
* Delete the newly created or updated `person` from the map. To accomplish this task, use the `erase()` function of the `kv map`.