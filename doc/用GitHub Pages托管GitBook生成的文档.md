# 用GitHub Pages托管GitBook 生成的文档网站教程
# 方式一
## 前期准备
github账户

## 部署方式
本地填写文档内容+github自动化部署
main分支---deploy.yml---》自动生成gh-pages
分支（pages的内容）---》setting的pages选项选择使用deploy from a branch

## 本地仓库内容（main）
my-gitbook/
├── doc  
├── .github/workflows/deploy.yml  
├── README.md  
├── SUMMARY.md  
└── book.json  （可选）  

.github/workflows/deploy.yml：因为在github上自动部署，所以使用了这个文件。需要setting-actions-general选择workflow permission选择读和写权限开启（不过后面新仓库里面部署的时候直接使用默认的选项也可以，不知道怎么回事，不管了）  
doc：写好的文档存放在这里  
README.md：当成首页内容  
SUMMARY.md：目录  
book.json：gitbook根据里面的配置编译，不管在本地还是在github端执行 gitbook build都会读取该配置  

README.md、SUMMARY.md必须有，要不然没有内容显示



## github端的操作
新建github仓库；  
github仓库克隆到本地，把my-gitbook/下面的的内容放到main分支的根目录，推送到github，  
（或者本地建立仓库，关联到远端仓库也可以）；  
.github/workflows/deploy.yml会根据yml里面设置的条件自动执行，自动新建分支gh-pages，gitbook把main的内容编译成 网页内容，生成到_book文件夹下，然后自动把_book文件夹下的内容复制到gh-pages，执行完毕，网页内容生成完成，都是自动完成，大概2分钟；  
把gh-pages的内容部署到网页：setting的pages选项选择使用deploy from a branch，github自动部署，大概1分钟；  
刷新自己的网页 `https://username.github.io/仓库名`，就会显示文档内容了。  

这种方式就是只能在线部署后才能看到效果。

# 方式二
本地使用gitbook把原文档内容编译生成网页内容，一般存放在_book文件夹，把_book文件夹下的内容（不是_book文件夹）推送到云端仓库根目录下，setting的pages选项选择使用deploy from a branch选择分支部署网页即可。
尝试了，但是gitbook使用的node版本旧Node 10，没下载好，就没有再搞了。

或者使用docker容器，这样就不用管那些版本问题，可以在本地先显示效果，，但是有一些插件没有设置好，效果有一点点差别，之后有时间再尝试了。

# 附录：
| 格式                         | 是否支持      | 推荐程度    | 说明                              |
| -------------------------- | --------- | ------- | ------------------------------- |
| `.md` (Markdown)           |  **支持**  |  强烈推荐 | GitBook 的主力格式，用于编写文档、目录、章节内容    |
| `.asciidoc`                |  支持（需插件） |  一般   | 需要安装 `asciidoc` 插件，不是默认支持       |
| `.html`                    |  可以内嵌   |  不推荐  | 可以在 `.md` 里嵌入少量 HTML，但不适合作主文档格式 |
| `.txt`                     |  不支持    | -       | 纯文本无法直接用作 GitBook 页面            |
| `.rst` (reStructuredText)  |  不支持    | -       | GitBook 默认不支持 RST（Sphinx 用这个）   |
| `.pdf` / `.epub` / `.mobi` |  不是输入格式 | -       | 这些是 GitBook 的输出格式，不是写作格式        |


book.json内容解释  

| 字段            | 用途                                                    |
| ------------- | ----------------------------------------------------- |
| `title`       | 网页生成的 `<title>` 标签内容（浏览器标签页标题）                        |
| `description` | 网页 `<meta name="description">` 的内容，用于 SEO（不会直接显示在页面上） |
