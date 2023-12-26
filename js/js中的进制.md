## 2进制
- 以0b开头
```javascript
console.info(0b11)//3
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
##  16进制
- 以0x卡头
```javascript
console.info(0x11)//17
```