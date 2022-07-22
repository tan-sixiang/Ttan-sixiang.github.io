# 异常

````java
 Java中Exception又分为2种异常类型

一. RuntimeException  不受检测异常(不太严重的问题)，就算是有这种发生问题的可能性，既不要try-catch，也不需要throws
二. 非RuntimeException的子类  受检测异常（较为严重的问题)，编译器强制要求开发人员面对这个问题:
1、自己来处理，编写try-catch
2、自己不处理，在方法上添加throwS XxxException，它的用意是告诉调用这个方法的人，这个方法会有发生错误的风险，你需要注意

throw 用来手工抛出异常
throws 用来声明该方法可能会发生异常
````

案例:自己创建异常类型并调用:

````java
 public static void main(String[] args) throws Exception {
		String[] arr = {"a", "bxx", "c"};
     	List<String> errors = batchValidate(arr);
     
private static List<String> batchValidate(String[] arr) {
        List<String> errors = new ArrayList<>();
        for (String s : arr) {
            try {
                validateItem(s); // bxx抛出了一个错误
                saveItem(s);
            } catch (Exception e) { // 如果try里面发生的错误，是参数声明的类型，就会执行catch中的逻辑
                // 判断错误的性质
                if(e instanceof NetworkRuntimeException){
                    errors.add(e.getMessage());
                }
                if(e instanceof ValidateRuntimeException){
                    errors.add(e.getMessage());
                }
                e.printStackTrace();
            }
        }
        System.out.println("批量校验完毕！");
        return errors;
    }

    static int count;
    static void saveItem(String s) {
        if (count++ == 1) throw new NetworkRuntimeException("网络链接错误");
        System.out.println("把视频保存起来");
        // 网络连接的问题
    }
    private static void validateItem(String s) { // 踢皮球
        if (s.length() > 1) {
            throw new ValidateRuntimeException("字符串长度不符合要求");
            // System.out.println("不符合要求");
        } else {
            System.out.println(s + "是合乎要求的");
        }
    }

class ValidateRuntimeException extends RuntimeException{
    ValidateRuntimeException(String msg) {
        super(msg);
    }
}
class NetworkRuntimeException extends RuntimeException{
    NetworkRuntimeException(String msg) {
        super(msg);
    }
}
````

