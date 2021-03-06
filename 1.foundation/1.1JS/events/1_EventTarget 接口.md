1. Dom的事件操作(监听和触发)，都定义在EventTarget接口。所有节点对象都部署了这个接口，其他一些需要事件通信的
   浏览器内置对象,[如：XMLHTTPRequest、AudioNode、AudioContext]也部署了这个接口。
   * 该接口主要提供三个实例方法：
       * addEventListener:绑定事件的监听函数
       * removeEventListener:移除事件的监听函数
       * dispatchEvent：触发事件
2. addEventListener()
    * EventTarget.addEventListener()用于在当前结点或对象上，定义一个特定事件的监听函数，一旦这个事件发生就会触发监听函数。该方法没有返回值。
    * 参数：
          * type:事件名称，大小写敏感。
          * listener：监听函数。
          * useCapture：布尔值，表示监听函数是否在捕获阶段（capture）触发，（监听函数只在冒泡阶段被触发）。该参数可选。默认为false。
         ```javascript
              function hello() {
                console.log('Hello world');
              }
              var button = document.getElementById('btn');
              button.addEventListener('click', hello, false);
         ```
         * 参数的注意事项：
            1. 第二个参数除了监听函数，还可以是一个具有handleEvent方法的对象。
              ```javascript
               buttonElement.addEventListener('click', {
                 handleEvent: function (event) {
                   console.log('click');
                 }
               });
              ```
            2. 第三个参数除了布尔值useCapture，还可以是一个属性配置对象。该对象有以下属性。
               * capture：布尔值，表示该事件是否在捕获阶段触发监听函数。
               * once：布尔值，表示监听函数是否只触发一次，然后就自动移除。
               * passive：布尔值，表示监听函数不会调用事件的preventDefault方法。如果监听函数调用了，浏览器将忽略这个要求，并在监控台输出一行警告。
               ```javascript
                element.addEventListener('click', function (event) {
                  // 只执行一次的代码
                }, {once: true});
    * addEventListener方法可以为针对当前对象的同一个事件，添加多个不同的监听函数。这些函数按照添加顺序触发，即先添加先触发。如果为同一个事件多次添加同一个监听函数，该函数只会执行一次，多余的添加将自动被去除（不必使用removeEventListener方法手动去除）。
    * 如果希望向监听函数传递参数，可以用匿名函数包装一下监听函数。
      ```javascript
        function print(x) {
          console.log(x);
        }

        var el = document.getElementById('div1');
        el.addEventListener('click', function () { print('Hello'); }, false);
      ```
    * 监听函数内部的this，指向当前事件所在的那个对象。
      ```javascript
        // HTML 代码如下
        // <p id="para">Hello</p>
        var para = document.getElementById('para');
        para.addEventListener('click', function (e) {
          console.log(this.nodeName); // "P"
        }, false);
        //this指向事件所在的对象para
      ```
3. EventTarget.removeEventListener()
    * 用来移除addEventListener方法添加的事件监听函数。该方法没有返回值。
    * removeEventListener方法的参数，与addEventListener方法完全一致。它的第一个参数“事件类型”，大小写敏感。
    * 注意，removeEventListener方法移除的监听函数，必须是addEventListener方法添加的那个监听函数，而且必须在同一个元素节点，否则无效
    * 匿名函数无法移除监听函数

4. EventTarget.dispatchEvent()
    * 在当前节点上触发指定事件，从而触发监听函数的执行。该方法返回一个布尔值，只要有一个监听函数调用了Event.preventDefault()，则返回值为false，否则为true。
    * dispatchEvent方法的参数是一个Event对象的实例。
    ```javascript
        para.addEventListener('click', hello, false);
        var event = new Event('click'); // document.createEvent("");
        para.dispatchEvent(event);
        //在当前节点触发了click事件
    ```
    * 如果dispatchEvent方法的参数为空，或者不是一个有效的事件对象，将报错