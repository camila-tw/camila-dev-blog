# Camila's Hexo Dev Blog

這是一個使用 Hexo 構建的靜態博客，並使用 Git 子模組來管理主題。

## 目錄

- [安裝](#安裝)
- [配置](#配置)
- [使用](#使用)
- [部署](#部署)
- [注意事項](#注意事項)
- [許可證](#許可證)

## 安裝

1. 克隆這個倉庫：

    ```bash
    git clone https://github.com/camila-tw/camila-dev-blog.git
    cd camila-dev-blog
    ```

2. 初始化子模組以獲取主題：

    ```bash
    git submodule update --init --recursive
    ```

    如果子模組沒有被正確初始化，請確認 `.gitmodules` 文件是否存在且配置正確。該文件應該包含以下內容：

    ```plaintext
    [submodule "themes/hexo-theme-redefine"]
        path = themes/hexo-theme-redefine
        url = https://github.com/camila-tw/hexo-theme-redefine.git
    ```

    如果 `.gitmodules` 文件不存在或配置不正確，請手動添加並初始化子模組：

    ```bash
    git submodule add https://github.com/camila-tw/hexo-theme-redefine.git themes/hexo-theme-redefine
    git submodule update --init --recursive
    ```

3. 安裝 Hexo 所需的依賴：

    ```bash
    npm install
    ```

## 配置

1. 打開 Hexo 配置文件 `_config.yml`，並確保 `theme` 設置為你克隆的主題名稱。例如：

    ```yaml
    theme: hexo-theme-redefine
    ```

2. 如果主題有特定的配置，請參考 `themes/hexo-theme-redefine` 下的 `_config.yml` 進行配置。

## 使用

1. 生成靜態文件：

    ```bash
    hexo generate
    ```

2. 啟動本地服務器：

    ```bash
    hexo server
    ```

3. 打開瀏覽器並訪問 `http://localhost:4000` 查看博客。

## 部署

此博客使用 GitHub Pages 部署。部署到 `gh-pages` 分支後，可以通過 [https://camila-tw.github.io/camila-dev-blog](https://camila-tw.github.io/camila-dev-blog) 訪問。

1. 在 `_config.yml` 中設置部署配置：

    ```yaml
    deploy:
      type: git
      repo: https://github.com/camila-tw/camila-dev-blog.git
      branch: gh-pages
    ```

2. 部署到遠端倉庫：

    ```bash
    hexo deploy
    ```

## 注意事項

- 每次克隆倉庫後，記得初始化子模組。
- 如果子模組初始化失敗，請檢查 `.gitmodules` 文件的配置並重新初始化子模組。
- 如需更新主題，請參考主題的官方文檔。

## LICENSE

本項目基於 GNU General Public License v3.0 許可證開源。詳細信息請參閱 LICENSE 文件。
