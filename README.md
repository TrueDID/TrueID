# TrueID MVP 实施方案

## 1. 项目背景
随着去中心化金融（DeFi）生态系统的发展，越来越多的人希望在无需传统金融机构中介的情况下，进行贷款和其他金融活动。然而，现有的DeFi贷款模式由于缺乏有效的信用评估机制，通常要求用户提供超额抵押品。这种过度抵押要求虽然降低了贷款风险，但也限制了许多潜在用户的参与，尤其是那些没有足够抵押资产的人。

为了降低对过度抵押的依赖，提升DeFi贷款的灵活性和便捷性，TrueID MVP引入了基于去中心化身份（DID）的链上声誉系统，并结合了Chainlink预言机技术。通过这种方式，用户的信用评分可以基于其在区块链上的行为和历史数据来计算，从而为信用良好的用户提供更加优惠的贷款条件，如较低的抵押要求或更低的利率。这种新模式不仅能吸引更多用户参与DeFi，还能促进金融包容性的发展。

## 2. 产品目标
- 构建一个高效、安全的链上声誉系统。
- 提高区块链身份验证的易用性和可访问性。
- 保护用户隐私，同时提供透明的声誉评分机制。

## 3. 用户故事
- **作为一个用户**，我希望能够轻松创建和管理我的数字身份。
- **作为一个借贷者**，我希望我的还款记录能够提高我的信用评分。
- **作为一个投资者**，我希望能够查看借款人的声誉评分，以做出更好的投资决策。

## 4. 实施详细步骤和流程

### 4.1 建立DID
1. **用户使用DID标准创建其数字身份**
    - **工具选择**：选择一个开源DID实现，如ION或Universal Resolver。
    - **生成DID**：用户通过前端界面输入必要信息，点击生成DID按钮。
    - **签名与存储**：用户使用其数字钱包对DID文档进行签名，并将签名后的DID文档存储在区块链上或GitHub等公共存储平台。

2. **将DID链接到钱包地址**
    - **钱包验证**：用户通过钱包插件（如Metamask）进行身份验证。
    - **关联过程**：系统将用户的DID与其钱包地址进行关联，并在区块链上记录此关联关系。

### 4.2 数据聚合
3. **从多个DeFi平台收集数据**
    - **API集成**：开发与各个DeFi平台的数据API集成，收集用户的交易历史、还款记录等数据。
    - **数据格式化**：将收集到的数据进行格式化处理，统一数据格式以便后续使用。

4. **通过Chainlink预言机传输数据**
    - **预言机设置**：配置Chainlink预言机节点，确保其能够从外部数据源安全地获取数据。
    - **数据上链**：预言机将格式化后的数据传输到区块链，确保数据的透明性和不可篡改性。

### 4.3 信用评分计算
5. **链外计算**
    - **信用评分合约部署**：在安全飞地（如Intel SGX）中部署信用评分计算逻辑，确保数据在计算过程中不被泄露。
    - **评分模型应用**：应用多变量评分模型，根据用户的交易历史、还款行为等因素计算信用评分。

6. **上传计算证明**
    - **生成证明**：生成信用评分的计算证明（如零知识证明）。
    - **上链存储**：将信用评分和计算证明上传到区块链，以确保评分过程的透明和可信。

### 4.4 贷款申请与批准
7. **用户申请贷款**
    - **提交申请**：用户通过前端界面填写贷款申请表，包括贷款金额、期限等信息。
    - **智能合约交互**：系统通过智能合约提交贷款申请，并调用评分验证合约获取用户的信用评分。

8. **评估贷款条件**
    - **评分验证**：智能合约验证用户的信用评分，并根据评分结果确定贷款条件。
    - **条件反馈**：系统将评估结果反馈给用户，包括贷款金额、利率、抵押要求等。

9. **贷款发放**
    - **智能合约执行**：智能合约根据评估结果执行贷款发放，将贷款金额转账至用户钱包。
    - **记录更新**：更新链上记录，反映贷款发放和用户的债务状况。

## 5. 分工安排

### 项目经理（PM）
- 制定项目计划和时间表
- 分配任务和协调各团队
- 监督项目进度

### 前端开发团队（2人）
- **任务**：设计并实现身份验证、铭文上传和查询记录的用户界面
- **时间**：2天

### 后端开发团队（2人）
- **任务**：实现数据聚合模块，包括数据源集成和数据存储
- **时间**：2天

### 区块链开发团队（2人）
- **任务**：开发身份验证模块（DID生成与管理）、实现评分算法和智能合约（铭文存储、记录查询）
- **时间**：3天

### 测试工程师（1人）
- **任务**：进行单元测试和集成测试，确保系统各模块协同工作
- **时间**：2天

### 时间安排（7天）
| 任务 | 负责人 | 时间框架 |
|---|---|---|
| 制定项目计划和时间表 | 项目经理 | 第1天 |
| 前端界面设计与开发 | 前端开发团队 | 第1-2天 |
| 数据源集成和数据存储 | 后端开发团队 | 第1-2天 |
| DID生成与管理开发 | 区块链开发团队 | 第1-2天 |
| 实现评分算法和智能合约 | 区块链开发团队 | 第3-5天 |
| 系统整合与调试 | 全体开发团队 | 第5天 |
| 单元测试和集成测试 | 测试工程师 | 第6天 |
| 项目验收与展示 | 全体团队 | 第7天 |

### 备注
- **沟通与协调**：各团队应保持密切沟通，定期进行项目状态更新会议，及时解决开发过程中遇到的问题。
- **文档记录**：各团队应详细记录开发过程中的技术文档，以便后续维护和优化。
