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
g->J;<br>
所以加密结果是：OLPLQJ.<br>
凯撒密码的解密就是将密文字母按字母表顺序反向平移3个字母。<br>
在知道密钥的情况下，破译凯撒密码是非常简单的。当不知道密钥时，可以采用暴力破解的方式来破译密码。<br>
**比如**：凯撒密码的秘钥其实就都是字母平移的位数，字母表只有26个字母，那么秘钥也就只有0-25共26个秘钥（平移0个字母相当于没有加密）。暴力破解就是按照顺序把26个秘钥都试一遍，当然这些我们可以借助工具来完成。<br>
**加密代码**
```C
#include <stdio.h>
#include <string.h>

int main()
{
    char passwd[100],encrypted[100];
    int i;
    int k;
    int t;
    int move;
    while(1)
    {
        printf("Enter message to be encrypted:");
        gets(passwd);
        printf("Enter shift amount(0-25):");
        scanf("%d%*c",&move);
        for(i=0; i<strlen(passwd);i++)
        {
            if(passwd[i] >= 'A' && passwd[i] <= 'Z')
            {
                passwd[i] = ((passwd[i]-'A')+move)%26+'A';
            }
            else if(passwd[i] >= 'a' && passwd[i] <= 'z')
            {
                passwd[i] = ((passwd[i]-'a')+move)%26+'a';
            }
        }
        printf("%s",passwd);
        printf("\n");
        break;

    }
    return 0;
}
```
## 置换密码
置换密码又称换位密码，明文和密文的字母相同，但是顺序被打乱。解密方式有点类似于拼图游戏，换位密码的加密方法有很多种。最简单的有单行置换加密，基于数组的置换密码，等等。最简单的置换码就是栅栏密码。<br>
### 栅栏密码
栅栏密码：就是把要加密的明文分成N个一组，然后把每组的第1个字，第二个字，第三个字。。。。连起来，形成一段无规律的话。不过栅栏密码本身有一个潜规则，就是组成栅栏的字母一般不会太多。<br>
**再举个栗子**
明文：guan guan ju jiu zai he zhi zhou;<br>
去掉空格分成两两一组（2栏的栅栏加密）：gu an gu an ju ji uz ai he zh iz ho u ;最后一组不足两个可以补上任意字母或空格。<br>
提取第一个字符：gagajjuahzihu;<br>提取第二个字符：ununuiziehzo;<br>两串字符连接就是密文：gagajjuahzihuununuiziehzo;<br>
**解密**：将密文分成两段：<br>
第一段：gagajjuahzihu<br>
第二段：ununuiziehzo<br>
最后将两串字符交叉连接：guanguanjujiuzaihezhizhou;最后手动插入空格，就可以知道明文的内容了。<br>
除了2栏的栅栏码，还有多栏栅栏码，加解密方法相近，同学们可以自行拓展。<br>

*上述内容只是介绍了最简单的加密方法，各位同学可以自行查找资料,拓展不同的加密形式*

