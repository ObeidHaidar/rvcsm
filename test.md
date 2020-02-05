---
home_spotlights:
  home_img:
    data_position: top center
    path: ''
    url: ''
  enabled: false
  weight: 
  excerpt: ''
layout: page
title: test
content_img_path: ''
published: false

---
Hello

# hey


<img src="https://render.githubusercontent.com/render/math?math=e^{i \pi} = -1">

$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$

# Chapter 4: Mobile robot vehicles

## Q1
### a)
Using the equation 4.2 $ \dot{\theta}=\displaystyle \frac{v}{L}\tan{\gamma}$ after transforming the inputs to SI units

```matlab
Turn_rate = deg2rad(10);
Forward_speed = 20*(60/1000);
L=2;
Steering_wheel_angle_in_degrees = atand(Turn_rate*L/Forward_speed)
```
> Steering\_wheel\_angle\_in\_degrees = 16.2191

### b)
$R_B=\displaystyle \frac{L}{\tan{\gamma}}$  $\therefore$ $\gamma = \tan^{-1}\left({\displaystyle\frac{L}{R_B}}\right)$

```matlab
Rb=[10 50 100];
L=2;
W=1.5;
RbInner = Rb-W/2;
RbOuter = Rb+W/2;
wheel_steer_angle_in_degrees_inner = atand(L./RbInner)
```
>wheel\_steer\_angle\_in\_degrees\_inner = 1×3
>
>   12.2005    2.3255    1.1544
   
   
```matlab
wheel_steer_angle_in_degrees_outer = atand(L./RbOuter)
```
>wheel\_steer\_angle\_in\_degrees\_outer = 1×3
>
>   10.5392    2.2568    1.1372
   
```matlab
difference_in_steering_angle = wheel_steer_angle_in_degrees_inner - wheel_steer_angle_in_degrees_outer
```
>difference_in_steering_angle = 1×3
>
>    1.6613    0.0687    0.0172

in units of degrees. For a tight turn we see that the front wheels are 1.6deg off parallel. Note that we’ve made use of MATLAB code vectorization here to compute the result in one hit for various values of R. Since R is a vector and L is a scalar we must use the element-by-element division operator ./. In fact the two front wheels will not exactly lie on the radial line through ICR and this properly needs to be taken into consideration (exercise for the reader). 
