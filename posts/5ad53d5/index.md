# C&#43;&#43;代码书写规范


&lt;!--more--&gt;
{{&lt; figure src=&#34;https://cdn.pixabay.com/photo/2024/04/02/09/20/woman-8670414_1280.jpg&#34;&gt;}}
#  C&#43;&#43;代码书写规范

1. 变量命名使用下划线命名法，函数命名使用大驼峰命名法，类和结构体使用大驼峰命名法，文件名使用下划线命名法
2. 全局变量和常量使用k&#43;大驼峰命名法，类成员变量可以以下划线作为结尾，结构体成员变量不加下划线
3. 尽量不要使用全局变量，可以将其封装进对象里
4. ros中回调函数的形参可以使用const name &amp; 修饰
5. 函数声明中const修饰符无意义，只需在函数定义中使用
6. 在成员函数中使用ros中的subscribe需要参考以下格式：省略.subscribe(&#34;话题&#34;, 1, &amp;类::回调函数, this);
7. 模板类的静态成员变量是每个特定实例化类型共享一份，而不是所有实例化类共享同一份。例如MyClass\&lt;int\&gt;和MyClass\&lt;double\&gt;的静态成员变量是独立的。

---

> 作者: Lv Wenbo  
> URL: https://WbLv66.github.io/posts/5ad53d5/  

