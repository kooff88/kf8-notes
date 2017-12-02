# 结构体指针作为函数参数

结构体变量名代表的是整个集合本身，作为函数参数时传递的整个集合，也就是所有成员，儿不是像数组一样  
被换成一个指针。如果结构体成员较多，尤其是成员为数组时，传递的时间和空间开销会很大，影响程序的  
运行效率。所以最好的办法就是使用结构体指针，这时由实参传向形参的只是一个地址，非常快速。  

```
#include<stadio.h>
struct stu{
   char *name;
   int score;
} stus[]={
    {"zhangsan1",65},
    {"zhangsan2",98}
};

void averge(struct stu *,int);
int main(){
    int len=sizeof(stus)/sizeof(struct stu);
    printf("start...\n");
    // 数组名可以认为是一个指针
    averge(stus,len)
}

void averge(struct stu *stus,int len){
  char *name;
  int score;
  int sum=0;
  for(int i=0;i<len;i++){
     name=stus[i].name; // 第一种形式
     score=(*(stus+i)).score; // 第二种形式
     sum += score;
     printf("%s...%d \n",name,score);
  }

  printf("平均分:%d...\n",sum/len);
}


```
