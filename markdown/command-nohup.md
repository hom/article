1. `zsh`执行
```bash
$ nohup node index &
```
2. 提示
```bash
zsh: you have running jobs
```
3. 解决办法
```bash
#在命令结尾添加!
$ nohup node index &!
#或者给相关的任务id添加disown
$ disown %1
```
4. 参考  
[Exiting terminal running “nohup ./my_script &” => “You have running jobs”. OK to exit?](https://unix.stackexchange.com/questions/231316/exiting-terminal-running-nohup-my-script-you-have-running-jobs-ok-to)