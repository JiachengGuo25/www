# Day 5 项目模板 · 从这里开始

> **Wind × Python × AI 暑期训练营 — Day 5 下午**
>
> 这个仓库是你今天下午项目的起点。先按下面的步骤把它在自己电脑上跑起来，
> 看到一个真正的网页应用，再开始改成你自己的。

**读完这一页大约 5 分钟，跑通大约 15 分钟。**

---

## 一、什么是 Streamlit？

### 先说你现在遇到的问题

上午你在 Jupyter Notebook 里做完了分析：取数、清洗、画图、算相关系数。
现在假设你要把结果给别人看。

- 发 `.ipynb` 文件？对方要装 Anaconda，还要会按 Shift + Enter
- 截图发出去？别人想换个时间段看，只能来问你
- 做成 PPT？下周数据更新了，整套图要重做一遍

**Notebook 是给你自己用的。它记录你怎么想的，但它不是一个"产品"。**

### Streamlit 做的事

Streamlit 是一个 Python 库，它把你的 Python 脚本变成一个**网页**。

关键在于：**你不需要学 HTML、CSS 或 JavaScript。** 你只写 Python。

```python
import streamlit as st

st.title("我的标题")          # 网页上出现一个标题
st.line_chart(df)             # 网页上出现一张折线图
st.dataframe(df)              # 网页上出现一张可以滚动的表格
```

三行 Python，就有了一个网页。

### 和 Notebook 的分工

| | Jupyter Notebook | Streamlit |
|---|---|---|
| 给谁看 | **你自己**，和懂 Python 的同事 | **任何人**，包括不会编程的人 |
| 打开方式 | 装 Anaconda，打开文件 | 点一个网址 |
| 展示什么 | 完整的推理过程、每一步的代码 | 结论、图表、可交互的筛选 |
| 用来做什么 | 分析、试错、留下记录 | 汇报、分享、放进简历 |

**两个都要有。** Notebook 证明你会分析，Streamlit 证明你能交付。

> 今天不学 Streamlit 的高级功能（session state、cache、复杂布局、回调）。
> 你只需要知道：**它读你导出的 CSV，然后把图画在网页上。**

---

## 二、五分钟跑起来

### 第 1 步 · 下载这个仓库

点这个页面右上角绿色的 **`< > Code`** 按钮 → **Download ZIP**

<details>
<summary>装了 Git 的同学也可以用 clone（可选，不装 Git 完全没问题）</summary>

```bash
git clone https://github.com/xiangyun-lu/ibss_wind_camp_2026_template.git
```

</details>

下载完**解压**到一个你找得到的地方，比如桌面。

> ⚠️ **一定要解压。** Windows 可以直接双击进 zip 看里面的文件，
> 但那只是"预览"，程序跑不了。右键 → 全部解压缩。

### 第 2 步 · 打开 Anaconda Prompt

开始菜单 → 找到 **Anaconda3** 文件夹 → 点 **Anaconda Prompt**

会弹出一个命令行窗口，开头长这样：

```
(base) C:\Users\你的名字>
```

> 这不是 Jupyter。它是命令行 —— 今天我们只在这里敲**三条命令**，敲完就不用了。

### 第 3 步 · 切换到项目文件夹

用 `cd` 命令（change directory，切换目录）。

**最省事的办法**：先打 `cd ` （注意 `cd` 后面有个空格），
然后**把解压出来的文件夹直接拖进命令行窗口**，路径会自动填好。再按回车。

```
cd C:\Users\你的名字\Downloads\day5-industry-monitor-template
```

按回车后，行首会变成你的文件夹路径。用 `dir` 确认一下：

```
dir
```

**你应该看到 `streamlit_app.py` 和 `requirements.txt`。**
如果没看到，说明还没进对文件夹（解压后常常会多一层同名文件夹，再 `cd` 一次）。

### 第 4 步 · 安装 Streamlit

```
pip install -r requirements.txt
```

`requirements.txt` 里写了这个项目需要哪些库。这条命令的意思是：
"照着这个清单，把缺的都装上"。

会滚动一堆文字，等它停下来。看到 `Successfully installed ...`
或者 `Requirement already satisfied` 都算成功。**第一次大约需要 1–3 分钟。**

### 第 5 步 · 运行

```
streamlit run streamlit_app.py
```

**第一次运行会问你要邮箱** —— 直接按回车跳过，不用填。

然后你会看到：

```
  You can now view your Streamlit app in your browser.

  Local URL: http://localhost:8501
```

**浏览器会自动打开**，你的应用就在那里了。
（没自动打开的话，手动把 `http://localhost:8501` 复制到浏览器。）

### 第 6 步 · 玩一下

- 拖动左边侧边栏的**时间范围**滑块，看图表怎么变
- 勾选/取消不同的**宏观指标**
- 展开最下面的"数据字典"看看

**恭喜。你刚刚在自己电脑上跑起来了一个 Web 应用。**

### 停止运行

回到命令行窗口，按 **`Ctrl + C`**。

---

## 三、你刚才到底看到了什么

这是今天最值得花两分钟看懂的部分：**把网页和代码对起来。**

| 你在网页上看到的 | `streamlit_app.py` 里对应的代码 |
|---|---|
| 最上面的大标题 | `st.title(APP_TITLE)` |
| 四个数字方块（利率、销售…） | `col.metric(label, value, delta)`，`col` 来自 `st.columns(4)` |
| 折线图 | `st.line_chart(macro_view[chosen])` |
| 散点图 | `st.scatter_chart(scatter_df, x=..., y=...)` |
| 可滚动的表格 | `st.dataframe(corr.round(2))` |
| 左边的筛选栏 | `st.sidebar.multiselect(...)` |
| "数据字典"那个可折叠区 | `st.expander("数据字典")` |
| 段落文字 | `st.markdown("...")` |

**规律**：`st.` 开头的每一行，都会在网页上"长出"一个东西，
从上往下按代码的顺序排列。

### 数据是从哪来的？

打开 `data/` 文件夹看看 —— 里面是六个 CSV。

应用开头这几行把它们读进来：

```python
macro = pd.read_csv("data/macro_monthly.csv", index_col="Date", parse_dates=True)
```

**注意：这个应用没有连 Wind，也没有联网取数。它只是读 CSV。**

> 这就是上午 Part 9 讲的**"算一次，存下来，画很多次"**。
> 现在 `data/` 里放的是示例数据；下午你要把它换成**你自己导出的**。

### 改一行试试

1. 用记事本（或 VS Code）打开 `streamlit_app.py`
2. 找到最上面的 `APP_TITLE = "Power Tools Industry Monitor"`
3. 改成你自己的标题，保存
4. 回到浏览器 —— 右上角会出现 **Rerun** 按钮，点它（或者直接按 `R`）

**改代码 → 保存 → 刷新，几秒钟就能看到效果。** 这就是 Streamlit 的开发方式。

---

## 四、常见问题

| 现象 | 原因 | 怎么办 |
|---|---|---|
| `'pip' 不是内部或外部命令` | 用了系统 cmd，不是 Anaconda Prompt | 从开始菜单重新打开 **Anaconda Prompt** |
| `'streamlit' 不是内部或外部命令` | 第 4 步没装成功 | 重跑 `pip install -r requirements.txt`，看有没有报错 |
| `系统找不到指定的路径` | `cd` 的路径不对 | 用拖拽文件夹的办法重新 `cd` |
| `FileNotFoundError: data/...csv` | 没在项目根目录运行 | 先 `dir`，确认能看到 `streamlit_app.py` |
| 浏览器打开是空白 | 应用还在启动 | 等几秒，刷新一次 |
| 装的时候卡住不动 | 网络慢 | 换国内镜像（见下） |
| 端口被占用 | 上一个应用没关 | `streamlit run streamlit_app.py --server.port 8502` |

<details>
<summary>pip 装得很慢？用清华镜像</summary>

```
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
```

</details>

**卡住超过 10 分钟，请举手。** 不要一个人闷着。

---

## 五、接下来做什么

| 步骤 | 做什么 |
|---|---|
| 1 | 注册 GitHub 账号 |
| 2 | **（你已经完成）** 下载模板，本地跑通，看到 dashboard |
| 3 | 从 FRED 下载四个 CSV |
| 4 | 完成你自己的 Notebook 分析 |
| 5 | 运行 Notebook Part 9，导出你的数据 |
| 6 | 用 **Use this template** 把这个仓库复制到你自己的账号 |
| 7 | 把你的 CSV 和 Notebook 上传上去 |
| 8 | 部署到 Streamlit Community Cloud (通过你的Github账号登录Streamlit)，拿到你的网址 |
| 9 | 改 `streamlit_app.py` 里的 5 个 `TODO`，写你自己的 Findings |
| 10 | **把这个 README 换成 `PROJECT_README.md` 的内容** |

> ### ⚠️ 第 10 步别忘了
>
> 你现在读的这个 README 是**操作说明**，是写给你的。
>
> 但等你的仓库公开之后，别人（包括面试官）点进来第一眼看到的就是它 ——
> 他们不需要知道怎么装 Streamlit，他们想知道**你做了什么**。
>
> 所以最后一步：把 `PROJECT_README.md` 的内容复制到 `README.md` 里，然后根据需要修改。

---

## 六、仓库结构

```
├── README.md               ← 你正在读的这一页（操作说明，最后要替换掉）
├── PROJECT_README.md       ← 给别人看的项目介绍模板
├── streamlit_app.py        应用本体，里面有 5 个 TODO
├── requirements.txt        依赖清单
├── data/                   数据（现在是示例，下午换成你自己的）
│   ├── macro_monthly.csv
│   ├── market_prices.csv
│   ├── market_normalized.csv
│   ├── company_snapshot.csv
│   ├── correlation.csv
│   └── data_dictionary.csv
└── notebook/
    └── analysis.ipynb      分析过程（下午换成你自己的）
```

## 七、学习其他同学的仓库

https://github.com/Surinnuo/PIZZA_Project

可搜索更多你感兴趣的仓库

---

## 声明

本项目为 Wind × Python × AI 暑期训练营的教学材料，仅用于学习演示，
**不构成任何投资建议**。宏观数据来自Demo模拟数据文件。
