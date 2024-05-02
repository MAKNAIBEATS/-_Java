# -_Java
тестовое задание Калькулятор_Java
//TIP To <b>Run</b> code, press <shortcut actionId="Run"/> or
// click the <icon src="AllIcons.Actions.Execute"/> icon in the gutter.
import java.net.Inet4Address;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) throws Exception {


        String[] roman_numbers = {"I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX", "X"};
        int[] arabic_numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
        char[] operands = {'+', '-', '*', '/'};

        System.out.println("Р’РІРµРґРёС‚Рµ РїСЂРёРјРµСЂ: ");
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();
        int operator_position = -1;
        int is_roman = 0;
        for (int i = 0;i < operands.length; i++){
            if(operator_position == -1)
                operator_position = s.indexOf(operands[i]);
        }
        if (operator_position == -1)
            Ex("РћРїРµСЂР°С‚РѕСЂ РЅРµ РЅР°Р№РґРµРЅ");

        String sa = "";
        String sb = "";
        String so = "";

        if(operator_position > 0 && s.length() >= 3)
        {
            sa = s.substring(0, operator_position);
            sb = s.substring(operator_position + 1);
            so = s.substring(operator_position, operator_position + 1);
            Integer a = 0;
            Integer b = 0;
            Integer ab = 0;

            if (check_the_numbers(roman_numbers, arabic_numbers, sa) != check_the_numbers(roman_numbers, arabic_numbers, sb))
            {
                Ex("Р Р°Р·РЅС‹Рµ СЃРёСЃС‚РµРјС‹ СЃС‡РёСЃР»РµРЅРёСЏ РЅРµ РґРѕРїСѓСЃС‚РёРјС‹");
            }

            if (check_the_numbers(roman_numbers, arabic_numbers, sa) == 0)
            {
                a = Integer.parseInt(sa);
                b = Integer.parseInt(sb);
            } else {
                is_roman = 1;
                for (int i = 0; i < roman_numbers.length; i++)
                {
                    if (sa.equals(roman_numbers[i]))
                        a = Integer.valueOf(arabic_numbers[i]);
                    if (sb.equals(roman_numbers[i]))
                        b = Integer.valueOf(arabic_numbers[i]);
                }
            }
            ab = Calculate(a, b, so);
            String out_string = s + " = ";
            clearScreen();
            System.out.println("\f");
            System.out.print(out_string);
            if (is_roman == 1)
            {
                System.out.print(Convert_to_roman(roman_numbers ,ab));
            }

            else
                System.out.print(ab);

        }
        else Ex("РџСЂРёРјРµСЂ РІРІРµРґРµРЅ РЅРµ РІРµСЂРЅРѕ");
    }
    public static int check_the_numbers (String[] acceptable_roman_numbers, int[] acceptable_arabic_numbers, String number) throws Exception { // Р’РѕР·РІСЂР°С‰Р°РµС‚ 0 РµСЃР»Рё С‡РёСЃР»Рѕ Р°СЂР°Р±СЃРєРѕРµ, 1 РµСЃР»Рё С‡РёСЃР»Рѕ СЂРёРјСЃРєРѕРµ
        int result = -1;
        for (int i = 0; i < acceptable_roman_numbers.length; i++)
        {
            if(result == -1)
            {
                if(number.equals(acceptable_roman_numbers[i]))
                {
                    result = 1;
                }
            }
        }
        if(result == -1)
        for (int i = 0; i < acceptable_arabic_numbers.length; i++)
        {
            if(result == -1)
            {
                if(number.equals(String.valueOf(acceptable_arabic_numbers[i])))
                {
                    result = 0;
                }
            }
        }
        if (result == -1)
            Ex("Р’РІРµРґРµРЅРѕ РЅРµ РІРµСЂРЅРѕРµ С‡РёСЃР»Рѕ");
        return result;
    }
    public static String Convert_to_roman (String[] _roman_numbers ,Integer _integer) throws Exception { // Р’РѕР·РІСЂР°С‰Р°РµС‚ РѕС‚РІРµС‚ РІ СЂРёРјСЃРєРёС… С‡РёСЃР»Р°С…
        String result = "";
        boolean bl = true;
        Integer ost = _integer;
        if (ost <= 0)
            Ex("Р§РёСЃР»Рѕ СЂР°РІРЅРѕ РёР»Рё РјРµРЅСЊС€Рµ С‡РµРј 0");
        if (ost / 100 == 1)
        {
            result += "C";
            ost -= 100;
        }
        if (ost / 90 == 1)
        {
            result += "XC";
            ost -= 90;

        }
        if (ost / 50 == 1)
        {
            result += "L";
            ost -= 50;
        }
        if (ost / 40 == 1)
        {
            result += "XL";
            ost -= 40;
        }
        for (int i = 0; i < (ost / 10); )
        {
            result += "X";
            ost -= 10;
        }
        if (ost > 0)
        {
            result += _roman_numbers[ost - 1];
        }
        return result;
    }
    public static Integer Calculate(Integer a, Integer b, String operator) {
        if(operator.equals("+"))
        {
            return a + b;
        }
        if(operator.equals("-"))
        {
            return a - b;
        }
        if(operator.equals("*"))
        {
            return a * b;
        }
        if(operator.equals("/"))
        {
            return a / b;
        }
        return 0;
    }
    public static void clearScreen() {
        System.out.print("\033[H\033[2J");
        System.out.flush();
    }
    public static void Ex () throws Exception { // Р’С‹С‹РѕРґРёС‚ СЃРѕРѕР±С‰РµРЅРёРµ РѕР± РѕС€РёР±РєРµ
        throw new Exception("РћС€РёР±РєР°");
    }
    public static void Ex (String error_description) throws Exception { // Р’С‹С‹РѕРґРёС‚ СЃРѕРѕР±С‰РµРЅРёРµ РѕР± РѕС€РёР±РєРµ, РїРѕР»СѓС‡Р°РµС‚ String СЃ РѕРїРёСЃР°РЅРёРµРј РѕС€РёР±РєРё
        throw new Exception(error_description);
    }
}    
