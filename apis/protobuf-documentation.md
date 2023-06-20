# Protobuf Documentation

## cosmos/base/v1beta1/coin.proto

### Coin

Coin defines a token with a denomination and an amount.

NOTE: The amount field is an Int which implements the custom method signatures required by gogoproto.

| Field    | Type                       | Label | Description |
| -------- | -------------------------- | ----- | ----------- |
| `denom`  | [string](broken-reference) |       |             |
| `amount` | [string](broken-reference) |       |             |

### DecCoin

DecCoin defines a token with a denomination and a decimal amount.

NOTE: The amount field is an Dec which implements the custom method signatures required by gogoproto.

| Field    | Type                       | Label | Description |
| -------- | -------------------------- | ----- | ----------- |
| `denom`  | [string](broken-reference) |       |             |
| `amount` | [string](broken-reference) |       |             |

### DecProto

DecProto defines a Protobuf wrapper around a Dec object.

| Field | Type                       | Label | Description |
| ----- | -------------------------- | ----- | ----------- |
| `dec` | [string](broken-reference) |       |             |

### IntProto

IntProto defines a Protobuf wrapper around an Int object.

| Field | Type                       | Label | Description |
| ----- | -------------------------- | ----- | ----------- |
| `int` | [string](broken-reference) |       |             |

## cosmos/base/query/v1beta1/pagination.proto

### PageRequest

PageRequest is to be embedded in gRPC request messages for efficient pagination. Ex:

message SomeRequest { Foo some\_parameter = 1; PageRequest pagination = 2; }

| Field         | Type                       | Label | Description                                                                                                                                                                                                                         |
| ------------- | -------------------------- | ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `key`         | [bytes](broken-reference)  |       | key is a value returned in PageResponse.next\_key to begin querying the next page most efficiently. Only one of offset or key should be set.                                                                                        |
| `offset`      | [uint64](broken-reference) |       | offset is a numeric offset that can be used when key is unavailable. It is less efficient than using key. Only one of offset or key should be set.                                                                                  |
| `limit`       | [uint64](broken-reference) |       | limit is the total number of results to be returned in the result page. If left empty it will default to a value to be set by each app.                                                                                             |
| `count_total` | [bool](broken-reference)   |       | count\_total is set to true to indicate that the result set should include a count of the total number of items available for pagination in UIs. count\_total is only respected when offset is used. It is ignored when key is set. |

### PageResponse

PageResponse is to be embedded in gRPC response messages where the corresponding request message has used PageRequest.

message SomeResponse { repeated Bar results = 1; PageResponse page = 2; }

| Field      | Type                       | Label | Description                                                                                                      |
| ---------- | -------------------------- | ----- | ---------------------------------------------------------------------------------------------------------------- |
| `next_key` | [bytes](broken-reference)  |       | next\_key is the key to be passed to PageRequest.key to query the next page most efficiently                     |
| `total`    | [uint64](broken-reference) |       | total is total number of results available if PageRequest.count\_total was set, its value is undefined otherwise |

## cosmos/auth/v1beta1/auth.proto

### BaseAccount

BaseAccount defines a base account type. It contains all the necessary fields for basic account functionality. Any custom account type should extend this type for additional functionality (e.g. vesting).

| Field            | Type                                    | Label | Description |
| ---------------- | --------------------------------------- | ----- | ----------- |
| `address`        | [string](broken-reference)              |       |             |
| `pub_key`        | [google.protobuf.Any](broken-reference) |       |             |
| `account_number` | [uint64](broken-reference)              |       |             |
| `sequence`       | [uint64](broken-reference)              |       |             |

### ModuleAccount

ModuleAccount defines an account for modules that holds coins on a pool.

| Field          | Type                                                 | Label    | Description |
| -------------- | ---------------------------------------------------- | -------- | ----------- |
| `base_account` | [BaseAccount](protobuf-documentation.md#baseaccount) |          |             |
| `name`         | [string](broken-reference)                           |          |             |
| `permissions`  | [string](broken-reference)                           | repeated |             |

### Params

Params defines the parameters for the auth module.

| Field                       | Type                       | Label | Description |
| --------------------------- | -------------------------- | ----- | ----------- |
| `max_memo_characters`       | [uint64](broken-reference) |       |             |
| `tx_sig_limit`              | [uint64](broken-reference) |       |             |
| `tx_size_cost_per_byte`     | [uint64](broken-reference) |       |             |
| `sig_verify_cost_ed25519`   | [uint64](broken-reference) |       |             |
| `sig_verify_cost_secp256k1` | [uint64](broken-reference) |       |             |

## cosmos/auth/v1beta1/genesis.proto

### GenesisState

GenesisState defines the auth module's genesis state.

| Field      | Type                                    | Label    | Description                                      |
| ---------- | --------------------------------------- | -------- | ------------------------------------------------ |
| `params`   | [Params](broken-reference)              |          | params defines all the paramaters of the module. |
| `accounts` | [google.protobuf.Any](broken-reference) | repeated | accounts are the accounts present at genesis.    |

## cosmos/auth/v1beta1/query.proto

### QueryAccountRequest

QueryAccountRequest is the request type for the Query/Account RPC method.

| Field     | Type                       | Label | Description                               |
| --------- | -------------------------- | ----- | ----------------------------------------- |
| `address` | [string](broken-reference) |       | address defines the address to query for. |

### QueryAccountResponse

QueryAccountResponse is the response type for the Query/Account RPC method.

| Field     | Type                                    | Label | Description                                               |
| --------- | --------------------------------------- | ----- | --------------------------------------------------------- |
| `account` | [google.protobuf.Any](broken-reference) |       | account defines the account of the corresponding address. |

### QueryParamsRequest

QueryParamsRequest is the request type for the Query/Params RPC method.

### QueryParamsResponse

QueryParamsResponse is the response type for the Query/Params RPC method.

| Field    | Type                       | Label | Description                                  |
| -------- | -------------------------- | ----- | -------------------------------------------- |
| `params` | [Params](broken-reference) |       | params defines the parameters of the module. |

### Query

Query defines the gRPC querier service.

| Method Name | Request Type                            | Response Type                            | Description                                       | HTTP Verb | Endpoint                                |
| ----------- | --------------------------------------- | ---------------------------------------- | ------------------------------------------------- | --------- | --------------------------------------- |
| `Account`   | [QueryAccountRequest](broken-reference) | [QueryAccountResponse](broken-reference) | Account returns account details based on address. | GET       | /cosmos/auth/v1beta1/accounts/{address} |
| `Params`    | [QueryParamsRequest](broken-reference)  | [QueryParamsResponse](broken-reference)  | Params queries all parameters.                    | GET       | /cosmos/auth/v1beta1/params             |

## cosmos/bank/v1beta1/bank.proto

### DenomUnit

DenomUnit represents a struct that describes a given denomination unit of the basic token.

| Field      | Type                       | Label    | Description                                                                                                                                                                                                                                                                           |
| ---------- | -------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `denom`    | [string](broken-reference) |          | denom represents the string name of the given denom unit (e.g uatom).                                                                                                                                                                                                                 |
| `exponent` | [uint32](broken-reference) |          | exponent represents power of 10 exponent that one must raise the base\_denom to in order to equal the given DenomUnit's denom 1 denom = 1^exponent base\_denom (e.g. with a base\_denom of uatom, one can create a DenomUnit of 'atom' with exponent = 6, thus: 1 atom = 10^6 uatom). |
| `aliases`  | [string](broken-reference) | repeated | aliases is a list of string aliases for the given denom                                                                                                                                                                                                                               |

### Input

Input models transaction input.

| Field     | Type                                         | Label    | Description |
| --------- | -------------------------------------------- | -------- | ----------- |
| `address` | [string](broken-reference)                   |          |             |
| `coins`   | [cosmos.base.v1beta1.Coin](broken-reference) | repeated |             |

### Metadata

Metadata represents a struct that describes a basic token.

| Field         | Type                          | Label    | Description                                                                 |
| ------------- | ----------------------------- | -------- | --------------------------------------------------------------------------- |
| `description` | [string](broken-reference)    |          |                                                                             |
| `denom_units` | [DenomUnit](broken-reference) | repeated | denom\_units represents the list of DenomUnit's for a given coin            |
| `base`        | [string](broken-reference)    |          | base represents the base denom (should be the DenomUnit with exponent = 0). |
| `display`     | [string](broken-reference)    |          | display indicates the suggested denom that should be displayed in clients.  |

### Output

Output models transaction outputs.

| Field     | Type                                         | Label    | Description |
| --------- | -------------------------------------------- | -------- | ----------- |
| `address` | [string](broken-reference)                   |          |             |
| `coins`   | [cosmos.base.v1beta1.Coin](broken-reference) | repeated |             |

### Params

Params defines the parameters for the bank module.

| Field                  | Type                            | Label    | Description |
| ---------------------- | ------------------------------- | -------- | ----------- |
| `send_enabled`         | [SendEnabled](broken-reference) | repeated |             |
| `default_send_enabled` | [bool](broken-reference)        |          |             |

### SendEnabled

SendEnabled maps coin denom to a send\_enabled status (whether a denom is sendable).

| Field     | Type                       | Label | Description |
| --------- | -------------------------- | ----- | ----------- |
| `denom`   | [string](broken-reference) |       |             |
| `enabled` | [bool](broken-reference)   |       |             |

### Supply

Supply represents a struct that passively keeps track of the total supply amounts in the network.

| Field   | Type                                         | Label    | Description |
| ------- | -------------------------------------------- | -------- | ----------- |
| `total` | [cosmos.base.v1beta1.Coin](broken-reference) | repeated |             |

## cosmos/bank/v1beta1/genesis.proto

### Balance

Balance defines an account address and balance pair used in the bank module's genesis state.

| Field     | Type                                         | Label    | Description                                           |
| --------- | -------------------------------------------- | -------- | ----------------------------------------------------- |
| `address` | [string](broken-reference)                   |          | address is the address of the balance holder.         |
| `coins`   | [cosmos.base.v1beta1.Coin](broken-reference) | repeated | coins defines the different coins this balance holds. |

### GenesisState

GenesisState defines the bank module's genesis state.

| Field            | Type                                         | Label    | Description                                                       |
| ---------------- | -------------------------------------------- | -------- | ----------------------------------------------------------------- |
| `params`         | [Params](broken-reference)                   |          | params defines all the paramaters of the module.                  |
| `balances`       | [Balance](broken-reference)                  | repeated | balances is an array containing the balances of all the accounts. |
| `supply`         | [cosmos.base.v1beta1.Coin](broken-reference) | repeated | supply represents the total supply.                               |
| `denom_metadata` | [Metadata](broken-reference)                 | repeated | denom\_metadata defines the metadata of the differents coins.     |

## cosmos/bank/v1beta1/query.proto

### QueryAllBalancesRequest

QueryBalanceRequest is the request type for the Query/AllBalances RPC method.

| Field        | Type                                                      | Label | Description                                                |
| ------------ | --------------------------------------------------------- | ----- | ---------------------------------------------------------- |
| `address`    | [string](broken-reference)                                |       | address is the address to query balances for.              |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request. |

### QueryAllBalancesResponse

QueryAllBalancesResponse is the response type for the Query/AllBalances RPC method.

| Field        | Type                                                       | Label    | Description                                        |
| ------------ | ---------------------------------------------------------- | -------- | -------------------------------------------------- |
| `balances`   | [cosmos.base.v1beta1.Coin](broken-reference)               | repeated | balances is the balances of all the coins.         |
| `pagination` | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response. |

### QueryBalanceRequest

QueryBalanceRequest is the request type for the Query/Balance RPC method.

| Field     | Type                       | Label | Description                                    |
| --------- | -------------------------- | ----- | ---------------------------------------------- |
| `address` | [string](broken-reference) |       | address is the address to query balances for.  |
| `denom`   | [string](broken-reference) |       | denom is the coin denom to query balances for. |

### QueryBalanceResponse

QueryBalanceResponse is the response type for the Query/Balance RPC method.

| Field     | Type                                         | Label | Description                         |
| --------- | -------------------------------------------- | ----- | ----------------------------------- |
| `balance` | [cosmos.base.v1beta1.Coin](broken-reference) |       | balance is the balance of the coin. |

### QueryDenomMetadataRequest

QueryDenomMetadataRequest is the request type for the Query/DenomMetadata RPC method.

| Field   | Type                       | Label | Description                                        |
| ------- | -------------------------- | ----- | -------------------------------------------------- |
| `denom` | [string](broken-reference) |       | denom is the coin denom to query the metadata for. |

### QueryDenomMetadataResponse

QueryDenomMetadataResponse is the response type for the Query/DenomMetadata RPC method.

| Field      | Type                         | Label | Description                                                                         |
| ---------- | ---------------------------- | ----- | ----------------------------------------------------------------------------------- |
| `metadata` | [Metadata](broken-reference) |       | metadata describes and provides all the client information for the requested token. |

### QueryDenomsMetadataRequest

QueryDenomsMetadataRequest is the request type for the Query/DenomsMetadata RPC method.

| Field        | Type                                                      | Label | Description                                                |
| ------------ | --------------------------------------------------------- | ----- | ---------------------------------------------------------- |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request. |

### QueryDenomsMetadataResponse

QueryDenomsMetadataResponse is the response type for the Query/DenomsMetadata RPC method.

| Field        | Type                                                       | Label    | Description                                                             |
| ------------ | ---------------------------------------------------------- | -------- | ----------------------------------------------------------------------- |
| `metadatas`  | [Metadata](broken-reference)                               | repeated | metadata provides the client information for all the registered tokens. |
| `pagination` | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response.                      |

### QueryParamsRequest

QueryParamsRequest defines the request type for querying x/bank parameters.

### QueryParamsResponse

QueryParamsResponse defines the response type for querying x/bank parameters.

| Field    | Type                       | Label | Description |
| -------- | -------------------------- | ----- | ----------- |
| `params` | [Params](broken-reference) |       |             |

### QuerySupplyOfRequest

QuerySupplyOfRequest is the request type for the Query/SupplyOf RPC method.

| Field   | Type                       | Label | Description                                    |
| ------- | -------------------------- | ----- | ---------------------------------------------- |
| `denom` | [string](broken-reference) |       | denom is the coin denom to query balances for. |

### QuerySupplyOfResponse

QuerySupplyOfResponse is the response type for the Query/SupplyOf RPC method.

| Field    | Type                                         | Label | Description                       |
| -------- | -------------------------------------------- | ----- | --------------------------------- |
| `amount` | [cosmos.base.v1beta1.Coin](broken-reference) |       | amount is the supply of the coin. |

### QueryTotalSupplyRequest

QueryTotalSupplyRequest is the request type for the Query/TotalSupply RPC method.

### QueryTotalSupplyResponse

QueryTotalSupplyResponse is the response type for the Query/TotalSupply RPC method

| Field    | Type                                         | Label    | Description                       |
| -------- | -------------------------------------------- | -------- | --------------------------------- |
| `supply` | [cosmos.base.v1beta1.Coin](broken-reference) | repeated | supply is the supply of the coins |

### Query

Query defines the gRPC querier service.

| Method Name      | Request Type                                   | Response Type                                   | Description                                                                       | HTTP Verb | Endpoint                                        |
| ---------------- | ---------------------------------------------- | ----------------------------------------------- | --------------------------------------------------------------------------------- | --------- | ----------------------------------------------- |
| `Balance`        | [QueryBalanceRequest](broken-reference)        | [QueryBalanceResponse](broken-reference)        | Balance queries the balance of a single coin for a single account.                | GET       | /cosmos/bank/v1beta1/balances/{address}/{denom} |
| `AllBalances`    | [QueryAllBalancesRequest](broken-reference)    | [QueryAllBalancesResponse](broken-reference)    | AllBalances queries the balance of all coins for a single account.                | GET       | /cosmos/bank/v1beta1/balances/{address}         |
| `TotalSupply`    | [QueryTotalSupplyRequest](broken-reference)    | [QueryTotalSupplyResponse](broken-reference)    | TotalSupply queries the total supply of all coins.                                | GET       | /cosmos/bank/v1beta1/supply                     |
| `SupplyOf`       | [QuerySupplyOfRequest](broken-reference)       | [QuerySupplyOfResponse](broken-reference)       | SupplyOf queries the supply of a single coin.                                     | GET       | /cosmos/bank/v1beta1/supply/{denom}             |
| `Params`         | [QueryParamsRequest](broken-reference)         | [QueryParamsResponse](broken-reference)         | Params queries the parameters of x/bank module.                                   | GET       | /cosmos/bank/v1beta1/params                     |
| `DenomMetadata`  | [QueryDenomMetadataRequest](broken-reference)  | [QueryDenomMetadataResponse](broken-reference)  | DenomsMetadata queries the client metadata of a given coin denomination.          | GET       | /cosmos/bank/v1beta1/denoms\_metadata/{denom}   |
| `DenomsMetadata` | [QueryDenomsMetadataRequest](broken-reference) | [QueryDenomsMetadataResponse](broken-reference) | DenomsMetadata queries the client metadata for all registered coin denominations. | GET       | /cosmos/bank/v1beta1/denoms\_metadata           |

## cosmos/bank/v1beta1/tx.proto

### MsgMultiSend

MsgMultiSend represents an arbitrary multi-in, multi-out send message.

| Field     | Type                       | Label    | Description |
| --------- | -------------------------- | -------- | ----------- |
| `inputs`  | [Input](broken-reference)  | repeated |             |
| `outputs` | [Output](broken-reference) | repeated |             |

### MsgMultiSendResponse

MsgMultiSendResponse defines the Msg/MultiSend response type.

### MsgSend

MsgSend represents a message to send coins from one account to another.

| Field          | Type                                         | Label    | Description |
| -------------- | -------------------------------------------- | -------- | ----------- |
| `from_address` | [string](broken-reference)                   |          |             |
| `to_address`   | [string](broken-reference)                   |          |             |
| `amount`       | [cosmos.base.v1beta1.Coin](broken-reference) | repeated |             |

### MsgSendResponse

MsgSendResponse defines the Msg/Send response type.

### Msg

Msg defines the bank Msg service.

| Method Name | Request Type                     | Response Type                            | Description                                                                        | HTTP Verb | Endpoint |
| ----------- | -------------------------------- | ---------------------------------------- | ---------------------------------------------------------------------------------- | --------- | -------- |
| `Send`      | [MsgSend](broken-reference)      | [MsgSendResponse](broken-reference)      | Send defines a method for sending coins from one account to another account.       |           |          |
| `MultiSend` | [MsgMultiSend](broken-reference) | [MsgMultiSendResponse](broken-reference) | MultiSend defines a method for sending coins from some accounts to other accounts. |           |          |

## cosmos/base/abci/v1beta1/abci.proto

### ABCIMessageLog

ABCIMessageLog defines a structure containing an indexed tx ABCI message log.

| Field       | Type                            | Label    | Description                                                                       |
| ----------- | ------------------------------- | -------- | --------------------------------------------------------------------------------- |
| `msg_index` | [uint32](broken-reference)      |          |                                                                                   |
| `log`       | [string](broken-reference)      |          |                                                                                   |
| `events`    | [StringEvent](broken-reference) | repeated | Events contains a slice of Event objects that were emitted during some execution. |

### Attribute

Attribute defines an attribute wrapper where the key and value are strings instead of raw bytes.

| Field   | Type                       | Label | Description |
| ------- | -------------------------- | ----- | ----------- |
| `key`   | [string](broken-reference) |       |             |
| `value` | [string](broken-reference) |       |             |

### GasInfo

GasInfo defines tx execution gas context.

| Field        | Type                       | Label | Description                                                         |
| ------------ | -------------------------- | ----- | ------------------------------------------------------------------- |
| `gas_wanted` | [uint64](broken-reference) |       | GasWanted is the maximum units of work we allow this tx to perform. |
| `gas_used`   | [uint64](broken-reference) |       | GasUsed is the amount of gas actually consumed.                     |

### MsgData

MsgData defines the data returned in a Result object during message execution.

| Field      | Type                       | Label | Description |
| ---------- | -------------------------- | ----- | ----------- |
| `msg_type` | [string](broken-reference) |       |             |
| `data`     | [bytes](broken-reference)  |       |             |

### Result

Result is the union of ResponseFormat and ResponseCheckTx.

| Field    | Type                                      | Label    | Description                                                                                                                                         |
| -------- | ----------------------------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| `data`   | [bytes](broken-reference)                 |          | Data is any data returned from message or handler execution. It MUST be length prefixed in order to separate data from multiple message executions. |
| `log`    | [string](broken-reference)                |          | Log contains the log information from message or handler execution.                                                                                 |
| `events` | [tendermint.abci.Event](broken-reference) | repeated | Events contains a slice of Event objects that were emitted during message or handler execution.                                                     |

### SearchTxsResult

SearchTxsResult defines a structure for querying txs pageable

| Field         | Type                           | Label    | Description                         |
| ------------- | ------------------------------ | -------- | ----------------------------------- |
| `total_count` | [uint64](broken-reference)     |          | Count of all txs                    |
| `count`       | [uint64](broken-reference)     |          | Count of txs in current page        |
| `page_number` | [uint64](broken-reference)     |          | Index of current page, start from 1 |
| `page_total`  | [uint64](broken-reference)     |          | Count of total pages                |
| `limit`       | [uint64](broken-reference)     |          | Max count txs per page              |
| `txs`         | [TxResponse](broken-reference) | repeated | List of txs in current page         |

### SimulationResponse

SimulationResponse defines the response generated when a transaction is successfully simulated.

| Field      | Type                        | Label | Description |
| ---------- | --------------------------- | ----- | ----------- |
| `gas_info` | [GasInfo](broken-reference) |       |             |
| `result`   | [Result](broken-reference)  |       |             |

### StringEvent

StringEvent defines en Event object wrapper where all the attributes contain key/value pairs that are strings instead of raw bytes.

| Field        | Type                          | Label    | Description |
| ------------ | ----------------------------- | -------- | ----------- |
| `type`       | [string](broken-reference)    |          |             |
| `attributes` | [Attribute](broken-reference) | repeated |             |

### TxMsgData

TxMsgData defines a list of MsgData. A transaction will have a MsgData object for each message.

| Field  | Type                        | Label    | Description |
| ------ | --------------------------- | -------- | ----------- |
| `data` | [MsgData](broken-reference) | repeated |             |

### TxResponse

TxResponse defines a structure containing relevant tx data and metadata. The tags are stringified and the log is JSON decoded.

| Field        | Type                                    | Label    | Description                                                                                                                                                             |
| ------------ | --------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `height`     | [int64](broken-reference)               |          | The block height                                                                                                                                                        |
| `txhash`     | [string](broken-reference)              |          | The transaction hash.                                                                                                                                                   |
| `codespace`  | [string](broken-reference)              |          | Namespace for the Code                                                                                                                                                  |
| `code`       | [uint32](broken-reference)              |          | Response code.                                                                                                                                                          |
| `data`       | [string](broken-reference)              |          | Result bytes, if any.                                                                                                                                                   |
| `raw_log`    | [string](broken-reference)              |          | The output of the application's logger (raw string). May be non-deterministic.                                                                                          |
| `logs`       | [ABCIMessageLog](broken-reference)      | repeated | The output of the application's logger (typed). May be non-deterministic.                                                                                               |
| `info`       | [string](broken-reference)              |          | Additional information. May be non-deterministic.                                                                                                                       |
| `gas_wanted` | [int64](broken-reference)               |          | Amount of gas requested for transaction.                                                                                                                                |
| `gas_used`   | [int64](broken-reference)               |          | Amount of gas consumed by transaction.                                                                                                                                  |
| `tx`         | [google.protobuf.Any](broken-reference) |          | The request transaction bytes.                                                                                                                                          |
| `timestamp`  | [string](broken-reference)              |          | Time of the previous block. For heights > 1, it's the weighted median of the timestamps of the valid votes in the block.LastCommit. For height == 1, it's genesis time. |

## cosmos/base/kv/v1beta1/kv.proto

### Pair

Pair defines a key/value bytes tuple.

| Field   | Type                      | Label | Description |
| ------- | ------------------------- | ----- | ----------- |
| `key`   | [bytes](broken-reference) |       |             |
| `value` | [bytes](broken-reference) |       |             |

### Pairs

Pairs defines a repeated slice of Pair objects.

| Field   | Type                     | Label    | Description |
| ------- | ------------------------ | -------- | ----------- |
| `pairs` | [Pair](broken-reference) | repeated |             |

## cosmos/base/reflection/v1beta1/reflection.proto

### ListAllInterfacesRequest

ListAllInterfacesRequest is the request type of the ListAllInterfaces RPC.

### ListAllInterfacesResponse

ListAllInterfacesResponse is the response type of the ListAllInterfaces RPC.

| Field             | Type                       | Label    | Description                                                    |
| ----------------- | -------------------------- | -------- | -------------------------------------------------------------- |
| `interface_names` | [string](broken-reference) | repeated | interface\_names is an array of all the registered interfaces. |

### ListImplementationsRequest

ListImplementationsRequest is the request type of the ListImplementations RPC.

| Field            | Type                       | Label | Description                                                             |
| ---------------- | -------------------------- | ----- | ----------------------------------------------------------------------- |
| `interface_name` | [string](broken-reference) |       | interface\_name defines the interface to query the implementations for. |

### ListImplementationsResponse

ListImplementationsResponse is the response type of the ListImplementations RPC.

| Field                          | Type                       | Label    | Description |
| ------------------------------ | -------------------------- | -------- | ----------- |
| `implementation_message_names` | [string](broken-reference) | repeated |             |

### ReflectionService

ReflectionService defines a service for interface reflection.

| Method Name           | Request Type                                   | Response Type                                   | Description                                                                       | HTTP Verb | Endpoint                                                                     |
| --------------------- | ---------------------------------------------- | ----------------------------------------------- | --------------------------------------------------------------------------------- | --------- | ---------------------------------------------------------------------------- |
| `ListAllInterfaces`   | [ListAllInterfacesRequest](broken-reference)   | [ListAllInterfacesResponse](broken-reference)   | ListAllInterfaces lists all the interfaces registered in the interface registry.  | GET       | /cosmos/base/reflection/v1beta1/interfaces                                   |
| `ListImplementations` | [ListImplementationsRequest](broken-reference) | [ListImplementationsResponse](broken-reference) | ListImplementations list all the concrete types that implement a given interface. | GET       | /cosmos/base/reflection/v1beta1/interfaces/{interface\_name}/implementations |

## cosmos/base/snapshots/v1beta1/snapshot.proto

### Metadata

Metadata contains SDK-specific snapshot metadata.

| Field          | Type                      | Label    | Description          |
| -------------- | ------------------------- | -------- | -------------------- |
| `chunk_hashes` | [bytes](broken-reference) | repeated | SHA-256 chunk hashes |

### Snapshot

Snapshot contains Tendermint state sync snapshot info.

| Field      | Type                         | Label | Description |
| ---------- | ---------------------------- | ----- | ----------- |
| `height`   | [uint64](broken-reference)   |       |             |
| `format`   | [uint32](broken-reference)   |       |             |
| `chunks`   | [uint32](broken-reference)   |       |             |
| `hash`     | [bytes](broken-reference)    |       |             |
| `metadata` | [Metadata](broken-reference) |       |             |

## cosmos/base/store/v1beta1/commit\_info.proto

### CommitID

CommitID defines the committment information when a specific store is committed.

| Field     | Type                      | Label | Description |
| --------- | ------------------------- | ----- | ----------- |
| `version` | [int64](broken-reference) |       |             |
| `hash`    | [bytes](broken-reference) |       |             |

### CommitInfo

CommitInfo defines commit information used by the multi-store when committing a version/height.

| Field         | Type                          | Label    | Description |
| ------------- | ----------------------------- | -------- | ----------- |
| `version`     | [int64](broken-reference)     |          |             |
| `store_infos` | [StoreInfo](broken-reference) | repeated |             |

### StoreInfo

StoreInfo defines store-specific commit information. It contains a reference between a store name and the commit ID.

| Field       | Type                         | Label | Description |
| ----------- | ---------------------------- | ----- | ----------- |
| `name`      | [string](broken-reference)   |       |             |
| `commit_id` | [CommitID](broken-reference) |       |             |

## cosmos/base/store/v1beta1/snapshot.proto

### SnapshotIAVLItem

SnapshotIAVLItem is an exported IAVL node.

| Field     | Type                      | Label | Description |
| --------- | ------------------------- | ----- | ----------- |
| `key`     | [bytes](broken-reference) |       |             |
| `value`   | [bytes](broken-reference) |       |             |
| `version` | [int64](broken-reference) |       |             |
| `height`  | [int32](broken-reference) |       |             |

### SnapshotItem

SnapshotItem is an item contained in a rootmulti.Store snapshot.

| Field   | Type                                  | Label | Description |
| ------- | ------------------------------------- | ----- | ----------- |
| `store` | [SnapshotStoreItem](broken-reference) |       |             |
| `iavl`  | [SnapshotIAVLItem](broken-reference)  |       |             |

### SnapshotStoreItem

SnapshotStoreItem contains metadata about a snapshotted store.

| Field  | Type                       | Label | Description |
| ------ | -------------------------- | ----- | ----------- |
| `name` | [string](broken-reference) |       |             |

## cosmos/base/tendermint/v1beta1/query.proto

### GetBlockByHeightRequest

GetBlockByHeightRequest is the request type for the Query/GetBlockByHeight RPC method.

| Field    | Type                      | Label | Description |
| -------- | ------------------------- | ----- | ----------- |
| `height` | [int64](broken-reference) |       |             |

### GetBlockByHeightResponse

GetBlockByHeightResponse is the response type for the Query/GetBlockByHeight RPC method.

| Field      | Type                                         | Label | Description |
| ---------- | -------------------------------------------- | ----- | ----------- |
| `block_id` | [tendermint.types.BlockID](broken-reference) |       |             |
| `block`    | [tendermint.types.Block](broken-reference)   |       |             |

### GetLatestBlockRequest

GetLatestBlockRequest is the request type for the Query/GetLatestBlock RPC method.

### GetLatestBlockResponse

GetLatestBlockResponse is the response type for the Query/GetLatestBlock RPC method.

| Field      | Type                                         | Label | Description |
| ---------- | -------------------------------------------- | ----- | ----------- |
| `block_id` | [tendermint.types.BlockID](broken-reference) |       |             |
| `block`    | [tendermint.types.Block](broken-reference)   |       |             |

### GetLatestValidatorSetRequest

GetLatestValidatorSetRequest is the request type for the Query/GetValidatorSetByHeight RPC method.

| Field        | Type                                                      | Label | Description                                       |
| ------------ | --------------------------------------------------------- | ----- | ------------------------------------------------- |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an pagination for the request. |

### GetLatestValidatorSetResponse

GetLatestValidatorSetResponse is the response type for the Query/GetValidatorSetByHeight RPC method.

| Field          | Type                                                       | Label    | Description                                        |
| -------------- | ---------------------------------------------------------- | -------- | -------------------------------------------------- |
| `block_height` | [int64](broken-reference)                                  |          |                                                    |
| `validators`   | [Validator](broken-reference)                              | repeated |                                                    |
| `pagination`   | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines an pagination for the response. |

### GetNodeInfoRequest

GetNodeInfoRequest is the request type for the Query/GetNodeInfo RPC method.

### GetNodeInfoResponse

GetNodeInfoResponse is the request type for the Query/GetNodeInfo RPC method.

| Field                 | Type                                               | Label | Description |
| --------------------- | -------------------------------------------------- | ----- | ----------- |
| `default_node_info`   | [tendermint.p2p.DefaultNodeInfo](broken-reference) |       |             |
| `application_version` | [VersionInfo](broken-reference)                    |       |             |

### GetSyncingRequest

GetSyncingRequest is the request type for the Query/GetSyncing RPC method.

### GetSyncingResponse

GetSyncingResponse is the response type for the Query/GetSyncing RPC method.

| Field     | Type                     | Label | Description |
| --------- | ------------------------ | ----- | ----------- |
| `syncing` | [bool](broken-reference) |       |             |

### GetValidatorSetByHeightRequest

GetValidatorSetByHeightRequest is the request type for the Query/GetValidatorSetByHeight RPC method.

| Field        | Type                                                      | Label | Description                                       |
| ------------ | --------------------------------------------------------- | ----- | ------------------------------------------------- |
| `height`     | [int64](broken-reference)                                 |       |                                                   |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an pagination for the request. |

### GetValidatorSetByHeightResponse

GetValidatorSetByHeightResponse is the response type for the Query/GetValidatorSetByHeight RPC method.

| Field          | Type                                                       | Label    | Description                                        |
| -------------- | ---------------------------------------------------------- | -------- | -------------------------------------------------- |
| `block_height` | [int64](broken-reference)                                  |          |                                                    |
| `validators`   | [Validator](broken-reference)                              | repeated |                                                    |
| `pagination`   | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines an pagination for the response. |

### Module

Module is the type for VersionInfo

| Field     | Type                       | Label | Description    |
| --------- | -------------------------- | ----- | -------------- |
| `path`    | [string](broken-reference) |       | module path    |
| `version` | [string](broken-reference) |       | module version |
| `sum`     | [string](broken-reference) |       | checksum       |

### Validator

Validator is the type for the validator-set.

| Field               | Type                                    | Label | Description |
| ------------------- | --------------------------------------- | ----- | ----------- |
| `address`           | [string](broken-reference)              |       |             |
| `pub_key`           | [google.protobuf.Any](broken-reference) |       |             |
| `voting_power`      | [int64](broken-reference)               |       |             |
| `proposer_priority` | [int64](broken-reference)               |       |             |

### VersionInfo

VersionInfo is the type for the GetNodeInfoResponse message.

| Field                | Type                       | Label    | Description |
| -------------------- | -------------------------- | -------- | ----------- |
| `name`               | [string](broken-reference) |          |             |
| `app_name`           | [string](broken-reference) |          |             |
| `version`            | [string](broken-reference) |          |             |
| `git_commit`         | [string](broken-reference) |          |             |
| `build_tags`         | [string](broken-reference) |          |             |
| `go_version`         | [string](broken-reference) |          |             |
| `build_deps`         | [Module](broken-reference) | repeated |             |
| `cosmos_sdk_version` | [string](broken-reference) |          |             |

### Service

Service defines the gRPC querier service for tendermint queries.

| Method Name               | Request Type                                       | Response Type                                       | Description                                                      | HTTP Verb | Endpoint                                               |
| ------------------------- | -------------------------------------------------- | --------------------------------------------------- | ---------------------------------------------------------------- | --------- | ------------------------------------------------------ |
| `GetNodeInfo`             | [GetNodeInfoRequest](broken-reference)             | [GetNodeInfoResponse](broken-reference)             | GetNodeInfo queries the current node info.                       | GET       | /cosmos/base/tendermint/v1beta1/node\_info             |
| `GetSyncing`              | [GetSyncingRequest](broken-reference)              | [GetSyncingResponse](broken-reference)              | GetSyncing queries node syncing.                                 | GET       | /cosmos/base/tendermint/v1beta1/syncing                |
| `GetLatestBlock`          | [GetLatestBlockRequest](broken-reference)          | [GetLatestBlockResponse](broken-reference)          | GetLatestBlock returns the latest block.                         | GET       | /cosmos/base/tendermint/v1beta1/blocks/latest          |
| `GetBlockByHeight`        | [GetBlockByHeightRequest](broken-reference)        | [GetBlockByHeightResponse](broken-reference)        | GetBlockByHeight queries block for given height.                 | GET       | /cosmos/base/tendermint/v1beta1/blocks/{height}        |
| `GetLatestValidatorSet`   | [GetLatestValidatorSetRequest](broken-reference)   | [GetLatestValidatorSetResponse](broken-reference)   | GetLatestValidatorSet queries latest validator-set.              | GET       | /cosmos/base/tendermint/v1beta1/validatorsets/latest   |
| `GetValidatorSetByHeight` | [GetValidatorSetByHeightRequest](broken-reference) | [GetValidatorSetByHeightResponse](broken-reference) | GetValidatorSetByHeight queries validator-set at a given height. | GET       | /cosmos/base/tendermint/v1beta1/validatorsets/{height} |

## cosmos/capability/v1beta1/capability.proto

### Capability

Capability defines an implementation of an object capability. The index provided to a Capability must be globally unique.

| Field   | Type                       | Label | Description |
| ------- | -------------------------- | ----- | ----------- |
| `index` | [uint64](broken-reference) |       |             |

### CapabilityOwners

CapabilityOwners defines a set of owners of a single Capability. The set of owners must be unique.

| Field    | Type                      | Label    | Description |
| -------- | ------------------------- | -------- | ----------- |
| `owners` | [Owner](broken-reference) | repeated |             |

### Owner

Owner defines a single capability owner. An owner is defined by the name of capability and the module name.

| Field    | Type                       | Label | Description |
| -------- | -------------------------- | ----- | ----------- |
| `module` | [string](broken-reference) |       |             |
| `name`   | [string](broken-reference) |       |             |

## cosmos/capability/v1beta1/genesis.proto

### GenesisOwners

GenesisOwners defines the capability owners with their corresponding index.

| Field          | Type                                 | Label | Description                                      |
| -------------- | ------------------------------------ | ----- | ------------------------------------------------ |
| `index`        | [uint64](broken-reference)           |       | index is the index of the capability owner.      |
| `index_owners` | [CapabilityOwners](broken-reference) |       | index\_owners are the owners at the given index. |

### GenesisState

GenesisState defines the capability module's genesis state.

| Field    | Type                              | Label    | Description                                                                                                          |
| -------- | --------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------- |
| `index`  | [uint64](broken-reference)        |          | index is the capability global index.                                                                                |
| `owners` | [GenesisOwners](broken-reference) | repeated | owners represents a map from index to owners of the capability index index key is string to allow amino marshalling. |

## cosmos/crisis/v1beta1/genesis.proto

### GenesisState

GenesisState defines the crisis module's genesis state.

| Field          | Type                                         | Label | Description                                                                 |
| -------------- | -------------------------------------------- | ----- | --------------------------------------------------------------------------- |
| `constant_fee` | [cosmos.base.v1beta1.Coin](broken-reference) |       | constant\_fee is the fee used to verify the invariant in the crisis module. |

## cosmos/crisis/v1beta1/tx.proto

### MsgVerifyInvariant

MsgVerifyInvariant represents a message to verify a particular invariance.

| Field                   | Type                       | Label | Description |
| ----------------------- | -------------------------- | ----- | ----------- |
| `sender`                | [string](broken-reference) |       |             |
| `invariant_module_name` | [string](broken-reference) |       |             |
| `invariant_route`       | [string](broken-reference) |       |             |

### MsgVerifyInvariantResponse

MsgVerifyInvariantResponse defines the Msg/VerifyInvariant response type.

### Msg

Msg defines the bank Msg service.

| Method Name       | Request Type                           | Response Type                                  | Description                                                         | HTTP Verb | Endpoint |
| ----------------- | -------------------------------------- | ---------------------------------------------- | ------------------------------------------------------------------- | --------- | -------- |
| `VerifyInvariant` | [MsgVerifyInvariant](broken-reference) | [MsgVerifyInvariantResponse](broken-reference) | VerifyInvariant defines a method to verify a particular invariance. |           |          |

## cosmos/crypto/ed25519/keys.proto

### PrivKey

PrivKey defines a ed25519 private key.

| Field | Type                      | Label | Description |
| ----- | ------------------------- | ----- | ----------- |
| `key` | [bytes](broken-reference) |       |             |

### PubKey

PubKey defines a ed25519 public key Key is the compressed form of the pubkey. The first byte depends is a 0x02 byte if the y-coordinate is the lexicographically largest of the two associated with the x-coordinate. Otherwise the first byte is a 0x03. This prefix is followed with the x-coordinate.

| Field | Type                      | Label | Description |
| ----- | ------------------------- | ----- | ----------- |
| `key` | [bytes](broken-reference) |       |             |

## cosmos/crypto/multisig/keys.proto

### LegacyAminoPubKey

LegacyAminoPubKey specifies a public key type which nests multiple public keys and a threshold, it uses legacy amino address rules.

| Field         | Type                                    | Label    | Description |
| ------------- | --------------------------------------- | -------- | ----------- |
| `threshold`   | [uint32](broken-reference)              |          |             |
| `public_keys` | [google.protobuf.Any](broken-reference) | repeated |             |

## cosmos/crypto/multisig/v1beta1/multisig.proto

### CompactBitArray

CompactBitArray is an implementation of a space efficient bit array. This is used to ensure that the encoded data takes up a minimal amount of space after proto encoding. This is not thread safe, and is not intended for concurrent usage.

| Field               | Type                       | Label | Description |
| ------------------- | -------------------------- | ----- | ----------- |
| `extra_bits_stored` | [uint32](broken-reference) |       |             |
| `elems`             | [bytes](broken-reference)  |       |             |

### MultiSignature

MultiSignature wraps the signatures from a multisig.LegacyAminoPubKey. See cosmos.tx.v1betata1.ModeInfo.Multi for how to specify which signers signed and with which modes.

| Field        | Type                      | Label    | Description |
| ------------ | ------------------------- | -------- | ----------- |
| `signatures` | [bytes](broken-reference) | repeated |             |

## cosmos/crypto/secp256k1/keys.proto

### PrivKey

PrivKey defines a secp256k1 private key.

| Field | Type                      | Label | Description |
| ----- | ------------------------- | ----- | ----------- |
| `key` | [bytes](broken-reference) |       |             |

### PubKey

PubKey defines a secp256k1 public key Key is the compressed form of the pubkey. The first byte depends is a 0x02 byte if the y-coordinate is the lexicographically largest of the two associated with the x-coordinate. Otherwise the first byte is a 0x03. This prefix is followed with the x-coordinate.

| Field | Type                      | Label | Description |
| ----- | ------------------------- | ----- | ----------- |
| `key` | [bytes](broken-reference) |       |             |

## cosmos/distribution/v1beta1/distribution.proto

### CommunityPoolSpendProposal

CommunityPoolSpendProposal details a proposal for use of community funds, together with how many coins are proposed to be spent, and to which recipient account.

| Field         | Type                                         | Label    | Description |
| ------------- | -------------------------------------------- | -------- | ----------- |
| `title`       | [string](broken-reference)                   |          |             |
| `description` | [string](broken-reference)                   |          |             |
| `recipient`   | [string](broken-reference)                   |          |             |
| `amount`      | [cosmos.base.v1beta1.Coin](broken-reference) | repeated |             |

### CommunityPoolSpendProposalWithDeposit

CommunityPoolSpendProposalWithDeposit defines a CommunityPoolSpendProposal with a deposit

| Field         | Type                       | Label | Description |
| ------------- | -------------------------- | ----- | ----------- |
| `title`       | [string](broken-reference) |       |             |
| `description` | [string](broken-reference) |       |             |
| `recipient`   | [string](broken-reference) |       |             |
| `amount`      | [string](broken-reference) |       |             |
| `deposit`     | [string](broken-reference) |       |             |

### DelegationDelegatorReward

DelegationDelegatorReward represents the properties of a delegator's delegation reward.

| Field               | Type                                            | Label    | Description |
| ------------------- | ----------------------------------------------- | -------- | ----------- |
| `validator_address` | [string](broken-reference)                      |          |             |
| `reward`            | [cosmos.base.v1beta1.DecCoin](broken-reference) | repeated |             |

### DelegatorStartingInfo

DelegatorStartingInfo represents the starting info for a delegator reward period. It tracks the previous validator period, the delegation's amount of staking token, and the creation height (to check later on if any slashes have occurred). NOTE: Even though validators are slashed to whole staking tokens, the delegators within the validator may be left with less than a full token, thus sdk.Dec is used.

| Field             | Type                       | Label | Description |
| ----------------- | -------------------------- | ----- | ----------- |
| `previous_period` | [uint64](broken-reference) |       |             |
| `stake`           | [string](broken-reference) |       |             |
| `height`          | [uint64](broken-reference) |       |             |

### FeePool

FeePool is the global fee pool for distribution.

| Field            | Type                                            | Label    | Description |
| ---------------- | ----------------------------------------------- | -------- | ----------- |
| `community_pool` | [cosmos.base.v1beta1.DecCoin](broken-reference) | repeated |             |

### Params

Params defines the set of params for the distribution module.

| Field                   | Type                       | Label | Description |
| ----------------------- | -------------------------- | ----- | ----------- |
| `community_tax`         | [string](broken-reference) |       |             |
| `base_proposer_reward`  | [string](broken-reference) |       |             |
| `bonus_proposer_reward` | [string](broken-reference) |       |             |
| `withdraw_addr_enabled` | [bool](broken-reference)   |       |             |

### ValidatorAccumulatedCommission

ValidatorAccumulatedCommission represents accumulated commission for a validator kept as a running counter, can be withdrawn at any time.

| Field        | Type                                            | Label    | Description |
| ------------ | ----------------------------------------------- | -------- | ----------- |
| `commission` | [cosmos.base.v1beta1.DecCoin](broken-reference) | repeated |             |

### ValidatorCurrentRewards

ValidatorCurrentRewards represents current rewards and current period for a validator kept as a running counter and incremented each block as long as the validator's tokens remain constant.

| Field     | Type                                            | Label    | Description |
| --------- | ----------------------------------------------- | -------- | ----------- |
| `rewards` | [cosmos.base.v1beta1.DecCoin](broken-reference) | repeated |             |
| `period`  | [uint64](broken-reference)                      |          |             |

### ValidatorHistoricalRewards

ValidatorHistoricalRewards represents historical rewards for a validator. Height is implicit within the store key. Cumulative reward ratio is the sum from the zeroeth period until this period of rewards / tokens, per the spec. The reference count indicates the number of objects which might need to reference this historical entry at any point. ReferenceCount = number of outstanding delegations which ended the associated period (and might need to read that record)

* number of slashes which ended the associated period (and might need to read that record)
* one per validator for the zeroeth period, set on initialization

| Field                     | Type                                            | Label    | Description |
| ------------------------- | ----------------------------------------------- | -------- | ----------- |
| `cumulative_reward_ratio` | [cosmos.base.v1beta1.DecCoin](broken-reference) | repeated |             |
| `reference_count`         | [uint32](broken-reference)                      |          |             |

### ValidatorOutstandingRewards

ValidatorOutstandingRewards represents outstanding (un-withdrawn) rewards for a validator inexpensive to track, allows simple sanity checks.

| Field     | Type                                            | Label    | Description |
| --------- | ----------------------------------------------- | -------- | ----------- |
| `rewards` | [cosmos.base.v1beta1.DecCoin](broken-reference) | repeated |             |

### ValidatorSlashEvent

ValidatorSlashEvent represents a validator slash event. Height is implicit within the store key. This is needed to calculate appropriate amount of staking tokens for delegations which are withdrawn after a slash has occurred.

| Field              | Type                       | Label | Description |
| ------------------ | -------------------------- | ----- | ----------- |
| `validator_period` | [uint64](broken-reference) |       |             |
| `fraction`         | [string](broken-reference) |       |             |

### ValidatorSlashEvents

ValidatorSlashEvents is a collection of ValidatorSlashEvent messages.

| Field                    | Type                                    | Label    | Description |
| ------------------------ | --------------------------------------- | -------- | ----------- |
| `validator_slash_events` | [ValidatorSlashEvent](broken-reference) | repeated |             |

## cosmos/distribution/v1beta1/genesis.proto

### DelegatorStartingInfoRecord

DelegatorStartingInfoRecord used for import / export via genesis json.

| Field               | Type                                      | Label | Description                                              |
| ------------------- | ----------------------------------------- | ----- | -------------------------------------------------------- |
| `delegator_address` | [string](broken-reference)                |       | delegator\_address is the address of the delegator.      |
| `validator_address` | [string](broken-reference)                |       | validator\_address is the address of the validator.      |
| `starting_info`     | [DelegatorStartingInfo](broken-reference) |       | starting\_info defines the starting info of a delegator. |

### DelegatorWithdrawInfo

DelegatorWithdrawInfo is the address for where distributions rewards are withdrawn to by default this struct is only used at genesis to feed in default withdraw addresses.

| Field               | Type                       | Label | Description                                                             |
| ------------------- | -------------------------- | ----- | ----------------------------------------------------------------------- |
| `delegator_address` | [string](broken-reference) |       | delegator\_address is the address of the delegator.                     |
| `withdraw_address`  | [string](broken-reference) |       | withdraw\_address is the address to withdraw the delegation rewards to. |

### GenesisState

GenesisState defines the distribution module's genesis state.

| Field                               | Type                                                     | Label    | Description                                                                |
| ----------------------------------- | -------------------------------------------------------- | -------- | -------------------------------------------------------------------------- |
| `params`                            | [Params](broken-reference)                               |          | params defines all the paramaters of the module.                           |
| `fee_pool`                          | [FeePool](broken-reference)                              |          | fee\_pool defines the fee pool at genesis.                                 |
| `delegator_withdraw_infos`          | [DelegatorWithdrawInfo](broken-reference)                | repeated | fee\_pool defines the delegator withdraw infos at genesis.                 |
| `previous_proposer`                 | [string](broken-reference)                               |          | fee\_pool defines the previous proposer at genesis.                        |
| `outstanding_rewards`               | [ValidatorOutstandingRewardsRecord](broken-reference)    | repeated | fee\_pool defines the outstanding rewards of all validators at genesis.    |
| `validator_accumulated_commissions` | [ValidatorAccumulatedCommissionRecord](broken-reference) | repeated | fee\_pool defines the accumulated commisions of all validators at genesis. |
| `validator_historical_rewards`      | [ValidatorHistoricalRewardsRecord](broken-reference)     | repeated | fee\_pool defines the historical rewards of all validators at genesis.     |
| `validator_current_rewards`         | [ValidatorCurrentRewardsRecord](broken-reference)        | repeated | fee\_pool defines the current rewards of all validators at genesis.        |
| `delegator_starting_infos`          | [DelegatorStartingInfoRecord](broken-reference)          | repeated | fee\_pool defines the delegator starting infos at genesis.                 |
| `validator_slash_events`            | [ValidatorSlashEventRecord](broken-reference)            | repeated | fee\_pool defines the validator slash events at genesis.                   |

### ValidatorAccumulatedCommissionRecord

ValidatorAccumulatedCommissionRecord is used for import / export via genesis json.

| Field               | Type                                               | Label | Description                                               |
| ------------------- | -------------------------------------------------- | ----- | --------------------------------------------------------- |
| `validator_address` | [string](broken-reference)                         |       | validator\_address is the address of the validator.       |
| `accumulated`       | [ValidatorAccumulatedCommission](broken-reference) |       | accumulated is the accumulated commission of a validator. |

### ValidatorCurrentRewardsRecord

ValidatorCurrentRewardsRecord is used for import / export via genesis json.

| Field               | Type                                        | Label | Description                                         |
| ------------------- | ------------------------------------------- | ----- | --------------------------------------------------- |
| `validator_address` | [string](broken-reference)                  |       | validator\_address is the address of the validator. |
| `rewards`           | [ValidatorCurrentRewards](broken-reference) |       | rewards defines the current rewards of a validator. |

### ValidatorHistoricalRewardsRecord

ValidatorHistoricalRewardsRecord is used for import / export via genesis json.

| Field               | Type                                           | Label | Description                                                |
| ------------------- | ---------------------------------------------- | ----- | ---------------------------------------------------------- |
| `validator_address` | [string](broken-reference)                     |       | validator\_address is the address of the validator.        |
| `period`            | [uint64](broken-reference)                     |       | period defines the period the historical rewards apply to. |
| `rewards`           | [ValidatorHistoricalRewards](broken-reference) |       | rewards defines the historical rewards of a validator.     |

### ValidatorOutstandingRewardsRecord

ValidatorOutstandingRewardsRecord is used for import/export via genesis json.

| Field                 | Type                                            | Label    | Description                                                            |
| --------------------- | ----------------------------------------------- | -------- | ---------------------------------------------------------------------- |
| `validator_address`   | [string](broken-reference)                      |          | validator\_address is the address of the validator.                    |
| `outstanding_rewards` | [cosmos.base.v1beta1.DecCoin](broken-reference) | repeated | outstanding\_rewards represents the oustanding rewards of a validator. |

### ValidatorSlashEventRecord

ValidatorSlashEventRecord is used for import / export via genesis json.

| Field                   | Type                                    | Label | Description                                                       |
| ----------------------- | --------------------------------------- | ----- | ----------------------------------------------------------------- |
| `validator_address`     | [string](broken-reference)              |       | validator\_address is the address of the validator.               |
| `height`                | [uint64](broken-reference)              |       | height defines the block height at which the slash event occured. |
| `period`                | [uint64](broken-reference)              |       | period is the period of the slash event.                          |
| `validator_slash_event` | [ValidatorSlashEvent](broken-reference) |       | validator\_slash\_event describes the slash event.                |

## cosmos/distribution/v1beta1/query.proto

### QueryCommunityPoolRequest

QueryCommunityPoolRequest is the request type for the Query/CommunityPool RPC method.

### QueryCommunityPoolResponse

QueryCommunityPoolResponse is the response type for the Query/CommunityPool RPC method.

| Field  | Type                                            | Label    | Description                          |
| ------ | ----------------------------------------------- | -------- | ------------------------------------ |
| `pool` | [cosmos.base.v1beta1.DecCoin](broken-reference) | repeated | pool defines community pool's coins. |

### QueryDelegationRewardsRequest

QueryDelegationRewardsRequest is the request type for the Query/DelegationRewards RPC method.

| Field               | Type                       | Label | Description                                                    |
| ------------------- | -------------------------- | ----- | -------------------------------------------------------------- |
| `delegator_address` | [string](broken-reference) |       | delegator\_address defines the delegator address to query for. |
| `validator_address` | [string](broken-reference) |       | validator\_address defines the validator address to query for. |

### QueryDelegationRewardsResponse

QueryDelegationRewardsResponse is the response type for the Query/DelegationRewards RPC method.

| Field     | Type                                            | Label    | Description                                          |
| --------- | ----------------------------------------------- | -------- | ---------------------------------------------------- |
| `rewards` | [cosmos.base.v1beta1.DecCoin](broken-reference) | repeated | rewards defines the rewards accrued by a delegation. |

### QueryDelegationTotalRewardsRequest

QueryDelegationTotalRewardsRequest is the request type for the Query/DelegationTotalRewards RPC method.

| Field               | Type                       | Label | Description                                                    |
| ------------------- | -------------------------- | ----- | -------------------------------------------------------------- |
| `delegator_address` | [string](broken-reference) |       | delegator\_address defines the delegator address to query for. |

### QueryDelegationTotalRewardsResponse

QueryDelegationTotalRewardsResponse is the response type for the Query/DelegationTotalRewards RPC method.

| Field     | Type                                            | Label    | Description                                             |
| --------- | ----------------------------------------------- | -------- | ------------------------------------------------------- |
| `rewards` | [DelegationDelegatorReward](broken-reference)   | repeated | rewards defines all the rewards accrued by a delegator. |
| `total`   | [cosmos.base.v1beta1.DecCoin](broken-reference) | repeated | total defines the sum of all the rewards.               |

### QueryDelegatorValidatorsRequest

QueryDelegatorValidatorsRequest is the request type for the Query/DelegatorValidators RPC method.

| Field               | Type                       | Label | Description                                                    |
| ------------------- | -------------------------- | ----- | -------------------------------------------------------------- |
| `delegator_address` | [string](broken-reference) |       | delegator\_address defines the delegator address to query for. |

### QueryDelegatorValidatorsResponse

QueryDelegatorValidatorsResponse is the response type for the Query/DelegatorValidators RPC method.

| Field        | Type                       | Label    | Description                                                      |
| ------------ | -------------------------- | -------- | ---------------------------------------------------------------- |
| `validators` | [string](broken-reference) | repeated | validators defines the validators a delegator is delegating for. |

### QueryDelegatorWithdrawAddressRequest

QueryDelegatorWithdrawAddressRequest is the request type for the Query/DelegatorWithdrawAddress RPC method.

| Field               | Type                       | Label | Description                                                    |
| ------------------- | -------------------------- | ----- | -------------------------------------------------------------- |
| `delegator_address` | [string](broken-reference) |       | delegator\_address defines the delegator address to query for. |

### QueryDelegatorWithdrawAddressResponse

QueryDelegatorWithdrawAddressResponse is the response type for the Query/DelegatorWithdrawAddress RPC method.

| Field              | Type                       | Label | Description                                                   |
| ------------------ | -------------------------- | ----- | ------------------------------------------------------------- |
| `withdraw_address` | [string](broken-reference) |       | withdraw\_address defines the delegator address to query for. |

### QueryParamsRequest

QueryParamsRequest is the request type for the Query/Params RPC method.

### QueryParamsResponse

QueryParamsResponse is the response type for the Query/Params RPC method.

| Field    | Type                       | Label | Description                                  |
| -------- | -------------------------- | ----- | -------------------------------------------- |
| `params` | [Params](broken-reference) |       | params defines the parameters of the module. |

### QueryValidatorCommissionRequest

QueryValidatorCommissionRequest is the request type for the Query/ValidatorCommission RPC method

| Field               | Type                       | Label | Description                                                    |
| ------------------- | -------------------------- | ----- | -------------------------------------------------------------- |
| `validator_address` | [string](broken-reference) |       | validator\_address defines the validator address to query for. |

### QueryValidatorCommissionResponse

QueryValidatorCommissionResponse is the response type for the Query/ValidatorCommission RPC method

| Field        | Type                                               | Label | Description                                              |
| ------------ | -------------------------------------------------- | ----- | -------------------------------------------------------- |
| `commission` | [ValidatorAccumulatedCommission](broken-reference) |       | commission defines the commision the validator received. |

### QueryValidatorOutstandingRewardsRequest

QueryValidatorOutstandingRewardsRequest is the request type for the Query/ValidatorOutstandingRewards RPC method.

| Field               | Type                       | Label | Description                                                    |
| ------------------- | -------------------------- | ----- | -------------------------------------------------------------- |
| `validator_address` | [string](broken-reference) |       | validator\_address defines the validator address to query for. |

### QueryValidatorOutstandingRewardsResponse

QueryValidatorOutstandingRewardsResponse is the response type for the Query/ValidatorOutstandingRewards RPC method.

| Field     | Type                                            | Label | Description |
| --------- | ----------------------------------------------- | ----- | ----------- |
| `rewards` | [ValidatorOutstandingRewards](broken-reference) |       |             |

### QueryValidatorSlashesRequest

QueryValidatorSlashesRequest is the request type for the Query/ValidatorSlashes RPC method

| Field               | Type                                                      | Label | Description                                                                 |
| ------------------- | --------------------------------------------------------- | ----- | --------------------------------------------------------------------------- |
| `validator_address` | [string](broken-reference)                                |       | validator\_address defines the validator address to query for.              |
| `starting_height`   | [uint64](broken-reference)                                |       | starting\_height defines the optional starting height to query the slashes. |
| `ending_height`     | [uint64](broken-reference)                                |       | starting\_height defines the optional ending height to query the slashes.   |
| `pagination`        | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request.                  |

### QueryValidatorSlashesResponse

QueryValidatorSlashesResponse is the response type for the Query/ValidatorSlashes RPC method.

| Field        | Type                                                       | Label    | Description                                         |
| ------------ | ---------------------------------------------------------- | -------- | --------------------------------------------------- |
| `slashes`    | [ValidatorSlashEvent](broken-reference)                    | repeated | slashes defines the slashes the validator received. |
| `pagination` | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response.  |

### Query

Query defines the gRPC querier service for distribution module.

| Method Name                   | Request Type                                                | Response Type                                                | Description                                                                   | HTTP Verb | Endpoint                                                                                  |
| ----------------------------- | ----------------------------------------------------------- | ------------------------------------------------------------ | ----------------------------------------------------------------------------- | --------- | ----------------------------------------------------------------------------------------- |
| `Params`                      | [QueryParamsRequest](broken-reference)                      | [QueryParamsResponse](broken-reference)                      | Params queries params of the distribution module.                             | GET       | /cosmos/distribution/v1beta1/params                                                       |
| `ValidatorOutstandingRewards` | [QueryValidatorOutstandingRewardsRequest](broken-reference) | [QueryValidatorOutstandingRewardsResponse](broken-reference) | ValidatorOutstandingRewards queries rewards of a validator address.           | GET       | /cosmos/distribution/v1beta1/validators/{validator\_address}/outstanding\_rewards         |
| `ValidatorCommission`         | [QueryValidatorCommissionRequest](broken-reference)         | [QueryValidatorCommissionResponse](broken-reference)         | ValidatorCommission queries accumulated commission for a validator.           | GET       | /cosmos/distribution/v1beta1/validators/{validator\_address}/commission                   |
| `ValidatorSlashes`            | [QueryValidatorSlashesRequest](broken-reference)            | [QueryValidatorSlashesResponse](broken-reference)            | ValidatorSlashes queries slash events of a validator.                         | GET       | /cosmos/distribution/v1beta1/validators/{validator\_address}/slashes                      |
| `DelegationRewards`           | [QueryDelegationRewardsRequest](broken-reference)           | [QueryDelegationRewardsResponse](broken-reference)           | DelegationRewards queries the total rewards accrued by a delegation.          | GET       | /cosmos/distribution/v1beta1/delegators/{delegator\_address}/rewards/{validator\_address} |
| `DelegationTotalRewards`      | [QueryDelegationTotalRewardsRequest](broken-reference)      | [QueryDelegationTotalRewardsResponse](broken-reference)      | DelegationTotalRewards queries the total rewards accrued by a each validator. | GET       | /cosmos/distribution/v1beta1/delegators/{delegator\_address}/rewards                      |
| `DelegatorValidators`         | [QueryDelegatorValidatorsRequest](broken-reference)         | [QueryDelegatorValidatorsResponse](broken-reference)         | DelegatorValidators queries the validators of a delegator.                    | GET       | /cosmos/distribution/v1beta1/delegators/{delegator\_address}/validators                   |
| `DelegatorWithdrawAddress`    | [QueryDelegatorWithdrawAddressRequest](broken-reference)    | [QueryDelegatorWithdrawAddressResponse](broken-reference)    | DelegatorWithdrawAddress queries withdraw address of a delegator.             | GET       | /cosmos/distribution/v1beta1/delegators/{delegator\_address}/withdraw\_address            |
| `CommunityPool`               | [QueryCommunityPoolRequest](broken-reference)               | [QueryCommunityPoolResponse](broken-reference)               | CommunityPool queries the community pool coins.                               | GET       | /cosmos/distribution/v1beta1/community\_pool                                              |

## cosmos/distribution/v1beta1/tx.proto

### MsgFundCommunityPool

MsgFundCommunityPool allows an account to directly fund the community pool.

| Field       | Type                                         | Label    | Description |
| ----------- | -------------------------------------------- | -------- | ----------- |
| `amount`    | [cosmos.base.v1beta1.Coin](broken-reference) | repeated |             |
| `depositor` | [string](broken-reference)                   |          |             |

### MsgFundCommunityPoolResponse

MsgFundCommunityPoolResponse defines the Msg/FundCommunityPool response type.

### MsgSetWithdrawAddress

MsgSetWithdrawAddress sets the withdraw address for a delegator (or validator self-delegation).

| Field               | Type                       | Label | Description |
| ------------------- | -------------------------- | ----- | ----------- |
| `delegator_address` | [string](broken-reference) |       |             |
| `withdraw_address`  | [string](broken-reference) |       |             |

### MsgSetWithdrawAddressResponse

MsgSetWithdrawAddressResponse defines the Msg/SetWithdrawAddress response type.

### MsgWithdrawDelegatorReward

MsgWithdrawDelegatorReward represents delegation withdrawal to a delegator from a single validator.

| Field               | Type                       | Label | Description |
| ------------------- | -------------------------- | ----- | ----------- |
| `delegator_address` | [string](broken-reference) |       |             |
| `validator_address` | [string](broken-reference) |       |             |

### MsgWithdrawDelegatorRewardResponse

MsgWithdrawDelegatorRewardResponse defines the Msg/WithdrawDelegatorReward response type.

### MsgWithdrawValidatorCommission

MsgWithdrawValidatorCommission withdraws the full commission to the validator address.

| Field               | Type                       | Label | Description |
| ------------------- | -------------------------- | ----- | ----------- |
| `validator_address` | [string](broken-reference) |       |             |

### MsgWithdrawValidatorCommissionResponse

MsgWithdrawValidatorCommissionResponse defines the Msg/WithdrawValidatorCommission response type.

### Msg

Msg defines the distribution Msg service.

| Method Name                   | Request Type                                       | Response Type                                              | Description                                                                                                        | HTTP Verb | Endpoint |
| ----------------------------- | -------------------------------------------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ | --------- | -------- |
| `SetWithdrawAddress`          | [MsgSetWithdrawAddress](broken-reference)          | [MsgSetWithdrawAddressResponse](broken-reference)          | SetWithdrawAddress defines a method to change the withdraw address for a delegator (or validator self-delegation). |           |          |
| `WithdrawDelegatorReward`     | [MsgWithdrawDelegatorReward](broken-reference)     | [MsgWithdrawDelegatorRewardResponse](broken-reference)     | WithdrawDelegatorReward defines a method to withdraw rewards of delegator from a single validator.                 |           |          |
| `WithdrawValidatorCommission` | [MsgWithdrawValidatorCommission](broken-reference) | [MsgWithdrawValidatorCommissionResponse](broken-reference) | WithdrawValidatorCommission defines a method to withdraw the full commission to the validator address.             |           |          |
| `FundCommunityPool`           | [MsgFundCommunityPool](broken-reference)           | [MsgFundCommunityPoolResponse](broken-reference)           | FundCommunityPool defines a method to allow an account to directly fund the community pool.                        |           |          |

## cosmos/evidence/v1beta1/evidence.proto

### Equivocation

Equivocation implements the Evidence interface and defines evidence of double signing misbehavior.

| Field               | Type                                          | Label | Description |
| ------------------- | --------------------------------------------- | ----- | ----------- |
| `height`            | [int64](broken-reference)                     |       |             |
| `time`              | [google.protobuf.Timestamp](broken-reference) |       |             |
| `power`             | [int64](broken-reference)                     |       |             |
| `consensus_address` | [string](broken-reference)                    |       |             |

## cosmos/evidence/v1beta1/genesis.proto

### GenesisState

GenesisState defines the evidence module's genesis state.

| Field      | Type                                    | Label    | Description                                   |
| ---------- | --------------------------------------- | -------- | --------------------------------------------- |
| `evidence` | [google.protobuf.Any](broken-reference) | repeated | evidence defines all the evidence at genesis. |

## cosmos/evidence/v1beta1/query.proto

### QueryAllEvidenceRequest

QueryEvidenceRequest is the request type for the Query/AllEvidence RPC method.

| Field        | Type                                                      | Label | Description                                                |
| ------------ | --------------------------------------------------------- | ----- | ---------------------------------------------------------- |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request. |

### QueryAllEvidenceResponse

QueryAllEvidenceResponse is the response type for the Query/AllEvidence RPC method.

| Field        | Type                                                       | Label    | Description                                        |
| ------------ | ---------------------------------------------------------- | -------- | -------------------------------------------------- |
| `evidence`   | [google.protobuf.Any](broken-reference)                    | repeated | evidence returns all evidences.                    |
| `pagination` | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response. |

### QueryEvidenceRequest

QueryEvidenceRequest is the request type for the Query/Evidence RPC method.

| Field           | Type                      | Label | Description                                                |
| --------------- | ------------------------- | ----- | ---------------------------------------------------------- |
| `evidence_hash` | [bytes](broken-reference) |       | evidence\_hash defines the hash of the requested evidence. |

### QueryEvidenceResponse

QueryEvidenceResponse is the response type for the Query/Evidence RPC method.

| Field      | Type                                    | Label | Description                              |
| ---------- | --------------------------------------- | ----- | ---------------------------------------- |
| `evidence` | [google.protobuf.Any](broken-reference) |       | evidence returns the requested evidence. |

### Query

Query defines the gRPC querier service.

| Method Name   | Request Type                                | Response Type                                | Description                                       | HTTP Verb | Endpoint                                           |
| ------------- | ------------------------------------------- | -------------------------------------------- | ------------------------------------------------- | --------- | -------------------------------------------------- |
| `Evidence`    | [QueryEvidenceRequest](broken-reference)    | [QueryEvidenceResponse](broken-reference)    | Evidence queries evidence based on evidence hash. | GET       | /cosmos/evidence/v1beta1/evidence/{evidence\_hash} |
| `AllEvidence` | [QueryAllEvidenceRequest](broken-reference) | [QueryAllEvidenceResponse](broken-reference) | AllEvidence queries all evidence.                 | GET       | /cosmos/evidence/v1beta1/evidence                  |

## cosmos/evidence/v1beta1/tx.proto

### MsgSubmitEvidence

MsgSubmitEvidence represents a message that supports submitting arbitrary Evidence of misbehavior such as equivocation or counterfactual signing.

| Field       | Type                                    | Label | Description |
| ----------- | --------------------------------------- | ----- | ----------- |
| `submitter` | [string](broken-reference)              |       |             |
| `evidence`  | [google.protobuf.Any](broken-reference) |       |             |

### MsgSubmitEvidenceResponse

MsgSubmitEvidenceResponse defines the Msg/SubmitEvidence response type.

| Field  | Type                      | Label | Description                            |
| ------ | ------------------------- | ----- | -------------------------------------- |
| `hash` | [bytes](broken-reference) |       | hash defines the hash of the evidence. |

### Msg

Msg defines the evidence Msg service.

| Method Name      | Request Type                          | Response Type                                 | Description                                                                                                 | HTTP Verb | Endpoint |
| ---------------- | ------------------------------------- | --------------------------------------------- | ----------------------------------------------------------------------------------------------------------- | --------- | -------- |
| `SubmitEvidence` | [MsgSubmitEvidence](broken-reference) | [MsgSubmitEvidenceResponse](broken-reference) | SubmitEvidence submits an arbitrary Evidence of misbehavior such as equivocation or counterfactual signing. |           |          |

## cosmos/genutil/v1beta1/genesis.proto

### GenesisState

GenesisState defines the raw genesis transaction in JSON.

| Field     | Type                      | Label    | Description                                |
| --------- | ------------------------- | -------- | ------------------------------------------ |
| `gen_txs` | [bytes](broken-reference) | repeated | gen\_txs defines the genesis transactions. |

## cosmos/gov/v1beta1/gov.proto

### Deposit

Deposit defines an amount deposited by an account address to an active proposal.

| Field         | Type                                         | Label    | Description |
| ------------- | -------------------------------------------- | -------- | ----------- |
| `proposal_id` | [uint64](broken-reference)                   |          |             |
| `depositor`   | [string](broken-reference)                   |          |             |
| `amount`      | [cosmos.base.v1beta1.Coin](broken-reference) | repeated |             |

### DepositParams

DepositParams defines the params for deposits on governance proposals.

| Field                | Type                                         | Label    | Description                                                                        |
| -------------------- | -------------------------------------------- | -------- | ---------------------------------------------------------------------------------- |
| `min_deposit`        | [cosmos.base.v1beta1.Coin](broken-reference) | repeated | Minimum deposit for a proposal to enter voting period.                             |
| `max_deposit_period` | [google.protobuf.Duration](broken-reference) |          | Maximum period for Atom holders to deposit on a proposal. Initial value: 2 months. |

### Proposal

Proposal defines the core field members of a governance proposal.

| Field                | Type                                          | Label    | Description |
| -------------------- | --------------------------------------------- | -------- | ----------- |
| `proposal_id`        | [uint64](broken-reference)                    |          |             |
| `content`            | [google.protobuf.Any](broken-reference)       |          |             |
| `status`             | [ProposalStatus](broken-reference)            |          |             |
| `final_tally_result` | [TallyResult](broken-reference)               |          |             |
| `submit_time`        | [google.protobuf.Timestamp](broken-reference) |          |             |
| `deposit_end_time`   | [google.protobuf.Timestamp](broken-reference) |          |             |
| `total_deposit`      | [cosmos.base.v1beta1.Coin](broken-reference)  | repeated |             |
| `voting_start_time`  | [google.protobuf.Timestamp](broken-reference) |          |             |
| `voting_end_time`    | [google.protobuf.Timestamp](broken-reference) |          |             |

### TallyParams

TallyParams defines the params for tallying votes on governance proposals.

| Field            | Type                      | Label | Description                                                                                     |
| ---------------- | ------------------------- | ----- | ----------------------------------------------------------------------------------------------- |
| `quorum`         | [bytes](broken-reference) |       | Minimum percentage of total stake needed to vote for a result to be considered valid.           |
| `threshold`      | [bytes](broken-reference) |       | Minimum proportion of Yes votes for proposal to pass. Default value: 0.5.                       |
| `veto_threshold` | [bytes](broken-reference) |       | Minimum value of Veto votes to Total votes ratio for proposal to be vetoed. Default value: 1/3. |

### TallyResult

TallyResult defines a standard tally for a governance proposal.

| Field          | Type                       | Label | Description |
| -------------- | -------------------------- | ----- | ----------- |
| `yes`          | [string](broken-reference) |       |             |
| `abstain`      | [string](broken-reference) |       |             |
| `no`           | [string](broken-reference) |       |             |
| `no_with_veto` | [string](broken-reference) |       |             |

### TextProposal

TextProposal defines a standard text proposal whose changes need to be manually updated in case of approval.

| Field         | Type                       | Label | Description |
| ------------- | -------------------------- | ----- | ----------- |
| `title`       | [string](broken-reference) |       |             |
| `description` | [string](broken-reference) |       |             |

### Vote

Vote defines a vote on a governance proposal. A Vote consists of a proposal ID, the voter, and the vote option.

| Field         | Type                           | Label | Description |
| ------------- | ------------------------------ | ----- | ----------- |
| `proposal_id` | [uint64](broken-reference)     |       |             |
| `voter`       | [string](broken-reference)     |       |             |
| `option`      | [VoteOption](broken-reference) |       |             |

### VotingParams

VotingParams defines the params for voting on governance proposals.

| Field           | Type                                         | Label | Description                  |
| --------------- | -------------------------------------------- | ----- | ---------------------------- |
| `voting_period` | [google.protobuf.Duration](broken-reference) |       | Length of the voting period. |

### ProposalStatus

ProposalStatus enumerates the valid statuses of a proposal.

| Name                              | Number | Description                                                                                |
| --------------------------------- | ------ | ------------------------------------------------------------------------------------------ |
| PROPOSAL\_STATUS\_UNSPECIFIED     | 0      | PROPOSAL\_STATUS\_UNSPECIFIED defines the default propopsal status.                        |
| PROPOSAL\_STATUS\_DEPOSIT\_PERIOD | 1      | PROPOSAL\_STATUS\_DEPOSIT\_PERIOD defines a proposal status during the deposit period.     |
| PROPOSAL\_STATUS\_VOTING\_PERIOD  | 2      | PROPOSAL\_STATUS\_VOTING\_PERIOD defines a proposal status during the voting period.       |
| PROPOSAL\_STATUS\_PASSED          | 3      | PROPOSAL\_STATUS\_PASSED defines a proposal status of a proposal that has passed.          |
| PROPOSAL\_STATUS\_REJECTED        | 4      | PROPOSAL\_STATUS\_REJECTED defines a proposal status of a proposal that has been rejected. |
| PROPOSAL\_STATUS\_FAILED          | 5      | PROPOSAL\_STATUS\_FAILED defines a proposal status of a proposal that has failed.          |

### VoteOption

VoteOption enumerates the valid vote options for a given governance proposal.

| Name                         | Number | Description                                                      |
| ---------------------------- | ------ | ---------------------------------------------------------------- |
| VOTE\_OPTION\_UNSPECIFIED    | 0      | VOTE\_OPTION\_UNSPECIFIED defines a no-op vote option.           |
| VOTE\_OPTION\_YES            | 1      | VOTE\_OPTION\_YES defines a yes vote option.                     |
| VOTE\_OPTION\_ABSTAIN        | 2      | VOTE\_OPTION\_ABSTAIN defines an abstain vote option.            |
| VOTE\_OPTION\_NO             | 3      | VOTE\_OPTION\_NO defines a no vote option.                       |
| VOTE\_OPTION\_NO\_WITH\_VETO | 4      | VOTE\_OPTION\_NO\_WITH\_VETO defines a no with veto vote option. |

## cosmos/gov/v1beta1/genesis.proto

### GenesisState

GenesisState defines the gov module's genesis state.

| Field                  | Type                              | Label    | Description                                                |
| ---------------------- | --------------------------------- | -------- | ---------------------------------------------------------- |
| `starting_proposal_id` | [uint64](broken-reference)        |          | starting\_proposal\_id is the ID of the starting proposal. |
| `deposits`             | [Deposit](broken-reference)       | repeated | deposits defines all the deposits present at genesis.      |
| `votes`                | [Vote](broken-reference)          | repeated | votes defines all the votes present at genesis.            |
| `proposals`            | [Proposal](broken-reference)      | repeated | proposals defines all the proposals present at genesis.    |
| `deposit_params`       | [DepositParams](broken-reference) |          | params defines all the paramaters of related to deposit.   |
| `voting_params`        | [VotingParams](broken-reference)  |          | params defines all the paramaters of related to voting.    |
| `tally_params`         | [TallyParams](broken-reference)   |          | params defines all the paramaters of related to tally.     |

## cosmos/gov/v1beta1/query.proto

### QueryDepositRequest

QueryDepositRequest is the request type for the Query/Deposit RPC method.

| Field         | Type                       | Label | Description                                                 |
| ------------- | -------------------------- | ----- | ----------------------------------------------------------- |
| `proposal_id` | [uint64](broken-reference) |       | proposal\_id defines the unique id of the proposal.         |
| `depositor`   | [string](broken-reference) |       | depositor defines the deposit addresses from the proposals. |

### QueryDepositResponse

QueryDepositResponse is the response type for the Query/Deposit RPC method.

| Field     | Type                        | Label | Description                            |
| --------- | --------------------------- | ----- | -------------------------------------- |
| `deposit` | [Deposit](broken-reference) |       | deposit defines the requested deposit. |

### QueryDepositsRequest

QueryDepositsRequest is the request type for the Query/Deposits RPC method.

| Field         | Type                                                      | Label | Description                                                |
| ------------- | --------------------------------------------------------- | ----- | ---------------------------------------------------------- |
| `proposal_id` | [uint64](broken-reference)                                |       | proposal\_id defines the unique id of the proposal.        |
| `pagination`  | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request. |

### QueryDepositsResponse

QueryDepositsResponse is the response type for the Query/Deposits RPC method.

| Field        | Type                                                       | Label    | Description                                        |
| ------------ | ---------------------------------------------------------- | -------- | -------------------------------------------------- |
| `deposits`   | [Deposit](broken-reference)                                | repeated |                                                    |
| `pagination` | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response. |

### QueryParamsRequest

QueryParamsRequest is the request type for the Query/Params RPC method.

| Field         | Type                       | Label | Description                                                                                          |
| ------------- | -------------------------- | ----- | ---------------------------------------------------------------------------------------------------- |
| `params_type` | [string](broken-reference) |       | params\_type defines which parameters to query for, can be one of "voting", "tallying" or "deposit". |

### QueryParamsResponse

QueryParamsResponse is the response type for the Query/Params RPC method.

| Field            | Type                              | Label | Description                                                |
| ---------------- | --------------------------------- | ----- | ---------------------------------------------------------- |
| `voting_params`  | [VotingParams](broken-reference)  |       | voting\_params defines the parameters related to voting.   |
| `deposit_params` | [DepositParams](broken-reference) |       | deposit\_params defines the parameters related to deposit. |
| `tally_params`   | [TallyParams](broken-reference)   |       | tally\_params defines the parameters related to tally.     |

### QueryProposalRequest

QueryProposalRequest is the request type for the Query/Proposal RPC method.

| Field         | Type                       | Label | Description                                         |
| ------------- | -------------------------- | ----- | --------------------------------------------------- |
| `proposal_id` | [uint64](broken-reference) |       | proposal\_id defines the unique id of the proposal. |

### QueryProposalResponse

QueryProposalResponse is the response type for the Query/Proposal RPC method.

| Field      | Type                         | Label | Description |
| ---------- | ---------------------------- | ----- | ----------- |
| `proposal` | [Proposal](broken-reference) |       |             |

### QueryProposalsRequest

QueryProposalsRequest is the request type for the Query/Proposals RPC method.

| Field             | Type                                                      | Label | Description                                                 |
| ----------------- | --------------------------------------------------------- | ----- | ----------------------------------------------------------- |
| `proposal_status` | [ProposalStatus](broken-reference)                        |       | proposal\_status defines the status of the proposals.       |
| `voter`           | [string](broken-reference)                                |       | voter defines the voter address for the proposals.          |
| `depositor`       | [string](broken-reference)                                |       | depositor defines the deposit addresses from the proposals. |
| `pagination`      | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request.  |

### QueryProposalsResponse

QueryProposalsResponse is the response type for the Query/Proposals RPC method.

| Field        | Type                                                       | Label    | Description                                        |
| ------------ | ---------------------------------------------------------- | -------- | -------------------------------------------------- |
| `proposals`  | [Proposal](broken-reference)                               | repeated |                                                    |
| `pagination` | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response. |

### QueryTallyResultRequest

QueryTallyResultRequest is the request type for the Query/Tally RPC method.

| Field         | Type                       | Label | Description                                         |
| ------------- | -------------------------- | ----- | --------------------------------------------------- |
| `proposal_id` | [uint64](broken-reference) |       | proposal\_id defines the unique id of the proposal. |

### QueryTallyResultResponse

QueryTallyResultResponse is the response type for the Query/Tally RPC method.

| Field   | Type                            | Label | Description                        |
| ------- | ------------------------------- | ----- | ---------------------------------- |
| `tally` | [TallyResult](broken-reference) |       | tally defines the requested tally. |

### QueryVoteRequest

QueryVoteRequest is the request type for the Query/Vote RPC method.

| Field         | Type                       | Label | Description                                         |
| ------------- | -------------------------- | ----- | --------------------------------------------------- |
| `proposal_id` | [uint64](broken-reference) |       | proposal\_id defines the unique id of the proposal. |
| `voter`       | [string](broken-reference) |       | voter defines the oter address for the proposals.   |

### QueryVoteResponse

QueryVoteResponse is the response type for the Query/Vote RPC method.

| Field  | Type                     | Label | Description                    |
| ------ | ------------------------ | ----- | ------------------------------ |
| `vote` | [Vote](broken-reference) |       | vote defined the queried vote. |

### QueryVotesRequest

QueryVotesRequest is the request type for the Query/Votes RPC method.

| Field         | Type                                                      | Label | Description                                                |
| ------------- | --------------------------------------------------------- | ----- | ---------------------------------------------------------- |
| `proposal_id` | [uint64](broken-reference)                                |       | proposal\_id defines the unique id of the proposal.        |
| `pagination`  | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request. |

### QueryVotesResponse

QueryVotesResponse is the response type for the Query/Votes RPC method.

| Field        | Type                                                       | Label    | Description                                        |
| ------------ | ---------------------------------------------------------- | -------- | -------------------------------------------------- |
| `votes`      | [Vote](broken-reference)                                   | repeated | votes defined the queried votes.                   |
| `pagination` | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response. |

### Query

Query defines the gRPC querier service for gov module

| Method Name   | Request Type                                | Response Type                                | Description                                                               | HTTP Verb | Endpoint                                                          |
| ------------- | ------------------------------------------- | -------------------------------------------- | ------------------------------------------------------------------------- | --------- | ----------------------------------------------------------------- |
| `Proposal`    | [QueryProposalRequest](broken-reference)    | [QueryProposalResponse](broken-reference)    | Proposal queries proposal details based on ProposalID.                    | GET       | /cosmos/gov/v1beta1/proposals/{proposal\_id}                      |
| `Proposals`   | [QueryProposalsRequest](broken-reference)   | [QueryProposalsResponse](broken-reference)   | Proposals queries all proposals based on given status.                    | GET       | /cosmos/gov/v1beta1/proposals                                     |
| `Vote`        | [QueryVoteRequest](broken-reference)        | [QueryVoteResponse](broken-reference)        | Vote queries voted information based on proposalID, voterAddr.            | GET       | /cosmos/gov/v1beta1/proposals/{proposal\_id}/votes/{voter}        |
| `Votes`       | [QueryVotesRequest](broken-reference)       | [QueryVotesResponse](broken-reference)       | Votes queries votes of a given proposal.                                  | GET       | /cosmos/gov/v1beta1/proposals/{proposal\_id}/votes                |
| `Params`      | [QueryParamsRequest](broken-reference)      | [QueryParamsResponse](broken-reference)      | Params queries all parameters of the gov module.                          | GET       | /cosmos/gov/v1beta1/params/{params\_type}                         |
| `Deposit`     | [QueryDepositRequest](broken-reference)     | [QueryDepositResponse](broken-reference)     | Deposit queries single deposit information based proposalID, depositAddr. | GET       | /cosmos/gov/v1beta1/proposals/{proposal\_id}/deposits/{depositor} |
| `Deposits`    | [QueryDepositsRequest](broken-reference)    | [QueryDepositsResponse](broken-reference)    | Deposits queries all deposits of a single proposal.                       | GET       | /cosmos/gov/v1beta1/proposals/{proposal\_id}/deposits             |
| `TallyResult` | [QueryTallyResultRequest](broken-reference) | [QueryTallyResultResponse](broken-reference) | TallyResult queries the tally of a proposal vote.                         | GET       | /cosmos/gov/v1beta1/proposals/{proposal\_id}/tally                |

## cosmos/gov/v1beta1/tx.proto

### MsgDeposit

MsgDeposit defines a message to submit a deposit to an existing proposal.

| Field         | Type                                         | Label    | Description |
| ------------- | -------------------------------------------- | -------- | ----------- |
| `proposal_id` | [uint64](broken-reference)                   |          |             |
| `depositor`   | [string](broken-reference)                   |          |             |
| `amount`      | [cosmos.base.v1beta1.Coin](broken-reference) | repeated |             |

### MsgDepositResponse

MsgDepositResponse defines the Msg/Deposit response type.

### MsgSubmitProposal

MsgSubmitProposal defines an sdk.Msg type that supports submitting arbitrary proposal Content.

| Field             | Type                                         | Label    | Description |
| ----------------- | -------------------------------------------- | -------- | ----------- |
| `content`         | [google.protobuf.Any](broken-reference)      |          |             |
| `initial_deposit` | [cosmos.base.v1beta1.Coin](broken-reference) | repeated |             |
| `proposer`        | [string](broken-reference)                   |          |             |

### MsgSubmitProposalResponse

MsgSubmitProposalResponse defines the Msg/SubmitProposal response type.

| Field         | Type                       | Label | Description |
| ------------- | -------------------------- | ----- | ----------- |
| `proposal_id` | [uint64](broken-reference) |       |             |

### MsgVote

MsgVote defines a message to cast a vote.

| Field         | Type                           | Label | Description |
| ------------- | ------------------------------ | ----- | ----------- |
| `proposal_id` | [uint64](broken-reference)     |       |             |
| `voter`       | [string](broken-reference)     |       |             |
| `option`      | [VoteOption](broken-reference) |       |             |

### MsgVoteResponse

MsgVoteResponse defines the Msg/Vote response type.

### Msg

Msg defines the bank Msg service.

| Method Name      | Request Type                          | Response Type                                 | Description                                                             | HTTP Verb | Endpoint |
| ---------------- | ------------------------------------- | --------------------------------------------- | ----------------------------------------------------------------------- | --------- | -------- |
| `SubmitProposal` | [MsgSubmitProposal](broken-reference) | [MsgSubmitProposalResponse](broken-reference) | SubmitProposal defines a method to create new proposal given a content. |           |          |
| `Vote`           | [MsgVote](broken-reference)           | [MsgVoteResponse](broken-reference)           | Vote defines a method to add a vote on a specific proposal.             |           |          |
| `Deposit`        | [MsgDeposit](broken-reference)        | [MsgDepositResponse](broken-reference)        | Deposit defines a method to add deposit on a specific proposal.         |           |          |

## cosmos/params/v1beta1/params.proto

### ParamChange

ParamChange defines an individual parameter change, for use in ParameterChangeProposal.

| Field      | Type                       | Label | Description |
| ---------- | -------------------------- | ----- | ----------- |
| `subspace` | [string](broken-reference) |       |             |
| `key`      | [string](broken-reference) |       |             |
| `value`    | [string](broken-reference) |       |             |

### ParameterChangeProposal

ParameterChangeProposal defines a proposal to change one or more parameters.

| Field         | Type                            | Label    | Description |
| ------------- | ------------------------------- | -------- | ----------- |
| `title`       | [string](broken-reference)      |          |             |
| `description` | [string](broken-reference)      |          |             |
| `changes`     | [ParamChange](broken-reference) | repeated |             |

## cosmos/params/v1beta1/query.proto

### QueryParamsRequest

QueryParamsRequest is request type for the Query/Params RPC method.

| Field      | Type                       | Label | Description                                             |
| ---------- | -------------------------- | ----- | ------------------------------------------------------- |
| `subspace` | [string](broken-reference) |       | subspace defines the module to query the parameter for. |
| `key`      | [string](broken-reference) |       | key defines the key of the parameter in the subspace.   |

### QueryParamsResponse

QueryParamsResponse is response type for the Query/Params RPC method.

| Field   | Type                            | Label | Description                          |
| ------- | ------------------------------- | ----- | ------------------------------------ |
| `param` | [ParamChange](broken-reference) |       | param defines the queried parameter. |

### Query

Query defines the gRPC querier service.

| Method Name | Request Type                           | Response Type                           | Description                                                                  | HTTP Verb | Endpoint                      |
| ----------- | -------------------------------------- | --------------------------------------- | ---------------------------------------------------------------------------- | --------- | ----------------------------- |
| `Params`    | [QueryParamsRequest](broken-reference) | [QueryParamsResponse](broken-reference) | Params queries a specific parameter of a module, given its subspace and key. | GET       | /cosmos/params/v1beta1/params |

## cosmos/slashing/v1beta1/slashing.proto

### Params

Params represents the parameters used for by the slashing module.

| Field                        | Type                                         | Label | Description |
| ---------------------------- | -------------------------------------------- | ----- | ----------- |
| `signed_blocks_window`       | [int64](broken-reference)                    |       |             |
| `min_signed_per_window`      | [bytes](broken-reference)                    |       |             |
| `downtime_jail_duration`     | [google.protobuf.Duration](broken-reference) |       |             |
| `slash_fraction_double_sign` | [bytes](broken-reference)                    |       |             |
| `slash_fraction_downtime`    | [bytes](broken-reference)                    |       |             |

### ValidatorSigningInfo

ValidatorSigningInfo defines a validator's signing info for monitoring their liveness activity.

| Field                   | Type                                          | Label | Description                                                                  |
| ----------------------- | --------------------------------------------- | ----- | ---------------------------------------------------------------------------- |
| `address`               | [string](broken-reference)                    |       |                                                                              |
| `start_height`          | [int64](broken-reference)                     |       | height at which validator was first a candidate OR was unjailed              |
| `index_offset`          | [int64](broken-reference)                     |       | index offset into signed block bit array                                     |
| `jailed_until`          | [google.protobuf.Timestamp](broken-reference) |       | timestamp validator cannot be unjailed until                                 |
| `tombstoned`            | [bool](broken-reference)                      |       | whether or not a validator has been tombstoned (killed out of validator set) |
| `missed_blocks_counter` | [int64](broken-reference)                     |       | missed blocks counter (to avoid scanning the array every time)               |

## cosmos/slashing/v1beta1/genesis.proto

### GenesisState

GenesisState defines the slashing module's genesis state.

| Field           | Type                                      | Label    | Description                                                                          |
| --------------- | ----------------------------------------- | -------- | ------------------------------------------------------------------------------------ |
| `params`        | [Params](broken-reference)                |          | params defines all the paramaters of related to deposit.                             |
| `signing_infos` | [SigningInfo](broken-reference)           | repeated | signing\_infos represents a map between validator addresses and their signing infos. |
| `missed_blocks` | [ValidatorMissedBlocks](broken-reference) | repeated | signing\_infos represents a map between validator addresses and their missed blocks. |

### MissedBlock

MissedBlock contains height and missed status as boolean.

| Field    | Type                      | Label | Description                                        |
| -------- | ------------------------- | ----- | -------------------------------------------------- |
| `index`  | [int64](broken-reference) |       | index is the height at which the block was missed. |
| `missed` | [bool](broken-reference)  |       | missed is the missed status.                       |

### SigningInfo

SigningInfo stores validator signing info of corresponding address.

| Field                    | Type                                     | Label | Description                                                             |
| ------------------------ | ---------------------------------------- | ----- | ----------------------------------------------------------------------- |
| `address`                | [string](broken-reference)               |       | address is the validator address.                                       |
| `validator_signing_info` | [ValidatorSigningInfo](broken-reference) |       | validator\_signing\_info represents the signing info of this validator. |

### ValidatorMissedBlocks

ValidatorMissedBlocks contains array of missed blocks of corresponding address.

| Field           | Type                            | Label    | Description                                                   |
| --------------- | ------------------------------- | -------- | ------------------------------------------------------------- |
| `address`       | [string](broken-reference)      |          | address is the validator address.                             |
| `missed_blocks` | [MissedBlock](broken-reference) | repeated | missed\_blocks is an array of missed blocks by the validator. |

## cosmos/slashing/v1beta1/query.proto

### QueryParamsRequest

QueryParamsRequest is the request type for the Query/Params RPC method

### QueryParamsResponse

QueryParamsResponse is the response type for the Query/Params RPC method

| Field    | Type                       | Label | Description |
| -------- | -------------------------- | ----- | ----------- |
| `params` | [Params](broken-reference) |       |             |

### QuerySigningInfoRequest

QuerySigningInfoRequest is the request type for the Query/SigningInfo RPC method

| Field          | Type                       | Label | Description                                           |
| -------------- | -------------------------- | ----- | ----------------------------------------------------- |
| `cons_address` | [string](broken-reference) |       | cons\_address is the address to query signing info of |

### QuerySigningInfoResponse

QuerySigningInfoResponse is the response type for the Query/SigningInfo RPC method

| Field              | Type                                     | Label | Description                                                          |
| ------------------ | ---------------------------------------- | ----- | -------------------------------------------------------------------- |
| `val_signing_info` | [ValidatorSigningInfo](broken-reference) |       | val\_signing\_info is the signing info of requested val cons address |

### QuerySigningInfosRequest

QuerySigningInfosRequest is the request type for the Query/SigningInfos RPC method

| Field        | Type                                                      | Label | Description |
| ------------ | --------------------------------------------------------- | ----- | ----------- |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       |             |

### QuerySigningInfosResponse

QuerySigningInfosResponse is the response type for the Query/SigningInfos RPC method

| Field        | Type                                                       | Label    | Description                                |
| ------------ | ---------------------------------------------------------- | -------- | ------------------------------------------ |
| `info`       | [ValidatorSigningInfo](broken-reference)                   | repeated | info is the signing info of all validators |
| `pagination` | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          |                                            |

### Query

Query provides defines the gRPC querier service

| Method Name    | Request Type                                 | Response Type                                 | Description                                                | HTTP Verb | Endpoint                                                |
| -------------- | -------------------------------------------- | --------------------------------------------- | ---------------------------------------------------------- | --------- | ------------------------------------------------------- |
| `Params`       | [QueryParamsRequest](broken-reference)       | [QueryParamsResponse](broken-reference)       | Params queries the parameters of slashing module           | GET       | /cosmos/slashing/v1beta1/params                         |
| `SigningInfo`  | [QuerySigningInfoRequest](broken-reference)  | [QuerySigningInfoResponse](broken-reference)  | SigningInfo queries the signing info of given cons address | GET       | /cosmos/slashing/v1beta1/signing\_infos/{cons\_address} |
| `SigningInfos` | [QuerySigningInfosRequest](broken-reference) | [QuerySigningInfosResponse](broken-reference) | SigningInfos queries signing info of all validators        | GET       | /cosmos/slashing/v1beta1/signing\_infos                 |

## cosmos/slashing/v1beta1/tx.proto

### MsgUnjail

MsgUnjail defines the Msg/Unjail request type

| Field            | Type                       | Label | Description |
| ---------------- | -------------------------- | ----- | ----------- |
| `validator_addr` | [string](broken-reference) |       |             |

### MsgUnjailResponse

MsgUnjailResponse defines the Msg/Unjail response type

### Msg

Msg defines the slashing Msg service.

| Method Name | Request Type                  | Response Type                         | Description                                                                                                                                                            | HTTP Verb | Endpoint |
| ----------- | ----------------------------- | ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | -------- |
| `Unjail`    | [MsgUnjail](broken-reference) | [MsgUnjailResponse](broken-reference) | Unjail defines a method for unjailing a jailed validator, thus returning them into the bonded validator set, so they can begin receiving provisions and rewards again. |           |          |

## cosmos/staking/v1beta1/staking.proto

### Commission

Commission defines commission parameters for a given validator.

| Field              | Type                                          | Label | Description                                                                                 |
| ------------------ | --------------------------------------------- | ----- | ------------------------------------------------------------------------------------------- |
| `commission_rates` | [CommissionRates](broken-reference)           |       | commission\_rates defines the initial commission rates to be used for creating a validator. |
| `update_time`      | [google.protobuf.Timestamp](broken-reference) |       | update\_time is the last time the commission rate was changed.                              |

### CommissionRates

CommissionRates defines the initial commission rates to be used for creating a validator.

| Field             | Type                       | Label | Description                                                                                      |
| ----------------- | -------------------------- | ----- | ------------------------------------------------------------------------------------------------ |
| `rate`            | [string](broken-reference) |       | rate is the commission rate charged to delegators, as a fraction.                                |
| `max_rate`        | [string](broken-reference) |       | max\_rate defines the maximum commission rate which validator can ever charge, as a fraction.    |
| `max_change_rate` | [string](broken-reference) |       | max\_change\_rate defines the maximum daily increase of the validator commission, as a fraction. |

### DVPair

DVPair is struct that just has a delegator-validator pair with no other data. It is intended to be used as a marshalable pointer. For example, a DVPair can be used to construct the key to getting an UnbondingDelegation from state.

| Field               | Type                       | Label | Description |
| ------------------- | -------------------------- | ----- | ----------- |
| `delegator_address` | [string](broken-reference) |       |             |
| `validator_address` | [string](broken-reference) |       |             |

### DVPairs

DVPairs defines an array of DVPair objects.

| Field   | Type                       | Label    | Description |
| ------- | -------------------------- | -------- | ----------- |
| `pairs` | [DVPair](broken-reference) | repeated |             |

### DVVTriplet

DVVTriplet is struct that just has a delegator-validator-validator triplet with no other data. It is intended to be used as a marshalable pointer. For example, a DVVTriplet can be used to construct the key to getting a Redelegation from state.

| Field                   | Type                       | Label | Description |
| ----------------------- | -------------------------- | ----- | ----------- |
| `delegator_address`     | [string](broken-reference) |       |             |
| `validator_src_address` | [string](broken-reference) |       |             |
| `validator_dst_address` | [string](broken-reference) |       |             |

### DVVTriplets

DVVTriplets defines an array of DVVTriplet objects.

| Field      | Type                           | Label    | Description |
| ---------- | ------------------------------ | -------- | ----------- |
| `triplets` | [DVVTriplet](broken-reference) | repeated |             |

### Delegation

Delegation represents the bond with tokens held by an account. It is owned by one delegator, and is associated with the voting power of one validator.

| Field               | Type                       | Label | Description                                                        |
| ------------------- | -------------------------- | ----- | ------------------------------------------------------------------ |
| `delegator_address` | [string](broken-reference) |       | delegator\_address is the bech32-encoded address of the delegator. |
| `validator_address` | [string](broken-reference) |       | validator\_address is the bech32-encoded address of the validator. |
| `shares`            | [string](broken-reference) |       | shares define the delegation shares received.                      |

### DelegationResponse

DelegationResponse is equivalent to Delegation except that it contains a balance in addition to shares which is more suitable for client responses.

| Field        | Type                                         | Label | Description |
| ------------ | -------------------------------------------- | ----- | ----------- |
| `delegation` | [Delegation](broken-reference)               |       |             |
| `balance`    | [cosmos.base.v1beta1.Coin](broken-reference) |       |             |

### Description

Description defines a validator description.

| Field              | Type                       | Label | Description                                                             |
| ------------------ | -------------------------- | ----- | ----------------------------------------------------------------------- |
| `moniker`          | [string](broken-reference) |       | moniker defines a human-readable name for the validator.                |
| `identity`         | [string](broken-reference) |       | identity defines an optional identity signature (ex. UPort or Keybase). |
| `website`          | [string](broken-reference) |       | website defines an optional website link.                               |
| `security_contact` | [string](broken-reference) |       | security\_contact defines an optional email for security contact.       |
| `details`          | [string](broken-reference) |       | details define other optional details.                                  |

### HistoricalInfo

HistoricalInfo contains header and validator information for a given block. It is stored as part of staking module's state, which persists the `n` most recent HistoricalInfo (`n` is set by the staking module's `historical_entries` parameter).

| Field    | Type                                        | Label    | Description |
| -------- | ------------------------------------------- | -------- | ----------- |
| `header` | [tendermint.types.Header](broken-reference) |          |             |
| `valset` | [Validator](broken-reference)               | repeated |             |

### Params

Params defines the parameters for the staking module.

| Field                | Type                                         | Label | Description                                                                                      |
| -------------------- | -------------------------------------------- | ----- | ------------------------------------------------------------------------------------------------ |
| `unbonding_time`     | [google.protobuf.Duration](broken-reference) |       | unbonding\_time is the time duration of unbonding.                                               |
| `max_validators`     | [uint32](broken-reference)                   |       | max\_validators is the maximum number of validators.                                             |
| `max_entries`        | [uint32](broken-reference)                   |       | max\_entries is the max entries for either unbonding delegation or redelegation (per pair/trio). |
| `historical_entries` | [uint32](broken-reference)                   |       | historical\_entries is the number of historical entries to persist.                              |
| `bond_denom`         | [string](broken-reference)                   |       | bond\_denom defines the bondable coin denomination.                                              |

### Pool

Pool is used for tracking bonded and not-bonded token supply of the bond denomination.

| Field               | Type                       | Label | Description |
| ------------------- | -------------------------- | ----- | ----------- |
| `not_bonded_tokens` | [string](broken-reference) |       |             |
| `bonded_tokens`     | [string](broken-reference) |       |             |

### Redelegation

Redelegation contains the list of a particular delegator's redelegating bonds from a particular source validator to a particular destination validator.

| Field                   | Type                                  | Label    | Description                                                                         |
| ----------------------- | ------------------------------------- | -------- | ----------------------------------------------------------------------------------- |
| `delegator_address`     | [string](broken-reference)            |          | delegator\_address is the bech32-encoded address of the delegator.                  |
| `validator_src_address` | [string](broken-reference)            |          | validator\_src\_address is the validator redelegation source operator address.      |
| `validator_dst_address` | [string](broken-reference)            |          | validator\_dst\_address is the validator redelegation destination operator address. |
| `entries`               | [RedelegationEntry](broken-reference) | repeated | entries are the redelegation entries.                                               |

redelegation entries |

### RedelegationEntry

RedelegationEntry defines a redelegation object with relevant metadata.

| Field             | Type                                          | Label | Description                                                                        |
| ----------------- | --------------------------------------------- | ----- | ---------------------------------------------------------------------------------- |
| `creation_height` | [int64](broken-reference)                     |       | creation\_height defines the height which the redelegation took place.             |
| `completion_time` | [google.protobuf.Timestamp](broken-reference) |       | completion\_time defines the unix time for redelegation completion.                |
| `initial_balance` | [string](broken-reference)                    |       | initial\_balance defines the initial balance when redelegation started.            |
| `shares_dst`      | [string](broken-reference)                    |       | shares\_dst is the amount of destination-validator shares created by redelegation. |

### RedelegationEntryResponse

RedelegationEntryResponse is equivalent to a RedelegationEntry except that it contains a balance in addition to shares which is more suitable for client responses.

| Field                | Type                                  | Label | Description |
| -------------------- | ------------------------------------- | ----- | ----------- |
| `redelegation_entry` | [RedelegationEntry](broken-reference) |       |             |
| `balance`            | [string](broken-reference)            |       |             |

### RedelegationResponse

RedelegationResponse is equivalent to a Redelegation except that its entries contain a balance in addition to shares which is more suitable for client responses.

| Field          | Type                                          | Label    | Description |
| -------------- | --------------------------------------------- | -------- | ----------- |
| `redelegation` | [Redelegation](broken-reference)              |          |             |
| `entries`      | [RedelegationEntryResponse](broken-reference) | repeated |             |

### UnbondingDelegation

UnbondingDelegation stores all of a single delegator's unbonding bonds for a single validator in an time-ordered list.

| Field               | Type                                         | Label    | Description                                                        |
| ------------------- | -------------------------------------------- | -------- | ------------------------------------------------------------------ |
| `delegator_address` | [string](broken-reference)                   |          | delegator\_address is the bech32-encoded address of the delegator. |
| `validator_address` | [string](broken-reference)                   |          | validator\_address is the bech32-encoded address of the validator. |
| `entries`           | [UnbondingDelegationEntry](broken-reference) | repeated | entries are the unbonding delegation entries.                      |

unbonding delegation entries |

### UnbondingDelegationEntry

UnbondingDelegationEntry defines an unbonding object with relevant metadata.

| Field             | Type                                          | Label | Description                                                                       |
| ----------------- | --------------------------------------------- | ----- | --------------------------------------------------------------------------------- |
| `creation_height` | [int64](broken-reference)                     |       | creation\_height is the height which the unbonding took place.                    |
| `completion_time` | [google.protobuf.Timestamp](broken-reference) |       | completion\_time is the unix time for unbonding completion.                       |
| `initial_balance` | [string](broken-reference)                    |       | initial\_balance defines the tokens initially scheduled to receive at completion. |
| `balance`         | [string](broken-reference)                    |       | balance defines the tokens to receive at completion.                              |

### ValAddresses

ValAddresses defines a repeated set of validator addresses.

| Field       | Type                       | Label    | Description |
| ----------- | -------------------------- | -------- | ----------- |
| `addresses` | [string](broken-reference) | repeated |             |

### Validator

Validator defines a validator, together with the total amount of the Validator's bond shares and their exchange rate to coins. Slashing results in a decrease in the exchange rate, allowing correct calculation of future undelegations without iterating over delegators. When coins are delegated to this validator, the validator is credited with a delegation whose number of bond shares is based on the amount of coins delegated divided by the current exchange rate. Voting power can be calculated as total bonded shares multiplied by exchange rate.

| Field                 | Type                                          | Label | Description                                                                                      |
| --------------------- | --------------------------------------------- | ----- | ------------------------------------------------------------------------------------------------ |
| `operator_address`    | [string](broken-reference)                    |       | operator\_address defines the address of the validator's operator; bech encoded in JSON.         |
| `consensus_pubkey`    | [google.protobuf.Any](broken-reference)       |       | consensus\_pubkey is the consensus public key of the validator, as a Protobuf Any.               |
| `jailed`              | [bool](broken-reference)                      |       | jailed defined whether the validator has been jailed from bonded status or not.                  |
| `status`              | [BondStatus](broken-reference)                |       | status is the validator status (bonded/unbonding/unbonded).                                      |
| `tokens`              | [string](broken-reference)                    |       | tokens define the delegated tokens (incl. self-delegation).                                      |
| `delegator_shares`    | [string](broken-reference)                    |       | delegator\_shares defines total shares issued to a validator's delegators.                       |
| `description`         | [Description](broken-reference)               |       | description defines the description terms for the validator.                                     |
| `unbonding_height`    | [int64](broken-reference)                     |       | unbonding\_height defines, if unbonding, the height at which this validator has begun unbonding. |
| `unbonding_time`      | [google.protobuf.Timestamp](broken-reference) |       | unbonding\_time defines, if unbonding, the min time for the validator to complete unbonding.     |
| `commission`          | [Commission](broken-reference)                |       | commission defines the commission parameters.                                                    |
| `min_self_delegation` | [string](broken-reference)                    |       | min\_self\_delegation is the validator's self declared minimum self delegation.                  |

### BondStatus

BondStatus is the status of a validator.

| Name                      | Number | Description                                      |
| ------------------------- | ------ | ------------------------------------------------ |
| BOND\_STATUS\_UNSPECIFIED | 0      | UNSPECIFIED defines an invalid validator status. |
| BOND\_STATUS\_UNBONDED    | 1      | UNBONDED defines a validator that is not bonded. |
| BOND\_STATUS\_UNBONDING   | 2      | UNBONDING defines a validator that is unbonding. |
| BOND\_STATUS\_BONDED      | 3      | BONDED defines a validator that is bonded.       |

## cosmos/staking/v1beta1/genesis.proto

### GenesisState

GenesisState defines the staking module's genesis state.

| Field                   | Type                                    | Label    | Description                                                                                                       |
| ----------------------- | --------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------- |
| `params`                | [Params](broken-reference)              |          | params defines all the paramaters of related to deposit.                                                          |
| `last_total_power`      | [bytes](broken-reference)               |          | last\_total\_power tracks the total amounts of bonded tokens recorded during the previous end block.              |
| `last_validator_powers` | [LastValidatorPower](broken-reference)  | repeated | last\_validator\_powers is a special index that provides a historical list of the last-block's bonded validators. |
| `validators`            | [Validator](broken-reference)           | repeated | delegations defines the validator set at genesis.                                                                 |
| `delegations`           | [Delegation](broken-reference)          | repeated | delegations defines the delegations active at genesis.                                                            |
| `unbonding_delegations` | [UnbondingDelegation](broken-reference) | repeated | unbonding\_delegations defines the unbonding delegations active at genesis.                                       |
| `redelegations`         | [Redelegation](broken-reference)        | repeated | redelegations defines the redelegations active at genesis.                                                        |
| `exported`              | [bool](broken-reference)                |          |                                                                                                                   |

### LastValidatorPower

LastValidatorPower required for validator set update logic.

| Field     | Type                       | Label | Description                               |
| --------- | -------------------------- | ----- | ----------------------------------------- |
| `address` | [string](broken-reference) |       | address is the address of the validator.  |
| `power`   | [int64](broken-reference)  |       | power defines the power of the validator. |

## cosmos/staking/v1beta1/query.proto

### QueryDelegationRequest

QueryDelegationRequest is request type for the Query/Delegation RPC method.

| Field            | Type                       | Label | Description                                                 |
| ---------------- | -------------------------- | ----- | ----------------------------------------------------------- |
| `delegator_addr` | [string](broken-reference) |       | delegator\_addr defines the delegator address to query for. |
| `validator_addr` | [string](broken-reference) |       | validator\_addr defines the validator address to query for. |

### QueryDelegationResponse

QueryDelegationResponse is response type for the Query/Delegation RPC method.

| Field                 | Type                                   | Label | Description                                                        |
| --------------------- | -------------------------------------- | ----- | ------------------------------------------------------------------ |
| `delegation_response` | [DelegationResponse](broken-reference) |       | delegation\_responses defines the delegation info of a delegation. |

### QueryDelegatorDelegationsRequest

QueryDelegatorDelegationsRequest is request type for the Query/DelegatorDelegations RPC method.

| Field            | Type                                                      | Label | Description                                                 |
| ---------------- | --------------------------------------------------------- | ----- | ----------------------------------------------------------- |
| `delegator_addr` | [string](broken-reference)                                |       | delegator\_addr defines the delegator address to query for. |
| `pagination`     | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request.  |

### QueryDelegatorDelegationsResponse

QueryDelegatorDelegationsResponse is response type for the Query/DelegatorDelegations RPC method.

| Field                  | Type                                                       | Label    | Description                                                             |
| ---------------------- | ---------------------------------------------------------- | -------- | ----------------------------------------------------------------------- |
| `delegation_responses` | [DelegationResponse](broken-reference)                     | repeated | delegation\_responses defines all the delegations' info of a delegator. |
| `pagination`           | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response.                      |

### QueryDelegatorUnbondingDelegationsRequest

QueryDelegatorUnbondingDelegationsRequest is request type for the Query/DelegatorUnbondingDelegations RPC method.

| Field            | Type                                                      | Label | Description                                                 |
| ---------------- | --------------------------------------------------------- | ----- | ----------------------------------------------------------- |
| `delegator_addr` | [string](broken-reference)                                |       | delegator\_addr defines the delegator address to query for. |
| `pagination`     | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request.  |

### QueryDelegatorUnbondingDelegationsResponse

QueryUnbondingDelegatorDelegationsResponse is response type for the Query/UnbondingDelegatorDelegations RPC method.

| Field                 | Type                                                       | Label    | Description                                        |
| --------------------- | ---------------------------------------------------------- | -------- | -------------------------------------------------- |
| `unbonding_responses` | [UnbondingDelegation](broken-reference)                    | repeated |                                                    |
| `pagination`          | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response. |

### QueryDelegatorValidatorRequest

QueryDelegatorValidatorRequest is request type for the Query/DelegatorValidator RPC method.

| Field            | Type                       | Label | Description                                                 |
| ---------------- | -------------------------- | ----- | ----------------------------------------------------------- |
| `delegator_addr` | [string](broken-reference) |       | delegator\_addr defines the delegator address to query for. |
| `validator_addr` | [string](broken-reference) |       | validator\_addr defines the validator address to query for. |

### QueryDelegatorValidatorResponse

QueryDelegatorValidatorResponse response type for the Query/DelegatorValidator RPC method.

| Field       | Type                          | Label | Description                               |
| ----------- | ----------------------------- | ----- | ----------------------------------------- |
| `validator` | [Validator](broken-reference) |       | validator defines the the validator info. |

### QueryDelegatorValidatorsRequest

QueryDelegatorValidatorsRequest is request type for the Query/DelegatorValidators RPC method.

| Field            | Type                                                      | Label | Description                                                 |
| ---------------- | --------------------------------------------------------- | ----- | ----------------------------------------------------------- |
| `delegator_addr` | [string](broken-reference)                                |       | delegator\_addr defines the delegator address to query for. |
| `pagination`     | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request.  |

### QueryDelegatorValidatorsResponse

QueryDelegatorValidatorsResponse is response type for the Query/DelegatorValidators RPC method.

| Field        | Type                                                       | Label    | Description                                                 |
| ------------ | ---------------------------------------------------------- | -------- | ----------------------------------------------------------- |
| `validators` | [Validator](broken-reference)                              | repeated | validators defines the the validators' info of a delegator. |
| `pagination` | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response.          |

### QueryHistoricalInfoRequest

QueryHistoricalInfoRequest is request type for the Query/HistoricalInfo RPC method.

| Field    | Type                      | Label | Description                                                  |
| -------- | ------------------------- | ----- | ------------------------------------------------------------ |
| `height` | [int64](broken-reference) |       | height defines at which height to query the historical info. |

### QueryHistoricalInfoResponse

QueryHistoricalInfoResponse is response type for the Query/HistoricalInfo RPC method.

| Field  | Type                               | Label | Description                                           |
| ------ | ---------------------------------- | ----- | ----------------------------------------------------- |
| `hist` | [HistoricalInfo](broken-reference) |       | hist defines the historical info at the given height. |

### QueryParamsRequest

QueryParamsRequest is request type for the Query/Params RPC method.

### QueryParamsResponse

QueryParamsResponse is response type for the Query/Params RPC method.

| Field    | Type                       | Label | Description                                     |
| -------- | -------------------------- | ----- | ----------------------------------------------- |
| `params` | [Params](broken-reference) |       | params holds all the parameters of this module. |

### QueryPoolRequest

QueryPoolRequest is request type for the Query/Pool RPC method.

### QueryPoolResponse

QueryPoolResponse is response type for the Query/Pool RPC method.

| Field  | Type                     | Label | Description                 |
| ------ | ------------------------ | ----- | --------------------------- |
| `pool` | [Pool](broken-reference) |       | pool defines the pool info. |

### QueryRedelegationsRequest

QueryRedelegationsRequest is request type for the Query/Redelegations RPC method.

| Field                | Type                                                      | Label | Description                                                            |
| -------------------- | --------------------------------------------------------- | ----- | ---------------------------------------------------------------------- |
| `delegator_addr`     | [string](broken-reference)                                |       | delegator\_addr defines the delegator address to query for.            |
| `src_validator_addr` | [string](broken-reference)                                |       | src\_validator\_addr defines the validator address to redelegate from. |
| `dst_validator_addr` | [string](broken-reference)                                |       | dst\_validator\_addr defines the validator address to redelegate to.   |
| `pagination`         | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request.             |

### QueryRedelegationsResponse

QueryRedelegationsResponse is response type for the Query/Redelegations RPC method.

| Field                    | Type                                                       | Label    | Description                                        |
| ------------------------ | ---------------------------------------------------------- | -------- | -------------------------------------------------- |
| `redelegation_responses` | [RedelegationResponse](broken-reference)                   | repeated |                                                    |
| `pagination`             | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response. |

### QueryUnbondingDelegationRequest

QueryUnbondingDelegationRequest is request type for the Query/UnbondingDelegation RPC method.

| Field            | Type                       | Label | Description                                                 |
| ---------------- | -------------------------- | ----- | ----------------------------------------------------------- |
| `delegator_addr` | [string](broken-reference) |       | delegator\_addr defines the delegator address to query for. |
| `validator_addr` | [string](broken-reference) |       | validator\_addr defines the validator address to query for. |

### QueryUnbondingDelegationResponse

QueryDelegationResponse is response type for the Query/UnbondingDelegation RPC method.

| Field    | Type                                    | Label | Description                                               |
| -------- | --------------------------------------- | ----- | --------------------------------------------------------- |
| `unbond` | [UnbondingDelegation](broken-reference) |       | unbond defines the unbonding information of a delegation. |

### QueryValidatorDelegationsRequest

QueryValidatorDelegationsRequest is request type for the Query/ValidatorDelegations RPC method

| Field            | Type                                                      | Label | Description                                                 |
| ---------------- | --------------------------------------------------------- | ----- | ----------------------------------------------------------- |
| `validator_addr` | [string](broken-reference)                                |       | validator\_addr defines the validator address to query for. |
| `pagination`     | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request.  |

### QueryValidatorDelegationsResponse

QueryValidatorDelegationsResponse is response type for the Query/ValidatorDelegations RPC method

| Field                  | Type                                                       | Label    | Description                                        |
| ---------------------- | ---------------------------------------------------------- | -------- | -------------------------------------------------- |
| `delegation_responses` | [DelegationResponse](broken-reference)                     | repeated |                                                    |
| `pagination`           | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response. |

### QueryValidatorRequest

QueryValidatorRequest is response type for the Query/Validator RPC method

| Field            | Type                       | Label | Description                                                 |
| ---------------- | -------------------------- | ----- | ----------------------------------------------------------- |
| `validator_addr` | [string](broken-reference) |       | validator\_addr defines the validator address to query for. |

### QueryValidatorResponse

QueryValidatorResponse is response type for the Query/Validator RPC method

| Field       | Type                          | Label | Description                               |
| ----------- | ----------------------------- | ----- | ----------------------------------------- |
| `validator` | [Validator](broken-reference) |       | validator defines the the validator info. |

### QueryValidatorUnbondingDelegationsRequest

QueryValidatorUnbondingDelegationsRequest is required type for the Query/ValidatorUnbondingDelegations RPC method

| Field            | Type                                                      | Label | Description                                                 |
| ---------------- | --------------------------------------------------------- | ----- | ----------------------------------------------------------- |
| `validator_addr` | [string](broken-reference)                                |       | validator\_addr defines the validator address to query for. |
| `pagination`     | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request.  |

### QueryValidatorUnbondingDelegationsResponse

QueryValidatorUnbondingDelegationsResponse is response type for the Query/ValidatorUnbondingDelegations RPC method.

| Field                 | Type                                                       | Label    | Description                                        |
| --------------------- | ---------------------------------------------------------- | -------- | -------------------------------------------------- |
| `unbonding_responses` | [UnbondingDelegation](broken-reference)                    | repeated |                                                    |
| `pagination`          | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response. |

### QueryValidatorsRequest

QueryValidatorsRequest is request type for Query/Validators RPC method.

| Field        | Type                                                      | Label | Description                                                     |
| ------------ | --------------------------------------------------------- | ----- | --------------------------------------------------------------- |
| `status`     | [string](broken-reference)                                |       | status enables to query for validators matching a given status. |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request.      |

### QueryValidatorsResponse

QueryValidatorsResponse is response type for the Query/Validators RPC method

| Field        | Type                                                       | Label    | Description                                        |
| ------------ | ---------------------------------------------------------- | -------- | -------------------------------------------------- |
| `validators` | [Validator](broken-reference)                              | repeated | validators contains all the queried validators.    |
| `pagination` | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response. |

### Query

Query defines the gRPC querier service.

| Method Name                     | Request Type                                                  | Response Type                                                  | Description                                                                                   | HTTP Verb | Endpoint                                                                                                 |
| ------------------------------- | ------------------------------------------------------------- | -------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------- | -------------------------------------------------------------------------------------------------------- |
| `Validators`                    | [QueryValidatorsRequest](broken-reference)                    | [QueryValidatorsResponse](broken-reference)                    | Validators queries all validators that match the given status.                                | GET       | /cosmos/staking/v1beta1/validators                                                                       |
| `Validator`                     | [QueryValidatorRequest](broken-reference)                     | [QueryValidatorResponse](broken-reference)                     | Validator queries validator info for given validator address.                                 | GET       | /cosmos/staking/v1beta1/validators/{validator\_addr}                                                     |
| `ValidatorDelegations`          | [QueryValidatorDelegationsRequest](broken-reference)          | [QueryValidatorDelegationsResponse](broken-reference)          | ValidatorDelegations queries delegate info for given validator.                               | GET       | /cosmos/staking/v1beta1/validators/{validator\_addr}/delegations                                         |
| `ValidatorUnbondingDelegations` | [QueryValidatorUnbondingDelegationsRequest](broken-reference) | [QueryValidatorUnbondingDelegationsResponse](broken-reference) | ValidatorUnbondingDelegations queries unbonding delegations of a validator.                   | GET       | /cosmos/staking/v1beta1/validators/{validator\_addr}/unbonding\_delegations                              |
| `Delegation`                    | [QueryDelegationRequest](broken-reference)                    | [QueryDelegationResponse](broken-reference)                    | Delegation queries delegate info for given validator delegator pair.                          | GET       | /cosmos/staking/v1beta1/validators/{validator\_addr}/delegations/{delegator\_addr}                       |
| `UnbondingDelegation`           | [QueryUnbondingDelegationRequest](broken-reference)           | [QueryUnbondingDelegationResponse](broken-reference)           | UnbondingDelegation queries unbonding info for given validator delegator pair.                | GET       | /cosmos/staking/v1beta1/validators/{validator\_addr}/delegations/{delegator\_addr}/unbonding\_delegation |
| `DelegatorDelegations`          | [QueryDelegatorDelegationsRequest](broken-reference)          | [QueryDelegatorDelegationsResponse](broken-reference)          | DelegatorDelegations queries all delegations of a given delegator address.                    | GET       | /cosmos/staking/v1beta1/delegations/{delegator\_addr}                                                    |
| `DelegatorUnbondingDelegations` | [QueryDelegatorUnbondingDelegationsRequest](broken-reference) | [QueryDelegatorUnbondingDelegationsResponse](broken-reference) | DelegatorUnbondingDelegations queries all unbonding delegations of a given delegator address. | GET       | /cosmos/staking/v1beta1/delegators/{delegator\_addr}/unbonding\_delegations                              |
| `Redelegations`                 | [QueryRedelegationsRequest](broken-reference)                 | [QueryRedelegationsResponse](broken-reference)                 | Redelegations queries redelegations of given address.                                         | GET       | /cosmos/staking/v1beta1/delegators/{delegator\_addr}/redelegations                                       |
| `DelegatorValidators`           | [QueryDelegatorValidatorsRequest](broken-reference)           | [QueryDelegatorValidatorsResponse](broken-reference)           | DelegatorValidators queries all validators info for given delegator address.                  | GET       | /cosmos/staking/v1beta1/delegators/{delegator\_addr}/validators                                          |
| `DelegatorValidator`            | [QueryDelegatorValidatorRequest](broken-reference)            | [QueryDelegatorValidatorResponse](broken-reference)            | DelegatorValidator queries validator info for given delegator validator pair.                 | GET       | /cosmos/staking/v1beta1/delegators/{delegator\_addr}/validators/{validator\_addr}                        |
| `HistoricalInfo`                | [QueryHistoricalInfoRequest](broken-reference)                | [QueryHistoricalInfoResponse](broken-reference)                | HistoricalInfo queries the historical info for given height.                                  | GET       | /cosmos/staking/v1beta1/historical\_info/{height}                                                        |
| `Pool`                          | [QueryPoolRequest](broken-reference)                          | [QueryPoolResponse](broken-reference)                          | Pool queries the pool info.                                                                   | GET       | /cosmos/staking/v1beta1/pool                                                                             |
| `Params`                        | [QueryParamsRequest](broken-reference)                        | [QueryParamsResponse](broken-reference)                        | Parameters queries the staking parameters.                                                    | GET       | /cosmos/staking/v1beta1/params                                                                           |

## cosmos/staking/v1beta1/tx.proto

### MsgBeginRedelegate

MsgBeginRedelegate defines a SDK message for performing a redelegation of coins from a delegator and source validator to a destination validator.

| Field                   | Type                                         | Label | Description |
| ----------------------- | -------------------------------------------- | ----- | ----------- |
| `delegator_address`     | [string](broken-reference)                   |       |             |
| `validator_src_address` | [string](broken-reference)                   |       |             |
| `validator_dst_address` | [string](broken-reference)                   |       |             |
| `amount`                | [cosmos.base.v1beta1.Coin](broken-reference) |       |             |

### MsgBeginRedelegateResponse

MsgBeginRedelegateResponse defines the Msg/BeginRedelegate response type.

| Field             | Type                                          | Label | Description |
| ----------------- | --------------------------------------------- | ----- | ----------- |
| `completion_time` | [google.protobuf.Timestamp](broken-reference) |       |             |

### MsgCreateValidator

MsgCreateValidator defines a SDK message for creating a new validator.

| Field                 | Type                                         | Label | Description |
| --------------------- | -------------------------------------------- | ----- | ----------- |
| `description`         | [Description](broken-reference)              |       |             |
| `commission`          | [CommissionRates](broken-reference)          |       |             |
| `min_self_delegation` | [string](broken-reference)                   |       |             |
| `delegator_address`   | [string](broken-reference)                   |       |             |
| `validator_address`   | [string](broken-reference)                   |       |             |
| `pubkey`              | [google.protobuf.Any](broken-reference)      |       |             |
| `value`               | [cosmos.base.v1beta1.Coin](broken-reference) |       |             |

### MsgCreateValidatorResponse

MsgCreateValidatorResponse defines the Msg/CreateValidator response type.

### MsgDelegate

MsgDelegate defines a SDK message for performing a delegation of coins from a delegator to a validator.

| Field               | Type                                         | Label | Description |
| ------------------- | -------------------------------------------- | ----- | ----------- |
| `delegator_address` | [string](broken-reference)                   |       |             |
| `validator_address` | [string](broken-reference)                   |       |             |
| `amount`            | [cosmos.base.v1beta1.Coin](broken-reference) |       |             |

### MsgDelegateResponse

MsgDelegateResponse defines the Msg/Delegate response type.

### MsgEditValidator

MsgEditValidator defines a SDK message for editing an existing validator.

| Field                 | Type                            | Label | Description                                                                                                                                                                                                                 |
| --------------------- | ------------------------------- | ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `description`         | [Description](broken-reference) |       |                                                                                                                                                                                                                             |
| `validator_address`   | [string](broken-reference)      |       |                                                                                                                                                                                                                             |
| `commission_rate`     | [string](broken-reference)      |       | We pass a reference to the new commission rate and min self delegation as it's not mandatory to update. If not updated, the deserialized rate will be zero with no way to distinguish if an update was intended. REF: #2373 |
| `min_self_delegation` | [string](broken-reference)      |       |                                                                                                                                                                                                                             |

### MsgEditValidatorResponse

MsgEditValidatorResponse defines the Msg/EditValidator response type.

### MsgUndelegate

MsgUndelegate defines a SDK message for performing an undelegation from a delegate and a validator.

| Field               | Type                                         | Label | Description |
| ------------------- | -------------------------------------------- | ----- | ----------- |
| `delegator_address` | [string](broken-reference)                   |       |             |
| `validator_address` | [string](broken-reference)                   |       |             |
| `amount`            | [cosmos.base.v1beta1.Coin](broken-reference) |       |             |

### MsgUndelegateResponse

MsgUndelegateResponse defines the Msg/Undelegate response type.

| Field             | Type                                          | Label | Description |
| ----------------- | --------------------------------------------- | ----- | ----------- |
| `completion_time` | [google.protobuf.Timestamp](broken-reference) |       |             |

### Msg

Msg defines the staking Msg service.

| Method Name       | Request Type                           | Response Type                                  | Description                                                                                                                               | HTTP Verb | Endpoint |
| ----------------- | -------------------------------------- | ---------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | --------- | -------- |
| `CreateValidator` | [MsgCreateValidator](broken-reference) | [MsgCreateValidatorResponse](broken-reference) | CreateValidator defines a method for creating a new validator.                                                                            |           |          |
| `EditValidator`   | [MsgEditValidator](broken-reference)   | [MsgEditValidatorResponse](broken-reference)   | EditValidator defines a method for editing an existing validator.                                                                         |           |          |
| `Delegate`        | [MsgDelegate](broken-reference)        | [MsgDelegateResponse](broken-reference)        | Delegate defines a method for performing a delegation of coins from a delegator to a validator.                                           |           |          |
| `BeginRedelegate` | [MsgBeginRedelegate](broken-reference) | [MsgBeginRedelegateResponse](broken-reference) | BeginRedelegate defines a method for performing a redelegation of coins from a delegator and source validator to a destination validator. |           |          |
| `Undelegate`      | [MsgUndelegate](broken-reference)      | [MsgUndelegateResponse](broken-reference)      | Undelegate defines a method for performing an undelegation from a delegate and a validator.                                               |           |          |

## cosmos/tx/signing/v1beta1/signing.proto

### SignatureDescriptor

SignatureDescriptor is a convenience type which represents the full data for a signature including the public key of the signer, signing modes and the signature itself. It is primarily used for coordinating signatures between clients.

| Field        | Type                                         | Label | Description                                                                                                                                                    |
| ------------ | -------------------------------------------- | ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `public_key` | [google.protobuf.Any](broken-reference)      |       | public\_key is the public key of the signer                                                                                                                    |
| `data`       | [SignatureDescriptor.Data](broken-reference) |       |                                                                                                                                                                |
| `sequence`   | [uint64](broken-reference)                   |       | sequence is the sequence of the account, which describes the number of committed transactions signed by a given address. It is used to prevent replay attacks. |

### SignatureDescriptor.Data

Data represents signature data

| Field    | Type                                                | Label | Description                        |
| -------- | --------------------------------------------------- | ----- | ---------------------------------- |
| `single` | [SignatureDescriptor.Data.Single](broken-reference) |       | single represents a single signer  |
| `multi`  | [SignatureDescriptor.Data.Multi](broken-reference)  |       | multi represents a multisig signer |

### SignatureDescriptor.Data.Multi

Multi is the signature data for a multisig public key

| Field        | Type                                                               | Label    | Description                                                   |
| ------------ | ------------------------------------------------------------------ | -------- | ------------------------------------------------------------- |
| `bitarray`   | [cosmos.crypto.multisig.v1beta1.CompactBitArray](broken-reference) |          | bitarray specifies which keys within the multisig are signing |
| `signatures` | [SignatureDescriptor.Data](broken-reference)                       | repeated | signatures is the signatures of the multi-signature           |

### SignatureDescriptor.Data.Single

Single is the signature data for a single signer

| Field       | Type                         | Label | Description                                   |
| ----------- | ---------------------------- | ----- | --------------------------------------------- |
| `mode`      | [SignMode](broken-reference) |       | mode is the signing mode of the single signer |
| `signature` | [bytes](broken-reference)    |       | signature is the raw signature bytes          |

### SignatureDescriptors

SignatureDescriptors wraps multiple SignatureDescriptor's.

| Field        | Type                                    | Label    | Description                              |
| ------------ | --------------------------------------- | -------- | ---------------------------------------- |
| `signatures` | [SignatureDescriptor](broken-reference) | repeated | signatures are the signature descriptors |

### SignMode

SignMode represents a signing mode with its own security guarantees.

| Name                            | Number | Description                                                                                                                                                          |
| ------------------------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SIGN\_MODE\_UNSPECIFIED         | 0      | SIGN\_MODE\_UNSPECIFIED specifies an unknown signing mode and will be rejected                                                                                       |
| SIGN\_MODE\_DIRECT              | 1      | SIGN\_MODE\_DIRECT specifies a signing mode which uses SignDoc and is verified with raw bytes from Tx                                                                |
| SIGN\_MODE\_TEXTUAL             | 2      | SIGN\_MODE\_TEXTUAL is a future signing mode that will verify some human-readable textual representation on top of the binary representation from SIGN\_MODE\_DIRECT |
| SIGN\_MODE\_LEGACY\_AMINO\_JSON | 127    | SIGN\_MODE\_LEGACY\_AMINO\_JSON is a backwards compatibility mode which uses Amino JSON and will be removed in the future                                            |

## cosmos/tx/v1beta1/tx.proto

### AuthInfo

AuthInfo describes the fee and signer modes that are used to sign a transaction.

| Field          | Type                           | Label    | Description                                                                                                                                                                                                                                                                        |
| -------------- | ------------------------------ | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `signer_infos` | [SignerInfo](broken-reference) | repeated | signer\_infos defines the signing modes for the required signers. The number and order of elements must match the required signers from TxBody's messages. The first element is the primary signer and the one which pays the fee.                                                 |
| `fee`          | [Fee](broken-reference)        |          | Fee is the fee and gas limit for the transaction. The first signer is the primary signer and the one which pays the fee. The fee can be calculated based on the cost of evaluating the body and doing signature verification of the signers. This can be estimated via simulation. |

### Fee

Fee includes the amount of coins paid in fees and the maximum gas to be used by the transaction. The ratio yields an effective "gasprice", which must be above some miminum to be accepted into the mempool.

| Field       | Type                                         | Label    | Description                                                                                                                                                                                                                                                                             |
| ----------- | -------------------------------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `amount`    | [cosmos.base.v1beta1.Coin](broken-reference) | repeated | amount is the amount of coins to be paid as a fee                                                                                                                                                                                                                                       |
| `gas_limit` | [uint64](broken-reference)                   |          | gas\_limit is the maximum gas that can be used in transaction processing before an out of gas error occurs                                                                                                                                                                              |
| `payer`     | [string](broken-reference)                   |          | if unset, the first signer is responsible for paying the fees. If set, the specified account must pay the fees. the payer must be a tx signer (and thus have signed this field in AuthInfo). setting this field does _not_ change the ordering of required signers for the transaction. |
| `granter`   | [string](broken-reference)                   |          | if set, the fee payer (either the first signer or the value of the payer field) requests that a fee grant be used to pay fees instead of the fee payer's own balance. If an appropriate fee grant does not exist or the chain does not support fee grants, this will fail               |

### ModeInfo

ModeInfo describes the signing mode of a single or nested multisig signer.

| Field    | Type                                | Label | Description                               |
| -------- | ----------------------------------- | ----- | ----------------------------------------- |
| `single` | [ModeInfo.Single](broken-reference) |       | single represents a single signer         |
| `multi`  | [ModeInfo.Multi](broken-reference)  |       | multi represents a nested multisig signer |

### ModeInfo.Multi

Multi is the mode info for a multisig public key

| Field        | Type                                                               | Label    | Description                                                                                                           |
| ------------ | ------------------------------------------------------------------ | -------- | --------------------------------------------------------------------------------------------------------------------- |
| `bitarray`   | [cosmos.crypto.multisig.v1beta1.CompactBitArray](broken-reference) |          | bitarray specifies which keys within the multisig are signing                                                         |
| `mode_infos` | [ModeInfo](broken-reference)                                       | repeated | mode\_infos is the corresponding modes of the signers of the multisig which could include nested multisig public keys |

### ModeInfo.Single

Single is the mode info for a single signer. It is structured as a message to allow for additional fields such as locale for SIGN\_MODE\_TEXTUAL in the future

| Field  | Type                                                   | Label | Description                                   |
| ------ | ------------------------------------------------------ | ----- | --------------------------------------------- |
| `mode` | [cosmos.tx.signing.v1beta1.SignMode](broken-reference) |       | mode is the signing mode of the single signer |

### SignDoc

SignDoc is the type used for generating sign bytes for SIGN\_MODE\_DIRECT.

| Field             | Type                       | Label | Description                                                                                                                                               |
| ----------------- | -------------------------- | ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `body_bytes`      | [bytes](broken-reference)  |       | body\_bytes is protobuf serialization of a TxBody that matches the representation in TxRaw.                                                               |
| `auth_info_bytes` | [bytes](broken-reference)  |       | auth\_info\_bytes is a protobuf serialization of an AuthInfo that matches the representation in TxRaw.                                                    |
| `chain_id`        | [string](broken-reference) |       | chain\_id is the unique identifier of the chain this transaction targets. It prevents signed transactions from being used on another chain by an attacker |
| `account_number`  | [uint64](broken-reference) |       | account\_number is the account number of the account in state                                                                                             |

### SignerInfo

SignerInfo describes the public key and signing mode of a single top-level signer.

| Field        | Type                                    | Label | Description                                                                                                                                                                                                     |
| ------------ | --------------------------------------- | ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `public_key` | [google.protobuf.Any](broken-reference) |       | public\_key is the public key of the signer. It is optional for accounts that already exist in state. If unset, the verifier can use the required \ signer address for this position and lookup the public key. |
| `mode_info`  | [ModeInfo](broken-reference)            |       | mode\_info describes the signing mode of the signer and is a nested structure to support nested multisig pubkey's                                                                                               |
| `sequence`   | [uint64](broken-reference)              |       | sequence is the sequence of the account, which describes the number of committed transactions signed by a given address. It is used to prevent replay attacks.                                                  |

### Tx

Tx is the standard type used for broadcasting transactions.

| Field        | Type                         | Label    | Description                                                                                                                                                                                   |
| ------------ | ---------------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `body`       | [TxBody](broken-reference)   |          | body is the processable content of the transaction                                                                                                                                            |
| `auth_info`  | [AuthInfo](broken-reference) |          | auth\_info is the authorization related content of the transaction, specifically signers, signer modes and fee                                                                                |
| `signatures` | [bytes](broken-reference)    | repeated | signatures is a list of signatures that matches the length and order of AuthInfo's signer\_infos to allow connecting signature meta information like public key and signing mode by position. |

### TxBody

TxBody is the body of a transaction that all signers sign over.

| Field                            | Type                                    | Label    | Description                                                                                                                                                                                                                                                                                                                                                                                                                |
| -------------------------------- | --------------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `messages`                       | [google.protobuf.Any](broken-reference) | repeated | messages is a list of messages to be executed. The required signers of those messages define the number and order of elements in AuthInfo's signer\_infos and Tx's signatures. Each required signer address is added to the list only the first time it occurs. By convention, the first required signer (usually from the first message) is referred to as the primary signer and pays the fee for the whole transaction. |
| `memo`                           | [string](broken-reference)              |          | memo is any arbitrary memo to be added to the transaction                                                                                                                                                                                                                                                                                                                                                                  |
| `timeout_height`                 | [uint64](broken-reference)              |          | timeout is the block height after which this transaction will not be processed by the chain                                                                                                                                                                                                                                                                                                                                |
| `extension_options`              | [google.protobuf.Any](broken-reference) | repeated | extension\_options are arbitrary options that can be added by chains when the default options are not sufficient. If any of these are present and can't be handled, the transaction will be rejected                                                                                                                                                                                                                       |
| `non_critical_extension_options` | [google.protobuf.Any](broken-reference) | repeated | extension\_options are arbitrary options that can be added by chains when the default options are not sufficient. If any of these are present and can't be handled, they will be ignored                                                                                                                                                                                                                                   |

### TxRaw

TxRaw is a variant of Tx that pins the signer's exact binary representation of body and auth\_info. This is used for signing, broadcasting and verification. The binary `serialize(tx: TxRaw)` is stored in Tendermint and the hash `sha256(serialize(tx: TxRaw))` becomes the "txhash", commonly used as the transaction ID.

| Field             | Type                      | Label    | Description                                                                                                                                                                                   |
| ----------------- | ------------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `body_bytes`      | [bytes](broken-reference) |          | body\_bytes is a protobuf serialization of a TxBody that matches the representation in SignDoc.                                                                                               |
| `auth_info_bytes` | [bytes](broken-reference) |          | auth\_info\_bytes is a protobuf serialization of an AuthInfo that matches the representation in SignDoc.                                                                                      |
| `signatures`      | [bytes](broken-reference) | repeated | signatures is a list of signatures that matches the length and order of AuthInfo's signer\_infos to allow connecting signature meta information like public key and signing mode by position. |

## cosmos/tx/v1beta1/service.proto

### BroadcastTxRequest

BroadcastTxRequest is the request type for the Service.BroadcastTxRequest RPC method.

| Field      | Type                              | Label | Description                       |
| ---------- | --------------------------------- | ----- | --------------------------------- |
| `tx_bytes` | [bytes](broken-reference)         |       | tx\_bytes is the raw transaction. |
| `mode`     | [BroadcastMode](broken-reference) |       |                                   |

### BroadcastTxResponse

BroadcastTxResponse is the response type for the Service.BroadcastTx method.

| Field         | Type                                                    | Label | Description                              |
| ------------- | ------------------------------------------------------- | ----- | ---------------------------------------- |
| `tx_response` | [cosmos.base.abci.v1beta1.TxResponse](broken-reference) |       | tx\_response is the queried TxResponses. |

### GetTxRequest

GetTxRequest is the request type for the Service.GetTx RPC method.

| Field  | Type                       | Label | Description                                            |
| ------ | -------------------------- | ----- | ------------------------------------------------------ |
| `hash` | [string](broken-reference) |       | hash is the tx hash to query, encoded as a hex string. |

### GetTxResponse

GetTxResponse is the response type for the Service.GetTx method.

| Field         | Type                                                    | Label | Description                              |
| ------------- | ------------------------------------------------------- | ----- | ---------------------------------------- |
| `tx`          | [Tx](broken-reference)                                  |       | tx is the queried transaction.           |
| `tx_response` | [cosmos.base.abci.v1beta1.TxResponse](broken-reference) |       | tx\_response is the queried TxResponses. |

### GetTxsEventRequest

GetTxsEventRequest is the request type for the Service.TxsByEvents RPC method.

| Field        | Type                                                      | Label    | Description                                       |
| ------------ | --------------------------------------------------------- | -------- | ------------------------------------------------- |
| `events`     | [string](broken-reference)                                | repeated | events is the list of transaction event type.     |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |          | pagination defines an pagination for the request. |
| `order_by`   | [OrderBy](broken-reference)                               |          |                                                   |

### GetTxsEventResponse

GetTxsEventResponse is the response type for the Service.TxsByEvents RPC method.

| Field          | Type                                                       | Label    | Description                                        |
| -------------- | ---------------------------------------------------------- | -------- | -------------------------------------------------- |
| `txs`          | [Tx](broken-reference)                                     | repeated | txs is the list of queried transactions.           |
| `tx_responses` | [cosmos.base.abci.v1beta1.TxResponse](broken-reference)    | repeated | tx\_responses is the list of queried TxResponses.  |
| `pagination`   | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines an pagination for the response. |

### SimulateRequest

SimulateRequest is the request type for the Service.Simulate RPC method.

| Field | Type                   | Label | Description                        |
| ----- | ---------------------- | ----- | ---------------------------------- |
| `tx`  | [Tx](broken-reference) |       | tx is the transaction to simulate. |

### SimulateResponse

SimulateResponse is the response type for the Service.SimulateRPC method.

| Field      | Type                                                 | Label | Description                                                    |
| ---------- | ---------------------------------------------------- | ----- | -------------------------------------------------------------- |
| `gas_info` | [cosmos.base.abci.v1beta1.GasInfo](broken-reference) |       | gas\_info is the information about gas used in the simulation. |
| `result`   | [cosmos.base.abci.v1beta1.Result](broken-reference)  |       | result is the result of the simulation.                        |

### BroadcastMode

BroadcastMode specifies the broadcast mode for the TxService.Broadcast RPC method.

| Name                         | Number | Description                                                                                                         |
| ---------------------------- | ------ | ------------------------------------------------------------------------------------------------------------------- |
| BROADCAST\_MODE\_UNSPECIFIED | 0      | zero-value for mode ordering                                                                                        |
| BROADCAST\_MODE\_BLOCK       | 1      | BROADCAST\_MODE\_BLOCK defines a tx broadcasting mode where the client waits for the tx to be committed in a block. |
| BROADCAST\_MODE\_SYNC        | 2      | BROADCAST\_MODE\_SYNC defines a tx broadcasting mode where the client waits for a CheckTx execution response only.  |
| BROADCAST\_MODE\_ASYNC       | 3      | BROADCAST\_MODE\_ASYNC defines a tx broadcasting mode where the client returns immediately.                         |

### OrderBy

OrderBy defines the sorting order

| Name                   | Number | Description                                                                                      |
| ---------------------- | ------ | ------------------------------------------------------------------------------------------------ |
| ORDER\_BY\_UNSPECIFIED | 0      | ORDER\_BY\_UNSPECIFIED specifies an unknown sorting order. OrderBy defaults to ASC in this case. |
| ORDER\_BY\_ASC         | 1      | ORDER\_BY\_ASC defines ascending order                                                           |
| ORDER\_BY\_DESC        | 2      | ORDER\_BY\_DESC defines descending order                                                         |

### Service

Service defines a gRPC service for interacting with transactions.

| Method Name   | Request Type                           | Response Type                           | Description                                                          | HTTP Verb | Endpoint                      |
| ------------- | -------------------------------------- | --------------------------------------- | -------------------------------------------------------------------- | --------- | ----------------------------- |
| `Simulate`    | [SimulateRequest](broken-reference)    | [SimulateResponse](broken-reference)    | Simulate simulates executing a transaction for estimating gas usage. | POST      | /cosmos/tx/v1beta1/simulate   |
| `GetTx`       | [GetTxRequest](broken-reference)       | [GetTxResponse](broken-reference)       | GetTx fetches a tx by hash.                                          | GET       | /cosmos/tx/v1beta1/txs/{hash} |
| `BroadcastTx` | [BroadcastTxRequest](broken-reference) | [BroadcastTxResponse](broken-reference) | BroadcastTx broadcast transaction.                                   | POST      | /cosmos/tx/v1beta1/txs        |
| `GetTxsEvent` | [GetTxsEventRequest](broken-reference) | [GetTxsEventResponse](broken-reference) | GetTxsEvent fetches txs by event.                                    | GET       | /cosmos/tx/v1beta1/txs        |

## cosmos/upgrade/v1beta1/upgrade.proto

### CancelSoftwareUpgradeProposal

CancelSoftwareUpgradeProposal is a gov Content type for cancelling a software upgrade.

| Field         | Type                       | Label | Description |
| ------------- | -------------------------- | ----- | ----------- |
| `title`       | [string](broken-reference) |       |             |
| `description` | [string](broken-reference) |       |             |

### Plan

Plan specifies information about a planned upgrade and when it should occur.

| Field                   | Type                                          | Label | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ----------------------- | --------------------------------------------- | ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`                  | [string](broken-reference)                    |       | Sets the name for the upgrade. This name will be used by the upgraded version of the software to apply any special "on-upgrade" commands during the first BeginBlock method after the upgrade is applied. It is also used to detect whether a software version can handle a given upgrade. If no upgrade handler with this name has been set in the software, it will be assumed that the software is out-of-date when the upgrade Time or Height is reached and the software will exit. |
| `time`                  | [google.protobuf.Timestamp](broken-reference) |       | The time after which the upgrade must be performed. Leave set to its zero value to use a pre-defined Height instead.                                                                                                                                                                                                                                                                                                                                                                     |
| `height`                | [int64](broken-reference)                     |       | The height at which the upgrade must be performed. Only used if Time is not set.                                                                                                                                                                                                                                                                                                                                                                                                         |
| `info`                  | [string](broken-reference)                    |       | Any application specific upgrade info to be included on-chain such as a git commit that validators could automatically upgrade to                                                                                                                                                                                                                                                                                                                                                        |
| `upgraded_client_state` | [google.protobuf.Any](broken-reference)       |       | IBC-enabled chains can opt-in to including the upgraded client state in its upgrade plan This will make the chain commit to the correct upgraded (self) client state before the upgrade occurs, so that connecting chains can verify that the new upgraded client is valid by verifying a proof on the previous version of the chain. This will allow IBC connections to persist smoothly across planned chain upgrades                                                                  |

### SoftwareUpgradeProposal

SoftwareUpgradeProposal is a gov Content type for initiating a software upgrade.

| Field         | Type                       | Label | Description |
| ------------- | -------------------------- | ----- | ----------- |
| `title`       | [string](broken-reference) |       |             |
| `description` | [string](broken-reference) |       |             |
| `plan`        | [Plan](broken-reference)   |       |             |

## cosmos/upgrade/v1beta1/query.proto

### QueryAppliedPlanRequest

QueryCurrentPlanRequest is the request type for the Query/AppliedPlan RPC method.

| Field  | Type                       | Label | Description                                        |
| ------ | -------------------------- | ----- | -------------------------------------------------- |
| `name` | [string](broken-reference) |       | name is the name of the applied plan to query for. |

### QueryAppliedPlanResponse

QueryAppliedPlanResponse is the response type for the Query/AppliedPlan RPC method.

| Field    | Type                      | Label | Description                                               |
| -------- | ------------------------- | ----- | --------------------------------------------------------- |
| `height` | [int64](broken-reference) |       | height is the block height at which the plan was applied. |

### QueryCurrentPlanRequest

QueryCurrentPlanRequest is the request type for the Query/CurrentPlan RPC method.

### QueryCurrentPlanResponse

QueryCurrentPlanResponse is the response type for the Query/CurrentPlan RPC method.

| Field  | Type                     | Label | Description                       |
| ------ | ------------------------ | ----- | --------------------------------- |
| `plan` | [Plan](broken-reference) |       | plan is the current upgrade plan. |

### QueryUpgradedConsensusStateRequest

QueryUpgradedConsensusStateRequest is the request type for the Query/UpgradedConsensusState RPC method.

| Field         | Type                      | Label | Description                                                                                                               |
| ------------- | ------------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------- |
| `last_height` | [int64](broken-reference) |       | last height of the current chain must be sent in request as this is the height under which next consensus state is stored |

### QueryUpgradedConsensusStateResponse

QueryUpgradedConsensusStateResponse is the response type for the Query/UpgradedConsensusState RPC method.

| Field                      | Type                                    | Label | Description |
| -------------------------- | --------------------------------------- | ----- | ----------- |
| `upgraded_consensus_state` | [google.protobuf.Any](broken-reference) |       |             |

### Query

Query defines the gRPC upgrade querier service.

| Method Name              | Request Type                                           | Response Type                                           | Description                                                                                                                                                                                                                                      | HTTP Verb | Endpoint                                                          |
| ------------------------ | ------------------------------------------------------ | ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- | ----------------------------------------------------------------- |
| `CurrentPlan`            | [QueryCurrentPlanRequest](broken-reference)            | [QueryCurrentPlanResponse](broken-reference)            | CurrentPlan queries the current upgrade plan.                                                                                                                                                                                                    | GET       | /cosmos/upgrade/v1beta1/current\_plan                             |
| `AppliedPlan`            | [QueryAppliedPlanRequest](broken-reference)            | [QueryAppliedPlanResponse](broken-reference)            | AppliedPlan queries a previously applied upgrade plan by its name.                                                                                                                                                                               | GET       | /cosmos/upgrade/v1beta1/applied\_plan/{name}                      |
| `UpgradedConsensusState` | [QueryUpgradedConsensusStateRequest](broken-reference) | [QueryUpgradedConsensusStateResponse](broken-reference) | UpgradedConsensusState queries the consensus state that will serve as a trusted kernel for the next version of this chain. It will only be stored at the last height of this chain. UpgradedConsensusState RPC not supported with legacy querier | GET       | /cosmos/upgrade/v1beta1/upgraded\_consensus\_state/{last\_height} |

## cosmos/vesting/v1beta1/tx.proto

### MsgCreateVestingAccount

MsgCreateVestingAccount defines a message that enables creating a vesting account.

| Field          | Type                                         | Label    | Description |
| -------------- | -------------------------------------------- | -------- | ----------- |
| `from_address` | [string](broken-reference)                   |          |             |
| `to_address`   | [string](broken-reference)                   |          |             |
| `amount`       | [cosmos.base.v1beta1.Coin](broken-reference) | repeated |             |
| `end_time`     | [int64](broken-reference)                    |          |             |
| `delayed`      | [bool](broken-reference)                     |          |             |

### MsgCreateVestingAccountResponse

MsgCreateVestingAccountResponse defines the Msg/CreateVestingAccount response type.

### Msg

Msg defines the bank Msg service.

| Method Name            | Request Type                                | Response Type                                       | Description                                                                    | HTTP Verb | Endpoint |
| ---------------------- | ------------------------------------------- | --------------------------------------------------- | ------------------------------------------------------------------------------ | --------- | -------- |
| `CreateVestingAccount` | [MsgCreateVestingAccount](broken-reference) | [MsgCreateVestingAccountResponse](broken-reference) | CreateVestingAccount defines a method that enables creating a vesting account. |           |          |

## cosmos/vesting/v1beta1/vesting.proto

### BaseVestingAccount

BaseVestingAccount implements the VestingAccount interface. It contains all the necessary fields needed for any vesting account implementation.

| Field               | Type                                                | Label    | Description |
| ------------------- | --------------------------------------------------- | -------- | ----------- |
| `base_account`      | [cosmos.auth.v1beta1.BaseAccount](broken-reference) |          |             |
| `original_vesting`  | [cosmos.base.v1beta1.Coin](broken-reference)        | repeated |             |
| `delegated_free`    | [cosmos.base.v1beta1.Coin](broken-reference)        | repeated |             |
| `delegated_vesting` | [cosmos.base.v1beta1.Coin](broken-reference)        | repeated |             |
| `end_time`          | [int64](broken-reference)                           |          |             |

### ContinuousVestingAccount

ContinuousVestingAccount implements the VestingAccount interface. It continuously vests by unlocking coins linearly with respect to time.

| Field                  | Type                                   | Label | Description |
| ---------------------- | -------------------------------------- | ----- | ----------- |
| `base_vesting_account` | [BaseVestingAccount](broken-reference) |       |             |
| `start_time`           | [int64](broken-reference)              |       |             |

### DelayedVestingAccount

DelayedVestingAccount implements the VestingAccount interface. It vests all coins after a specific time, but non prior. In other words, it keeps them locked until a specified time.

| Field                  | Type                                   | Label | Description |
| ---------------------- | -------------------------------------- | ----- | ----------- |
| `base_vesting_account` | [BaseVestingAccount](broken-reference) |       |             |

### Period

Period defines a length of time and amount of coins that will vest.

| Field    | Type                                         | Label    | Description |
| -------- | -------------------------------------------- | -------- | ----------- |
| `length` | [int64](broken-reference)                    |          |             |
| `amount` | [cosmos.base.v1beta1.Coin](broken-reference) | repeated |             |

### PeriodicVestingAccount

PeriodicVestingAccount implements the VestingAccount interface. It periodically vests by unlocking coins during each specified period.

| Field                  | Type                                   | Label    | Description |
| ---------------------- | -------------------------------------- | -------- | ----------- |
| `base_vesting_account` | [BaseVestingAccount](broken-reference) |          |             |
| `start_time`           | [int64](broken-reference)              |          |             |
| `vesting_periods`      | [Period](broken-reference)             | repeated |             |

## ibc/applications/transfer/v1/transfer.proto

### DenomTrace

DenomTrace contains the base denomination for ICS20 fungible tokens and the source tracing information path.

| Field        | Type                       | Label | Description                                                                                           |
| ------------ | -------------------------- | ----- | ----------------------------------------------------------------------------------------------------- |
| `path`       | [string](broken-reference) |       | path defines the chain of port/channel identifiers used for tracing the source of the fungible token. |
| `base_denom` | [string](broken-reference) |       | base denomination of the relayed fungible token.                                                      |

### FungibleTokenPacketData

FungibleTokenPacketData defines a struct for the packet payload See FungibleTokenPacketData spec: https://github.com/cosmos/ics/tree/master/spec/ics-020-fungible-token-transfer#data-structures

| Field      | Type                       | Label | Description                                    |
| ---------- | -------------------------- | ----- | ---------------------------------------------- |
| `denom`    | [string](broken-reference) |       | the token denomination to be transferred       |
| `amount`   | [uint64](broken-reference) |       | the token amount to be transferred             |
| `sender`   | [string](broken-reference) |       | the sender address                             |
| `receiver` | [string](broken-reference) |       | the recipient address on the destination chain |

### Params

Params defines the set of IBC transfer parameters. NOTE: To prevent a single token from being transferred, set the TransfersEnabled parameter to true and then set the bank module's SendEnabled parameter for the denomination to false.

| Field             | Type                     | Label | Description                                                                         |
| ----------------- | ------------------------ | ----- | ----------------------------------------------------------------------------------- |
| `send_enabled`    | [bool](broken-reference) |       | send\_enabled enables or disables all cross-chain token transfers from this chain.  |
| `receive_enabled` | [bool](broken-reference) |       | receive\_enabled enables or disables all cross-chain token transfers to this chain. |

## ibc/applications/transfer/v1/genesis.proto

### GenesisState

GenesisState defines the ibc-transfer genesis state

| Field          | Type                           | Label    | Description |
| -------------- | ------------------------------ | -------- | ----------- |
| `port_id`      | [string](broken-reference)     |          |             |
| `denom_traces` | [DenomTrace](broken-reference) | repeated |             |
| `params`       | [Params](broken-reference)     |          |             |

## ibc/applications/transfer/v1/query.proto

### QueryDenomTraceRequest

QueryDenomTraceRequest is the request type for the Query/DenomTrace RPC method

| Field  | Type                       | Label | Description                                                 |
| ------ | -------------------------- | ----- | ----------------------------------------------------------- |
| `hash` | [string](broken-reference) |       | hash (in hex format) of the denomination trace information. |

### QueryDenomTraceResponse

QueryDenomTraceResponse is the response type for the Query/DenomTrace RPC method.

| Field         | Type                           | Label | Description                                                        |
| ------------- | ------------------------------ | ----- | ------------------------------------------------------------------ |
| `denom_trace` | [DenomTrace](broken-reference) |       | denom\_trace returns the requested denomination trace information. |

### QueryDenomTracesRequest

QueryConnectionsRequest is the request type for the Query/DenomTraces RPC method

| Field        | Type                                                      | Label | Description                                                |
| ------------ | --------------------------------------------------------- | ----- | ---------------------------------------------------------- |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request. |

### QueryDenomTracesResponse

QueryConnectionsResponse is the response type for the Query/DenomTraces RPC method.

| Field          | Type                                                       | Label    | Description                                                |
| -------------- | ---------------------------------------------------------- | -------- | ---------------------------------------------------------- |
| `denom_traces` | [DenomTrace](broken-reference)                             | repeated | denom\_traces returns all denominations trace information. |
| `pagination`   | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response.         |

### QueryParamsRequest

QueryParamsRequest is the request type for the Query/Params RPC method.

### QueryParamsResponse

QueryParamsResponse is the response type for the Query/Params RPC method.

| Field    | Type                       | Label | Description                                  |
| -------- | -------------------------- | ----- | -------------------------------------------- |
| `params` | [Params](broken-reference) |       | params defines the parameters of the module. |

### Query

Query provides defines the gRPC querier service.

| Method Name   | Request Type                                | Response Type                                | Description                                               | HTTP Verb | Endpoint                                                |
| ------------- | ------------------------------------------- | -------------------------------------------- | --------------------------------------------------------- | --------- | ------------------------------------------------------- |
| `DenomTrace`  | [QueryDenomTraceRequest](broken-reference)  | [QueryDenomTraceResponse](broken-reference)  | DenomTrace queries a denomination trace information.      | GET       | /ibc/applications/transfer/v1beta1/denom\_traces/{hash} |
| `DenomTraces` | [QueryDenomTracesRequest](broken-reference) | [QueryDenomTracesResponse](broken-reference) | DenomTraces queries all denomination traces.              | GET       | /ibc/applications/transfer/v1beta1/denom\_traces        |
| `Params`      | [QueryParamsRequest](broken-reference)      | [QueryParamsResponse](broken-reference)      | Params queries all parameters of the ibc-transfer module. | GET       | /ibc/applications/transfer/v1beta1/params               |

## ibc/core/client/v1/client.proto

### ClientConsensusStates

ClientConsensusStates defines all the stored consensus states for a given client.

| Field              | Type                                         | Label    | Description                                                   |
| ------------------ | -------------------------------------------- | -------- | ------------------------------------------------------------- |
| `client_id`        | [string](broken-reference)                   |          | client identifier                                             |
| `consensus_states` | [ConsensusStateWithHeight](broken-reference) | repeated | consensus states and their heights associated with the client |

### ClientUpdateProposal

ClientUpdateProposal is a governance proposal. If it passes, the client is updated with the provided header. The update may fail if the header is not valid given certain conditions specified by the client implementation.

| Field         | Type                                    | Label | Description                                                               |
| ------------- | --------------------------------------- | ----- | ------------------------------------------------------------------------- |
| `title`       | [string](broken-reference)              |       | the title of the update proposal                                          |
| `description` | [string](broken-reference)              |       | the description of the proposal                                           |
| `client_id`   | [string](broken-reference)              |       | the client identifier for the client to be updated if the proposal passes |
| `header`      | [google.protobuf.Any](broken-reference) |       | the header used to update the client if the proposal passes               |

### ConsensusStateWithHeight

ConsensusStateWithHeight defines a consensus state with an additional height field.

| Field             | Type                                    | Label | Description            |
| ----------------- | --------------------------------------- | ----- | ---------------------- |
| `height`          | [Height](broken-reference)              |       | consensus state height |
| `consensus_state` | [google.protobuf.Any](broken-reference) |       | consensus state        |

### Height

Height is a monotonically increasing data type that can be compared against another Height for the purposes of updating and freezing clients

Normally the RevisionHeight is incremented at each height while keeping RevisionNumber the same. However some consensus algorithms may choose to reset the height in certain conditions e.g. hard forks, state-machine breaking changes In these cases, the RevisionNumber is incremented so that height continues to be monitonically increasing even as the RevisionHeight gets reset

| Field             | Type                       | Label | Description                                  |
| ----------------- | -------------------------- | ----- | -------------------------------------------- |
| `revision_number` | [uint64](broken-reference) |       | the revision that the client is currently on |
| `revision_height` | [uint64](broken-reference) |       | the height within the given revision         |

### IdentifiedClientState

IdentifiedClientState defines a client state with an additional client identifier field.

| Field          | Type                                    | Label | Description       |
| -------------- | --------------------------------------- | ----- | ----------------- |
| `client_id`    | [string](broken-reference)              |       | client identifier |
| `client_state` | [google.protobuf.Any](broken-reference) |       | client state      |

### Params

Params defines the set of IBC light client parameters.

| Field             | Type                       | Label    | Description                                                      |
| ----------------- | -------------------------- | -------- | ---------------------------------------------------------------- |
| `allowed_clients` | [string](broken-reference) | repeated | allowed\_clients defines the list of allowed client state types. |

## ibc/applications/transfer/v1/tx.proto

### MsgTransfer

MsgTransfer defines a msg to transfer fungible tokens (i.e Coins) between ICS20 enabled chains. See ICS Spec here: https://github.com/cosmos/ics/tree/master/spec/ics-020-fungible-token-transfer#data-structures

| Field               | Type                                          | Label | Description                                                                                                        |
| ------------------- | --------------------------------------------- | ----- | ------------------------------------------------------------------------------------------------------------------ |
| `source_port`       | [string](broken-reference)                    |       | the port on which the packet will be sent                                                                          |
| `source_channel`    | [string](broken-reference)                    |       | the channel by which the packet will be sent                                                                       |
| `token`             | [cosmos.base.v1beta1.Coin](broken-reference)  |       | the tokens to be transferred                                                                                       |
| `sender`            | [string](broken-reference)                    |       | the sender address                                                                                                 |
| `receiver`          | [string](broken-reference)                    |       | the recipient address on the destination chain                                                                     |
| `timeout_height`    | [ibc.core.client.v1.Height](broken-reference) |       | Timeout height relative to the current block height. The timeout is disabled when set to 0.                        |
| `timeout_timestamp` | [uint64](broken-reference)                    |       | Timeout timestamp (in nanoseconds) relative to the current block timestamp. The timeout is disabled when set to 0. |

### MsgTransferResponse

MsgTransferResponse defines the Msg/Transfer response type.

### Msg

Msg defines the ibc/transfer Msg service.

| Method Name | Request Type                    | Response Type                           | Description                                            | HTTP Verb | Endpoint |
| ----------- | ------------------------------- | --------------------------------------- | ------------------------------------------------------ | --------- | -------- |
| `Transfer`  | [MsgTransfer](broken-reference) | [MsgTransferResponse](broken-reference) | Transfer defines a rpc handler method for MsgTransfer. |           |          |

## ibc/core/channel/v1/channel.proto

### Acknowledgement

Acknowledgement is the recommended acknowledgement format to be used by app-specific protocols. NOTE: The field numbers 21 and 22 were explicitly chosen to avoid accidental conflicts with other protobuf message formats used for acknowledgements. The first byte of any message with this format will be the non-ASCII values `0xaa` (result) or `0xb2` (error). Implemented as defined by ICS: https://github.com/cosmos/ics/tree/master/spec/ics-004-channel-and-packet-semantics#acknowledgement-envelope

| Field    | Type                       | Label | Description |
| -------- | -------------------------- | ----- | ----------- |
| `result` | [bytes](broken-reference)  |       |             |
| `error`  | [string](broken-reference) |       |             |

### Channel

Channel defines pipeline for exactly-once packet delivery between specific modules on separate blockchains, which has at least one end capable of sending packets and one end capable of receiving packets.

| Field             | Type                             | Label    | Description                                                                                    |
| ----------------- | -------------------------------- | -------- | ---------------------------------------------------------------------------------------------- |
| `state`           | [State](broken-reference)        |          | current state of the channel end                                                               |
| `ordering`        | [Order](broken-reference)        |          | whether the channel is ordered or unordered                                                    |
| `counterparty`    | [Counterparty](broken-reference) |          | counterparty channel end                                                                       |
| `connection_hops` | [string](broken-reference)       | repeated | list of connection identifiers, in order, along which packets sent on this channel will travel |
| `version`         | [string](broken-reference)       |          | opaque channel version, which is agreed upon during the handshake                              |

### Counterparty

Counterparty defines a channel end counterparty

| Field        | Type                       | Label | Description                                                             |
| ------------ | -------------------------- | ----- | ----------------------------------------------------------------------- |
| `port_id`    | [string](broken-reference) |       | port on the counterparty chain which owns the other end of the channel. |
| `channel_id` | [string](broken-reference) |       | channel end on the counterparty chain                                   |

### IdentifiedChannel

IdentifiedChannel defines a channel with additional port and channel identifier fields.

| Field             | Type                             | Label    | Description                                                                                    |
| ----------------- | -------------------------------- | -------- | ---------------------------------------------------------------------------------------------- |
| `state`           | [State](broken-reference)        |          | current state of the channel end                                                               |
| `ordering`        | [Order](broken-reference)        |          | whether the channel is ordered or unordered                                                    |
| `counterparty`    | [Counterparty](broken-reference) |          | counterparty channel end                                                                       |
| `connection_hops` | [string](broken-reference)       | repeated | list of connection identifiers, in order, along which packets sent on this channel will travel |
| `version`         | [string](broken-reference)       |          | opaque channel version, which is agreed upon during the handshake                              |
| `port_id`         | [string](broken-reference)       |          | port identifier                                                                                |
| `channel_id`      | [string](broken-reference)       |          | channel identifier                                                                             |

### Packet

Packet defines a type that carries data across different chains through IBC

| Field                 | Type                                          | Label | Description                                                                                                                                                                   |
| --------------------- | --------------------------------------------- | ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `sequence`            | [uint64](broken-reference)                    |       | number corresponds to the order of sends and receives, where a Packet with an earlier sequence number must be sent and received before a Packet with a later sequence number. |
| `source_port`         | [string](broken-reference)                    |       | identifies the port on the sending chain.                                                                                                                                     |
| `source_channel`      | [string](broken-reference)                    |       | identifies the channel end on the sending chain.                                                                                                                              |
| `destination_port`    | [string](broken-reference)                    |       | identifies the port on the receiving chain.                                                                                                                                   |
| `destination_channel` | [string](broken-reference)                    |       | identifies the channel end on the receiving chain.                                                                                                                            |
| `data`                | [bytes](broken-reference)                     |       | actual opaque bytes transferred directly to the application module                                                                                                            |
| `timeout_height`      | [ibc.core.client.v1.Height](broken-reference) |       | block height after which the packet times out                                                                                                                                 |
| `timeout_timestamp`   | [uint64](broken-reference)                    |       | block timestamp (in nanoseconds) after which the packet times out                                                                                                             |

### PacketState

PacketState defines the generic type necessary to retrieve and store packet commitments, acknowledgements, and receipts. Caller is responsible for knowing the context necessary to interpret this state as a commitment, acknowledgement, or a receipt.

| Field        | Type                       | Label | Description                                 |
| ------------ | -------------------------- | ----- | ------------------------------------------- |
| `port_id`    | [string](broken-reference) |       | channel port identifier.                    |
| `channel_id` | [string](broken-reference) |       | channel unique identifier.                  |
| `sequence`   | [uint64](broken-reference) |       | packet sequence.                            |
| `data`       | [bytes](broken-reference)  |       | embedded data that represents packet state. |

### Order

Order defines if a channel is ORDERED or UNORDERED

| Name                     | Number | Description                                                                                     |
| ------------------------ | ------ | ----------------------------------------------------------------------------------------------- |
| ORDER\_NONE\_UNSPECIFIED | 0      | zero-value for channel ordering                                                                 |
| ORDER\_UNORDERED         | 1      | packets can be delivered in any order, which may differ from the order in which they were sent. |
| ORDER\_ORDERED           | 2      | packets are delivered exactly in the order which they were sent                                 |

### State

State defines if a channel is in one of the following states: CLOSED, INIT, TRYOPEN, OPEN or UNINITIALIZED.

| Name                              | Number | Description                                                                                 |
| --------------------------------- | ------ | ------------------------------------------------------------------------------------------- |
| STATE\_UNINITIALIZED\_UNSPECIFIED | 0      | Default State                                                                               |
| STATE\_INIT                       | 1      | A channel has just started the opening handshake.                                           |
| STATE\_TRYOPEN                    | 2      | A channel has acknowledged the handshake step on the counterparty chain.                    |
| STATE\_OPEN                       | 3      | A channel has completed the handshake. Open channels are ready to send and receive packets. |
| STATE\_CLOSED                     | 4      | A channel has been closed and can no longer be used to send or receive packets.             |

## ibc/core/channel/v1/genesis.proto

### GenesisState

GenesisState defines the ibc channel submodule's genesis state.

| Field                   | Type                                  | Label    | Description                                            |
| ----------------------- | ------------------------------------- | -------- | ------------------------------------------------------ |
| `channels`              | [IdentifiedChannel](broken-reference) | repeated |                                                        |
| `acknowledgements`      | [PacketState](broken-reference)       | repeated |                                                        |
| `commitments`           | [PacketState](broken-reference)       | repeated |                                                        |
| `receipts`              | [PacketState](broken-reference)       | repeated |                                                        |
| `send_sequences`        | [PacketSequence](broken-reference)    | repeated |                                                        |
| `recv_sequences`        | [PacketSequence](broken-reference)    | repeated |                                                        |
| `ack_sequences`         | [PacketSequence](broken-reference)    | repeated |                                                        |
| `next_channel_sequence` | [uint64](broken-reference)            |          | the sequence for the next generated channel identifier |

### PacketSequence

PacketSequence defines the genesis type necessary to retrieve and store next send and receive sequences.

| Field        | Type                       | Label | Description |
| ------------ | -------------------------- | ----- | ----------- |
| `port_id`    | [string](broken-reference) |       |             |
| `channel_id` | [string](broken-reference) |       |             |
| `sequence`   | [uint64](broken-reference) |       |             |

## ibc/core/channel/v1/query.proto

### QueryChannelClientStateRequest

QueryChannelClientStateRequest is the request type for the Query/ClientState RPC method

| Field        | Type                       | Label | Description               |
| ------------ | -------------------------- | ----- | ------------------------- |
| `port_id`    | [string](broken-reference) |       | port unique identifier    |
| `channel_id` | [string](broken-reference) |       | channel unique identifier |

### QueryChannelClientStateResponse

QueryChannelClientStateResponse is the Response type for the Query/QueryChannelClientState RPC method

| Field                     | Type                                                         | Label | Description                              |
| ------------------------- | ------------------------------------------------------------ | ----- | ---------------------------------------- |
| `identified_client_state` | [ibc.core.client.v1.IdentifiedClientState](broken-reference) |       | client state associated with the channel |
| `proof`                   | [bytes](broken-reference)                                    |       | merkle proof of existence                |
| `proof_height`            | [ibc.core.client.v1.Height](broken-reference)                |       | height at which the proof was retrieved  |

### QueryChannelConsensusStateRequest

QueryChannelConsensusStateRequest is the request type for the Query/ConsensusState RPC method

| Field             | Type                       | Label | Description                            |
| ----------------- | -------------------------- | ----- | -------------------------------------- |
| `port_id`         | [string](broken-reference) |       | port unique identifier                 |
| `channel_id`      | [string](broken-reference) |       | channel unique identifier              |
| `revision_number` | [uint64](broken-reference) |       | revision number of the consensus state |
| `revision_height` | [uint64](broken-reference) |       | revision height of the consensus state |

### QueryChannelConsensusStateResponse

QueryChannelClientStateResponse is the Response type for the Query/QueryChannelClientState RPC method

| Field             | Type                                          | Label | Description                                   |
| ----------------- | --------------------------------------------- | ----- | --------------------------------------------- |
| `consensus_state` | [google.protobuf.Any](broken-reference)       |       | consensus state associated with the channel   |
| `client_id`       | [string](broken-reference)                    |       | client ID associated with the consensus state |
| `proof`           | [bytes](broken-reference)                     |       | merkle proof of existence                     |
| `proof_height`    | [ibc.core.client.v1.Height](broken-reference) |       | height at which the proof was retrieved       |

### QueryChannelRequest

QueryChannelRequest is the request type for the Query/Channel RPC method

| Field        | Type                       | Label | Description               |
| ------------ | -------------------------- | ----- | ------------------------- |
| `port_id`    | [string](broken-reference) |       | port unique identifier    |
| `channel_id` | [string](broken-reference) |       | channel unique identifier |

### QueryChannelResponse

QueryChannelResponse is the response type for the Query/Channel RPC method. Besides the Channel end, it includes a proof and the height from which the proof was retrieved.

| Field          | Type                                          | Label | Description                                     |
| -------------- | --------------------------------------------- | ----- | ----------------------------------------------- |
| `channel`      | [Channel](broken-reference)                   |       | channel associated with the request identifiers |
| `proof`        | [bytes](broken-reference)                     |       | merkle proof of existence                       |
| `proof_height` | [ibc.core.client.v1.Height](broken-reference) |       | height at which the proof was retrieved         |

### QueryChannelsRequest

QueryChannelsRequest is the request type for the Query/Channels RPC method

| Field        | Type                                                      | Label | Description        |
| ------------ | --------------------------------------------------------- | ----- | ------------------ |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination request |

### QueryChannelsResponse

QueryChannelsResponse is the response type for the Query/Channels RPC method.

| Field        | Type                                                       | Label    | Description                           |
| ------------ | ---------------------------------------------------------- | -------- | ------------------------------------- |
| `channels`   | [IdentifiedChannel](broken-reference)                      | repeated | list of stored channels of the chain. |
| `pagination` | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination response                   |
| `height`     | [ibc.core.client.v1.Height](broken-reference)              |          | query block height                    |

### QueryConnectionChannelsRequest

QueryConnectionChannelsRequest is the request type for the Query/QueryConnectionChannels RPC method

| Field        | Type                                                      | Label | Description                  |
| ------------ | --------------------------------------------------------- | ----- | ---------------------------- |
| `connection` | [string](broken-reference)                                |       | connection unique identifier |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination request           |

### QueryConnectionChannelsResponse

QueryConnectionChannelsResponse is the Response type for the Query/QueryConnectionChannels RPC method

| Field        | Type                                                       | Label    | Description                                    |
| ------------ | ---------------------------------------------------------- | -------- | ---------------------------------------------- |
| `channels`   | [IdentifiedChannel](broken-reference)                      | repeated | list of channels associated with a connection. |
| `pagination` | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination response                            |
| `height`     | [ibc.core.client.v1.Height](broken-reference)              |          | query block height                             |

### QueryNextSequenceReceiveRequest

QueryNextSequenceReceiveRequest is the request type for the Query/QueryNextSequenceReceiveRequest RPC method

| Field        | Type                       | Label | Description               |
| ------------ | -------------------------- | ----- | ------------------------- |
| `port_id`    | [string](broken-reference) |       | port unique identifier    |
| `channel_id` | [string](broken-reference) |       | channel unique identifier |

### QueryNextSequenceReceiveResponse

QuerySequenceResponse is the request type for the Query/QueryNextSequenceReceiveResponse RPC method

| Field                   | Type                                          | Label | Description                             |
| ----------------------- | --------------------------------------------- | ----- | --------------------------------------- |
| `next_sequence_receive` | [uint64](broken-reference)                    |       | next sequence receive number            |
| `proof`                 | [bytes](broken-reference)                     |       | merkle proof of existence               |
| `proof_height`          | [ibc.core.client.v1.Height](broken-reference) |       | height at which the proof was retrieved |

### QueryPacketAcknowledgementRequest

QueryPacketAcknowledgementRequest is the request type for the Query/PacketAcknowledgement RPC method

| Field        | Type                       | Label | Description               |
| ------------ | -------------------------- | ----- | ------------------------- |
| `port_id`    | [string](broken-reference) |       | port unique identifier    |
| `channel_id` | [string](broken-reference) |       | channel unique identifier |
| `sequence`   | [uint64](broken-reference) |       | packet sequence           |

### QueryPacketAcknowledgementResponse

QueryPacketAcknowledgementResponse defines the client query response for a packet which also includes a proof and the height from which the proof was retrieved

| Field             | Type                                          | Label | Description                               |
| ----------------- | --------------------------------------------- | ----- | ----------------------------------------- |
| `acknowledgement` | [bytes](broken-reference)                     |       | packet associated with the request fields |
| `proof`           | [bytes](broken-reference)                     |       | merkle proof of existence                 |
| `proof_height`    | [ibc.core.client.v1.Height](broken-reference) |       | height at which the proof was retrieved   |

### QueryPacketAcknowledgementsRequest

QueryPacketAcknowledgementsRequest is the request type for the Query/QueryPacketCommitments RPC method

| Field        | Type                                                      | Label | Description               |
| ------------ | --------------------------------------------------------- | ----- | ------------------------- |
| `port_id`    | [string](broken-reference)                                |       | port unique identifier    |
| `channel_id` | [string](broken-reference)                                |       | channel unique identifier |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination request        |

### QueryPacketAcknowledgementsResponse

QueryPacketAcknowledgemetsResponse is the request type for the Query/QueryPacketAcknowledgements RPC method

| Field              | Type                                                       | Label    | Description         |
| ------------------ | ---------------------------------------------------------- | -------- | ------------------- |
| `acknowledgements` | [PacketState](broken-reference)                            | repeated |                     |
| `pagination`       | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination response |
| `height`           | [ibc.core.client.v1.Height](broken-reference)              |          | query block height  |

### QueryPacketCommitmentRequest

QueryPacketCommitmentRequest is the request type for the Query/PacketCommitment RPC method

| Field        | Type                       | Label | Description               |
| ------------ | -------------------------- | ----- | ------------------------- |
| `port_id`    | [string](broken-reference) |       | port unique identifier    |
| `channel_id` | [string](broken-reference) |       | channel unique identifier |
| `sequence`   | [uint64](broken-reference) |       | packet sequence           |

### QueryPacketCommitmentResponse

QueryPacketCommitmentResponse defines the client query response for a packet which also includes a proof and the height from which the proof was retrieved

| Field          | Type                                          | Label | Description                               |
| -------------- | --------------------------------------------- | ----- | ----------------------------------------- |
| `commitment`   | [bytes](broken-reference)                     |       | packet associated with the request fields |
| `proof`        | [bytes](broken-reference)                     |       | merkle proof of existence                 |
| `proof_height` | [ibc.core.client.v1.Height](broken-reference) |       | height at which the proof was retrieved   |

### QueryPacketCommitmentsRequest

QueryPacketCommitmentsRequest is the request type for the Query/QueryPacketCommitments RPC method

| Field        | Type                                                      | Label | Description               |
| ------------ | --------------------------------------------------------- | ----- | ------------------------- |
| `port_id`    | [string](broken-reference)                                |       | port unique identifier    |
| `channel_id` | [string](broken-reference)                                |       | channel unique identifier |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination request        |

### QueryPacketCommitmentsResponse

QueryPacketCommitmentsResponse is the request type for the Query/QueryPacketCommitments RPC method

| Field         | Type                                                       | Label    | Description         |
| ------------- | ---------------------------------------------------------- | -------- | ------------------- |
| `commitments` | [PacketState](broken-reference)                            | repeated |                     |
| `pagination`  | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination response |
| `height`      | [ibc.core.client.v1.Height](broken-reference)              |          | query block height  |

### QueryPacketReceiptRequest

QueryPacketReceiptRequest is the request type for the Query/PacketReceipt RPC method

| Field        | Type                       | Label | Description               |
| ------------ | -------------------------- | ----- | ------------------------- |
| `port_id`    | [string](broken-reference) |       | port unique identifier    |
| `channel_id` | [string](broken-reference) |       | channel unique identifier |
| `sequence`   | [uint64](broken-reference) |       | packet sequence           |

### QueryPacketReceiptResponse

QueryPacketReceiptResponse defines the client query response for a packet receipt which also includes a proof, and the height from which the proof was retrieved

| Field          | Type                                          | Label | Description                             |
| -------------- | --------------------------------------------- | ----- | --------------------------------------- |
| `received`     | [bool](broken-reference)                      |       | success flag for if receipt exists      |
| `proof`        | [bytes](broken-reference)                     |       | merkle proof of existence               |
| `proof_height` | [ibc.core.client.v1.Height](broken-reference) |       | height at which the proof was retrieved |

### QueryUnreceivedAcksRequest

QueryUnreceivedAcks is the request type for the Query/UnreceivedAcks RPC method

| Field                  | Type                       | Label    | Description                       |
| ---------------------- | -------------------------- | -------- | --------------------------------- |
| `port_id`              | [string](broken-reference) |          | port unique identifier            |
| `channel_id`           | [string](broken-reference) |          | channel unique identifier         |
| `packet_ack_sequences` | [uint64](broken-reference) | repeated | list of acknowledgement sequences |

### QueryUnreceivedAcksResponse

QueryUnreceivedAcksResponse is the response type for the Query/UnreceivedAcks RPC method

| Field       | Type                                          | Label    | Description                                  |
| ----------- | --------------------------------------------- | -------- | -------------------------------------------- |
| `sequences` | [uint64](broken-reference)                    | repeated | list of unreceived acknowledgement sequences |
| `height`    | [ibc.core.client.v1.Height](broken-reference) |          | query block height                           |

### QueryUnreceivedPacketsRequest

QueryUnreceivedPacketsRequest is the request type for the Query/UnreceivedPackets RPC method

| Field                         | Type                       | Label    | Description               |
| ----------------------------- | -------------------------- | -------- | ------------------------- |
| `port_id`                     | [string](broken-reference) |          | port unique identifier    |
| `channel_id`                  | [string](broken-reference) |          | channel unique identifier |
| `packet_commitment_sequences` | [uint64](broken-reference) | repeated | list of packet sequences  |

### QueryUnreceivedPacketsResponse

QueryUnreceivedPacketsResponse is the response type for the Query/UnreceivedPacketCommitments RPC method

| Field       | Type                                          | Label    | Description                         |
| ----------- | --------------------------------------------- | -------- | ----------------------------------- |
| `sequences` | [uint64](broken-reference)                    | repeated | list of unreceived packet sequences |
| `height`    | [ibc.core.client.v1.Height](broken-reference) |          | query block height                  |

### Query

Query provides defines the gRPC querier service

| Method Name              | Request Type                                           | Response Type                                           | Description                                                                                                             | HTTP Verb | Endpoint                                                                                                                                  |
| ------------------------ | ------------------------------------------------------ | ------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `Channel`                | [QueryChannelRequest](broken-reference)                | [QueryChannelResponse](broken-reference)                | Channel queries an IBC Channel.                                                                                         | GET       | /ibc/core/channel/v1beta1/channels/{channel\_id}/ports/{port\_id}                                                                         |
| `Channels`               | [QueryChannelsRequest](broken-reference)               | [QueryChannelsResponse](broken-reference)               | Channels queries all the IBC channels of a chain.                                                                       | GET       | /ibc/core/channel/v1beta1/channels                                                                                                        |
| `ConnectionChannels`     | [QueryConnectionChannelsRequest](broken-reference)     | [QueryConnectionChannelsResponse](broken-reference)     | ConnectionChannels queries all the channels associated with a connection end.                                           | GET       | /ibc/core/channel/v1beta1/connections/{connection}/channels                                                                               |
| `ChannelClientState`     | [QueryChannelClientStateRequest](broken-reference)     | [QueryChannelClientStateResponse](broken-reference)     | ChannelClientState queries for the client state for the channel associated with the provided channel identifiers.       | GET       | /ibc/core/channel/v1beta1/channels/{channel\_id}/ports/{port\_id}/client\_state                                                           |
| `ChannelConsensusState`  | [QueryChannelConsensusStateRequest](broken-reference)  | [QueryChannelConsensusStateResponse](broken-reference)  | ChannelConsensusState queries for the consensus state for the channel associated with the provided channel identifiers. | GET       | /ibc/core/channel/v1beta1/channels/{channel\_id}/ports/{port\_id}/consensus\_state/revision/{revision\_number}/height/{revision\_height}  |
| `PacketCommitment`       | [QueryPacketCommitmentRequest](broken-reference)       | [QueryPacketCommitmentResponse](broken-reference)       | PacketCommitment queries a stored packet commitment hash.                                                               | GET       | /ibc/core/channel/v1beta1/channels/{channel\_id}/ports/{port\_id}/packet\_commitments/{sequence}                                          |
| `PacketCommitments`      | [QueryPacketCommitmentsRequest](broken-reference)      | [QueryPacketCommitmentsResponse](broken-reference)      | PacketCommitments returns all the packet commitments hashes associated with a channel.                                  | GET       | /ibc/core/channel/v1beta1/channels/{channel\_id}/ports/{port\_id}/packet\_commitments                                                     |
| `PacketReceipt`          | [QueryPacketReceiptRequest](broken-reference)          | [QueryPacketReceiptResponse](broken-reference)          | PacketReceipt queries if a given packet sequence has been received on the queried chain                                 | GET       | /ibc/core/channel/v1beta1/channels/{channel\_id}/ports/{port\_id}/packet\_receipts/{sequence}                                             |
| `PacketAcknowledgement`  | [QueryPacketAcknowledgementRequest](broken-reference)  | [QueryPacketAcknowledgementResponse](broken-reference)  | PacketAcknowledgement queries a stored packet acknowledgement hash.                                                     | GET       | /ibc/core/channel/v1beta1/channels/{channel\_id}/ports/{port\_id}/packet\_acks/{sequence}                                                 |
| `PacketAcknowledgements` | [QueryPacketAcknowledgementsRequest](broken-reference) | [QueryPacketAcknowledgementsResponse](broken-reference) | PacketAcknowledgements returns all the packet acknowledgements associated with a channel.                               | GET       | /ibc/core/channel/v1beta1/channels/{channel\_id}/ports/{port\_id}/packet\_acknowledgements                                                |
| `UnreceivedPackets`      | [QueryUnreceivedPacketsRequest](broken-reference)      | [QueryUnreceivedPacketsResponse](broken-reference)      | UnreceivedPackets returns all the unreceived IBC packets associated with a channel and sequences.                       | GET       | /ibc/core/channel/v1beta1/channels/{channel\_id}/ports/{port\_id}/packet\_commitments/{packet\_commitment\_sequences}/unreceived\_packets |
| `UnreceivedAcks`         | [QueryUnreceivedAcksRequest](broken-reference)         | [QueryUnreceivedAcksResponse](broken-reference)         | UnreceivedAcks returns all the unreceived IBC acknowledgements associated with a channel and sequences.                 | GET       | /ibc/core/channel/v1beta1/channels/{channel\_id}/ports/{port\_id}/packet\_commitments/{packet\_ack\_sequences}/unreceived\_acks           |
| `NextSequenceReceive`    | [QueryNextSequenceReceiveRequest](broken-reference)    | [QueryNextSequenceReceiveResponse](broken-reference)    | NextSequenceReceive returns the next receive sequence for a given channel.                                              | GET       | /ibc/core/channel/v1beta1/channels/{channel\_id}/ports/{port\_id}/next\_sequence                                                          |

## ibc/core/channel/v1/tx.proto

### MsgAcknowledgement

MsgAcknowledgement receives incoming IBC acknowledgement

| Field             | Type                                          | Label | Description |
| ----------------- | --------------------------------------------- | ----- | ----------- |
| `packet`          | [Packet](broken-reference)                    |       |             |
| `acknowledgement` | [bytes](broken-reference)                     |       |             |
| `proof_acked`     | [bytes](broken-reference)                     |       |             |
| `proof_height`    | [ibc.core.client.v1.Height](broken-reference) |       |             |
| `signer`          | [string](broken-reference)                    |       |             |

### MsgAcknowledgementResponse

MsgAcknowledgementResponse defines the Msg/Acknowledgement response type.

### MsgChannelCloseConfirm

MsgChannelCloseConfirm defines a msg sent by a Relayer to Chain B to acknowledge the change of channel state to CLOSED on Chain A.

| Field          | Type                                          | Label | Description |
| -------------- | --------------------------------------------- | ----- | ----------- |
| `port_id`      | [string](broken-reference)                    |       |             |
| `channel_id`   | [string](broken-reference)                    |       |             |
| `proof_init`   | [bytes](broken-reference)                     |       |             |
| `proof_height` | [ibc.core.client.v1.Height](broken-reference) |       |             |
| `signer`       | [string](broken-reference)                    |       |             |

### MsgChannelCloseConfirmResponse

MsgChannelCloseConfirmResponse defines the Msg/ChannelCloseConfirm response type.

### MsgChannelCloseInit

MsgChannelCloseInit defines a msg sent by a Relayer to Chain A to close a channel with Chain B.

| Field        | Type                       | Label | Description |
| ------------ | -------------------------- | ----- | ----------- |
| `port_id`    | [string](broken-reference) |       |             |
| `channel_id` | [string](broken-reference) |       |             |
| `signer`     | [string](broken-reference) |       |             |

### MsgChannelCloseInitResponse

MsgChannelCloseInitResponse defines the Msg/ChannelCloseInit response type.

### MsgChannelOpenAck

MsgChannelOpenAck defines a msg sent by a Relayer to Chain A to acknowledge the change of channel state to TRYOPEN on Chain B.

| Field                     | Type                                          | Label | Description |
| ------------------------- | --------------------------------------------- | ----- | ----------- |
| `port_id`                 | [string](broken-reference)                    |       |             |
| `channel_id`              | [string](broken-reference)                    |       |             |
| `counterparty_channel_id` | [string](broken-reference)                    |       |             |
| `counterparty_version`    | [string](broken-reference)                    |       |             |
| `proof_try`               | [bytes](broken-reference)                     |       |             |
| `proof_height`            | [ibc.core.client.v1.Height](broken-reference) |       |             |
| `signer`                  | [string](broken-reference)                    |       |             |

### MsgChannelOpenAckResponse

MsgChannelOpenAckResponse defines the Msg/ChannelOpenAck response type.

### MsgChannelOpenConfirm

MsgChannelOpenConfirm defines a msg sent by a Relayer to Chain B to acknowledge the change of channel state to OPEN on Chain A.

| Field          | Type                                          | Label | Description |
| -------------- | --------------------------------------------- | ----- | ----------- |
| `port_id`      | [string](broken-reference)                    |       |             |
| `channel_id`   | [string](broken-reference)                    |       |             |
| `proof_ack`    | [bytes](broken-reference)                     |       |             |
| `proof_height` | [ibc.core.client.v1.Height](broken-reference) |       |             |
| `signer`       | [string](broken-reference)                    |       |             |

### MsgChannelOpenConfirmResponse

MsgChannelOpenConfirmResponse defines the Msg/ChannelOpenConfirm response type.

### MsgChannelOpenInit

MsgChannelOpenInit defines an sdk.Msg to initialize a channel handshake. It is called by a relayer on Chain A.

| Field     | Type                        | Label | Description |
| --------- | --------------------------- | ----- | ----------- |
| `port_id` | [string](broken-reference)  |       |             |
| `channel` | [Channel](broken-reference) |       |             |
| `signer`  | [string](broken-reference)  |       |             |

### MsgChannelOpenInitResponse

MsgChannelOpenInitResponse defines the Msg/ChannelOpenInit response type.

### MsgChannelOpenTry

MsgChannelOpenInit defines a msg sent by a Relayer to try to open a channel on Chain B.

| Field                  | Type                                          | Label | Description                                                                                                                           |
| ---------------------- | --------------------------------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `port_id`              | [string](broken-reference)                    |       |                                                                                                                                       |
| `previous_channel_id`  | [string](broken-reference)                    |       | in the case of crossing hello's, when both chains call OpenInit, we need the channel identifier of the previous channel in state INIT |
| `channel`              | [Channel](broken-reference)                   |       |                                                                                                                                       |
| `counterparty_version` | [string](broken-reference)                    |       |                                                                                                                                       |
| `proof_init`           | [bytes](broken-reference)                     |       |                                                                                                                                       |
| `proof_height`         | [ibc.core.client.v1.Height](broken-reference) |       |                                                                                                                                       |
| `signer`               | [string](broken-reference)                    |       |                                                                                                                                       |

### MsgChannelOpenTryResponse

MsgChannelOpenTryResponse defines the Msg/ChannelOpenTry response type.

### MsgRecvPacket

MsgRecvPacket receives incoming IBC packet

| Field              | Type                                          | Label | Description |
| ------------------ | --------------------------------------------- | ----- | ----------- |
| `packet`           | [Packet](broken-reference)                    |       |             |
| `proof_commitment` | [bytes](broken-reference)                     |       |             |
| `proof_height`     | [ibc.core.client.v1.Height](broken-reference) |       |             |
| `signer`           | [string](broken-reference)                    |       |             |

### MsgRecvPacketResponse

MsgRecvPacketResponse defines the Msg/RecvPacket response type.

### MsgTimeout

MsgTimeout receives timed-out packet

| Field                | Type                                          | Label | Description |
| -------------------- | --------------------------------------------- | ----- | ----------- |
| `packet`             | [Packet](broken-reference)                    |       |             |
| `proof_unreceived`   | [bytes](broken-reference)                     |       |             |
| `proof_height`       | [ibc.core.client.v1.Height](broken-reference) |       |             |
| `next_sequence_recv` | [uint64](broken-reference)                    |       |             |
| `signer`             | [string](broken-reference)                    |       |             |

### MsgTimeoutOnClose

MsgTimeoutOnClose timed-out packet upon counterparty channel closure.

| Field                | Type                                          | Label | Description |
| -------------------- | --------------------------------------------- | ----- | ----------- |
| `packet`             | [Packet](broken-reference)                    |       |             |
| `proof_unreceived`   | [bytes](broken-reference)                     |       |             |
| `proof_close`        | [bytes](broken-reference)                     |       |             |
| `proof_height`       | [ibc.core.client.v1.Height](broken-reference) |       |             |
| `next_sequence_recv` | [uint64](broken-reference)                    |       |             |
| `signer`             | [string](broken-reference)                    |       |             |

### MsgTimeoutOnCloseResponse

MsgTimeoutOnCloseResponse defines the Msg/TimeoutOnClose response type.

### MsgTimeoutResponse

MsgTimeoutResponse defines the Msg/Timeout response type.

### Msg

Msg defines the ibc/channel Msg service.

| Method Name           | Request Type                               | Response Type                                      | Description                                                                  | HTTP Verb | Endpoint |
| --------------------- | ------------------------------------------ | -------------------------------------------------- | ---------------------------------------------------------------------------- | --------- | -------- |
| `ChannelOpenInit`     | [MsgChannelOpenInit](broken-reference)     | [MsgChannelOpenInitResponse](broken-reference)     | ChannelOpenInit defines a rpc handler method for MsgChannelOpenInit.         |           |          |
| `ChannelOpenTry`      | [MsgChannelOpenTry](broken-reference)      | [MsgChannelOpenTryResponse](broken-reference)      | ChannelOpenTry defines a rpc handler method for MsgChannelOpenTry.           |           |          |
| `ChannelOpenAck`      | [MsgChannelOpenAck](broken-reference)      | [MsgChannelOpenAckResponse](broken-reference)      | ChannelOpenAck defines a rpc handler method for MsgChannelOpenAck.           |           |          |
| `ChannelOpenConfirm`  | [MsgChannelOpenConfirm](broken-reference)  | [MsgChannelOpenConfirmResponse](broken-reference)  | ChannelOpenConfirm defines a rpc handler method for MsgChannelOpenConfirm.   |           |          |
| `ChannelCloseInit`    | [MsgChannelCloseInit](broken-reference)    | [MsgChannelCloseInitResponse](broken-reference)    | ChannelCloseInit defines a rpc handler method for MsgChannelCloseInit.       |           |          |
| `ChannelCloseConfirm` | [MsgChannelCloseConfirm](broken-reference) | [MsgChannelCloseConfirmResponse](broken-reference) | ChannelCloseConfirm defines a rpc handler method for MsgChannelCloseConfirm. |           |          |
| `RecvPacket`          | [MsgRecvPacket](broken-reference)          | [MsgRecvPacketResponse](broken-reference)          | RecvPacket defines a rpc handler method for MsgRecvPacket.                   |           |          |
| `Timeout`             | [MsgTimeout](broken-reference)             | [MsgTimeoutResponse](broken-reference)             | Timeout defines a rpc handler method for MsgTimeout.                         |           |          |
| `TimeoutOnClose`      | [MsgTimeoutOnClose](broken-reference)      | [MsgTimeoutOnCloseResponse](broken-reference)      | TimeoutOnClose defines a rpc handler method for MsgTimeoutOnClose.           |           |          |
| `Acknowledgement`     | [MsgAcknowledgement](broken-reference)     | [MsgAcknowledgementResponse](broken-reference)     | Acknowledgement defines a rpc handler method for MsgAcknowledgement.         |           |          |

## ibc/core/client/v1/genesis.proto

### GenesisMetadata

GenesisMetadata defines the genesis type for metadata that clients may return with ExportMetadata

| Field   | Type                      | Label | Description                                   |
| ------- | ------------------------- | ----- | --------------------------------------------- |
| `key`   | [bytes](broken-reference) |       | store key of metadata without clientID-prefix |
| `value` | [bytes](broken-reference) |       | metadata value                                |

### GenesisState

GenesisState defines the ibc client submodule's genesis state.

| Field                  | Type                                          | Label    | Description                                           |
| ---------------------- | --------------------------------------------- | -------- | ----------------------------------------------------- |
| `clients`              | [IdentifiedClientState](broken-reference)     | repeated | client states with their corresponding identifiers    |
| `clients_consensus`    | [ClientConsensusStates](broken-reference)     | repeated | consensus states from each client                     |
| `clients_metadata`     | [IdentifiedGenesisMetadata](broken-reference) | repeated | metadata from each client                             |
| `params`               | [Params](broken-reference)                    |          |                                                       |
| `create_localhost`     | [bool](broken-reference)                      |          | create localhost on initialization                    |
| `next_client_sequence` | [uint64](broken-reference)                    |          | the sequence for the next generated client identifier |

### IdentifiedGenesisMetadata

IdentifiedGenesisMetadata has the client metadata with the corresponding client id.

| Field             | Type                                | Label    | Description |
| ----------------- | ----------------------------------- | -------- | ----------- |
| `client_id`       | [string](broken-reference)          |          |             |
| `client_metadata` | [GenesisMetadata](broken-reference) | repeated |             |

## ibc/core/client/v1/query.proto

### QueryClientParamsRequest

QueryClientParamsRequest is the request type for the Query/ClientParams RPC method.

### QueryClientParamsResponse

QueryClientParamsResponse is the response type for the Query/ClientParams RPC method.

| Field    | Type                       | Label | Description                                  |
| -------- | -------------------------- | ----- | -------------------------------------------- |
| `params` | [Params](broken-reference) |       | params defines the parameters of the module. |

### QueryClientStateRequest

QueryClientStateRequest is the request type for the Query/ClientState RPC method

| Field       | Type                       | Label | Description                    |
| ----------- | -------------------------- | ----- | ------------------------------ |
| `client_id` | [string](broken-reference) |       | client state unique identifier |

### QueryClientStateResponse

QueryClientStateResponse is the response type for the Query/ClientState RPC method. Besides the client state, it includes a proof and the height from which the proof was retrieved.

| Field          | Type                                    | Label | Description                                         |
| -------------- | --------------------------------------- | ----- | --------------------------------------------------- |
| `client_state` | [google.protobuf.Any](broken-reference) |       | client state associated with the request identifier |
| `proof`        | [bytes](broken-reference)               |       | merkle proof of existence                           |
| `proof_height` | [Height](broken-reference)              |       | height at which the proof was retrieved             |

### QueryClientStatesRequest

QueryClientStatesRequest is the request type for the Query/ClientStates RPC method

| Field        | Type                                                      | Label | Description        |
| ------------ | --------------------------------------------------------- | ----- | ------------------ |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination request |

### QueryClientStatesResponse

QueryClientStatesResponse is the response type for the Query/ClientStates RPC method.

| Field           | Type                                                       | Label    | Description                               |
| --------------- | ---------------------------------------------------------- | -------- | ----------------------------------------- |
| `client_states` | [IdentifiedClientState](broken-reference)                  | repeated | list of stored ClientStates of the chain. |
| `pagination`    | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination response                       |

### QueryConsensusStateRequest

QueryConsensusStateRequest is the request type for the Query/ConsensusState RPC method. Besides the consensus state, it includes a proof and the height from which the proof was retrieved.

| Field             | Type                       | Label | Description                                                                             |
| ----------------- | -------------------------- | ----- | --------------------------------------------------------------------------------------- |
| `client_id`       | [string](broken-reference) |       | client identifier                                                                       |
| `revision_number` | [uint64](broken-reference) |       | consensus state revision number                                                         |
| `revision_height` | [uint64](broken-reference) |       | consensus state revision height                                                         |
| `latest_height`   | [bool](broken-reference)   |       | latest\_height overrrides the height field and queries the latest stored ConsensusState |

### QueryConsensusStateResponse

QueryConsensusStateResponse is the response type for the Query/ConsensusState RPC method

| Field             | Type                                    | Label | Description                                                               |
| ----------------- | --------------------------------------- | ----- | ------------------------------------------------------------------------- |
| `consensus_state` | [google.protobuf.Any](broken-reference) |       | consensus state associated with the client identifier at the given height |
| `proof`           | [bytes](broken-reference)               |       | merkle proof of existence                                                 |
| `proof_height`    | [Height](broken-reference)              |       | height at which the proof was retrieved                                   |

### QueryConsensusStatesRequest

QueryConsensusStatesRequest is the request type for the Query/ConsensusStates RPC method.

| Field        | Type                                                      | Label | Description        |
| ------------ | --------------------------------------------------------- | ----- | ------------------ |
| `client_id`  | [string](broken-reference)                                |       | client identifier  |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination request |

### QueryConsensusStatesResponse

QueryConsensusStatesResponse is the response type for the Query/ConsensusStates RPC method

| Field              | Type                                                       | Label    | Description                                     |
| ------------------ | ---------------------------------------------------------- | -------- | ----------------------------------------------- |
| `consensus_states` | [ConsensusStateWithHeight](broken-reference)               | repeated | consensus states associated with the identifier |
| `pagination`       | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination response                             |

### Query

Query provides defines the gRPC querier service

| Method Name       | Request Type                                    | Response Type                                    | Description                                                                                | HTTP Verb | Endpoint                                                                                                      |
| ----------------- | ----------------------------------------------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------ | --------- | ------------------------------------------------------------------------------------------------------------- |
| `ClientState`     | [QueryClientStateRequest](broken-reference)     | [QueryClientStateResponse](broken-reference)     | ClientState queries an IBC light client.                                                   | GET       | /ibc/core/client/v1beta1/client\_states/{client\_id}                                                          |
| `ClientStates`    | [QueryClientStatesRequest](broken-reference)    | [QueryClientStatesResponse](broken-reference)    | ClientStates queries all the IBC light clients of a chain.                                 | GET       | /ibc/core/client/v1beta1/client\_states                                                                       |
| `ConsensusState`  | [QueryConsensusStateRequest](broken-reference)  | [QueryConsensusStateResponse](broken-reference)  | ConsensusState queries a consensus state associated with a client state at a given height. | GET       | /ibc/core/client/v1beta1/consensus\_states/{client\_id}/revision/{revision\_number}/height/{revision\_height} |
| `ConsensusStates` | [QueryConsensusStatesRequest](broken-reference) | [QueryConsensusStatesResponse](broken-reference) | ConsensusStates queries all the consensus state associated with a given client.            | GET       | /ibc/core/client/v1beta1/consensus\_states/{client\_id}                                                       |
| `ClientParams`    | [QueryClientParamsRequest](broken-reference)    | [QueryClientParamsResponse](broken-reference)    | ClientParams queries all parameters of the ibc client.                                     | GET       | /ibc/client/v1beta1/params                                                                                    |

## ibc/core/client/v1/tx.proto

### MsgCreateClient

MsgCreateClient defines a message to create an IBC client

| Field             | Type                                    | Label | Description                                                                    |
| ----------------- | --------------------------------------- | ----- | ------------------------------------------------------------------------------ |
| `client_state`    | [google.protobuf.Any](broken-reference) |       | light client state                                                             |
| `consensus_state` | [google.protobuf.Any](broken-reference) |       | consensus state associated with the client that corresponds to a given height. |
| `signer`          | [string](broken-reference)              |       | signer address                                                                 |

### MsgCreateClientResponse

MsgCreateClientResponse defines the Msg/CreateClient response type.

### MsgSubmitMisbehaviour

MsgSubmitMisbehaviour defines an sdk.Msg type that submits Evidence for light client misbehaviour.

| Field          | Type                                    | Label | Description                                     |
| -------------- | --------------------------------------- | ----- | ----------------------------------------------- |
| `client_id`    | [string](broken-reference)              |       | client unique identifier                        |
| `misbehaviour` | [google.protobuf.Any](broken-reference) |       | misbehaviour used for freezing the light client |
| `signer`       | [string](broken-reference)              |       | signer address                                  |

### MsgSubmitMisbehaviourResponse

MsgSubmitMisbehaviourResponse defines the Msg/SubmitMisbehaviour response type.

### MsgUpdateClient

MsgUpdateClient defines an sdk.Msg to update a IBC client state using the given header.

| Field       | Type                                    | Label | Description                       |
| ----------- | --------------------------------------- | ----- | --------------------------------- |
| `client_id` | [string](broken-reference)              |       | client unique identifier          |
| `header`    | [google.protobuf.Any](broken-reference) |       | header to update the light client |
| `signer`    | [string](broken-reference)              |       | signer address                    |

### MsgUpdateClientResponse

MsgUpdateClientResponse defines the Msg/UpdateClient response type.

### MsgUpgradeClient

MsgUpgradeClient defines an sdk.Msg to upgrade an IBC client to a new client state

| Field                           | Type                                    | Label | Description                                                                                             |
| ------------------------------- | --------------------------------------- | ----- | ------------------------------------------------------------------------------------------------------- |
| `client_id`                     | [string](broken-reference)              |       | client unique identifier                                                                                |
| `client_state`                  | [google.protobuf.Any](broken-reference) |       | upgraded client state                                                                                   |
| `consensus_state`               | [google.protobuf.Any](broken-reference) |       | upgraded consensus state, only contains enough information to serve as a basis of trust in update logic |
| `proof_upgrade_client`          | [bytes](broken-reference)               |       | proof that old chain committed to new client                                                            |
| `proof_upgrade_consensus_state` | [bytes](broken-reference)               |       | proof that old chain committed to new consensus state                                                   |
| `signer`                        | [string](broken-reference)              |       | signer address                                                                                          |

### MsgUpgradeClientResponse

MsgUpgradeClientResponse defines the Msg/UpgradeClient response type.

### Msg

Msg defines the ibc/client Msg service.

| Method Name          | Request Type                              | Response Type                                     | Description                                                                | HTTP Verb | Endpoint |
| -------------------- | ----------------------------------------- | ------------------------------------------------- | -------------------------------------------------------------------------- | --------- | -------- |
| `CreateClient`       | [MsgCreateClient](broken-reference)       | [MsgCreateClientResponse](broken-reference)       | CreateClient defines a rpc handler method for MsgCreateClient.             |           |          |
| `UpdateClient`       | [MsgUpdateClient](broken-reference)       | [MsgUpdateClientResponse](broken-reference)       | UpdateClient defines a rpc handler method for MsgUpdateClient.             |           |          |
| `UpgradeClient`      | [MsgUpgradeClient](broken-reference)      | [MsgUpgradeClientResponse](broken-reference)      | UpgradeClient defines a rpc handler method for MsgUpgradeClient.           |           |          |
| `SubmitMisbehaviour` | [MsgSubmitMisbehaviour](broken-reference) | [MsgSubmitMisbehaviourResponse](broken-reference) | SubmitMisbehaviour defines a rpc handler method for MsgSubmitMisbehaviour. |           |          |

## ibc/core/commitment/v1/commitment.proto

### MerklePath

MerklePath is the path used to verify commitment proofs, which can be an arbitrary structured object (defined by a commitment type). MerklePath is represented from root-to-leaf

| Field      | Type                       | Label    | Description |
| ---------- | -------------------------- | -------- | ----------- |
| `key_path` | [string](broken-reference) | repeated |             |

### MerklePrefix

MerklePrefix is merkle path prefixed to the key. The constructed key from the Path and the key will be append(Path.KeyPath, append(Path.KeyPrefix, key...))

| Field        | Type                      | Label | Description |
| ------------ | ------------------------- | ----- | ----------- |
| `key_prefix` | [bytes](broken-reference) |       |             |

### MerkleProof

MerkleProof is a wrapper type over a chain of CommitmentProofs. It demonstrates membership or non-membership for an element or set of elements, verifiable in conjunction with a known commitment root. Proofs should be succinct. MerkleProofs are ordered from leaf-to-root

| Field    | Type                                      | Label    | Description |
| -------- | ----------------------------------------- | -------- | ----------- |
| `proofs` | [ics23.CommitmentProof](broken-reference) | repeated |             |

### MerkleRoot

MerkleRoot defines a merkle root hash. In the Cosmos SDK, the AppHash of a block header becomes the root.

| Field  | Type                      | Label | Description |
| ------ | ------------------------- | ----- | ----------- |
| `hash` | [bytes](broken-reference) |       |             |

## ibc/core/connection/v1/connection.proto

### ClientPaths

ClientPaths define all the connection paths for a client state.

| Field   | Type                       | Label    | Description              |
| ------- | -------------------------- | -------- | ------------------------ |
| `paths` | [string](broken-reference) | repeated | list of connection paths |

### ConnectionEnd

ConnectionEnd defines a stateful object on a chain connected to another separate one. NOTE: there must only be 2 defined ConnectionEnds to establish a connection between two chains.

| Field          | Type                             | Label    | Description                                                                                                                                            |
| -------------- | -------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `client_id`    | [string](broken-reference)       |          | client associated with this connection.                                                                                                                |
| `versions`     | [Version](broken-reference)      | repeated | IBC version which can be utilised to determine encodings or protocols for channels or packets utilising this connection.                               |
| `state`        | [State](broken-reference)        |          | current state of the connection end.                                                                                                                   |
| `counterparty` | [Counterparty](broken-reference) |          | counterparty chain associated with this connection.                                                                                                    |
| `delay_period` | [uint64](broken-reference)       |          | delay period that must pass before a consensus state can be used for packet-verification NOTE: delay period logic is only implemented by some clients. |

### ConnectionPaths

ConnectionPaths define all the connection paths for a given client state.

| Field       | Type                       | Label    | Description                    |
| ----------- | -------------------------- | -------- | ------------------------------ |
| `client_id` | [string](broken-reference) |          | client state unique identifier |
| `paths`     | [string](broken-reference) | repeated | list of connection paths       |

### Counterparty

Counterparty defines the counterparty chain associated with a connection end.

| Field           | Type                                                    | Label | Description                                                                                 |
| --------------- | ------------------------------------------------------- | ----- | ------------------------------------------------------------------------------------------- |
| `client_id`     | [string](broken-reference)                              |       | identifies the client on the counterparty chain associated with a given connection.         |
| `connection_id` | [string](broken-reference)                              |       | identifies the connection end on the counterparty chain associated with a given connection. |
| `prefix`        | [ibc.core.commitment.v1.MerklePrefix](broken-reference) |       | commitment merkle prefix of the counterparty chain.                                         |

### IdentifiedConnection

IdentifiedConnection defines a connection with additional connection identifier field.

| Field          | Type                             | Label    | Description                                                                                                             |
| -------------- | -------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------- |
| `id`           | [string](broken-reference)       |          | connection identifier.                                                                                                  |
| `client_id`    | [string](broken-reference)       |          | client associated with this connection.                                                                                 |
| `versions`     | [Version](broken-reference)      | repeated | IBC version which can be utilised to determine encodings or protocols for channels or packets utilising this connection |
| `state`        | [State](broken-reference)        |          | current state of the connection end.                                                                                    |
| `counterparty` | [Counterparty](broken-reference) |          | counterparty chain associated with this connection.                                                                     |
| `delay_period` | [uint64](broken-reference)       |          | delay period associated with this connection.                                                                           |

### Version

Version defines the versioning scheme used to negotiate the IBC verison in the connection handshake.

| Field        | Type                       | Label    | Description                                               |
| ------------ | -------------------------- | -------- | --------------------------------------------------------- |
| `identifier` | [string](broken-reference) |          | unique version identifier                                 |
| `features`   | [string](broken-reference) | repeated | list of features compatible with the specified identifier |

### State

State defines if a connection is in one of the following states: INIT, TRYOPEN, OPEN or UNINITIALIZED.

| Name                              | Number | Description                                                                     |
| --------------------------------- | ------ | ------------------------------------------------------------------------------- |
| STATE\_UNINITIALIZED\_UNSPECIFIED | 0      | Default State                                                                   |
| STATE\_INIT                       | 1      | A connection end has just started the opening handshake.                        |
| STATE\_TRYOPEN                    | 2      | A connection end has acknowledged the handshake step on the counterparty chain. |
| STATE\_OPEN                       | 3      | A connection end has completed the handshake.                                   |

## ibc/core/connection/v1/genesis.proto

### GenesisState

GenesisState defines the ibc connection submodule's genesis state.

| Field                      | Type                                     | Label    | Description                                               |
| -------------------------- | ---------------------------------------- | -------- | --------------------------------------------------------- |
| `connections`              | [IdentifiedConnection](broken-reference) | repeated |                                                           |
| `client_connection_paths`  | [ConnectionPaths](broken-reference)      | repeated |                                                           |
| `next_connection_sequence` | [uint64](broken-reference)               |          | the sequence for the next generated connection identifier |

## ibc/core/connection/v1/query.proto

### QueryClientConnectionsRequest

QueryClientConnectionsRequest is the request type for the Query/ClientConnections RPC method

| Field       | Type                       | Label | Description                                    |
| ----------- | -------------------------- | ----- | ---------------------------------------------- |
| `client_id` | [string](broken-reference) |       | client identifier associated with a connection |

### QueryClientConnectionsResponse

QueryClientConnectionsResponse is the response type for the Query/ClientConnections RPC method

| Field              | Type                                          | Label    | Description                                                 |
| ------------------ | --------------------------------------------- | -------- | ----------------------------------------------------------- |
| `connection_paths` | [string](broken-reference)                    | repeated | slice of all the connection paths associated with a client. |
| `proof`            | [bytes](broken-reference)                     |          | merkle proof of existence                                   |
| `proof_height`     | [ibc.core.client.v1.Height](broken-reference) |          | height at which the proof was generated                     |

### QueryConnectionClientStateRequest

QueryConnectionClientStateRequest is the request type for the Query/ConnectionClientState RPC method

| Field           | Type                       | Label | Description           |
| --------------- | -------------------------- | ----- | --------------------- |
| `connection_id` | [string](broken-reference) |       | connection identifier |

### QueryConnectionClientStateResponse

QueryConnectionClientStateResponse is the response type for the Query/ConnectionClientState RPC method

| Field                     | Type                                                         | Label | Description                              |
| ------------------------- | ------------------------------------------------------------ | ----- | ---------------------------------------- |
| `identified_client_state` | [ibc.core.client.v1.IdentifiedClientState](broken-reference) |       | client state associated with the channel |
| `proof`                   | [bytes](broken-reference)                                    |       | merkle proof of existence                |
| `proof_height`            | [ibc.core.client.v1.Height](broken-reference)                |       | height at which the proof was retrieved  |

### QueryConnectionConsensusStateRequest

QueryConnectionConsensusStateRequest is the request type for the Query/ConnectionConsensusState RPC method

| Field             | Type                       | Label | Description           |
| ----------------- | -------------------------- | ----- | --------------------- |
| `connection_id`   | [string](broken-reference) |       | connection identifier |
| `revision_number` | [uint64](broken-reference) |       |                       |
| `revision_height` | [uint64](broken-reference) |       |                       |

### QueryConnectionConsensusStateResponse

QueryConnectionConsensusStateResponse is the response type for the Query/ConnectionConsensusState RPC method

| Field             | Type                                          | Label | Description                                   |
| ----------------- | --------------------------------------------- | ----- | --------------------------------------------- |
| `consensus_state` | [google.protobuf.Any](broken-reference)       |       | consensus state associated with the channel   |
| `client_id`       | [string](broken-reference)                    |       | client ID associated with the consensus state |
| `proof`           | [bytes](broken-reference)                     |       | merkle proof of existence                     |
| `proof_height`    | [ibc.core.client.v1.Height](broken-reference) |       | height at which the proof was retrieved       |

### QueryConnectionRequest

QueryConnectionRequest is the request type for the Query/Connection RPC method

| Field           | Type                       | Label | Description                  |
| --------------- | -------------------------- | ----- | ---------------------------- |
| `connection_id` | [string](broken-reference) |       | connection unique identifier |

### QueryConnectionResponse

QueryConnectionResponse is the response type for the Query/Connection RPC method. Besides the connection end, it includes a proof and the height from which the proof was retrieved.

| Field          | Type                                          | Label | Description                                       |
| -------------- | --------------------------------------------- | ----- | ------------------------------------------------- |
| `connection`   | [ConnectionEnd](broken-reference)             |       | connection associated with the request identifier |
| `proof`        | [bytes](broken-reference)                     |       | merkle proof of existence                         |
| `proof_height` | [ibc.core.client.v1.Height](broken-reference) |       | height at which the proof was retrieved           |

### QueryConnectionsRequest

QueryConnectionsRequest is the request type for the Query/Connections RPC method

| Field        | Type                                                      | Label | Description |
| ------------ | --------------------------------------------------------- | ----- | ----------- |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       |             |

### QueryConnectionsResponse

QueryConnectionsResponse is the response type for the Query/Connections RPC method.

| Field         | Type                                                       | Label    | Description                              |
| ------------- | ---------------------------------------------------------- | -------- | ---------------------------------------- |
| `connections` | [IdentifiedConnection](broken-reference)                   | repeated | list of stored connections of the chain. |
| `pagination`  | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination response                      |
| `height`      | [ibc.core.client.v1.Height](broken-reference)              |          | query block height                       |

### Query

Query provides defines the gRPC querier service

| Method Name                | Request Type                                             | Response Type                                             | Description                                                                          | HTTP Verb | Endpoint                                                                                                                         |
| -------------------------- | -------------------------------------------------------- | --------------------------------------------------------- | ------------------------------------------------------------------------------------ | --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `Connection`               | [QueryConnectionRequest](broken-reference)               | [QueryConnectionResponse](broken-reference)               | Connection queries an IBC connection end.                                            | GET       | /ibc/core/connection/v1beta1/connections/{connection\_id}                                                                        |
| `Connections`              | [QueryConnectionsRequest](broken-reference)              | [QueryConnectionsResponse](broken-reference)              | Connections queries all the IBC connections of a chain.                              | GET       | /ibc/core/connection/v1beta1/connections                                                                                         |
| `ClientConnections`        | [QueryClientConnectionsRequest](broken-reference)        | [QueryClientConnectionsResponse](broken-reference)        | ClientConnections queries the connection paths associated with a client state.       | GET       | /ibc/core/connection/v1beta1/client\_connections/{client\_id}                                                                    |
| `ConnectionClientState`    | [QueryConnectionClientStateRequest](broken-reference)    | [QueryConnectionClientStateResponse](broken-reference)    | ConnectionClientState queries the client state associated with the connection.       | GET       | /ibc/core/connection/v1beta1/connections/{connection\_id}/client\_state                                                          |
| `ConnectionConsensusState` | [QueryConnectionConsensusStateRequest](broken-reference) | [QueryConnectionConsensusStateResponse](broken-reference) | ConnectionConsensusState queries the consensus state associated with the connection. | GET       | /ibc/core/connection/v1beta1/connections/{connection\_id}/consensus\_state/revision/{revision\_number}/height/{revision\_height} |

## ibc/core/connection/v1/tx.proto

### MsgConnectionOpenAck

MsgConnectionOpenAck defines a msg sent by a Relayer to Chain A to acknowledge the change of connection state to TRYOPEN on Chain B.

| Field                        | Type                                          | Label | Description                                                                     |
| ---------------------------- | --------------------------------------------- | ----- | ------------------------------------------------------------------------------- |
| `connection_id`              | [string](broken-reference)                    |       |                                                                                 |
| `counterparty_connection_id` | [string](broken-reference)                    |       |                                                                                 |
| `version`                    | [Version](broken-reference)                   |       |                                                                                 |
| `client_state`               | [google.protobuf.Any](broken-reference)       |       |                                                                                 |
| `proof_height`               | [ibc.core.client.v1.Height](broken-reference) |       |                                                                                 |
| `proof_try`                  | [bytes](broken-reference)                     |       | proof of the initialization the connection on Chain B: `UNITIALIZED -> TRYOPEN` |
| `proof_client`               | [bytes](broken-reference)                     |       | proof of client state included in message                                       |
| `proof_consensus`            | [bytes](broken-reference)                     |       | proof of client consensus state                                                 |
| `consensus_height`           | [ibc.core.client.v1.Height](broken-reference) |       |                                                                                 |
| `signer`                     | [string](broken-reference)                    |       |                                                                                 |

### MsgConnectionOpenAckResponse

MsgConnectionOpenAckResponse defines the Msg/ConnectionOpenAck response type.

### MsgConnectionOpenConfirm

MsgConnectionOpenConfirm defines a msg sent by a Relayer to Chain B to acknowledge the change of connection state to OPEN on Chain A.

| Field           | Type                                          | Label | Description                                                             |
| --------------- | --------------------------------------------- | ----- | ----------------------------------------------------------------------- |
| `connection_id` | [string](broken-reference)                    |       |                                                                         |
| `proof_ack`     | [bytes](broken-reference)                     |       | proof for the change of the connection state on Chain A: `INIT -> OPEN` |
| `proof_height`  | [ibc.core.client.v1.Height](broken-reference) |       |                                                                         |
| `signer`        | [string](broken-reference)                    |       |                                                                         |

### MsgConnectionOpenConfirmResponse

MsgConnectionOpenConfirmResponse defines the Msg/ConnectionOpenConfirm response type.

### MsgConnectionOpenInit

MsgConnectionOpenInit defines the msg sent by an account on Chain A to initialize a connection with Chain B.

| Field          | Type                             | Label | Description |
| -------------- | -------------------------------- | ----- | ----------- |
| `client_id`    | [string](broken-reference)       |       |             |
| `counterparty` | [Counterparty](broken-reference) |       |             |
| `version`      | [Version](broken-reference)      |       |             |
| `delay_period` | [uint64](broken-reference)       |       |             |
| `signer`       | [string](broken-reference)       |       |             |

### MsgConnectionOpenInitResponse

MsgConnectionOpenInitResponse defines the Msg/ConnectionOpenInit response type.

### MsgConnectionOpenTry

MsgConnectionOpenTry defines a msg sent by a Relayer to try to open a connection on Chain B.

| Field                    | Type                                          | Label    | Description                                                                                                                                 |
| ------------------------ | --------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `client_id`              | [string](broken-reference)                    |          |                                                                                                                                             |
| `previous_connection_id` | [string](broken-reference)                    |          | in the case of crossing hello's, when both chains call OpenInit, we need the connection identifier of the previous connection in state INIT |
| `client_state`           | [google.protobuf.Any](broken-reference)       |          |                                                                                                                                             |
| `counterparty`           | [Counterparty](broken-reference)              |          |                                                                                                                                             |
| `delay_period`           | [uint64](broken-reference)                    |          |                                                                                                                                             |
| `counterparty_versions`  | [Version](broken-reference)                   | repeated |                                                                                                                                             |
| `proof_height`           | [ibc.core.client.v1.Height](broken-reference) |          |                                                                                                                                             |
| `proof_init`             | [bytes](broken-reference)                     |          | proof of the initialization the connection on Chain A: `UNITIALIZED -> INIT`                                                                |
| `proof_client`           | [bytes](broken-reference)                     |          | proof of client state included in message                                                                                                   |
| `proof_consensus`        | [bytes](broken-reference)                     |          | proof of client consensus state                                                                                                             |
| `consensus_height`       | [ibc.core.client.v1.Height](broken-reference) |          |                                                                                                                                             |
| `signer`                 | [string](broken-reference)                    |          |                                                                                                                                             |

### MsgConnectionOpenTryResponse

MsgConnectionOpenTryResponse defines the Msg/ConnectionOpenTry response type.

### Msg

Msg defines the ibc/connection Msg service.

| Method Name             | Request Type                                 | Response Type                                        | Description                                                                      | HTTP Verb | Endpoint |
| ----------------------- | -------------------------------------------- | ---------------------------------------------------- | -------------------------------------------------------------------------------- | --------- | -------- |
| `ConnectionOpenInit`    | [MsgConnectionOpenInit](broken-reference)    | [MsgConnectionOpenInitResponse](broken-reference)    | ConnectionOpenInit defines a rpc handler method for MsgConnectionOpenInit.       |           |          |
| `ConnectionOpenTry`     | [MsgConnectionOpenTry](broken-reference)     | [MsgConnectionOpenTryResponse](broken-reference)     | ConnectionOpenTry defines a rpc handler method for MsgConnectionOpenTry.         |           |          |
| `ConnectionOpenAck`     | [MsgConnectionOpenAck](broken-reference)     | [MsgConnectionOpenAckResponse](broken-reference)     | ConnectionOpenAck defines a rpc handler method for MsgConnectionOpenAck.         |           |          |
| `ConnectionOpenConfirm` | [MsgConnectionOpenConfirm](broken-reference) | [MsgConnectionOpenConfirmResponse](broken-reference) | ConnectionOpenConfirm defines a rpc handler method for MsgConnectionOpenConfirm. |           |          |

## ibc/core/types/v1/genesis.proto

### GenesisState

GenesisState defines the ibc module's genesis state.

| Field                | Type                                                    | Label | Description                        |
| -------------------- | ------------------------------------------------------- | ----- | ---------------------------------- |
| `client_genesis`     | [ibc.core.client.v1.GenesisState](broken-reference)     |       | ICS002 - Clients genesis state     |
| `connection_genesis` | [ibc.core.connection.v1.GenesisState](broken-reference) |       | ICS003 - Connections genesis state |
| `channel_genesis`    | [ibc.core.channel.v1.GenesisState](broken-reference)    |       | ICS004 - Channel genesis state     |

## ibc/lightclients/localhost/v1/localhost.proto

### ClientState

ClientState defines a loopback (localhost) client. It requires (read-only) access to keys outside the client prefix.

| Field      | Type                                          | Label | Description              |
| ---------- | --------------------------------------------- | ----- | ------------------------ |
| `chain_id` | [string](broken-reference)                    |       | self chain ID            |
| `height`   | [ibc.core.client.v1.Height](broken-reference) |       | self latest block height |

## ibc/lightclients/solomachine/v1/solomachine.proto

### ChannelStateData

ChannelStateData returns the SignBytes data for channel state verification.

| Field     | Type                                            | Label | Description |
| --------- | ----------------------------------------------- | ----- | ----------- |
| `path`    | [bytes](broken-reference)                       |       |             |
| `channel` | [ibc.core.channel.v1.Channel](broken-reference) |       |             |

### ClientState

ClientState defines a solo machine client that tracks the current consensus state and if the client is frozen.

| Field                         | Type                               | Label | Description                                                                                                           |
| ----------------------------- | ---------------------------------- | ----- | --------------------------------------------------------------------------------------------------------------------- |
| `sequence`                    | [uint64](broken-reference)         |       | latest sequence of the client state                                                                                   |
| `frozen_sequence`             | [uint64](broken-reference)         |       | frozen sequence of the solo machine                                                                                   |
| `consensus_state`             | [ConsensusState](broken-reference) |       |                                                                                                                       |
| `allow_update_after_proposal` | [bool](broken-reference)           |       | when set to true, will allow governance to update a solo machine client. The client will be unfrozen if it is frozen. |

### ClientStateData

ClientStateData returns the SignBytes data for client state verification.

| Field          | Type                                    | Label | Description |
| -------------- | --------------------------------------- | ----- | ----------- |
| `path`         | [bytes](broken-reference)               |       |             |
| `client_state` | [google.protobuf.Any](broken-reference) |       |             |

### ConnectionStateData

ConnectionStateData returns the SignBytes data for connection state verification.

| Field        | Type                                                     | Label | Description |
| ------------ | -------------------------------------------------------- | ----- | ----------- |
| `path`       | [bytes](broken-reference)                                |       |             |
| `connection` | [ibc.core.connection.v1.ConnectionEnd](broken-reference) |       |             |

### ConsensusState

ConsensusState defines a solo machine consensus state. The sequence of a consensus state is contained in the "height" key used in storing the consensus state.

| Field         | Type                                    | Label | Description                                                                                                                                                         |
| ------------- | --------------------------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `public_key`  | [google.protobuf.Any](broken-reference) |       | public key of the solo machine                                                                                                                                      |
| `diversifier` | [string](broken-reference)              |       | diversifier allows the same public key to be re-used across different solo machine clients (potentially on different chains) without being considered misbehaviour. |
| `timestamp`   | [uint64](broken-reference)              |       |                                                                                                                                                                     |

### ConsensusStateData

ConsensusStateData returns the SignBytes data for consensus state verification.

| Field             | Type                                    | Label | Description |
| ----------------- | --------------------------------------- | ----- | ----------- |
| `path`            | [bytes](broken-reference)               |       |             |
| `consensus_state` | [google.protobuf.Any](broken-reference) |       |             |

### Header

Header defines a solo machine consensus header

| Field             | Type                                    | Label | Description                                   |
| ----------------- | --------------------------------------- | ----- | --------------------------------------------- |
| `sequence`        | [uint64](broken-reference)              |       | sequence to update solo machine public key at |
| `timestamp`       | [uint64](broken-reference)              |       |                                               |
| `signature`       | [bytes](broken-reference)               |       |                                               |
| `new_public_key`  | [google.protobuf.Any](broken-reference) |       |                                               |
| `new_diversifier` | [string](broken-reference)              |       |                                               |

### HeaderData

HeaderData returns the SignBytes data for update verification.

| Field             | Type                                    | Label | Description        |
| ----------------- | --------------------------------------- | ----- | ------------------ |
| `new_pub_key`     | [google.protobuf.Any](broken-reference) |       | header public key  |
| `new_diversifier` | [string](broken-reference)              |       | header diversifier |

### Misbehaviour

Misbehaviour defines misbehaviour for a solo machine which consists of a sequence and two signatures over different messages at that sequence.

| Field           | Type                                 | Label | Description |
| --------------- | ------------------------------------ | ----- | ----------- |
| `client_id`     | [string](broken-reference)           |       |             |
| `sequence`      | [uint64](broken-reference)           |       |             |
| `signature_one` | [SignatureAndData](broken-reference) |       |             |
| `signature_two` | [SignatureAndData](broken-reference) |       |             |

### NextSequenceRecvData

NextSequenceRecvData returns the SignBytes data for verification of the next sequence to be received.

| Field           | Type                       | Label | Description |
| --------------- | -------------------------- | ----- | ----------- |
| `path`          | [bytes](broken-reference)  |       |             |
| `next_seq_recv` | [uint64](broken-reference) |       |             |

### PacketAcknowledgementData

PacketAcknowledgementData returns the SignBytes data for acknowledgement verification.

| Field             | Type                      | Label | Description |
| ----------------- | ------------------------- | ----- | ----------- |
| `path`            | [bytes](broken-reference) |       |             |
| `acknowledgement` | [bytes](broken-reference) |       |             |

### PacketCommitmentData

PacketCommitmentData returns the SignBytes data for packet commitment verification.

| Field        | Type                      | Label | Description |
| ------------ | ------------------------- | ----- | ----------- |
| `path`       | [bytes](broken-reference) |       |             |
| `commitment` | [bytes](broken-reference) |       |             |

### PacketReceiptAbsenceData

PacketReceiptAbsenceData returns the SignBytes data for packet receipt absence verification.

| Field  | Type                      | Label | Description |
| ------ | ------------------------- | ----- | ----------- |
| `path` | [bytes](broken-reference) |       |             |

### SignBytes

SignBytes defines the signed bytes used for signature verification.

| Field         | Type                         | Label | Description           |
| ------------- | ---------------------------- | ----- | --------------------- |
| `sequence`    | [uint64](broken-reference)   |       |                       |
| `timestamp`   | [uint64](broken-reference)   |       |                       |
| `diversifier` | [string](broken-reference)   |       |                       |
| `data_type`   | [DataType](broken-reference) |       | type of the data used |
| `data`        | [bytes](broken-reference)    |       | marshaled data        |

### SignatureAndData

SignatureAndData contains a signature and the data signed over to create that signature.

| Field       | Type                         | Label | Description |
| ----------- | ---------------------------- | ----- | ----------- |
| `signature` | [bytes](broken-reference)    |       |             |
| `data_type` | [DataType](broken-reference) |       |             |
| `data`      | [bytes](broken-reference)    |       |             |
| `timestamp` | [uint64](broken-reference)   |       |             |

### TimestampedSignatureData

TimestampedSignatureData contains the signature data and the timestamp of the signature.

| Field            | Type                       | Label | Description |
| ---------------- | -------------------------- | ----- | ----------- |
| `signature_data` | [bytes](broken-reference)  |       |             |
| `timestamp`      | [uint64](broken-reference) |       |             |

### DataType

DataType defines the type of solo machine proof being created. This is done to preserve uniqueness of different data sign byte encodings.

| Name                                   | Number | Description                                       |
| -------------------------------------- | ------ | ------------------------------------------------- |
| DATA\_TYPE\_UNINITIALIZED\_UNSPECIFIED | 0      | Default State                                     |
| DATA\_TYPE\_CLIENT\_STATE              | 1      | Data type for client state verification           |
| DATA\_TYPE\_CONSENSUS\_STATE           | 2      | Data type for consensus state verification        |
| DATA\_TYPE\_CONNECTION\_STATE          | 3      | Data type for connection state verification       |
| DATA\_TYPE\_CHANNEL\_STATE             | 4      | Data type for channel state verification          |
| DATA\_TYPE\_PACKET\_COMMITMENT         | 5      | Data type for packet commitment verification      |
| DATA\_TYPE\_PACKET\_ACKNOWLEDGEMENT    | 6      | Data type for packet acknowledgement verification |
| DATA\_TYPE\_PACKET\_RECEIPT\_ABSENCE   | 7      | Data type for packet receipt absence verification |
| DATA\_TYPE\_NEXT\_SEQUENCE\_RECV       | 8      | Data type for next sequence recv verification     |
| DATA\_TYPE\_HEADER                     | 9      | Data type for header verification                 |

## ibc/lightclients/tendermint/v1/tendermint.proto

### ClientState

ClientState from Tendermint tracks the current validator set, latest height, and a possible frozen height.

| Field                             | Type                                          | Label    | Description                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --------------------------------- | --------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `chain_id`                        | [string](broken-reference)                    |          |                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `trust_level`                     | [Fraction](broken-reference)                  |          |                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `trusting_period`                 | [google.protobuf.Duration](broken-reference)  |          | duration of the period since the LastestTimestamp during which the submitted headers are valid for upgrade                                                                                                                                                                                                                                                                                                                          |
| `unbonding_period`                | [google.protobuf.Duration](broken-reference)  |          | duration of the staking unbonding period                                                                                                                                                                                                                                                                                                                                                                                            |
| `max_clock_drift`                 | [google.protobuf.Duration](broken-reference)  |          | defines how much new (untrusted) header's Time can drift into the future.                                                                                                                                                                                                                                                                                                                                                           |
| `frozen_height`                   | [ibc.core.client.v1.Height](broken-reference) |          | Block height when the client was frozen due to a misbehaviour                                                                                                                                                                                                                                                                                                                                                                       |
| `latest_height`                   | [ibc.core.client.v1.Height](broken-reference) |          | Latest height the client was updated to                                                                                                                                                                                                                                                                                                                                                                                             |
| `proof_specs`                     | [ics23.ProofSpec](broken-reference)           | repeated | Proof specifications used in verifying counterparty state                                                                                                                                                                                                                                                                                                                                                                           |
| `upgrade_path`                    | [string](broken-reference)                    | repeated | Path at which next upgraded client will be committed. Each element corresponds to the key for a single CommitmentProof in the chained proof. NOTE: ClientState must stored under `{upgradePath}/{upgradeHeight}/clientState` ConsensusState must be stored under `{upgradepath}/{upgradeHeight}/consensusState` For SDK chains using the default upgrade module, upgrade\_path should be \[]string{"upgrade", "upgradedIBCState"}\` |
| `allow_update_after_expiry`       | [bool](broken-reference)                      |          | This flag, when set to true, will allow governance to recover a client which has expired                                                                                                                                                                                                                                                                                                                                            |
| `allow_update_after_misbehaviour` | [bool](broken-reference)                      |          | This flag, when set to true, will allow governance to unfreeze a client whose chain has experienced a misbehaviour event                                                                                                                                                                                                                                                                                                            |

### ConsensusState

ConsensusState defines the consensus state from Tendermint.

| Field                  | Type                                                  | Label | Description                                                                            |
| ---------------------- | ----------------------------------------------------- | ----- | -------------------------------------------------------------------------------------- |
| `timestamp`            | [google.protobuf.Timestamp](broken-reference)         |       | timestamp that corresponds to the block height in which the ConsensusState was stored. |
| `root`                 | [ibc.core.commitment.v1.MerkleRoot](broken-reference) |       | commitment root (i.e app hash)                                                         |
| `next_validators_hash` | [bytes](broken-reference)                             |       |                                                                                        |

### Fraction

Fraction defines the protobuf message type for tmmath.Fraction that only supports positive values.

| Field         | Type                       | Label | Description |
| ------------- | -------------------------- | ----- | ----------- |
| `numerator`   | [uint64](broken-reference) |       |             |
| `denominator` | [uint64](broken-reference) |       |             |

### Header

Header defines the Tendermint client consensus Header. It encapsulates all the information necessary to update from a trusted Tendermint ConsensusState. The inclusion of TrustedHeight and TrustedValidators allows this update to process correctly, so long as the ConsensusState for the TrustedHeight exists, this removes race conditions among relayers The SignedHeader and ValidatorSet are the new untrusted update fields for the client. The TrustedHeight is the height of a stored ConsensusState on the client that will be used to verify the new untrusted header. The Trusted ConsensusState must be within the unbonding period of current time in order to correctly verify, and the TrustedValidators must hash to TrustedConsensusState.NextValidatorsHash since that is the last trusted validator set at the TrustedHeight.

| Field                | Type                                              | Label | Description |
| -------------------- | ------------------------------------------------- | ----- | ----------- |
| `signed_header`      | [tendermint.types.SignedHeader](broken-reference) |       |             |
| `validator_set`      | [tendermint.types.ValidatorSet](broken-reference) |       |             |
| `trusted_height`     | [ibc.core.client.v1.Height](broken-reference)     |       |             |
| `trusted_validators` | [tendermint.types.ValidatorSet](broken-reference) |       |             |

### Misbehaviour

Misbehaviour is a wrapper over two conflicting Headers that implements Misbehaviour interface expected by ICS-02

| Field       | Type                       | Label | Description |
| ----------- | -------------------------- | ----- | ----------- |
| `client_id` | [string](broken-reference) |       |             |
| `header_1`  | [Header](broken-reference) |       |             |
| `header_2`  | [Header](broken-reference) |       |             |

## uptick/collection/v1/collection.proto

### BaseNFT

BaseNFT defines a non-fungible token

| Field      | Type                       | Label | Description |
| ---------- | -------------------------- | ----- | ----------- |
| `id`       | [string](broken-reference) |       |             |
| `name`     | [string](broken-reference) |       |             |
| `uri`      | [string](broken-reference) |       |             |
| `data`     | [string](broken-reference) |       |             |
| `owner`    | [string](broken-reference) |       |             |
| `uri_hash` | [string](broken-reference) |       |             |

### Collection

Collection defines a type of collection

| Field   | Type                        | Label    | Description |
| ------- | --------------------------- | -------- | ----------- |
| `denom` | [Denom](broken-reference)   |          |             |
| `nfts`  | [BaseNFT](broken-reference) | repeated |             |

### Denom

Denom defines a type of NFT

| Field               | Type                       | Label | Description |
| ------------------- | -------------------------- | ----- | ----------- |
| `id`                | [string](broken-reference) |       |             |
| `name`              | [string](broken-reference) |       |             |
| `schema`            | [string](broken-reference) |       |             |
| `creator`           | [string](broken-reference) |       |             |
| `symbol`            | [string](broken-reference) |       |             |
| `mint_restricted`   | [bool](broken-reference)   |       |             |
| `update_restricted` | [bool](broken-reference)   |       |             |
| `description`       | [string](broken-reference) |       |             |
| `uri`               | [string](broken-reference) |       |             |
| `uri_hash`          | [string](broken-reference) |       |             |
| `data`              | [string](broken-reference) |       |             |

### DenomMetadata

| Field               | Type                       | Label | Description |
| ------------------- | -------------------------- | ----- | ----------- |
| `creator`           | [string](broken-reference) |       |             |
| `schema`            | [string](broken-reference) |       |             |
| `mint_restricted`   | [bool](broken-reference)   |       |             |
| `update_restricted` | [bool](broken-reference)   |       |             |
| `data`              | [string](broken-reference) |       |             |

### IDCollection

IDCollection defines a type of collection with specified ID

| Field       | Type                       | Label    | Description |
| ----------- | -------------------------- | -------- | ----------- |
| `denom_id`  | [string](broken-reference) |          |             |
| `token_ids` | [string](broken-reference) | repeated |             |

### NFTMetadata

| Field  | Type                       | Label | Description |
| ------ | -------------------------- | ----- | ----------- |
| `name` | [string](broken-reference) |       |             |
| `data` | [string](broken-reference) |       |             |

### Owner

Owner defines a type of owner

| Field            | Type                             | Label    | Description |
| ---------------- | -------------------------------- | -------- | ----------- |
| `address`        | [string](broken-reference)       |          |             |
| `id_collections` | [IDCollection](broken-reference) | repeated |             |

## uptick/collection/v1/genesis.proto

### GenesisState

GenesisState defines the collection module's genesis state

| Field         | Type                           | Label    | Description |
| ------------- | ------------------------------ | -------- | ----------- |
| `collections` | [Collection](broken-reference) | repeated |             |

## uptick/collection/v1/query.proto

### QueryCollectionRequest

QueryCollectionRequest is the request type for the Query/Collection RPC method

| Field        | Type                                                      | Label | Description                                                |
| ------------ | --------------------------------------------------------- | ----- | ---------------------------------------------------------- |
| `denom_id`   | [string](broken-reference)                                |       |                                                            |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request. |

### QueryCollectionResponse

QueryCollectionResponse is the response type for the Query/Collection RPC method

| Field        | Type                                                       | Label | Description |
| ------------ | ---------------------------------------------------------- | ----- | ----------- |
| `collection` | [Collection](broken-reference)                             |       |             |
| `pagination` | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |       |             |

### QueryDenomRequest

QueryDenomRequest is the request type for the Query/Denom RPC method

| Field      | Type                       | Label | Description |
| ---------- | -------------------------- | ----- | ----------- |
| `denom_id` | [string](broken-reference) |       |             |

### QueryDenomResponse

QueryDenomResponse is the response type for the Query/Denom RPC method

| Field   | Type                      | Label | Description |
| ------- | ------------------------- | ----- | ----------- |
| `denom` | [Denom](broken-reference) |       |             |

### QueryDenomsRequest

QueryDenomsRequest is the request type for the Query/Denoms RPC method

| Field        | Type                                                      | Label | Description                                                |
| ------------ | --------------------------------------------------------- | ----- | ---------------------------------------------------------- |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request. |

### QueryDenomsResponse

QueryDenomsResponse is the response type for the Query/Denoms RPC method

| Field        | Type                                                       | Label    | Description |
| ------------ | ---------------------------------------------------------- | -------- | ----------- |
| `denoms`     | [Denom](broken-reference)                                  | repeated |             |
| `pagination` | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          |             |

### QueryNFTRequest

QueryNFTRequest is the request type for the Query/NFT RPC method

| Field      | Type                       | Label | Description |
| ---------- | -------------------------- | ----- | ----------- |
| `denom_id` | [string](broken-reference) |       |             |
| `token_id` | [string](broken-reference) |       |             |

### QueryNFTResponse

QueryNFTResponse is the response type for the Query/NFT RPC method

| Field | Type                        | Label | Description |
| ----- | --------------------------- | ----- | ----------- |
| `nft` | [BaseNFT](broken-reference) |       |             |

### QueryNFTsOfOwnerRequest

QueryNFTsOfOwnerRequest is the request type for the Query/Owner RPC method

| Field        | Type                                                      | Label | Description                                                |
| ------------ | --------------------------------------------------------- | ----- | ---------------------------------------------------------- |
| `denom_id`   | [string](broken-reference)                                |       |                                                            |
| `owner`      | [string](broken-reference)                                |       |                                                            |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request. |

### QueryNFTsOfOwnerResponse

QueryNFTsOfOwnerResponse is the response type for the Query/Owner RPC method

| Field        | Type                                                       | Label | Description |
| ------------ | ---------------------------------------------------------- | ----- | ----------- |
| `owner`      | [Owner](broken-reference)                                  |       |             |
| `pagination` | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |       |             |

### QuerySupplyRequest

QuerySupplyRequest is the request type for the Query/HTLC RPC method

| Field      | Type                       | Label | Description |
| ---------- | -------------------------- | ----- | ----------- |
| `denom_id` | [string](broken-reference) |       |             |
| `owner`    | [string](broken-reference) |       |             |

### QuerySupplyResponse

QuerySupplyResponse is the response type for the Query/Supply RPC method

| Field    | Type                       | Label | Description |
| -------- | -------------------------- | ----- | ----------- |
| `amount` | [uint64](broken-reference) |       |             |

### Query

Query defines the gRPC querier service for NFT module

| Method Name   | Request Type                                | Response Type                                | Description                                               | HTTP Verb | Endpoint                                          |
| ------------- | ------------------------------------------- | -------------------------------------------- | --------------------------------------------------------- | --------- | ------------------------------------------------- |
| `Supply`      | [QuerySupplyRequest](broken-reference)      | [QuerySupplyResponse](broken-reference)      | Supply queries the total supply of a given denom or owner | GET       | /uptick/collection/collections/{denom\_id}/supply |
| `NFTsOfOwner` | [QueryNFTsOfOwnerRequest](broken-reference) | [QueryNFTsOfOwnerResponse](broken-reference) | NFTsOfOwner queries the NFTs of the specified owner       | GET       | /uptick/collection/nfts                           |
| `Collection`  | [QueryCollectionRequest](broken-reference)  | [QueryCollectionResponse](broken-reference)  | Collection queries the NFTs of the specified denom        | GET       | /uptick/collection/collections/{denom\_id}        |
| `Denom`       | [QueryDenomRequest](broken-reference)       | [QueryDenomResponse](broken-reference)       | Denom queries the definition of a given denom             | GET       | /uptick/collection/nft/denoms/{denom\_id}         |
| `Denoms`      | [QueryDenomsRequest](broken-reference)      | [QueryDenomsResponse](broken-reference)      | Denoms queries all the denoms                             | GET       | /uptick/collection/nft/denoms                     |
| `NFT`         | [QueryNFTRequest](broken-reference)         | [QueryNFTResponse](broken-reference)         | NFT queries the NFT for the given denom and token ID      | GET       | /uptick/collection/nfts/{denom\_id}/{token\_id}   |

## uptick/collection/v1/tx.proto

### MsgBurnNFT

MsgBurnNFT defines an SDK message for burning a NFT.

| Field      | Type                       | Label | Description |
| ---------- | -------------------------- | ----- | ----------- |
| `id`       | [string](broken-reference) |       |             |
| `denom_id` | [string](broken-reference) |       |             |
| `sender`   | [string](broken-reference) |       |             |

### MsgBurnNFTResponse

MsgBurnNFTResponse defines the Msg/BurnNFT response type.

### MsgEditNFT

MsgEditNFT defines an SDK message for editing a nft.

| Field      | Type                       | Label | Description |
| ---------- | -------------------------- | ----- | ----------- |
| `id`       | [string](broken-reference) |       |             |
| `denom_id` | [string](broken-reference) |       |             |
| `name`     | [string](broken-reference) |       |             |
| `uri`      | [string](broken-reference) |       |             |
| `data`     | [string](broken-reference) |       |             |
| `sender`   | [string](broken-reference) |       |             |
| `uri_hash` | [string](broken-reference) |       |             |

### MsgEditNFTResponse

MsgEditNFTResponse defines the Msg/EditNFT response type.

### MsgIssueDenom

MsgIssueDenom defines an SDK message for creating a new denom.

| Field               | Type                       | Label | Description |
| ------------------- | -------------------------- | ----- | ----------- |
| `id`                | [string](broken-reference) |       |             |
| `name`              | [string](broken-reference) |       |             |
| `schema`            | [string](broken-reference) |       |             |
| `sender`            | [string](broken-reference) |       |             |
| `symbol`            | [string](broken-reference) |       |             |
| `mint_restricted`   | [bool](broken-reference)   |       |             |
| `update_restricted` | [bool](broken-reference)   |       |             |
| `description`       | [string](broken-reference) |       |             |
| `uri`               | [string](broken-reference) |       |             |
| `uri_hash`          | [string](broken-reference) |       |             |
| `data`              | [string](broken-reference) |       |             |

### MsgIssueDenomResponse

MsgIssueDenomResponse defines the Msg/IssueDenom response type.

### MsgMintNFT

MsgMintNFT defines an SDK message for creating a new NFT.

| Field       | Type                       | Label | Description |
| ----------- | -------------------------- | ----- | ----------- |
| `id`        | [string](broken-reference) |       |             |
| `denom_id`  | [string](broken-reference) |       |             |
| `name`      | [string](broken-reference) |       |             |
| `uri`       | [string](broken-reference) |       |             |
| `data`      | [string](broken-reference) |       |             |
| `sender`    | [string](broken-reference) |       |             |
| `recipient` | [string](broken-reference) |       |             |
| `uri_hash`  | [string](broken-reference) |       |             |

### MsgMintNFTResponse

MsgMintNFTResponse defines the Msg/MintNFT response type.

### MsgTransferDenom

MsgTransferDenom defines an SDK message for transferring an denom to recipient.

| Field       | Type                       | Label | Description |
| ----------- | -------------------------- | ----- | ----------- |
| `id`        | [string](broken-reference) |       |             |
| `sender`    | [string](broken-reference) |       |             |
| `recipient` | [string](broken-reference) |       |             |

### MsgTransferDenomResponse

MsgTransferDenomResponse defines the Msg/TransferDenom response type.

### MsgTransferNFT

MsgTransferNFT defines an SDK message for transferring an NFT to recipient.

| Field       | Type                       | Label | Description |
| ----------- | -------------------------- | ----- | ----------- |
| `id`        | [string](broken-reference) |       |             |
| `denom_id`  | [string](broken-reference) |       |             |
| `name`      | [string](broken-reference) |       |             |
| `uri`       | [string](broken-reference) |       |             |
| `data`      | [string](broken-reference) |       |             |
| `sender`    | [string](broken-reference) |       |             |
| `recipient` | [string](broken-reference) |       |             |
| `uri_hash`  | [string](broken-reference) |       |             |

### MsgTransferNFTResponse

MsgTransferNFTResponse defines the Msg/TransferNFT response type.

### Msg

Msg defines the nft Msg service.

| Method Name     | Request Type                         | Response Type                                | Description                                              | HTTP Verb | Endpoint |
| --------------- | ------------------------------------ | -------------------------------------------- | -------------------------------------------------------- | --------- | -------- |
| `IssueDenom`    | [MsgIssueDenom](broken-reference)    | [MsgIssueDenomResponse](broken-reference)    | IssueDenom defines a method for issue a denom.           |           |          |
| `MintNFT`       | [MsgMintNFT](broken-reference)       | [MsgMintNFTResponse](broken-reference)       | MintNFT defines a method for mint a new nft              |           |          |
| `EditNFT`       | [MsgEditNFT](broken-reference)       | [MsgEditNFTResponse](broken-reference)       | RefundHTLC defines a method for editing a nft.           |           |          |
| `TransferNFT`   | [MsgTransferNFT](broken-reference)   | [MsgTransferNFTResponse](broken-reference)   | TransferNFT defines a method for transferring a nft.     |           |          |
| `BurnNFT`       | [MsgBurnNFT](broken-reference)       | [MsgBurnNFTResponse](broken-reference)       | BurnNFT defines a method for burning a nft.              |           |          |
| `TransferDenom` | [MsgTransferDenom](broken-reference) | [MsgTransferDenomResponse](broken-reference) | TransferDenom defines a method for transferring a denom. |           |          |

## uptick/erc20/v1/erc20.proto

### RegisterCoinProposal

RegisterCoinProposal is a gov Content type to register a token pair

| Field         | Type                                             | Label | Description                                               |
| ------------- | ------------------------------------------------ | ----- | --------------------------------------------------------- |
| `title`       | [string](broken-reference)                       |       | title of the proposal                                     |
| `description` | [string](broken-reference)                       |       | proposal description                                      |
| `metadata`    | [cosmos.bank.v1beta1.Metadata](broken-reference) |       | token pair of Cosmos native denom and ERC20 token address |

### RegisterERC20Proposal

RegisterCoinProposal is a gov Content type to register a token pair

| Field          | Type                       | Label | Description                     |
| -------------- | -------------------------- | ----- | ------------------------------- |
| `title`        | [string](broken-reference) |       | title of the proposal           |
| `description`  | [string](broken-reference) |       | proposal description            |
| `erc20address` | [string](broken-reference) |       | contract address of ERC20 token |

### ToggleTokenRelayProposal

ToggleTokenRelayProposal is a gov Content type to toggle the internal relaying of a token pair.

| Field         | Type                       | Label | Description                                                                                          |
| ------------- | -------------------------- | ----- | ---------------------------------------------------------------------------------------------------- |
| `title`       | [string](broken-reference) |       | title of the proposal                                                                                |
| `description` | [string](broken-reference) |       | proposal description                                                                                 |
| `token`       | [string](broken-reference) |       | token identifier can be either the hex contract address of the ERC20 or the Cosmos base denomination |

### TokenPair

TokenPair defines an instance that records pairing consisting of a Cosmos native Coin and an ERC20 token address.

| Field            | Type                       | Label | Description                                                               |
| ---------------- | -------------------------- | ----- | ------------------------------------------------------------------------- |
| `erc20_address`  | [string](broken-reference) |       | address of ERC20 contract token                                           |
| `denom`          | [string](broken-reference) |       | cosmos base denomination to be mapped to                                  |
| `enabled`        | [bool](broken-reference)   |       | shows token mapping enable status                                         |
| `contract_owner` | [Owner](broken-reference)  |       | ERC20 owner address ENUM (0 invalid, 1 ModuleAccount, 2 external address) |

### UpdateTokenPairERC20Proposal

UpdateTokenPairERC20Proposal is a gov Content type to update a token pair's ERC20 contract address.

| Field               | Type                       | Label | Description                         |
| ------------------- | -------------------------- | ----- | ----------------------------------- |
| `title`             | [string](broken-reference) |       | title of the proposal               |
| `description`       | [string](broken-reference) |       | proposal description                |
| `erc20_address`     | [string](broken-reference) |       | contract address of ERC20 token     |
| `new_erc20_address` | [string](broken-reference) |       | new address of ERC20 token contract |

### Owner

Owner enumerates the ownership of a ERC20 contract.

| Name               | Number | Description                                               |
| ------------------ | ------ | --------------------------------------------------------- |
| OWNER\_UNSPECIFIED | 0      | OWNER\_UNSPECIFIED defines an invalid/undefined owner.    |
| OWNER\_MODULE      | 1      | OWNER\_MODULE erc20 is owned by the erc20 module account. |
| OWNER\_EXTERNAL    | 2      | EXTERNAL erc20 is owned by an external account.           |

## uptick/erc20/v1/genesis.proto

### GenesisState

GenesisState defines the module's genesis state.

| Field         | Type                          | Label    | Description            |
| ------------- | ----------------------------- | -------- | ---------------------- |
| `params`      | [Params](broken-reference)    |          | module parameters      |
| `token_pairs` | [TokenPair](broken-reference) | repeated | registered token pairs |

### Params

Params defines the erc20 module params

| Field             | Type                     | Label | Description                                                                                                                                                           |
| ----------------- | ------------------------ | ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `enable_erc20`    | [bool](broken-reference) |       | parameter to enable the intrarelaying of Cosmos coins <--> ERC20 tokens.                                                                                              |
| `enable_evm_hook` | [bool](broken-reference) |       | parameter to enable the EVM hook to convert an ERC20 token to a Cosmos Coin by transferring the Tokens through a MsgEthereumTx to the ModuleAddress Ethereum address. |

## uptick/erc20/v1/query.proto

### QueryParamsRequest

QueryParamsRequest is the request type for the Query/Params RPC method.

### QueryParamsResponse

QueryParamsResponse is the response type for the Query/Params RPC method.

| Field    | Type                       | Label | Description |
| -------- | -------------------------- | ----- | ----------- |
| `params` | [Params](broken-reference) |       |             |

### QueryTokenPairRequest

QueryTokenPairRequest is the request type for the Query/TokenPair RPC method.

| Field   | Type                       | Label | Description                                                                                          |
| ------- | -------------------------- | ----- | ---------------------------------------------------------------------------------------------------- |
| `token` | [string](broken-reference) |       | token identifier can be either the hex contract address of the ERC20 or the Cosmos base denomination |

### QueryTokenPairResponse

QueryTokenPairResponse is the response type for the Query/TokenPair RPC method.

| Field        | Type                          | Label | Description |
| ------------ | ----------------------------- | ----- | ----------- |
| `token_pair` | [TokenPair](broken-reference) |       |             |

### QueryTokenPairsRequest

QueryTokenPairsRequest is the request type for the Query/TokenPairs RPC method.

| Field        | Type                                                      | Label | Description                                                |
| ------------ | --------------------------------------------------------- | ----- | ---------------------------------------------------------- |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request. |

### QueryTokenPairsResponse

QueryTokenPairsResponse is the response type for the Query/TokenPairs RPC method.

| Field         | Type                                                       | Label    | Description                                        |
| ------------- | ---------------------------------------------------------- | -------- | -------------------------------------------------- |
| `token_pairs` | [TokenPair](broken-reference)                              | repeated |                                                    |
| `pagination`  | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response. |

### Query

Query defines the gRPC querier service.

| Method Name  | Request Type                               | Response Type                               | Description                              | HTTP Verb | Endpoint                              |
| ------------ | ------------------------------------------ | ------------------------------------------- | ---------------------------------------- | --------- | ------------------------------------- |
| `TokenPairs` | [QueryTokenPairsRequest](broken-reference) | [QueryTokenPairsResponse](broken-reference) | Retrieves registered token pairs         | GET       | /uptick/erc20/v1/token\_pairs         |
| `TokenPair`  | [QueryTokenPairRequest](broken-reference)  | [QueryTokenPairResponse](broken-reference)  | Retrieves a registered token pair        | GET       | /uptick/erc20/v1/token\_pairs/{token} |
| `Params`     | [QueryParamsRequest](broken-reference)     | [QueryParamsResponse](broken-reference)     | Params retrieves the erc20 module params | GET       | /uptick/erc20/v1/params               |

## uptick/erc20/v1/tx.proto

### MsgConvertCoin

MsgConvertCoin defines a Msg to convert a Cosmos Coin to a ERC20 token

| Field      | Type                                         | Label | Description                                                                                                              |
| ---------- | -------------------------------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------ |
| `coin`     | [cosmos.base.v1beta1.Coin](broken-reference) |       | Cosmos coin which denomination is registered on erc20 bridge. The coin amount defines the total ERC20 tokens to convert. |
| `receiver` | [string](broken-reference)                   |       | recipient hex address to receive ERC20 token                                                                             |
| `sender`   | [string](broken-reference)                   |       | cosmos bech32 address from the owner of the given ERC20 tokens                                                           |

### MsgConvertCoinResponse

MsgConvertCoinResponse returns no fields

### MsgConvertERC20

MsgConvertERC20 defines a Msg to convert an ERC20 token to a Cosmos SDK coin.

| Field              | Type                       | Label | Description                                                 |
| ------------------ | -------------------------- | ----- | ----------------------------------------------------------- |
| `contract_address` | [string](broken-reference) |       | ERC20 token contract address registered on erc20 bridge     |
| `amount`           | [string](broken-reference) |       | amount of ERC20 tokens to mint                              |
| `receiver`         | [string](broken-reference) |       | bech32 address to receive SDK coins.                        |
| `sender`           | [string](broken-reference) |       | sender hex address from the owner of the given ERC20 tokens |

### MsgConvertERC20Response

MsgConvertERC20Response returns no fields

### Msg

Msg defines the erc20 Msg service.

| Method Name    | Request Type                        | Response Type                               | Description                                                                                                          | HTTP Verb | Endpoint                           |
| -------------- | ----------------------------------- | ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | --------- | ---------------------------------- |
| `ConvertCoin`  | [MsgConvertCoin](broken-reference)  | [MsgConvertCoinResponse](broken-reference)  | ConvertCoin mints a ERC20 representation of the SDK Coin denom that is registered on the token mapping.              | GET       | /uptick/erc20/v1/tx/convert\_coin  |
| `ConvertERC20` | [MsgConvertERC20](broken-reference) | [MsgConvertERC20Response](broken-reference) | ConvertERC20 mints a Cosmos coin representation of the ERC20 token contract that is registered on the token mapping. | GET       | /uptick/erc20/v1/tx/convert\_erc20 |

## uptick/erc721/v1/erc721.proto

### TokenPair

TokenPair defines an instance that records a pairing consisting of a native Cosmos Coin and an ERC721 token address.

| Field            | Type                       | Label | Description                         |
| ---------------- | -------------------------- | ----- | ----------------------------------- |
| `erc721_address` | [string](broken-reference) |       | address of ERC721 contract token    |
| `class_id`       | [string](broken-reference) |       | cosmos nft class ID to be mapped to |

### UIDPair

defines the unique id of nft asset

| Field        | Type                       | Label | Description                                 |
| ------------ | -------------------------- | ----- | ------------------------------------------- |
| `erc721_did` | [string](broken-reference) |       | address of ERC721 contract token + tokenId  |
| `class_did`  | [string](broken-reference) |       | cosmos nft class ID to be mapped to + nftId |

### Owner

Owner enumerates the ownership of a ERC721 contract.

| Name               | Number | Description                                                 |
| ------------------ | ------ | ----------------------------------------------------------- |
| OWNER\_UNSPECIFIED | 0      | OWNER\_UNSPECIFIED defines an invalid/undefined owner.      |
| OWNER\_MODULE      | 1      | OWNER\_MODULE erc721 is owned by the erc721 module account. |
| OWNER\_EXTERNAL    | 2      | EXTERNAL erc721 is owned by an external account.            |

## uptick/erc721/v1/genesis.proto

### GenesisState

GenesisState defines the module's genesis state.

| Field         | Type                          | Label    | Description            |
| ------------- | ----------------------------- | -------- | ---------------------- |
| `params`      | [Params](broken-reference)    |          | module parameters      |
| `token_pairs` | [TokenPair](broken-reference) | repeated | registered token pairs |

### Params

Params defines the erc721 module params

| Field             | Type                     | Label | Description                                                                                                                                                              |
| ----------------- | ------------------------ | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `enable_erc721`   | [bool](broken-reference) |       | parameter to enable the conversion of Cosmos nft <--> ERC721 tokens.                                                                                                     |
| `enable_evm_hook` | [bool](broken-reference) |       | parameter to enable the EVM hook that converts an ERC721 token to a Cosmos NFT by transferring the Tokens through a MsgEthereumTx to the ModuleAddress Ethereum address. |

## uptick/erc721/v1/query.proto

### QueryParamsRequest

QueryParamsRequest is the request type for the Query/Params RPC method.

### QueryParamsResponse

QueryParamsResponse is the response type for the Query/Params RPC method.

| Field    | Type                       | Label | Description |
| -------- | -------------------------- | ----- | ----------- |
| `params` | [Params](broken-reference) |       |             |

### QueryTokenPairRequest

QueryTokenPairRequest is the request type for the Query/TokenPair RPC method.

| Field   | Type                       | Label | Description                                                                                     |
| ------- | -------------------------- | ----- | ----------------------------------------------------------------------------------------------- |
| `token` | [string](broken-reference) |       | token identifier can be either the hex contract address of the ERC721 or the Cosmos nft classID |

### QueryTokenPairResponse

QueryTokenPairResponse is the response type for the Query/TokenPair RPC method.

| Field        | Type                          | Label | Description |
| ------------ | ----------------------------- | ----- | ----------- |
| `token_pair` | [TokenPair](broken-reference) |       |             |

### QueryTokenPairsRequest

QueryTokenPairsRequest is the request type for the Query/TokenPairs RPC method.

| Field        | Type                                                      | Label | Description                                                |
| ------------ | --------------------------------------------------------- | ----- | ---------------------------------------------------------- |
| `pagination` | [cosmos.base.query.v1beta1.PageRequest](broken-reference) |       | pagination defines an optional pagination for the request. |

### QueryTokenPairsResponse

QueryTokenPairsResponse is the response type for the Query/TokenPairs RPC method.

| Field         | Type                                                       | Label    | Description                                        |
| ------------- | ---------------------------------------------------------- | -------- | -------------------------------------------------- |
| `token_pairs` | [TokenPair](broken-reference)                              | repeated |                                                    |
| `pagination`  | [cosmos.base.query.v1beta1.PageResponse](broken-reference) |          | pagination defines the pagination in the response. |

### Query

Query defines the gRPC querier service.

| Method Name  | Request Type                               | Response Type                               | Description                                 | HTTP Verb | Endpoint                              |
| ------------ | ------------------------------------------ | ------------------------------------------- | ------------------------------------------- | --------- | ------------------------------------- |
| `TokenPairs` | [QueryTokenPairsRequest](broken-reference) | [QueryTokenPairsResponse](broken-reference) | TokenPairs retrieves registered token pairs | GET       | /evmos/erc721/v1/token\_pairs         |
| `TokenPair`  | [QueryTokenPairRequest](broken-reference)  | [QueryTokenPairResponse](broken-reference)  | TokenPair retrieves a registered token pair | GET       | /evmos/erc721/v1/token\_pairs/{token} |
| `Params`     | [QueryParamsRequest](broken-reference)     | [QueryParamsResponse](broken-reference)     | Params retrieves the erc721 module params   | GET       | /evmos/erc721/v1/params               |

## uptick/erc721/v1/tx.proto

### MsgConvertERC721

MsgConvertERC721 defines a Msg to convert a ERC721 token to a native Cosmos nft.

| Field              | Type                       | Label    | Description                                                  |
| ------------------ | -------------------------- | -------- | ------------------------------------------------------------ |
| `contract_address` | [string](broken-reference) |          | ERC721 token contract address registered in a token pair     |
| `token_ids`        | [string](broken-reference) | repeated | tokenID to convert                                           |
| `receiver`         | [string](broken-reference) |          | bech32 address to receive native Cosmos coins                |
| `sender`           | [string](broken-reference) |          | sender hex address from the owner of the given ERC721 tokens |
| `class_id`         | [string](broken-reference) |          | nft classID to cnvert to ERC721                              |
| `nft_ids`          | [string](broken-reference) | repeated | nftID to cnvert to ERC721                                    |

### MsgConvertERC721Response

MsgConvertERC721Response returns no fields

### MsgConvertNFT

MsgConvertNFT defines a Msg to convert a native Cosmos nft to a ERC721 token

| Field              | Type                       | Label    | Description                                                    |
| ------------------ | -------------------------- | -------- | -------------------------------------------------------------- |
| `class_id`         | [string](broken-reference) |          | nft classID to cnvert to ERC721                                |
| `nft_ids`          | [string](broken-reference) | repeated | nftID to cnvert to ERC721                                      |
| `receiver`         | [string](broken-reference) |          | recipient hex address to receive ERC721 token                  |
| `sender`           | [string](broken-reference) |          | cosmos bech32 address from the owner of the given Cosmos coins |
| `contract_address` | [string](broken-reference) |          | ERC721 token contract address registered in a token pair       |
| `token_ids`        | [string](broken-reference) | repeated | ERC721 token id registered in a token pair                     |

### MsgConvertNFTResponse

MsgConvertNFTResponse returns no fields

### Msg

Msg defines the erc721 Msg service.

| Method Name     | Request Type                         | Response Type                                | Description                                                                                                                   | HTTP Verb | Endpoint                             |
| --------------- | ------------------------------------ | -------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | --------- | ------------------------------------ |
| `ConvertNFT`    | [MsgConvertNFT](broken-reference)    | [MsgConvertNFTResponse](broken-reference)    | ConvertNFT mints a ERC721 representation of the native Cosmos nft that is registered on the token mapping.                    | GET       | /uptick/erc721/v1/tx/convert\_nft    |
| `ConvertERC721` | [MsgConvertERC721](broken-reference) | [MsgConvertERC721Response](broken-reference) | ConvertERC721 mints a native Cosmos coin representation of the ERC721 token contract that is registered on the token mapping. | GET       | /uptick/erc721/v1/tx/convert\_erc721 |

## Scalar Value Types

| .proto Type | Notes                                                                                                                                           | C++    | Java       | Python      | Go      | C#         | PHP            | Ruby                           |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ---------- | ----------- | ------- | ---------- | -------------- | ------------------------------ |
| double      |                                                                                                                                                 | double | double     | float       | float64 | double     | float          | Float                          |
| float       |                                                                                                                                                 | float  | float      | float       | float32 | float      | float          | Float                          |
| int32       | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint32 instead. | int32  | int        | int         | int32   | int        | integer        | Bignum or Fixnum (as required) |
| int64       | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint64 instead. | int64  | long       | int/long    | int64   | long       | integer/string | Bignum                         |
| uint32      | Uses variable-length encoding.                                                                                                                  | uint32 | int        | int/long    | uint32  | uint       | integer        | Bignum or Fixnum (as required) |
| uint64      | Uses variable-length encoding.                                                                                                                  | uint64 | long       | int/long    | uint64  | ulong      | integer/string | Bignum or Fixnum (as required) |
| sint32      | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int32s.                            | int32  | int        | int         | int32   | int        | integer        | Bignum or Fixnum (as required) |
| sint64      | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int64s.                            | int64  | long       | int/long    | int64   | long       | integer/string | Bignum                         |
| fixed32     | Always four bytes. More efficient than uint32 if values are often greater than 2^28.                                                            | uint32 | int        | int         | uint32  | uint       | integer        | Bignum or Fixnum (as required) |
| fixed64     | Always eight bytes. More efficient than uint64 if values are often greater than 2^56.                                                           | uint64 | long       | int/long    | uint64  | ulong      | integer/string | Bignum                         |
| sfixed32    | Always four bytes.                                                                                                                              | int32  | int        | int         | int32   | int        | integer        | Bignum or Fixnum (as required) |
| sfixed64    | Always eight bytes.                                                                                                                             | int64  | long       | int/long    | int64   | long       | integer/string | Bignum                         |
| bool        |                                                                                                                                                 | bool   | boolean    | boolean     | bool    | bool       | boolean        | TrueClass/FalseClass           |
| string      | A string must always contain UTF-8 encoded or 7-bit ASCII text.                                                                                 | string | String     | str/unicode | string  | string     | string         | String (UTF-8)                 |
| bytes       | May contain any arbitrary sequence of bytes.                                                                                                    | string | ByteString | str         | \[]byte | ByteString | string         | String (ASCII-8BIT)            |
