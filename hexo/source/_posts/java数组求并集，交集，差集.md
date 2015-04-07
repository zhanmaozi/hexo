title: "java数组求并集，交集，差集"
date: 2015-03-31 21:43:04
tags: java
categories: j2se

---
> 
今天上班，下午的时候，不知道什么原因，自己一直不在状态，看着myeclipse在眼前晃悠，大脑怎么都转动不起来，无法聚集精神思考，一个java数组的差集半天想不出来，也懒得谷歌下，真的不想看网页，一点工作状态都没得,想想还是基础太差，之前学的时候以为自己很了解了。看来学了就要用，不会用相当于没学是对的。好了，不扯淡了。

```
//求差集
public static String[] minus(String[] s1,String[] s2){
	LinkedList<String> list = new LinkedList<String>();
	for(String str : s1){
    	if(!list.contains(str)){
        	list.add(str);
        }
    }
    for(String str : s2){
    	if(!list.contains(str)){
        	list.add(str);
        }
    }
    String[] result = {};
    return list.toArray(result);
}

//并集:set无序，不能重复
public static String[] union(Stirng[] s1,String [] s2){
	Set<String> set = new HashSet<String>();
    for(String str:arr1){
            set.add(str);
    }
    for(String str:arr2){
            set.add(str);
    }
    String[] result={};
    return set.toArray(result);
}

//交集(结果集中若使用LinkedList添加，则需要判断是否包含该元素，否则其中会包含重复的元素)
public static String[] intersect(String[] arr1, String[] arr2){
    List<String> list = new LinkedList<String>();
    Set<String> common = new HashSet<String>();
    for(String str:arr1){
        if(!list.contains(str)){
            list.add(str);
        }
    }
    for(String str:arr2){
        if(list.contains(str)){
            common.add(str);
        }
    }
    String[] result={};
    return common.toArray(result);
}

```
