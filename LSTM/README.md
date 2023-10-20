# 1 模型综述

本模型是针对于加密货币的收盘价进行预测，使用的是朴素LSTM模型。对于Seq2Seq模型而言，在测试集输入初期
加入一小段训练集加以矫正是有必要的，故在本模型中抽取50个训练集中的GroundTruth，对测试集输出进行矫正

# 2 数据来源
本次实验所选的货币是
[Crypto网站](https://crypto.com/price/categories/gamefi)中MarketCap排名前21的GameFi加密货币，
数据来自于[CoinMarketCap网站](https://coinmarketcap.com/)，选取的数值时间范围在2021/10/01-2023/10/01
选取的数据为：Open, High, Low, Close, Volume, MarketCap, 预测目标为Close

但部分数据出现一些问题：
- **Echolon** 只有2023/3-2023/10的[Echelon数据](https://coinmarketcap.com/currencies/echelon-prime/)，且市值全部为0, 故删去
                MarketCap，只输入四个元素
- **ECOMI** 由于官网提供的[ECOMI数据](https://coinmarketcap.com/currencies/ecomi-new/)中的MarketCap值为0，故只得在输入特征中删去MarketCap这一项，同时在训练过程中也不对其进行预测。
- **GALA** 由于收盘价波动明显异于其他货币，故另训练一个模型
- **Illuvium** 由于收盘价明显高于其他货币，故另训练一个模型

# 3 环境
- CPU: Intel(R) Core(TM) i7-10700K CPU @ 3.80GHz
- GPU: NVIDIA GeForce RTX 3050 Ti
- Python: 3.9
- Pytorch: 2.1.0 + CU117
- CUDA: 11.7

# 4 运行结果

| 货币种类          | R_square | MAPE    |
|---------------|----------|---------|
| Render_Token  | 0.96648  | 2.6205% |
| ImmuterX      | 0.90364  | 3.4494% |
| The Sandbox   | 0.9974   | 0.7754% |
| Axie Infinity | 0.9091   | 3.9181% |
| Decentraland  | 0.9942   | 1.2295% |
| Chiliz        | 0.9605   | 3.3264% |
| ApeCoin       | 0.8381   | 9.8433% |
| Gala          | 0.2848   | 15.312% |
| Wemix         | 0.6506   | 11.234% |
| ECOMI         | 0.9771   | 1.8356% |
| Enjin         | 0.9937   | 0.9350% |
| GMT           | 0.2973   | 13.479% |
| WAX           | 0.1069   | 11.685% |
| Floki         | 0.9850   | 1.9770% |
| MeritCircle   | 0.7350   | 12.721% |
| Illuvium      | 0.7647   | 3.4984% |
| BORA          | 0.9587   | 2.3867% |
| Magic         | 0.9838   | 2.3308% |
| Echelon       | 0.8678   | 3.6312% |
| Vulcan        | 0.7658   | 2.9093% |


