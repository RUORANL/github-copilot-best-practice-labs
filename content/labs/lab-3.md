+++
title = '实验3：理解GitHub Copilot的上下文机制'
date = 2024-06-26T02:49:40+08:00
+++

## 实验3：理解GitHub Copilot的上下文机制



**目标**：
理解如何Github Copilot上下文的获取方式，提高Copilot的建议准确性。

### 以不同的方式提供上下文

示例1：提供Top-level注释后自动生成代码
**步骤**：
   - 在文件开头加入如下注释
      ```python
      # 我们正在处理一个包含缺失值和重复记录的客户数据集，数据集包括客户的姓名、邮箱、电话和购买记录。
      # 我们的目标是清理数据集，以便我们可以更好地分析客户的购买行为。
      # 请注意，我们的数据集中有一些重复的记录，这些记录是由于数据输入错误而导致的。
      # 我们还有一些缺失值，这些缺失值可能是由于客户没有提供信息或数据输入错误导致的。
      # 我们将使用Python的pandas库来清理数据集。
      # 数据文件: 'data.csv'
      ```
   - 按Tab选择代码补全，直到实现所有要求的功能
   - 生成代码如下
      ```python
      import pandas as pd

      # Load the dataset into DataFrame 'df'
      df = pd.read_csv('data.csv')

      # 1. 删除重复记录
      df.drop_duplicates(inplace=True)

      # 2. 处理缺失值：删除含有任何缺失值的行

      df.dropna(inplace=True)

      # 3. 规范化邮箱地址为小写

      df['Email'] = df['Email'].str.lower()

      # 4. 规范化电话号码格式

      # 移除非数字字符，然后按照美国标准格式重新格式化电话号码
      df['Phone'] = df['Phone'].str.replace(r'\D', '', regex=True)

      df['Phone'] = df['Phone'].str.replace(r'(\d{3})(\d{3})(\d{4})', r'\1-\2-\3', regex=True)

      # 保存清理后的数据到新文件（或覆盖原文件）

      df.to_csv('cleaned_customer_data.csv', index=False)

      ```
   - 运行结果：获取到data.csv的正确路径，程序可以正常运行


示例2：提供不同的示例代码，查看生成代码的效果

**步骤**：
   - 在聊天窗口输入以下提示词
      ```markdown
      参考#file:sample_code_1.py 生成用于查询RDS DB Instance的代码
      ```
   - `sample_code_1.py` 的代码为
      ```python
      import boto3
      from typing import List, Dict

      def describe_rds_instances(client: boto3.client) -> List[Dict]:
         """
         Retrieves information about RDS instances using the provided AWS client.

         Parameters:
         - client: The AWS client object used to interact with the RDS service.

         Returns:
         - instances: A list of dictionaries containing information about the RDS instances.

         """
         instances = list()  # List to store the RDS instances
         response = client.describe_db_instances()  # Retrieve the initial response
         instances.extend(response['DBInstances'])  # Add instances from the initial response
         while 'Marker' in response:
            response = client.describe_db_instances(Marker=response['Marker'])  # Retrieve the next page of results
            instances.extend(response['DBInstances'])  # Add instances from the current response
         return instances
      ```
   - 生成代码如下
      ```python
      import boto3
      from typing import List, Dict

      def describe_rds_instances(client: boto3.client) -> List[Dict]:
         """
         Retrieves information about RDS instances using the provided AWS client.

         Parameters:
         - client: The AWS client object used to interact with the RDS service.

         Returns:
         - instances: A list of dictionaries containing information about the RDS instances.

         """
         instances = list()  # List to store the RDS instances
         response = client.describe_db_instances()  # Retrieve the initial response
         instances.extend(response['DBInstances'])  # Add instances from the initial response
         while 'Marker' in response:
            response = client.describe_db_instances(Marker=response['Marker'])  # Retrieve the next page of results
            instances.extend(response['DBInstances'])  # Add instances from the current response
         return instances
      ```
   - 在聊天窗口输入以下提示词
      ```markdown
      参考#file:sample_code_2.py 生成用于查询RDS DB Instance的代码
      ```
   - `sample_code_2.py` 的代码为
      ```python
      import boto3

      def describe_ec2_instances(client):
         instances = list()
         response = client.describe_instances()
         for reservation in response['Reservations']:
            instances.extend(reservation['Instances'])
         while 'NextToken' in response:
            response = client.describe_instances(NextToken=response['NextToken'])
            for reservation in response['Reservations']:
                  instances.extend(reservation['Instances'])
         return instances
      ```
   - 生成代码如下
      ```python
      import boto3

      def describe_rds_instances(client):
         instances = list()
         response = client.describe_db_instances()
         for instance in response['DBInstances']:
            instances.append(instance)
         while 'Marker' in response:
            response = client.describe_db_instances(Marker=response['Marker'])
            for instance in response['DBInstances']:
                  instances.append(instance)
         return instances
      ```

示例3：在编辑器中打开文件作为上下文

**步骤**：
   - 在编辑器窗口打开promps.md和data.csv两个文件
   - 在聊天窗口输入以下提示语
      ```markdown
      Context:
      我们正在处理一个包含缺失值和重复记录的客户数据集，数据集包括客户的姓名、邮箱、电话和购买记录。

      Action:
      编写数据清洗脚本

      Purpose:
      目的是清理和规范化客户数据，以便后续的数据分析和模型训练。
      ```
   - 生成的代码
      ```python
      import pandas as pd

      # 假设数据集存储在名为 'data.csv' 的文件中
      # 列名假设为 'Name', 'Email', 'Phone', 'PurchaseHistory'

      # 加载数据集
      df = pd.read_csv('customer_data.csv')

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
   - 运行结果：未获取到data.csv的正确路径，程序无法正常运行


示例4：使用#file指定文件作为上下文

**步骤**：
   - 在编辑器窗口打开promps.md文件
   - 在聊天窗口输入以下提示语
      ```markdown
      Context: 我们正在处理一个包含缺失值和重复记录的客户数据集，数据集为#file:data.csv ，数据集包括客户的姓名、邮箱、电话和购买记录。

      Action: 编写数据清洗脚本

      Purpose: 目的是清理和规范化客户数据，以便后续的数据分析和模型训练。
      ```
   - 生成的代码
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
      # 将所有的邮箱地址转换为小写
      df['Email'] = df['Email'].str.lower()

      # 规范化电话号码格式（例如：统一使用"-"分隔区号和电话号码）
      # 这里只是一个简单的示例，实际情况可能需要复杂的处理
      df['Phone'] = df['Phone'].str.replace(r'\D', '', regex=True).str.replace(r'(\d{3})(\d{3})(\d{4})', r'\1-\2-\3', regex=True)

      # 保存清理后的数据到新文件
      df.to_csv('cleaned_data.csv', index=False)
      ```
   - 运行结果：获取到data.csv的正确路径，程序可以正常运行

示例5：使用#editor指定打开的文件作为上下文

**步骤**：
   - 在编辑器窗口打开promps.md文件和data.csv，data.csv为活动窗口
   - 在聊天窗口输入以下提示语
      ```markdown
      Context: 我们正在处理一个包含缺失值和重复记录的客户数据集，数据集为#editor ，数据集包括客户的姓名、邮箱、电话和购买记录。

      Action: 编写数据清洗脚本

      Purpose: 目的是清理和规范化客户数据，以便后续的数据分析和模型训练。
      ```
   - 生成的代码
      ```python
      import pandas as pd
      from io import StringIO

      # 模拟从文件读取的数据
      data = """Name,Email,Phone,Purchase
      Alice,alice@example.com,123-456-7890,200
      Bob,bob@EXAMPLE.com,234.567.8901,150
      Ivan,ivan@example.com,901-234-5678,500
      Charlie,charlie@example.com,345-678-9012,300
      ,456*789*0123,250
      Eve,eve@example.com,567-890-1234,400
      Frank,frank@EXAMPLE.com,678-901-2345,100
      Frank,frank@EXAMPLE.com,,100
      Grace,grace@EXAMPLE.com,789-012-3456,350
      Heidi,heidi@example.com,890-123-4567,450
      Ivan,ivan@example.com,901-234-5678,500
      Judy,judy@example.com,012-345-6789,600"""

      # 使用 StringIO 来模拟从文件读取
      df = pd.read_csv(StringIO(data))

      # 删除重复记录，保留第一次出现的记录
      df.drop_duplicates(inplace=True)

      # 处理缺失值：删除含有任何缺失值的行
      df.dropna(inplace=True)

      # 规范化邮箱地址为小写
      df['Email'] = df['Email'].str.lower()

      # 规范化电话号码格式
      df['Phone'] = df['Phone'].str.replace(r'\D', '', regex=True)  # 移除非数字字符
      df['Phone'] = df['Phone'].str.replace(r'(\d{3})(\d{3})(\d{4})', r'\1-\2-\3', regex=True)  # 重新格式化

      # 输出清理后的数据，实际应用中应保存到文件
      print(df)
      ```
   - 运行结果：未获取到data.csv的正确路径，获取到了data.csv内的内容，程序可以正常运行

示例6：使用@workspace提供上下文

**步骤**：
   - 在编辑器窗口打开promps.md文件和data.csv，data.csv为活动窗口
   - 在聊天窗口输入以下提示语
      ```markdown
      @workspace Context: 我们正在处理一个包含缺失值和重复记录的客户数据集，数据集包括客户的姓名、邮箱、电话和购买记录。

      Action: 编写数据清洗脚本

      Purpose: 目的是清理和规范化客户数据，以便后续的数据分析和模型训练。
      ```
   - 生成的代码
      ```python
      import pandas as pd

      # 假设数据集的路径和文件名已知
      data_path = 'path_to_your_dataset.csv'  # 请替换为实际的文件路径和名称

      # 加载数据集
      df = pd.read_csv(data_path)

      # 删除重复记录
      df.drop_duplicates(inplace=True)

      # 处理缺失值：删除含有任何缺失值的行
      df.dropna(inplace=True)

      # 规范化邮箱地址为小写
      df['Email'] = df['Email'].str.lower()

      # 规范化电话号码格式
      # 移除非数字字符，然后按照美国标准格式重新格式化电话号码
      df['Phone'] = df['Phone'].str.replace(r'\D', '', regex=True)
      df['Phone'] = df['Phone'].str.replace(r'(\d{3})(\d{3})(\d{4})', r'\1-\2-\3', regex=True)

      # 保存清理后的数据到新文件（或覆盖原文件）
      cleaned_data_path = 'cleaned_customer_data.csv'  # 清理后的数据集文件名
      df.to_csv(cleaned_data_path, index=False)

      # 输出操作完成的消息
      print(f"Data cleaning completed. Cleaned dataset saved to '{cleaned_data_path}'.")
      ```
   - 运行结果：未获取到data.csv的正确路径，程序无法正常运行

示例7：使用@workspace提供上下文

**步骤**：
   - 在编辑器窗口打开promps.md文件高亮选中文件中的data.csv字符
   - 在聊天窗口输入以下提示语
      ```markdown
      @workspace Context: 我们正在处理一个包含缺失值和重复记录的客户数据集，数据集包括客户的姓名、邮箱、电话和购买记录。

      Action: 编写数据清洗脚本

      Purpose: 目的是清理和规范化客户数据，以便后续的数据分析和模型训练。
      ```
   - 生成的代码
      ```python
      import pandas as pd

      # 加载数据集
      df = pd.read_csv('data.csv')

      # 删除重复记录
      df.drop_duplicates(inplace=True)

      # 处理缺失值：删除含有任何缺失值的行
      df.dropna(inplace=True)

      # 规范化邮箱地址为小写
      df['Email'] = df['Email'].str.lower()

      # 规范化电话号码格式
      # 移除非数字字符，然后按照标准格式重新格式化电话号码
      df['Phone'] = df['Phone'].str.replace(r'\D', '', regex=True)
      df['Phone'] = df['Phone'].str.replace(r'(\d{3})(\d{3})(\d{4})', r'\1-\2-\3', regex=True)

      # 保存清理后的数据到新文件
      df.to_csv('cleaned_data.csv', index=False)
      ```
   - 运行结果：获取到data.csv的正确路径，程序可以正常运行