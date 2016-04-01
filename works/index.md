title: 关于几种数组的常见算法
date: 2016-01-17 21:30:14
categories:
  - web前端
  - JS
tags:
  -数组算法
摘要:
  - 数组降维，数组去重，数组出现最多的元素几个数
---

摘要：数组降维，数组去重，数组出现最多的元素几个数
<!--more-->

---
### 数组降维
* 方法1：循环嵌套
```
	Array.prototype.reduceDimension=function(){
			//遍历当前二维数组,同时创建结果数组
			for(var r=0,result=[];r<this.length;r++){
				for(var c=0;c<this[r].length;c++){
					//向结果数组中压入当前元素
					result.push(this[r][c]);
				}
			}
			return result;//遍历结束后，返回结果数组
   	}
```
* 方法2：单层循环
```
	Array.prototype.reduceDimension=function(){
      for(var r=0,result=[];r<this.length;r++){
        result=result.concat(this[r]);
      }
    }
```
* 方法3：不用循环
```
	Array.prototype.reduceDimension=function(){
      var result=[];
return Array.prototype.concat.apply(result,this);
    }

	var data=[
		[0,0,0,0],
		[0,0,0,0],
		[0,0,0,0],
		[0,0,0,0],
	];
	console.log(data);
	data=data.reduceDimension();
	console.log(data);
```
### 掉数组中的重复元素
```
function removerepeat(arr){
		var temp={};
		for(var i=0;i<arr.length;i++){
			temp[arr[i]]=true;
		}
		console.log(temp);
		var r=[];
		for(var k in temp){
			r.push(k);
		}
		return r;
	}
	var r=removerepeat(['a','d','d','c','h','f','b']);
	//console.log(r);
```
### 算出数组出现最多的元素及个数

```
function num(arr){
		var count=1;
		var yuansu=[];//存放数组中的每个不同的元素
		var sum=[]; //存放不同元素出现的个数
		for(var i=0;i<arr.length;i++){
			for(var k=i+1;k<arr.length;k++){
				if(arr[i]==arr[k]){
					count++;  //用来计算当前元素的相同个数
					arr.splice(k,1);
					k--;  // 把k留在原地
					
				}

			}
			yuansu[i]=arr[i];//将当前的元素放到yuansu数组中
			sum[i]=count;// 并将当前多少个这样的元素的数目放到sum数组中
			count=1; //再将count重新赋值，进入下个元素上的判断
		}
		//算出不同元素出现的个数
		var str='';
		for(var i=0;i<yuansu.length;i++){
			//console.log(yuansu);
			//console.log(yuansu.length);
			str+=yuansu[i]+"出现的次数为："+sum[i]+'; ';
		}
		//console.log(str);
		var newsum=[];
		for(var key in sum){
			newsum[key]=sum[key];
		}
		//console.log(newsum);
		newsum.sort();//考虑浏览器兼容性，需自定义sort方法，这里不当重点
		var first='';// 存放出现最最多的元素
		var fcount=0;//计算出现次数最多的元素总共有所少个
		for(var i=0;i<sum.length;i++){
			if(sum[i]==newsum[newsum.length-1]){
				first+="出现最多的元素是:"+yuansu[i]+";次数为:"+sum[i];
				fcount++;
			}
		}
		document.write("出现元素最多的元素有"+fcount+"个<br/>"+first)
	}
	num([10,20,10,10,30,20,54,15,58,15,12,15]);//测试代码
```