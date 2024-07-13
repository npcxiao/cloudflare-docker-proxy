## 部署

### Fork 下面的项目

`https://github.com/ciiiii/cloudflare-docker-proxy`

### 创建 API Token

1. 登录 Cloudflare，点击左侧的 Workers and Pages，复制右侧窗口的 Account ID
2. 点击右上角的头像，选择 My Profile
3. 点击左侧的 API Tokens，点击 Create Token, 选择 Edit Cloudflare Workers
4. 选择 Account Resources，选择 Specific Zone，选择自己的域名，点击 Continue to Summary
5. 检查并点击创建 cloudflare API Token，复制 Token

### 修改 `src/index.js`

> 将 `ketches.cn` 替换为自己的域名

```javascript
const routes = {
  "docker.ketches.cn": "https://registry-1.docker.io",
  "quay.ketches.cn": "https://quay.io",
  "gcr.ketches.cn": "https://gcr.io",
  "k8s-gcr.ketches.cn": "https://k8s.gcr.io",
  "k8s.ketches.cn": "https://registry.k8s.io",
  "ghcr.ketches.cn": "https://ghcr.io",
  "cloudsmith.ketches.cn": "https://docker.cloudsmith.io",
};
```

### 修改 README.md 中的 Deploy to Cloudflare Workers 按钮的 Url

> 将 `https://github.com/ciiiii/cloudflare-docker-proxy` 改为自己的仓库地址，例如：

```markdown
[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/ciiiii/cloudflare-docker-proxy)

# 更改为

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/npcxiao/cloudflare-docker-proxy)
```

[![部署](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/npcxiao/cloudflare-docker-proxy)


[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/ciiiii/cloudflare-docker-proxy)

### 点击 Deploy to Cloudflare Workers 部署代码

## 使用

### 修改 `/etc/docker/daemon.json`

```json
{
  "registry-mirrors": ["https://<workername>.<username>.workers.dev"]
}
```

```json
{
  "registry-mirrors": ["https://docker.yourdomain.com"]
}
```

### 拉取镜像

```bash
# docker pull k8s.gcr.io/pause:3.9
# use k8s.ketches.cn as the registry proxy =>

docker pull k8s.ketches.cn/pause:3.9
```

## 使用 Github Actions 部署

TODO: 待更新

### 为代码仓库启用 Github Actions

> Actions > I understand my workflows, go ahead and enable them

### 添加 Secrets

> Settings > Secrets > New repository secre

```
CLOUDFLARE_API_TOKEN: Cloudflare API Token
CLOUDFLARE_ACCOUNT_ID: Cloudflare Account ID

```
