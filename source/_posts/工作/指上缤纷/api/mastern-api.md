---
title: mastern api
abbrlink: api.mastern
sage: true
categories:
  - 工作
  - 指上缤纷
  - api
date: 2019-08-16 18:47:51
---

# 客户端api

## 获取ev

请求示例

```josn
http://192.168.0.246/mastern/api/ev.do?t=wd
```

定义

| 参数 | 涵义                       |
| ---- | -------------------------- |
| wd   | 微端ev（非小游戏类的类型） |
| wx   | 微信小游戏ev               |
| op   | oppo小游戏ev               |
| qq   | qq小游戏ev                 |
| zj   | 字节跳动小游戏ev           |

<!-- more -->

返回示例

```josn
{
    "data": "5"
}
```

## 获取gv

请求示例

```josn
http://192.168.0.246/mastern/api/gv.do?game=20001
```

返回示例

```josn
{
    "data": {
        "gv": "4", 
        "rv": "2", 
        "sv": "0"
    }
}
```

| 参数 | 涵义            |
| ---- | --------------- |
| gv   | gv版本          |
| rv   | 资源版本        |
| sv   | config.json版本 |

## 获取游戏公告

请求示例

```josn
http://192.168.0.246/mastern/api/anno.do?pf=7000004
```

| 参数 | 涵义     |
| ---- | -------- |
| pf   | 平台标识 |

返回示例

```josn
{
    "data": "this is a anno"
}
```

# 后台部分

## 后台登陆

通用字段涵义说明

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": true, 
        "noRight": false
    }
}
```

| 参数     | 涵义                                    |
| -------- | --------------------------------------- |
| callback | ture:无msg返回；false:有msg返回         |
| data     | 根数据堆                                |
| noLogin  | true:未登录（跳转至登陆页）；false:登陆 |
| noRight  | true:有权限；false:无权限               |

### 1. 验证码

请求示例

```json
http://192.168.0.246/mastern/auth/changeCaptcha.admin
```

| 参数 | 涵义 |
| ---- | ---- |
| -    | -    |

返回示例

```json
{
    "data": {
        "callback": true, 
        "data": {
            "admin": {
                "login": {
                    "captchaImgUrl": "http://test3.h5eco.com:1234/code/28ba6951-acd2-4f76-b17b-62516836fccf.jpeg", 
                    "captchaId": "28ba6951-acd2-4f76-b17b-62516836fccf"
                }, 
                "noRight": false
            }
        }, 
        "noLogin": true, 
        "noRight": false
    }
}

```

| 参数          | 涵义       |
| ------------- | ---------- |
| captchaImgUrl | 验证码图片 |
| captchaId     | 验证码id   |

### 2. 登陆

请求示例

```json
http://192.168.0.246/mastern/auth/login.admin?name=aldmd&pwd=yanfei&kaptcha=6436&captchaId=5d7cb1a4-a0ee-4bd4-8ff3-f8724d878db2

```

| 参数      | 涵义                             |
| --------- | -------------------------------- |
| name      | username                         |
| pwd       | password                         |
| kaptcha   | 验证码                           |
| captchaId | 验证码id(请求验证码命令时会返回) |

成功返回示例

```json
#超级管理员数据返回
{
    "data": {
        "callback": true, 
        "data": {
            "admin": {
                "user": {
                    "token": "fba5ffc9550418e61e61b967d5714023", 
                    "superman": true, 
                    "name": "aldmd", 
                    "nameCn": "超级管理员"
                }
            }
        }, 
        "noLogin": false;
        "noRight": false
    }
}
#普通账户数据返回
{
    "data": {
        "callback": true, 
        "data": {
            "admin": {
                "token": "5a3ea9b74282502317ba633ead314ea9", 
                "superman": false, 
                "name": "u1", 
                "nameCn": "用户2", 
                "roleName": "gcp", 
                "roleNameCn": "游戏cp", 
                "showTab": "110_210_310_410", 
                "channels": "8000001_8000002"
            }
        }, 
        "noLogin": false
        "noRight": false
    }
}

```

失败返回示例

```json
{
    "data": {
        "callback": false, 
        "data": {
            "admin": {
                "login": {
                    "needLogin": true, 
                    "captchaImgUrl": "http://test3.h5eco.com:1234/code/7251b058-b0b7-43b4-98ce-291f023cfefe.jpeg", 
                    "captchaId": "7251b058-b0b7-43b4-98ce-291f023cfefe", 
                    "result": "验证码错误"
                }
            }
        }, 
        "noLogin": true
        "noRight": false
    }
}

```

| 参数       | 涵义                               |
| ---------- | ---------------------------------- |
| token      | 服务端返回的用于校验用户是否已登陆 |
| superman   | 是否是超级管理员                   |
| name       | username                           |
| nameCn     | 中文名                             |
| roleName   | 角色                               |
| roleNameCn | 角色中文                           |
| showTab    | 前端显示权限                       |
| channels   | 渠道权限（多个时用“_”拼接）        |

### 3. 修改密码

请求示例

```json
http://192.168.0.246/mastern/auth/changePwd.admin?name=aldmd&pwd=yanfei1&oldPwd=yanfei

```

| 参数   | 涵义     |
| ------ | -------- |
| name   | username |
| pwd    | 新密码   |
| oldPwd | 旧密码   |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false
        "noRight":false
    }
}

```

### 4. 注销（退出登录）

请求示例

```json
http://192.168.0.246/mastern/auth/logout.admin

```

| 参数 | 涵义 |
| ---- | ---- |
| -    | -    |

返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false;
        "noRight":false
    }
}

```

## 用户管理

### 获取用户信息

请求示例

```json
http://192.168.0.246/mastern/um/userInfo.admin

```

| 参数 | 涵义 |
| ---- | ---- |
| -    | -    |

返回示例

```json
{
    "data": {
        "callback": true, 
        "data": {
            "admin": {
                "user": {
                    "superman": true, 
                    "name": "aldmd", 
                    "nameCn": "超级管理员"
                }, 
                "noRight": false
            }
        }, 
        "noLogin": false, 
        "noRight": false
    }
}

```

## `host`管理

### 添加`host`

请求示例

```json
http://192.168.0.246/mastern/host/add.admin?key=fk1&domain=fk1.h5eco.com&innerIp=192.168.0.248

```

| 参数    | 涵义             |
| ------- | ---------------- |
| key     | 服务器的key      |
| domain  | 服务器对应的域名 |
| innerIp | 服务器内网ip     |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false
        "noRight":false
    }
}

```

### 修改`host`

请求示例

```json
http://192.168.0.246/mastern/host/up.admin?key=fk1&domain=fk1.h5eco.com&innerIp=192.168.0.246

```

| 参数    | 涵义             |
| ------- | ---------------- |
| key     | 服务器的key      |
| domain  | 服务器对应的域名 |
| innerIp | 服务器内网ip     |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false
        "noRight":false
    }
}

```

### 查看`host`

请求示例

```json
http://192.168.0.246/mastern/host/view.admin

```

| 参数    | 涵义             |
| ------- | ---------------- |
| key     | 服务器的key      |
| domain  | 服务器对应的域名 |
| innerIp | 服务器内网ip     |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": {
            "host": {
                "hosts": {
                    "fk1": {
                        "key": "fk1", 
                        "domain": "fk1.h5eco.com", 
                        "innerIp": "192.168.0.248"
                    }
                }
            }
        }, 
        "noLogin": false, 
        "noRight": false
    }
}

```

### 删除`host`

请求示例

```json
http://192.168.0.246/mastern/host/del.admin?key=fk1

```

| 参数 | 涵义        |
| ---- | ----------- |
| key  | 服务器的key |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false
        "noRight":false
    }
}

```

## `server`包管理

### 一建添加

> 需要linux环境才可能添加成功
> 请求示例

```json
http://192.168.0.246/mastern/op/autoAddServer.admin?name=fk_1&hostKey=fk1&path=/data/fk_1&wssPort=12346&adminPort=88000

```

| 参数      | 涵义            |
| --------- | --------------- |
| serverKey | server包的key   |
| hostKey   | 服务器域名的key |

成功返回示例

```json
{
    "data": "succ"
}

```

### 新增`server`包

> 脚本调用，后台管理不会调用此命令

请求示例

```json
http://192.168.0.246/mastern/op/newServer.admin?name=g1&hostKey=fk1&wssPort=12346&adminPort=8800

```

| 参数      | 涵义            |
| --------- | --------------- |
| name      | 包name          |
| hostKey   | 服务器域名的key |
| path      | 服务器相对路径  |
| wssPort   | wss端口         |
| adminPort | 后台端口        |

成功返回示例

```json
{
    "data": "succ"
}

```

### `server`包列表

请求示例

```json
http://192.168.0.246/mastern/op/serverList.admin
```

| 参数 | 涵义 |
| ---- | ---- |
| -    | -    |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": {
            "pf": {
                "servers": {
                    "fk_1": {
                        "name": "fk_1", 
                        "hostKey": "fk1", 
                        "path": "/data/fk_1", 
                        "wssPort": 12346, 
                        "adminPort": 88000
                    }
                }
            }
        }, 
        "noLogin": false, 
        "noRight": false
    }
}

```

## 平台管理

### 添加平台类型

请求示例

```json
http://192.168.0.246/mastern/pf/addPft.admin?name=1&nameCn=微端

```

| 参数   | 涵义               |
| ------ | ------------------ |
| name   | 平台类型的唯一标识 |
| nameCn | 平台类型的中文     |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false
        "noRight":false
    }
}

```

### 删除平台类型

请求示例

```json
http://192.168.0.246/mastern/pf/delPft.admin?name=1

```

| 参数 | 涵义               |
| ---- | ------------------ |
| name | 平台类型的唯一标识 |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false
        "noRight":false
    }
}

```

### 修改平台类型

请求示例

```json
http://192.168.0.246/mastern/pf/upPft.admin?name=1&nameCn=微端

```

| 参数   | 涵义               |
| ------ | ------------------ |
| name   | 平台类型的唯一标识 |
| nameCn | 平台类型的中文     |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false
        "noRight":false
    }
}

```

### 查看平台类型

请求示例

```json
http://192.168.0.246/mastern/pf/viewPfts.admin

```

| 参数 | 涵义 |
| ---- | ---- |
| -    | -    |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": {
            "pf": {
                "pftMap": {
                    "1": "微端", 
                    "2": "小游戏"
                }
            }
        }, 
        "noLogin": false, 
        "noRight": false
    }
}

```

| 参数   | 涵义          |
| ------ | ------------- |
| pftMap | 平台类型的map |

### 添加平台/渠道

请求示例

```json
http://192.168.0.246/mastern/pf/addPf.admin?name=7000005&nameCn=疯狂&typeName=1&friend=7000004

```

| 参数     | 涵义                   |
| -------- | ---------------------- |
| name     | 平台name（唯一标识）   |
| nameCn   | 平台中文               |
| friend   | 主渠道（和哪个渠道混） |
| tyepName | 平台类型               |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": {}, 
        "noLogin": false, 
        "noRight": false
    }
}

```

### 修改平台/渠道

请求示例

```json
http://192.168.0.246/mastern/pf/upPf.admin?name=7000005&nameCn=疯狂1&typeName=1&friend=7000004

```

| 参数     | 涵义                   |
| -------- | ---------------------- |
| name     | 平台name（唯一标识）   |
| nameCn   | 平台中文               |
| friend   | 主渠道（和哪个渠道混） |
| tyepName | 平台类型               |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": {}, 
        "noLogin": false, 
        "noRight": false
    }
}

```

### 查看平台/渠道

请求示例

```json
http://192.168.0.246/mastern/pf/viewPfs.admin?type=0

```

| 参数 | 涵义                                                         |
| ---- | ------------------------------------------------------------ |
| type | 只能传0或者1。0:角色能看到的所有渠道；1:只能看到主渠道或者独服渠道 |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": {
            "pf": {
                "pfs": [
                    {
                        "name": "70000010", 
                        "nameCn": "疯狂12", 
                        "games": [ ], 
                        "typeName": "1"
                    }, 
                    {
                        "name": "7000004", 
                        "nameCn": "爱微游", 
                        "games": [
                            "20001"
                        ], 
                        "typeName": "1"
                    }, 
                    {
                        "name": "7000005", 
                        "nameCn": "疯狂e1", 
                        "friend": "7000004", 
                        "games": [ ], 
                        "typeName": "1"
                    }
                ]
            }
        }, 
        "noLogin": false, 
        "noRight": false
    }
}


```

| 参数     | 涵义                               |
| -------- | ---------------------------------- |
| name     | 平台唯一标识                       |
| nameCn   | 平台中文名                         |
| friend   | 混服主渠道为空是标识主渠道或者独服 |
| games    | 渠道包含的所有分区                 |
| typeName | 平台类型                           |

### 删除平台/渠道（仅指定用户可以删除）

请求示例

```json
http://192.168.0.246/mastern/pf/delPf.admin?name=70000010

```

| 参数 | 涵义     |
| ---- | -------- |
| name | 平台name |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": {}, 
        "noLogin": false, 
        "noRight": false
    }
}

```

### 添加分区

请求示例

```json
http://192.168.0.246/mastern/pf/addGame.admin?pf=7000004&name=20001&nameCn=疯狂一区&redis=192.168.0.37:6379&server=rx2_&openTime=1557201600000&mysql=192.168.0.37:3306/g1

```

| 参数     | 涵义                                                         |
| -------- | ------------------------------------------------------------ |
| pf       | 平台唯一标识                                                 |
| name     | 分区唯一标识                                                 |
| nameCn   | 分区中文                                                     |
| redis    | redis地址                                                    |
| server   | server包的name                                               |
| mysql    | mysql地址                                                    |
| openTime | 开区时间（需要用时间插件控制只是年月日，导出格式为unix时间戳到毫秒） |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": {}, 
        "noLogin": false, 
        "noRight": false
    }
}

```

### 修改分区

请求示例

```json
http://192.168.0.246/mastern/pf/upGame.admin?pf=7000004&name=1&nameCn=疯狂一区&redis=192.168.0.37:6379&server=fk_1&openTime=1557201600000&mysql=192.168.0.37:3306/g1

```

| 参数       | 涵义                                                         |
| ---------- | ------------------------------------------------------------ |
| name       | 分区唯一标识                                                 |
| nameCn     | 分区中文                                                     |
| wss        | wss地址                                                      |
| redis      | redis地址                                                    |
| serverIp   | server所在服务器ip                                           |
| serverPath | server所在服务器的绝对路径                                   |
| optTime    | 开区时间（需要用时间插件控制只是年月日，导出格式为unix时间戳到毫秒） |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false, 
        "noRight": false
    }
}

```

### 删除分区（指定用户可以操作）

请求示例

```json
http://192.168.0.246/mastern/pf/delGame.admin?name=200010

```

| 参数 | 涵义     |
| ---- | -------- |
| name | 分区name |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false, 
        "noRight": false
    }
}

```

### 查看指定渠道所有分区

请求示例

```json
http://192.168.0.246/mastern/pf/viewGames.admin?pf=7000004

```

| 参数 | 涵义     |
| ---- | -------- |
| pf   | 平台name |

成功返回示例

```
{
    "data": {
        "callback": true, 
        "data": {
            "pf": {
                "games": [
                    {
                        "name": "20001", 
                        "nameCn": "爱微游一区", 
                        "pf": "7000004", 
                        "wss": "wss://game.h5eco.com:12346", 
                        "redis": "192.168.0.37", 
                        "serverIp": "192.168.0.241", 
                        "serverPath": "/data/server_20001", 
                        "open": false, 
                        "openTime": "1557201600000"
                    }
                ]
            }
        }, 
        "noLogin": false, 
        "noRight": false
    }
}

```

| 参数       | 涵义                                                         |
| ---------- | ------------------------------------------------------------ |
| name       | 分区唯一标识                                                 |
| nameCn     | 分区中文                                                     |
| pf         | 平台唯一标识                                                 |
| wss        | wss地址                                                      |
| redis      | redis地址                                                    |
| serverIp   | server所在服务器ip                                           |
| serverPath | server所在服务器的绝对路径                                   |
| optTime    | 开区时间（需要用时间插件控制只是年月日，导出格式为unix时间戳到毫秒） |

### 开服

请求示例

```json
http://192.168.0.246/masterni/pf/startServer.admin?name=20001

```

| 参数 | 涵义     |
| ---- | -------- |
| name | 分区name |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false, 
        "noRight": false
    }
}

```

### 停服

请求示例

```json
http://192.168.0.246/masterni/pf/stopServer.admin?name=20001

```

| 参数 | 涵义     |
| ---- | -------- |
| name | 分区name |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false, 
        "noRight": false
    }
}

```

## 公告管理

### 添加公告

请求示例

```json
http://192.168.0.246/mastern/anno/up.admin?pfs=7000004_7000005&anno=this is a anno

```

| 参数 | 涵义                    |
| ---- | ----------------------- |
| pfs  | 平台类型多个时用“_”隔开 |
| anno | 公告内容                |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": {}
        }, 
        "noLogin": false, 
        "noRight": false
    }
}

```

### 公告列表

请求示例

```json
http://192.168.0.246/mastern/anno/view.admin

```

成功返回示例

| 参数 | 涵义 |
| ---- | ---- |
| -    | -    |

```json
{
    "data": {
        "callback": true, 
        "data": {
            "anno": {
                "annos": {
                    "7000004": "this is a anno", 
                    "7000005": "this is a anno"
                }
            }
        }, 
        "noLogin": false, 
        "noRight": false
    }
}

```

| 参数  | 涵义                |
| ----- | ------------------- |
| annos | <渠道name,公告内容> |

## 客户端版本管理

### 查看ev

请求示例

```json
http://192.168.0.246/mastern/client/viewEv.admin

```

成功返回示例

| 参数 | 涵义 |
| ---- | ---- |
| -    | -    |

```json
{
    "data": {
        "callback": true, 
        "data": {
            "client": {
                "evs": {
                    "qq": "1", 
                    "zj": "1", 
                    "wx": "1", 
                    "op": "1", 
                    "wd": "1"
                }
            }
        }, 
        "noLogin": false, 
        "noRight": false
    }
}

```

| 参数 | 涵义             |
| ---- | ---------------- |
| wd   | 微端ev           |
| wx   | 微信小游戏ev     |
| op   | oppo小游戏ev     |
| qq   | qq小游戏ev       |
| zj   | 字节跳动小游戏ev |

### 更新ev

请求示例

```json
http://192.168.0.246/mastern/client/upEv.admin?t=wd&v=1

```

| 参数 | 涵义                                                         |
| ---- | ------------------------------------------------------------ |
| t    | 类型(目前仅支持{wd（微端）,wx（微信小游戏）,op（oppo小游戏）,qq（qq小游戏）,zj（字节跳动小游戏）}) |
| v    | 版本号                                                       |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": {}
        }, 
        "noLogin": false, 
        "noRight": false
    }
}

```

### 更新通用gv

请求示例

```json
http://192.168.0.246/mastern/client/upGv.admin?v=1

```

| 参数 | 涵义   |
| ---- | ------ |
| v    | 版本号 |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false
        "noRight":false
    }
}

```

### 查看通用gv

请求示例

```json
http://192.168.0.246/mastern/client/viewGv.admin

```

| 参数 | 涵义   |
| ---- | ------ |
| v    | 版本号 |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": {
            "client": {
                "gv": "1"
            }
        }, 
        "noLogin": false, 
        "noRight": false
    }
}

```

| 参数 | 涵义   |
| ---- | ------ |
| gv   | gv版本 |

### 添加区间gv

请求示例

```json
http://192.168.0.246/mastern/client/addSgv.admin?pf=7000004&sgv=20001:1;20002-20005:2

```

| 参数 | 涵义                                                         |
| ---- | ------------------------------------------------------------ |
| pf   | 平台name                                                     |
| sgv  | 版本号希望添加个提示让运维按照我的格式填写格式内容为（20001 gv版本为xx 20002-20005 gv版本为gv版本yy 格式为： 20001:xx;20002-20005:yy ） |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false
        "noRight":false
    }
}

```

### 修改区间gv

请求示例

```json
http://192.168.0.246/mastern/client/upSgv.admin?pf=7000004&sgv=20001:1;20002-20005:3

```

| 参数 | 涵义                                                         |
| ---- | ------------------------------------------------------------ |
| pf   | 平台name                                                     |
| sgv  | 版本号希望添加个提示让运维按照我的格式填写格式内容为（20001 gv版本为xx 20002-20005 gv版本为gv版本yy 格式为： 20001:xx;20002-20005:yy ） |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false
        "noRight":false
    }
}

```

### 查看区间gv

请求示例

```json
http://192.168.0.246/mastern/client/viewSgv.admin

```

| 参数 | 涵义   |
| ---- | ------ |
| v    | 版本号 |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": {
            "client": {
                "sgv": {
                    "7000004": "20001:1;20002-20005:3"
                }
            }
        }, 
        "noLogin": false, 
        "noRight": false
    }
}

```

| 参数 | 涵义          |
| ---- | ------------- |
| sgv  | 区间版本的map |

### 删除区间gv

请求示例

```json
http://192.168.0.246/mastern/client/delSgv.admin?pf=7000004

```

| 参数 | 涵义     |
| ---- | -------- |
| pf   | 平台name |

成功返回示例

```json
{
    "data": {
        "callback": true, 
        "data": { }, 
        "noLogin": false
        "noRight":false
    }
}

```