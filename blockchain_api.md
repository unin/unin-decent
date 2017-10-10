# DECENT Blockchain API Document

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:0 orderedList:0 -->

- [1. Introduction](#1-introduction)
	- [1.1 How to call blockchain API](#11-how-to-call-blockchain-api)
		- [1.1.1 HTTP Calls](#111-http-calls)
		- [1.1.2 WebSocket Calls](#112-websocket-calls)
	- [1.2 Category](#12-category)
- [2 API Definition](#2-api-definition)
	- [2.1 Login APIs](#21-login-apis)
		- [LOGIN](#login)
			- [login](#login)
		- [REGISTRATION](#registration)
			- [network_broadcast](#networkbroadcast)
			- [database](#database)
			- [history](#history)
			- [network_node](#networknode)
			- [crypto](#crypto)
			- [debug](#debug)
			- [messaging](#messaging)
	- [2.2 Database APIs](#22-database-apis)
		- [Subscriptions](#subscriptions)
			- [set_subscribe_callback](#setsubscribecallback)
			- [set_pending_transaction_callback](#setpendingtransactioncallback)
			- [set_block_applied_callback](#setblockappliedcallback)
			- [cancel_all_subscriptions](#cancelallsubscriptions)
			- [get_subscription](#getsubscription)
			- [list_active_subscriptions_by_consumer](#listactivesubscriptionsbyconsumer)
			- [list_subscriptions_by_consumer](#listsubscriptionsbyconsumer)
			- [list_active_subscriptions_by_author](#listactivesubscriptionsbyauthor)
			- [list_subscriptions_by_author](#listsubscriptionsbyauthor)
		- [Blocks and transactions](#blocks-and-transactions)
			- [get_block_header](#getblockheader)
			- [get_block](#getblock)
			- [get_transaction](#gettransaction)
			- [get_recent_transaction_by_id](#getrecenttransactionbyid)
		- [GLOBALS](#globals)
			- [get_chain_properties](#getchainproperties)
			- [get_global_properties](#getglobalproperties)
			- [get_config](#getconfig)
			- [get_chain_id](#getchainid)
			- [get_dynamic_global_properties](#getdynamicglobalproperties)
		- [KEYS](#keys)
			- [get_key_references](#getkeyreferences)
			- [generate_content_keys](#generatecontentkeys)
			- [restore_encryption_key](#restoreencryptionkey)
		- [ACCOUNTS](#accounts)
			- [get_accounts](#getaccounts)
			- [get_full_accounts](#getfullaccounts)
			- [get_account_by_name](#getaccountbyname)
			- [get_account_references](#getaccountreferences)
			- [lookup_account_names](#lookupaccountnames)
			- [lookup_accounts](#lookupaccounts)
			- [get_account_count](#getaccountcount)
		- [BALANCES](#balances)
			- [get_account_balances](#getaccountbalances)
			- [get_named_account_balances](#getnamedaccountbalances)
			- [get_vesting_balances](#getvestingbalances)
		- [ASSETS](#assets)
			- [get_assets](#getassets)
			- [list_assets](#listassets)
			- [lookup_asset_symbols](#lookupassetsymbols)
			- [get_real_supply](#getrealsupply)
		- [MINERS](#miners)
			- [get_miners](#getminers)
			- [get_miner_by_account](#getminerbyaccount)
			- [lookup_miner_accounts](#lookupmineraccounts)
			- [get_miner_count](#getminercount)
		- [VOTES](#votes)
			- [lookup_vote_ids](#lookupvoteids)
		- [AUTHORITY & VALIDATION](#authority-validation)
			- [get_transaction_hex](#gettransactionhex)
			- [get_required_signatures](#getrequiredsignatures)
			- [get_potential_signatures](#getpotentialsignatures)
			- [verify_authority](#verifyauthority)
			- [verify_account_authority](#verifyaccountauthority)
			- [validate_transaction](#validatetransaction)
			- [get_required_fees](#getrequiredfees)
		- [PROPOSED TRANSACTIONS](#proposed-transactions)
			- [get_proposed_transactions](#getproposedtransactions)
		- [BLOCK](#block)
			- [head_block_time](#headblocktime)
			- [get_new_asset_per_block](#getnewassetperblock)
			- [get_asset_per_block_by_block_num](#getassetperblockbyblocknum)
			- [get_time_to_maint_by_block_time](#gettimetomaintbyblocktime)
		- [CONTENTS](#contents)
			- [set_content_update_callback](#setcontentupdatecallback)
			- [get_content](#getcontent)
			- [search_content](#searchcontent)
			- [get_feeds_by_miner](#getfeedsbyminer)
		- [PUBLISHERS & SEEDERS](#publishers-seeders)
			- [list_publishing_managers](#listpublishingmanagers)
			- [list_publishers_by_price](#listpublishersbyprice)
			- [list_seeders_by_upload](#listseedersbyupload)
			- [list_seeders_by_region](#listseedersbyregion)
			- [list_seeders_by_rating](#listseedersbyrating)
			- [get_seeder](#getseeder)
		- [BUYINGS](#buyings)
			- [get_open_buyings](#getopenbuyings)
			- [get_open_buyings_by_URI](#getopenbuyingsbyuri)
			- [get_open_buyings_by_consumer](#getopenbuyingsbyconsumer)
			- [get_buying_by_consumer_URI](#getbuyingbyconsumeruri)
			- [get_buying_history_objects_by_consumer](#getbuyinghistoryobjectsbyconsumer)
			- [get_buying_objects_by_consumer](#getbuyingobjectsbyconsumer)
		- [DCT](#dct)
			- [price_to_dct](#pricetodct)
	- [2.3 History APIs](#23-history-apis)
		- [ACCOUNTS](#accounts)
			- [get_account_history](#getaccounthistory)
			- [get_relative_account_history](#getrelativeaccounthistory)
	- [2.4 Network Broadcast APIs](#24-network-broadcast-apis)
		- [TRANSACTIONS](#transactions)
			- [broadcast_transaction](#broadcasttransaction)
			- [broadcast_transaction_with_callback](#broadcasttransactionwithcallback)
		- [BLOCK](#block)
			- [broadcast_block](#broadcastblock)
	- [2.5 Network Node APIs](#25-network-node-apis)
		- [OBTAIN NETWORK INFORMATION](#obtain-network-information)
			- [get_info](#getinfo)
			- [get_connected_peers](#getconnectedpeers)
			- [get_potential_peers](#getpotentialpeers)
			- [get_advanced_node_parameters](#getadvancednodeparameters)
		- [CHANGE NETWORK SETTINGS](#change-network-settings)
			- [add_node](#addnode)
			- [set_advanced_node_parameters](#setadvancednodeparameters)
			- [seeding_startup](#seedingstartup)

<!-- /TOC -->

# 1. Introduction

## 1.1 How to call blockchain API

### 1.1.1 HTTP Calls

HTTP call are only supported by database APIs. Starting decentd will by default expose port 8090 as HTTP endpoint. These APIs can be called via any HTTP Client or compatible SDK for multiple programming languages.

Both request and response of these APIs are JSON formated. The request must follow JSON-RPC 2.0 specifications, including four base elements:

1. id (any integer specified, simply to remark the sequence of API call)
2. method (the name of API to be revoked)
3. params (a list of parameters of this API)

**request:**   
``  > {
	"jsonrpc": "2.0",
	"method": "head_block_time",
	"params": [],
	"id": 1
}``

**response:**    
`` < {
    "id": 1,
    "result": "2017-10-06T10:49:35"
}``


### 1.1.2 WebSocket Calls

APIs of all categories, e.g. database, login, network_node, network_broadcast, can be called via WebSocket. Starting decentd will by default expose port 8090 as WebSocket endpoint. These APIs can be called via any Websocket Client or compatible SDK for multiple programming languages.

Both request and response of these APIs are JSON formated. The request must follow JSON-RPC 2.0 specifications, including four base elements:

1. id (any integer specified, simply to remark the sequence of API call)
2. method (always "call" in our case)
3. params (a list of parameters, the first element is "API identifier", the second element is the name of API to be revoked)

**request:**    
`` > {
  "id": 10,
  "method": "call",
  "params": [
    1,
    "messaging",
    []
  ]
}``  

**response:**  
`` < {
  "id": 1,
  "result": 8
}``



## 1.2 Category


1. Login  
**Description:** A series of APIs to login to the RPC server and get API identifiers.  
**Identifier:** 1  
**Protocol:** WebSocket      

2. Database  
**Description:** A series of APIs to query data from DECENT network which is visible to anyone.  
**Identifier:** 0  
**Protocol:**  WebSocket, HTTP   

3. history  
**Description:** A series of APIs to query historical data related to the account.  
**Identifier:** An integer greater than 1, depends on sequence of invoke.  
**Protocol:** WebSocket  

4. network_broadcast  
**Description:** A series of APIs to broadcast state to the network.  
**Identifier:** An integer greater than 1, depends on sequence of invoke.  
**Protocol:** WebSocket  

5. network_node  
**Description:** A series of APIs to manage network nodes.  
**Identifier:** An integer greater than 1, depends on sequence of invoke.  
**Protocol:** WebSocket  




# 2 API Definition

## 2.1 Login APIs

### LOGIN

#### login
**Description:** Login to RPC server in current session.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| user | string | ... |
| password | string | ... |

**Returns:** response status  
**Example:**  
``  > {
  "id": 10,
  "method": "call",
  "params": [
    1,
    "login",
    [
      "myusername",
      "mypassword"
    ]
  ]
} ``  

``  < {
  "id": 10,
  "result": true
}``

----

### REGISTRATION

#### network_broadcast
**Description:** Get network_broadcast API identifier.  
**Returns:** response status  
**Example:**  
`` > {
  "id": 10,
  "method": "call",
  "params": [
    1,
    "network_broadcast",
    []
  ]
}  ``  

`` < {
  "id": 1,
  "result": 2
}``

----

#### database
**Description:** Get database API identifier.    
**Returns:** response status  
**Example:**  
`` > {
  "id": 10,
  "method": "call",
  "params": [
    1,
    "database",
    []
  ]
}``  

`` < {
  "id": 1,
  "result": 3
}``

----

#### history
**Description:** Get history API identifier.  
**Returns:** response status    
**Example:**  
`` > {
  "id": 10,
  "method": "call",
  "params": [
    1,
    "history",
    []
  ]
}``  

`` < {
  "id": 1,
  "result": 4
}``

----

#### network_node
**Description:** Get network_node API identifier.  
**Returns:** response status  
**Example:**  
`` > {
  "id": 10,
  "method": "call",
  "params": [
    1,
    "network_node",
    []
  ]
}``  

`` < {
  "id": 1,
  "result": 5
}``

----

#### crypto
**Description:** Get network_broadcast API identifier.  
**Returns:** response status  
**Example:**  
`` > {
  "id": 10,
  "method": "call",
  "params": [
    1,
    "crypto",
    []
  ]
}``  

`` < {
  "id": 1,
  "result": 6
}``

----

#### debug
**Description:** Get debug API identifier.  
**Returns:** response status  
**Example:**  
`` > {
  "id": 10,
  "method": "call",
  "params": [
    1,
    "debug",
    []
  ]
}``  

`` < {
  "id": 1,
  "result": 7
}``

----

#### messaging
**Description:** Get messaging API identifier.  
**Returns:** response status  
**Example:**  
`` > {
  "id": 10,
  "method": "call",
  "params": [
    1,
    "messaging",
    []
  ]
}``  

`` < {
  "id": 1,
  "result": 8
}``

----

## 2.2 Database APIs

### Subscriptions

#### set_subscribe_callback
**Description:** Set callback function when subscribe.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| cb | confirmation_callback | callback confirmation |
| clear_filter | bool | ... |

**Returns:** response status    

----

#### set_pending_transaction_callback
**Description:** Set callback function when pending transaction.   
**Parameters:**  

| name | type | desc |
| -------- | -------- | -------- |  
| cb | confirmation_callback | callback confirmation |

**Returns**: response status    

----

#### set_block_applied_callback
**Method:** set_block_applied_callback  
**Description:** set callback function when block applied   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| cb | confirmation_callback | callback confirmation |

**Returns**: response status  

----

#### cancel_all_subscriptions
**Description:** Stop receiving any notifications.   
**Returns:** response status  
**Note:** This unsubscribes from all subscribed markets and objects.

----

#### get_subscription  
**Description:** Query for a subscription object by ID.                     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| sid	| subscription_id_type | ID of the subscription to retrieve |   	

**Returns:** subscription object              

----

#### list_active_subscriptions_by_consumer  
**Description:** Query for a list of active (not expired) subscriptions to account (consumer).                     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account | account_id_type | account ID |
| count | uint32_t |	maximum number of subscription objects to fetch (must not exceed 100) |

**Returns:** list of subscription object              

----

#### list_subscriptions_by_consumer
**Description:** Query for a list of subscriptions subscribed to account (consumer).  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account | account_id_type | account ID |
| count | uint32_t |	maximum number of subscription objects to fetch (must not exceed 100) |

**Returns:** list of subscription object              

----

#### list_active_subscriptions_by_author  
**Description:** Query for a list of active (not expired) subscriptions to account (author).                     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account | account_id_type | account ID |
| count | uint32_t |	maximum number of subscription objects to fetch (must not exceed 100) |

**Returns:** list of subscription object

----

#### list_subscriptions_by_author
**Description:** Query for a list of subscriptions subscribed to account. (author)                     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account | account_id_type | account ID |
| count | uint32_t |	maximum number of subscription objects to fetch (must not exceed 100) |

**Returns:** list of subscription object

----

### Blocks and transactions

#### get_block_header
**Description:** Retrieve block header.  
**Parameters:**  

| name | type | desc |
| -------- | -------- | -------- |
| block_num | uint32_t | 	height of the block whose header should be returned |

**Returns:** header of the referenced block  
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_block_header",
	"params": [1658953],
	"id": 1
}``

``  < {"id": 1,
        "result": {
        "previous": "0019504822e648793fbdc842f541b7bb468de492",
        "timestamp": "2017-10-06T08:32:50",
        "miner": "1.4.165",
        "transaction_merkle_root": "0000000000000000000000000000000000000000",
        "extensions": []
    }
}``

----

#### get_block  
**Description:** Retrieve a full, signed block.   
**Parameters:**  

| name | type | desc |
| -------- | -------- | -------- |
| block_num | uint32_t | 	height of the block to be returned |

**Returns:** referenced block  
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_block",
	"params": [1658953],
	"id": 1
}``

``  > {
    "id": 1,
    "result": {
        "previous": "0019504822e648793fbdc842f541b7bb468de492",
        "timestamp": "2017-10-06T08:32:50",
        "miner": "1.4.165",
        "transaction_merkle_root": "0000000000000000000000000000000000000000",
        "extensions": [],
        "miner_signature": "1f5f0450e22edcd78fb87a7ad03cb91d26553215e0eff185bc6416addc6b202f01286adab94022f309d9cebd3a1c9c9d838ce148e4121b011db6889e5ea94a27c9",
        "transactions": []
    }
}``

----

#### get_transaction
**Description:**  Fetch an individual transaction.   
**Parameters:**  

| name | type | desc |
| -------- | -------- | -------- |
| block_num | uint32_t | 	ID of the block |
| trx_in_block | uint32_t | the position of the transaction within the block |

**Returns:** referenced transaction  
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_transaction",
	"params": [1660536, 1],
	"id": 1
}``

`` < ...``

----

#### get_recent_transaction_by_id
**Description:** If the transaction has not expired, this method will return the transaction for the given ID or it will return NULL if it is not known. Just because it is not known does not mean it wasn’t included in the blockchain.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| id | string |	ID of the transaction to retrieve |

**Returns:** referenced transaction  
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_recent_transaction_by_id",
	"params": ["1"],
	"id": 1
}``

``  < {
    "id": 1,
    "result": null
}``

----

### GLOBALS


#### get_chain_properties
**Description:** Retrieve the chain_property_object associated with the chain.    
**Returns:** properties associated with current chain  
**Example:**    
``  > {
	"jsonrpc": "2.0",
	"method": "get_chain_properties",
	"params": [],
	"id": 1
}``

``  > {
    "id": 1,
    "result": {
        "id": "2.9.0",
        "chain_id": "4777b283f8006237590c67a5001fb62e14fdfd2c0f5f5afb55e687ae8082d483",
        "immutable_parameters": {
            "min_miner_count": 11,
            "num_special_accounts": 0,
            "num_special_assets": 0
        }
    }
}``

----

#### get_global_properties  
**Description:** Retrieve the current global_property_object.     
**Returns:** global properties  
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_global_properties",
	"params": [],
	"id": 1
}``

``  > ...``

----

#### get_config
**Description:** Retrieve compile-time constants.   
**Returns:** configurations   
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_config",
	"params": [],
	"id": 1
}``

``  < {
    "id": 1,
    "result": {
        "GRAPHENE_SYMBOL": "DCT",
        "GRAPHENE_ADDRESS_PREFIX": "DCT",
        "GRAPHENE_MIN_ACCOUNT_NAME_LENGTH": 5,
        "GRAPHENE_MAX_ACCOUNT_NAME_LENGTH": 63, ...
    }
}``

----

#### get_chain_id
**Description:** Get the chain ID.   
**Returns:** chain ID  
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_chain_id",
	"params": [],
	"id": 1
}``

``  < {
    "id": 1,
    "result": "4777b283f8006237590c67a5001fb62e14fdfd2c0f5f5afb55e687ae8082d483"
}``

----

#### get_dynamic_global_properties
**Description:** Retrieve the current dynamic_global_property_object.    
**Returns:** dynamic global properties    
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_dynamic_global_properties",
	"params": [],
	"id": 1
}``

``  > {
    "id": 1,
    "result": {
        "id": "2.1.0",
        "head_block_number": 1660805,
        "head_block_id": "0019578573bc1e4952ed2050758dd4ec950805d0",
        "time": "2017-10-06T11:07:10", ...
    }
}``

----

### KEYS

#### get_key_references
**Description:** Query for all accounts that refer to the key in their owner or active authorities.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| key | vector&lt;public_key_type> | list of public keys |

**Returns:** list of account IDs  
**Example:**   
``  > {
	"jsonrpc": "2.0",
	"method": "get_key_references",
	"params": [["DCT7e15SHKeWhNZfidDdi8D515bQ13XFirog4XjYwnkznLL", "DCT7e15SHKeWi8D515bQ13xUuHFrXFirog4XjYwnkznLL"]],
	"id": 1
}``

``  < {
    "id": 1,
    "result": [
        [
            "1.2.5548"
        ],
        [
            "1.2.5549"
        ]
    ]
}``

----

#### generate_content_keys  
**Description:** Generate keys for new content submission.                
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| seeders | vector&lt;account_id_type> | list of seeder account IDs |

**Returns:** generated key and particles                  

----

#### restore_encryption_key  
**Description:** Restores AES key.           
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| el_gamal_priv_key_string | DIntegerString  | private key | 	
| buying | buying_id_type | buying ID |

**Returns:** AES key              

----

### ACCOUNTS

#### get_accounts
**Description:** Get a list of accounts by ID.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_ids |  vector&lt;account_id_type> | IDs of the accounts to retrieve |

**Returns:** list of accounts      
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_accounts",
	"params": [["1.2.5548"]],
	"id": 1
}``

``  < {
    "id": 1,
    "result": [
        {
            "id": "1.2.5548",
            "registrar": "1.2.21",
            "name": "u24e69b70a09e16b0dab800e26d947dfd",
            "owner": {
                "weight_threshold": 1,
                "account_auths": [],
                "key_auths": [
                    [
                        "DCT7e15SHKeWhNZfidDdi8D515bQ13xUuHFrXFirog4XjYwnkznLL",
                        1
                    ]
                ]
            }, ...
}``  
**Note:** This function has semantics identical to get_objects

----

#### get_full_accounts
**Description:** Retrieve all objects relevant to the specified accounts and subscribe to updates.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| names_or_ids | vector&lt;string | the name or ID of an account to retrieve |
| subscribe | bool | 	true to subscribe to updates  |

**Returns:** map of string from name or id to the account  
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_full_accounts",
	"params": [["1.2.5548"], false ],
	"id": 1
}``

``  < {
    "id": 1,
    "result": [
        [
            "1.2.5548",
            {
                "account": {
                    "id": "1.2.5548",
                    "registrar": "1.2.21", ...
}``

----

#### get_account_by_name
**Description:** Query for an account by name.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| name | string |	name of the account to retrieve |

**Returns:** referenced account    
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_account_by_name",
	"params": ["u24e69b70a09e16b0dab800e26d947dfd"],
	"id": 1
}``

``  < {
    "id": 1,
    "result": {
        "id": "1.2.5548",
        "registrar": "1.2.21", ...
}``

----

#### get_account_references
**Description:** Query for all accounts that refer to the account id in their owner or active authorities.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| account_id | string | account ID to be searched |

**Returns:** list of account IDs    
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_account_references",
	"params": ["1.2.5548"],
	"id": 1
}``

``  < {
    "id": 1,
    "result": []
}``

----

#### lookup_account_names
**Description:** Get a list of accounts by name.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| account_names | vector&lt;string> | names of the accounts to retrieve |

**Returns:** list of accounts    
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "lookup_account_names",
	"params": [["u24e69b70a09e16b0dab800e26d947dfd"]],
	"id": 1
}``

``  < {
    "id": 1,
    "result": [
        {
            "id": "1.2.5548",
            "registrar": "1.2.21", ...
}``  
**Note:** This function has semantics identical to get_objects.

----

#### lookup_accounts
**Description:** Get names and IDs for registered accounts.     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| lower_bound_name | string | lower bound of the first name to return |
| limit	| uint32_t | maximum number of results to return (must not exceed 10000) |

**Returns:** map of account name to ID    
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "lookup_accounts",
	"params": ["a", 100 ],
	"id": 1
}``

``  < {
    "id": 1,
    "result": [
        [
            "aaaa-jesus-saves",
            "1.2.3083"
        ],
        [
            "aaaaaaaaaaaaaaaa",
            "1.2.3169"
        ],
        [
            "abcde",
            "1.2.3547"
        ],
        [
            "adilminer",
            "1.2.3495"
        ],
        [
            "adsactly",
            "1.2.3062"
        ],
        [
            "adult",
            "1.2.3164"
        ],
        [
            "agoric.systems",
            "1.2.2713"
        ],
        [
            "alcurex",
            "1.2.3072"
        ],
        [
            "alexalexrus",
            "1.2.4753"
        ],
        [
            "alexfff17",
            "1.2.3227"
        ]
    ]
}``

----

#### get_account_count
**Description:** Get the total number of accounts registered with the blockchain.         
**Returns:** number of registered account     
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_account_count",
	"params": [],
	"id": 1
}``

``  < {
    "id": 1,
    "result": 6655
}``

----

### BALANCES

#### get_account_balances
**Description:** Get an account’s balances in various assets.          
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
|	id | account_id_type | ID of the account to get balances for |   
| assets | flat_set&lt;asset_id_type> | IDs of the assets to get balances of; if empty, get all assets account has a balance in  |

**Returns:** list account balance       
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_account_balances",
	"params": ["1.2.5548", [] ],
	"id": 1
}``

``  < {
    "id": 1,
    "result": [
        {
            "amount": 500000,
            "asset_id": "1.3.0"
        }
    ]
}``

----

#### get_named_account_balances
**Description:** Semantically equivalent to get_account_balances, but takes a name instead of an ID.           
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
|	name | string | name of the account to get balances for IDs of the assets to get balances of; if empty, get all assets account has a balance in |   
| assets | flat_set&lt;asset_id_type> | 	IDs of the assets to get balances of; if empty, get all assets account has a balance in  |

**Returns:** account balance       
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_named_account_balances",
	"params": ["u24e69b70a09e16b0dab800e26d947dfd", [] ],
	"id": 1
}``

``  < {
    "id": 1,
    "result": [
        {
            "amount": 500000,
            "asset_id": "1.3.0"
        }
    ]
}``

----

#### get_vesting_balances
**Description:** Query for vesting balance.         
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_id | account_id_type | ... |

**Returns:** vesting balance       
**Example:**   
``  > {
	"jsonrpc": "2.0",
	"method": "get_vesting_balances",
	"params": ["1.2.5548"],
	"id": 1
}``

``  < {
    "id": 1,
    "result": []
}``

----

### ASSETS

#### get_assets
**Description:** Get a list of assets by ID.           
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| asset_ids	| vector&lt;asset_id_type> | IDs of the assets to retrieve |

**Returns:** list of assets       
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_assets",
	"params": [["1.3.2"]],
	"id": 1
}``

``  < {
    "id": 1,
    "result": [
        {
            "id": "1.3.2",
            "symbol": "EUR",
            "precision": 4,
            "issuer": "1.2.20",
            "description": "Euro",
            "max_supply": 0,
            "monitored_asset_opts": {
                "feeds": [
                    [
                        "1.2.1948",
                        [
                            "2017-10-05T19:05:05",
                            {
                                "core_exchange_rate": {
                                    "base": {
                                        "amount": 543964203,
                                        "asset_id": "1.3.2"
                                    },
                                    "quote": {
                                        "amount": "10000000000000",
                                        "asset_id": "1.3.0"
                                    }
                                }
                            }
                        ]
                    ],
                    [
                        "1.2.2044",
                        [
                            "2017-09-28T12:17:50",
                            {
                                "core_exchange_rate": {
                                    "base": {
                                        "amount": "5339529209",
                                        "asset_id": "1.3.2"
                                    },
                                    "quote": {
                                        "amount": "100000000000000",
                                        "asset_id": "1.3.0"
                                    }
                                }
                            }
                        ]
                    ],
                    [
                        "1.2.2064",
                        [
                            "2017-09-11T13:00:00",
                            {
                                "core_exchange_rate": {
                                    "base": {
                                        "amount": "5751964929",
                                        "asset_id": "1.3.2"
                                    },
                                    "quote": {
                                        "amount": "10000000000",
                                        "asset_id": "1.3.0"
                                    }
                                }
                            }
                        ]
                    ], ...
    ]
}``  

**Note:** This function has semantics identical to get_objects.

----

#### list_assets
**Description:** Get assets alphabetically by symbol name.            
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| lower_bound_symbol | string | lower bound of symbol names to retrieve |
| limit	| uint32_t | maximum number of assets to fetch (must not exceed 100) |

**Returns:** list of assets       
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "list_assets",
	"params": ["DCT", 2],
	"id": 1
}``

``  < {
    "id": 1,
    "result": [
        {
            "id": "1.3.0",
            "symbol": "DCT",
            "precision": 8,
            "issuer": "1.2.1",
            "description": "",
            "max_supply": "7319777577456900",
            "dynamic_asset_data_id": "2.3.0"
        }, ...
    ]
}``

----

#### lookup_asset_symbols
**Description:** Get a list of assets by symbol.          

**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| symbols_or_ids | vector&lt;string> | symbols or stringified IDs of the assets to retrieve |

**Returns:** list of assets       
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "lookup_asset_symbols",
	"params": [["1.3.0", "1.3.1", "1.3.2"]],
	"id": 1
}``

``  < {
    "id": 1,
    "result": [
        {
            "id": "1.3.0",
            "symbol": "DCT",
            "precision": 8,
            "issuer": "1.2.1",
            "description": "",
            "max_supply": "7319777577456900",
            "dynamic_asset_data_id": "2.3.0"
        },  ...
    ]
}``

**Note:** This function has semantics identical to get_objects.

----

#### get_real_supply    
**Description:** query for current core asset supply.   
**Returns:** number of assets       

----

### MINERS

#### get_miners
**Description:** Get a list of miners by ID.          
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| miner_ids | vector&lt;miner_id_type> |	IDs of the miners to retrieve |

**Returns:** list of miners       

----

#### get_miner_by_account
**Description:** Get the miner owned by a given account.          
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| account	| account_id_type | the ID of the account whose miner should be retrieved |

**Returns:** the miner information       
**Example:**  
``  > {
  "jsonrpc": "2.0",
	"method": "get_miner_by_account",
	"params": ["1.2.5548"],
	"id": 1
}``

`` < {
  "id": 1,
  "result": null
}``

----

#### lookup_miner_accounts
**Description:** Get names and IDs for registered miners.            
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| lower_bound_name	| string | lower bound of the first name to return |
| limit	| uint32_t | maximum number of results to return (must not exceed 1000) |


Returns: map of names to IDs of miners     
Example:  
``  > {
	"jsonrpc": "2.0",
	"method": "get_miner_by_account",
	"params": ["1.2.1", 10 ],
	"id": 1
}``

``  < {
    "id": 1,
    "result": null
}``

----

#### get_miner_count
**Description:** Get the total number of miners registered with the blockchain.              
**Returns:** the number of miners     
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_miner_count",
	"params": [],
	"id": 1
}``

``  < {
    "id": 1,
    "result": 11
}``

----

### VOTES

#### lookup_vote_ids
**Description:** Given a set of votes, return the objects they are voting for.          
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| votes	| vector&lt;vote_id_type> | set of votes, the results will be in the same order as the votes |

**Returns:** voting objects     
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "lookup_vote_ids",
	"params": [[""]],
	"id": 1
}``

``  < {
    "id": 1,
    "result": [
        {
            "id": "1.4.1",
            "miner_account": "1.2.4",
            "last_aslot": 730169,
            "signing_key": "DCT7WajG3BUdorEndqQLtWvYM3xyGjtE9yhxhNDFGqsBoSDc1s35g",
            "vote_id": "0:0",
            "total_votes": 0,
            "url": "",
            "total_missed": 65923,
            "last_confirmed_block_num": 4998
        }
    ]
}``  
**Note:** This will be a mixture of committee_member_object, witness_objects, and worker_objects. The results will be in the same order as the votes. Null will be returned for any vote ids that are not found.

----

### AUTHORITY & VALIDATION

#### get_transaction_hex
**Description:** Get a hexdump of the serialized binary form of a transaction.             
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| trx	| signed_transaction | ... |

* _object trx   
{  
  _int_ ref_block_num,  
  _int_ ref_block_prefix,  
  _int_ expiration,  
  _list of string_ operations,  
  _string_ extensions  
}   

**Returns:** hexdump binary     

----

#### get_required_signatures
**Description:** Take a partially signed transaction and a set of public keys that the owner has the ability to sign for and return the minimal subset of public keys that should add signatures to the transaction.  

| name | type | desc |
| -------- | -------- | -------- |  
| trx	| signed_transaction | ... |
| available_keys | string | 	set of available public keys |

* _object trx_   
{  
  _int_ ref_block_num,  
  _int_ ref_block_prefix,  
  _int_ expiration,  
  _list of string_ operations,  
  _string_ extensions  
}

**Returns:** set of public keys         

----

#### get_potential_signatures
**Description:** Return the set of all public keys that could possibly sign for a given transaction. This call can be used by wallets to filter their set of public keys to just the relevant subset prior to calling get_required_signatures to get the minimum subset.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| trx	| signed_transaction | ... |

* _object trx_   
{  
  _int_ ref_block_num,  
  _int_ ref_block_prefix,  
  _int_ expiration,  
  _list of string_ operations,  
  _string_ extensions  
}

**Returns:** set of public keys     

----

#### verify_authority
**Description:** Verify if a transaction has all of the required signatures.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| trx	| signed_transaction | ... |

* _object trx_   
{  
  _int_ ref_block_num,  
  _int_ ref_block_prefix,  
  _int_ expiration,  
  _list of string_ operations,  
  _string_ extensions  
}

**Returns:** bool       

----

#### verify_account_authority
**Description:** Verify if a signers have enough authority to authorize an account.        
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| name_or_id |	string | the name or id of the account |
| signers	| flat_set&lt;public_key_type> | Set of public keys |

**Returns:** bool       

----

#### validate_transaction
**Description:** Validates a transaction against the current state without broadcasting it on the network.      
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| trx	| signed_transaction | ... |

* _object trx_   
{  
  _int_ ref_block_num,  
  _int_ ref_block_prefix,  
  _int_ expiration,  
  _list of string_ operations,  
  _string_ extensions  
}

**Returns:** bool       

----

#### get_required_fees
**Description:** For each operation calculate the required fee in the specified asset type, if the asset type does not have a valid core_exchange_rate.       
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| ops |	vector&lt;operation> | the set of operations |
| id | asset_id_type | the asset ID |

**Returns:** map of asset type and fee       

----

### PROPOSED TRANSACTIONS

#### get_proposed_transactions
**Description:** Get proposed transactions relevant to the specified account id.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| id | account_id_type | the account ID |


**Returns:** set of proposed transactions         

----

### BLOCK

#### head_block_time
**Description:** Retrieve datetime of the last local block.  
**Returns:** referenced block  
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "head_block_time",
	"params": [],
	"id": 1
}``

`` < {
    "id": 1,
    "result": "2017-10-06T10:49:35"
}``

----

#### get_new_asset_per_block
**Description:** Retrieve the number of asset per block.  
**Returns:** the number of asset per block  
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_new_asset_per_block",
	"params": [],
	"id": 1
}``

``{
    "id": 1,
    "result": 37000000
}``

----

#### get_asset_per_block_by_block_num  
**Description:** Retrieve the number of asset for given block number.  
**Parameters:**  

| name | type | desc |
| -------- | -------- | -------- |
| block_num | uint32_t | 	ID of the block |

**Returns:** the number of asset for given block number  
**Example:**   
``  > {
	"jsonrpc": "2.0",
	"method": "get_asset_per_block_by_block_num",
	"params": [1658953],
	"id": 1
}``

``  > {
    "id": 1,
    "result": 37000000
}``

----

#### get_time_to_maint_by_block_time
**Description:** get time for maintenance for given datetime  
**Parameters:**  

| name | type | desc |
| -------- | -------- | -------- |
| datetime | string | date and time specified |

**Returns:** the number of asset for given block number  
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "get_time_to_maint_by_block_time",
	"params": ["2017-10-06T09:12:54"],
	"id": 1
}``

``  > {
    "id": 1,
    "result": {
        "time_to_maint": 86400,
        "from_accumulated_fees": 677352801,
        "block_interval": 5
    }
}``        

----

### CONTENTS

#### set_content_update_callback
**Description:** Set callback function on content update.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| URI | string | content that are monitored |
| cb | confirmation_callback | callback confirmation |

**Returns:** response status  

----

#### get_content  
**Description:** Retrieve a content by URI.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| URI	| string | URI of the content to retrieve |

**Returns:** content object             

----

#### search_content
**Description:** Search for term in contents (author, title and description).               
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| term | string | search term |
| order | string |	ordering field |
| user | string | content owner |
| region | string | two letter region code |
| id | object_id_type  | the id of content object to start searching from |
| type | string |the application and content type to be filtered |
| count |	uint32_t | maximum number of contents to fetch (must not exceed 100) |

**Returns:** content objects              

----

#### get_feeds_by_miner

----

### PUBLISHERS & SEEDERS

#### list_publishing_managers
**Description:** Query for a list of accounts holding publishing manager status.        
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| lower_bound_name | string |	the name of the first account to return, if the named account does not exist, the list will start at the account that comes after lower bound |
| limit | uint32_t | the maximum number of accounts to return  (must not exceed 100) |

**Returns:** list of accounts    

----

#### list_publishers_by_price  
**Description:** Query for a list of seeders by price (in decreasing order).                 
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| count	| uint32_t | maximum number of seeders to retrieve |

**Returns:** list of seeders              

----

#### list_seeders_by_upload  
**Description:** Query for a list of seeders by total upload (in decreasing order).  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| count	| uint32_t | maximum number of seeders to retrieve |

**Returns:** list of seeders              

----

#### list_seeders_by_region
**Description:** Query for a list of seeders by region (in decreasing order).                   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| count	| uint32_t | maximum number of seeders to retrieve |

**Returns:** list of seeders

----

#### list_seeders_by_rating
**Description:** Query for a list of seeders by rating (in decreasing order).                   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| count	| uint32_t | maximum number of seeders to retrieve |

**Returns:** list of seeders

----

#### get_seeder
Description: Query for a seeder by ID.                   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| ID | account_id_type | ID of the seeder to retrieve |

**Returns:** seeder object              

----

### BUYINGS

#### get_open_buyings
**Description:** Query for a list of open buying.         
**Returns:** list of buying objects         

----

#### get_open_buyings_by_URI
**Description:** Query for a list of open buying by URI.      
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| URI	| string | URI of the buying to retrieve |

**Returns:** list of buying objects         

----

#### get_open_buyings_by_consumer
**Description:** Query for a list of open buying by consumer.      
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |    
| consumer |  account_id_type | consumer of the buying to retrieve |

**Returns:** list of buying objects         

----

#### get_buying_by_consumer_URI
**Description:** Query for a list of open buying by consumer and URI.      
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| consumer |  account_id_type | consumer of the buying to retrieve |
| URI	| string | URI of the buying to retrieve |

**Returns:** list of buying objects         

----

#### get_buying_history_objects_by_consumer
**Description:** Query for history buying objects by consumer.        
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| consumer |  account_id_type | consumer of the buying to retrieve |

**Returns:** list of buying objects         

----

#### get_buying_objects_by_consumer
**Description:** Query for buying objects (open or history) by consumer.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| consumer | account_id_type | consumer of the buying to retrieve |
| order	| string | ordering field |
| id	| object_id_type | the id of buying object to start searching from |
| term	| string | search term |
| count	| uint32_t | maximum number of contents to fetch (must not exceed 100) |

**Returns:** list of buying objects         

----

### DCT

#### price_to_dct
**Description:** Converts price denominated in Monitored asset into DCT, using actual price feed.      
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| price	| asset | price in DCT or monitored asset |

**Returns:** price

----

## 2.3 History APIs

### ACCOUNTS

#### get_account_history  
**Description:** Get operations relevant to the specificed account.     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account	|  	account_id_type  | account ID |
| order | string | ... |
| stop | operation_history_id_type | ID of the earliest operation to retrieve |
| limit	| unsigned  | maximum number of operations to retrieve (must not exceed 100) |
| start	| operation_history_id_type | ID of the most recent operation to retrieve |


**Returns:** list of historical operations       
**Example:**  
``  > {
	"jsonrpc": "2.0",
	"method": "search_account_history",
	"params": ["1.2.5548", "asc", "2.0.0", 10],
	"id": 5
}``

``  < {
    "id": 1,
    "result": [
        {
            "id": "2.17.23193",
            "m_from_account": "1.2.21",
            "m_to_account": "1.2.5548",
            "m_operation_type": 0,
            "m_transaction_amount": {
                "amount": 500000,
                "asset_id": "1.3.0"
            }, ...
}``

----

#### get_relative_account_history  
**Description:** Query for historical operations relevant to given account.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account	|  	account_id_type  | account ID |
| stop | operation_history_id_type | sequence number of earliest operation, 0 is default and will query 'limit' number of operations |
| limit	| unsigned  | maximum number of operations to retrieve (must not exceed 100) |
| start	| operation_history_id_type | sequence number of the most recent operation to retrieve, 0 is default, which will start querying from the most recent operation |

**Returns:** list of historical operations       

----

## 2.4 Network Broadcast APIs

### TRANSACTIONS

#### broadcast_transaction
**Description:** Broadcast a transaction to the network.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| trx	| signed_transaction | the transaction to broadcast |

* _object trx   
{  
  _int_ ref_block_num,  
  _int_ ref_block_prefix,  
  _int_ expiration,  
  _list of string_ operations,  
  _string_ extensions  
}

**Returns:** response status  

----

#### broadcast_transaction_with_callback  
**Description:** This version of broadcast transaction registers a callback method that will be called when the transaction is included into a block. The callback method includes the transaction id, block number, and transaction number in the block.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| cb | confirmation_callback | callback confirmation |
| trx	| signed_transaction | transaction object |

* _object transaction_   
{  
  _int_ ref_block_num,  
  _int_ ref_block_prefix,  
  _int_ expiration,  
  _list of string_ operations,  
  _string_ extensions  
}

**Returns:** response status  

----

### BLOCK

#### broadcast_block
**Description:** Broadcast a block to the network.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| b	| signed_block | block object |

* _object block_   
{  
  _list of object transaction_ {_int_ ref_block_num, _int_ ref_block_prefix, _int_ expiration, _list of string_ operations, _string_ extensions }   
  _string_ signature_type,  
  _string_ block_id_type,  
  _string_ timestamp,  
  _string_ miner,  
  _string_ transaction_merkle_root,  
  _string_ extensions  
}

**Returns:** response status  

----

## 2.5 Network Node APIs

### OBTAIN NETWORK INFORMATION

#### get_info
**Description:** Retrieve general network information.  
**Returns:** network information  
**Example:**  
``  > {
  "id": 2,
  "method": "call",
  "params": [
    4,
    "get_info",
    []
  ]
}``

``  < {
  "id": 2,
  "result": {
    "listening_on": "0.0.0.0:39435",
    "node_public_key": "03a588497d473fa2ed85c7b8f50125f0a3433d4bcee432302c32db408208f987e8",
    "node_id": "f38b89d5dafbd09f55e3fd1a195ef600c1d9d09a3290c9906f38d86b4d165c6dff",
    "firewalled": "firewalled",
    "connection_count": 0
  }
}``

----

#### get_connected_peers
**Description:** Get status of all current connections to peers.     
**Returns:** list of connected peers  
**Example:**  
``  > {
  "id": 2,
  "method": "call",
  "params": [
    4,
    "get_connected_peers",
    [
      ""
    ]
  ]
}``

``  < {
  "id": 2,
  "result": null
}``

----

#### get_potential_peers
**Description:** Return list of potential peers.     
**Returns:** list of potential peers  
**Example:**  
``  > {
  "id": 2,
  "method": "call",
  "params": [
    4,
    "get_potential_peers",
    [
      ""
    ]
  ]
}``

``  < {
  "id": 2,
  "result": [
    {
      "endpoint": "45.32.154.218:40000",
      "last_seen_time": "1970-01-01T00:00:00",
      "last_connection_disposition": "last_connection_failed",
      "last_connection_attempt_time": "2017-10-11T02:37:03",
      "number_of_successful_connection_attempts": 0,
      "number_of_failed_connection_attempts": 86,
      "last_error": {
        "code": 0,
        "name": "exception",
        "message": "unspecified",
        "stack": [
          {
            "context": {
              "level": "error",
              "file": "asio.cpp",
              "line": 60,
              "method": "error_handler",
              "hostname": "",
              "thread_name": "asio",
              "timestamp": "2017-10-11T02:37:06"
            },
            "format": "${message} ",
            "data": {
              "message": "No route to host"
            }
          }
        ]
      }
    }, ...
  ]
}``

----

#### get_advanced_node_parameters
**Description:** Get advanced node parameters, such as desired and max number of connections.     
**Returns:** node parameters  
**Example:**
``  > {
  "id": 2,
  "method": "call",
  "params": [
    4,
    "get_advanced_node_parameters",
    [
      ""
    ]
  ]
}``

``  < {
  "id": 2,
  "result": {
    "peer_connection_retry_timeout": 30,
    "desired_number_of_connections": 20,
    "maximum_number_of_connections": 200,
    "maximum_number_of_blocks_to_handle_at_one_time": 200,
    "maximum_number_of_sync_blocks_to_prefetch": 2000,
    "maximum_blocks_per_peer_during_syncing": 200
  }
}``

----

### CHANGE NETWORK SETTINGS

#### add_node
**Description:** Connect to a new peer.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| ep | endpoint | the IP:Port of the peer to connect to |

**Returns:** response status    
**Example:**  
``  > {
  "id": 2,
  "method": "call",
  "params": [
    4,
    "add_node",
    [
      "66.70.188.105:40000"
    ]
  ]
}``

``  < {
  "id": 2,
  "result": null
}``

----

#### set_advanced_node_parameters
**Description:** Set advanced node parameters.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| params | variant_object |	a JSON object containing the name/value pairs for the parameters to set

* _object params   
{  
  _int_ peer_connection_retry_timeout,  
  _int_ desired_number_of_connections,  
  _int_ maximum_number_of_connections,  
  _int_ maximum_number_of_blocks_to_handle_at_one_time,  
  _int_ maximum_number_of_sync_blocks_to_prefetch,  
  _int_ maximum_blocks_per_peer_during_syncing  
}   

**Returns:** response status  
**Example:**  
`` > {
  "id": 2,
  "method": "call",
  "params": [
    4,
    "set_advanced_node_parameters",
    [
      {
        "peer_connection_retry_timeout": 30,
        "desired_number_of_connections": 20,
        "maximum_number_of_connections": 200,
        "maximum_number_of_blocks_to_handle_at_one_time": 200,
        "maximum_number_of_sync_blocks_to_prefetch": 2000,
        "maximum_blocks_per_peer_during_syncing": 200
      }
    ]
  ]
}``

``  < {
  "id": 2,
  "result": null
}``

----

#### seeding_startup
**Description:** Start seeding plugin from running application.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_id | account_id_type | ID of account controlling this seeder |
| content_private_key | DInteger |	El Gamal content private key |
| seeder_private_key	| private_key | private key of the account controlling this seeder |
| free_space | uint64_t | allocated disk space (in MegaBytes) |
| seeding_price	| uint32_t | price per MegaBytes |
| packages_path	| string | packages storage path |

**Returns:** response status    

----
