# Counter
在完成基本的加减乘除运算成功能基础上，对程序进行重构，当用户选择加法操作时，可以对输入的两个字符串进行连接运算；当用户选择减法操作时，可以从用户输入的第一个字符串中去除第二个字符串。
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace ConsoleApplication11
{
    abstract class Add
    {
       private double _numb1;//数1
       public double Numb1
       {
       get { return _numb1; }
       set { _numb1 = value; }
        }
       private double _numb2;//数2
       public double Numb2
       {
           get { return _numb2; }
           set { _numb2 = value; }
       }
       private String stringnumb1;//字符串1

       public String Stringnumb1
       {
           get { return stringnumb1; }
           set { stringnumb1 = value; }
       }
       private String stringnumb2;//字符串2
       public String Stringnumb2
       {
           get { return stringnumb2; }
           set { stringnumb2 = value; }
       }
       private double doubleResult;//数字结果
       public double DoubleResult
       {
           get { return doubleResult; }
           set { doubleResult = value; }
       }
       private String stringResult;//字符串结果
       public String StringResult
       {
           get { return stringResult; }
           set { stringResult = value; }
       }
        public abstract void Adds();//加
        public abstract void Subs();//减
    }
}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Text.RegularExpressions;

namespace ConsoleApplication11
{
class Cou:Add
    {
        private int num1;//数1
        private int num2;//数2
        private char oper;//运算符
        public static bool flagbool;
        public int flagoper;
        public int Num1
        {
            get { return num1; }
            set { num1 = value; }
        }
        public int Num2
        {
            get { return num2; }
            set { num2 = value; }
        }
        public char Oper
        {
            get { return oper; }
            set { oper = value; }
        }
        public static bool IsNumeric(string value)//判断一个数是否为整数
        {
            Regex regex = new Regex("^[0-9]*$");
            flagbool = Regex.IsMatch(value, @"^[+-]?\d*[.]?\d*$");
            return flagbool;
        }

        public void output()
        {
            oper = Convert.ToChar(Console.ReadLine());
            Console.WriteLine("请输入一个数字或者字符串：");
            String input1 = Console.ReadLine();
            Console.WriteLine("请再输入一个数字或者字符串：");
            if (IsNumeric(input1))
            {
                //执行数字的程序
                flagoper = 1;
                Numb1 = Convert.ToInt32(input1);
                Numb2 = Convert.ToInt32(Console.ReadLine());
            }
            else
            {
                //执行字符串的程序
                flagoper = 2;
                Stringnumb1 = input1;      
                Stringnumb2 = Console.ReadLine();  
            }      
        }     
        public void Count()
        {               
            if (oper == '*')
            Console.WriteLine(Mul());
            else if (oper == '/')
                Console.WriteLine(Div());
        }
        public bool Equals(int a, int b)
        {
            if (a == b) return true;
            else return false;
        }
        //*&/
        public double Mul()
        {
            return Numb1 * Numb2;
        }

        public double Div()
        {
            return Numb1 / Numb2;
        }

        public override void Adds()
        {
            DoubleResult = Numb1 + Numb2;
            Console.WriteLine(DoubleResult.ToString());
        }

        public override void Subs()
        {
            DoubleResult = Numb1 - Numb2;
            Console.WriteLine(DoubleResult.ToString());
        }
    }
}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace ConsoleApplication11
{
    class Sco:Add//字符串结果
    {
         public override void Adds()
        {
            StringResult = Stringnumb1 + Stringnumb2;
            Console.WriteLine(StringResult.ToString());
        }

        public override void Subs()
        {
            StringResult = Stringnumb1.Replace(Stringnumb2, "");//去掉原字符中Stringnumb2字符
            Console.WriteLine(StringResult);
        }
    }

}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace ConsoleApplication11
{
    class Program
    {
        static void Main(string[] args)
        { 
            Console.WriteLine("请输入+ - * / 中任意一个符号：");
            Cou cou= new Cou();         
            Sco sc = new Sco();
            cou.output();          
            sc.Stringnumb1 = cou.Stringnumb1;
            sc.Stringnumb2 = cou.Stringnumb2;
            Console.WriteLine("结果为：");
            cou.Count();        
            if (cou.Oper == '+' && cou.flagoper == 1)
                cou.Adds();
            if (cou.Oper == '+' && cou.flagoper == 2)
                sc.Adds();

            if (cou.Oper== '-' && cou.flagoper == 1)
                cou.Subs();
            if (cou.Oper == '-' && cou.flagoper == 2)
            {
                sc.Subs();
            }
            Console.ReadLine();
        }
    }
}

