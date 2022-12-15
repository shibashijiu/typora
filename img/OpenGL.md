# OpenGL

## 1.OpenGL入门

OpenGL文档地址：https://learnopengl-cn.github.io/

### 1.1Creating a window

配置visual studio环境，我用的是VS2022

下载GLFW库，网址：https://www.glfw.org/

点击Download

![img](OpenGL.assets/%60YJIF0NGWOPU%5D%5B43D%7DR@%25S.png)



下载32位（因为64位bug多）

![image-20221214133142985](OpenGL.assets/image-20221214133142985.png)





下载GLEW库，网址：https://glew.sourceforge.net/

![image-20221214133353016](OpenGL.assets/image-20221214133353016.png)



下载完成后，有：

![image-20221214133500958](OpenGL.assets/image-20221214133500958.png)



新建一个OpenGL的文件夹，把上面下载的两个东西丢进去。



配置visual studio

打开VS，在主界面，依次点击：文件——新建——项目——空项目——下一步

![image-20221214133826309](OpenGL.assets/image-20221214133826309.png)

自定义项目名称和位置，点击创建



右键刚才新建的项目，点击属性

![image-20221214134514384](OpenGL.assets/image-20221214134514384.png)

将上方的配置修改为所有配置；平台修改为所有平台。

选择C/C++选项中的常规，点击“附加包含目录”，右侧会出现一个下拉框，点击编辑

![image-20221214134750054](OpenGL.assets/image-20221214134750054.png)

点击右上角的红色小框的按钮，添加你刚才下载的两个库的“include”目录，到include为止，不再往下选，点击确定。



选择链接器选项中的常规，点击“附加库目录”，右侧会出现一个下拉框，点击编辑

![image-20221214135314917](OpenGL.assets/image-20221214135314917.png)

和上面的流程一样，添加以下目录

![image-20221214135511150](OpenGL.assets/image-20221214135511150.png)



然后选择链接器选项中的输入，点击“附加依赖项”，右侧会有一个下拉框，点击编辑

![image-20221214135941028](OpenGL.assets/image-20221214135941028.png)

如下图，输入这三个包添加进去，点击确定

![image-20221214140645832](OpenGL.assets/image-20221214140645832.png)

最后不要忘了点击确定

![image-20221214140815805](OpenGL.assets/image-20221214140815805.png)

然后就可以敲代码了



在官方的教程中配置了glad库，在这里补充一下：

glad库下载地址：https://glad.dav1d.de/

注意框出来的部分要改成这样：

![image-20221215151436729](OpenGL.assets/image-20221215151436729.png)

网页下滑，点击“GENERATE”，然后就跳转到这个界面：

![image-20221215151543213](OpenGL.assets/image-20221215151543213.png)

点击glad.zip，就开始下载啦，然后解压，丢到上面创建的OpenGL的文件夹里

![image-20221215151705950](OpenGL.assets/image-20221215151705950.png)

然后就开始配置了

右键刚才新建的项目，点击属性

![image-20221215152716066](OpenGL.assets/image-20221215152716066.png)

选择C/C++选项中的常规，选择“附加包含目录”，点击编辑

![image-20221215152823102](OpenGL.assets/image-20221215152823102.png)

添加红框中的目录，就是你刚刚下载的glad文件夹里，点击确定

最后再点一次确定

![image-20221215153001214](OpenGL.assets/image-20221215153001214.png)

就配置好啦。



然后在官方给出的代码包里用这个文件测试一下配置是否成功：

![image-20221215151942524](OpenGL.assets/image-20221215151942524.png)

运行之后报错了

![image-20221215152052542](OpenGL.assets/image-20221215152052542.png)

百度一下，是要将glad.c文件添加到当前项目

![image-20221215152213756](OpenGL.assets/image-20221215152213756.png)

依次点击：源文件——添加——现有项，然后在下面这个路径中找到glad.c文件

![image-20221215152326073](OpenGL.assets/image-20221215152326073.png)

就添加进去啦，然后再运行一次，就没有报错了

![image-20221215152432146](OpenGL.assets/image-20221215152432146.png)





### 1.2Hello window

```c++
#include<iostream>

#define GLEW_STATIC
#include<GL/glew.h>
#include<GLFW/glfw3.h>

int main()
{
	glfwInit();
	glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR,3);
	glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);
	glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);

	return 0;
}
```

在我的电脑上，VS的默认编译环境是64位的，运行上述代码后会报错

![image-20221214144625485](OpenGL.assets/image-20221214144625485.png)

解决方案：

![image-20221214144756023](OpenGL.assets/image-20221214144756023.png)

![image-20221214144928567](OpenGL.assets/image-20221214144928567.png)

选择x86，点击关闭，再运行就没有报错了

![image-20221214145102069](OpenGL.assets/image-20221214145102069.png)



```c++
#include<iostream>
using namespace std;

#define GLEW_STATIC
#include<GL/glew.h>
#include<GLFW/glfw3.h>

//按下esc键，可以关闭窗口
void processInput(GLFWwindow* window)
{
	if (glfwGetKey(window, GLFW_KEY_ESCAPE) == GLFW_PRESS)
		glfwSetWindowShouldClose(window, true);
}

//实例化GLFW窗口
int main()
{
	//在main函数中调用glfwInit函数来初始化GLFW，然后我们可以使用glfwWindowHint函数来配置GLFW。
	glfwInit();
	//此文档基于OpenGL3.3版本展开
	glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);
	glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);
	glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);

	//建一个800x600的名字叫“My OpenGL Game”的窗口
	//创建一个窗口对象，这个窗口对象存放了所有和窗口相关的数据，而且会被GLFW的其他函数频繁地用到。
	GLFWwindow* window = glfwCreateWindow(800, 600, "My OpenGL Game", NULL, NULL);
	if (window == NULL)
	{
		cout << "Failed to create GLFW window" << endl;
		glfwTerminate();
		return -1;
	}
	glfwMakeContextCurrent(window);

	//初始化
	glewExperimental = true;
	if (glewInit() != GLEW_OK)
	{
		cout << "Failed to create GLEW window" << endl;
		glfwTerminate();
		return -1;
	}

	//必须告诉OpenGL渲染窗口的尺寸大小，即视口(Viewport)，这样OpenGL才只能知道怎样根据窗口大小显示数据和坐标
	//我们可以通过调用glViewport函数来设置窗口的维度
	glViewport(0, 0, 800, 600);

	//glfwWindowShouldClose函数在我们每次循环的开始前检查一次GLFW是否被要求退出
	//如果是的话该函数返回true然后渲染循环便结束了，之后我们就可以关闭应用程序了。
	while (!glfwWindowShouldClose(window))
	{
		//在渲染循环的每一个迭代中调用processInput
		processInput(window);

		//调用glClearColor来设置清空屏幕所用的颜色
		glClearColor(0.5f, 0, 0, 1.0f);

		//调用glClear函数来清空屏幕的颜色缓冲
		glClear(GL_COLOR_BUFFER_BIT);

		//glfwSwapBuffers函数会交换颜色缓冲（它是一个储存着GLFW窗口每一个像素颜色值的大缓冲），
		//它在这一迭代中被用来绘制，并且将会作为输出显示在屏幕上。
		glfwSwapBuffers(window);

		//glfwPollEvents函数检查有没有触发什么事件（比如键盘输入、鼠标移动等）、更新窗口状态，
		//并调用对应的回调函数（可以通过回调方法手动设置）。
		glfwPollEvents();
	}

	//最后，当渲染循环结束后我们需要正确释放/删除之前的分配的所有资源。
	//我们可以在main函数的最后调用glfwTerminate函数来完成。
	glfwTerminate();
	return 0;
}
```

不出意外的话，运行之后就出现了以下界面：

![image-20221214185400898](OpenGL.assets/image-20221214185400898.png)



### 1.3Hello triangle

在学习这一小节之前，先注意：

- 顶点数组对象：Vertex Araay Object，VAO
- 顶点缓冲对象：Vertex Buffer Object，VBO
- 元素缓冲对象：Element Buffer Object，EBO（或索引缓冲对象：Index Buffer Object，IBO）

当指代这三个东西的时候，可能使用的是全称，也可能是英文缩写，都指的是一个东西

在OpenGL中，任何事物都在3D空间中，而屏幕和窗口却是2D像素数组，

因此OpenGL的大部分工作都是关于把3D坐标转变为适应你屏幕的2D像素。

3D坐标转为2D坐标的处理过程是由OpenGL的==图形渲染管线==（Graphics Pipeline，又称为管线，实际上就是一堆原始图形数据经过一个输送管道，期间经过各种变化处理最终出现在屏幕上的过程）管理的。

图形渲染管线被分为两个主要部分：

1. 把你的3D坐标转换为2D坐标
2. 把2D坐标转变为实际的有颜色的像素

在这里，简单讨论一下图形渲染管线，以及如何利用它创建一些好看的像素

==注意==：2D坐标和像素也是不同的，2D坐标精确表示一个点在2D空间中的位置，而2D像素是这个点的近似值，2D像素受到你的屏幕/窗口分辨率的限制。

图形渲染管线接受一组3D坐标，然后把它们转变为你屏幕上的有色2D像素输出。图形渲染管线可以被划分为几个阶段，每个阶段将会把前一个阶段的输出作为输入。

所有这些阶段都是高度专门化的（它们都有一个特定的函数），并且很容易并行执行。

正由于并行执行的特点，当今大多数显卡都有成千上万的小处理核心，它们在GPU上为每一个（渲染管线）阶段运行各自的小程序，从而在图形渲染管线中快速处理你的数据。

这些小程序叫做==着色器==（Shader）

有些着色器由开发者配置，因为允许用自己写的着色器来代替默认的，所以能够更细致地控制图形渲染管线中的特定部分。

由于运行在GPU上，所有又节省了宝贵的CPU时间。

OpenGL着色器是用==OpenGL着色器语言==（OpenGL Shading Language，GLSL）写成的。

下面是，一个图形渲染管线的每个阶段的抽象展示，蓝色部分代表的是我们可以注入自定义的着色器的部分

![img](OpenGL.assets/pipeline.png)

可见，图形渲染管线包含很多部分，每个部分都将在转换顶点数据到最终像素这一过程中处理各自特定的阶段。

1. 首先，以数组的形式传递三个3D坐标作为图形渲染管线的输入，用来表示一个三角形，这个数组叫顶点数据（Vertex Data）；顶点数据是一系列顶点的集合，一个==顶点==（Vertex）是一个3D坐标的数据的集合，而顶点数据是用==顶点属性==（Vertex Attribute）表示的，它可以包含任何我们想用的数据。简单起见，我们假定每个顶点只由一个3D位置和一些颜色值组成

==注意==：当提起“位置”的时候，它代表在一个“空间”中所处地点的这个特殊属性，同时“空间”代表着任何一种坐标系，比如三维坐标系或者二维坐标系，或者一条直线上x和y的线性关系。

为了让OpenGL知道我们的坐标和颜色值构成的是什么，OpenGL需要你去指定这些数据所表示的渲染类型。

那我们要把这些数据渲染成点还是三角形还是线呢？

做出的提示叫做==图元==（Primitive）任何一个绘制指令的调用都将把图元传递给OpenGL。

这是其中的几个：`GL_POINTS`、`GL_TRIANGLES`、`GL_LINE_STRIP`。



图形渲染管线的第一个部分是==顶点着色器==（Vertex Shader），它把一个单独的顶点作为输入。

顶点着色器主要的目的是把3D坐标转为另一种3D坐标（后面会解释），同时顶点着色器允许我们对顶点属性进行一些基本处理。

==图元装配==（Primitive Assembly）阶段，将顶点着色器输出的所有顶点作为输入（如果是`GL_POINTS`，那么就是一个顶点），将所有的点装配成指定图元的形状，。本节例子中是一个三角形。

图元装配阶段的输出会传递给==几何着色器==（Geometry Shader）。几何着色器把图元形式的一系列顶点的集合作为输入，它可以通过产生新顶点构造出新的（或其它的）图元来生成其他形状。本例中，它生成了另一个三角形。

几何着色器的输出会被传入==光栅化阶段==（Rasterization Stage），这里它会把图元映射成最终屏幕上相应的像素，生成供==片段着色器==（Fragment Shader）使用的片段（Fragment）。在片段着色器运行之前会执行==裁切==（Clipping）。裁切会丢弃超出你的视图以外的所有像素，用来提升执行效率。

==注意==：OpenGL中的一个片段是OpenGL渲染一个像素所需的所有数据。

片段着色器的主要目的是计算一个像素的最终颜色，这也是所有OpenGL高级效果产生的地方。通常，片段着色器包含3D场景的数据（比如光照、阴影、光的颜色等等），这些数据可以被用来计算最终像素的颜色。

在所有对应颜色值确定以后，最终的对象将会被传到最后一个阶段，称为==Alpha测试==和==混合==（Blending）阶段。这个阶段检测片段对应的深度值，会用来判断这个像素是其它物体的前面还是后面，决定是否应该丢弃。这个阶段也会检查==alpha==值（alpha值定义一个物体的透明度）并对物体进行==混合==（Blend）。所以，即使在片段着色器中计算出来了一个像素输出的颜色，在渲染多个三角形的时候最后的像素颜色也可能完全不同。

图形渲染管线非常复杂，它包含很多可配置的部分。然而，对于大多数场合，我们只需要配置顶点和片段着色器就行了。几何着色器是可选的，通常使用它默认的着色器就行了。

#### 1.3.1顶点输入





![image-20221215160540642](OpenGL.assets/image-20221215160540642.png)

