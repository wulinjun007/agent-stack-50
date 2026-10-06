# 部署四通道 · AgentStack 50

站点是单文件静态页（`index.html`），无构建步骤——任何能伺服静态文件的东西都能部署它。

## 通道 ① GitHub Pages（主通道，当前生效）

```bash
git init && git add -A && git commit -m "AgentStack 50 v1.0"
gh repo create agent-stack-50 --public --source=. --push
gh api repos/wulinjun007/agent-stack-50/pages -X POST \
   -f "source[branch]=main" -f "source[path]=/"
```

生产地址：`https://wulinjun007.github.io/agent-stack-50/`

## 通道 ② Docker（任意主机）

```bash
docker compose -f deploy/docker-compose.yml up -d
# → http://localhost:8080
```

镜像 = nginx:alpine + 单个 index.html，无构建层。构建上下文是仓库根（compose 已写好），Coolify/Dokploy 会自动识别这份 compose。

## 通道 ③ Coolify / Dokploy（自托管 PaaS）

1. 新建应用 → 指向本仓库；
2. 构建包选 **Docker Compose**，Compose 文件路径填 `deploy/docker-compose.yml`；
3. Coolify 记得在域名设置里放开端口映射（8080）；Dokploy 默认直接暴露。

## 通道 ④ 本地零依赖预览

```bash
python3 -m http.server 8080
# → http://localhost:8080
```

（直接双击 index.html 也能用——数据内联在页面里，无 fetch 请求。）

---

## 月度刷新流程（新维护者照此执行）

1. 重跑数据核验：对 `TOP50-榜单.md` 中 50 个仓库重拉 `GET /repos/{owner}/{repo}`（star/pushed_at/license）；
2. 人工过差异：star 变动照抄；仓库若 301 迁移，更新 `org/repo` 并在条目内注明；推送超 6 个月的条目加「停更」标记并复核入选理由；
3. 同步更新三处：`index.html` 内嵌 DATA 数组、`TOP50-榜单.md`、页眉期号行（`第 00N 期 · 快照 <日期>`）与 PRD 中的总星数；
4. 重跑 QA（四视口截图 + 58 门禁抽检）后按通道 ①/② 重新部署；
5. 在 git tag 记录期号：`git tag v1.1-2026-11 && git push --tags`。
