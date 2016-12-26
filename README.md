# regular-expression-1
本文将复习正则表达式的定义、总结正则表达式中的常用方法

一、什么是正则？

正则：也叫规则，让计算机能够读懂人类的规则

正则都是操作字符串的

正则中的默认：是区分大小写的（如果不区分大小写，在正则的最后加标识符i）

二、正则的写法

var re=//;（简写方式）                                           var re=/a/;     
                                              >>>
var re=new RegExp();  （全称写法方式）                           var re=new RegExp('a');

因为简写的性能比全程写法性能要好，所以一般情况下采用简写的方式。但是也有一种特殊的的情况，必须用到全称写法（这里后期再续上）

三、转义字符
eg.\n换行 \r制表 \t回车

   \s空格 \S非空格   
   
   \d数字 \D非数字
   
   \w字符（字母、数字、下划线） \W非字符

四、正则表达式常用方法

(1).正则中的test方法
 
    test:正则去匹配字符串，如果匹配成功返回true,如果匹配失败返回false
    
    test的写法：正则.test(字符串)
    
    example: var str='12345t6789'
        var re=/\D/
        if(re.test(str)){
        
           alert('不全是数字')
        
        }else{
        
           alert('全是数字')
        
        };
        
  (2).正则中的search方法  
      
      search:正则去匹配字符串，如果匹配成功返回匹配成功的位置,如果匹配失败返回-1;
    
      search的写法：字符串.search(正则)
      
      example:var str="abcdef"
              var re=/b/
              str.search(re) //1
                                          
              var str="abcdef"
              var re=/B/




str.search(re) //-1
                            
              如果想达到不区分大小写的效果则在正则的最后加标识符i
              
              var str="abcdef"
              
              var re=/B/i 这一行 也可以写成var re=RegExp("B","i")
              
              str.search(re) //-1
              
              
   (3).正则中的match方法     
   
       match:正则去匹配字符串，如果匹配成功返回匹配成功的数组,如果匹配失败返回null;
       
       match的写法：字符串.match(正则)
       
       example:var str="abc123e5f88gg99ls80";
               
               var re=/\d+/g;// +为量词    量词：匹配不确定的位置   +：至少出现一次
               
               str.match(re);//["123", "5", "88", "99", "80"]
               
               
    (4).正则中的replace方法   
        
        replace:正则去匹配字符串，匹配成功的字符去替换成新的字符串
       
        replace的写法：字符串.replace(正则,新的字符串)
        
        
        example:var str="aaa";
                
                var re=/a/;
                
                str.replace(re,'b')//'baa'
                
                
                var str="aaa";
                
                var re=/a/g;
                
                str.replace(re,'b')//'bbb'
                                
                var str="aaa";
                
                var re=/a+/;
                
                str.replace(re,'b')//'b'
                
                
       example:1.通过replace来做敏感词过滤
       
               
               <html>
               
               <body>
               
               <textarea>
               
               </textarea>
               
               <textarea>
               
               </textarea>
               
               <input id="input1"></input>
               
               </body>
               
               <script>
               
               window.onload=function(){
               
               var aT=document.getElementsByTagName("textarea");
               
               var oInput=document.getElementById("input1");
               
               var re=/非礼宾|南海|中国渔船/g           //  |:或者的意思
               
               oInput.onclick=function(){
               
               aT[1].value=aT[0].value.replace(re,"*")；  //结果被替换的部分无论有几个汉字，都只有一颗*
               
               //解决方案 replace的写法：字符串.replace(正则,新的字符串)   replace()里面，第二个参数可以是字符串，也可以是回调函数；
               
               //  所以aT[1].value=aT[0].value.replace(re,"*")可以等同于 
               
              //   aT[1].value=aT[0].value.replace(re,function(str){ 
              
              //   return '*';   
              
             //    })
                 
                 aT[1].value=aT[0].value.replace(re,function(str){
                 
                 //函数的第一个参数就是:匹配成功的字符，
                 
                 var result="";
                 
                 for(var i=0;i<str.length;i++){
                 
                    result+="*";
                    
                 };
                 
                 return result;//这样就可以做到过滤敏感词的效果
                 
                 }); 
                 
               }
               
               }
               
               </script>
               
               </html>
               
       (5).正则中的小括号的作用
              
              匹配子项：小括号()（还有另外一个意思，分组操作）
              
              把正则的整体叫做(母亲)，然后把左边第一个小括号里面的正则，叫做这个第一个子项（母亲的第一个孩子），
              
              第二个小括号叫做第二个孩子。
              
              var str='2016-08-09';
              
              var re=/(\d+)(-)/g;
              
              str=str.replace(re,function($0,$1,$2){
              
              //第一个参数：$0（母亲），第二个参数：$1（第二个孩子），第三个参数：$2(第三个孩子)
              
              //alert($2);
              
              return $1+'.';
              
              });
              
              
              var str='abc';
              
              var re=/(a)(b)(c)/;
              
              str.match(re);//["abc", "a", "b", "c"]
              
              
              var str='abc';
              
              var re=/(a)(b)(c)/g;
              
              str.match(re);//["abc"]
              
       (6).正则中的字符类     
       
              任意字符   [abc]    例子：a[bcd]e-abc,ace,ade
              
              排除       [^a] ^写在[]里面的话，就代表排除的意思     例子：o[^0-9]t-oat,o?t,o t
              
              范围       [a-z]、[0-9]    例子：id[0-9]-id0,id5
                 
              
              字符类：一组相似的元素，[]中括号的整体代表一个字符
              
              var str='abc';var re=/abc/;re.test(str);    //true

              var str='abc';var re=/a[bss]c/;re.test(str);//true

              var str='abc';var re=/a[efg]c/;re.test(str);//false
              
              var str='abcd';var re=/a[bc]d/;re.test(str);//true
              
              

              
              

              
     
               
                
                
                
       
               
       
       
       
       
       
              
              
  
        
        
    
    
