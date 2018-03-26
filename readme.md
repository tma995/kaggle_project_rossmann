# Rossmann Store Sales Prediction
### 机器学习项目实践
-----
### 项目文件：
* 总结报告：`report.pdf`
* 程序--数据预处理及特征工程：`rossmann_data_preprocess.ipynb`
* 程序--模型训练（划分训练数据最后六周为验证集）：`rossmann_train_validate_xgb.ipynb`
* 程序--模型训练（所有数据参与训练）：`rossmann_train_predict_xgb.ipynb`
* 数据文件：`data`目录下，`train.csv`，`test.csv`，`store.csv`，可从Kaggle直接下载，为保程序正常运行，数据需放在data目录下；

### 环境搭建：
* `ubuntu linux`操作系统，我在aws运行时选择的多核cpu实例的型号为c5.18xlarge；
* 代码运行在Jupyter Notebook
* 主要python库：pandas, numpy, matplotlib, seaborn, xgboost, sklearn；

### 运行概述：
* 数据预处理：主要耗时在生成店铺+日期的衍生变量，因循环程序为单核处理，大概需两小时，其他模块耗时可忽略；生成数据供后续模型训练使用；
* 常规模型训练：见`rossmann_train_validate_xgb.ipynb`
>* 在取训练数据最后六周为验证集的条件下，模型训练在迭代500颗树左右收敛，对验证集的预测效果很好，具体见可视化图表；
>* 提交Kaggle的测试集预测分数达到0.11656，高于设定对基准分数0.11773（Top 10%）；
* 尝试训练全量数据：
>* 因上述方案中，验证集在时间维度离测试集最近，理论上两者有更强的相关性，故尝试将其也直接放入训练集训练，在迭代1万多棵树后，提交Kaggle的分数进一步增加，达到0.11413，可以排到106名，约前3%；
>* 在该项尝试中，由于计算量大，耗时很长；基于aws虚拟机，CPU版本的xgboost，n_thread=16，训练耗时约3小时；
* 实际运行中，可以跳过网格搜索优化参数模块，直接运行训练模块； 
* 上述几项程序总耗时约5到6小时；