<div align="center">

<img src="./static/image/MiroFish_logo_compressed.jpeg" alt="MiroFish Logo" width="75%"/>

<a href="https://trendshift.io/repositories/16144" target="_blank"><img src="https://trendshift.io/api/badge/repositories/16144" alt="MiroFish | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>

简洁通用的群体智能引擎，预测万物
</br>
<em>A Simple and Universal Swarm Intelligence Engine, Predicting Anything</em>

[English](./README.md) | [中文文档](./README-ZH.md)

</div>

## 项目概述

MiroFish 是一套基于多智能体与图谱推理的预测引擎。它会把现实世界中的种子材料转成图谱、人格和行为环境，再通过模拟、检索和报告生成，推演未来可能发生的结果。

当前版本支持：
- 图谱构建与实体关系抽取
- 多智能体社交模拟
- 报告生成与深度检索
- 足球比分概率模拟与分布输出
- Neo4j 本地图谱后端

## 核心能力

- 现实种子提取与图谱化
- Agent 人设生成与行为注入
- Twitter / Reddit 双平台模拟
- 报告 Agent 深度检索与章节生成
- 结构化比分预测、胜平负概率、比分矩阵

## 目录结构

```text
backend/   后端 Flask 服务
frontend/  前端 Vite + Vue
locales/   多语言文案
static/    图片与静态资源
```

## 快速开始

### 1. 环境要求

- Node.js 18+
- Python 3.11 - 3.12
- uv
- Neo4j 5.x（本地模式）

### 2. 配置环境变量

复制示例文件并填写真实值：

```bash
cp .env.example .env
```

常用配置：

```env
LLM_API_KEY=your_api_key
LLM_BASE_URL=https://dashscope.aliyuncs.com/compatible-mode/v1
LLM_MODEL_NAME=qwen-plus

GRAPH_BACKEND=neo4j
NEO4J_URI=bolt://localhost:7687
NEO4J_USERNAME=neo4j
NEO4J_PASSWORD=password
NEO4J_DATABASE=neo4j
```

### 3. 安装依赖

```bash
npm run setup:all
```

### 4. 启动服务

```bash
npm run dev
```

服务地址：
- 前端：`http://localhost:3000`
- 后端：`http://localhost:5001`

## Neo4j 启动

如果你使用本地图谱后端，可以先启动 Neo4j：

```bash
docker compose -f docker-compose.neo4j.yml up -d
```

默认连接：
- Bolt: `bolt://localhost:7687`
- Browser: `http://localhost:7474`

## 报告与模拟

报告生成过程会：
- 先规划大纲
- 再逐章调用检索工具
- 最后输出完整 Markdown 报告

如果当前模拟场景是足球比赛，系统会自动生成：
- 主胜 / 平局 / 客胜概率
- 最可能比分 Top Scorelines
- 期望进球
- 比分分布矩阵

## 日志位置

- 后端服务日志：`log/backend-restart.out.log`
- 后端错误日志：`log/backend-restart.err.log`
- 前端日志：`log/frontend-direct.out.log`
- 报告日志：`backend/uploads/reports/<report_id>/`

## 常见问题

### 1. 429 限流

LLM 接口如果返回 429，系统会自动等待后重试，不会直接中断任务。

### 2. 检索结果为空

当前项目已切换到 Neo4j 关键词检索与文本化输出。如果仍为空，通常是图谱里还没有足够的实体或关系数据。

### 3. 报告缺少比分预测

足球场景会自动注入结构化概率模块。若仍未出现，请检查模拟需求中是否包含足球/比分/泊松等关键词，以及模拟配置是否正确生成了 `lambda_home` / `lambda_away`。

## 许可证

AGPL-3.0
