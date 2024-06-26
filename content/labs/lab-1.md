+++
title = '实验1：体验GitHub Copilot基本功能'
date = 2024-06-26T02:49:40+08:00
+++

## 实验1：体验GitHub Copilot基本功能

### 代码补全

**目标**：
体验GitHub Copilot的代码补全功能，理解其基本操作。

#### 1.**Ghost Text**
在VS Code中开始输入一段代码，观察Copilot提供的自动补全建议。

示例1：在Python文件中输入 `def calculate_sum(`，Copilot会自动补全函数的参数和实现。

**步骤**：
   - 在Python文件中输入 `def calculate_sum(`，Copilot会自动补全函数的参数和实现。
   ![Ghost Text 1](/github-copilot-best-practice-labs/ghost_text_1.png)

示例2：在Python文件中输入 `def calculate_sum(`，在多个建议之间切换，选择接受或部分接受。

**步骤**：
   - 在Python文件中输入 `def calculate_sum(`，在多个建议之间切换，选择接受或部分接受。
   ![Ghost Text 2](/github-copilot-best-practice-labs/ghost_text_2.png)

示例3：在Python文件中输入 `def calculate_sum(`，打开建议面板，查看所有可能的建议，选择更符合你要求的建议。

**步骤**：
   - 在Python文件中输入 `def calculate_sum(`，打开建议面板，查看所有可能的建议，选择更符合你要求的建议。
   ![Ghost Text 3](/github-copilot-best-practice-labs/ghost_text_3.png)

#### 2.**Comment to Code**：
使用注释提示代码生成。

示例1：在Python文件中开头的注释中输入 `# 计算两个数的和`，然后按 `Tab` 键，让Copilot生成相应的函数代码。

**步骤**：
   - 在Python文件中开头的注释中输入 `# 计算两个数的和`，然后按 `Tab` 键，让Copilot生成相应的函数代码。
   ![Comments to Code 1](/github-copilot-best-practice-labs/comments_to_code_1.png)

示例2：在函数内部加入注释 `# 分别打印两个数字`，然后按 `Tab` 键，让Copilot生成相应的函数代码。

**步骤**：
   - 在Python文件中输入 `def calculate_sum(`，在多个建议之间切换，选择接受或部分接受。
   ![Comments to Code 2](/github-copilot-best-practice-labs/comments_to_code_2.png)

示例3：使用更复杂的提示语来生成代码，打开建议面板，查看所有可能的建议，选择更符合你要求的建议。

**步骤**：
   - 在Python文件中加入以下注释，创建一个方法，列出所有EC2实例
      ```python
      # 按照以下步骤，将注释转换为代码
      # 1. 定义一个函数，名为list_running_ec2_instances，接受一个参数，名为ec2_client
      # 2. 在函数内部，调用ec2_client的describe_instances方法，将结果赋值给变量response
      # 3. 从response中提取出所有的实例，将其赋值给变量instances
      # 4. 返回instances
      ```

   - 在Python文件中加入以下注释，创建一个方法，列出所有EC2预留实例
      ```python
      # 按照以下步骤，将注释转换为代码
      # 1. 定义一个函数，名为list_reserved_ec2_instances，接受一个参数，名为ec2_client
      # 2. 在函数内部，调用ec2_client的describe_reserved_instances方法，将结果赋值给变量response
      # 3. 从response中提取出所有的实例，将其赋值给变量reserved_instances
      # 4. 返回instances
      ```

      ![Comments to Code 3](/github-copilot-best-practice-labs/comments_to_code_3.png)


### 聊天交互

**目标**：
体验GitHub Copilot的聊天交互功能，理解其在不同场景下的应用。


#### 1. **内联聊天交互**
示例1：在代码编辑过程中，使用内联聊天功能与Copilot互动。

**步骤**：
   - 按`command + I`打开内联聊天窗口，输入 `给定一个list，其中的对象为结构相同的dict，如何根据dict中特定的key，对list进行排序`，查看Copilot的回答。
   
      ![Inline Chat 1](/github-copilot-best-practice-labs/inline_chat_1.png)

示例2：在代码编辑过程中，使用内联聊天窗口触发快捷操作。

**步骤**：
   - 选中 `list_running_ec2_instances` 方法的全部代码。
   - 按`command + I`打开内联聊天窗口，输入 `/doc`，为方法添加文档。

      ![Inline Chat 2](/github-copilot-best-practice-labs/inline_chat_2.png)

示例2：在代码编辑过程中，使用内联聊天窗口触编写新的代码。

**步骤**：
   - 光标移动到函数内部
   - 按`command + I`打开内联聊天窗口，输入 `确认response中的结果是否被分页，如果还有下一页，继续请求，直到获得所有信息为止`，生成新的代码。

      ![Inline Chat 3](/github-copilot-best-practice-labs/inline_chat_3.png)

   >- 注意：目前在Inline Chat中无法使用`@`和`#`

#### 2. **快速聊天窗口**
示例1：使用快速聊天窗口进行简短的询问。

**步骤**：
   - 激活快速聊天窗口
      - 按 `F1` 或 `command + shift + P` 打开命令面板，运行 `Chat: Open Quick Chat`，打开快捷聊天窗口
      - 直接 `command + shift + I` 打开快捷聊天窗口。
   - 在聊天界面中询问 `如何在Python中实现快速排序？` ，并查看详细的回答和代码示例。
      
      ![Quick Chat 1](/github-copilot-best-practice-labs/quick_chat_1.png)

示例2：在快速聊天窗口中使用Chat Participants和Chat Variables。

**步骤**：
   - 激活快速聊天窗口
      - 按 `F1` 或 `command + shift + P` 打开命令面板，运行 `Chat: Open Quick Chat`，打开快捷聊天窗口
      - 直接 `command + shift + I` 打开快捷聊天窗口。
   - 在聊天界面中询问 `@workspace #selection 解释选中的代码` ，并查看详细的回答
      
      ![Quick Chat 2](/github-copilot-best-practice-labs/quick_chat_2.png)
   >- 注意：目前在Quick Chat中无法使用#file来选择具体的文件


#### 3. **聊天界面**
示例1：使用完整的聊天界面进行复杂的交互。

**步骤**：
   - 打开聊天窗口 
   ![Chat View New Project 0](/github-copilot-best-practice-labs/chat_view_1.png)
   - 在聊天界面中输入 `@workspace #editor 告诉我当前编辑的文件的git repo地址`，并查看详细的回答和代码示例。
   ![Chat View QA 1](/github-copilot-best-practice-labs/chat_view_qa_1.png)
   - 在聊天界面中输入 `@terminal 以树状图的方式列出项目结构`，并查看详细的回答和代码示例。
   ![Chat View QA 2](/github-copilot-best-practice-labs/chat_view_qa_2.png)
   - 在聊天界面中继续追问命令的详细使用方式，并查看详细的回答和代码示例。
   ![Chat View QA 3](/github-copilot-best-practice-labs/chat_view_qa_3.png)


### 智能操作

**目标**：
了解并使用GitHub Copilot的智能操作功能。

#### 1. **Slash Commands**：

示例1：在聊天界面中输入 `/new` 创建一个新的工作区。

**步骤**：
   - 打开聊天窗口 
   ![Chat View New Project 0](/github-copilot-best-practice-labs/chat_view_1.png)
   - 在聊天界面中输入 `@workspace /new 根据最佳实践，创建规范的FastAPI项目`，并查看详细的回答和代码示例。
   ![Chat View New Project 1](/github-copilot-best-practice-labs/chat_view_new_project_1.png)
   - 点击 `create workspace` 创建一个新的工作空间
   ![Chat View New Project 2](/github-copilot-best-practice-labs/chat_view_new_project_2.png)
   - 打开工作空间，查看详细项目结构
   ![Chat View New Project 3](/github-copilot-best-practice-labs/chat_view_new_project_3.png)

#### 2. **Chat Participant**：

示例1：使用聊天参与者获取特定领域的帮助。

**步骤**：
   - 打开聊天窗口 
   ![Chat View New Project 0](/github-copilot-best-practice-labs/chat_view_1.png)
   - 在聊天界面中输入 `@workspace 如果我想增加一个API接口，应该修改哪个文件`，并查看详细的回答和代码示例。
   ![Chat View QA 4](/github-copilot-best-practice-labs/chat_view_qa_4.png)

#### 3. **Chat Variables**：

示例1：在聊天中使用 `#file` 引用具体的文件作为上下文，生成代码到新的文件。

**步骤**：
   - 在聊天界面中输入 `@workspace #file:example_model.py 根据示例，生成EC2 Instance类的模型`，并查看详细的回答和代码示例，点击更多选项，选择插入到新文件。
   ![Chat New File 1](/github-copilot-best-practice-labs/chat_view_create_new_file_1.png)
   
#### 4. **组合使用**：

示例1：结合使用多种智能操作提高效率。
**步骤**：
   - 在聊天界面中输入 `@workspace #file:ec2_instance_model.py fix the findings`，并查看详细的回答和代码示例，点击复制，覆盖原有内容。
   ![Chat Workspace Fix 1](/github-copilot-best-practice-labs/chat_view_workspace_file_fix.png)



#### 5. **生成Commit Message**：

示例1：在完成一段代码修改后，让Copilot生成一个描述性强的提交信息。
**步骤**：
   - 选中需要提交的变更，点击闪光标记，生成提交信息。
   ![Chat Generate Commit Messages](/github-copilot-best-practice-labs/chat_view_generate_commit_message.png)
