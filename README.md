![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 关于在SQL中创建ModifedDate列的基本方法
### Basic Way To Create ModifedDate Column In SQL
**发布-日期: 2018年01月19日 (评论)**

![#](images/create-modified-date-column-in-sql.png?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
这是为一些表创建[ModifedDate]列的基本方法。通常，每当你创建一个会进行各种更新和修改的表时，你需要为[CreateDate]和[ModifedDate]添加经典列。

在这个例子中，我正在调用的基本表[Standard_Rules_00]基本上是可以存储我的一些自定义构建或修改脚本的地方。



## English
Here’s a basic way to create the [ModifedDate] column for some of your tables. Often times whenever you create a table that will undergo various updates and modifications; you’ll find yourself wanting to add the classic columns for [CreateDate] and [ModifedDate].
In this example; I have a basic table I’m calling [Standard_Rules_00] which is basically a place where I can store some of my custom build, or modification scripts.


---
## Logic
```SQL

use [compliance];
set nocount on
 
create table [STANDARD_RULES_00]
(
    [lineid]    	int identity(1,1)
,   [createdate]    datetime null
,   [statements]    varchar(max)
,   [modifieddate]  datetime null
,   [description]   varchar(max)
)
go
 
create trigger trig_post_insert
on [dbo].[STANDARD_RULES_00]
after insert
as
begin
    update [dbo].[STANDARD_RULES_00]
    set [createdate] = getdate()
    from dbo.[STANDARD_RULES_00] sr
    where exists (select 1 from inserted i where i.[lineid] = sr.[lineid]);
end
go
 
create trigger trig_post_update
on [dbo].[STANDARD_RULES_00]
after update
as
begin
    update [dbo].[standard_rules_00]
    set [modifieddate] = getdate()
    from dbo.[STANDARD_RULES_00] sr
    where exists (select 1 from inserted i where i.[lineid] = sr.[lineid]);
end
go

```



[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

