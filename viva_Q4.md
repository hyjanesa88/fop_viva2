```java

import java.util.Scanner;
import java.text.DecimalFormat;

public class VivaQ4 {
    private static final DecimalFormat df = new DecimalFormat("0.00");
    private static final Scanner scanner = new Scanner(System.in);

    public static double getSideBySAS(double side1, double angle, double side2) {
        //Change angle to radians
        double angleRad = Math.toRadians(angle);
        //By using law of cosines: a^2 = b^2 + c^2 - 2bc*cos(A)
        double sideSquared = Math.pow(side1,2) + Math.pow(side2,2) - 2*side1*side2* Math.cos(angleRad);

        return Math.sqrt(sideSquared);
    }

    public static double getAngleBySSS(double side1, double side2, double targetSide){
        //Use law of cosines to find Angle
        double numerator = Math.pow(side1, 2) + Math.pow(side2, 2) - Math.pow(targetSide, 2);
        double denominator = 2 * side1 * side2;

        //To Ensure the value is within [-1, 1] for Math.acos()
        double cosValue = numerator / denominator;
        cosValue = Math.max(-1,Math.min(1,cosValue));

        double angleRad = Math.acos(cosValue);
        return Math.toDegrees(angleRad);
    }

    public static double getArea(double a, double b, double c){
        double s = (a+b+c)/2;
        return Math.sqrt(s * (s - a) * (s - b) * (s - c));
    }

    public static boolean isValidTriangle(double a, double b, double c){
        return (a + b > c) && (a + c > b) && (b + c > a);
    }

    //Handles SSS triangle calculation
    public static void handleSSS(){
        System.out.print("Enter side 1: ");
        double a = scanner.nextDouble();
        System.out.print("Enter side 2: ");
        double b = scanner.nextDouble();
        System.out.print("Enter side 3: ");
        double c = scanner.nextDouble();

        if(!isValidTriangle(a,b,c)){
            System.out.println("Not a valid triangle");
            return;
        }

        // Calculate all angles
        double angleA = getAngleBySSS(b, c, a); // Angle opposite side a
        double angleB = getAngleBySSS(a, c, b); // Angle opposite side b
        double angleC = getAngleBySSS(a, b, c); // Angle opposite side c

        // Calculate area
        double area = getArea(a,b,c);

        // Display results
        System.out.println("\nTriangle Info ↓");
        System.out.println();
        System.out.println("Side A: " + df.format(a));
        System.out.println("Side B: " + df.format(b));
        System.out.println("Side C: " + df.format(c));
        System.out.println("Angle BC: " + df.format(angleA));
        System.out.println("Angle AC: " + df.format(angleB));
        System.out.println("Angle AB: " + df.format(angleC));
        System.out.println("Area of Triangle: " + df.format(area));
    }
    // Handle SAS triangle calculation
    public static void handleSAS() {
        System.out.print("Enter side 1: ");
        double side1 = scanner.nextDouble();
        System.out.print("Enter angle (in degrees): ");
        double angle = scanner.nextDouble();
        System.out.print("Enter side 2: ");
        double side2 = scanner.nextDouble();

        // Calculate the third side
        double side3 = getSideBySAS(side1, angle, side2);

        if (!isValidTriangle(side1, side2, side3)) {
            System.out.println("Not a valid triangle");
            return;
        }

        // Calculate remaining angles
        double angle1 = getAngleBySSS(side2, side3, side1); // Angle opposite side1
        double angle2 = getAngleBySSS(side1, side3, side2); // Angle opposite side2
        double angle3 = angle; // The given angle

        // Calculate area
        double area = getArea(side1, side2, side3);

        System.out.println("\nTriangle Info ↓");
        System.out.println();
        System.out.println("Side A: " + df.format(side1));
        System.out.println("Side B: " + df.format(side2));
        System.out.println("Side C: " + df.format(side3));
        System.out.println("Angle BC: " + df.format(angle1));
        System.out.println("Angle AC: " + df.format(angle2));
        System.out.println("Angle AB: " + df.format(angle3));
        System.out.println("Area of Triangle: " + df.format(area));
    }



    public static void main(String[] args) {
        System.out.print("Enter triangle type (SSS or SAS): ");
        String type = scanner.next().toUpperCase();

        if (type.equals("SSS")) {
            handleSSS();
        } else if (type.equals("SAS")) {
            handleSAS();
        } else {
            System.out.println("Invalid triangle type. Please enter SSS or SAS.");
        }

        scanner.close();
    }
    }

```
