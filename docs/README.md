# OpenCV.js教程

# OpenCV.js简介

## OpenCV.js简介

**OpenCV**

OpenCV由Gary Bradski于1999年在英特尔创建。第一个版本于 2000 年发布。Vadim Pisarevsky加入Gary Bradski，管理英特尔的俄罗斯软件OpenCV团队。2005年，OpenCV被用于斯坦利;赢得2005年DARPA大挑战赛的车辆。后来，在Willow Garage的支持下，它继续积极发展，由Gary Bradski和Vadim Pisarevsky领导该项目。OpenCV现在支持与计算机视觉和机器学习相关的多种算法，并且每天都在扩展。

OpenCV支持多种编程语言，如C++，Python和Java，并且可以在不同的平台上使用，包括Windows，Linux，OS X，Android和iOS。基于 CUDA 和 OpenCL 的高速 GPU 操作接口也在积极开发中。OpenCV.js将OpenCV带到了开放的Web平台，并将其提供给JavaScript程序员。

**OpenCV.js：JavaScript程序员的OpenCV**

Web是最普遍的开放计算平台。随着每个浏览器中实施HTML5标准，Web应用程序能够使用HTML5视频标签呈现在线视频，通过WebRTC API捕获网络摄像头视频，并通过画布API访问视频帧的每个像素。随着大量可用的多媒体内容，Web 开发人员需要 JavaScript 中的各种图像和视觉处理算法来构建创新应用程序。对于Web上的新兴应用程序，例如Web虚拟现实（WebVR）和增强现实（WebAR），这一要求更为重要。所有这些用例都需要在 Web 上高效实现计算密集型视觉内核。

Emscripten是一个LLVM-to-JavaScript编译器。它采用LLVM位码 - 可以使用clang从C / C++生成，并将其编译为asm.js或可以直接在Web浏览器中执行的WebAssembly。.Asm.js 是 JavaScript 的一个高度可优化的低级子集。Asm.js 在 JavaScript 引擎中支持提前编译和优化，提供接近本机的执行速度。WebAssembly是一种新的可移植，大小和加载时间高效的二进制格式，适合编译到Web。WebAssembly旨在以本机速度执行。WebAssembly目前被W3C设计为开放标准。

OpenCV.js 是 Web 平台的选定 OpenCV 函数子集的 JavaScript 绑定。它允许具有多媒体处理功能的新兴Web应用程序从OpenCV中提供的各种视觉功能中受益。OpenCV.js利用Emscripten将OpenCV函数编译为asm.js或WebAssembly目标，并为Web应用程序提供JavaScript API来访问它们。该库的未来版本将利用 Web 上提供的加速 API，例如 SIMD 和多线程执行。

OpenCV.js最初是在加州大学欧文分校（UCI）的并行架构和系统组创建的，是一个由英特尔公司资助的研究项目。OpenCV.js 得到了进一步改进，并作为 Google Summer of Code 2017 计划的一部分集成到 OpenCV 项目中。

**OpenCV.js教程**

OpenCV引入了一组新的教程，这些教程将指导您完成OpenCV.js中可用的各种功能。本指南主要关注OpenCV 3.x版本。

**OpenCV.js教程的目的是：**

帮助 OpenCV 在 Web 开发中的适应性
帮助 Web 社区、开发人员和计算机视觉研究人员以交互方式访问各种基于 Web 的 OpenCV 示例，以帮助他们了解特定的视觉算法。
由于OpenCV.js能够直接在浏览器中运行，因此OpenCV.js教程网页具有直观性和交互性。例如，使用WebRTC API和评估JavaScript代码将允许开发人员更改CV函数的参数，并在网页上进行实时CV编码以实时查看结果。

建议先了解 JavaScript 和 Web 应用程序开发，以便理解本指南。

**贡献**

以下是OpenCV.js绑定和教程的贡献者列表。

Sajjad Taheri（初始版本的架构师和GSoC导师，加州大学欧文分校）
潘聪祥（上海交通大学GSoC学生）
宋刚（上海交通大学GSoC学生）
甘文耀（上海交通大学实习生）
Mohammad Reza Haghighat（英特尔公司项目发起人和赞助商）
胡宁新（英特尔公司学生导师）

# 使用OpenCV.js

## 下载OpenCV.js

在本教程中，您将学习如何在网页中开始使用OpenCV.js。您可以在每个版本中获取副本，或者只需从`https://docs.opencv.org/{版本号}/opencv.js`（例如：[https://docs.opencv.org/3.4.0/opencv.js](https://docs.opencv.org/3.4.0/opencv.js)，如果需要最新版本，请使用）。您还可以按照教程构建 OpenCV.js 构建自己的副本。opencv.jsopencv.jsopencv-{版本号}-docs.zip3.4

## 第一步：创建网页

首先，让我们创建一个能够上传图像的简单网页。

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Hello OpenCV.js</title>
</head>
<body>
<h2>Hello OpenCV.js</h2>
<div>
  <div class="inputoutput">
    <img id="imageSrc" alt="No Image" />
    <div class="caption">imageSrc <input type="file" id="fileInput" name="file" /></div>
  </div>
</div>
<script type="text/javascript">
let imgElement = document.getElementById("imageSrc")
let inputElement = document.getElementById("fileInput");
inputElement.addEventListener("change", (e) => {
  imgElement.src = URL.createObjectURL(e.target.files[0]);
}, false);
</script>
</body>
</html>
```

要运行此网页，请复制上述内容并保存到index.html文件。请使用 Web 浏览器打开即可运行。

?>更好的做法是使用本地 Web 服务器来托管index.html

**同步加载示例：**

<script src=“opencv.js” type=“text/javascript”></script>

您可能希望在 <script> 标记中按属性异步加载。要在准备就绪时收到通知，您可以注册对属性的回调。opencv.js async opencv.js onload

**异步加载示例**

<script async src=“opencv.js” onload=“onOpenCvReady（）;” type=“text/javascript”></script>

## 第二步：使用OpenCV.js

准备就绪后，您可以通过对象访问 OpenCV 对象和函数。`opencv.js``cv`

例如，您可以通过 `cv.imread` 从图像创建 `cv.Mat`。

!>由于图像加载是异步的，因此您需要将 [cv.Mat](https://docs.opencv.org/3.4/d3/d63/classcv_1_1Mat.html) 创建放在回调中。`onload`

```js
imgElement.onload = function（） {
	let mat = cv.imread(mgElement);
}
```

许多OpenCV函数可用于处理[cv.Mat](https://docs.opencv.org/3.4/d3/d63/classcv_1_1Mat.html)。有关详细信息，您可以参考其他教程，例如[图像处理](https://docs.opencv.org/3.4/d2/df0/tutorial_js_table_of_contents_imgproc.html)。

在本教程中，我们只在屏幕上显示一个 [cv.Mat](https://docs.opencv.org/3.4/d3/d63/classcv_1_1Mat.html)。要显示 [cv.Mat](https://docs.opencv.org/3.4/d3/d63/classcv_1_1Mat.html)，您需要一个 canvas 元素。

```html
<canvas id=“outputCanvas”></canvas>
```

您可以使用 [cv.imshow](https://docs.opencv.org/3.4/d7/dfc/group__highgui.html#ga453d42fe4cb60e5723281a89973ee563) 在画布上显示 [cv.Mat](https://docs.opencv.org/3.4/d3/d63/classcv_1_1Mat.html)。

```js
cv.imshow("outputCanvas", mat);
```

将所有步骤放在一起，最终index.html如下所示:

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>Hello OpenCV.js</title>
</head>

<body>
    <h2>Hello OpenCV.js</h2>
    <p id="status">OpenCV.js is loading...</p>
    <div>
        <div class="inputoutput">
            <img id="imageSrc" alt="No Image" />
            <div class="caption">imageSrc <input type="file" id="fileInput" name="file" /></div>
        </div>
        <div class="inputoutput">
            <canvas id="canvasOutput"></canvas>
            <div class="caption">canvasOutput</div>
        </div>
    </div>
    <script type="text/javascript">
        let imgElement = document.getElementById('imageSrc');
        let inputElement = document.getElementById('fileInput');
        inputElement.addEventListener('change', (e) => {
            imgElement.src = URL.createObjectURL(e.target.files[0]);
        }, false);
        imgElement.onload = function () {
            let mat = cv.imread(imgElement);
            cv.imshow('canvasOutput', mat);
            mat.delete();
        };
        var Module = {
            onRuntimeInitialized() {
                document.getElementById('status').innerHTML = 'OpenCV.js is ready.';
            }
        };
    </script>
    <script async src="https://docs.opencv.org/3.4.0/opencv.js" type="text/javascript"></script>
</body>

</html>
```

!>你必须调用[cv.Mat](https://docs.opencv.org/3.4/d3/d63/classcv_1_1Mat.html)的删除方法来释放Emscripten堆中分配的内存。有关详细信息，请参阅 [Emscripten 的内存管理](https://emscripten.org/docs/porting/connecting_cpp_and_javascript/embind.html#memory-management)。

# 图形用户界面功能

在这里，您将学习如何读取和显示图像和视频，并创建跟踪栏。

## 图像入门

学习加载图像并将其显示在 Web 中

OpenCV.js将图像保存为cv.Mat类型。我们使用HTML画布元素将cv.Mat传输到Web或反向传输。ImageData 接口可以表示或设置画布元素区域的基础像素数据。

**首先，从画布创建一个图像数据对象**

```js
let canvas = document.getElementById(canvasInputId);
let ctx = canvas.getContext('2d');
let imgData = ctx.getImageData(0， 0， canvas.width， canvas.height);
```

**然后，使用 cv.matFromImageData 构造一个 cv.Mat：**

```js
let src = cv.matFromImageData(imgData);
```

!>由于画布仅支持具有连续存储的 8 位 RGBA 图像，因此 cv.Mat 类型为 cv.CV_8UC4。它与本机 OpenCV 不同，因为由本机 imread 和 imshow 返回和显示的图像具有按 BGR 顺序存储的通道。

**显示图像**

首先，将 src 的类型转换为 cv.CV_8UC4：

```js
let dst = new cv.Mat();
//比例和移位用于将数据映射到 [0,255]。
src.convertTo（dst, cv.CV_8U, scale,shift）;
//根据 src.channels（） 是 GRAY、RGB 或 RGBA，是 1、3 或 4。
cv.cvtColor（dst，dst，cv.COLOR_***2RGBA）;
```

然后，从 dst 新建一个 ImageData obj：

```js
let imgData = new ImageData（new Uint8ClampedArray(dst.data, dst.cols,dst.rows);
```

最后，显示它：

```js
let canvas = document.getElementById（canvasOutputId）;
let ctx = canvas.getContext（'2d'）;
ctx.clearRect(0, 0,canvas.width, canvas.height);
canvas.width = imgData.width;
canvas.height = imgData.height;
ctx.putImageData(imgData, 0, 0);
```

我们使用`cv.imread（imageSource）`从html画布或img元素中读取图像。

**参数**:imageSource:	画布元素或 ID，或 IMG 元素或 ID。

**返回值：**通道以 RGBA 顺序存储。

我们使用`cv.imshow（canvasSource，mat）`来显示它。该函数可能会缩放mat，具体取决于其深度：

如果 mat 是 8 位无符号的，它将按原样显示。
如果mat 是 16 位无符号或 32 位整数，则像素除以 256。也就是说，值范围 [0，255*256] 映射到 [0，255]。
如果mat 是 32 位浮点数，则像素值乘以 255。也就是说，值范围 [0，1] 映射到 [0，255]。

**参数**:canvasSource：画布元素或 ID。

**mat**：要显示的mat。

上面的图像读取和显示代码可以简化如下：

```js
let img = cv.imread(imageSource);
cv.imshow(canvasOutput, img);
img.delete();
```

**示例**：

```js
let src = cv.imread('canvasInput');
let dst = new cv.Mat();
// 为了区分输入和输出，我们对图像进行了灰度处理
// 您可以尝试不同的转换
cv.cvtColor(src, dst, cv.COLOR_RGBA2GRAY);
cv.imshow('canvasOutput', dst);
src.delete();
dst.delete();
```

## 视频入门

学习从相机捕获视频并播放

通常，我们必须使用相机捕获实时流。在OpenCV.js中，我们使用[WebRTC](https://webrtc.org/)和HTML canvas元素来实现这一点。让我们从相机（内置或USB）捕获视频，将其转换为灰度视频并显示。

**首先，我们使用WebRTC navigator.mediaDevices.getUserMedia来获取媒体流。**

```js
let video = document.getElementById("videoInput")); //videoInput是<video>标签的 ID
navigator.mediaDevices.getUserMedia({ video： true, audio： false })
    .then(function(stream) {
        video.srcObject = stream;
        video.play();
    })
    .catch(function(err) {
        console.log("An error occured! " + err);
    });
```

!从视频文件捕获视频时，不需要此功能。但请注意，HTML视频元素仅支持Ogg（Theora），WebM（VP8 / VP9）或MP4（H.264）的视频格式。

**播放视频**

现在，浏览器获取相机流。然后，我们使用 Canvas 2D API 的 CanvasRenderingContext2D.drawImage（） 方法将视频绘制到画布上。最后，我们可以使用图像入门中的方法来读取和显示画布中的[图像](https://docs.opencv.org/3.3.1/df/d24/tutorial_js_image_display.html)。为了播放视频，[cv.imshow（）](https://docs.opencv.org/3.3.1/d7/dfc/group__highgui.html#ga453d42fe4cb60e5723281a89973ee563) 应该每延迟一毫秒执行一次。我们推荐 setTimeout（） 方法。如果视频为 30fps，则延迟毫秒应为 （1000/30 - processing_time）。

```js
let canvasFrame = document.getElementById("canvasFrame"); // canvasFrame是<canvas>标签的ID 
let context = canvasFrame.getContext("2d");
let src = new cv.Mat(height, width, cv.CV_8UC4);
let dst = new cv.Mat(height, width, cv.CV_8UC1);
const FPS = 30;
function processVideo() {
    let begin = Date.now();
    context.drawImage(video, 0, 0, width, height);
    src.data.set(context.getImageData(0, 0, width, height).data);
    cv.cvtColor(src, dst, cv.COLOR_RGBA2GRAY);
    cv.imshow("canvasOutput", dst); // canvasOutput是另一个<canvas>标签的 id;
    // 播放下一个
    let delay = 1000/FPS - (Date.now() - begin);
    setTimeout(processVideo, delay);
}
// 播放第一个
setTimeout(processVideo, 0);
```

OpenCV.js 使用上述方法实现 `cv.VideoCapture(videoSource)`您无需手动添加隐藏的画布元素。

**videoSource**：视频 ID 或元素

上面的视频播放代码可以简化如下：

```js
let src = new cv.Mat(height, width, cv.CV_8UC4);
let dst = new cv.Mat(height, width, cv.CV_8UC1);
let cap = new cv.VideoCapture(videoSource);
const FPS = 30;
function processVideo() {
    let begin = Date.now();
    cap.read(src);
    cv.cvtColor(src, dst, cv.COLOR_RGBA2GRAY);
    cv.imshow("canvasOutput", dst);
    // 播放下一个
    let delay = 1000/FPS - (Date.now() - begin);
    setTimeout(processVideo, delay);
}
// 播放第一个
setTimeout(processVideo, 0);
```

!>请记住在停止后删除 src 和 dst

**完整示例：**

```js
let video = document.getElementById('videoInput');
let src = new cv.Mat(video.height, video.width, cv.CV_8UC4);
let dst = new cv.Mat(video.height, video.width, cv.CV_8UC1);
let cap = new cv.VideoCapture(video); //创建相机捕捉实例。请正确连接相机设备。否则可能报错“相机错误：未找到错误请求的设备”

const FPS = 30;
function processVideo() {
    try {
        if (!streaming) {
            // 清除src和dst并停止任务
            src.delete();
            dst.delete();
            return;
        }
        let begin = Date.now();
        // 开始处理.
        cap.read(src);
        cv.cvtColor(src, dst, cv.COLOR_RGBA2GRAY);
        cv.imshow('canvasOutput', dst);
        // 播放第二个
        let delay = 1000/FPS - (Date.now() - begin);
        setTimeout(processVideo, delay);
    } catch (err) {
        utils.printError(err);
    }
};

// 播放第一个
setTimeout(processVideo, 0);
```



## 向应用程序添加跟踪栏

创建跟踪栏以控制某些参数

使用 HTML DOM 输入范围对象将跟踪栏添加到应用程序。

**首先，我们需要创建三个画布元素：两个用于输入，一个用于输出。请参阅[教程图像入门](https://docs.opencv.org/3.3.1/df/d24/tutorial_js_image_display.html)。**

```js
let src1 = cv.imread('canvasInput1');
let src2 = cv.imread('canvasInput2');
```

**然后，我们使用 HTML DOM 输入范围对象来实现跟踪栏,如下所示：**

<input type="range">

!>`type=“range”` 的` <input> `属性在 Internet Explorer 9 和更早版本中不支持。

您可以使用 `document.createElement()`方法创建一个 type=“range” 的` <input> `元素：

```js
let x = document.createElement('INPUT');
x.setAttribute('type', 'range');
```

您也可以使用`getElementById()`访问type="range"的`<input>`元素：

```js
let x = document.getElementById('myRange');
```

作为跟踪栏，range 元素需要跟踪栏名称、默认值、最小值、最大值、步长和每次跟踪栏值更改时执行的回调函数。回调函数始终具有默认参数，即跟踪栏位置。此外，显示跟踪栏值的文本元素也可以。在我们的例子中，我们可以创建如下所示的跟踪栏：

```js
重量: <input type="range" id="trackbar" value="50" min="0" max="100" step="1" oninput="callback()">
<input type="text" id="weightValue" size="3" value="50"/>
```

**最后，我们可以在回调函数中使用跟踪栏值，混合两张图片，并显示结果**。

```js
let weightValue = document.getElementById('weightValue');
let trackbar = document.getElementById('trackbar');
weightValue.setAttribute('value', trackbar.value);
let alpha = trackbar.value/trackbar.max;
let beta = ( 1.0 - alpha );
let src1 = cv.imread('canvasInput1');
let src2 = cv.imread('canvasInput2');
let dst = new cv.Mat();
cv.addWeighted( src1, alpha, src2, beta, 0.0, dst, -1);
cv.imshow('canvasOutput', dst);
dst.delete();
src1.delete();
src2.delete();
```

**完整示例：**

```js
let trackbar = document.getElementById('trackbar');
let alpha = trackbar.value/trackbar.max;
let beta = ( 1.0 - alpha );
let src1 = cv.imread('canvasInput1');
let src2 = cv.imread('canvasInput2');
let dst = new cv.Mat();
cv.addWeighted( src1, alpha, src2, beta, 0.0, dst, -1);
cv.imshow('canvasOutput', dst);
dst.delete();
src1.delete();
src2.delete();
```

