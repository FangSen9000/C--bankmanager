# C#-bankmanager
A bank management system written in C # language

## 设计说明书


班    级   2020级中澳计科2班
组    长  2024030139 蔡静雯
小组成员   2024030107 房森
          2024030006 马俊杨
指导教师   侯彦娥



2022   年  12  月  20  日
 
 
## 目录

1 系统功能说明	
2 小组人员分工	
3 系统设计	
4 数据库结构	
5 页面运行截图及描述	

 
1 系统功能说明
 
该银行账户管理系统实现的基本功能有：登录。开户、存款、取款；当日汇总，汇总查询。职员管理，工资调整；更改账户密码，更改操作员密码。利率设置。系统帮助页面。
实现的拓展功能有：打印单据、基金管理
2 小组人员分工
蔡静雯：开户、存款、取款，系统帮助，拓展功能-基金管理
房森：当日汇总、汇总查询、打印单据
马俊杨：职员管理、调整工资
 
3 系统设计
该系统的主要功能是为用户办理开户、存/取款业务,管理每个用户的信息,生成资金明细，工作人员登陆系统后，可以查看用户的信息、修改用户的信息、查看用户的余额。
	存款取款：
开户：为用户开户
账户名：不能为空
身份证号：长度必须为18位
密码：长度为6位的数字
开户类型：有"活期存款", "定期存款一年", "定期存款三年", "定期存款五年", "零存整取一年", "零存整取三年", "零存整取五年"供用户选择。

开户金额：大于等于0
将用户信息保存到数据库中
存款：向账户存款
      判断存款金额，必须大于0。
判断账户类型，活期账户存款无限制，定期账户在定期期限内不能存款，零存整取账户在期限内存款次数不能超过12/36/60次。
取款：从账户取款
所有账户都只能取大于等于余额的钱数，活期账户除此之外无限制，定期账户和零存整取账户理论上只能在到期后一次性取完。对于提前/延期取款，利率不同
结息：
活期：利息=账户金额×活期利率×存款年限
定期：
按规定时间存取：利息=账户金额×定期一年/三年/五年年利率×存款年限
超期取款：利息=账户金额×定期一/三/五年年利率×年数 + 账户金额×定期超期年利率×超期时间；
提前支取：结息=账户金额×定期提前支取年利率×存款年限。
零存整取：
按规定时间、次数存取：利息=账户金额×零存整取一年/三年/五年年利率×存款年数
提前支取：利息=单笔存储金额×零存整取违规年利率×单笔金额的存储年数。
存款次数符合规定，超期取款：利息=单笔存储金额×零存整取一/三/五年年利率×单笔存储金额的存款年数+账户金额（含单笔利息）×零存整取超期年利率×超期时间
存款次数不符合规定：利息=单笔存储金额×零存整取违规年利率×单笔存储金额的存储年数；
存款次数不符合规定，超期取款：利息=单笔存储金额×零存整取违规年利率×单笔存储金额的存储年数+账户金额（含单笔利息）×定期超期年利率×超期年数；
	汇总查询：
对汇总查询和单日查询页面分别按账户、处理时间、处理地址、处理金额、
账户余额进行5种查询操作；对查询的结果导出并打印单据
	金融理财：帮助用户了解现阶段的基金情况（收益率、预计收入）
用户输入预计投资的金额，选择不同类型的基金，银行根据所选基金显示收益率，点击计算，系统会帮忙计算出预计年收益。
	职员管理：
	其他功能：
	利率设置：
	系统帮助：
显示一些用户在数据输入时的提示信息，通过点击按钮连接在线客服、了解近期活动、咨询更多业务
4.数据库结构
（1）用户信息表（AccountInfo）：保存银行用户的基本信息。表结构如表4-1所示。
表4-1 用户信息表
字段名称	字段类型	字段含义	备注
accountNo	nchar(6)	用户编号	主键
IdCard	nchar(18)	用户身份证号	
accountName	nvarchar(20)	用户名	
accountPass	nvarchar(20)	用户密码	
accountType	nvarchar(8)	用户类型	

（2）员工信息表（EmployeeInfo）：保存银行职员员工的基本信息。表结构如表4-2所示。
表4-2 员工信息表
字段名称	字段类型	字段含义	备注
EmployeeNo	nchar(5)	员工编号	主键
EmployeeName	Nvarchar(20)	员工姓名	
sex	nchar(1)	员工性别	
workDate	datetime	入职时间	
telephone	nvarchar(11)	手机号码	
idCard	Nchar(18)	身份证号	
Photo	Varbinary(MAX)	员工照片	
		工资	




（3）登录信息表（LoginInfo）：保存登录的基本信息。表结构如表4-3所示。
表4-3 管理员登录信息表
字段名称	字段类型	字段含义	备注
Bno	nchar(5)	账号	主键
Password	nvarchar(20)	密码	
（4）存取款操作信息表（MoneyInfo）：保存银行账户交易的基本信息。表结构如表4-4所示。
表4-4 账户信息表
字段名称	字段类型	字段含义	备注
Id	int	编号	主键
accountNo	nchar(6)	账号	


dealDate
	datatime	操作时间	
dealType	Navrchar(8)	操作类型	
dealMoney
	float	操作金额	
balance	float	账户余额	
（5）利率设置信息表（RateInfo）：保存利率信息。表结构如表4-5所示。
表4-5 利率信息表
字段名称	字段类型	字段含义	备注
rationType	nvarchar(20)	存款类型	主键
rationValue	float	利率	

5 页面运行截图及描述
登录页面

![image](https://user-images.githubusercontent.com/72308243/217994920-63c9296b-e8e1-4f0c-817f-2027251866cc.png)


开户
 
![image](https://user-images.githubusercontent.com/72308243/217994968-aff849ff-fe30-456c-b872-52cbda59a8bc.png)

![image](https://user-images.githubusercontent.com/72308243/217995031-93ef24c7-cd58-4ce7-add6-31cb3bd71b00.png)


存款
 
![image](https://user-images.githubusercontent.com/72308243/217994989-350680cb-d566-4978-a2d8-02e64702d26f.png)

 
 
定期存款
 ![image](https://user-images.githubusercontent.com/72308243/217995009-cc8518f9-bf13-4253-91de-ad2bf925041d.png)


零存整取
 
 
 ![image](https://user-images.githubusercontent.com/72308243/217995065-c1c63c67-3f25-482e-9cb9-d00bc79660b5.png)
 ![image](https://user-images.githubusercontent.com/72308243/217995090-185048b1-a27a-4c65-8977-98a2c16d57cf.png)


取款
 
 
![image](https://user-images.githubusercontent.com/72308243/217995122-2a1d480c-dd0c-4956-ab32-193bc3190291.png)


 ![image](https://user-images.githubusercontent.com/72308243/217995201-6eb703c8-3e89-4750-98c3-ff30772ae640.png)

  


汇总查询：
 
![image](https://user-images.githubusercontent.com/72308243/217995239-3ac659eb-df1b-4dff-a15d-573e9a214dd0.png)

按账户查询
当日汇总
 ![image](https://user-images.githubusercontent.com/72308243/217995254-99b6d8fc-243a-4d8c-ac3d-ee746f1881c7.png)


金融理财
 
基金管理页面
 ![image](https://user-images.githubusercontent.com/72308243/217995334-2a0b7af6-3430-4636-8253-ab9675cc7f80.png)
![image](https://user-images.githubusercontent.com/72308243/217995365-7f329c9c-d479-4c0c-b887-07b0fd3557a4.png)

职员管理
 ![image](https://user-images.githubusercontent.com/72308243/217995378-8479b000-4eac-465c-a0ba-c85c487d8a7c.png)

 职员信息页面

 ![image](https://user-images.githubusercontent.com/72308243/217995387-8d06cccd-c2d3-4956-a4fb-1e6ed1333e8b.png)

更新职员信息

![image](https://user-images.githubusercontent.com/72308243/217995400-efff36c9-b98a-42c0-aca1-fbe4e0642feb.png)

 
调整工资

![image](https://user-images.githubusercontent.com/72308243/217995415-0502a6ec-69df-425b-b04b-36dbd9caba8b.png)

打印单据
 ![image](https://user-images.githubusercontent.com/72308243/217995453-89735ad1-072e-42ae-a7b7-935909df26c9.png)

打印导出查询结果的页面
系统帮助
 
![image](https://user-images.githubusercontent.com/72308243/217995474-5300c967-066e-4482-918a-93a9243bc4ce.png)



