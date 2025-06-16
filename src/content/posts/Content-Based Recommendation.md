---
title: Content-Based Recommendation
author: Francisco
description: 基于内容的推荐系统通过分析用户历史行为和物品特征，为用户推荐相似内容。特征处理方法包括独热编码、标签编码、归一化、特征选择和提取，以及降维。代码示例展示了如何计算用户相似度并推荐商品。
pubDate: 2025-01-12
categories: ["Machine Learning"]
slug: ai-cbr
pin: false
---

## 基于内容的推荐系统[Content-Based Recommendation]

### 特征处理方式

#### 独热编码[One-Hot Encoding]

> 将每个分类特征转换为一个二进制特征向量，其中每个特征的值只有0或1。例: 对于一个性别特征，可以将它转换为两个二进制特征：一个表示男性，一个表示女性。男性特征向量为[1, 0], 女性对应的特征向量为[0, 1]。这种编码方式的好处是每个特征之间都是相互独立的，易于计算机处理和使用。

#### 标签编码[Label Encoding]

> 将每个分类特征转换为一个整数数值，其中每个整数代表一个分类。例: 对于一个性别特征，可以将它转换为0或1，其中0表示男性，1表示女性。这种编码方式的好处是可以减少特征的维度，但它的缺点是可能会产生一些误导性的关系，例如，计算机可能会认为女性是男性的两倍。

#### 归一化[normalization]

> 对于数值型特征，可以进行归一化或标准化处理，使得特征值具有相似的尺度范围。归一化将特征值缩放到0和1之间，而标准化则基于特征的均值和标准差进行缩放。这样处理可以避免某些特征对模型造成不必要的影响。

#### 特征选择[Feature Selection]

> 选择最相关的特征，以便于计算机处理和使用。例如，选择对用户推荐最相关的商品特征。

#### 特征提取[Feature Extraction]

> 从原始特征中提取出更有意义的特征，以便于计算机处理和使用。例如，从商品的标题、描述和图片中提取出商品的关键特征。

#### 降维[Dimensionality Reduction]

> 将高维特征空间降低到低维特征空间，以便于计算机处理和使用。例如，使用主成分分析（PCA）将商品的多个特征降低到几个主要特征。
> 会根据用户的历史行为和偏好，为用户推荐与其喜好相似的内容。它会分析项目或产品的特征以及用户的个人资料和历史数据，并基于这些信息预测用户的偏好。例如，根据用户过去观看的电影类型和电影的内容特征（演员、导演、类型等）来推荐相似的电影。内容就是特征, 用户和商品的特征就是内容, 人的特征有年龄, 性别, 兴趣爱好等, 商品的特征有价格, 功效, 等特征.
> 基于内容的推荐系统主要依赖于物品的特征信息进行推荐。用户也可以是物品, 商品也可以是物品.

### 基于用户偏好[人以群分]

- 特性：年龄, 性别, 职业, 地理位置[经度,纬度], 兴趣, 收入水平。
- 数据: 用户购买数据集。

#### 代码

```python
import pandas as pd
from sklearn.preprocessing import OneHotEncoder, MinMaxScaler
from sklearn.metrics.pairwise import cosine_similarity

# 读取用户数据集和购买记录数据集
users_df = pd.read_csv('users.csv')
purchases_df = pd.read_csv('purchases.csv')

# 使用独热编码处理分类特征
encoder = OneHotEncoder(sparse=False)
encoded_users = encoder.fit_transform(users_df[['gender', 'city']])
encoded_users_df = pd.DataFrame(encoded_users, columns=encoder.get_feature_names_out(['gender', 'city']))

# 归一化处理年龄特征
scaler = MinMaxScaler()
scaled_age = scaler.fit_transform(users_df[['age']])
encoded_users_df['scaled_age'] = scaled_age

# 计算用户之间的相似度矩阵
similarity_matrix = cosine_similarity(encoded_users_df)

# 获取与用户1最相似的用户
user_id = 1
similar_users = similarity_matrix[user_id-1]  # 索引从0开始，所以需要减1
most_similar_user_id = similar_users.argsort()[-2] + 1  # 最相似的用户排在最后，所以选择倒数第二个

# 获取用户1还没有购买过的商品
user1_purchased_products = purchases_df[purchases_df['user_id'] == user_id]['product_name'].tolist()
similar_user_purchased_products = purchases_df[purchases_df['user_id'] == most_similar_user_id]['product_name'].tolist()
recommended_products = list(set(similar_user_purchased_products) - set(user1_purchased_products))

print(f"推荐给用户1的商品：{recommended_products}")
```

#### 详解

1.导入所需的库

```python
import pandas as pd
from sklearn.preprocessing import OneHotEncoder, MinMaxScaler
from sklearn.metrics.pairwise import cosine_similarity
```

- Pandas：用于处理数据表格
- OneHotEncoder：用于对分类特征进行独热编码
- MinMaxScaler：用于对连续特征进行归一化处理
- Cosine_Similarity：用于计算用户之间的余弦相似度

  2.读取用户数据集和购买记录数据集

```python
users_df = pd.read_csv('users.csv')
purchases_df = pd.read_csv('purchases.csv')
```

- **users.csv**: 用户数据集

![image.png](https://s2.loli.net/2025/06/16/IbXxBzGSvh5jYg1.webp)

- **purchases.csv**: 购买记录数据集

![](https://s2.loli.net/2025/06/16/WHsp3RdyAFfSbOD.webp)

**pd.read_csv**

方法的具体作用是将CSV文件中的数据读取到内存中，并将其转换为一个Pandas的DataFrame对象，以便进行数据分析和处理。

1. 读取CSV文件：pd.read_csv()可以读取本地文件系统中的CSV文件，也可以读取远程服务器上的CSV文件，只需提供文件的路径或URL即可。
2. 处理不同的分隔符：除了默认的逗号分隔符，pd.read_csv()还支持处理其他分隔符，例如制表符、空格等。
3. 处理缺失值：pd.read_csv()可以自动处理CSV文件中的缺失值，将其转换为Pandas中的NaN（Not a Number）表示。
4. 自动推断数据类型：pd.read_csv()会自动推断每列数据的类型，并将其存储为相应的Pandas数据类型，例如整数、浮点数、字符串等。
5. 自定义参数设置：pd.read_csv()提供了许多参数，可以根据需要进行自定义设置，例如指定列名、解析日期、跳过行、选择特定列等。

**使用示例**

```python
import pandas as pd

# 从本地文件读取CSV数据
data = pd.read_csv('data.csv')

# 从远程服务器读取CSV数据
data = pd.read_csv('https://example.com/data.csv')

# 使用自定义参数设置
data = pd.read_csv('data.csv', delimiter='\t', skiprows=2, names=['col1', 'col2'])
```

3.对用户数据进行预处理

**使用独热编码处理分类特征**

```python
import pandas as pd
from sklearn.preprocessing import OneHotEncoder, MinMaxScaler
from sklearn.metrics.pairwise import cosine_similarity
```

```python
OneHotEncoder(sparse=False)
# 使用OneHotEncoder对分类特征进行独热编码。
encoder.fit_transform(users_df[['gender', 'city']])
# 选择了gender和city作为分类特征，并使用encoder.fit_transform方法将其转换为独热编码后的特征。
pd.DataFrame(encoded_users, columns=encoder.get_feature_names_out(['gender', 'city']))
# 使用pd.DataFrame创建了一个新的DataFrame对象encoded_users_df，列名为独热编码后的特征的名称。
```

**encoder**：创建一个独热编码器实例。

**encoded_users**：将原始用户数据的性别和城市特征进行独热编码处理。

![img](https://s2.loli.net/2025/06/16/e5lR1Uz6qhmKSZx.webp)

**encoded_users_df**：将独热编码后的数据转换为DataFrame格式，并设置列名

![img](https://s2.loli.net/2025/06/16/FVdqpyBTLGDS5n3.webp)

**独热编码[One-Hot Encoding]**

> One-Hot Encoding是一种常用的特征编码方法，用于将分类变量转换为数值变量。在机器学习和数据分析中，我们通常需要将非数值类型的特征转换为数值类型，以便算法能够处理。
>
> 举个例子，假设我们有一个分类变量"颜色"，可能的取值为["红色", "蓝色", "绿色"]。使用独热编码，我们可以将这个变量转换为三个二进制向量：["1, 0, 0"]表示红色，["0, 1, 0"]表示蓝色，["0, 0, 1"]表示绿色。

**使用独热编码处理分类特征**

```python
encoder = OneHotEncoder(sparse=False)
encoded_users = encoder.fit_transform(users_df[['gender', 'city']])
encoded_users_df = pd.DataFrame(encoded_users, columns=encoder.get_feature_names_out(['gender', 'city']))
OneHotEncoder(sparse=False)
# 使用OneHotEncoder对分类特征进行独热编码。
encoder.fit_transform(users_df[['gender', 'city']])
# 选择了gender和city作为分类特征，并使用encoder.fit_transform方法将其转换为独热编码后的特征。
pd.DataFrame(encoded_users, columns=encoder.get_feature_names_out(['gender', 'city']))
# 使用pd.DataFrame创建了一个新的DataFrame对象encoded_users_df，列名为独热编码后的特征的名称。
```

**encoder**：创建一个独热编码器实例。

**encoded_users**：将原始用户数据的性别和城市特征进行独热编码处理。

![img](https://s2.loli.net/2025/06/16/e5lR1Uz6qhmKSZx.webp)

**encoded_users_df**：将独热编码后的数据转换为DataFrame格式，并设置列名

![img](https://s2.loli.net/2025/06/16/FVdqpyBTLGDS5n3.webp)

**独热编码[One-Hot Encoding]**

One-Hot Encoding是一种常用的特征编码方法，用于将分类变量转换为数值变量。在机器学习和数据分析中，我们通常需要将非数值类型的特征转换为数值类型，以便算法能够处理。

举个例子，假设我们有一个分类变量"颜色"，可能的取值为["红色", "蓝色", "绿色"]。使用独热编码，我们可以将这个变量转换为三个二进制向量：["1, 0, 0"]表示红色，["0, 1, 0"]表示蓝色，["0, 0, 1"]表示绿色。

**归一化处理年龄特征**

```python
scaler = MinMaxScaler()
scaled_age = scaler.fit_transform(users_df[['age']])
encoded_users_df['scaled_age'] = scaled_age
```

```python
MinMaxScaler()
# 使用MinMaxScaler对年龄特征进行归一化处理。
scaler.fit_transform(users_df[['age']])
# 选择了age作为年龄特征，并使用scaler.fit_transform方法将其归一化。
encoded_users_df['scaled_age'] = scaled_age
# 归一化后的年龄特征存储在scaled_age中，并将其作为新的列添加到encoded_users_df中。
```

**scaler**：创建一个最小最大归一化处理实例。

**scaled_age**：将原始用户数据的年龄特征进行归一化处理。

![img](https://s2.loli.net/2025/06/16/pJKsz1AOMuekvl7.webp)

**encoded_users_df:**

![img](https://s2.loli.net/2025/06/16/IVmr9MuUoOEeQgz.webp)

4.计算用户之间的相似度矩阵

```python
similarity_matrix = cosine_similarity(encoded_users_df)
```

使用cosine_similarity计算用户之间的相似度矩阵。将encoded_users_df作为输入，该方法将计算每对用户之间的余弦相似度，并返回一个相似度矩阵。相似度矩阵存储在similarity_matrix中。

**similarity_matrix**

![img](https://s2.loli.net/2025/06/16/2XTsPO6p3aSfREe.webp)

5.获取与目标用户最相似的用户

```python
user_id = 1
similar_users = similarity_matrix[user_id-1]
most_similar_user_id = similar_users.argsort()[-2] + 1
```

```python
user_id = 1
# 1 为目标用户ID
similarity_matrix[user_id-1]
# 使用similarity_matrix[user_id-1]获取用户1与其他用户之间的相似度向量
most_similar_user_id = similar_users.argsort()[-2] + 1
# 使用argsort方法对相似度向量进行排序，返回排序后的索引数组。由于索引从0开始，所以需要将最相似的用户索引加1，得到最相似用户的ID。这里选择了倒数第二个最相似的用户，因为最相似的用户是用户本身。
```

**similar_users**

![img](https://s2.loli.net/2025/06/16/jwI7XDna48kfLWY.webp)

**most_similar_user_id**

![img](https://s2.loli.net/2025/06/16/aP34CXir7Uc8tAm.webp)

6.获取目标用户还没有购买过的商品

```python
user1_purchased_products = purchases_df[purchases_df['user_id'] == user_id]['product_name'].tolist()
similar_user_purchased_products = purchases_df[purchases_df['user_id'] == most_similar_user_id]['product_name'].tolist()
recommended_products = list(set(similar_user_purchased_products) - set(user1_purchased_products))
```

```python
purchases_df[purchases_df['user_id'] == user_id]['product_name'].tolist()
# 获取用户1已购买的商品列表
purchases_df[purchases_df['user_id'] == most_similar_user_id]['product_name'].tolist()
# 获取最相似用户已购买的商品列表
list(set(similar_user_purchased_products) - set(user1_purchased_products))
# 使用集合操作符-计算差集，得到推荐给用户1的商品列表，存储在recommended_products中
```

**user1_purchased_products**: 目标用户购买的商品列表

![img](https://s2.loli.net/2025/06/16/YS7WAxdI8UywZ1q.webp)

**similar_user_purchased_products**: 相似用户购买的商品列表

![img](https://s2.loli.net/2025/06/16/JzgQEHi6f3tT5vb.webp)

**recommended_products**: 推荐给目标用户的商品列表

![img](https://s2.loli.net/2025/06/16/5AWIZrVukjmRye6.webp)

7.打印推荐商品列表

```python
print(f"推荐给用户1的商品：{recommended_products}")
```

打印出推荐的商品

![img](https://s2.loli.net/2025/06/16/TOFpblMa9XVGDqR.webp)
