## 部署

1. 打开下面的仓库链接，将项目 Fork 到自己账号

`https://github.com/ciiiii/cloudflare-docker-proxy`

2. 创建 API Token

1. 登录 Cloudflare，点击左侧的 Workers and Pages，复制右侧窗口的 Account ID
2. 点击右上角的头像，选择 My Profile
3. 点击左侧的 API Tokens，点击 Create Token, 选择 Edit Cloudflare Workers
4. 选择 Account Resources，选择 Specific Zone，选择自己的域名，点击 Continue to Summary
5. 检查并点击创建 cloudflare API Token，复制 Token

3. 修改仓库中的 `src/index.js`

> 将 `ketches.cn` 替换为自己的域名

```javascript
const routes = {
  "docker.yourdomain.com": "https://registry-1.docker.io",
  "quay.yourdomain.com": "https://quay.io",
  "gcr.yourdomain.com": "https://gcr.io",
  "k8s-gcr.yourdomain.com": "https://k8s.gcr.io",
  "k8s.yourdomain.com": "https://registry.k8s.io",
  "ghcr.yourdomain.com": "https://ghcr.io",
  "cloudsmith.yourdomain.com": "https://docker.cloudsmith.io",
};
```
### 修改 README.md 文件中的 Deploy to Cloudflare Workers 按钮的 Url

> 将 `https://github.com/ciiiii/cloudflare-docker-proxy` 改为自己的仓库地址，例如：

```markdown
[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/ciiiii/cloudflare-docker-proxy)

# 更改为

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/npcxiao/cloudflare-docker-proxy)
```

[![部署](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/npcxiao/cloudflare-docker-proxy)

### 点击 README.md 中的按钮 `Deploy to Cloudflare Workers` 部署代码

### 为代码仓库启用 Github Actions

> Actions > I understand my workflows, go ahead and enable them

### 添加 Secrets

> Settings > Secrets > New repository secre

```
CLOUDFLARE_API_TOKEN: Cloudflare API Token
CLOUDFLARE_ACCOUNT_ID: Cloudflare Account ID
```

## 使用

### 修改 `/etc/docker/daemon.json`

```json
{
  "registry-mirrors": ["https://docker.yourdomain.com"]
}
```

### 拉取镜像

```bash
# docker pull k8s.gcr.io/pause:3.9
# use k8s.yourdomain.com as the registry proxy =>

docker pull k8s.yourdomain.com/pause:3.9
```


