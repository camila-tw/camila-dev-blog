---
title: 智能合約語言認識
date: 2022-05-13 10:26:31
tags:
  - blockchain
thumbnail: https://firebasestorage.googleapis.com/v0/b/camila-dev-blog.appspot.com/o/DALL%C2%B7E%202024-05-26%2010.28.21%20-%20A%20modern%20digital%20banner%20illustrating%20various%20programming%20languages%20used%20for%20smart%20contract%20development.%20The%20banner%20features%20prominent%20logos%20and%20symbol.jpeg?alt=media&token=025cb54b-85a0-4a1c-a554-b56762c87888

excerpt: 介紹了多種智能合約開發語言，包括 Solidity、Rust、JavaScript (Web3.js)、Vyper 及其他語言，如 Python、Go、C++、Move、LLL、Michelson、DAML 和 Plutus。每種語言都有其特定的應用場景和優勢，適合不同的區塊鏈平台。本文提供了每種語言的簡介和示例代碼，幫助讀者了解並選擇合適的語言來開發智能合約。
---

## Solidity

Solidity 是一種高級編程語言，專門用於在區塊鏈平台（如以太坊、幣安鏈、Tron、Avalanche 等）上開發智能合約。

### 使用範圍:
  幣安鏈、Ethereum、Tron、Avalanche...etc.

### Example:

        ```solidity
        pragma solidity ^0.8.7;
        
        contract MyContract {
        
            constructor() public{
        
                value = "My value";
            }
        
            string public value;
        
            function get() public view returns (string memory){
                return value;
            }
        
            function set(string memory _value) public{
                value = _value;
            }
        }
        ```

## Rust

Rust 是一種系統編程語言，適用於 Solana、Polkadot 等區塊鏈平台的智能合約開發。

### 使用範圍: 
Solana、Polkadot...etc

### Example

    ```rust
    async fn main() -> web3::Result {
        let _ = env_logger::try_init();
        let http = web3::transports::Http::new("http://localhost:8545")?;
        let web3 = web3::Web3::new(web3::transports::Batch::new(http));
    
        let accounts = web3.eth().accounts();
        let block = web3.eth().block_number();
    
        let result = web3.transport().submit_batch().await?;
        println!("Result: {:?}", result);
    
        let accounts = accounts.await?;
        println!("Accounts: {:?}", accounts);
    
        let block = block.await?;
        println!("Block: {:?}", block);
    
        Ok(())
    }
    ```

## JavaScript

### [web3.js](https://web3js.readthedocs.io/en/v1.5.2/)

是一個函式庫，把以太坊的 `JSON-RPC API` 重新封裝過，並添加一下實用的函式庫，常用於 `Dapp` 網站的前端部分。

### Example

    ```jsx
    var Contract = require('web3-eth-contract');
    
    // set provider for all later instances to use
    Contract.setProvider('ws://localhost:8546');
    
    var contract = new Contract(jsonInterface, address);
    
    contract.methods.somFunc().send({from: ....})
    .on('receipt', function(){
        ...
    });
    ```

## **[Vyper](https://vyper.readthedocs.io/en/stable/)**

  - Vyper 是除 Solidity 外，以太坊上的另一Smart Contract Language。
  - 其語法和 Python 相近。
  - 主要被設計和 Solidity 的區別是**安全性**及**可讀性。**

### Example

    ```solidity
    @internal
    def _times_two(amount: uint256) -> uint256:
        return amount * 2
    
    @external
    def calculate(amount: uint256) -> uint256:
        return self._times_two(amount)
    ```

這些是常見智能合約語言的簡介和示例。每種語言都有其特定的應用場景和優勢，可以根據需求選擇合適的語言來開發智能合約。

## 其他智能合約語言
### Python
Python 是一種廣泛使用的高級編程語言，可以用來開發智能合約。以太坊有一個名為 Py-EVM 的 Python 實現，以及 Brownie 框架，這些都可以用於編寫和測試智能合約。

### Go

Go 語言（Golang）也被用來開發智能合約，尤其是在 Hyperledger Fabric 平台上。Hyperledger Fabric 是一個企業級的區塊鏈平台，支持用 Go 語言編寫鏈碼（智能合約）。

### C++

C++ 是一種高效的系統編程語言，被 EOS.IO 區塊鏈平台用來編寫智能合約。EOS.IO 提供了一個強大的 C++ 智能合約開發框架，允許開發者構建高性能的區塊鏈應用。

### Move

Move 是一種新興的智能合約語言，專為 Libra（現在的 Diem）區塊鏈平台設計。Move 語言旨在提高智能合約的安全性和靈活性。

### LLL (Low-Level Lisp-like Language)

LLL 是一種低級的 Lisp 類語言，專門為以太坊智能合約設計。它的語法簡潔，適合那些需要直接操作以太坊虛擬機（EVM）的開發者。

### Michelson

Michelson 是 Tezos 區塊鏈平台使用的智能合約語言。它是一種堆棧語言，專為形式化驗證和安全性設計。

### DAML

DAML 是一種智能合約語言，用於數字資產和分佈式賬本技術（DLT）平台，如 Hyperledger Sawtooth 和 Corda。DAML 專注於業務邏輯和合約安全。

### Plutus

Plutus 是 Cardano 區塊鏈平台的智能合約語言，基於 Haskell 語言。Plutus 提供了強大的數學和形式化驗證工具，以確保智能合約的正確性和安全性。
