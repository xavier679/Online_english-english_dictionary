	client : 客户端
		cli.h :头文件
		包含：
			void length(char *buf);//检测输入的是数字和密码,但是长度1-15,第一个开头是小写字母或则大些字母.
			
			void deal_with_recv_and_send(int ret); //判断recv和send 接受或发送情况
			
			void print_word_information();//打印查询单词操作说明 

			void print_user_opration();//打印用户注册说明

			
			void deal_with_regist(int connfd,STAT * cmd); //用来判断recv和send函数接受情况
			
			
			int deal_with_login(int connfd,STAT *cmd);//注册函数,如果用户名重复就重新注册
			
			void  deal_with_query(int connfd,STAT *cmd);//查找单词
			
			
			void deal_with_history(int connfd,STAT * cmd);//查看用户的历史情况.

		main_cli.c//客户端主函数

		main_cli_fun.c//第一层功能：注册，登陆，退出

						   //第二层功能：查询单词，查询历史记录，退出


	server : 服务器
		ser.h :头文件
			包含:
			
			extern void deal_with_recv_and_send(int ret);//处理 recv和send 发送失败
			
			extern void deal_with_sqlite3_option(int ret,char *errmsg);//处理sqlite3函数操作失败
			  
			 extern void regist(int connfd,STAT *cmd, sqlite3 *db);//注册
			
			extern int login(int connfd,STAT *cmd,sqlite3 *db);//登录
			
			extern void get_date(char *data);//获取时间
			
			extern int query(int connfd,STAT *cmd,sqlite3 *db);//查询单词
			
			extern int  history(int connfd,STAT *cmd,sqlite3 *db);//历史记录
			
			
			 extern void *function(void *arg); //线程函数 功能 查询功能函数
		main_ser.c//服务器主体 包含：function线程接口;
		main_ser_fun.c //功能函数的实现

	dict.db :这个文件包括翻译的词典,用户注册的信息,用户历史记录.
	
	copy_test_to_sqlite3_db.c 转化txt格式字典为数据库字典表

	具体操作:
	编译opy_test_to_sqlite3_db.c，执行./a.out
	执行make，然后先运行服务器（ser），在执行客户端（cli）

