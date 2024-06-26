+++
title = '实验2：体验GitHub Copilot高级功能'
date = 2024-06-26T02:49:40+08:00
+++

## 实验2：体验GitHub Copilot高级功能

### 体验GitHub Copilot on Github.com

**目标**：
体验GitHub Copilot在GitHub网站上的高级功能。

#### 1. **PR摘要生成**：
示例1：在PR页面中，自动生成PR摘要，包含变更的描述和受影响的文件列表。

**步骤**：
   - 在GitHub PR（Pull Request）页面上，创建PR
   ![Github Copilot Enterprise 1](/github-copilot-best-practice-labs/github_dot_com_4.png)
   - 使用Copilot生成Pull Request摘要
   ![Github Copilot Enterprise 2](/github-copilot-best-practice-labs/github_dot_com_5.png)
   - 查看生成的摘要信息
   ![Github Copilot Enterprise 3](/github-copilot-best-practice-labs/github_dot_com_6.png)

#### 2. **对代码库进行索引作为上下文**：
示例1：对选中的代码库进行索引，获得有针对性的准确答案。

**步骤**：
   - 在GitHub Copilot Chat界面上，点击按钮对Repo进行索引
   ![Github Copilot Enterprise 4](/github-copilot-best-practice-labs/github_dot_com_2.png)

   - 提问相关问题时自动查询相关问题
   ![Github Copilot Enterprise 5](/github-copilot-best-practice-labs/github_dot_com_3.png)


#### 3. 创建和使用知识库

**目标**：
创建知识库，以便在Copilot中使用。

示例1：创建知识库。

**步骤**：
   - 准备好Markdown格式的文档，并上传到用于构建知识库的Repo中
   - 在GitHub上创建一个知识库，存储项目的文档和代码示例。
   ![Github Copilot Knowledge Base 1](/github-copilot-best-practice-labs/create_knowledge_base_1.png)

示例2：基于知识库的问答

**步骤**：
   - 在Copilot中使用知识库进行问答，获取更相关的回答。
   ![Github Copilot Knowledge Base 2](/github-copilot-best-practice-labs/create_knowledge_base_2.png)