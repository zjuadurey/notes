# 使用 pnpm 新建与打开 Slidev 项目

## 1. 基本原则

以后创建和管理 Slidev 项目时，建议统一使用 `pnpm`，不要混用 `npm install`、`yarn install` 等命令。

推荐原因：

- `pnpm` 可以复用全局依赖缓存，避免每个项目重复下载大量依赖；
- 安装速度通常更快；
- 多个 Slidev / Vue / Vite 项目之间更节省磁盘空间；
- 项目依赖管理更稳定。

---

## 2. 第一次配置 pnpm

如果系统还没有启用 pnpm，可以先执行：

```bash
corepack enable
corepack prepare pnpm@latest --activate
```

检查是否安装成功：

```bash
pnpm -v
```

如果能正常输出版本号，说明 `pnpm` 已经可以使用。

---

## 3. 新建 Slidev 项目

推荐使用：

```bash
pnpm create slidev@latest my-slidev-project
```

例如：

```bash
pnpm create slidev@latest nature-system-survey
```

创建过程中，如果出现：

```text
Install and start it now?
```

建议选择：

```text
no
```

这样可以避免 Slidev Creator 内部自动选择错误的包管理器。

然后手动进入项目：

```bash
cd nature-system-survey
```

安装依赖：

```bash
pnpm install
```

启动项目：

```bash
pnpm dev
```

启动成功后，终端一般会显示类似：

```text
Local: http://localhost:3030/
```

在浏览器中打开该地址即可查看 Slidev 页面。

---

## 4. 如果创建时误选了 npm

如果在创建项目时误选了：

```text
Choose the package manager › npm
```

可以先中断：

```bash
Ctrl + C
```

然后进入项目目录：

```bash
cd nature-system-survey
```

删除 npm 生成的依赖文件：

```bash
rm -rf node_modules package-lock.json
```

重新用 pnpm 安装：

```bash
pnpm install
```

启动项目：

```bash
pnpm dev
```

---

## 5. 打开已有 Slidev 项目

如果项目已经存在，例如：

```bash
cd ~/notes/06_slidev/nature-system-survey
```

先安装依赖：

```bash
pnpm install
```

然后启动：

```bash
pnpm dev
```

启动成功后，在浏览器中打开终端给出的本地地址，例如：

```text
http://localhost:3030/
```

---

## 6. 日常使用命令

进入项目目录：

```bash
cd nature-system-survey
```

启动本地预览：

```bash
pnpm dev
```

构建静态文件：

```bash
pnpm build
```

导出 PDF：

```bash
pnpm export
```

如果导出 PDF 时提示缺少浏览器依赖，可以先安装 Playwright：

```bash
pnpm exec playwright install
```

然后再次导出：

```bash
pnpm export
```

---

## 7. 推荐工作流总结

### 新建项目

```bash
pnpm create slidev@latest project-name
cd project-name
pnpm install
pnpm dev
```

### 打开已有项目

```bash
cd project-name
pnpm install
pnpm dev
```

### 如果误用了 npm

```bash
rm -rf node_modules package-lock.json
pnpm install
pnpm dev
```

---

## 8. 注意事项

不要在同一个项目中混用以下锁文件：

```text
package-lock.json
pnpm-lock.yaml
yarn.lock
```

如果决定使用 `pnpm`，项目中应主要保留：

```text
pnpm-lock.yaml
```

以后安装依赖统一使用：

```bash
pnpm install
```

启动项目统一使用：

```bash
pnpm dev
```

不推荐：

```bash
npm init slidev@latest
npm install
npm run dev
```

推荐：

```bash
pnpm create slidev@latest
pnpm install
pnpm dev
```