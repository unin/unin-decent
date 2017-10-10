# DECENT Wallet API Document

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:0 orderedList:0 -->

- [1. Introduction](#1-introduction)
	- [1.1 How to call wallet API](#11-how-to-call-wallet-api)
		- [1.1.1 HTTP Calls](#111-http-calls)
		- [1.1.2 WebSocket Calls](#112-websocket-calls)
- [2. API Definition](#2-api-definition)
	- [2.1 General APIs](#21-general-apis)
		- [GENERAL](#general)
			- [help](#help)
			- [gethelp](#gethelp)
			- [info](#info)
			- [about](#about)
			- [network_add_nodes](#networkaddnodes)
			- [network_get_connected_peers](#networkgetconnectedpeers)
	- [2.2 Wallet APIs](#22-wallet-apis)
		- [WALLET](#wallet)
			- [is_new](#isnew)
			- [is_locked](#islocked)
			- [lock](#lock)
			- [unlock](#unlock)
			- [set_password](#setpassword)
			- [dump_private_keys](#dumpprivatekeys)
			- [import_key](#importkey)
			- [import_accounts](#importaccounts)
			- [import_account_keys](#importaccountkeys)
			- [suggest_brain_key](#suggestbrainkey)
			- [get_private_key](#getprivatekey)
			- [load_wallet_file](#loadwalletfile)
			- [normalize_brain_key](#normalizebrainkey)
			- [save_wallet_file](#savewalletfile)
	- [2.2 Account APIs](#22-account-apis)
		- [ACCOUNT](#account)
			- [list_my_accounts](#listmyaccounts)
			- [list_accounts](#listaccounts)
			- [list_account_balances](#listaccountbalances)
			- [register_account](#registeraccount)
			- [create_account_with_brain_key](#createaccountwithbrainkey)
			- [transfer](#transfer)
			- [transfer2](#transfer2)
			- [get_transaction_id](#gettransactionid)
			- [get_vesting_balances](#getvestingbalances)
			- [withdraw_vesting](#withdrawvesting)
			- [get_account](#getaccount)
			- [get_account_id](#getaccountid)
			- [get_account_history](#getaccounthistory)
			- [approve_proposal](#approveproposal)
	- [2.3 Asset APIs](#23-asset-apis)
		- [ASSET](#asset)
			- [list_assets](#listassets)
			- [publish_asset_feed](#publishassetfeed)
			- [issue_asset](#issueasset)
			- [get_asset](#getasset)
			- [reserve_asset](#reserveasset)
	- [2.4 Inspection APIs](#24-inspection-apis)
		- [INSPECTION](#inspection)
			- [get_block](#getblock)
			- [get_account_count](#getaccountcount)
			- [get_global_properties](#getglobalproperties)
			- [get_dynamic_global_properties](#getdynamicglobalproperties)
			- [get_object](#getobject)
	- [2.5 TRANSACTION APIs](#25-transaction-apis)
		- [TRANSACTION BUILDER](#transaction-builder)
			- [begin_builder_transaction](#beginbuildertransaction)
			- [add_operation_to_builder_transaction](#addoperationtobuildertransaction)
			- [replace_operation_in_builder_transaction](#replaceoperationinbuildertransaction)
			- [set_fees_on_builder_transaction](#setfeesonbuildertransaction)
			- [preview_builder_transaction](#previewbuildertransaction)
			- [sign_builder_transaction](#signbuildertransaction)
			- [propose_builder_transaction](#proposebuildertransaction)
			- [propose_builder_transaction2](#proposebuildertransaction2)
			- [remove_builder_transaction](#removebuildertransaction)
			- [serialize_transaction](#serializetransaction)
			- [sign_transaction](#signtransaction)
			- [get_prototype_operation](#getprototypeoperation)
	- [2.6 OTHERS](#26-others)
		- [UNCLASSIFIED](#unclassified)
			- [claim_fees](#claimfees)
			- [content_cancellation](#contentcancellation)
			- [create_miner](#createminer)
			- [create_monitored_asset](#createmonitoredasset)
			- [create_package](#createpackage)
			- [create_user_issued_asset](#createuserissuedasset)
			- [dbg_generate_blocks](#dbggenerateblocks)
			- [dbg_make_mia](#dbgmakemia)
			- [dbg_push_blocks](#dbgpushblocks)
			- [dbg_stream_json_objects](#dbgstreamjsonobjects)
			- [dbg_update_object](#dbgupdateobject)
			- [download_content](#downloadcontent)
			- [download_package](#downloadpackage)
			- [extract_package](#extractpackage)
			- [flood_network](#floodnetwork)
			- [fund_asset_pools](#fundassetpools)
			- [generate_brain_key_el_gamal_key](#generatebrainkeyelgamalkey)
			- [generate_el_gamal_keys](#generateelgamalkeys)
			- [generate_encryption_key](#generateencryptionkey)
			- [get_author_and_co_authors_by_URI](#getauthorandcoauthorsbyuri)
			- [get_brain_key_info](#getbrainkeyinfo)
			- [get_buying_by_consumer_URI](#getbuyingbyconsumeruri)
			- [get_buying_history_objects_by_consumer](#getbuyinghistoryobjectsbyconsumer)
			- [get_content](#getcontent)
			- [get_download_status](#getdownloadstatus)
			- [get_el_gammal_key](#getelgammalkey)
			- [get_feeds_by_miner](#getfeedsbyminer)
			- [get_message_objects](#getmessageobjects)
			- [get_messages](#getmessages)
			- [get_miner](#getminer)
			- [get_monitored_asset_data](#getmonitoredassetdata)
			- [get_open_buyings](#getopenbuyings)
			- [get_open_buyings_by_URI](#getopenbuyingsbyuri)
			- [get_open_buyings_by_consumer](#getopenbuyingsbyconsumer)
			- [get_proposed_transactions](#getproposedtransactions)
			- [get_real_supply](#getrealsupply)
			- [head_block_time](#headblocktime)
			- [leave_rating_and_comment](#leaveratingandcomment)
			- [list_active_subscriptions_by_author](#listactivesubscriptionsbyauthor)
			- [list_active_subscriptions_by_consumer](#listactivesubscriptionsbyconsumer)
			- [list_miners](#listminers)
			- [list_publishers_by_price](#listpublishersbyprice)
			- [list_publishing_managers](#listpublishingmanagers)
			- [list_seeders_by_rating](#listseedersbyrating)
			- [list_seeders_by_region](#listseedersbyregion)
			- [list_seeders_by_upload](#listseedersbyupload)
			- [list_subscriptions_by_author](#listsubscriptionsbyauthor)
			- [list_subscriptions_by_consumer](#listsubscriptionsbyconsumer)
			- [price_to_dct](#pricetodct)
			- [propose_fee_change](#proposefeechange)
			- [propose_parameter_change](#proposeparameterchange)
			- [propose_transfer](#proposetransfer)
			- [remove_package](#removepackage)
			- [request_to_buy](#requesttobuy)
			- [restore_encryption_key](#restoreencryptionkey)
			- [search_account_history](#searchaccounthistory)
			- [search_accounts](#searchaccounts)
			- [search_content](#searchcontent)
			- [search_feedback](#searchfeedback)
			- [search_my_purchases](#searchmypurchases)
			- [search_user_content](#searchusercontent)
			- [seeding_startup](#seedingstartup)
			- [send_message](#sendmessage)
			- [set_automatic_renewal_of_subscription](#setautomaticrenewalofsubscription)
			- [set_desired_miner_count](#setdesiredminercount)
			- [set_publishing_manager](#setpublishingmanager)
			- [set_publishing_right](#setpublishingright)
			- [set_subscription](#setsubscription)
			- [set_transfer_logs](#settransferlogs)
			- [set_voting_proxy](#setvotingproxy)
			- [sign_buffer](#signbuffer)
			- [submit_content](#submitcontent)
			- [submit_content_async](#submitcontentasync)
			- [subscribe_by_author](#subscribebyauthor)
			- [subscribe_to_author](#subscribetoauthor)
			- [update_miner](#updateminer)
			- [update_monitored_asset](#updatemonitoredasset)
			- [update_user_issued_asset](#updateuserissuedasset)
			- [upload_package](#uploadpackage)
			- [verify_signature](#verifysignature)
			- [vote_for_miner](#voteforminer)

<!-- /TOC -->

# 1. Introduction

## 1.1 How to call wallet API

### 1.1.1 HTTP Calls

HTTP call are only supported by those wallet APIs that do not require login. No HTTP endpoint will be opend by default. You can expose HTTP endpoint for wallet APIs by command:

> cli_wallet --rpc-http-endpoint="127.0.0.1:8081"

You can specify IP and port for your HTTP connection. These APIs can be called via any HTTP Client or compatible SDK for multiple programming languages.

Both request and response of these APIs are JSON formated. The request must follow JSON-RPC 2.0 specifications, including three base elements:

1. id (any integer specified, simply to remark the sequence of API call)
2. method (the name of API to be revoked)
3. params (a list of parameters of this API)

**request:**   
``  > {
	"method": "info",
	"params": [""],
	"id": 1
}``

**response:**    
`` < {
    "id": 1,
    "result": {
        "head_block_num": 0,
        "head_block_id": "0000000000000000000000000000000000000000",
        "head_block_age": "25 weeks old",
        "next_maintenance_time": "47 years ago",
        "chain_id": "4777b283f8006237590c67a5001fb62e14fdfd2c0f5f5afb55e687ae8082d483",
        "participation": "100.00000000000000000",
        "active_miners": [
            "1.4.1",
            "1.4.2",
            "1.4.3",
            "1.4.4",
            "1.4.5",
            "1.4.6",
            "1.4.7",
            "1.4.8",
            "1.4.9",
            "1.4.10",
            "1.4.11"
        ]
    }
}``


### 1.1.2 WebSocket Calls

WebSocket call are only supported by those wallet APIs that do not require login. No WebSocket endpoint will be opend by default. You can expose HTTP endpoint for wallet APIs by command:

> cli_wallet --rpc-endpoint="127.0.0.1:8082"

You can specify IP and port for your WebSocket connection. These APIs can be called via any WebSocket Client or compatible SDK for multiple programming languages.

Both request and response of these APIs are JSON formated. The request must follow JSON-RPC 2.0 specifications, including three base elements:

1. id (any integer specified, simply to remark the sequence of API call)
2. method (the name of API to be revoked)
3. params (a list of parameters of this API)

**request:**    
`` > {
  "method": "is_locked",
  "params": [],
  "id": 2
}``  

**response:**  
`` {
  "id": 2,
  "result": false
}``


# 2. API Definition

## 2.1 General APIs

### GENERAL

#### help
**Description:** Returns a list of all commands supported by the wallet API.   
**Parameters:**  
**Returns:** multi-line string  
**Note:** This lists each command, along with its arguments and return types. For more detailed help on a single command, use get_help().

----

#### gethelp
**Description:** Returns detailed help on a single API command.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| method | string | the name of the API command you want help with |

**Returns:** multi-line string  

----

#### info
**Description:** Get current blockchain info.    
**Parameters:**  
**Returns:** JSON object  

----

#### about
**Description:**  Returns info such as client version, git version of graphene/fc, version of boost, openssl.     
**Parameters:**  
**Returns:** JSON object  

----

#### network_add_nodes
**Description:** Add network nodes.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| nodes | vector<string> | network nodes to be added |

**Returns:** void  

----

#### network_get_connected_peers
**Description:** Get connected peers.   
 **Parameters:**   
**Returns:** vector&lt;variant>  

----

## 2.2 Wallet APIs

### WALLET

#### is_new
**Description:** Checks whether the wallet has just been created and has not yet had a password set.  
**Parameters:**  
**Returns:** bool  
**Note:** Calling set_password will transition the wallet to the locked state.

----

#### is_locked
**Description:** Checks whether the wallet is locked (is unable to use its private keys).   
**Parameters:**   
**Returns:** bool  
**Note:** This state can be changed by calling lock() or unlock().

----

#### lock
**Description:** Locks the wallet immediately.     
**Parameters:**   
**Returns:** void  

----

#### unlock
**Description:** Unlocks the wallet.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| password | string |  the password previously set with set_password() |


**Returns:** void  
**Note:**  
The wallet remains unlocked until the 'lock' is called or the program exits.  

----

#### set_password
**Description:** Sets a new password on the wallet.     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| password | string | password to set |

**Returns:** void  
**Note:**  
The wallet must be either 'new' or 'unlocked' to execute this command.  

----

#### dump_private_keys
**Description:**  Dumps all private keys owned by the wallet.    
**Parameters:**  
**Returns:** a map containing the private keys, indexed by their public key  
**Note:** The keys are printed in WIF format. You can import these keys into another wallet using import_key().

----

#### import_key
**Description:** Imports the private key for an existing account.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_name_or_id | string |  the account owning the key |
| wif_key | string | the private key in WIF format |

**Returns:** bool  
**Note:** The private key must match either an owner key or an active key for the named account.

----

#### import_accounts
**Description:** Get mapped account names to boolean values indicating whether the account was successfully imported.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| filename | string | the filename of the wallet JSON file |
| password | string | user's password to the wallet |

**Returns:** map of account names and boolean values

----

#### import_account_keys
**Description:** Check whether the keys were imported.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| filename | string | the filename of the wallet JSON file |
| password | string | user's password to the wallet |
| src_account_name | string | name of the source account |
| dest_account_name | string | name of the destination account |

**Returns:** bool  

----

#### suggest_brain_key
**Description:** Suggests a safe brain key to use for creating your account. create_account_with_brain_key() requires you to specify a ‘brain key’, a long passphrase that provides enough entropy to generate cyrptographic keys. This function will suggest a suitably random string that should be easy to write down (and, with effort, memorize).     
**Parameters:**  
**Returns:** string

----

#### get_private_key
**Description:** Get the WIF private key corresponding to a public key. The private key must already be in the wallet.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| pubkey | public_key_type | public key |

**Returns:** string  

----

#### load_wallet_file
**Description:**  Loads a specified Graphene wallet.     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| wallet_filename | string | the filename of the wallet JSON file to load. If wallet_filename is empty, it reloads the existing wallet file |

**Returns:** bool  
**Note:**  
The current wallet is closed before the new wallet is loaded. This does not change the filename that will be used for future wallet writes, so this may cause you to overwrite your original wallet unless you also call set_wallet_filename().  

----

#### normalize_brain_key
**Description:** Transforms a brain key to reduce the chance of errors when re-entering the key from memory.     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| s | string | the brain key as supplied by the user |

**Returns:** string  
**Note:**  
This takes a user-supplied brain key and normalizes it into the form used
for generating private keys. In particular, this upper-cases all ASCII
characters and collapses multiple spaces into one.

----

#### save_wallet_file
**Description:** Save wallet file.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| wallet_filename | | the filename of the new wallet JSON file to create or overwrite, if 'wallet_filename' is empty, save to the current filename |

**Returns:** void

----

## 2.2 Account APIs

### ACCOUNT

#### list_my_accounts
**Description:** Get a list of my account objects.     
**Parameters:**  
**Returns:** vector&lt;account_object>

----

#### list_accounts
**Description:** Get a list of accounts mapping account names to account ids.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| lowerbound | string | the name of the first account to return. If the named account does not exist, the list will start at the account that comes after 'lowerbound' |
| limit | uint32_t | the maximum number of accounts to return (max: 1000) |


**Returns:** map&lt;string, account_id_type>  
**Note:**  
Use the 'lowerbound' and limit parameters to page through the list. To
retrieve all accounts, start by setting 'lowerbound' to the empty string
'""', and then each iteration, pass the last account name returned as the
'lowerbound' for the next 'list_accounts()' call.

----

#### list_account_balances
**Description:** Get a list of the given account's balances.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| id | string | the name or id of the account whose balances you want |

**Returns:** vector&lt;asset>

----

#### register_account
**Description:** Registers a third party’s account on the blockckain.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| name | string | the name of the account, must be unique on the blockchain. Shorter names are more expensive to register; the rules are still in flux, but in general names of more than 8 characters with at least one digit will be cheap |
| owner | public_key_type | the owner key for the new account |
| active | public_key_type | the active key for the new account |
| registrar_account | string | the account which will pay the fee to register the user |
| referrer_percent | uint32_t | the percentage (0 - 100) of the new user’s transaction fees not claimed by the blockchain that will be distributed to the referrer; the rest will be sent to the registrar. Will be multiplied by GRAPHENE_1_PERCENT when constructing the transaction |
| broadcast | bool |  true to broadcast the transaction on the network |
TBD

**Returns:** signed transaction object  
**Note:** This function is used to register an account for which you do not own the private keys. When acting as a registrar, an end user will generate their own private keys and send you the public keys. The registrar will use this function to register the account on behalf of the end user.

----

#### create_account_with_brain_key
**Description:** Creates a new account and registers it on the blockchain.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| brain_key | string | the brain key used for generating the account’s private keys |
| account_name | string | the name of the account, must be unique on the blockchain. Shorter names are more expensive to register; the rules are still in flux, but in general names of more than 8 characters with at least one digit will be cheap |
| registrar_account | string | the account which will pay the fee to register the user |
| broadcast | bool |  true to broadcast the transaction on the network |

**Returns:** signed transaction object

----

#### transfer
**Description:** Transfer an amount from one account to another.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| from | string | the name or id of the account sending the funds |
| to | string | the name or id of the account receiving the funds |
| amount | string | the amount to send (in nominal units to send half of a BTS, specify 0.5) |
| asset_symbol | string | the symbol or id of the asset to send |
| memo | string | a memo to attach to the transaction. The memo will be encrypted in the transaction and readable for the receiver. There is no length limit other than the limit imposed by maximum transaction size, but transaction increase with transaction size |
| broadcast | bool |  true to broadcast the transaction on the network |

TBDTBDTBD

**Returns:** signed transaction object

----

#### transfer2
**Description:** This method works just like transfer, except it always broadcasts and returns the transaction ID along with the signed transaction.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| from | string | the name or id of the account sending the funds |
| to | string | the name or id of the account receiving the funds |
| amount | string | the amount to send (in nominal units to send half of a BTS, specify 0.5) |
| asset_symbol | string | the symbol or id of the asset to send |
| memo | string | a memo to attach to the transaction. The memo will be encrypted in the transaction and readable for the receiver. There is no length limit other than the limit imposed by maximum transaction size, but transaction increase with transaction size |
| broadcast | bool |  true to broadcast the transaction on the network |

**Returns:** pair of transaction id and signed transaction object

----

#### get_transaction_id
**Description:**  convert a JSON transaction to its transactin ID.     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| trx | signed_transaction | signed transaction |

**Returns:** string

----

#### get_vesting_balances
**Description:** Get information about a vesting balance object.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_name | string | an account name, account ID, or vesting balance object ID |

**Returns:** vector&lt;vesting_balance_object_with_info>

----

#### withdraw_vesting
**Description:** Withdraw a vesting balance.     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| miner_name | string | The account name of the witness, also accepts account ID or vesting balance ID |
| amount | string | The amount to withdraw |
| asset_symbol | string |  The symbol of the asset to withdraw |
| broadcast | bool | true if you wish to broadcast the transaction |

**Returns:** signed_transaction

----

#### get_account
**Description:** Returns information about the given account.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| account_name_or_id | string | the name or id of the account to provide information about |

**Returns:** account object

----

#### get_account_id
**Description:**  Lookup the id of a named account.      
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_name_or_id | string | the name of the account to look up |

**Returns:** account id

----

#### get_account_history
**Description:**  Returns the most recent operations on the named account.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| name | string | the name or id of the account |
| limit | int | the number of entries to return (starting from the most recent) (max 100) |

**Returns:** vector&lt;operation_detail>  
**Note:** This returns a list of operation history objects, which describe activity on the account.

----

#### approve_proposal
**Description:** Approve or disapprove a proposal.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| fee_paying_account | string | the account paying the fee for the op |  
| proposal_id | string | the proposal to modify |  
| delta | approval_delta |  Members contain approvals to create or remove. In JSON you can leave empty members undefined |  
| broadcast | bool | true if you wish to broadcast the transaction |

**Returns:** signed transaction

----

## 2.3 Asset APIs

### ASSET

#### list_assets
**Description:**  Lists all assets registered on the blockchain.     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| lowerbound | string | the symbol of the first asset to include in the list |
| limit | uint32_t | the maximum number of assets to return (max: 100) |


**Returns:** vector of asset object  
**Note:** To list all assets, pass the empty string "" for the lowerbound to start at the beginning of the list, and iterate as necessary.

----

#### publish_asset_feed
**Description:** Publishes a price feed for the named asset.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| publishing_account | string | the account publishing the price feed |
| symbol | string | the name or id of the asset whose feed we're publishing |
| feed | price_feed | the price_feed object for particular market-issued asset |
| broadcast | bool | true to broadcast the transaction on the network |


**Returns:** signed_transaction  
**Note:**  
Price feed providers use this command to publish their price feeds for market-issued assets. A price feed is used to tune the market for a particular market-issued asset. For each value in the feed, the median across all committee_member feeds for that asset is calculated and the market for the asset is configured with the median of that value.  
The feed object in this command contains three prices: a call price limit, a short price limit, and a settlement price. The call limit price is structured as (collateral asset) / (debt asset) and the short limit price is structured as (asset for sale) / (collateral asset). Note that the asset IDs are opposite to eachother, so if we’re publishing a feed for USD, the call limit price will be CORE/USD and the short limit price will be USD/CORE. The settlement price may be flipped either direction, as long as it is a ratio between the market-issued asset and its collateral.

----

#### issue_asset
**Description:** Issue new shares of an asset.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| to_account | string | the name or id of the account to receive the new shares |
| amount | string | the amount to issue, in nominal units |
| symbol | string | the ticker symbol of the asset to issue |
| memo | string | a memo to include in the transaction, readable by the recipient |
| broadcast | bool | true to broadcast the transaction on the network |

**Returns:** signed transaction object

----

#### get_asset
**Description:** Returns information about the given asset.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| asset_name_or_id | string | the symbol or id of the asset in question |

**Returns:** asset object

----

#### reserve_asset
**Description:** Burns the given user-issued asset.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| from | string | the account containing the asset you wish to burn |
| amount | string | the amount to burn, in nominal units |
| symbol | string | the name or id of the asset to burn |
| broadcast | bool | true to broadcast the transaction on the network |


**Returns:** signed_transaction  
**Note:** This command burns the user-issued asset to reduce the amount in circulation. you cannot burn market-issued assets.

----

## 2.4 Inspection APIs

### INSPECTION

#### get_block
**Description:** Get the referenced block with info.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| num | uint32_t | ID of the block |

**Returns:** signed block object

----

#### get_account_count
**Description:** Returns the number of accounts registered on the blockchain.     
**Parameters:**   
**Returns:** uint64_t

----

#### get_global_properties
**Description:** Returns the block chain’s slowly-changing settings. This object contains all of the properties of the blockchain that are fixed or that change only once per maintenance interval (daily) such as the current list of witnesses, committee_members, block interval, etc.      
**Parameters:**   
**Returns:** global properties object  
**Note:** get_dynamic_global_properties() for frequently changing properties

----

#### get_dynamic_global_properties
**Description:**  Returns the block chain’s rapidly-changing properties. The returned object contains information that changes every block interval such as the head block number, the next witness, etc.     
**Parameters:**   
**Returns:** dynami global properties object

----

#### get_object
**Description:** Returns the blockchain object corresponding to the given id.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| id | object_id_type | the id of the object to return |

**Returns:** the requested object  
**Note:**  
This generic function can be used to retrieve any object from the blockchain that is assigned an ID. Certain types of objects have specialized convenience functions to return their objects e.g., assets have get_asset(), accounts have get_account(), but this function will work for any object.

----

## 2.5 TRANSACTION APIs

### TRANSACTION BUILDER

#### begin_builder_transaction
**Description:** Begin builder transaction.    
**Parameters:**  
**Returns:** transaction handle    

----

#### add_operation_to_builder_transaction
**Description:** Add an operation to builder transaction.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| transaction_handle | transaction_handle_type | ... |
| operation | operation | ... |

**Returns:** void  

----

#### replace_operation_in_builder_transaction
**Description:** Replace operation in a builder transaction.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| handle | transaction_handle_type | ... |
| operation_index | unsigned | ... |
| new_op | operation | ... |

**Returns:** void

----

#### set_fees_on_builder_transaction
**Description:** Set builder transaction fees.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| handle | transaction_handle_type | handle of the transaction |
| fee_asset | string | ... |

**Returns:** asset object

----

#### preview_builder_transaction
**Description:** Preview builder transaction.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| handle | transaction_handle_type | ... |

**Returns:** transaction object

----

#### sign_builder_transaction
**Description:** Sign builder transaction.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| transaction_handle | transaction_handle_type | ... |
| broadcast | bool | true to broadcast the transaction on the network |

**Returns:** signed transaction object

----

#### propose_builder_transaction
**Description:** Propose builder transaction.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| handle | transaction_handle_type | ... |
| expiration | time_point_sec | ... |
| review_period_seconds | uint32_t | ... |
| broadcast | bool | true to broadcast the transaction on the network |

**Returns:** signed transaction object

----

#### propose_builder_transaction2
**Description:**  Propose builder transaction.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| handle | transaction_handle_type | ... |
| account_name_or_id | string | ... |
| expiration | time_point_sec | ... |
| review_period_seconds | uint32_t | ... |
| broadcast | bool | true to broadcast the transaction on the network |

**Returns:** void

----

#### remove_builder_transaction
**Description:** Remove builder transactions.   
**Synopsis:**
> remove_builder_transaction &lt;handle&gt;  

**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| handle | transaction_handle_type | transaction handle |

**Returns:** void

----

#### serialize_transaction
**Description:** Converts a signed_transaction in JSON form to its binary representation.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| tx | signed_transaction | the transaction to serialize |

**Returns:** signed_transaction  
**Note:** It will not be hex encoded, this returns a raw string that may have null characters embedded in it    

----

#### sign_transaction
**Description:** Signs a transaction.       
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| tx | signed_transaction | the unsigned transaction |
| broadcast | bool | true if you wish to broadcast the transaction |

**Returns:** signed_transaction  
**Note:** Given a fully-formed transaction that is only lacking signatures, this signs the transaction with the necessary keys and optionally broadcasts the transaction.

----

#### get_prototype_operation
**Description:** Returns an uninitialized object representing a given blockchain operation.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
|  operation_type | string |  the type of operation to return, must be one of the operations defined in graphene/chain/operations.hpp (e.g., "global_parameters_update_operation") |

**Returns:** a default-constructed operation of the given type   
**Note:**  
This returns a default-initialized object of the given type; it can be used during early development of the wallet when we don’t yet have custom commands for creating all of the operations the blockchain supports.
Any operation the blockchain supports can be created using the transaction builder’s add_operation_to_builder_transaction() , but to do that from the CLI you need to know what the JSON form of the operation looks like. This will give you a template you can fill in. It’s better than nothing.

----

## 2.6 OTHERS

### UNCLASSIFIED

#### claim_fees
**Description:** Transfers accumulated assets from pools back to the issuer's balance.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |  
| uia_amount | string | the amount of "this" asset to claim, in nominal units |
| uia_symbol | string | the name or id of the asset to claim |
| dct_amount | string | the amount of DCT asset to claim, in nominal units |
* dct_symbol: the name or id of the DCT asset to claim (type: string)  
* broadcast: true to broadcast the transaction on the network (type:
	bool)  

**Returns:** transaction_handle_type

----

#### content_cancellation
**Description:** Cancel content.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| author | string | the author of the content |
| URI | string | the URI of the content |  
| broadcast | bool | true to broadcast the transaction on the network |

**Returns:** signed_transaction

----

#### create_miner
**Description:** Create a minor.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| owner_account | string | the name or id of the account which is creating the miner |
| url | string | a URL to include in the miner record in the blockchain, clients may display this when showing a list of miners |
| broadcast | bool | true to broadcast the transaction on the network |

**Returns:** signed_transaction

----

#### create_monitored_asset
**Description:** Create monitored assets.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| issuer | string | ... |
| symbol | string | ... |
| precision | uint8_t | the number of digits after the decimal point |
| feed_lifetime_sec | uint32_t | ... |
| minimum_feeds | uint32_t | ... |
| broadcast | bool | ... |

**Returns:** signed_transaction

----

#### create_package
**Description:**  Get package hash (ripemd160 hash of package content) and content custody data.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| content_dir | string | directory containing all content that should be packed |
| samples_dir | string | directory containing samples of content |  
| aes_key | DInteger | AES key for encryption |

**Returns:** std::pair&lt;string, decent::encrypt::CustodyData&gt;   

----

#### create_user_issued_asset
**Description:** Create user issued asset.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| issuer | string | the name or id of the account who will pay the fee and become the issuer of the new asset |
| symbol | string | the ticker symbol of the new asset |
| precision | uint8_t | the number of digits of precision to the right of the decimal point, must be less than or equal to 12 |
| description | string | asset description, maximal length is 1000 chars |
| max_supply | uint64_t | the maximum supply of this asset which may exist at any given time |
| core_exchange_rate | price | core_exchange_rate technically needs to store the asset ID of this new asset, since this ID is not known at the time this operation is created, create this price as though the new asset has instance ID 1, and the chain will overwrite it with the new asset's ID |
| is_exchangeable | bool | true to allow implicit conversion of this asset to/from core asset |
| broadcast | bool | true to broadcast the transaction on the network |

**Returns:** signed_transaction

----

#### dbg_generate_blocks
**Description:** Generate blocks (debug).      
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| debug_wif_key | string | ... |
| count | uint32_t | ... |

**Returns:** void

----

#### dbg_make_mia
**Description:** Make mia (debug).    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| creator | string | ... |
| symbol | string | ... |

**Returns:**

void dbg_make_mia(string creator, string symbol)

----

#### dbg_push_blocks
**Description:**  Push blocks (debug).     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| src_filename | string | ... |
| count | uint32_t | ... |

**Returns:** void

----

#### dbg_stream_json_objects
**Description:**  Stream JSON objects (debug).    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| filename | string | ... |

**Returns:** void

----

#### dbg_update_object
**Description:**  Update object (debug).  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| update | variant_object | ... |

**Returns:** void

----

#### download_content
**Description:**  Download content.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| consumer | string | consumer of the content |
| URI | string | the URI of the content |
| region_code_from | string | two letter region code |
| broadcast | bool | true to broadcast the transaction on the network |

**Returns:** void

----

#### download_package
**Description:**  Download package.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| url | string | magnet or IPFS URL of package |

**Returns:** void

----

#### extract_package
**Description:**  Extract packages.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| package_hash | string | hash of package that needs to be extracted |
| output_dir | string | directory where extracted files will be created |
| aes_key | DInteger | AES key for decryption |

**Returns:** void

----

#### flood_network
**Description:** Flood network.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| prefix | string | ... |
| number_of_transactions | uint32_t | ... |

**Returns:** void

----

#### fund_asset_pools
**Description:**  Pay into the pools for the given asset.     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| from | string | the name or id of the account sending the core asset |
| uia_amount | string | the amount of "this" asset to deposit |
| uia_symbol | string | the name or id of the asset whose pool you wish to fund |
| dct_amount | string | the amount of the core asset to deposit |
| dct_symbol | string | the name or id of the DCT asset |
| broadcast | bool | true to broadcast the transaction on the network |


**Returns:** signed_transaction  
**Note:**  
User-issued assets can optionally have a pool of the core asset which is
automatically used to pay transaction fees for any transaction using that
asset (using the asset's core exchange rate).  
Allows anyone to deposit core/asset into pools. This pool are used when
conversion between assets is needed (paying fees, paying for a content in
different asset).

----

#### generate_brain_key_el_gamal_key
**Description:**  Generate brain key.    
**Parameters:**  
**Returns:** pair&lt;brain_key_info, el_gamal_key_pair>

----

#### generate_el_gamal_keys
**Description:** Generate ElGamal keys.    
**Parameters:**  
**Returns:** el_gamal_key_pair

----

#### generate_encryption_key
**Description:** Generate encryption key.   
**Parameters:**  
**Returns:** DInteger

----

#### get_author_and_co_authors_by_URI
**Description:** Get the autor of the content and the list of co-authors.     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| URI | string | URI of the content |

**Returns:** pair&lt;account_id_type, vector&lt;account_id_type>>

----

#### get_brain_key_info
**Description:**  Get brain key info.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| brain_key | string | the brain key to be used for calculation |

**Returns:** brain_key_info

----

#### get_buying_by_consumer_URI
**Description:**  Get buying objects corresponding to the provided consumer.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_id_or_name | string | consumer of the buying to retrieve |
| URI | string | URI of the buying to retrieve |

**Returns:** optional&lt;buying_object>

----

#### get_buying_history_objects_by_consumer
**Description:**  Get history buying objects corresponding to the provided consumer.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_id_or_name | string | consumer of the buyings to retrieve |

**Returns:** vector&lt;buying_object>

----

#### get_content
**Description:** Get the content corresponding to the provided URI.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| URI | string | URI of the content to retrieve |

**Returns:** optional&lt;content_object>

----

#### get_download_status
**Description:** Get download status.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| consumer | string | consumer of the content |
| URI | string | the URI of the content |

**Returns:** optional&lt;content_download_status>

----

#### get_el_gammal_key
**Description:** Get pair of ElGamal keys.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| consumer | string | ... |

**Returns:** el_gamal_key_pair_str

 get_el_gammal_key(string const & consumer)

----

#### get_feeds_by_miner
**Description:**  Get list of price feeds published by the miner.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_name_or_id | string | the name or id of the account |
| count | uint32_t | maximum number of price feeds to fetch (must not exceed 100) |
**Returns:** multimap&lt;time_point_sec, price_feed>

----

#### get_message_objects
**Description:** Get vector of message objects.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| receiver | string | name of message receiver |
| max_count | uint32_t | maximal number of last messages to be displayed |

**Returns:** vector&lt;message_object>

----

#### get_messages
**Description:** Get vector of message objects.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| receiver | string | name of message receiver |
| max_count | uint32_t | maximal number of last messages to be displayed |

**Returns:** vector<text_message>

----

#### get_miner
**Description:**  Get the information about the miner stored in the blockchain.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| owner_account | string | the name or id of the miner account owner, or the id of the miner |

**Returns:** miner_object

----

#### get_monitored_asset_data
**Description:** Get the BitAsset-specific data for this asset.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| asset_name_or_id | string | the symbol or id of the BitAsset in question |

**Returns:** monitored_asset_options

----

#### get_open_buyings
**Description:** Get open buying objects.   
**Returns:** vector&lt;buying_object>

----

#### get_open_buyings_by_URI
**Description:** Get open buyings corresponding to the provided URI.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| URI | string | URI of the buyings to retrieve |

**Returns:** vector&lt;buying_object>

----

#### get_open_buyings_by_consumer
**Description:** Get open buyings corresponding to the provided consumer.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
|  account_id_or_name | string | consumer of the buyings to retrieve |

**Returns:** vector<buying_object>

----

#### get_proposed_transactions
**Description:** Get list of proposed transactions.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_or_id | string | ... |

**Returns:** vector<proposal_object>

----

#### get_real_supply
**Description:** Get current supply of the core asset.    
**Parameters:**  
**Returns:** real_supply

----

#### head_block_time
**Description:** Get the head block time.   
**Parameters:**  
**Returns:** fc::time_point_sec

----

#### leave_rating_and_comment
**Description:** Rate and comment.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |
| consumer | string | consumer giving the rating |
| URI | string |the URI of the content |
| rating | uint64_t | ... |
| comment | string | ... |
| broadcast | bool | true to broadcast the transaction on the network |

**Returns:** void

----

#### list_active_subscriptions_by_author
**Description:**  Get list of active subscription objects corresponding to the provided author.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_id_or_name | string | the name or id of the author |
| count | uint32_t | maximum number of subscriptions to fetch (must not exceed 100) |

**Returns:** vector&lt;subscription_object>

----

#### list_active_subscriptions_by_consumer
**Description:**  Get list of active subscription objects corresponding to the provided consumer.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_id_or_name | string | the name or id of the consumer |
| count | uint32_t | maximum number of subscriptions to fetch (must not exceed 100) |

**Returns:** vector&lt;subscription_object>  

----

#### list_miners
**Description:** Get a list of miners mapping miner names to miner ids.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| lowerbound | string | the name of the first miner to return. If the named miner does not exist, the list will start at the miner that comes after 'lowerbound' |
| limit | uint32_t | the maximum number of miners to return (max: 1000) |


**Returns:** map&lt;string, miner_id_type>  
**Note:**
Use the 'lowerbound' and limit parameters to page through the list. To
retrieve all miners, start by setting 'lowerbound' to the empty string
'""', and then each iteration, pass the last miner name returned as the
'lowerbound' for the next 'list_miners()' call.

----

#### list_publishers_by_price
**Description:** List publishers by price.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| count | uint32_t | maximum number of seeders to retrieve |

**Returns:** vector&lt;seeder_object>



#### list_publishing_managers
**Description:** Get list of publishing managers   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| lower_bound_name | string | the name of the first account to return, if the named account does not exist, the list will start at the account that comes after 'lowerbound' |
| limit | uint32_t | the maximum number of accounts to return (max: 100) |


**Returns:** vector&lt;account_id_type>

----

#### list_seeders_by_rating
**Description:** Get list of seeders by rating.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| count | uint32_t | maximum number of seeders to retrieve |

**Returns:** vector&lt;seeder_object>

----

#### list_seeders_by_region
**Description:** Get list of seeders by region.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| region_code | string | region code of seeders to retrieve |

**Returns:** vector&lt;seeder_object>

----


#### list_seeders_by_upload
**Description:** Get list of seeders by upload.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| count | uint32_t | maximum number of seeders to retrieve |

**Returns:** optional&lt;vector&lt;seeder_object>>

----

#### list_subscriptions_by_author
**Description:** Get list of subscription objects corresponding to the provided author.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_id_or_name | string | the name or id of the author |
| count | uint32_t | maximum number of subscriptions to fetch (must not exceed 100) |


**Returns:** vector&lt;subscription_object>

----

#### list_subscriptions_by_consumer
**Description:** Get list of subscription objects corresponding to the provided consumer.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_id_or_name | string | the name or id of the consumer |
| count | uint32_t | maximum number of subscriptions to fetch (must not exceed 100) |
**Returns:** vector&lt;subscription_object>

----

#### price_to_dct
**Description:** Get price in DCT.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| price | asset | asset in DCT, monitored asset or user issued asset |

**Returns:** asset

----

#### propose_fee_change
**Description:** Get the signed version of the transaction.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| proposing_account | string | the account paying the fee to propose the transaction |
| expiration_time | time_point_sec | Timestamp specifying when the proposal will either take effect or expire |
| changed_values | variant_object | map of operation type to new fee, operations may be specified by name or ID, the "scale" key changes the scale |
| broadcast | bool | true if you wish to broadcast the transaction |

**Returns:** signed_transaction

----

#### propose_parameter_change
**Description:** Get the signed version of the transaction.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| proposing_account | string | the account paying the fee to propose the transaction |
| expiration_time | time_point_sec | Timestamp specifying when the proposal will either take effect or expire |
| changed_values | variant_object | the values to change; all other chain parameters are filled in with default values |
| broadcast | bool | true if you wish to broadcast the transaction |


**Returns:** signed_transaction

----

#### propose_transfer
**Description:** Propose a transfer transaction.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| proposer | string | ... |
| from | string | the name or id of the account sending the funds |
| to | string | the name or id of the account receiving the funds |
| amount | string | the amount to send (in nominal units - to send half of a BTS, specify 0.5) |
| asset_symbol | string | the symbol or id of the asset to send |
| memo | string | a memo to attach to the transaction, which will be encrypted in the transaction and readable for the receiver. There is no length limit other than the limit imposed by maximum transaction size, but transaction increase with transaction size |
| expiration | time_point_sec | expiration time |

**Returns:** void

----

#### remove_package
**Description:** Remove packages.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
|  package_hash | string | Hash of package that needs to be removed |

**Returns:** void

----

#### request_to_buy
**Description:** Request to buy content.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| consumer | string | consumer of the content |
| URI | string | the URI of the content |
| price_asset_name | string | ticker symbol of the asset which will be used to buy content |
| price_amount | string | the price of the content |
| str_region_code_from | string | two letter region code |
| broadcast | bool | true to broadcast the transaction on the network |


**Returns:** signed_transaction

----

#### restore_encryption_key
**Description:** Restored AES key from particles.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account | string | consumers account id or name |
| buying | buying_id_type | the buying object containing key particles |

**Returns:** DInteger

----

#### search_account_history
**Description:**  Get a list of transaction detail object, which describe activity
on the account.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_name | string | the name or id of the account |
| order | string | sort data by field |
| id | string | object_id to start searching from |
| limit | int | the number of entries to return (starting from the most recent) (max 100) |

**Returns:** vector&lt;class transaction_detail_object>

----

#### search_accounts
**Description:** Get map of account names to corresponding ID.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| term | string | will try to partially match account name or id |
| limit | uint32_t | maximum number of results to return (must not exceed 1000) |
| order | string | sort data by field |
| id | string | object_id to start searching from |


**Returns:** vector&lt;account_object>

----

#### search_content
**Description:** Search for content.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| term | string | search term |
| order | string | order field |
| user | string | content owner |
| region_code | string | two letter region code |
| id | string | the id of content object to start searching from |
| type | string | the application and content type to be filtered |
| count | uint32_t | maximum number of contents to fetch (must not exceed 100) |


**Returns:** vector&gt;content_summary>

----

#### search_feedback
**Description:**  Search for feedbacks.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| user | string | feedback author |
| URI | string | the content object URI |
| id | string | the id of feedback object to start searching from |
| count | uint32_t | maximum number of feedbacks to fetch |

**Returns:** vector&lt;rating_object_ex>

----

#### search_my_purchases
**Description:** Search for historical purchases.     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_id_or_name | string | consumer of the buyings to retrieve |
| term | string | search term to look up in Title and Description |
| order | string | sort data by field |
| id | string | object_id to start searching from |
| count | uint32_t | maximum number of contents to fetch (must not exceed 100) |


**Returns:** vector&lt;buying_object_ex>

----

#### search_user_content
**Description:** Search for user content.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| user | string | content owner |
| term | string | search term |
| order | string | order field |
| region_code | string | two letter region code |
| id | string | the id of content object to start searching from |
| type | string | the application and content type to be filtered |
| count | uint32_t| maximum number of contents to fetch (must not exceed 100) |

**Returns:** vector&lt;content_summary>

----

#### seeding_startup
**Description:** Startup seeding.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_id_type_or_name | string | name or ID of account controlling this seeder |
| content_private_key | DInteger | El Gamal content private key |
| seeder_private_key | string | private key of the account controlling this seeder |
| free_space | uint64_t | allocated disk space in MegaBytes |
| seeding_price | uint32_t | price per MegaByte |
| packages_path | string | packages storage path |
| region_code | string | optional ISO 3166-1 alpha-2 two-letter region code |

**Returns:** void

----

#### send_message
**Description:** Send messages.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| from | string | ... |
| to | string | ... |
| text | string | message to send |
| broadcast | bool | true to broadcast the transaction on the network |

**Returns:** signed_transaction

----

#### set_automatic_renewal_of_subscription
**Description:** Set automatic renewal of subscription.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_id_or_name | string | the name or id of the account to update |
| subscription_id | subscription_id_type | the ID of the subscription |
| automatic_renewal | bool | true if account (consumer) wants to allow automatic renewal of subscription, false otherwise |
| broadcast | bool | true if you wish to broadcast the transaction |

**Returns:** signed_transaction

----

#### set_desired_miner_count
**Description:** Set desired number of miners.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_to_modify | string | the name or id of the account to update |
| desired_number_of_miners | uint16_t | ... |
| broadcast | bool | true if you wish to broadcast the transaction |

**Returns:** signed_transaction  
**Note:**  
Each account can voice their opinion on how many miners there should be in
the active miner list. These are independent of each other. You must vote
your approval of at least as many miners as you claim there should be (you
can't say that there should be 20 miners but only vote for 10).

There are maximum values for each set in the blockchain parameters
(currently defaulting to 1001).

----

#### set_publishing_manager
**Description:** Set publishing manager.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| from | string | account ( DECENT account ) giving/removing status of the publishing manager |
| to | vector&lt;string> | list of accounts getting status of the publishing manager |
| is_allowed | bool | true to give the status, false to remove it |
| broadcast | bool | true to broadcast the transaction on the network |

**Returns:** signed_transaction

----

#### set_publishing_right
**Description:** Set publishing authorities.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| from | string | account giving/removing right to publish a content |
| to | vector&lg;string> | list of accounts getting right to publish a content |
| is_allowed | bool | true to give the right, false to remove it |
| broadcast | bool | true to broadcast the transaction on the network |

**Returns:** signed_transaction

----

#### set_subscription
**Description:** Set account subscription.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account | string | the name or id of the account to update |
| allow_subscription | bool | true if account (author) wants to allow subscription, false otherwise |
| subscription_period | uint32_t | duration of subscription in days |
| price_amount | string | price for subscription per one subscription period |
| price_asset_symbol | string | ticker symbol of the asset which will be used to buy subscription |
| broadcast | bool | true if you wish to broadcast the transaction |

**Returns:** signed_transaction

----

#### set_transfer_logs
**Description:** Enable or disable transfer logs.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| enable | bool | true to enable transfer logs, false to otherwise |

**Returns:** void

----

#### set_voting_proxy
**Description:**  Set voting proxy.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| account_to_modify | string | the name or id of the account to update |
| voting_account | optional&lg;string> | the name or id of an account authorized to vote account_to_modify's shares, or null to vote your own shares |
| broadcast | bool | true if you wish to broadcast the transaction |


**Returns:** signed_transaction  
**Note:**  
If a user does not wish to take an active part in voting, they can choose
to allow another account to vote their stake. Setting a vote proxy does not remove your previous votes from the
blockchain, they remain there but are ignored. If you later null out your
vote proxy, your previous votes will take effect again. This setting can be changed at any time.

----

#### sign_buffer
**Description:** Sign buffer.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| str_buffer | string | the buffer to be signed |
| str_brainkey | string | derives the private key used for signature |

**Returns:**  string

----

#### submit_content
**Description:** Submit content to blockchain.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| author | string | the author of the content |
| co_authors | vector&lt;pair&lt;string,uint32_t>> | the co-authors' account name or ID mapped to corresponding payment split based on basis points |
| URI | string | the URI of the content |
| price_amounts | vector&lt;regional_price_info> | the price of the content per regions |
| size | uint64_t | the size of the content |
| hash | ripemd160 | the Hash of the package |
| seeders | vector&lt;account_id_type> | list of the seeders, which will publish the content |
| quorum | uint32_t | defines number of seeders needed to restore the encryption key |
| expiration | time_point_sec | the expiration time of the content. The content is available to buy till it's expiration time |
| publishing_fee_asset | string | ticker symbol of the asset which will be used to publish content |
| publishing_fee_amount | string | publishing price |
| synopsis | string | the description of the content |
| secret | DInteger | the AES key used to encrypt and decrypt the content |
| cd | CustodyData | custody data |
| broadcast | bool | true to broadcast the transaction on the network |

**Returns:** signed_transaction

----

#### submit_content_async
**Description:** Submit content asynchronously.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| author | string | the author of the content |
| co_authors | vector&lt;pair&lt;string, uint32_t>> | the co-authors' account name or ID mapped to corresponding payment split based on basis points |
| content_dir | string | path to the directory containing all content that should be packed |
| samples_dir | string | path to the directory containing samples of content |
| protocol | string | protocol for uploading package (e.g. "ipfs") |
| price_amounts | vector&lt;regional_price_info> | the prices of the content per regions |
| seeders | vector&lt;account_id_type> | list of the seeders, which will publish the content |
| expiration | time_point_sec | the expiration time of the content |
| synopsis | string | the description of the content |

**Returns:** void  

----

#### subscribe_by_author
**Description:**  Obtain subscription from the author.  
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| from | string | the account obtaining subscription from the author |
| to | string | the name or id of the author |
| broadcast | bool | true if you wish to broadcast the transaction |

**Returns:** signed_transaction

----

#### subscribe_to_author
**Description:**  Subscribe the consumer to the author.     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| from | string | account who wants subscription to author |
| to | string | the author you wish to subscribe to |
| price_amount | string | price for the subscription |
| price_asset_symbol | string | symbol of the asset which will be used to buy subscription (must be DCT token) |
| broadcast | bool | true if you wish to broadcast the transaction |

**Returns:** signed_transaction

----

#### update_miner
**Description:**  Update miner settings.     
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| miner_name | string | the name of the miner's owner account, also accepts the ID of the owner account or the ID of the miner |
| url | string | same as for create_miner, empty string makes it remain the same |
| block_signing_key | string | the new block signing public key, empty string makes it remain the same |
| broadcast | bool | true if you wish to broadcast the transaction |

**Returns:** signed_transaction

----

#### update_monitored_asset
**Description:** Update monitored asset.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| symbol | string | the name or id of the asset to update, which must be a market-issued asset |
| description | string | asset description |
| feed_lifetime_sec | uint32_t | time before a price feed expires |
| minimum_feeds | uint8_t | minimum number of unexpired feeds required to extract a median feed from |
| broadcast | bool | true to broadcast the transaction on the network |

**Returns:** signed_transaction  
**Note:**   
Monitored assets have some options which are not relevant to other asset
types. This operation is used to update those options and an existing
monitored asset.

----

#### update_user_issued_asset
**Description:** Update user issued asset.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| symbol | string | the name or id of the asset to update, which must be a market-issued asset |
| new_issuer | string | if the asset is to be given a new issuer, specify his ID here |
| description | string | asset description |
| max_supply | uint64_t | the maximum supply of this asset which may exist at any given time |
| core_exchange_rate | price | price used to convert non-core asset to core asset |
| is_exchangeable | bool | true to allow implicit conversion of this asset to/from core asset |
| broadcast | bool | true to broadcast the transaction on the network |

**Returns:** signed_transaction  
**Note:**  
User issued assets have some options which are not relevant to other asset
types. This operation is used to update those options an an existing user
issues asset.

----

#### upload_package
**Description:** Upload packages.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| package_hash | string | Hash of package that needs to be extracted |
| protocol | string | protocol for uploading package (IPFS) |

**Returns:** string  

----

#### verify_signature
**Description:** Verify a signature.   
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| str_buffer | string | the original buffer |
| str_publickey | string | the public key used for verification |
| str_signature | string | the signed buffer |

**Returns:** bool

----

#### vote_for_miner
**Description:** Vote for a miner.    
**Parameters:**

| name | type | desc |
| -------- | -------- | -------- |   
| voting_account | string | the name or id of the account who is voting with their shares |
| miner | string | the name or id of the miner' owner account |
| approve | bool | true if you wish to vote in favor of that miner, false to remove your vote in favor of that miner |
| broadcast | bool | true if you wish to broadcast the transaction |


**Returns:** signed_transaction  
**Note:**  
An account can publish a list of all miners they approve of. This command
allows you to add or remove miners from this list. Each account's vote is
weighted according to the number of shares of the core asset owned by that
account at the time the votes are tallied.

----
