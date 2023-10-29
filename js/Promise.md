## Promise.all
等待所有的promise完成，如果有一个失败就立即失败
## Promise.any
只需要等待一个promise完成，如果所有的promise失败了则返回失败
### Promise.race
返回最先完成的promise，只要第一个promise状态不再是pending，Promise.race就会结束
