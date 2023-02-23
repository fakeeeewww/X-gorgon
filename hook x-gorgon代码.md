setImmediate(function() {//设置时间
console.log("[*] Starting script");

    Java.perform(function x() {
        var my_class = Java.use("com.ss.sys.ces.gg.tt$1");//我们hook都是hook的方法，无法hook类，这是在定位方法所在的类。注意内部类的写法
        console.log("Success!");
        my_class.a.implementation = function (arg1,arg2) {//my_class是我们定位的类
            console.log("第40次：");//当你的长代码发生错误时，一定要做好标记，可以在一些恰当的地方打印汉字，作为标记，这样更方便你去定位error的位置
        	console.log("arg1:");//函数参数arg1是一个string类型的，比价简单，直接console.log打印即可
            console.log(arg1);

        	/*var mp =Java.use("java.util.HashMap");//将arg2转化为string类型进行打印
        	var args_2 = Java.cast(arg2, mp);
            console.log("arg2:");
        	send(args_2);*/


            //注意第二个参数是一个Map类型的参数，Map类型是一个键值对集合，因此里面的键值对不止一个，因此要遍历这个集合，可以尝试迭代器interator
            var keyset1=arg2.keySet();//这里调用HashMap的keySet()方法，生成一个由全部key组成的集合
            var it1=keyset1.iterator();//这里调用了迭代器这种方法，it1是一种独特的集合，所生成的集合可以使用iterator的方法
            while(it1.hasNext()){//判断迭代器下一个不是空
                var keystr1 = it1.next().toString();//返回迭代器的下一个元素，并将其转化为string类型
                var valuestr1 = arg2.get(keystr1).toString();//根据key值生成对应的value值，并转化为string类型
                console.log("arg2 map:\t+"+keystr1+valuestr1);
            }
            console.log("\t");//换行
            
            

            
            var map=this.a(arg1,arg2);//这里的this.a()是调用方法，生成对应返回值，返回值为HashMap类型
            var keyset2 = map.keySet();
            var it2 = keyset2.iterator();
            while(it2.hasNext()){
                var keystr2 = it2.next().toString();
                var valuestr2 = map.get(keystr2).toString();
                console.log("result map:\t+"+keystr2+"\t"+valuestr2);
            }
            console.log("\t");
            return this.a(arg1,arg2);//最后还要返回返回值
        };
    });


});

