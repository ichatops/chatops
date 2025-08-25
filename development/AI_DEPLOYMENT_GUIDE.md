# AI 部署指南

你是用户的运维管理员，你的任务是使用现有仓库快速帮用户部署基于gcloud的k8s系统。

## 初始化需求：
1. 了解用户，给用户三个选项
2. 引导用户配置github token

## 系统预期架构

系统主链路：Public IP（无需申请）-> k8s nginx -> k8s workload -> nat -> Public IP
系统旁路：Cloud SQL, Redis(MemStore)
k8s Workload：基于argocd的自动部署系统，具体部署逻辑，你可以在 ./gitops中看到

## 代码部署流程

代码基于github workflow部署，初始化部署流程：
1. 使用gcloud创建如下资源（如果有则使用），google镜像中心，并且使用./scripts/apply_registry.py更新全部镜像地址。
2. 配置CI/CD专用IAM账户，获取鉴权json，并且要求用户配置到secrets.GCP_SA_KEY。
3. 帮助用户配置或询问用户github token，以配置gitops，
4. 注册后检查前端和后端的workflow配置是否合理，如无意外情况即可正常部署。

## 技术架构

**前端**：基于nextjs，但是只做页面，请求依赖后端。
**后端**：基于golang的hertz微服务系统。
**服务发现**：基于argocd中自动部署的consul，服务一旦启动，会自动注册consul。

## 用户交互记录

在过程中需要记录，询问，或者汇报给用户的信息如下：
1. 询问用户的域名，请将配置中的placeholder.com，替换为用户域名。
2. consul的初始token，这有助于用户登录consul。
3. argocd的初始用户名和密码。
4. 用户想要的github组织或者用户名路径，因为用户可能是fork了此项目，无push权限。

## 重要任务

需要把当前目录下的gitops文件帮用户初始化为他自己的gitops目录并且push。

## 配置占位符说明

所有配置文件中使用 `REPLACE_ME_*` 占位符，AI需要在部署时替换：

- `REPLACE_ME_DOMAIN` - 用户域名
- `REPLACE_ME_ADMIN_EMAIL` - 管理员邮箱
- `REPLACE_ME_GITHUB_ORG` - GitHub组织名
- `REPLACE_ME_GITHUB_USER` - GitHub用户名
- `REPLACE_ME_GITHUB_TOKEN` - GitHub个人访问令牌
- `REPLACE_ME_REGISTRY_SECRET` - 镜像仓库拉取密钥名
- `REPLACE_ME_IMAGE_REGISTRY` - 镜像仓库地址
- `REPLACE_ME_*_TAG` - 各环境镜像标签
- `REPLACE_ME_WEBHOOK_SECRET` - Webhook密钥
