# DSAI2022_HW2-AutoTrading
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
