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

由於close、open之間存在延遲一天的關係，因此將使用close作為模型訓練的特徵。

### training model 
由於股票價格有關於時間序列，所以我們選用LSTM模型。

model summary：

![GITHUB](https://github.com/fylin625/DSAI2022_HW2-AutoTrading/blob/main/images/summary.PNG?raw=true)

我們預測出的結果如下：

![GITHUB](https://github.com/fylin625/DSAI2022_HW2-AutoTrading/blob/main/images/GPU.png?raw=true)
## Trader Strategy

若預測出的開盤價大於前一天的開盤價，也就是漲價，則執行賣出的動作（-1）。

若預測出的開盤價小於於前一天的開盤價，也就是跌價，則執行買入的動作（1）。

但若是在持有股票的狀況下預測到隔天漲價或賣空股票的狀況下預測隔天跌價，則不執行動作（0）。

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
