* [参考](https://wangdoc.com/javascript/bom/file.html)
1. Filed对象
  * 代表一个文件，用来读取文件信息。它继承了Blob对象，或者说是一种特殊的blob对象。
  * 最常见的使用场合是表单的文件上传控件（\<input type="file">），用户选中文件以后，浏览器就会生成一个数组，里面是每一个用户选中的文件，它们都是 File 实例对象。
  ```javascript
    // HTML 代码如下
    // <input id="fileItem" type="file">
    var file = document.getElementById('fileItem').files[0];
    file instanceof File // true
  ```
  * 构造函数
      * 浏览器提供原生的构造函数，生成File实例。
      > new File(array,name,option)
        array:一个数组，成员可以是二进制对象或字符串，表示文件内容。
        name:字符串，表示文件名或文件路径
        option:可选，配置对象，设置实例属性。1，type：字符串，表示对象的MIME类型，默认空字符串；2，lastModified：表示上传修改的时间，默认Data.now();
      ```javascript
          eg:
          var file = new File(
            ['foo'],
            'foo.txt',
            {
              type: 'text/plain',
            }
          );
      ```
  * File对象的实例属性和方法
       * File.name
       * File.size
       * File.type
       * File.lastModified
       * File没有自己的实例方法，但是因为继承了Blob，所以可以用Blob的实例方法slice()
2. FileList对象
  * 一个类似数组的对象，代表一组选中的文件，每个成员都是File实例。它主要出现在两个场合：
     * 文件控制节点\<input type="file">的files属性。返回一个FileList实例.
     * 拖拉一组文件时，目标区的DataTransfer.files属性。返回一个FileList实例。
     ```javascript
       // <input id="a" type="file">
       var files=document.getElementById("a").files;
       files instanceof FileList //true
     ```
     * FileList 的实例属性主要是length，表示包含多少个文件。
     * FileList 的实例方法主要是item()，用来返回指定位置的实例。它接受一个整数作为参数，表示位置的序号（从零开始）。但是，由于 FileList 的实例是一个类似数组的对象，可以直接用方括号运算符，即myFileList[0]等同于myFileList.item(0)，所以一般用不到item()方法。
3. FileReader对象
  * 用于读取File对象或者Blob对象包含的文件内容
  * 浏览器提供一个原生的FileReader对象，用来生成FileReader实例。
  * FileReader的实例属性：
       * FileReader.error：读取文件产生的错误对象
       * FileReader.readyState：整数，表示读取文件的当前状态，0表示未读取，1表示正读取，2表示读取完成
       * FileReader.result：读取完成后的文件内容，有可能是字符串，有可能是ArrayBuffer实例
       * FileReader.onabort:abort事件(用户终止读取操作)的监听函数
       * FileReader.onerror:error事件(读取出错)的监听函数
       * FileReader.onload:load事件(读取操作完成)的监听函数，通常在这个事件里使用result属性，读取文件内容
       * FileReader.onloadstart：load事件(读取操作开始)的监听函数
       * FileReader.onloadend:load事件(读取操作完成)的监听函数
       * FileReader.onprogress:load事件(读取操作进行中)的监听函数
  ```javascrapt

   // HTML 代码如下
   // <input type="file" onchange="onChange(event)">

   function onChange(event) {
     var file = event.target.files[0];
     var reader = new FileReader();
     reader.onload = function (event) {
       console.log(event.target.result)
     };

     reader.readAsText(file);
   }
  ```
  * ReaderFile有下列实例方法：
      * ReaderFile.abort():终止读取操作，readyState变为2.
      * ReaderFile.readAsArrayBuffer():以ArrayBuffer的格式读取文件，读取完后，result属性返回一个ArrayBuffer实例。
      * ReaderFile.readAsBinaryString():读取完后，result将返回原始的二进制字符串。
      * ReaderFile.readAsDataURL:读取完后，result将返回一个Data URL格式<BASE 64编码>的字符串，代表文件内容。对于图片文件，这个字符串可以用于<img>元素的src属性。注意，这个字符串不能直接进行 Base64 解码，必须把前缀data:*/*;base64,从字符串里删除以后，再进行解码。
      * ReaderFile.readAsText():读取完后，result属性将返回文件内容的文本字符串。该方法的第一个参数是代表文件的 Blob 实例，第二个参数是可选的，表示文本编码，默认为 UTF-8。
  ```javascript
   eg:
    /* HTML 代码如下
      <input type="file" onchange="previewFile()">
      <img src="" height="200">
    */

    function previewFile() {
      var preview = document.querySelector('img');
      var file    = document.querySelector('input[type=file]').files[0];
      var reader  = new FileReader();

      reader.addEventListener('load', function () {
        preview.src = reader.result;
      }, false);

      if (file) {
        reader.readAsDataURL(file);
      }
    }
  ```
