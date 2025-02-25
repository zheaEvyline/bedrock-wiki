---
title: Scoreboard Operations
category: General
mentions:
    - Sprunkles137
    - Luthorius
    - MedicalJewel105
    - Hatchibombotar
description: Scoreboards can be used to perform complex operations, similar to MoLang. Operations come in two flavors - mathematical, and logical.
---

Scoreboards can be used to perform complex operations, similar to [Molang](/concepts/molang). Operations come in two flavors: mathematical, and logical.

## Overview
Operations are performed using the `/scoreboard players operation` command. The full syntax is laid out below:
```
/scoreboard players operation <targetScore> <objective> <operation> <sourceScore> <objective>
```
The command consists of two score holders: The target score, and the source score. The target score is the value being operated on, and the source score is the value affecting the operation. The result of the operation is written into the target score, and the source score's value is not touched, save for [one operation](/commands/scoreboard-operations#swap-operator).

## Mathematical Operators
Mathematical operators use arithmetic to affect the target score. There are five mathematical operations available: addition, subtraction, multiplication, floor division, and floor modulo division.

For each of the following examples below, assume that score holder `A var` equals 25, and `B var` equals 10.

### Addition
Operator: **+=**

This operation adds the target score and source scores together, then stores the sum into the target score.
```
/scoreboard players operation A var += B var
```
`A = A + B`, and as such `25 + 10 = 35`.

### Subtraction
Operator: **-=**

This operation subtracts the target score by the source score, then stores the difference into the target score.
```
/scoreboard players operation A var -= B var
```
`A = A - B`, and as such `25 - 10 = 15`.

### Multiplication
Operator: **\*=**

This operation multiplies the target score by the source score, then stores the product into the target score.
```
/scoreboard players operation A var *= B var
```
`A = A * B`, and as such `25 * 10 = 250`.

### Floored Division
Operator: **/=**

This operation divides the target score by the source score, then stores the quotient into the target score. Because score values can only be integers, the value is floored, or rounded down.
```
/scoreboard players operation A var /= B var
```
`A = floor(A / B)`, and as such `floor(25 / 10) = 2`.

### Floored Modulo Division
Operator: **%=**

This operation also divides the target score by the source score, but instead returns the remainder after the division into the target score. This is also floored.
```
/scoreboard players operation A var %= B var
```
`A = floor(mod(A, B))`, and as such `floor(mod(25, 10)) = 5`.

## Logical Operators
Logical operations use logic gates and assignments to affect the target score. There are four logical operations available: assignment, less than, greater than, and swap.

Similar to the above, assume that score holder `A var` equals 25, and `B var` equals 10.

### Assignment Operator
Operator: **=**

This operation sets the target score equal to the source score.
```
/scoreboard players operation A var = B var
```
`A = B`, and as such the result is `10`.

### Minimum Operator
Operator: **<**

This operation returns the smallest of the input scores, and stores it into the target score.
```
/scoreboard players operation A var < B var
```
`A = min(A, B)`, and as such `min(25, 10) = 10`.

### Maximum Operator
Operator: **>**

This operation returns the largest of the input scores, and stores it into the target score.
```
/scoreboard players operation A var > B var
```
`A = max(A, B)`, and as such `max(25, 10) = 25`.

### Swap Operator
Operator: **><**

This operation swaps the target score and source scores with each other. This is the only operation that affects the source score.
```
/scoreboard players operation A var >< B var
```
The above command would swap the values of A and B e.g.

Before: A = 10; B = 25;

After: A = 25; B = 10;

This can be seen as three operations: `temp = A; A = B; B = temp;`, and as such `A var = 10` and `B var = 25`.

## Useful Creations

#### Check If Values are Equal

If you want to check in scoreboard, whether one value equals another value, you can copy first value to temporary value, subtract the other and compare temporary value to zero. Given values A and B:

<CodeHeader></CodeHeader>

```
scoreboard objectives add temp dummy
scoreboard players operation @e temp = @s A
scoreboard players operation @e temp -= @s B
execute @e[scores={temp=0}] ~~~ say A equals B
scoreboard objectives remove temp
```

#### Scoreboard Initialization

If you want to initialize a scoreboard value to 0, but only if it doesn't exists, you can use `scoreboard players add <selector> <name> 0`. It will set the value to 0, if it doesn't exist on the entity and do nothing, if it already exist.
