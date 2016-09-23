# Hackthon Project: Data visualization

This is about what I did in our 3 days hackthon project which is a data visualization application using D3. There are two main functions I implemented. One is the CSV upload function which allows user to upload their own csv datasets and dynamically shows the fields for users to select. Another one is a prediction function which uses two algorithms to calculate the theta and generates a line chart to visualize the data. Also, I used a singleton class in this project to persist data. In this blog, I will mainly take about the prediction function and how I implement them in Ruby.

The prediction line chart shows the relationship between two related features. It can be used to predict the value of y from the value of x. It reads a dataset, and, by implementing a normal equation, predicts the reasonable value of y based on the dataset. I used three standerd the Ruby classes, Matrix, Vector, and Rational.

Model Selection
A good model will give you a good prediction result. The two features(x, y) must have a linear relationship between them, because the equation is a linear equation.

Algorithm Selection
I use a normal equation to calculate the reasonable y from x based on a dataset. I tried to implement a regression equation with a gradient descent function, but, in Ruby, it is difficult to implement the complex functions. Using a normal equation is not the best approach for prediction, but, in Ruby, it is efficient on implementation and I do not need to iterate the datasets myself. I found several Ruby classes(Matrix, Vector, Rational) which helps me to implement the equation. I wrote a class UniPre.rb which takes two arrays(x, y) which must be in the same order and gives you a optimal value(T) for prediction.

The prediction function is:
￼![Normal Equation](https://github.com/YuanGao0317/hackathon-data-visualization/blob/master/app/assets/images/equation.png)

X is the features of the training examples, y is the prediction vector of the training examples.

The implementation of the method for the algorithm is:
	def n   
		x_t = self.x.transpose
		first = x_t * self.x
		x_i = first.inverse

		theta =  x_i * x_t * self.y

		m = theta.collect { |e| Rational(e).to_f }
		self.theta = m.row(0)[0]
	end

This equation takes the advantages of matrix calculation; thus I don’t need to write a tons of code to iterate the dataset.

After I get the theta, I use a linear equation y = theta * x to predict the y.

This is not the best equation. There are several ways to optimize it by changing the equation to a complex polynomial to generate a complex line, for instance, square equation, however, which may generate other issues, for example, local optimal and overfitting which may force us to apply regularization to the prediction function.

Based on our datasets and time limitation, the prediction algorithms are good enough to show the information that I want. 

There are two big challenges. One is that we all don’t know about D3 at that time, so it is not easy for us to implement it. Second is that I have to find a way to implement the algorithm, and test the prediction results.


## Test
1. bundle
2. rake db:migrate or bunlde exec rake db:migrate
3. rails s

http://localhost:3000/linechart
