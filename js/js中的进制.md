## 2进制

- 以0b开头

```javascript
console.info(0b11); //3
```

## 8进制

- 以0开头的视为8进制，无效数字视为10进制
- 以0o开头的视为8进制

```javascript
console.info(011)//9
console.info(080)//80
console.info(0o11)//9
console.info(0o80)//报错
```

## 16进制

- 以0x卡头

```javascript
console.info(0x11); //17
```

## 进制转换的几种方式
1. toString(radix)方法
```javascript
(255).toString(2);    // "11111111"  二进制
(255).toString(8);    // "377"       八进制
(255).toString(16);   // "ff"        十六进制
```
2. parseInt(str,radix)：将某个进制视为radix进制并转换为10进制的数据返回
```javascript
	parseInt("11111111", 2);   // 255
  parseInt("377", 8);        // 255
  parseInt("ff", 16);        // 255
 //组合使用就可以实现任意进制的转换
 // 二进制 → 十六进制
  parseInt("11111111", 2).toString(16);   // "ff"
``` 