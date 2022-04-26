# DSAI2022_HW2-AutoTrading
## Overview
### NCKU DSAI HW2 - AutoTrading

根據 NASDAQ:IBM 中的股票價格資料，使用 LSTM 模型，預測出是否買入或是賣出。

## Data
### Stock Prices
* 資料：NASDAQ:IBM的價格資料
* 說明：資料中依序包含 IBM 5年的開盤、最高、最低、收盤（open、high、low、close）。

## Method & Training
### Data Selection
我們分別利用 open、high、low、close訓練出LSTM模型(一層)，最終依據結果選擇了close做為訓練的資料。

open：

![GITHUB](https://github.com/fylin625/DSAI2022_HW2-AutoTrading/blob/main/images/open.png?raw=true)

high：

![GITHUB](https://github.com/fylin625/DSAI2022_HW2-AutoTrading/blob/main/images/high.png?raw=true)

low：

![GITHUB](https://github.com/fylin625/DSAI2022_HW2-AutoTrading/blob/main/images/low.png?raw=true)

close：

![GITHUB](https://github.com/fylin625/DSAI2022_HW2-AutoTrading/blob/main/images/close.png?raw=true)

### training model 
由於股票價格有關於時間序列，所以我們選用LSTM模型。


我們預測出的結果如下：

![GITHUB](https://github.com/fylin625/DSAI2022_HW2-AutoTrading/blob/main/images/GPU.png?raw=true)
## Trader Strategy
判斷目前股票數量為0、1或-1，並以買入之收盤價與預測收盤價比較，以此為依據判斷動作為買、賣、持有，並記錄每一次買入時所花費的價錢。

我們將買入股票的開盤價與預測的開盤價比價差。

當價差大於0時賣出，反之持有。

ex1:持有股票數量為0，預測開盤價<預測前一天開盤價(跌)則買入，action為1，反之賣空，action為-1。

ex2:持有股票數量為-1，預測開盤價與賣空價價差小於0.6則買入，action為1，反之持有，action為0。

ex3:持有股票數量為1，當時買入此張股票的開盤價與預測開盤價價差小於0.6則繼續持有，action為0，反之賣出，action為-1。

```
目前持有股票 |     預測開盤價與買進開盤價比較    | 執行動作 
-------------------------------------------------------
     0      |    預測開盤價 < 預測前一天開盤價  |    1  
-------------------------------------------------------
     0      |    預測開盤價 > 預測前一天開盤價  |   -1  
-------------------------------------------------------
     1      |      預測開盤價 < 買進開盤價     |    0  
-------------------------------------------------------
     1      |      預測開盤價 > 買進開盤價     |   -1  
-------------------------------------------------------
    -1      |      預測開盤價 < 賣空開盤價     |    1  
-------------------------------------------------------
    -1      |      預測開盤價 > 賣空開盤價     |    0  
-------------------------------------------------------
```

## Run

環境 Python "3.7.1"

```
conda create -n auto_trading python=="3.7"
```
```
activate auto_trading
```
路徑移至 requirements.txt 所在的資料夾，輸入安裝套件指令
```
conda install --yes --file requirements.txt
```
將 trader.py、training.csv、testing.csv、output.csv 下載至同資料夾內

輸入以下指令
```
python trader.py --training training.csv --testing testing.csv --output output.csv
