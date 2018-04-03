---
title:  How to Install XGboost
date: 2018/1/23 20:35:32
categories: 
- python


tags: 
- python
- speedml
- XGboost
- environment
- deep learning
- machine learning


---


## 背景
- 深度学习的 kaggle 平台, Titanic项目 推荐 speedml[Titanic Data Science Solutions | Kaggle](https://www.kaggle.com/startupsci/titanic-data-science-solutions/notebook), speedml 需要提前安装 [Xgboost](https://en.wikipedia.org/wiki/Xgboost), 这个[在机器学习竞赛中表现卓越](https://juejin.im/post/5a03fabcf265da432b4a44e2)的模块.

```pip install speedml
```

报错: XGBoostLibraryNotFound 

```
Command "python setup.py egg_info" failed with error code 1 in /private/var/folders/mx/jr287k4x6x50nkb0t20x4lcc0000gn/T/pip-build-iulz4qok/xgboost/.
```

- 查到: [xgboost/build_trouble_shooting.md at master · dmlc/xgboost](https://github.com/dmlc/xgboost/blob/master/python-package/build_trouble_shooting.md) 
- [Discussion and troubleshooting on PyPI (pip) installation (the newest 0.6 version) · Issue #1446 · dmlc/xgboost](https://github.com/dmlc/xgboost/issues/1446)
- 尝试 ```brew install gcc``` 和 ```clang-omg```, 找不到模块

## xgboost
- 要用到 [GCC](https://zh.wikipedia.org/wiki/GCC)
-  GCC 之前要按照 xcode(苹果商店就有)

## 操作
- 安装时遵循 [xgboost官方github](https://github.com/dmlc/xgboost/tree/master/python-package), 不要使用 ```pip install xgboost```的方式, 而是使用 clone文件夹到本地的方式(from source). 
- 先安装 gcc@5
    - set compiler 的方法是: 在 config.mk(在 xgboost 里) 中添加: ```export CC = gcc-5 ,export CXX = g++-5```
- 官网 [Installation Guide — xgboost 0.6 documentation](https://xgboost.readthedocs.io/en/latest/build.html) from source. 
- ```make -j4``` 这一步可能会遇到 [Error installing xgboost with OpenMP-enabled compliers · Issue #1442 · dmlc/xgboost](https://github.com/dmlc/xgboost/issues/1442)  按上文 set compiler 即可. 
- 如果你的 python 环境另有设置, 比如我用了 pyenv 来管理 python 的版本, 即在 ```cd xgboost``` 后, 使用: ```cd python-package; sudo python setup.py install```, 即可将 xgboost 转到相应的路径下. 
- 以上的安装步骤可参照: [Installing XGBoost on Mac OSX (IT Best Kept Secret Is Optimization)](https://www.ibm.com/developerworks/community/blogs/jfp/entry/Installing_XGBoost_on_Mac_OSX?lang=en)
- 在安装了 xgboost 后, ```pip install speedml```, 安装成功后, ```import speedml``` 检测成功.

