---
title: "beecrowd 1040 – Average 3 (Java)"
date: 2017-02-20 12:20:00
category: "Programming"
tags: ["java", "beecrowd", "competitive-programming"]
wp_url: https://capivarainformacoes.wordpress.com/2017/02/20/exercicio-1040-uri/
---

Problem: [beecrowd 1040](https://judge.beecrowd.com/en/problems/view/1040)

Compute a weighted average of four grades (weights 2, 3, 4 and 1).
If the average is 7.0 or higher, the student passes. Below 5.0, the student fails.
Otherwise, read the exam grade and print the result.

```java
import java.text.DecimalFormat;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        DecimalFormat df = new DecimalFormat("0.0");

        double n1 = Double.parseDouble(scan.next());
        double n2 = Double.parseDouble(scan.next());
        double n3 = Double.parseDouble(scan.next());
        double n4 = Double.parseDouble(scan.next());

        // Weighted average with weights 2, 3, 4 and 1
        double average = (n1 * 2 + n2 * 3 + n3 * 4 + n4) / 10;

        // Output messages are in Portuguese because the judge expects them
        if (average >= 7) {
            System.out.println("Media: " + round(df, average) + "\nAluno aprovado.");
        } else if (average < 5) {
            System.out.println("Media: " + round(df, average) + "\nAluno reprovado.");
        } else {
            double exam = Double.parseDouble(scan.next());
            double finalAverage = (average + exam) / 2;

            System.out.println("Media: " + round(df, average));
            System.out.println("Aluno em exame.");
            System.out.println("Nota do exame: " + round(df, exam));

            if (exam >= 5) {
                System.out.println("Aluno aprovado.\nMedia final: " + round(df, finalAverage));
            } else {
                System.out.println("Aluno reprovado.\nMedia final: " + round(df, finalAverage));
            }
        }
    }

    // Truncates to one decimal place using DecimalFormat (its output may use ',' depending on locale)
    private static double round(DecimalFormat df, double value) {
        return Double.parseDouble(df.format(value).replace(',', '.'));
    }
}
```

> URI Online Judge is now called **beecrowd**. The output messages stay in Portuguese because the judge checks them exactly.
