定时任务
###### **sudo crontab -e** 
- 选择vim编译器，进入蓝色页面
- 分 时 日 月 周
- `* * * * *`
`/`表示时间间隔
-表示连续
，表示不连续
> `* 2,4 * * *`每天的2，4点
> `* 2-4 * * *` 每天的2~4点
> ![[file-20240903084302067.png]]
![[file-20240902123003307.png]]

>  - 查看任务是否成功执行
>  **ps -ef |grep cron** 
>  如果为**cron -f** 代表正在执行
>  - **service cron** 开启服务
>  - **tail -f /1.txt**（路径） 来动态监测文件的变化
>  - 关闭服务 **service cron stop** 