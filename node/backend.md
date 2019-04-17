###  分层

1. Web层(接受与发送http请求,封装  也叫controller层)LoginController

 　　　作用:

 　　　1、用户权限校验
 
　　　 2、数据预校验和预处理

 　　　3、数据预校验后的用户提示

 　　　4、对下一层处理结果的判断处理以及合适的用户提示

2. 业务逻辑层(服务层,  文件通常以XXXService)LoginService

　　　作用

　　　1、业务逻辑判断与处理

　　　2、数据库层的交互

　　　3、将业务结果进行标准化处理后返回（状态码，状态值，返回值）

3. DAO层LoginDAO

　　　　DataBase(DB)：存数据

　　　　作用:

　　　　对对象进行操作

　　　　如果要存储:对象转化为数据

　　　　如果要读取:数据转化为对象　

4. 持久层:存在磁盘里（这个不需要单独存在一个文件）

　　　　文件,数据库(MySql,Oracle,MongoDB)

5. Domain  user  实体对象