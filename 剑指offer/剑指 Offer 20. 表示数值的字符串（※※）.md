剑指 Offer 20. 表示数值的字符串

请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100"、"5e2"、"-123"、"3.1416"、"-1E-16"、"0123"都表示数值，但"12e"、"1a3.14"、"1.2.3"、"+-5"及"12e+5.4"都不是。

通过次数34,083提交次数147,603


```java
class Solution {
    public boolean isNumber(String s) {
        // 1. 预处理，去除两端空格，将字符串转为小写（E->e）
        s = s.trim();
        if(s.length() == 0){
            return false;
        }
        s = s.toLowerCase();

        // 2. 分为有无指数两种情况
        int ei = s.indexOf("e");

        // 2.1 有指数
        if(ei != -1){
            // 以e为基准分割出两个字符串
            if(ei == 0 || ei == s.length() - 1){
                return false;
            }
            String nl = s.substring(0, ei);
            String nr = s.substring(ei + 1, s.length());

            // 特殊情况，e的指数不能是小数
            if(nr.indexOf('.') != -1){
                return false;
            }
            // 分别判断指数左右数字是否合法
            if(!canParseVal(nl) || !canParseVal(nr)){
                return false;
            }
        }
        // 2.2 无指数
        else{
            return canParseVal(s);
        }
        return true;
    }

    /**
     * 判断数字字符串是否合法
     * @param num
     * @return
     */
    private boolean canParseVal(String num){
        int dotCount = 0;   // 记录小数点的个数
        int numCount = 0;   // 记录数字出现的个数
        for(int i = 0; i < num.length(); ++i){
            char ch = num.charAt(i);
            if(ch == '+' || ch == '-'){
                // 如果出现的是+、-但不是在字符串开始，则非法
                if(i != 0){
                    return false;
                }
            }
            else if(ch == '.'){
                // 如果出现的是小数点，则对小数点出现的次数进行统计，超过一个则非法
                ++dotCount;
                if(dotCount > 1){
                    return false;
                }
            }
            else if(ch < '0' || ch > '9'){
                // 出现了非法字符
                return false;
            }
            else{
                // 出现了数字
                ++numCount;
            }
        }
        // 如果遍历结束发现没有出现数字，则非法，如"-."
        if(numCount == 0){
            return false;
        }
        return true;
    }
}
```