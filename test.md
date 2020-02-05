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


 x \\[\dot{\theta}=\displaystyle \frac{v}{L}\tan{\gamma}\\]

# Chapter 4: Mobile robot vehicles

## Q1
### a)
Using the equation 4.2  $\dot{\theta}=\displaystyle \frac{v}{L}\tan{\gamma}$ after transforming the inputs to SI units

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

### c)
We will consider the back wheels and assume the wheel radius is Rw = 0.3. The left- and right-hand wheels have respective path radii of

$$R_{1L}=R-W/2$$

$$R_{1R}=R+W/2$$

Vehicle speed V is measured at the origin of the frame {V} located between the back wheels. We can apply equation (4.1) to both back wheels

$$\dot\theta=\frac{V}{R}=\frac{V_{1L}}{R_{1L}}=\frac{V_{1R}}{R_{1R}}$$

and the wheel velocity is related to wheel angular velocity by $$V_i=\omega _iR_{w_i}$$ so we can write

$$\frac{V}{R}=\frac{\omega _{1L}R_w}{R_{1L}}=\frac{\omega _{1R}R_w}{R_{1R}}$$

In MATLAB this is simply

```matlab
>> R = [10 50 100];
>> L = 2; W = 1.5; Rw = 0.3;
>> V = 80 * (1000/3600) % m/s 
V=
     22.2222
>> R1L = R-W/2; R1R = R+W/2;
>> omega1L = V ./ R .* R1L/Rw
omega1L =
 68.5185   72.9630   73.5185
>> omega1R = V ./ R .* R1R/Rw
omega1R =
 79.6296   75.1852   74.6296
>> omega1R./omega1L
ans =
  1.1622    1.0305    1.0151
```
So for the tight turn (10m) radius the outside wheel is rotating 16% faster than the inside wheel. That’s why a car’s motor is not connected directly to the wheels but rather via a differential gearbox which allows the wheels to rotate at different speeds.