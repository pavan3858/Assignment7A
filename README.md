# Assignment7A  BADHAVATH PAVAN,EE19B010
## Introduction 
In this assignment,the functions sympy were used to solve the equations for a low-pass and a high-pass filter,employed using opamps,and as such get the transfer function of the system.Then,this transfer function was used to end the output waveform when an input with different frequency components were given.Using the functions scipy.signal.lsim and scipy.signal.impulse.The latter was used to end the waveform when the laplace transform of the output was known and the former was used to end the output when the input signal in the time domain is known, as well as the transfer function (in the frequency domain). Then, the input to the system was varied from a step function, to an exponentially decaying sinusoid and the various outputs that were obtained were noted.
### Low Pass Filter
In this,a low-pass filter circuit was realised using capacitors,resistors and an opamp in negative feedback.The various KCL equations at the different nodes that are used for solving the circuit are:

        Vm=Vo/G   
        Vp=V1(1/(1+jwR2C2))
        Vo=G(Vp-Vm)
        (Vi-V1)/R1 + (Vp-V1)/R2 + jwC1(V0-V1) = 0
        
In the above equations,G is the ratio in which the output voltage is divided in the resistive path of the opamp,as well as numerically equally to the gain of the opamp.Vp is the voltage at the positive terminal of the opamp,where Vm is that in the negative terminal.Vi is the input node1(corresponding to V1).R2 is connected between V1 and Vp,while C2 is connected between Vp and the ground.Finally,the capacitor C1 is connected between V1 and Vo in another feedback path that would be blocked for DC signals. These above equations were solved using matrices in sympy.

In this,matrix A is the coefficient matrix and B is the matrix having the independent sources.The various functions related to calculating the time domain output are declared.

The second function is called from the main program for calculating the output,which in turn calls the function to the end and return the coefficients of the laplace transform of the output,so that scipy.signal.impulse can calculate the output correctly.The above function can be used if the laplace transform of the input is known.If,only the time domain representation of the input is known,the following function can be used to calculate the output using scipy.signal.lism instead of scipy.signal.impulse.The function takes 3 parameters.The sympy expression of the transfer function,time domain input wave as well as the time interval to calculate the output.

#### Transfer function of the system
If,the input Vi is given as an impulse(i.e laplace transform input is 1),then,the transfer function of the above system can be known.Thus,the transfer function is calculated and plotted.

![Figure_7A](https://user-images.githubusercontent.com/81006760/117527931-366aa200-afed-11eb-87b6-3dc6d2db616a.png)

Figure-1 Bode plots of low-pass transfer function

Thus,it is evident that,the system above acts as a low-pass filter,as it passes low frequencies with almost no attenuation,while highly attenuates high frequency inputs.Also,the 3dB bandwidth (magnitude at phase of pi/2),is around 100000 Hz,which means that,any frequency below this,it will pass with minimal attenuation.

##### Step Response
The response of the low-pass filter o a step input is calculated.For this,the laplace transform of the step input is used as input to the above functions and the step response in both time and frequency domains are plotted.


![Figure_7B](https://user-images.githubusercontent.com/81006760/117527988-92cdc180-afed-11eb-8724-85fe2ab9e39f.png)

Figure-2 Step Response of low-pass transfer function


![Figure_7C](https://user-images.githubusercontent.com/81006760/117528127-40d96b80-afee-11eb-9c7a-eabd1fad5153.png)

For this,the lsim function is used,wherein we know the time domain input,and the transfer function of the system (calculated above as H).Using these and scipy.signal.lsim ,the output time domain wave is calculated.In the below code segment,both the input and output waves are plotted for comparison.

![Figure_7D](https://user-images.githubusercontent.com/81006760/117528193-9150c900-afee-11eb-88a1-ea4a9c7b1c67.png)

Thus,it is found that,although input had high frequency components, the circuit filters all of this,and gives output as only the low frequency component.

High-pass Filter


The only difference in this implementation is that the KCL equations used for calculating Vo would be different.The KCL equations for a high pass filter using opamps,resistors and capacitors are 

![Figure_7E](https://user-images.githubusercontent.com/81006760/117528295-189e3c80-afef-11eb-8142-cea59a92e101.png)

Figure-5 Bode plot of high-pass transfer function

Vm = Vo/G
Vp = V1(jwR3C2/1+jwR3C2)
Vo = G(Vp-Vm)
jwC1(Vi-V1) + jwC2(Vp-V1) + (Vo-V1)/R1 = 0

In this above equations G is the ratio in which the output voltage is divided in the resistive dividing feedback path of the opampas well as numerically equal to the gain of the opamp.Vp is the voltage at the positive terminal of the opamp ,while Vm is that in the negative terminal.Vi is the input node of the system,and the capacitor C1 is connected between this and node 1 (corresponding to V1 ).C2 is connected between V1 and Vp,while R3 is connected between Vp and ground .Finally,the resistor R1 is connected between Vp and ground.Finally,the resistor R1 is connected between V1 and Vo,in another feedback path.A python function is declared that solves the above equations similar to that done for low-pass filter.
All the other functions that were declared to calculate and plot the output transforms and signals can be used here also,as except the equations,nothing else changes in the overall logic of the program.

![Figure_7F](https://user-images.githubusercontent.com/81006760/117528417-ca3d6d80-afef-11eb-8882-e4e5afd89508.png)

Figure-6 Step Response of high pass filter

![Figure_7G](https://user-images.githubusercontent.com/81006760/117528456-fce76600-afef-11eb-99cf-83fb07cee6ac.png)

Figure-7 Time domain output to the step input

###### Input as (sin(2000t) + cos(210e6t))uo(t)

In this the same input ,which was given to the low-pass filter is given to the high-pass filter case,it was seen that ,only the low frequency component was passed,so here the expected output is that only high frequency component should pass.

![Figure_7H](https://user-images.githubusercontent.com/81006760/117528567-8303ac80-aff0-11eb-8879-ea928d72fafe.png)

 Low Frequency Decay Wave
 
A decaying wave of frequency 2000 Hz,is given as input to the high pass filter and output obtained is observed.The input given is sin(2000t)e 1000t.

High frequency decay wave

Here,a high frequency wave of frequency 2M is given.

![Figure_7I](https://user-images.githubusercontent.com/81006760/117528710-28b71b80-aff1-11eb-9734-7abf429dffdb.png)

![Figure_7J](https://user-images.githubusercontent.com/81006760/117528720-39679180-aff1-11eb-85c3-109abbd6a79a.png)

Conclusion

For the other signal input to the filter, it is seen that, the low pass filter passes only the low frequency component and almost completely attenuates the high frequency part, as expected. Also, from the Bode plots of the transfer function of the low pass filter, it is observed that as the low frequency component of the input (1000 Hz) is less than the 3dB bandwidth of the system it passes with little attenuation (a gain of around 0.8), whereas for that of the high frequency component (10e6 Hz), which is higher than the 3dB bandwidth of around 10e5 , gain is almost 10e2 , and hence is not visible in the graph

From the step-response, of the low pass filter, it is seen that, at steady state, output is a constant value (at a very low attenuation). This is because, low pass filter will pass DC signals , and at time t much greater 0 step input is a DC input.At t = 0, though the rise is gradual, as the capacitors them- selves take time to charge, and once they have done, the output becomes DC.

From the step-response of the high pass filter, it is seen that at t much greater than 0, output is 0. This is because, at these instants, input is a DC value and the high pass filter will attenuate this, and thus output will be almost 0. At t = 0, though, there is a peak for the output. This is because, at this point of discontinuity in the input, as seen from the frequency domain, a lot of high frequency components would be there, hence these would be passed, and so, an output is observed only at this point. These high frequency components are due to the discontinuity, which cannot be replicated using the fourier transform as the fourier transform decomposes the function into a bunch of continuous time sinusoids, hence, Gibb's phenomenon occurs at the discontinuity, causing the initial peak in the step response.






