### 01_ Simple_encryption
+ 直接看到主逻辑 

 

:::color2
  for ( j = 0; j < len; ++j )

  {  if ( !(j % 3) )

      input[j] -= 31;

    if ( j % 3 == 1 )

      input[j] += 41;

    if ( j % 3 == 2 )

      input[j] ^= 0x55u;  }

:::

+ 在对比   input[k] != buffer[k]
+ 点击buffer得到  47 95 34 48 A4 1C 35 88  64 16 88 07 14 6A 39 12

A2 0A 37 5C 07 5A 56 60  12 76 25 12 8E 28 

+ 写解密

:::color2
#include <stdio.h>



int main() {   //h->0x

    char  arr[]{ 0x47, 0x95, 0x34, 0x48, 0xA4, 0x1C, 0x35, 0x88, 0x64, 0x16,

  0x88, 0x07, 0x14, 0x6A, 0x39, 0x12, 0xA2, 0x0A, 0x37, 0x5C,

  0x07, 0x5A, 0x56, 0x60, 0x12, 0x76, 0x25, 0x12, 0x8E, 0x28 };

    int len = sizeof(arr) / sizeof(char);

    

    for (int j = 0; j<len;j++)

    {

        if (!(j % 3))

            arr[j] += 31;

        if (j % 3 == 1)

            arr[j] -= 41;

        if (j % 3 == 2)

            arr[j] ^= 0x55u;



     }

    for (int j = 0; j < len; j++) {

        printf("%c", arr[j]);

    }

    //      flag{IT_15_R3Al1y_V3Ry-51Mp1e}

 

    return 0;

}

:::

---

### 02_Base64
+ 输出 result
+ result = sub_14000EF40((unsigned int)dword_140014028, qword_140014020);
+ 主逻辑 if ( strlen(Str) == 26 && (sub_1400014E0(Str, 26LL, Str1), !strcmp(Str1, "g84Gg6m2ATtVeYqUZ9xRnaBpBvOVZYtj+Tc=")) )
+ 编译结果知道，看编译规则 

:::color2
v17[0] = (v14 >> 2) | (((unsigned __int8)((v15 >> 4) + ((16 * v14) & 0x30)) | (((unsigned __int8)((v16 >> 6) + ((4 * v15) & 0x3C)) | ((v16 & 0x3F) << 8)) << 8)) << 8);

      for ( i = 0LL; i != 4; ++i )

        a3[i] = aWhydo3sthis7ab[*((unsigned __int8 *)v17 + i)];

      a3 += 4;

      v6 = 0;

    }

:::

:::color2
aWhydo3sthis7ab db 'WHydo3sThiS7ABLElO0k5trange+CZfVIGRvup81NKQbjmPzU4MDc9Y6q2XwFxJ/',0

:::

+ 解题

:::color2
//  3—8  --> 4-6

// 编码对应则'WHydo3sThiS7ABLElO0k5trange+CZfVIGRvup81NKQbjmPzU4MDc9Y6q2XwFxJ/'

// 编码后结果为g84Gg6m2ATtVeYqUZ9xRnaBpBvOVZYtj+Tc=

#include <stdio.h>

#include <string.h>

#include <stdlib.h>



const char Compre[] = "WHydo3sThiS7ABLElO0k5trange+CZfVIGRvup81NKQbjmPzU4MDc9Y6q2XwFxJ/";

int arr[256] = { 0 };   



// 初始化 

void init_table() {

    memset(arr, -1, sizeof(arr));

    for (int i = 0; i < 64; i++) {

        arr[(unsigned char)Compre[i]] = i;

    }

    arr['='] = 0;

}



void decode(const char* in, unsigned char* out, int* out_len) {   

    init_table();

    int i = 0, j = 0;

    while (in[i] && in[i] != '=') {

        int d[4] = {

            arr[(unsigned char)in[i++]],

            arr[(unsigned char)in[i++]],

            arr[(unsigned char)in[i++]],

            arr[(unsigned char)in[i++]]

        };

        out[j++] = (d[0] << 2) | (d[1] >> 4);

        out[j++] = (d[1] << 4) | (d[2] >> 2);

        out[j++] = (d[2] << 6) | d[3];

    }

    *out_len = j;

}



int main() {

    // 待解密字符串

    const char* encoded = "g84Gg6m2ATtVeYqUZ9xRnaBpBvOVZYtj+Tc=";

    unsigned char out[128] = { 0 };

    int len = 0;

     

    decode(encoded, out, &len);

    printf("%s\n", out);

     // flag{y0u_kn0w_base64_well}

    return 0;

:::

### 03-Begin
+ 题干 flag  
+ 找trcpy          A                 flag_part1      flag{Mak3_aN_',0  
+ 再根据提示， Shift+F12    	  flag part2: 3Ff0rt_tO_5eArcH_  

               

+ 根据提示 Format     找到printf    flag part3: F0r_th3_f14g_C0Rpse 

:::color2
flag{ Mak3_aN_

 3Ff0rt_tO_5eArcH_

 F0r_th3_f14g_C0Rpse    }

flag{Mak3_aN_3Ff0rt_tO_5eArcH_F0r_th3_f14g_C0Rpse} 

:::

#### 04 ezAndroidStudy
+ 题

:::color2
 题干自己把flag在哪描述的比较详细

:::

+ AndroidManifest.xml    package = "work.pangbai.ezandroidstudy"

      android:name = "work.pangbai.ezandroidstudy.MainActivity"

      android:name = "work.pangbai.ezandroidstudy.Homo" 

+  

           MainActivity  无

           Homo          flag{Y0u

+ 根据提示  res  resources.arsc:/res/values/strings.xml            flag2: _@r4  
+   res/layout/activity_main.xml                       flag3: _900d
+ //  lib              _r4V4rs4r
+ flag{Y0u_@r4_900d_andr01d_r4V4rs4r}

:::color2
先看   AndroidManifest.xml  

llib/     ibezandroidstudy.so

res/       res/layout/       res/raw/   res/xml/   res/navigation/ 

resources.arsc   res/values/strings.xml

:::

### 05 **<font style="color:rgb(0, 0, 0);">ez_debug</font>**
+   找主逻辑
+ 给you 函数下断点  看寄存器变化和函数执行步骤
+ 单步运行循环过完之后，直接双击 `v5`，查看变量 
+ flag {y0u_ ar3__g0od__@_ Debu9}

:::color2
这里我有问题，断点下的位置不同，有时直接就卡退报出一堆中文乱码；只

:::

