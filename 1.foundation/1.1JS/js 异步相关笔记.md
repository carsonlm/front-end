1. async/await 处理异步： [可参考阮一峰](http://www.ruanyifeng.com/blog/2015/05/async.html)
   * 和Generate函数一样，async异步函数会返回一个Promise。【如果有一个返回值，内部会调用Promise.solve()方法把它转为一个promise对象返回，
              如果函数内部抛出错误，则会调用Promise.reject()方法返回一个promise对象。】；返回成功用then()方法处理，返回出错用catch()方法处理。
   ```javascript
     async function timeout() {
         return '2'
     } []( []( []( []( []( []( []() ) ) ) ) ) )
     timeout().then(result => {
         console.log(result);
     })
     console.log('1');
    //1
    //2
   ``` 
   * await 表示等待，后面可以接任何表达式。更多是放一个返回Promise对象的表达式。
       * async 会将其后的函数（函数表达式或 Lambda）的返回值封装成一个 Promise 对象，而 await 会等待这个 Promise 完成，并将其 resolve 的结果返回出来。
       
       
   * **async/await的优势在于处理then()链** Promise通过then链来解决多层回调的问题，现在又用 async/await 来进一步优化它
   ```javascript
   eg:
        function takeLongTime(n) {
            return new Promise(resolve => {
                setTimeout(() => resolve(n + 200), n);
            });
        }
        function step1(n) {
            console.log(`step1 with ${n}`);
            return takeLongTime(n);
        }
        function step2(n) {
            console.log(`step2 with ${n}`);
            return takeLongTime(n);
        }
        function step3(n) {
            console.log(`step3 with ${n}`);
            return takeLongTime(n);
        }
     //Promise的处理方式
          function doIt() {
              console.time("doIt");
              const time1 = 300;
              step1(time1)
                  .then(time2 => step2(time2))
                  .then(time3 => step3(time3))
                  .then(result => {
                      console.log(`result is ${result}`);
                      console.timeEnd("doIt");
                  });
          }
          doIt();
          // c:\var\test>node --harmony_async_await .
          // step1 with 300
          // step2 with 500
          // step3 with 700
          // result is 900
          // doIt: 1507.251ms
     // async/await方式实现  
          async function doIt() {
              console.time("doIt");
              const time1 = 300;
              const time2 = await step1(time1);
              const time3 = await step2(time2);
              const result = await step3(time3);
              console.log(`result is ${result}`);
              console.timeEnd("doIt");
          }
          doIt();
   ```