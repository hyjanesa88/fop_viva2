```java
import java.util.Scanner;

public class v2q1 {
    //check if input is prime
    public static boolean isPrime(int num) {
        if (num < 2) return false;
        if (num == 2) return true;
        if (num % 2 == 0) return false;
        for (int i = 3; i <= Math.sqrt(num); i += 2) {
            if (num % i == 0) return false;
        }
        return true;
    }

    //check input's front and back numbers to find the closest prime
    public static int getNearestPrime(int num) {
        int distance = 1;
        while (true) {
            int left = num - distance;
            int right = num + distance;

            if (isPrime(left) && isPrime(right)) {
                return left;
            } else if (isPrime(left)) {
                return left;
            } else if (isPrime(right)) {
                return right;
            }
            distance++;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter an integer: ");
        int n = sc.nextInt();
        if (isPrime(n)) {
            System.out.println("Prime number: " + n);
        } else {
            System.out.println("Nearest prime number: " + getNearestPrime(n));
        }
    }
}

```
