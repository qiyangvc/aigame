# 环境配置

默认采用 conda 进行 Pyhton 虚拟环境管理，请提前配好 conda 环境

1. **创建 Python 虚拟环境**

```bash
conda create -n aigame python=3.12
conda activate aigame
```

如果是在 windows 上使用 conda，可能会遇到 `conda activate` 无效问题，请查看此[链接](https://blog.csdn.net/u010393510/article/details/130715238)解决

2. **下载 Python 依赖**

```bash
git clone https://github.com/SYSUMSC/aigame.git
cd aigame

pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
pip install -r requirements.txt
```

3. **运行**

```bash
cd app
python main.py
```

接着在本地浏览器打开 `localhost:8000/admin` 路径，开发默认账号是 **admin**，密码是 **123456**

# 路径说明

```
- app #python fastapi后端与admin(采用layuiadmin非前后端分离)
- frontend # 用户端 前后端分离
```

# 格式化 import

```
python -m isort .
```

美化jinja html

```
d:\ProgramData\miniconda3\envs\newaigame\python.exe -m pip install -U djlint --target D:\ProgramData\miniconda3\envs\newaigame\Lib\site-packages
```



fastcrud文档：https://igorbenav.github.io/fastcrud/

SQLModel文档：https://sqlmodel.fastapi.org.cn/

接口说明，返回json，有字段code 0正常，1异常,msg中文消息,data=数据（可能没有）,count数据总长度，是分页前的总长度（可能没有）

错误返回的http码仍是200，只是code变为1，msg为异常原因，禁止使用返回接口raise HTTPException(status_code=404, detail="错误")

后台对于一个表，通常有的操作有

- 新增，修改（传入id），根据ModelSchema字段进行添加

- 删除（传入id），批量删除（传入ids，`,`分割）

- 查询
    post参数根据ModelSearchSchema的字段进行查询，如果是int则=匹配，如果是str则like % %匹配
    get参数为page，limit
    
- 使用json body传参（后台layuiadmin需要修改）

    ```
                      contentType: "application/json;charset=UTF-8",
                      data: JSON.stringify(field),
    ```

    

# vscode拓展

admin相关

- Jinja2 Snippet Kit
- Better Jinja
- djlint


# 杂


在我电脑的conda上不知道为啥需要指定才能安装到特定环境的路径
```
pip install -r requirements.txt --target D:\ProgramData\miniconda3\envs\newaigame\Lib\site-packages
```
