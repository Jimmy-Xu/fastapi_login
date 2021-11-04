# About
This project implements a simple blogging platform with user accounts, to showcase how to work with `fastapi-login`.

# Getting started
First you have to download this project, there are various methods how to download only this folder.
 - https://download-directory.github.io/ Downloads the folder as a zip file.
 - Clone the complete project and enter the examples folder by hand.

Next we have to create a virtual environement to install the dependencies
```
python -m venv venv
````

After activating the newly created environement we can install the project's dependencies
```
pip install -i https://mirrors.aliyun.com/pypi/simple/ -r requirements.txt`
```

Microsoft Visual C++ 14.0 or greater is required
```
Microsoft Visual C++ 14.0 or greater is required. Get it with "Microsoft C++ Build Tools": https://visualstudio.microsoft.com/visual-cpp-build-tools/

// method 1 (recommend)
wget https://download.visualstudio.microsoft.com/download/pr/5a50b8ac-2c22-47f1-ba60-70d4257a78fa/d662d2f23b4b523f30e24cbd7e5e651c7c6a712f21f48e032f942dc678f08beb/vs_Community.exe
需要选择 Visual C++生成工具(CMake) 和 windows 10 SDK即可，安装位置可以自行修改. 可以看到安装大小大约为4GB左右

// method 2
到 https://www.lfd.uci.edu/~gohlke/pythonlibs/ 下载对应后缀为 .whl 的安装包进行安装。
```

Before we can run the webapp we need to create a suitable secret key and a admin user:
```
cd example\full-example

// install requirements
pip install -i https://mirrors.aliyun.com/pypi/simple/ wheel python-dotenv sqlalchemy sphinx pysqlite3 pydantic fastapi_login bcrypt uvicorn python-multipart

// create .env
echo secret=test > .env
python main.py create-secret

// create sqlite db file: app.db
python main.py create-admin <username> <password>
```


create users table if users not exist
```
//open app.db with SQLiteStudio
CREATE TABLE users (
    username VARCHAR (20)  PRIMARY KEY,
    password VARCHAR (128),
    is_admin INTEGER
);
```


Now we can start running the application
```
python main.py start
```

This will start the application on [127.0.0.1:8000](127.0.0.1:8000).

Visist [127.0.0.1:8000/docs](127.0.0.1:8000/docs) to try out the API.

# Technical information
We will use `fastapi-login` for authentication and `sqlalchemy` together with `sqlite` as our database.
`python-dotenv` is used in combination with pydantics `BaseConfig` for config management.
All code concerning `fastapi-login` is contained inside the `app/auth` folder.