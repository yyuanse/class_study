# class_study
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------
2023.2.27
课堂练习01题目:计算最长英语单词链。
一、题目内容：
大家经常玩成语接龙游戏，我们试一试英语的接龙吧：一个文本文件中有N 个不同的英语单词， 我们能否写一个程序，
快速找出最长的能首尾相连的英语单词链，每个单词最多只能用一次。
最长的定义是：最多单词数量，和单词中字母的数量无关。
二、总结：
问题很多，掌握的知识太少了，很多都不会怎么处理好，以下代码也只是在我这个txt文件才能成功执行，而且我是直接
从第一个单词开始算的，并没有全部遍历，找出最长的单词接龙链。
input文件：
output文件：
控制台输出：
代码：
import java.io.*;
import java.util.Map;
import java.util.TreeMap;

public class class_test {
    public static void main(String[] args) throws IOException {

//        //写入操作
//        try{
//            BufferedReader bufferedReader = new BufferedReader(new FileReader("D:\\input1.txt"));
//            String b = null;
//            FileWriter fileWriter = new FileWriter("D:\\output1.txt",true);
//            while(( b = bufferedReader.readLine()) != null){
//                System.out.println(b);
//                fileWriter.write(b+'\n');
//            }
//            fileWriter.close();
//            bufferedReader.close();
//        }catch (IOException exception){
//            System.out.println(exception);
//        }

        File file = new File("D:\\input1.txt");
        FileWriter fileWriter = new FileWriter("D:\\output1.txt",true);
        try {
            FileReader fr = new FileReader(file);
            BufferedReader bufr = new BufferedReader(fr);
            //按行读取返回的字符串
            String s = null;
            //将所有s字符串拼接
            String all = "";
            while ((s = bufr.readLine()) != null) {
                all = all + s;
            }
            String[] strs = all.split("[^a-zA-Z0-9]");
            int[] n = new int[26];
            for(int i=0;i<26;i++) n[i]=0;
            String[][] r1 = new String[26][strs.length];//存数组按照开头存
//            String[][] r2 = new String[strs.length][strs.length];//按照尾存
            Map<String, Integer> tm = new TreeMap<>();//
            for (int i = 0; i < strs.length; i++) {
                if (!tm.containsKey(strs[i])) {//用来判断map中是否有key值，是否出现过。
                    tm.put(strs[i], 0);//key,value:单词，readed
//                    String start,end;
//                    start = strs[i].substring(0,1);
//                    end = strs[i].substring(strs[i].length()-1,strs[i].length());
                    char[] chs = strs[i].toCharArray();
                    //试着先输出以下看看结果
                    r1[chs[0] - 'a'][n[chs[0] - 'a']++] = strs[i];
//                    r2[chs[strs[i].length() - 1] - 'a'][n[chs[strs[i].length() - 1] - 'a']] = strs[i];
                }
            }
            String rs = "";
            String str = strs[0];
            rs+=str;
            tm.put(str,1);
            while(true) {
                int i=0;
                char[] c = str.toCharArray();
                char ch = c[str.length() - 1];
                for ( i = 0; i < n[ch - 'a']; i++) {
                    String str1 = r1[ch - 'a'][i];
                    if (tm.get(str1) == 0) {
                        tm.put(str1, 1);
                        rs += " " + str1;
                        str = str1;
                        break;
                    } else {
                        continue;
                    }
                }
                if(i>=n[ch-'a'])break;
            }
//            while(tm.get(str) == 0){
//                rs += str;
//                tm.put(str,1);
//                char[] c = str.toCharArray();
//                char ch = c[str.length() - 1];
//                for (int i = 0; i < n[ch - 'a']; i++) {
//                    String str1 = r1[ch - 'a'][i];
//                    if (tm.get(str1) == 0) {
//                        tm.put(str1,1);
//                        rs += " "+ str1;
//                        str=str1;
//                        break;
//                    } else {
//                        continue;
//                    }
//                }
//            }
            System.out.println("最长单词链为："+rs);
            fileWriter.write(rs+'\n');
            fileWriter.close();
            bufr.close();
            fr.close();
        } catch(Exception e){
        e.printStackTrace();
    }

    }

}

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
