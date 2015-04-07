title: "java数组基础"
date: 2015-04-05 11:32:22
tags:
categories: j2se

---


数组概念：具有相同类型的数据的集合


数组定义：

```
type [] name = new type[数组个数];
```
数组定义时直接初始化：
```
type[] name = new type[]{1,2,3,4,5};
//上面行中的第二个 new type[]部分可以省略，所以又有两种：
int a ={1,2,3};
int a = new int[]{1,2,3};//第二个方括号中不能加上数组长度，因为元素个数是由后面花括号的内容决定的。
```

数组长度：
```
length，注意不是length();
```

声明数组：
```
String[] a = new String[3];
String[] b = {"a","b","c"};
String[] c = new String[]{"a","b","c"};
```

输出数组：
```
int i ={1,2,3};
String a = Arrays.toString(i);
System.out.prinlt(a);//[1,2,3,4,5]
```

从一个数组创建数组List
```
int[] a ={1,2,3,4,5};
List<Integer> arraylist = new ArrayList<Integer>(Arrays.asList(a));
system.out.println(arraylist);//[1,2,3,4,5]
```

检查一个数组是否包含某个值：
```
String[]  a = {"a","b","c"};
boolean b = Arrays.asList(a).contains("a");//true
```

连接两个数组：
```
int[] a = {1,2,3,4};
int[] b = {5,6,7,8};
int[] c = ArrayUtils.addAll(a,b);
```

把提供的数组元素放入一个字符串：
```
String a =StringUtils.join(new String[]{"a","b","c"},",");//a,b,c
```

数组比较：
```
int[] a = {1,2,3};
int[] b = {1,2,3};
a.equals(b);//false
```
如何比较：
```
ArrayEqualsTest.java 
import java.util.Arrays;
public class ArrayEqualsTest{
    public static boolean isEquals(int[] a, int[] b){
        if( a == null || b == null ){ 
            return false;
        }
        if(a.length != b.length) {
            return false;
        }
        for(int i = 0; i < a.length; ++i ){            
        	if(a[i] != b[i]){
                return false;
            }
        }
        return true;
    }
    public static void main(String[] args){   
    	int[] a = {1, 2, 3};
        int[] b = {1, 2, 3};
        System.out.println(isEquals(a,b));
        System.out.println(Arrays.equals(a,b));
    }
}
```
