 

```bash
# tf1.12
conda create -y -n tf1 python=3.6 tensorflow-gpu=1.12 keras=2.2.4 &&
conda activate tf1 &&
pip install pandas tqdm sklearn
# pip install glove_python gensim 

# tf2.2
conda create -y -n tf2 python=3.8 tensorflow-gpu=2.2 &&
conda activate tf2 &&
pip install pandas tqdm sklearn

# torch1.4
conda create -y -n torch python=3.8 pytorch=1.4.0 &&
conda activate torch &&
pip install gensim pandas tqdm sklearn
```

环境详见requirements_tf1.txt，requirements_tf2.txt 和 requirements_torch.txt

#### 3. 运行

```bash
bash run.sh
```

运行顺序是：

```bash
#!/bin/bash
bash preprocess/run.sh &&  # 数据预处理
bash get_emb/run.sh &&     # embedding
bash model/run.sh &&       # 模型的训练，均采用20分类进行预测
bash oof/run.sh &&         # 对模型训练的输出结果进行归并，处理成model.npy，里面是[400w,20]的矩阵
bash ensemble/run.sh       # 对模型的oof做stacking，用的是Ridge
echo "all done!"
```

 

