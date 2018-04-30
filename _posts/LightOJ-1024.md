---
title: LightOJ-1024
date: 2018-04-22 22:29:32
tags: [algorithm,BigInteger]
---
来源：LightOJ1024

Java学习一个

```java
    
    import java.util.*; 
    import java.math.*;  
    import java.io.*;
    public class Main{
        public static void main(String args[]){
            Scanner input = new Scanner(System.in);
            int n;
            BigInteger du;
            int T,nc = 1;
            T = input.nextInt();
            while(T>0){
                T--;
                n = input.nextInt();
                BigInteger start = BigInteger.ONE;
                for(int i=0;i<n;i++) {
                    du = input.nextBigInteger();
                    start = start.divide(start.gcd(du)).multiply(du);
                    //printfBig(start);
                }
                System.out.printf("Case "+ nc + ": " + start.toString()+'\n');
                System.gc();
                nc ++;
            }
        }
    }  

```