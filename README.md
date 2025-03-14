# iLoRA
https://arxiv.org/pdf/2408.10159

1. 传统方法的缺点 （利用LLM生成式序列推荐）
 1)将一系列历史行为转换为提示;(2)将这些提示与后续感兴趣的项目配对，以创建指令微调数据集;(3)将可训练的Low-RankAdaptation(LoRA)模块(5,16,10,9】集成到LLMs中，并在这些提示上进行微调。现有研究【17,3,18,6,9,10,16】主要关注于优化高质量的提示，以更有效地整合推荐信息，同时没有探索LoRA的选择。相反，它们使用标准的LoRA模块进行微调，该块冻结LLMs权重并通过两个额外的低秩矩阵更新型。

我们的方法考虑用户行为多样性，观察的现象：
  LTäRA当不同的序列相关联，并显示出显著的错位，如图所示。1.具体来说，我们观察到在协作空间中，沿着梯度相似性矩阵的对角线，成员接近性形成了强烈的聚类。同时，在协作空间中距离较远的聚类倾向于表现出不同的梯度轨迹。显然，这些梯度是不一致的，这可能导致性能不佳。为了缓解这个问题，一个直接的解决方案是部署多个LORA模块，每个模块针对特定的序列进行微调，使每个模块能够作为轻量级专家，针对其各自的序列进行操作。然而，从资源和时间复杂性的角度来看，这是不切实际的，因为序列的数量通常达到数百万。
  <img width="1345" alt="image" src="https://github.com/user-attachments/assets/3a3f8e9a-9517-4b41-960f-3d98ec044777" />

LoRA主要更新transformer的投影矩阵：
  <img width="1354" alt="image" src="https://github.com/user-attachments/assets/ffe882c2-0767-4ea6-9501-e5b3566262d4" />

保持总参数量一致： <img width="1400" alt="image" src="https://github.com/user-attachments/assets/3593d3e6-5adb-4de8-aab7-489e0f433896" />


注意维度： 整个序列输入到SR-EMB得到一个emb
<img width="1356" alt="image" src="https://github.com/user-attachments/assets/c134ecc2-684a-4b55-af79-7059b10c7acd" />
