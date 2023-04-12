


The example we will use in this course is taken from the official PyTorch page:
<https://pytorch.org/> and the problem is of fitting `y=sin(x)` with a third
order polynomial.

``` python title="torch_test.py"
import torch
import math

dtype = torch.float
device = torch.device("gpu")
# device = torch.device("cuda:0") # Uncomment this to run on GPU

# Create random input and output data
x = torch.linspace(-math.pi, math.pi, 2000, device=device, dtype=dtype)
y = torch.sin(x)

# Randomly initialize weights
a = torch.randn((), device=device, dtype=dtype)
b = torch.randn((), device=device, dtype=dtype)
c = torch.randn((), device=device, dtype=dtype)
d = torch.randn((), device=device, dtype=dtype)

learning_rate = 1e-6
for t in range(2000):
    # Forward pass: compute predicted y
    y_pred = a + b * x + c * x ** 2 + d * x ** 3
    
    # Compute and print loss
    loss = (y_pred - y).pow(2).sum().item()
    if t % 100 == 99:
	print(t, loss)
    
    # Backprop to compute gradients of a, b, c, d with respect to loss
    grad_y_pred = 2.0 * (y_pred - y)
    grad_a = grad_y_pred.sum()
    grad_b = (grad_y_pred * x).sum()
    grad_c = (grad_y_pred * x ** 2).sum()
    grad_d = (grad_y_pred * x ** 3).sum()
    
    # Update weights using gradient descent
    a -= learning_rate * grad_a
    b -= learning_rate * grad_b
    c -= learning_rate * grad_c
    d -= learning_rate * grad_d
```

Now let's start an interactive job with GPU 

```
interactive -A staff -n 1 -M snowy --gres=gpu:1  -t 1:00:01
```


!!! tip "Exercise 3: Run Pytorch on GPU (10 min)"
	
	1. In groups of 3-4 persons
	2. Create a very simple python script that:
	    1. Checks that a GPU is available
	    2. Prints the model name of the gpu
	3. Create and submit a batch script that allocates a GPU on Snowy and
	   runs the python script. Remeber to use the correct project name!
	4. Monitor the job using `jobinfo` and view the output once finished
