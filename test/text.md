# 密码学基础作业

## 凯撒密码

凯撒密码：凯撒密码属于古典密码的一种，通过将明文中所使用的的字母表按照一定的字数“平移”来进行加密。<br>
**举个栗子**<br>
对liming进行加密，密钥是3。<br>
为了便于区分，我们用小写字母表示明文，用大写字母小时密文。<br>
*加密过程*<br>
l->O;<br>
i->L;<br>
m->P;<br>
n->Q;<br>
g->M;<br>
所以加密结果是：OLPLQM.<br>
凯撒密码的解密就是将密文字母按字母表顺序反向平移3个字母。<br>
在知道密钥的情况下，破译凯撒密码是非常简单的。当不知道密钥时，可以采用暴力破解的方式来破译密码。<br>
**比如**：凯撒密码的秘钥其实就都是字母平移的位数，字母表只有26个字母，那么秘钥也就只有0-25共26个秘钥（平移0个字母相当于没有加密）。暴力破解就是按照顺序把26个秘钥都试一遍，当然这些我们可以借助工具来完成。<br>
**加密代码**
```C
#include <stdio.h>
#include <conio.h>
 int main(){
 int key;
 char mingma,mima;
 printf("\nPlease input the character:");
 scanf("%c",&mingma); //输入明码
 printf("\nPlease input the key:");
 scanf("%d",&key); //输入秘钥
 if((mingma>='A')&&(mingma<='Z'))
  mima='A'+(mingma-'A'+key)%26; //大写字母移位
 else if((mingma>='a')&&(mingma<='z'))
  mima='a'+(mingma-'a'+key)%26; //小写字母移位
 printf("\n The output is:%c",mima); //输出密码
 printf("\nFinished!\n");
 getch();
 return 0;
}
```
## 栅栏密码
栅栏密码：就是把要加密的明文分成N个一组，然后把每组的第1个字，第二个字，第三个字。。。。连起来，形成一段无规律的话。不过栅栏密码本身有一个潜规则，就是组成栅栏的字母一般不会太多。<br>
**再举个栗子**
明文：guan guan ju jiu zai he zhi zhou;<br>
去掉空格分成两两一组（2栏的栅栏加密）：gu an gu an ju ji uz ai he zh iz ho u ;最后一组不足两个可以补上任意字母或空格。<br>

