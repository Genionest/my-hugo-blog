+++
date = '2023-07-14T22:48:31+08:00'
title = 'hugo部署个人博客'
categories = ['website']
tags = ['hugo', 'blog']
cover = "/images/wallpaper1.jpg"
+++

### 安装hugo
[hugo官方文档](https://gohugo.io/getting-started/installing/)

### 选择reimu主题
[reimu主题](https://github.com/D-Sketon/hugo-theme-reimu?tab=readme-ov-file#%E5%AE%89%E8%A3%85)

### 添加或修改图片
[教程链接](https://github.com/D-Sketon/hugo-theme-reimu?tab=readme-ov-file#%E5%A4%B4%E5%83%8F%E5%B0%81%E9%9D%A2%E5%A4%B4%E5%9B%BE%E5%92%8Cfavicon)
如果希望添加静态图片，可以放在themes/reimu/images目录下

如果想要给文章制定封面
```markdown
+++
cover = "/images/wallpaper1.jpg"
+++
```

### 添加tag
```markdown
+++
tags = ['标签']
categories = ['类型']
+++
```

### 添加文章
```bash
hugo new posts/文章名.md
```

或者直接在post目录下创建markdown文件，但要注意带上front matter
```markdown
+++
title = '文章名'
+++
```

如果想要把文章添加到其他目录下（非post目录），需要修改params.yml文件

```yml
mainSections: ["post", "xxx"] 
# xxx为你想添加的目录名
```

### 评论系统
[开启评论](https://github.com/D-Sketon/hugo-theme-reimu?tab=readme-ov-file#%E7%AB%99%E5%86%85%E8%AF%84%E8%AE%BA)
使用waline评论系统，配置LeanCloud和部署Vercel。
[waline配置](https://waline.js.org/guide/get-started/#leancloud-%E8%AE%BE%E7%BD%AE-%E6%95%B0%E6%8D%AE%E5%BA%93)

### 其他需要配置的点
[代码块](https://github.com/D-Sketon/hugo-theme-reimu?tab=readme-ov-file#%E4%BB%A3%E7%A0%81%E5%9D%97)

### 部署hugo到云服务器
打包到public目录下
```bash
hugo -d public
```
public里就有了完整的网站内容，只依赖nginx就可以工作了，
nginx是可以部署网页内容的。

在gitee(因为服务器是在国内，国外可以尝试github)上创建一个my_blog仓库，并同步到本地，
得到一个my_blog目录，
将public目录复制到my_blog目录下，
这样就有了my_blog/public目录

我们使用nginx部署网站，并通过docker启动nginx

创建my_blog/Dockerfile
```Dockerfile
FROM nginx:alpine

# 删除默认内容
RUN rm -rf /usr/share/nginx/html/*

EXPOSE 80 443
```

创建my_blog/nginx.conf (nginx配置文件)
```nginx
server {
    listen 80;
    listen 443 ssl;
    server_name _;

    root /usr/share/nginx/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
        # Hugo 的 pretty URL 支持
        # if (-f $request_filename/index.html) {
        #     rewrite (.*) $1/index.html break;
        # }
    }

    # 缓存静态资源
    location ~* \.(jpg|jpeg|png|gif|ico|css|js|svg|webp)$ {
        expires 365d;
    }
}
```

现在我们可以上传到gitee服务器上了，
然后我们在云服务器上同步my_blog仓库，
进入my_blog/目录下

创建docker镜像
```bash
docker build -t hugo-site .
```
创建并运行容器
```bash
docker run -d \
    --name my-hugo \
    -p 80:80 \
    -p 443:443 \
    -v ./public:/usr/share/nginx/html \
    -v ./nginx.conf:/etc/nginx/conf.d/default.conf \
    hugo-site
```
如果权限不够，请使用sudo

云服务起一般都会开放80和443端口，如果没有，请自行开放，
80端口是http，443端口是https

### 一些问题
如果使用http访问，可能会有些图片加载不出来