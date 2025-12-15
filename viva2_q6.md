```java
import java.util.Scanner;

public class v2q6 {
    public static boolean canbePalindrome(String str) {
        int[] freq = new int[128]; //freq array for ASCII chars

        for (int i = 0; i < str.length(); i++) {
            freq[str.charAt(i)]++; // exp i = 0 = 'a', implicit casting char -> int 97
            // at index 97, value 0 became 1/2/3...
        }

        int oddchars = 0;
        for (int i = 0; i < freq.length; i++) {
            if (freq[i] % 2 != 0) {
                oddchars++;
            }
        }
        return oddchars <= 1; //at most 1 char can have odd count
        /* return oddchars same as:
        if (oddchars <= 1) {
            return true;
        } else {
            return false;
        }
        */
    }

    public static void getPossiblePalindrome(String str) {
        int length = str.length();
        int[] freq = new int[128];

        //count freq of char
        for (int i = 0; i < length; i++) {
            freq[str.charAt(i)]++;
        }
        //Find odd char if exist
        char[] halfArr = new char[length / 2]; //create array for the left half

        String middlechar = ""; //store that character if odd count of it exists

        int index = 0; //track position in halfArr

        for (int i = 0; i < freq.length; i++) { //check all ASCII from 0 -127
            if (freq[i] > 0) {
                if (freq[i] % 2 != 0) {
                    middlechar = String.valueOf((char) i);//convert ascii to char
                }else {
                    for (int j = 0; j < freq[i] / 2; j++) {
                        halfArr[index] = (char) i; //add the char to the array
                        index ++;
                    }
                }
            }
        }
        //calls the recursive method
        generatePermutations(halfArr, 0, middlechar);
    }

    public static void swap(char[] arr, int i, int j) {
        char temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public static void generatePermutations(char[] arr, int currentIndex, String mid) {
        //Base case
        if (currentIndex == arr.length) {
            printFullPalindrome(arr, mid);
            return;
        }
        boolean[] used = new boolean[128]; //check duplicates
        for (int i = currentIndex; i < arr.length; i++) {
            char ch = arr[i];

            if (!used[ch]) {
                used[ch] = true;

                swap(arr, currentIndex, i);

                generatePermutations(arr, currentIndex + 1, mid);

                swap(arr, currentIndex,i);
            }
        }
    }

    public static void printFullPalindrome(char[] halfArr, String mid) {
        for (int i = 0; i < halfArr.length; i++) {
            System.out.print(halfArr[i]);
        }

        System.out.print(mid);

        for (int i = halfArr.length - 1; i >= 0; i--) {
            System.out.print(halfArr[i]);
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter a string: ");
        String str = sc.nextLine();
        String strlow = str.toLowerCase();

        System.out.println("Can be Palindrome? ");
        if (canbePalindrome(strlow)) {
            System.out.println("All Possible Palindromes: ");
            getPossiblePalindrome(strlow);
        } else {
            System.out.println("Cannot be Palindrome ");
        }
        sc.close();
    }
}
```
