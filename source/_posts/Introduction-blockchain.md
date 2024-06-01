---
title: 區塊鏈介紹
date: 2022-05-13 10:16:09
tags:
  - Blockchain
categories: 
  - Blockchain
thumbnail: https://firebasestorage.googleapis.com/v0/b/camila-dev-blog.appspot.com/o/DALL%C2%B7E%202024-05-26%2014.18.02%20-%20A%20modern%20digital%20banner%20illustrating%20the%20concept%20of%20blockchain.%20The%20banner%20features%20key%20elements%20such%20as%20interconnected%20blocks%20forming%20a%20chain%2C%20nodes%2C.webp?alt=media&token=82d548de-6bf6-4f2f-8ef8-cccfa2482b3d
excerpt: 介紹了區塊鏈的基本概念、去中心化的意義及不同的共識機制，並提供了一些額外的學習資源
---

### 何謂區塊鏈？

- 區塊鏈是一種去中心化的分佈式帳本技術，利用雜湊演算法確保每個區塊的唯一性。雖然有極小機率會造成區塊碰撞（hash值重複），但這種情況非常罕見。

    ![Hash計算過程](https://firebasestorage.googleapis.com/v0/b/camila-dev-blog.appspot.com/o/Untitled.png?alt=media&token=1f5f94bb-d946-4b16-9334-152f3b4755e0)

- 由於每一個區塊都會紀錄父節點的hash值，因此若被人意圖竄改，竄改速度必須要比其他區塊節點接受者還要快速才會被認可，否則會被網路拒絕。

### 去中心化

區塊鏈利用分散式帳本技術，讓所有節點達成共識，避免單一控制點的風險，提高系統的安全性和透明度。

### 共識機制

- POW (工作量證明)
  - 目前比特幣採用的共識機制
  - 透過礦工計算數學題比賽來獲得記帳權，成功者把區塊添加到區塊鏈上，並獲得貨幣獎勵。

- 其他共識機制
  - 市面上各種幣有各式各樣的共識機制，如POS（權益證明）、DPOS（委託權益證明）等，各有其優劣和適用場景。

    ![各種幣別的共識制度](https://miro.medium.com/max/2000/1*Sk0ceaeM3EqeD9EPO-3b6g.png)

### 工具

- [Etherscan](https://etherscan.io/) 可觀察區塊或交易訊息，當礦工取得記帳權之後，將以下資訊打包成區塊上鏈並獲得獎勵。

    ![Untitled](https://firebasestorage.googleapis.com/v0/b/camila-dev-blog.appspot.com/o/Untitled%201.png?alt=media&token=51ebe597-e0bc-49b0-b307-7b6923aafb66)

---

### 其他學習資源

> [區塊鏈知識 - 桑幣知識+](https://know.zombit.info/blockchain/)
