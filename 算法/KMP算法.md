KMP算法是一种字符串匹配算法，可以在O(n+m)的时间复杂度内实现两个字符串的匹配，而使用暴力的时间复杂度是O(m*n)
假设主串为S，正比较的下标为i,模式串为T,正比较的下标为j,(注意j的开始下标是从1开始的)因为暴力解法每次都是回溯了i，而KMP的做法就是让i不回溯，如果不匹配，每次改变的都是j的值，而j的值就是对应的next[j],KMP的核心部分就是求取next数组的值
## 如何使用next数组？

- 从主串和模式串的第pos个字符开始进行比较,j=1
- 如果字符相等，继续逐个比较后续字符，i++,j++
- 如果j==0,(j=next[j]=0)这表示模式串的第一个字符和T[i]匹配不成功，则应该i++,j++
- 如果两个字符不相等，主串位置i不发生变化，j=next[j],然后比较S[i]和T[j]
## 何时匹配成功?

1. 如果匹配成功(j>S.len)，返回模式串第一个字符相对应在主串中的序号，return i-S.len
2. 如果匹配不成功，返回-1

## next的计算思想
![image.png](https://cdn.nlark.com/yuque/0/2022/png/29486774/1670157171348-5441429d-6d14-4704-89ad-772b2b07db28.png#averageHue=%23fbfbf5&clientId=u6dd3dd73-20d5-4&from=paste&height=222&id=uf871cf41&originHeight=333&originWidth=1053&originalType=binary&ratio=1&rotation=0&showTitle=false&size=138685&status=done&style=none&taskId=ua15cb47a-06fb-4ca4-b052-8486b4c46cc&title=&width=702)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/29486774/1670157297010-821b348c-0ff2-400b-bc1b-e5eceff55b3d.png#averageHue=%23fafbf5&clientId=u6dd3dd73-20d5-4&from=paste&height=386&id=u8dab6d3e&originHeight=579&originWidth=905&originalType=binary&ratio=1&rotation=0&showTitle=false&size=265990&status=done&style=none&taskId=ue3edd727-dfd0-4739-9552-b43d84cf83b&title=&width=603.3333333333334)
也就是说真前缀和真后缀的值要尽可能大，这样移动的模式串移动的距离就是最远的
所以求next数组的值只需要通过模式串就可以计算
![image.png](https://cdn.nlark.com/yuque/0/2022/png/29486774/1670157610629-6a5d1ea8-8e68-432b-a1bb-1db7e7bf972d.png#averageHue=%23f6f7f5&clientId=u6dd3dd73-20d5-4&from=paste&height=427&id=uf4a57422&originHeight=641&originWidth=1216&originalType=binary&ratio=1&rotation=0&showTitle=false&size=331539&status=done&style=none&taskId=u567791e0-b459-4724-bb13-979fe4032e7&title=&width=810.6666666666666)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/29486774/1670158428694-d742b1a3-4894-4886-9798-12d03db9516e.png#averageHue=%23f7f7f4&clientId=u6dd3dd73-20d5-4&from=paste&height=413&id=u6e109c0d&originHeight=620&originWidth=941&originalType=binary&ratio=1&rotation=0&showTitle=false&size=289069&status=done&style=none&taskId=u176e5215-cb4e-4d06-b67d-25cfa78283e&title=&width=627.3333333333334)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/29486774/1670163081220-a12e4509-4715-4de4-bef8-d2eba8fa2c86.png#averageHue=%23faf7f0&clientId=u6dd3dd73-20d5-4&from=paste&height=383&id=uec39808f&originHeight=574&originWidth=735&originalType=binary&ratio=1&rotation=0&showTitle=false&size=197066&status=done&style=none&taskId=uc556fa2a-fe3f-4932-ada2-e15b5100852&title=&width=490)
