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
       
       
       
       
              
              
  
        
        
    
    
