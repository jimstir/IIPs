---
iip: <to be assigned>
title: User preference interface
author: Jimmy Debe
discussions-to: 
status: Draft
type: Interface
category 
created: (2023/09/05)

---

<!--You can leave these HTML comments in your merged IIP and delete the visible duplicate text guides, they will not appear and may be helpful to refer to if you edit it again. This is the suggested template for new IIPs. Note that an IIP number will be assigned by an editor. When opening a pull request to submit your IIP, please use an abbreviated title in the filename, `iip-draft_title_abbrev.md`. The title should be 44 characters or less.-->


## Simple Summary
Identity management interface with cross chain capabilities. Each identity can set preferences that are readable from multiple blockchains.

## Abstract
Blockchains storing data should be available to Web3 apps requards less if the dApp supports the network. When cross-chain interoperability becomes common across hundreds of blockchains, dApps that support different blockchain networks can support sharing of user data preferences that are linked on the blockchain.

## Motivation
The future of blockchains will have millions of blockchains that carry all kinds of data. Blockchains communicating with one another will be similar to the current distributed systems. Users should have a way for other blockchains to know what preferences the user wants depending on the web3 application. To achieve this there can be identity contracts that keeps track of identities and their preferences. Once users have an established preference they should be able be able to allow web3 apps to access the preferences from the blockchain. The use of preferences is important to protect user data that could be stored off chain.

## Specification

#### getPref
> - Get the preference bytes32 hash
```yaml
- name: getPref
	type: function
	stateMutability: view
	inputs:
		- name: id
		type: int
	outputs:
		- name: _userPref
		type: String

```

#### getActivityPref
> - Get the activity link stored in token URI
```yaml
- name: getActivityPref
	type: function
	stateMutability: view
	inputs: 
		- name: user
		type: address
	outputs:
		- name: tokenURI
		type: String

```

#### approvedAccess
> - Get the approved addresses for this issuer
```yaml
- name: approvedAccess
	type: function
	stateMutability: view
	inputs:
		- name: user
		type: address
	outputs:
		- name: approveId
		type: bool

```

#### didInfo
> - Get the DID URL
```yaml
- name: didInfo
	type: function
	stateMutability: view
	inputs:
		- name: user
		type: address
	outputs:
		- name: _didInfo
		type: String

```

#### addPref
> - Add preference for a user, should link to user preference
```yaml
- name: addPref
	type: function
	stateMutability: nonpayable
	inputs:
		- name: pref
		type: byte
	outputs:
		[ ]

```

#### addParty
> - Approve addresses to use activityMint

```yaml
- name: addParty
	type: function
	stateMutability: nonPayable

	inputs:
		- name: user
		type: address
		- name: uri
		type: String
	outputs:
		[ ]

```

#### activityMint
> - Mint token for each activity
```yaml
- name: activityMint
	type: function
	stateMutability: nonpayable
	inputs:
		- name: from
		type: address
		- name: to
		type: address
		- name: uri
		type: String
	outputs:
		[ ]

```

#### handleCallMessage
> - Handle xCall message call
  ```yaml
- name: handleCallMessage
	type: function
	stateMutability: nonpayable
	inputs:
		- name: _from
		type: string
		- name: data
		type: Class 
	outputs:
		- name: getPref
		type: String
		- name: activityMint
		type: String
		- name:revert
		type: revert

   ```

### Interacting With Contracts

```js

/* 
* @dev Send message to contract on desination
* @param {string} _to The BTP(Blockchain Transmisson Protocol) address of the callee on the destination chain
* @param {object} _data The calldata for the destination chain
*/
async function sendMessage(_to, _data)

/*
* @dev Get sendMessage() call result, if fail retry?
* @param{object} rs The rs of the sendMessage() txns 
*/
async function messageResult(rs)

/*
* @dev Listen for event on destination chain
* @param {object} abi
* @param {string} address EVM xCall address 
* @return {object} contractObject
* 
*/
const cmFilters = async function getContractObjectEVM(abi, address)

/*
* @dev Wait for callMessage event on destiation chain
* @param {string} contract address of EOA?? destination?? xCall??
* @param{object} cmfilters Object returned from getContractObjectEVM callMessageFilters

* @return events arguments
* @param _from The BTP address of the caller on the source chain
* @param _to A string representation of the callee address
* @param _sn The serial number of the request from the source
* @param _reqId The request id of the destination chain
* @param _data The calldata
*/
const events = async function waitEventEVM(contract, cmFilters)
/*
* @dev Once you have verifed that the event has been raised in the destniation chain, call the handleCallMessage. This is done by calling excuteCall
* @param _reqId The request id from events.reqId
* @param data The calldata
*/
async function excuteCall(reqId, data)

/*
* @dev Fetch the event on destination chain after executeCall
* @param contract Address of contract on destination chain
* @param filter List of events
* @param reciept 

*/
function filterEventEVM(contract, filter, reciept)


```

## Rationale
<!--The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g. how the feature is supported in other languages. The rationale may also provide evidence of consensus within the community, and should discuss important objections or concerns raised during discussion.-->


## Backwards Compatibility
<!--All IIPs that introduce backwards incompatibilities must include a section describing these incompatibilities and their severity. The IIP must explain how the author proposes to deal with these incompatibilities. IIP submissions without a sufficient backwards compatibility treatise may be rejected outright.-->

## Test Cases
<!--Test cases for an implementation are mandatory for IIPs that are affecting consensus changes. Other IIPs can choose to include links to test cases if applicable.-->


## Implementation
<!--The implementations must be completed before any IIP is given status "Final", but it need not be completed before the IIP is accepted. While there is merit to the approach of reaching consensus on the specification and rationale before writing code, the principle of "rough consensus and running code" is still useful when it comes to resolving many discussions of API details.-->


## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
