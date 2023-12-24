import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Point {
    double x, y;

    public Point(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double distanceTo(Point other) {
        return Math.sqrt(Math.pow(this.x - other.x, 2) + Math.pow(this.y - other.y, 2));
    }
}

class Shape {
    List<Point> points;

    public Shape(List<Point> points) {
        this.points = points;
    }

    public double perimeter() {
        double totalDistance = 0;
        int numPoints = points.size();

        for (int i = 0; i < numPoints; i++) {
            Point currentPoint = points.get(i);
            Point nextPoint = points.get((i + 1) % numPoints);
            totalDistance += currentPoint.distanceTo(nextPoint);
        }

        return totalDistance;
    }

    public double longestSide() {
        double maxDistance = 0;

        for (int i = 0; i < points.size(); i++) {
            for (int j = i + 1; j < points.size(); j++) {
                double distance = points.get(i).distanceTo(points.get(j));
                maxDistance = Math.max(maxDistance, distance);
            }
        }

        return maxDistance;
    }

    public double averageSide() {
        double totalDistance = 0;

        for (int i = 0; i < points.size(); i++) {
            for (int j = i + 1; j < points.size(); j++) {
                totalDistance += points.get(i).distanceTo(points.get(j));
            }
        }

        return totalDistance / points.size();
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        List<Point> points = new ArrayList<>();
        for (int i = 0; i < 10; i++) {
            System.out.println("Enter the coordinates for the point " + (i + 1) + ":");
            System.out.print("x: ");
            double x = scanner.nextDouble();
            System.out.print("y: ");
            double y = scanner.nextDouble();
            points.add(new Point(x, y));
        }

        Shape shape = new Shape(points);

        double perimeter = shape.perimeter();
        double longestSide = shape.longestSide();
        double averageSide = shape.averageSide();

        System.out.println("Perimeter: " + perimeter);
        System.out.println("The longest side: " + longestSide);
        System.out.println("The average length of the side: " + averageSide);
    }
}
