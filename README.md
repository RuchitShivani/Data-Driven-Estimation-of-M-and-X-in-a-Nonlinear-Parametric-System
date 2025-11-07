# Data-Driven-Estimation-of-M-and-X-in-a-Nonlinear-Parametric-System



Optimal Parameters:

	Theta (°): 28.1209
	M: 0.021397
	X: 54.9011
	Average L1 Distance per Point: 25.2434
	Score (out of 100): 74.7566

Relevant Graph: https://www.desmos.com/calculator/dwvd59wtd5

Before we dive into the logic used in the process of solving this problem, there are certain relevant technical terms that need to be simplified (that helped me in understanding the approach to this particular problem), here are their simplified definitions:

	Parametric Curve: A curve that can be defined using a separate variable (called a parameter, usually t) that determines both x and y values.
Example: x=f(t), y=g(t). As t changes, it traces a path in two-dimensional space.

	Parameters (θ, M, X): These control how the curve looks:
	θ (theta): the rotation angle of the curve.
	M: the exponential growth or decay rate.
	X: the horizontal shift or offset of the curve.
	The goal is to find the best values for these parameters so that the curve matches the data points.
3. Curve Fitting: The process of adjusting parameters in an equation so that the curve produced by the equation closely matches a given set of data points, the set of data points in this case being present in the dataset provided.
4. Optimization: A mathematical method essentially used to find the best possible values for parameters by minimizing (or maximizing) a chosen measure of error or performance.
5. Objective Function (or Cost Function): The function that measures and helps determine how far the model’s predictions are from the actual data. In this case, it is the L1 distance, which represents the total error between predicted and actual points.

6. L1 Distance (Manhattan Distance): A measure of error obtained by summing the absolute differences between predicted and actual values.

Formula:
L1=∑∣x_pred-x_actual∣+∣y_pred-y_actual∣

A smaller L1 value indicates a better fit, extremely relevant in finding the accuracy of the output.
7. Exponential Term (e^(M∣t∣)): This term causes the curve to increase or decrease exponentially with t.
	When M>0, the curve grows.
	When M<0, it decays.
	The ∣t∣makes it symmetric for both positive and negative values of t.














Explanation

Yeah, right measure how close the predicted curve is to the real data, we calculate an error for each data point. For every t, we find the predicted values (x_pred,y_pred)from the equations and compare them with the given values (x_data,y_data). The difference for each point is found using the L1 distance, also called the Manhattan distance (extremely important):
"Error"=∣x_pred-x_data∣+∣y_pred-y_data∣

We do this for all the data points and add up all the errors to get a total error value.
Then, we divide this total by the number of points to find the average error per point.
This average L1 error tells us how far off our curve is, on average, from the real data.
A smaller value means a better fit and provides better accuracy.
Ultimately, we use an optimization method to automatically adjust θ, M, and Xuntil this average error becomes as small as possible within the given ranges of 6-60. When the optimizer finishes, we get the best-fitting values of θ, M, and X and these values can then be used to plot the final fitted curve and compare it visually with the data points.















Methodology

	Importing Libraries: We first import the required Python libraries :
	NumPy for mathematical functions,
	Pandas for reading and handling the CSV file,
	SciPy for the optimization function, and
	Matplotlib for plotting the final results.

	Reading the Data: The dataset xy_data.csv contains pairs of x and y values that lie on the given curve. Using Pandas, we read this file and store the data in two arrays: x_data and y_data. 

	Generating Parameter Values (t): The variable tis the parameter that runs the curve.
Since tranges from 6 to 60, we generate equally spaced values using NumPy’s linspace function. This gives one t value for each data point in the CSV file.

	Defining the Curve Function: We define a function that calculates x(t)and y(t)for any given set of parameters θ, M, and X. This function directly implements the equations given in the problem statement. The angle θ is converted from degrees to radians before using trigonometric functions because Python uses radians by default.

	Defining the Objective (Error) Function We define another function that measures how far the predicted curve is from the real data. This function calculates the L1 distance (sum of absolute differences) between predicted and actual xand yvalues.
The smaller this number, the closer the fit.

	Optimization Process We use the scipy.optimize.minimize function to automatically find the values of θ, M, and Xthat make the L1 error as small as possible.
We also provide bounds for each parameter so that the optimizer only searches within valid ranges:
	0°<θ<50°
	-0.05<M<0.05
	0<X<100

	Evaluating the Fit: After the optimizer finds the best parameters, we calculate:
	The total L1 distance,
	The average L1 distance per point, and
	A score out of 100 (calculated as 100-"average L1" ) to represent how good the fit is.

	Visualization: We plot the original data points and the fitted curve together using Matplotlib. This helps visually confirm how well the fitted curve matches the actual data. A close overlap between the two indicates a successful fit.
 
	Result Interpretation: Finally, the optimized parameter values (θ, M, and X) are reported. These represent the best estimates that describe the dataset according to the given model. The curve can also be visualized in tools like Desmos using the same final equations for better clarity.

 
Latex Graph on Desmos
<img width="940" height="446" alt="image" src="https://github.com/user-attachments/assets/db5edf5d-c03e-4608-bbe0-a9238000bb2f" />



















Conclusion

Ultimately this process of calculating the required values of the three parameters was an interesting task that provided a unique perspective of working on this problem and served as a good learning outcome regardless of the accuracy or the validity of the answers as breaking down complex topics such as L1 Distance among others and analysing a dataset full of x and y values proved to be an interesting task that was extremely fun to solve and that’s it.

Thank you for giving me this opportunity to participate in this assignment round.

It’s been a pleasure.
Thank you
