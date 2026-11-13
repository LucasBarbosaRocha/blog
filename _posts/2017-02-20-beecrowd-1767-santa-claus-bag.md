---
title: "beecrowd 1767 – Santa Claus Bag (0/1 Knapsack in C)"
date: 2017-02-20 12:00:00
category: "Programming"
tags: ["c", "beecrowd", "dynamic-programming", "competitive-programming"]
wp_url: https://capivarainformacoes.wordpress.com/2017/02/20/exercicio-1767-uri/
---

Problem: [beecrowd 1767](https://judge.beecrowd.com/en/problems/view/1767)

A classic **0/1 knapsack**: each package has a number of toys (its value) and a weight,
and the bag holds at most 50 kg. Dynamic programming finds the maximum number of toys.
Then we walk back through the table to find which packages were chosen.

```c
/*
 * beecrowd 1767 - Santa Claus Bag (0/1 knapsack)
 * Author: Lucas Barbosa Rocha
 */
#include <stdio.h>
#include <stdlib.h>

#define MAX_WEIGHT 50

/*
 * Solves the 0/1 knapsack problem.
 *   v - value of each item (here, the number of toys in each package), 1-indexed
 *   w - weight of each item, 1-indexed
 *   W - maximum weight the bag can carry
 *   n - number of items
 * Returns an array where position 0 holds the best total value and
 * positions 1..n are 1 if the item is part of the optimal solution, 0 otherwise.
 */
int *knapsack(int *v, int *w, int W, int n);

int max(int a, int b);

/* Stores the total weight of the selected items in out[0] and the number of items left out in out[1]. */
void weight_and_leftover(int *w, int *selected, int n, int *out);

int main(void)
{
    int *v, *w, *selected, out[2], packages, i, tests;

    scanf("%d", &tests);
    while (tests-- > 0) {
        scanf("%d", &packages);

        v = malloc((packages + 1) * sizeof(int));
        w = malloc((packages + 1) * sizeof(int));
        v[0] = w[0] = 0;

        for (i = 1; i <= packages; i++)
            scanf("%d %d", &v[i], &w[i]);

        selected = knapsack(v, w, MAX_WEIGHT, packages);
        weight_and_leftover(w, selected, packages, out);

        /* Output format required by the judge (in Portuguese) */
        printf("%d brinquedos\n", selected[0]);
        printf("Peso: %d kg\n", out[0]);
        printf("sobra(m) %d pacote(s)\n", out[1]);
        printf("\n");

        free(v);
        free(w);
        free(selected);
    }
    return 0;
}

int *knapsack(int *v, int *w, int W, int n)
{
    int t[n + 1][W + 1];
    int *selected = malloc((n + 1) * sizeof(int));
    int i, cap, without, with;

    for (cap = 0; cap <= W; cap++) {
        t[0][cap] = 0;
        for (i = 1; i <= n; i++) {
            without = t[i - 1][cap];
            with = (w[i] > cap) ? 0 : t[i - 1][cap - w[i]] + v[i];
            t[i][cap] = max(without, with);
        }
    }

    /* Walk back through the table to find which items were chosen */
    cap = W;
    for (i = n; i >= 1; i--) {
        if (t[i][cap] == t[i - 1][cap]) {
            selected[i] = 0; /* same value without item i: not in the optimal solution */
        } else {
            selected[i] = 1;
            cap -= w[i];
        }
    }

    selected[0] = t[n][W];
    return selected;
}

int max(int a, int b)
{
    return a >= b ? a : b;
}

void weight_and_leftover(int *w, int *selected, int n, int *out)
{
    int i, weight = 0, leftover = 0;

    for (i = 1; i <= n; i++) {
        if (selected[i])
            weight += w[i];
        else
            leftover++;
    }
    out[0] = weight;
    out[1] = leftover;
}
```

> URI Online Judge is now called **beecrowd**. The output messages stay in Portuguese because the judge checks them exactly.
