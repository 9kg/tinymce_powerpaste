### 使用说明

#### 我默认你们都能在官网下载到tinymce，鉴于部分同学是通过npm安装的，要注意了：npm安装的不行！！！！不能用powerpaste！！！！
#### 要用这个插件，先从官网下载tinymce！！下载地址：https://www.tiny.cloud/get-tiny/self-hosted/
#### 语言包下载：[https://www.tiny.cloud/get-tiny/language-packages/](https://www.tiny.cloud/get-tiny/language-packages/)

#### tinymce 大版本4，对应powerpaste-3.3.3-308, 大版本5对应4.0.1-317


将powerpaste放入tinymce模块的plugins文件夹下。放进去后的tinymce文件夹长这样
![tinymce目录](https://upload-images.jianshu.io/upload_images/2626329-5130e0b35c771422.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

然后！在你webpack的index.html中，通过script标签引入tinymce.min.js！你不是用webpack也没关系，反正通过标签引入就是了！

![script标签引入](https://upload-images.jianshu.io/upload_images/2626329-1591d0d2392c2244.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接着tinymce初始化时


      tinymce.init({
        selector: '#tinymce', // css选择器，和jquery的选择器一个道理，建议直接用id
        language: 'zh_CN', // 需要在官网自己下载一个全局的langs包。同时我提供的powerpaste本身自带一个langs包里面含中文，所以可以100%支持中文。
        plugins: [
          'powerpaste', // plugins中，用powerpaste替换原来的paste
          //...
        ],
        powerpaste_word_import: 'propmt',// 参数可以是propmt, merge, clear，效果自行切换对比
        powerpaste_html_import: 'propmt',// propmt, merge, clear
        powerpaste_allow_local_images: true,
        paste_data_images: true,
        images_upload_handler: function (blobInfo, success, failure) {
          // 这个函数主要处理word中的图片，并自动完成上传；
          // ajaxUpload是自己定义的一个函数；在回调中，记得调用success函数，传入上传好的图片地址；
          // blobInfo.blob() 得到图片的file对象；
          ajaxUpload(blobInfo.blob()).then((data) => {
             // 上传成功后，调用success函数传入图片地址
             success(data.uploadedImageUrl)
           })
         },
        // tinymce的其他配置参数
      })

你可以进一步封装成组件等，但已经不是本文讨论的范畴了。

[效果预览]
![image.png](https://upload-images.jianshu.io/upload_images/2626329-71dc2d2dd1b4f338.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)




safari11版本以上不支持powerpaste，请各位注意。