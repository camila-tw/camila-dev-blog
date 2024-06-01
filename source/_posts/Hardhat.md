---
title: Hardhat
date: 2022-05-27 15:02:41
tags:
  - Blockchain
  - SmartContract
  - Tools
categories: 
  - Blockchain
thumbnail: https://firebasestorage.googleapis.com/v0/b/camila-dev-blog.appspot.com/o/DALL%C2%B7E%202024-05-27%2015.12.57%20-%20A%20modern%20digital%20banner%20for%20a%20blog%20post%20about%20Hardhat%2C%20an%20Ethereum%20development%20tool.%20The%20banner%20features%20the%20Hardhat%20logo%2C%20a%20construction%20hat%2C%20and%20ele.webp?alt=media&token=fbb84b06-45ba-41a7-991d-b7bbc44a027c
excerpt: 介紹Hardhat，一款兼容 EVM 的開發工具，專為以太坊和其他 EVM 兼容區塊鏈的開發者設計。詳細說明Hardhat簡介、安裝步驟、環境建置過程，以及如何編譯、部署和測試智能合約。內容包括配置 Hardhat、編寫和運行部署腳本以及測試合約的詳細說明，是一份全面的 Hardhat 使用指南。
---

### 簡介

Hardhat 是一款兼容 EVM (Ethereum Virtual Machine) 的開發工具，專為以太坊和其他 EVM 兼容區塊鏈的開發者設計。它提供了強大的開發環境，讓開發者可以輕鬆地編譯、測試和部署智能合約。

- **本地開發**
  - 支持使用常用的編輯器進行開發，如 VSCode。
  - 在本地端即可提供以下功能：編譯、測試、部署。
  - 提供本地端的測試用區塊鏈，亦可模擬其他鏈的資料，方便開發和測試。

- **提供多種插件**
  - **Etherscan 驗證**：自動驗證和發布智能合約到 Etherscan。
  - **Gas fee 消耗報告**：分析智能合約的 gas 消耗，幫助優化合約。
  - **智能合約內的 log**：方便地查看和調試合約中的 log 訊息。

### 安裝

要開始使用 Hardhat，可以按照以下步驟進行安裝：

```bash
# 1. 首先創立專案用的資料夾
mkdir your-solidity-project
cd your-solidity-project

# 2. 安裝 hardhat
npm install --save-dev hardhat

# 3. 創立 hardhat 專案
npx hardhat

# 4. 選擇 "Create a sample project" 並按下 Enter，其他提示也按 Enter 即可
# 5. 靜待安裝後即可完成
```

### 環境建置

#### 初始化專案

在初始化 Hardhat 專案後，會看到一個包含以下文件和資料夾的目錄結構：

+ contracts/：存放智能合約的目錄。
+ scripts/：存放部署腳本的目錄。
+ test/：存放測試文件的目錄。
+ hardhat.config.js：Hardhat 的配置文件。

#### 配置 Hardhat
在 hardhat.config.js 文件中配置 Hardhat 的各種選項，例如設置網絡、編譯器版本等：

``` javascript
require("@nomiclabs/hardhat-waffle");

module.exports = {
  solidity: "0.8.7",
  networks: {
    hardhat: {
      chainId: 1337
    },
    rinkeby: {
      url: "<https://rinkeby.infura.io/v3/YOUR_INFURA_PROJECT_ID>",
      accounts: ["YOUR_PRIVATE_KEY"]
    }
  }
};
```

#### 編譯合約

要編譯智能合約，可以執行以下命令：

``` bash
npx hardhat compile
```

#### 部署合約

在 scripts/ 目錄中創建一個部署腳本（例如 deploy.js），並添加以下內容：

``` javascript
async function main() {
  const [deployer] = await ethers.getSigners();

  console.log("Deploying contracts with the account:", deployer.address);

  const Token = await ethers.getContractFactory("Token");
  const token = await Token.deploy();

  console.log("Token contract deployed to:", token.address);
}

main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```

然後執行以下命令來部署合約：

```bash
npx hardhat run scripts/deploy.js --network rinkeby
```

#### 測試合約

在 test/ 目錄中創建測試文件（例如 Token.js），並添加測試內容：

``` javascript
const { expect } = require("chai");

describe("Token contract", function () {
  it("Deployment should assign the total supply of tokens to the owner", async function () {
    const [owner] = await ethers.getSigners();

    const Token = await ethers.getContractFactory("Token");

    const hardhatToken = await Token.deploy();

    const ownerBalance = await hardhatToken.balanceOf(owner.address);
    expect(await hardhatToken.totalSupply()).to.equal(ownerBalance);
  });
});
```

#### 運行測試

``` bash
npx hardhat test
```
