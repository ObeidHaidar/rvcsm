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

$$ \mathbf{X}\_{n,p} = \mathbf{A}\_{n,k} \mathbf{B}\_{k,p} $$


$$x^2$$

# Chapter 4: Mobile robot vehicles

## Q1

### a)

Using the equation 4.2 $ \\dot{\\theta}=\\displaystyle \\frac{v}{L}\\tan{\\gamma}$ after transforming the inputs to SI units

```matlab
Turn_rate = deg2rad(10);
Forward_speed = 20*(60/1000);
L=2;
Steering_wheel_angle_in_degrees = atand(Turn_rate*L/Forward_speed)
```

> Steering_wheel_angle_in_degrees = 16.2191

### b)

$R_B=\\displaystyle \\frac{L}{\\tan{\\gamma}}$  $\\therefore$ $\\gamma = \\tan^{-1}\\left({\\displaystyle\\frac{L}{R_B}}\\right)$

```matlab
Rb=[10 50 100];
L=2;
W=1.5;
RbInner = Rb-W/2;
RbOuter = Rb+W/2;
wheel_steer_angle_in_degrees_inner = atand(L./RbInner)
```

> wheel_steer_angle_in_degrees_inner = 1×3
>
> 12\.2005    2.3255    1.1544

```matlab
wheel_steer_angle_in_degrees_outer = atand(L./RbOuter)
```

> wheel_steer_angle_in_degrees_outer = 1×3
>
> 10\.5392    2.2568    1.1372

```matlab
difference_in_steering_angle = wheel_steer_angle_in_degrees_inner - wheel_steer_angle_in_degrees_outer
```

> difference_in_steering_angle = 1×3
>
> 1\.6613    0.0687    0.0172

in units of degrees. For a tight turn we see that the front wheels are 1.6deg off parallel. Note that we’ve made use of MATLAB code vectorization here to compute the result in one hit for various values of R. Since R is a vector and L is a scalar we must use the element-by-element division operator ./. In fact the two front wheels will not exactly lie on the radial line through ICR and this properly needs to be taken into consideration (exercise for the reader).