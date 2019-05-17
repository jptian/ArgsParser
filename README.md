```
//模拟输入命令行参数
        String cmdLine = "-arg1 1111 -arg3 2222 3333 -sum 1 2";
 //打印
  -sum
    1
    2
  -arg3
    2222
    3333
  -arg1
    1111
  SUM= 3
``` 
  
```
package cn.jptian.utils.args;

import java.util.ArrayList;
import java.util.HashMap;

public class Main {
    private static HashMap<String, String[]> parseArgs(String[] args) {
        HashMap<String, String[]> tmp = new HashMap<String, String[]>();
        ArrayList<String> arrValue = new ArrayList<>();
        String name = null;
        for (int i = 0; i < args.length; i++) {
            String arg = args[i];
            if (arg.startsWith("-")) {
                if (name != null) {
                    String[] argsValue = new String[arrValue.size()];
                    arrValue.toArray(argsValue);
                    tmp.put(name, argsValue);
                    arrValue.clear();
                }
                name = arg;
            } else {
                arrValue.add(arg);
            }
        }

        if (name != null) {
            String[] argsValue = new String[arrValue.size()];
            arrValue.toArray(argsValue);
            tmp.put(name, argsValue);
            arrValue.clear();
        }
        return tmp;
    }

    public static void main(String args[]) {
        //模拟命令行参数
        String cmdLine = "-arg1 1111 -arg3 2222 3333 -sum 1 2";
        args = cmdLine.split(" ");

        HashMap<String, String[]> parseArgs = parseArgs(args);
        for (String key : parseArgs.keySet()) {
            System.out.println(key);//打印参数名称

            String[] strings = parseArgs.get(key);
            for (String param : strings) {//打印参数值
                System.out.println("\t" + param);
            }
        }

        //使用示例
        if (parseArgs.containsKey("-sum")) {
            String[] vals = parseArgs.get("-sum");
            int i = 0;
            for (String item : vals) {
                i += Integer.parseInt(item);
            }
            System.out.println("SUM= " + i);
            return;
        }
    }
}

```
