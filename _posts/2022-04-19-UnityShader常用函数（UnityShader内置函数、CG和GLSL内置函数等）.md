---
layout:     post
title:      UnityShader常用函数（UnityShader内置函数、CG和GLSL内置函数等）
subtitle:   UnityShader
date:       2022-04-19
author:     坏人
header-img: img/the-first.png
catalog: false
tags:
    - Unity杂谈
---

# 一、CG和GLSL常用函数

## CG语言中的变量修饰符

| 修饰符 | 解析 |
| --- | --- |
| const | 变量被定义成常量的话，在程序中，就不能再对该变量赋值，除非const和uniform，varying一起使用。const修饰的变量，需要在声明时给予一个初始值 |
| extern | extern表明声明仅仅是声明，而非定义。在程序中一定有一个地方存在一个非extern的对应的声明 |
| in | 只在声明参数，或是使用varying修饰符时使用。将参数，或是varying作为函数或是程序的输入值。函数参数如果没有in，out，或者inout的话，隐式的默认为in |
| inline | 只在函数定义时有用，告诉编译器始终对该函数采取内联调用 |
| inout | 只在声明为参数和varying时使用，将参数或是varying声明为函数或是程序的输入输出值 |
| static | 只在声明全局变量时使用，static将使变量对程序而言成为私有的，外部不可见，不能和uniform，varying一起使用 |
| out | 只在声明参数和varying时使用，将变量或varying定义为函数或是程序的输出值 |
| uniform | 用于全局变量和程序的入口函数的参数，用来定义constant buffers(常量缓存)。如果用于一个非入口函数的参数，它将被忽略。这样做的目的是为了使一个函数既能作为入口函数，又能作为非入口函数。uniform的变量可以像非uniform的变量那样读写。uniform修饰符通过向外部语言提供一个机制，来提供变量的初始值是如何指定和保存的信息。 |

## 1、数学函数

| CG语言 | GLSL语言 | 功能描述 |
| --- | --- | --- |
| ceil(x) | ceil(x) | 对输入参数向上取整。例如： ceil(float(1.3)) ，其返回值为2.0 |
| floor(x) | floor(x) | 对输入参数向下取整。例如floor(float(1.3))返回的值为1.0；但是floor(float(-1.3))返回的值为-2.0。该函数与ceil(x)函数相对应。 |
| fmod(x,y) | mod(x, y) | 返回x/y的余数。如果y为0，结果不可预料。 |
| frac(x) | fract(x) | 返回标量或矢量的小数 |
| frexp(x, out i) |  | 将浮点数 x 分解为尾数和指数，即 x = m* 2^exp，返回 m，并将指数存入 exp 中；如果 x 为 0，则尾数和指数都返回 0 |
| modf(x, out ip) |  | 把x分解成整数和分数两部分，每部分都和x有着相同的符号，整数部分被保存在ip中，分数部分由函数返回 |
| round(x) |  | 返回四舍五入值。 |
| exp(x) | exp(x) | 计 算 e x 的 值 ， e = 2.71828182845904523536 计算 \def\bar#1{#1^x} \bar{e}的值，e=2.71828182845904523536 计算ex的值，e=2.71828182845904523536 |
| exp2(x) | exp2(x) | 计 算 2 x 的 值 计算 \def\bar#1{#1^x} \bar{2}的值 计算2x的值 |
| log(x) | log(x) | 计 算 ln ⁡ ( x ) 的 值 ， x 必 须 大 于 0 计算\ln(x)的值，x必须大于0 计算ln(x)的值，x必须大于0 |
| log2(x) | log2(x) | 计 算 log ⁡ 2 ( x ) 的 值 ， x 必 须 大 于 0 计算\log_2(x)的值，x必须大于0 计算log2​(x)的值，x必须大于0 |
| log10(x) |  | 计 算 lg ⁡ ( x ) 的 值 ， x 必 须 大 于 0 计算\lg(x)的值，x必须大于0 计算lg(x)的值，x必须大于0 |
| max(a, b) | max(a, b) | 比较两个标量或等长向量元素，返回最大值。 |
| min(a,b) | min(a,b) | 比较两个标量或等长向量元素，返回最小值。 |
| pow(x, y) | pow(x, y) | 计 算 x y 的 值 计算 \def\bar#1{#1^y} \bar{x}的值 计算xy的值 |
| sqrt(x) | sqrt(x) | 求x的平方根，，x必须大于0 |
| rsqrt(x) | inversesqrt(x) | x的平方根的倒数，x必须大于0 |
| abs(x) | abs(x) | 返回输入参数的绝对值 |
| ldexp(x, n) |  | 计 算 x ∗ 2 n 的 值 计算 x*\def\bar#1{#1^n} \bar{2}的值 计算x∗2n的值 |
| mul(M, N) | M*N | 矩阵M和矩阵N的积 |
| mul(M, v) | M*v | 矩阵M和列向量v的积 |
| mul(v, M) | v* M | 行向量v和矩阵M的积 |
| determinant(m) |  | 计算矩阵的行列式因子。 |
| transpose(M) |  | 矩阵M的转置矩阵
如果M是一个AxB矩阵，M的转置是一个BxA矩阵，它的第一列是M的第一行，第二列是M的第二行，第三列是M的第三行，等等 |
| asin(x) | asin(x) | 反正弦函数,输入参数取值区间为，返回角度值范围为[−π/2,π/2] |
| acos(x) | acos(x) | 反余切函数，输入参数范围为[-1,1]， 返回[0,π]区间的角度值 |
| atan(x) | atan(x) | 反正切函数，返回角度值范围为[−π/2,π/2] |
| atan2(y,x) | atan2(y,x) | 计算y/x的反正切值。实际上和atan(x)函数功能完全一样，至少输入参数不同。atan(x) = atan2(x, float(1))。 |
| sin(x) | sin(x) | 输入参数为弧度，计算正弦值，返回值范围 为[-1,1] |
| cos(x) | cos(x) | 返回弧度x的余弦值。返回值范围为 |
| tan(x) | tan(x) | 计算x正切值 |
| sincos(float x, out s, out c) |  | 该函数是同时计算x的sin值和cos值，其中s=sin(x)，c=cos(x)。该函数用于“同时需要计算sin值和cos值的情况”，比分别运算要快很多! |
| sinh(x) |  | 计算x的双曲正弦 |
| cosh(x) |  | 双曲余弦（hyperbolic cosine）函数，计算x的双曲余弦值。 |
| tanh(x) |  | 计算x的双曲线切线 |
| radians(x) | radians(x) | 函数将角度值转换为弧度值 |
| degrees(x) | degrees(x) | 输入参数为弧度值(radians)，函数将其转换为角度值(degrees) |
| cross(A,B) | cross(A,B) | 返回两个三元向量的叉积(cross product)。注意，输入参数必须是三元向量！ |
| lit(NdotL, NdotH, m) |  | 函数计算环境光、散射光、镜面光的贡献，返回的4元向量。
N表示法向量；
L表示入射光向量；
H表示半角向量；
m表示高光系数。
X位表示环境光的贡献，总是1.0;
Y位代表散射光的贡献，如果 N∙L<0，则为0；否则为N∙L
Z位代表镜面光的贡献，如果N∙L<0 或者N∙H<0，则位0；否则为(N∙L)m;
W位始终位1.0 |
| all(x) | all(x) | 如果输入参数均不为0，则返回ture； 否则返回flase。&&运算 |
| any(x) | any(x) | 输入参数只要有其中一个不为0，则返回true。 |
| isfinite(x) |  | 判断标量或者向量中的每个数据是否是有限数，如果是返回true；否则返回false; |
| isinf(x) |  | 判断标量或者向量中的每个数据是否是无限，如果是返回true；否则返回false; |
| isnan(x) |  | 判断标量或者向量中的每个数据是否是非数据(not-a-number NaN)，如果是返回true；否则返回false; |
| step(a, x) | step(a, x) | 如果x<a, 返回0；否则返回1 |
| sign(x) | sign(x) | 如果x>0则返回1；如果x=0返回0；如果x<0则返回-1 |
| dot(A,B) | dot(A,B) | 返回A和B的点积(dot product)。参数A和B可以是标量，也可以是向量（输入参数方面，点积和叉积函数有很大不同）。 |
| noise(x) |  | 根据它的参数类型，这个函数可以是一元、二元或三元噪音函数。返回的值在0和1之间，并且通常与给定的输入值一样 |
| clamp(x,a,b) | clamp(x,a,b) | 如果x值小于a，则返回a；
如果x值大于b，返回b；
否则，返回x。 |
| lerp(a, b, f) | mix(a, b, f) | 计算或者的值。即在下限a和上限b之间进行插值，f表示权值。注意，如果a和b是向量，则权值f必须是标量或者等长的向量。 |
| saturate(x) |  | 把x限制到[0,1]之间 |
| smoothstep(min, max, x) | smoothstep(min, max, x) | 值x位于min、max区间中。
如果x=min，返回0；如果x=max，返回1；
如果x在两者之间，按照下列公式返回数据：
– 2 ∗ ( ( x – m i n ) / ( m a x – m i n ) ) 3 + 3 ∗ ( ( x – m i n ) / ( m a x – m i n ) ) 2 \def\bar#1{#1^3} \bar{–2*(( x – min )/( max – min ))} + \def\bar#1{#1^2} \bar{3*(( x – min )/( max – min ))} –2∗((x–min)/(max–min))3+3∗((x–min)/(max–min))2 |

smoothstep(min, max, x)对于参数全是float的重载

```
float smoothstep(float a, float b, float x)
{
    float t = saturate((x - a)/(b - a));
    return t*t*(3.0 - (2.0*t));
}
12345
```

## 2、几何函数

| CG语言 | GLSL语言 | 功能描述 |
| --- | --- | --- |
| distance(pt1, pt2) | distance(pt1, pt2) | 两点之间的欧几里德距离（Euclidean distance） |
| faceforward(N,I,Ng) | faceforward(N,I,Ng) | 根据 矢量 N 与Nref 调整法向量,如果Ng•I < 0 ，返回 N；否则返回-N。 |
| length(v) | length(v) | 返回一个向量的模，即sqrt(dot(v,v)) |
| normalize(v) | normalize(v) | 返回v向量的单位向量 |
| reflect(I, N) | reflect(I, N) | 根据入射光方向向量 I，和顶点法向量 N，计算反射光方向向量。
其中 I 和 N 必须被归一化，需要非常注意的是，这个 I 是指向顶点的；
函数只对三元向量有效 |
| refract(I,N,eta) | refract(I,N,eta) | 计算折射向量，I 为入射光线，N 为法向量，eta 为折射系数；
其中 I 和 N 必须被归一化，如果 I 和 N 之间的夹角太大，则返回（0，0，0），也就是没有折射光线；I 是指向顶点的；
函数只对三元向量有效 |

## 3、纹理映射函数

| CG语言 | 功能描述 |
| --- | --- |
| tex1D(sampler1D tex, float s) | 一维纹理查询 |
| tex1D(sampler1D tex, float s, float dsdx, float dsdy) | 使用导数值（derivatives）查询一维纹理 |
| Tex1D(sampler1D tex, float2 sz) | 一维纹理查询，并进行深度值比较 |
| Tex1D(sampler1D tex, float2 sz, float dsdx,float dsdy) | 使用导数值（derivatives）查询一维纹理， 并进行深度值比较 |
| Tex1Dproj(sampler1D tex, float2 sq) | 一维投影纹理查询 |
| Tex1Dproj(sampler1D tex, float3 szq) | 一维投影纹理查询，并比较深度值 |
| Tex2D(sampler2D tex, float2 s) | 二维纹理查询 |
| Tex2D(sampler2D tex, float2 s, float2 dsdx, float2 dsdy) | 使用导数值（derivatives）查询二维纹理 |
| Tex2D(sampler2D tex, float3 sz) | 二维纹理查询，并进行深度值比较 |
| Tex2D(sampler2D tex, float3 sz, float2 dsdx,float2 dsdy) | 使用导数值（derivatives）查询二维纹理，并进行深度值比较 |
| Tex2Dproj(sampler2D tex, float3 sq) | 二维投影纹理查询 |
| Tex2Dproj(sampler2D tex, float4 szq) | 二维投影纹理查询，并进行深度值比较 |
| texRECT(samplerRECT tex, float2 s) | 二维非投影矩形纹理查询（OpenGL独有） |
| texRECT (samplerRECT tex, float3 sz, float2 dsdx,float2 dsdy) | 二维非投影使用导数的矩形纹理查询（OpenGL独有） |
| texRECT (samplerRECT tex, float3 sz) | 二维非投影深度比较矩形纹理查询（OpenGL独有） |
| texRECT (samplerRECT tex, float3 sz, float2 dsdx,float2 dsdy) | 二维非投影深度比较并使用导数的矩形纹理查询（OpenGL独有） |
| texRECT proj(samplerRECT tex, float3 sq) | 二维投影矩形纹理查询（OpenGL独有） |
| texRECT proj(samplerRECT tex, float3 szq) | 二维投影矩形纹理深度比较查询（OpenGL独有） |
| Tex3D(sampler3D tex, float s) | 三维纹理查询 |
| Tex3D(sampler3D tex, float3 s, float3 dsdx, float3 dsdy) | 结合导数值（derivatives）查询三维纹理 |
| Tex3Dproj(sampler3D tex, float4 szq) | 查询三维投影纹理，并进行深度值比较 |
| texCUBE(samplerCUBE tex, float3 s) | 查询立方体纹理 |
| texCUBE (samplerCUBE tex, float3 s, float3 dsdx, float3 dsdy) | 结合导数值（derivatives）查询立方体纹理 |
| texCUBEproj (samplerCUBE tex, float4 sq) | 查询投影立方体纹理 |

## 4、偏导函数

| 函数 | 功能描述 |
| --- | --- |
| ddx(a) | 近似a关于屏幕空间x轴的偏导数 |
| ddy(a) | 近似a关于屏幕空间y轴的偏导数 |

# 二、Unity常用的[内置函数](https://so.csdn.net/so/search?q=%E5%86%85%E7%BD%AE%E5%87%BD%E6%95%B0&spm=1001.2101.3001.7020)，变量

## 1、Unity常用的结构体

### 1.1、顶点着色器输入

| 名称 | 描述 | 包含的变量 |
| --- | --- | --- |
| appdata_base | 用于顶点着色器输入 | 顶点位置、顶点法线、第一组纹理坐标 |
| appdata_tan | 用于顶点着色器输入 | 顶点位置、顶点切线、顶点法线、第一组纹理坐标 |
| appdata_full | 用于顶点着色器输入 | 顶点位置、顶点切线、顶点法线、四组（或更多）纹理坐标 |
| appdata_img | 用于顶点着色器输入 | 顶点位置、第一组纹理坐标 |

```
struct appdata_base {
    float4 vertex : POSITION;
    float3 normal : NORMAL;
    float4 texcoord : TEXCOORD0;
    UNITY_VERTEX_INPUT_INSTANCE_ID
};

struct appdata_tan {
    float4 vertex : POSITION;
    float4 tangent : TANGENT;
    float3 normal : NORMAL;
    float4 texcoord : TEXCOORD0;
    UNITY_VERTEX_INPUT_INSTANCE_ID
};

struct appdata_full {
    float4 vertex : POSITION;
    float4 tangent : TANGENT;
    float3 normal : NORMAL;
    float4 texcoord : TEXCOORD0;
    float4 texcoord1 : TEXCOORD1;
    float4 texcoord2 : TEXCOORD2;
    float4 texcoord3 : TEXCOORD3;
    fixed4 color : COLOR;
    UNITY_VERTEX_INPUT_INSTANCE_ID
};
struct appdata_img
{
    float4 vertex : POSITION;
    half2 texcoord : TEXCOORD0;
    UNITY_VERTEX_INPUT_INSTANCE_ID
};
1234567891011121314151617181920212223242526272829303132
```

### 1.2、顶点着色器输出

| 名称 | 描述 | 包含的变量 |
| --- | --- | --- |
| v2f_img | 用于顶点着色器输出 | 裁剪空间中的位置、纹理坐标 |

```
struct v2f_img
{
    float4 pos : SV_POSITION;
    half2 uv : TEXCOORD0;
    UNITY_VERTEX_INPUT_INSTANCE_ID
    UNITY_VERTEX_OUTPUT_STEREO
};
1234567
```

## 2、空间变换函数及内置变量

### A、空间变换函数

| 函数名 | 描述 |
| --- | --- |
| float4 UnityWorldToClipPos(float3 pos ) | 把世界坐标空间中某一点pos变换到齐次裁剪空间 |
| float4 UnityViewToClipPos(float3 pos ) | 把观察坐标空间中某一点pos变换到齐次裁剪空间 |
| float3 UnityObjectToViewPos(float3 pos或float4 pos) | 模型局部空间坐标系中某一个点pos变换到观察空间坐标系 |
| float3 UnityWorldToViewPos(float3 pos ) | 把世界坐标系下的一个点pos变换到观察空间坐标系 |
| float3 UnityObjectToWorldDir(float3 dir ) | 把方向矢量从模型空间转换到世界空间（方向已单位化） |
| float3 UnityWorldToObjectDir(float3 dir ) | 把方向矢量从世界空间转换到模型空间（方向已单位化） |
| float3 UnityObjectToWorldNormal(float3 norm ) | 将法线从模型空间转换到世界空间（方向已单位化） |
| float3 UnityWorldSpaceLightDir(float3 worldPos ) | 输入参数worldPos是一个世界坐标系下的坐标，得到世界空间中从该点到光源（_WorldSpaceLightPos0）的光照方向。（方向没单位化） |
| float3 WorldSpaceLightDir(float4 localPos ) | 输入一个模型顶点坐标，得到世界空间中从该点到光源（_WorldSpaceLightPos0）的光照方向。（方向没单位化） |
| float3 ObjSpaceLightDir(float4 v ) | 输入一个模型顶点坐标，得到模型空间中从该点到光源（_WorldSpaceLightPos0）的光照方向。（方向没单位化） |
| float3 UnityWorldSpaceViewDir(float3 worldPos ) | 输入参数worldPos是一个世界坐标系下的坐标，得到世界空间中从该点到摄像机的观察方向。（方向没单位化） |
| float3 WorldSpaceViewDir(float4 localPos ) | 输入一个模型顶点坐标，得到世界空间中从该点到摄像机的观察方向。（方向没单位化） |
| float3 ObjSpaceViewDir(float4 v ) | 输入一个模型顶点坐标，得到模型空间中从该点到摄像机的观察方向。（方向没单位化） |

### B、屏幕空间相关函数

以下函数可计算用于采样屏幕空间纹理的坐标。它们返回 float4，其中用于纹理采样的最终坐标可以通过透视除法（例如 xy/w）计算得出。

| 函数名 | 描述 |
| --- | --- |
| float4 ComputeScreenPos (float4 clipPos) | 计算用于执行屏幕空间贴图纹理采样的纹理坐标。输入是裁剪空间位置。 |
| float4 ComputeGrabScreenPos (float4 clipPos) | 计算用于 GrabPass 纹理采样的纹理坐标。输入是裁剪空间位置。 |

### C、内置变量矩阵

| 变量名 | 描述 |
| --- | --- |
| UNITY_MATRIX_MVP | 当前的模型_观察_投影矩阵，用于将顶点/方向矢量从模型空间转换到裁剪空间 |
| UNITY_MATRIX_MV | 当前的模型*观察矩阵，用于将顶点/方向矢量从模型空间转换到观察空间 |
| UNITY_MATRIX_V | 当前的观察矩阵，用于将顶点/方向矢量从世界空间转换到观察空间 |
| UNITY_MATRIX_P | 当前的投影矩阵，用于将顶点/方向矢量从观察空间转换到裁剪空间 |
| UNITY_MATRIX_VP | 当前的观察*投影矩阵，用于将顶点/方向矢量从世界空间转换到裁剪空间 |
| UNITY_MATRIX_T_MV | UNITY_MATRIX_MV的转置矩阵 |
| UNITY_MATRIX_IT_MV | UNITY_MATRIX_MV的逆转置矩阵，用于将法线从模型空间转换到观察空间，也可以用于得到UNITY_MATRIX_MV的逆矩阵 |
| unity_ObjectToWorld | 当前模型矩阵 |
| unity_WorldToObject | 当前世界矩阵的逆矩阵。 |

### D、摄像机和屏幕参数

| 参数名 | 描述 |
| --- | --- |
| float3 _WorldSpaceCameraPos | 该摄像机在世界空间中的位置 |
| float4 _ProjectionParams | x=1.0(或-1.0，如果正在使用一个翻转的投影矩阵进行渲染)，y=Near,z=Far,w=1.0+1.0/Far,其中Near和Far分别是近裁剪平面和远裁剪平面到摄像机的距离 |
| float4 _ScreenParams | x=width,y=height,z=1.0+1.0/width,w=1.0+1.0/height,其中width和height分别是该摄像机的渲染目标（render target）的像素宽度和高度 |
| float4 _ZBufferParams | x=1-Far/Near,y=Far/Near,z=x/Far,w=y/Far,该变量用于线性化Z缓存中的深度值 |
| float4 unity_OrthoParams | x=width,y=height,z没有定义,w=1.0(该摄像机是正交摄像机)或w=0.0（该摄像机是透视摄像机），其中width和height是正交投影摄像机的宽度和高度 |
| float4x4 unity_CameraProjection | 该摄像机的投影矩阵 |
| float4x4 unity_CameraInvProjection | 该摄像机的投影矩阵的逆矩阵 |
| float4 unity_CameraWorldClipPlanes[6] | 该摄像机的6个裁剪平面在世界空间下的等式，按左、右、下、上、近、远裁剪平面 |

### E、时间相关参数

| 参数名 | 描述 |
| --- | --- |
| float4 _Time | 自关卡加载以来的时间 (t/20, t, t_2, t_3)，用于将着色器中的内容动画化 |
| float4 _SinTime | 时间正弦：(t/8, t/4, t/2, t) |
| float4 _CosTime | 时间余弦：(t/8, t/4, t/2, t) |
| float4 unity_DeltaTime | 增量时间：(dt, 1/dt, smoothDt, 1/smoothDt) |

### E、光照相关参数

前向渲染（ForwardBase 和 ForwardAdd 通道类型）：

| 参数名 | 描述 |
| --- | --- |
| fixed4 _LightColor0 | （在 Lighting.cginc 中声明）光源颜色。 |
| float4 _WorldSpaceLightPos0 | 方向光：（世界空间方向，0）。其他光源：（世界空间位置，1）。 |
| float4x4 _LightMatrix0 | （在 AutoLight.cginc 中声明） 世界/光源矩阵。用于对剪影和衰减纹理进行采样。 |
| float4 unity_4LightPosX0、unity_4LightPosY0、unity_4LightPosZ0 | （仅限 ForwardBase 通道）前四个非重要点光源的世界空间位置。 |
| float4 unity_4LightAtten0 | （仅限 ForwardBase 通道）前四个非重要点光源的衰减因子。 |
| half4[4] unity_LightColor | （仅限 ForwardBase 通道）前四个非重要点光源的颜色。 |
| float4x4[4] unity_WorldToShadow | 世界/阴影矩阵。聚光灯的一个矩阵，方向光级联最多有四个矩阵。 |

延迟着色和延迟光照，在光照通道着色器中使用（全部在 UnityDeferredLibrary.cginc 中声明）：

| 参数名 | 描述 |
| --- | --- |
| float4 _LightColor | 光源颜色。 |
| float4x4 _LightMatrix0 | 世界/光源矩阵。用于对剪影和衰减纹理进行采样。 |
| float4x4[4] unity_WorldToShadow | 世界/阴影矩阵。聚光灯的一个矩阵，方向光级联最多有四个矩阵。 |

### F、雾效和环境光

| 参数名 | 描述 |
| --- | --- |
| fixed4 unity_AmbientSky | 梯度环境光照情况下的天空环境光照颜色。 |
| fixed4 unity_AmbientEquato | 梯度环境光照情况下的赤道环境光照颜色。 |
| fixed4 unity_AmbientGround | 梯度环境光照情况下的地面环境光照颜色。 |
| fixed4 UNITY_LIGHTMODEL_AMBIENT | 环境光照颜色（梯度环境情况下的天空颜色）。旧版变量。 |
| fixed4 unity_FogColor | 雾效颜色。 |
| float4 unity_FogParams | 用于雾效计算的参数：(density / sqrt(ln(2))、density / ln(2)、–1/(end-start) 和 end/(end-start))。x 对于 Exp2 雾模式很有用；_y_ 对于 Exp 模式很有用，_z_ 和 w 对于 Linear 模式很有用。 |

## 3、数学常数

```
#ifndef UNITY_CG_INCLUDED
#define UNITY_CG_INCLUDED

#define UNITY_PI            3.14159265359f       //圆周率
#define UNITY_TWO_PI        6.28318530718f       //2倍圆周率
#define UNITY_FOUR_PI       12.56637061436f      //4倍圆周率
#define UNITY_INV_PI        0.31830988618f       //圆周率的倒数
#define UNITY_INV_TWO_PI    0.15915494309f       //2倍圆周率的倒数
#define UNITY_INV_FOUR_PI   0.07957747155f       //4倍圆周率的倒数
#define UNITY_HALF_PI       1.57079632679f       //半圆周率
#define UNITY_INV_HALF_PI   0.636619772367f      //半圆周率的倒数

123456789101112
```

## 4、与颜色空间相关

| 函数名 | 描述 |
| --- | --- |
| bool IsGammaSpace() | 根据宏UNITY_COLORSPACE_GAMMA是否被启用了，判断当前是否启用了伽马颜色空间。 |
| float GammaToLinearSpaceExact (float value) | 把一个颜色值精确地从伽马颜色空间(sRGB颜色空间)变化到线性空间(CIE-XYZ颜色空间)。 |
| half3 GammaToLinearSpace (half3 sRGB) | 用一个近似模拟的函数把颜色值近似地从伽马空间变换到线性空间。 |
| float LinearToGammaSpaceExact (float value) | 把一个颜色值精确地从线性空间变换到伽马颜色空间。 |
| half3 LinearToGammaSpace (half3 linRGB) | 用一个近似模拟的函数把颜色值近似地从线性空间变换到伽马颜色空间。 |

# 三、着色器其他特殊语义

## 1、屏幕空间像素位置：VPOS

片元着色器可以接收渲染为特殊 VPOS 语义的像素的位置。 此功能仅从着色器模型 3.0 开始存在，因此着色器需要具有 #pragma target 3.0 编译指令。
在不同的平台上，屏幕空间位置输入的基础类型会有所不同，因此为了获得最大的可移植性，请对其使用 UNITY_VPOS_TYPE 类型（在大多数平台上将是 float4，在 Direct3D 9 上将是 float2）。
另外，使用像素位置语义将导致难以让裁剪空间位置 (SV_POSITION) 和 VPOS 处于相同的顶点到片元结构中。因此顶点着色器应将裁剪空间位置输出为单独的“out”变量。请参阅以下示例着色器：

```
Shader "Unlit/Screen Position"
{
    Properties
    {
        _MainTex ("Texture", 2D) = "white" {}
    }
    SubShader
    {
        Pass
        {
            CGPROGRAM
            #pragma vertex vert
            #pragma fragment frag
            #pragma target 3.0

            // 注意：此结构中没有 SV_POSITION
            struct v2f {
                float2 uv : TEXCOORD0;
            };

            v2f vert (
                float4 vertex : POSITION, // 顶点位置输入
                float2 uv : TEXCOORD0, // 纹理坐标输入
                out float4 outpos : SV_POSITION // 裁剪空间位置输出
                )
            {
                v2f o;
                o.uv = uv;
                outpos = UnityObjectToClipPos(vertex);
                return o;
            }

            sampler2D _MainTex;

            fixed4 frag (v2f i, UNITY_VPOS_TYPE screenPos : VPOS) : SV_Target
            {
                // screenPos.xy 将包含像素整数坐标。
                // 使用它们来实现一个跳过渲染 4x4 像素块的
                // 棋盘图案

                // 棋盘图案中 4x4 像素块的 checker 值
                // 为负
                screenPos.xy = floor(screenPos.xy * 0.25) * 0.5;
                float checker = -frac(screenPos.r + screenPos.g);

                // 如果值为负，则 clip HLSL 指令停止渲染像素
                clip(checker);

                // 对于保留的像素，读取纹理并将其输出
                fixed4 c = tex2D (_MainTex, i.uv);
                return c;
            }
            ENDCG
        }
    }
}
1234567891011121314151617181920212223242526272829303132333435363738394041424344454647484950515253545556
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201009102228758.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTI3MjI1NTE=,size_16,color_FFFFFF,t_70#pic_center)

## 2、面对方向：VFACE

片元着色器可以接收一种指示渲染表面是面向摄像机还是背对摄像机的变量。这在渲染应从两侧可见的几何体时非常有用 - 通常用于树叶和类似的薄型物体。VFACE 语义输入变量将包含表示正面三角形的正值，以及表示背面三角形的负值。

此功能从着色器模型 3.0 开始才存在，因此着色器需要具有 #pragma target 3.0 编译指令。

```
Shader "Unlit/Face Orientation"
{
    Properties
    {
        _ColorFront ("Front Color", Color) = (1,0.7,0.7,1)
        _ColorBack ("Back Color", Color) = (0.7,1,0.7,1)
    }
    SubShader
    {
        Pass
        {
            Cull Off // 关闭背面剔除

            CGPROGRAM
            #pragma vertex vert
            #pragma fragment frag
            #pragma target 3.0

            float4 vert (float4 vertex : POSITION) : SV_POSITION
            {
                return UnityObjectToClipPos(vertex);
            }

            fixed4 _ColorFront;
            fixed4 _ColorBack;

            fixed4 frag (fixed facing : VFACE) : SV_Target
            {
                // 正面的 VFACE 输入为正，
                // 背面的为负。根据这种情况
                // 输出两种颜色中的一种。
                return facing > 0 ?_ColorFront : _ColorBack;
            }
            ENDCG
        }
    }
}
12345678910111213141516171819202122232425262728293031323334353637
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201009102408892.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTI3MjI1NTE=,size_16,color_FFFFFF,t_70#pic_center)

## 3、顶点 ID：SV_VertexID

顶点着色器可以接收具有“顶点编号”（为无符号整数）的变量。当您想要从纹理或 ComputeBuffers 中 获取额外的每顶点数据时，这非常有用。

此功能从 DX10（着色器模型 4.0）和 GLCore/OpenGL ES 3 开始才存在，因此着色器需要具有 #pragma target 3.5 编译指令。

```
Shader "Unlit/VertexID"
{
    SubShader
    {
        Pass
        {
            CGPROGRAM
            #pragma vertex vert
            #pragma fragment frag
            #pragma target 3.5

            struct v2f {
    			fixed4 color : TEXCOORD0;
                float4 pos : SV_POSITION;
            };

            v2f vert (
                float4 vertex : POSITION, // 顶点位置输入
                uint vid : SV_VertexID // 顶点 ID，必须为 uint
                )
            {
                v2f o;
                o.pos = UnityObjectToClipPos(vertex);
                // 基于顶点 ID 输出时髦颜色
                float f = (float)vid;
                o.color = half4(sin(f/10),sin(f/100),sin(f/1000),0) * 0.5 + 0.5;
                return o;
            }

            fixed4 frag (v2f i) : SV_Target
            {
    			return i.color;
            }
            ENDCG
        }
    }
}

1234567891011121314151617181920212223242526272829303132333435363738
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201009102529315.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTI3MjI1NTE=,size_16,color_FFFFFF,t_70#pic_center)

参考文献：<https://developer.download.nvidia.cn/cg/index_stdlib.html>
转载自：[enter description here](https://blog.csdn.net/u012722551/article/details/103926660)

