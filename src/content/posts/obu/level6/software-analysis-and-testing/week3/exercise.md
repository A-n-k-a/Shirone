---
title: "Software Analysis and Testing Exercise"
published: 2026-10-20
publishedAt: 2026-10-20T15:15:00+08:00
description: "Sample questions of final exam."
image: "./144173743.png"
tags: []
category: "Software Analysis and Testing"
draft: false
pinned: false
lang: en
---

Draw a flow graph model for the following piece of Java program code

```java
public class test {
    public static void fun(){
	    Input(x,y,z);
        if (x>y) {
            int a;
            a = x;
            if (z>a) {
                a = z;
                System.out.println(a);
            }
            else {
                System.out.println(a);
            }
        }
        else {
            int a;
            a = y;
            if (z>a) {
                a = z;
                System.out.println(a);
            }
            else {
                System.out.println(a);
            }
        }
    }
```

Reference Answer

```mermaid
flowchart TD
    B0["B0: Start; Input(x,y,z)"] --> B1{x>y?}
    B1 -- T --> B2["B2: int a; a=x;"]
    B2 --> B3{z>a?}
    B3 -- T --> B4["B4: a=z; println(a)"]
    B3 -- F --> B5["B5: println(a)"]
    B4 --> B6["B6: Exit"]
    B5 --> B6

    B1 -- F --> B7["B7: int a; a=y;"]
    B7 --> B8{z>a?}
    B8 -- T --> B9["B9: a=z; println(a)"]
    B8 -- F --> B10["B10: println(a)"]
    B9 --> B6
    B10 --> B6
```

---

The following is a flow graph model, and use two different methods to calculate cyclomatic complexity of the graph and write Independent complete Paths.

![](img/Pasted_image_20261022171420.png)

Reference Answer:  
$e-n+2=10-8+2=4$  
$p+1=3+1=4$  
predicate nodes: 1, 2, 4

---

```java
import java.util.Scanner;

public class NumberCheck {
    public static void main (String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Please enter an integer: ");
        int num = scanner.nextInt();
        if (num > 0) {
            if (num > 10) {
                System.out.println("This is a positive number greater than 10");
            } else {
                System.out.println("This is a positive number within 10 (including 10)");
        } else {
            System.out println ("This is not a positive number");
        }
        scanner.close ();
    }
}
```

1. Please draw the corresponding control flow diagram.

Reference Answer:

```mermaid
flowchart TD
    n1(["1. begin: create Scanner, print prompt"]) --> n2["2. num = scanner.nextInt() (def num)"]
    n2 --> n3{"3. num > 0 ? (p-use num)"}
    n3 -- "T" --> n4{"4. num > 10 ? (p-use num)"}
    n3 -- "F" --> n7["7. print 'not a positive number'"]
    n5["5. print 'positive > 10'"] --> n8(["8. scanner.close(), end"])
    n4 -- "T" --> n5
    n4 -- "F" --> n6["6. print 'positive within 10 (incl. 10)'"]
    n6 --> n8
    n7 --> n8

    style n3 fill:#fdebd0,stroke:#c0392b
    style n4 fill:#fdebd0,stroke:#c0392b
```

2. According the above flow graph model, please design a set of test cases satisfy the Statement coverage criterion, Branch coverage criterion.

Reference Answer:

|用例|输入 num|预期输出|覆盖说明|
|---|---|---|---|
|TC1|20|"positive number greater than 10"|DU-path 2-3、2-3-4；def-use (2,3)、(2,4)|
|TC2|10|"positive number within 10 (including 10)"|谓词 4 的 F 分支，scanner 的 DU-path 1-2-3-4-6-8|
|TC3|−8|"not a positive number"|谓词 3 的 F 分支，scanner 的 DU-path 1-2-3-7-8|

3. Please draw the corresponding data flow diagram and design the test data to satisfy  Definition/Use/DU-path coverage.

Reference Answer:

数据流图（DFG，标注 def/use 集合）：

```mermaid
flowchart TD
    n1(["1. DEF={scanner} USE={}"]) --> n2["2. DEF={num} USE={scanner} (c-use)"]
    n2 --> n3{"3. DEF={} USE={num} (p-use)"}
    n3 -- "T" --> n4{"4. DEF={} USE={num} (p-use)"}
    n3 -- "F" --> n7["7. DEF={} USE={}"]
    n4 -- "T" --> n5["5. DEF={} USE={}"]
    n4 -- "F" --> n6["6. DEF={} USE={}"]
    n5 --> n8(["8. DEF={} USE={scanner} (c-use)"])
    n6 --> n8
    n7 --> n8

    style n2 fill:#d5f5e3,stroke:#1e6641
    style n3 fill:#fdebd0,stroke:#c0392b
    style n4 fill:#fdebd0,stroke:#c0392b
```

DU-path: 

```mermaid
flowchart TD
    n2["2. def num"] -->|"du-path (2,3)"| n3{"3. p-use num"}
    n3 -->|"du-path (2,4)"| n4{"4. p-use num"}
    n3 -.->|F| n7["7"]
    n4 -.->|T| n5["5"]
    n4 -.->|F| n6["6"]

    linkStyle 0 stroke:#c0392b,stroke-width:3px
    linkStyle 1 stroke:#c0392b,stroke-width:3px
```

Source: [exercise.docx](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fvle.zycdut.net%2Fsites%2Fstudent.zy.cdut.edu.cn%2Ffiles%2Fattachments%2Fexercise_14.docx&wdOrigin=BROWSELINK)
