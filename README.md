# ChatOps - AI DevOps 自动化平台

🚀 一个基于AI的DevOps自动化平台，帮助您快速部署和管理基于Kubernetes的云原生应用。

## ✨ 特性

- 🤖 **AI驱动部署**: AI自动配置和部署整套系统
- ☁️ **Google Cloud原生**: 基于GKE、Cloud SQL、MemoryStore等GCP服务
- 🔄 **GitOps工作流**: 使用ArgoCD实现声明式部署
- 📱 **全栈架构**: Next.js前端 + Go微服务后端
- 🔐 **安全优先**: 完整的IAM、TLS证书、密钥管理
- 📊 **可观测性**: 集成监控、日志、指标收集

## 🏗️ 架构概览

```
Public IP → K8s Nginx Ingress → K8s Workloads → Cloud NAT → Public IP
                   ↓
        [Frontend] [Backend] [ArgoCD] [Consul]
                   ↓
           [Cloud SQL] [MemoryStore Redis]
```

## 🚀 快速开始

### 前置要求

- Google Cloud账户并启用必要API
- GitHub账户和仓库访问权限
- 自有域名（用于配置SSL证书）

### 一键部署

1. **Fork或克隆此仓库**
```bash
git clone https://github.com/ichatops/chatops.git
cd chatops
```

2. **与AI助手对话**
   - 告诉AI您的需求和环境信息
   - AI将自动为您配置所有组件
   - 提供必要的域名、GitHub token等信息

3. **等待部署完成**
   - AI将自动创建GCP资源
   - 配置Kubernetes集群
   - 部署应用和基础设施

## 📋 系统组件

### 应用服务
- **Frontend**: Next.js响应式Web应用 (端口3000)
- **Backend**: Go Hertz微服务框架 (端口8000)

### 基础设施
- **ArgoCD**: GitOps持续部署平台
- **Consul**: 服务发现和配置中心
- **Nginx Ingress**: 负载均衡和TLS终止
- **Cert-Manager**: 自动SSL证书管理

### 存储与缓存
- **Cloud SQL**: PostgreSQL托管数据库
- **MemoryStore**: Redis缓存服务

## 🔧 配置说明

所有配置文件使用占位符模式，AI将在部署时自动替换：

- `REPLACE_ME_DOMAIN` - 您的域名
- `REPLACE_ME_GITHUB_ORG` - GitHub组织名
- `REPLACE_ME_IMAGE_REGISTRY` - 容器镜像仓库
- 等等...

## 📁 项目结构

```
├── backend/          # Go后端服务代码
├── frontend/         # Next.js前端代码  
├── gitops/           # Kubernetes部署配置
├── scripts/          # 部署和管理脚本
└── development/      # 开发文档和指南
```

## 🛡️ 安全特性

- 🔐 TLS/SSL自动证书
- 🔑 IAM最小权限原则
- 🛡️ 网络安全组策略
- 🔒 密钥和配置加密存储

## 📚 了解更多

- [开发指南](./development/AI_DEPLOYMENT_GUIDE.md)
- [GitOps配置详解](./gitops/README.md)
- [API文档](./backend/README.md)

## 🤝 贡献

欢迎提交Issue和Pull Request来改进项目！

## 📄 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

---

⚡ **现在就开始与AI助手对话，一键部署您的云原生应用！**
