+++
title = '实验4：探索GitHub Copilot的Prompt技巧'
date = 2024-06-26T02:49:40+08:00
+++

## 实验4：探索GitHub Copilot的Prompt技巧

### 原则

掌握编写有效Prompt的3S原则：Simple，Specific，Short。

### 框架

**常见提示语框架集合**
   ![Prompt Engineering Framework](/github-copilot-best-practice-labs/prompt_engineering_framework_1.png)
   
>- 注意：可以扫码访问出处，WayToAGI在线文档，总结了大量高质量的AGI相关的知识。

**目标**：
了解主流的提示语框架，测试并观察不同框架的效果。

示例1：使用CO-STAR框架编写结构化的Prompt。

**步骤**：
   - 按照CO-STAR框架编写Prompt，包括上下文、目标、风格、语气、受众和响应格式。
   - 示例：
     ```markdown
     Context: 我是一名开发人员，希望了解如何实现二分查找。
     Objective: 生成一个二分查找的Python代码示例。
     Style: 项目符号
     Tone: 正式
     Audience: 初级程序员
     Response: 在200字以内
     ```

示例2：测试使用至少两种不同框架编写的Prompt生成数据清洗代码，并对比效果
**步骤**：
   - A.P.E
      ![Framework 1](/github-copilot-best-practice-labs/prompt_engineering_framework_4.png)
   - 提示语示例：
      ```markdown
      Context:
      我们正在处理一个包含缺失值和重复记录的客户数据集，数据集包括客户的姓名、邮箱、电话和购买记录。

      Action:
      编写数据清洗脚本

      Purpose:
      目的是清理和规范化客户数据，以便后续的数据分析和模型训练。
      ```
   - 提示语效果：
      ```python
      import pandas as pd

      # 假设数据集存储在名为 'data.csv' 的文件中
      # 列名假设为 'Name', 'Email', 'Phone', 'PurchaseHistory'

      # 加载数据集
      df = pd.read_csv('data.csv')

      # 删除重复记录
      df.drop_duplicates(inplace=True)

      # 处理缺失值：可以选择填充缺失值或删除含有缺失值的行
      # 这里选择删除含有任何缺失值的行
      df.dropna(inplace=True)

      # 规范化数据
      # 假设我们要将所有的邮箱地址转换为小写
      df['Email'] = df['Email'].str.lower()

      # 假设我们要规范化电话号码格式（例如：统一使用"-"分隔区号和电话号码）
      # 这里只是一个简单的示例，实际情况可能需要复杂的处理
      df['Phone'] = df['Phone'].str.replace(r'\D', '', regex=True).str.replace(r'(\d{3})(\d{3})(\d{4})', r'\1-\2-\3', regex=True)

      # 保存清理后的数据到新文件
      df.to_csv('cleaned_data.csv', index=False)

      ```
   - I.C.I.O
      ![Framework 3](/github-copilot-best-practice-labs/prompt_engineering_framework_3.png)
   - 提示语示例：
      ```markdown
      Context:
      我是一名数据分析师，目前正在处理一个包含缺失值和重复记录的客户数据集。数据集包括客户的姓名、邮箱、电话和购买记录。

      Instruction:
      请编写Python代码，对客户数据集进行数据清洗，包括以下步骤：
      1. 删除包含缺失值的记录。
      2. 去除重复记录。
      3. 规范化邮箱字段（全部转换为小写）。
      4. 将电话字段中的特殊字符移除。

      Input Data:
      #file:data.csv 

      Output Indicator:
      生成一段Python代码，实现上述数据清洗步骤，并使用pandas库进行处理。
      ```
   - 提示语效果：
      ```python
      import pandas as pd

      # Load the dataset
      df = pd.read_csv('data.csv')

      # Step 1: Delete records with missing values
      df.dropna(inplace=True)

      # Step 2: Remove duplicate records
      df.drop_duplicates(inplace=True)

      # Step 3: Normalize the email field (convert all to lowercase)
      df['Email'] = df['Email'].str.lower()

      # Step 4: Remove special characters from the phone field
      df['Phone'] = df['Phone'].str.replace(r'\D', '', regex=True)

      # Save the cleaned dataset
      df.to_csv('cleaned_data.csv', index=False)
      ```
   - C.A.R.E
      ![Framework 2](/github-copilot-best-practice-labs/prompt_engineering_framework_2.png)
   - B.R.O.K.E
      ![Framework 5](/github-copilot-best-practice-labs/prompt_engineering_framework_5.png)
   - R.A.C.E
      ![Framework 6](/github-copilot-best-practice-labs/prompt_engineering_framework_6.png)