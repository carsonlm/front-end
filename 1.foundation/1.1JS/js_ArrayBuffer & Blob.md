1. ArrayBuffer 表示一段二进制数据，用来模拟内存里面的数据，通过这个对象js可以读写二进制数据。
  * 浏览器原生提供ArrayBuffer构造函数来生成实例，需要一个整数参数，表示二进制数据占的字节。
  ```javascript
     var ab=new ArrayBuffer(8);
  ```
  * 它有两个实例属性length和byteLength.都表示内容长度
  * 实例方法slice(),用来复制内存，接受两个参数，表示复制开始和结束（不包括结束），结束参数省略则表示复制到结束。

2. Blob 表示一个二进制文件的数据内容，通常用来读写文件。
  * 构造函数：第一个参数是数组，成员是字符串或二进制对象，表示新生成的Blob实例对象的内容；第二个参数可选，是一个配置对象，目前就一个type属性，表示MIME类型，默认空字符串。
  ```javascript
     var s=[''<a id="a"><b id="b">hey!</b></a>'']
     var blob=new Blob(s,{type:'text/heml'})

     //保存json数据
     obj={hello:'world'}
     var blob=new Blob([JSON.stringify(obj)],{type:'application/json'})
  ```
  * Blob的实例属性：size和type
  * Blob实例方法slice(),复制原来的数据，返回的也是一个Blob实例
      * Blob.slice(start,end,contentType) 前两个参数同上，第三个表示新实例的数据类型，默认为空字符串