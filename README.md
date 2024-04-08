vscode服务器后台训练的一些指令
1.启动后台训练
可以使用nohup命令和&符号来执行你的Python脚本。这两个工具通常用于在后台运行进程，并确保进程在终端关闭后继续运行。下面是如何修改你的命令以使用nohup和&，以确保你的训练进程在退出VSCode后仍然运行：
nohup python train_net.py --config-file ./configs/faster_rcnn_res50_visdrone.yaml --num-gpus 1 SOLVER.IMS_PER_BATCH 2 > train_log.txt 2>&1 &
即nohup python xxx(你要执行的代码) > train_log.txt 2>&1 &

nohup：用于运行命令，使命令在用户注销或终端关闭时继续运行。
> train_log.txt：将标准输出重定向到train_log.txt文件中，你可以自定义文件名。这样做可以保存训练过程中的所有输出，便于以后查看。
2>&1：将标准错误重定向到标准输出，这意味着你的错误消息和正常消息都会被记录到同一个文件中。
&：将命令放到后台执行。

2.通过查看train_log.txt文件来检查训练过程的输出和进度
tail -f train_log.txt

3.查找进程ID（PID）： 使用下面的命令来找出所有Python进程的列表，从中找到你的训练进程。训练进程通常可以通过它的命令行参数（比如你的训练脚本的名称）来识别。
ps -ef | grep python

4.终止进程： 一旦找到你的训练进程的PID
比如root      101376  101198 17 17:46 ?        00:03:32 python train_net.py --config-file ./configs/faster_rcnn_res50_visdrone.yaml --num-gpus 1 SOLVER.IMS_PER_BATCH 2

101376为训练进程的PID
终止进程：
kill 101376

强制终止进程：
kill -9 101376

