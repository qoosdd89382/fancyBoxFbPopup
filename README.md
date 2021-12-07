# [2021/12/06] Fancybox Popup 說明

# Resources

1. [Github 靜態預覽頁面](https://qoosdd89382.github.io/fancyBoxFbPopup/index.html)：
主要是讓我們看目前測試機的 css 可以呈現什麼樣的基本效果
2. [Github 專案倉庫下載網址](https://github.com/qoosdd89382/fancyBoxFbPopup/archive/refs/heads/main.zip)：
提供範例檔案下載
3. [Jsfiddle 提供的所見即所得服務](https://jsfiddle.net/qoosdd89382/yL7gdqaw/)：
**讓我們可以即時看到修改的效果（在電腦環境不能裝配模擬伺服器開發工具的狀況下，折衷用這個方案）**

# TL;DR

做任何修改前請先按 Fork：

![Untitled](https://github.com/qoosdd89382/fancyBoxFbPopup/blob/ab3b40f7f3f0dd4b3cee1da8c6ef39c80d795c4b/%5B2021%2012%2006%5D%20Fancybox%20Popup%20%E8%AA%AA%E6%98%8E%202864a0294d564abab1a421a30ebd1610/Untitled.png)

預覽前請先切到 Right results，最接近真實瀏覽器的高度，不然會有一些東西被遮到：

![Untitled](https://github.com/qoosdd89382/fancyBoxFbPopup/blob/ab3b40f7f3f0dd4b3cee1da8c6ef39c80d795c4b/%5B2021%2012%2006%5D%20Fancybox%20Popup%20%E8%AA%AA%E6%98%8E%202864a0294d564abab1a421a30ebd1610/Untitled%201.png)

以下修改可以由 Jsfiddle 提供所見即所得的預覽：

1. 彈窗「內容部分的樣式」在CSS 區塊可修改。
2. 彈窗「內容部分的文字」在 HTML `<body>` 標籤中可以修改。
3. `sub_style_newpopup.css`：定義外框的樣式，要修改請從測試區抓同名檔案的最新版，往後要修改可以去掉資源網址的引入，將檔案內容直接完整直接貼到  `<head>` 的 `<style>` 裏面，預覽完再貼回檔案。
**注意**：目前 `<style>` 中包含 `main_style.css` 擷取出來的部分預覽所需 css，將來若要修改，請勿一同貼回 `sub_style_newpopup.css` 。

# 內容與修改說明

在 Jsfiddle 專案中，可以看到瀏覽器分為三個區塊：

1. HTML
2. CSS
3. JavaScript

以下分別說明。

## 1. HTML

在這邊已經套用好完整的 HTML 結構，由 `<html>` tag 中包裹 `<head>` 和 `<body>` 兩個部分，目前 fancybox 所需要用到的 JS 和 CSS 已全部在 `<head>` 裡引入好了。

### (1) Head

**引入的 JS**

`<head>` 中引入的JS 套件如以下，除非版本有巨大異動，否則不需要特別更新：

1. jQuery 3.6.0：JavaScript 的函式庫套件，可以大幅減短 JS 原生語法的撰寫長度，奈米投目前拿來降低前端開發成本用。JS 區塊的程式都是以 jQuery 語法寫成。
2. jQuery Fancybox 3.5.7：popup 彈出機制使用的 jQuery 附加套件。

**引入的 CSS**

1. jQuery Fancybox 3.5.7 CSS
2. **`sub_style_newpopup.css`：**
從股感改版的舊戶新增計畫頁（new_investment.html）投組建議頁（result.html）中抽出整理而成（騰訊文檔有相關說明）。
現在只要任何一個 html 頁面中有引入這支 css 和 main_style.css，再加上前面提到的幾支 JS 檔案，就一定可以使用 fancybox 且帶有當前測試區版本彈窗的樣式。
引入的網址是我從 Github 專案中硬轉出來的，主要還是以測試區版本為主。
3. **被 `<style>` 標籤包裹的全域 CSS**：
由 main_style.css 中擷取 Fancybox 會用到的部分。
包含：桂青定義的彈窗 scroll 樣式、點開彈窗時背景自動鎖住不能滑動的 css......。

**其他必須引入的資源**

1. Google font api
2. Google font 靜態資源
3. 兩個 Google fonts  的引入：
思源黑體、Rajdhani

### (2) Body

1. 一個可以開啟某 fancybox 彈窗的 a 連結：
    
    ```html
    <a data-fancybox class="fancybox" data-src="#etfWarning"
    	href="javascript:void(0)">閱讀ETF投資須知</a>
    ```
    
    - 說明
        
        任何可以點擊的元素都可以綁定 fancybox，只要帶有以下兩個屬性：
        
        1. `data-fancybox` 是對 fancybox 機制有意義的屬性，也就是說有了這個才會去綁定機制。
        2. `data-src` 提供 fancybox 開啟資源的指向，也就是會去開啟有這個選擇器的資源，在此例中為 `id="etfWarning"` 的元素。
        
        其他屬性：
        
        1. `class="fancybox"` 對 fancybox 機制開啟與否本身沒有意義，但若有樣式定義在這個選擇器上，還是必須帶有（建議暫時不要拿掉）。
        2. `href` 屬性為 a 連結預設行為中會去開啟的 url 位置，`javascript:void(0)` 代表著這是一個無目標的死連結，用來停止預設開啟連結的行為。如果元素本身不是 a 連結可以不用寫這個部分。
2. 兩個 fancybox 的隱藏元素：fancybox 開啟時機制會淡入，關閉時會淡出。
必要組成：
    
    ```html
    <div class="popup info" style="display: none;" id="自訂選擇器名稱">
        <div class="contentFiller scroll">
            <!-- 內容 -->
        </div>
    </div>
    ```
    
    - 說明
        1. `class` 屬性都為定義樣式用，建議不要修改或移除
        2. `id` 和用來點擊的元素適配，一個畫面上只能有一個，請勿重複
3. 一個撐開高度用的 div[id="test"]，用來測試背景是否可以鎖住。fancybox 打開時捲軸會消失。

## 2. CSS

這邊的 CSS 和在 HTML 區塊中引用的不同，`sub_style_newpopup.css` 中定義的是目前這種 fancybox 的全域外框部分，這裡目前放的是內容部分的樣式。

## 3. JavaScript

基本上維持不動複製貼上就可以使用，以下還是會稍做說明。

這個範例專案中，fancybox 有兩種開啟方式：

1. **點擊才開啟**
    
    前面 HTML Body 的部分已經有提到如何綁定點擊事件（click event），不過這邊的 JS 區塊還是有對它做一些屬性的設定：
    
    ```jsx
    /** data-fancybox 屬性的彈窗全域設定 **/
    $('[data-fancybox]').fancybox({
      touch: false,
      beforeShow: function() {
        $("html").addClass('-htmlNotScroll');
      },
      beforeClose: function() {
        $("html").removeClass('-htmlNotScroll');
      }
    });
    ```
    
    - 說明
        1. 對此畫面上所有有 `data-fancybox` 屬性的 fancybox 實體進行設定
        2. `touch: false` 彈窗開啟時畫面禁止滑動關閉
        3. `beforeShow` 以 callback function 定義彈窗顯示前要做的事情，這裡是在 <html> 標籤加上 `-htmlNotScroll` class，讓背景不能滑動
        4. `beforeClose` 以 callback function 定義彈窗關閉前要做的事情，這裡是移除 <html> 標籤上的 `-htmlNotScroll` class，讓背景恢復為可以滑動
2. **進畫面由 JS 自動開啟**
    
    ```jsx
    // 不觸發元素點擊事件, js 開啟
    // 以進網頁後一秒觸發為例
    setTimeout(() => {
      $.fancybox.open(
        $('#nano2Coming'), {
          touch: false,
          beforeShow: function() {
            $("html").addClass('-htmlNotScroll');
          },
          beforeClose: function() {
            $("html").removeClass('-htmlNotScroll');
          }
        }
      );
    }, 1000);
    ```
    
    - 說明
        1. setTimeout 為計時用，與 fancybox 設定無關，可忽略
        2. `$.fancybox.open( $('選擇器') , { 相關設定} )` open 為一個方法，告訴 fancybox 讀到這時馬上打開這個選擇器的元素，並設定這個 fancybox 實體
        
        定義內容則可參考第 1 點，大同小異
