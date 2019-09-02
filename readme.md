我默认你们都能在官网下载到tinymce，鉴于部分同学是通过npm安装的，要注意了：npm安装的不行！！！！不能用powerpaste！！！！
要用这个插件，先从官网下载tinymce！！下载地址：https://www.tiny.cloud/get-tiny/self-hosted/
语言包下载：[https://www.tiny.cloud/get-tiny/language-packages/](https://www.tiny.cloud/get-tiny/language-packages/)

然后，把我给你们发的插件解压
解压后我们放到tinymce模块的plugins文件夹下。放进去后的tinymce文件夹长这样
![tinymce目录](https://upload-images.jianshu.io/upload_images/2626329-5130e0b35c771422.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

然后！在你webpack的index.html中，通过script标签引入tinymce.min.js！你不是用webpack也没关系，反正通过标签引入就是了！

![script标签引入](https://upload-images.jianshu.io/upload_images/2626329-1591d0d2392c2244.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
这样说已经够明白了吧！还是看不懂的同学，打赏支持下吧

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




### 更新3.3.3-308版本
地址链接: https://pan.baidu.com/s/1LbqcDFx_jRv_wg94coVIsw 
据我初步观察有以下不同：
1 修复了第一次复制粘贴图片进入tinymce时，images_upload_handler会调用2次的bug
2 word中如有图片无法上传（比如图片格式错误，word中可以显示但是tinymce无法显示）增加了错误提示
3 体积更小，大概小了30%
4 猜测：应该与高版本tinymce兼容的更好。因为2.1.10-115是2017年初时候的版本了，那时候对应tinymce3.x，现在是tinymce4.9
这个版本在官网上的售价（请支持正版。买self-host!!!）
![image.png](https://upload-images.jianshu.io/upload_images/2626329-666343aed44fe5f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 更新4.0.1-317版本  适用tinymce5.0以上！！！
地址连接：https://pan.baidu.com/s/1EoXsbHOy-qk-q7VfnT8BVw
![4.0.1-317](https://upload-images.jianshu.io/upload_images/2626329-cad1c453c618aaf2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



大家随便打赏一点，我想得到简书钻，冲排名！谢谢！

safari11版本以上不支持powerpaste，请各位注意。