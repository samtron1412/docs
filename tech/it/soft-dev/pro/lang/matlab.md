# Overview

Matrix Laboratory programming language and numerical computing
environment.

# Syntax

## Variables

- Weekly types
- Defined using assignment operator `=`

```matlab
>> x = 17
x =
 17

>> x = 'hat'
x =
hat

>> x = [3*4, pi/2]
x =
   12.0000    1.5708

>> y = 3*sin(x)
y =
   -1.6097    3.0000
```

## Vectors and matrices

- Arrays: `x = 1:2:9`
    + `initial(inclusive):[increment]:terminator(inclusive)`
    + indices is one-based not zero-based
    + access using indices: `x(1), x(2)`
- Matrix

```matlab
>> A = [16 3 2 13; 5 10 11 8; 9 6 7 12; 4 15 14 1]

% Access elements
>> A(2,3)

% Row 2->4, column 3->4
>> A(2:4,3:4)

>> eye(3,3)
ans =
 1 0 0
 0 1 0
 0 0 1

>> zeros(2,3)
ans =
 0 0 0
 0 0 0

>> ones(2,3)
ans =
 1 1 1
 1 1 1

% Transpose
>> A = [1 ; 2],  B = A.', C = transpose(A)
A =
     1
     2
B =
     1     2
C =
     1     2

>> D = [0 3 ; 1 5], D.'
D =
     0     3
     1     5
ans =
     0     1
     3     5
```

## Functions

- When creating a MATLAB function, the name of the file should match the
  name of the first function in the file.
- Valid function names begin with an alphabetic character, and can
  contain letters, numbers, or underscores.
- Functions are often case sensitive.


## Class and OOP

```matlab
classdef hello
    methods
        function greet(this)
            disp('Hello!')
        end
    end
end


>> x = hello;
>> x.greet();
Hello!
```


## Graphics and GUI

```matlab
x = 0:pi/100:2*pi;
y = sin(x);
plot(x,y)
```

- 3D plot: `surf`, `plot3`, `mesh`

```matlab

[X,Y] = meshgrid(-10:0.25:10,-10:0.25:10);
f = sinc(sqrt((X/pi).^2+(Y/pi).^2));
mesh(X,Y,f);
axis([-10 10 -10 10 -0.3 1])
xlabel('{\bfx}')
ylabel('{\bfy}')
zlabel('{\bfsinc} ({\bfR})')
hidden off

% second example
[X,Y] = meshgrid(-10:0.25:10,-10:0.25:10);
f = sinc(sqrt((X/pi).^2+(Y/pi).^2));
surf(X,Y,f);
axis([-10 10 -10 10 -0.3 1])
xlabel('{\bfx}')
ylabel('{\bfy}')
zlabel('{\bfsinc} ({\bfR})')
```




# File extensions

## Matlab

Filetype | Description
:-|:-
.m | Matlab code
.mat | Matlab data
.mex* | Matlab executable MEX-files (platform specific)
.p | Matlab content-obscured
.mlx | Matlab live script
.fig | figure
.mlapp | application
.mlappinstall | packaged App installer
.mlpkginstall | support package installer
.prj | project file

