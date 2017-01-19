# git 合并多次commit

1. 首先使用git log查看提交历史
	![GitHub set up](http://ofoygdb8c.bkt.clouddn.com/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202016-12-30%2017.41.15.png)

2. git 压缩 git rebase -i HEAD~4
该命令执行后，会弹出一个编辑窗口，4次提交的commit倒序排列，最上面的是最早的提交，最下面的是最近一次提交。
当前我们只要知道 pick 和 squash 这两个命令即可。
	•	pick 的意思是要会执行这个 commit
	•	squash 的意思是这个 commit 会被合并到前一个commit
	修改第2-4行的第一个单词pick为squash,然后输入:wq以保存并退出.
	![GitHub set up](http://ofoygdb8c.bkt.clouddn.com/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202016-12-30%2017.50.40.png)
	
3. 这是我们会看到 commit message 的编辑界面,其中, 非注释部分就是两次的 commit message, 你要做的就是将这两个修改成新的 commit message。
	![GitHub set up](http://ofoygdb8c.bkt.clouddn.com/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202016-12-30%2017.50.53.png)

4. 输入wq保存并推出, 再次输入git log查看 commit 历史信息，你会发现这4个 commit 已经合并了。
	 ![GitHub set up](http://ofoygdb8c.bkt.clouddn.com/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202016-12-30%2017.51.50.png)



