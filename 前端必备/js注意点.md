- try-catch不能够捕获异步错误，例如:
```javascript
function asyncOperation() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      try {
        throw new Error("Error inside promise");
      } catch (err) {
        // This won't be reached
        console.error("Caught error inside promise:", err); 
      }
      resolve("Success");
    }, 1000);
  });
}
```
