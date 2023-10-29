## FormData.append方法和FormData.set方法区别
1. 添加数据方式不同：append方法用于向FormData对象中添加表单字段数据，而set方法用于设置请求头的键值对
2. 处理重复键名不同：append方法可以处理具有相同键名的多个字段，将它们作为数组传递，而set方法会覆盖之前设置的相同的键名的值
