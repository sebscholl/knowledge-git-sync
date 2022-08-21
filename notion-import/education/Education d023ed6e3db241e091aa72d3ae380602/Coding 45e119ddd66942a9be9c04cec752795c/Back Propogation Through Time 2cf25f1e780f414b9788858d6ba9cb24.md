# Back Propogation Through Time

Last Edited: December 19, 2019 11:43 PM

[Back%20Propogation%20Through%20Time%202cf25f1e780f414b9788858d6ba9cb24/untitled](Back%20Propogation%20Through%20Time%202cf25f1e780f414b9788858d6ba9cb24/untitled)

Image above represents a timescale moving from left to right.

Each state (Sn) is contributed to be the input (Xn), which influences that layers/states output weight (Wy)

We are dealing with multiple weight variables now.

- Input weights Wx
- State weights Ws
- Output weights Wy

When handling back-propagation in this network architecture, the weights accumulate between states overtime. Meaning that, to calculate the partial derivative of the Loss Function, we must use the chain rule to sum the weights of all previous states with the current - as to consider all states that have led to the current output.

[Back%20Propogation%20Through%20Time%202cf25f1e780f414b9788858d6ba9cb24/untitled%201](Back%20Propogation%20Through%20Time%202cf25f1e780f414b9788858d6ba9cb24/untitled%201)

To articulate this process of updating the weights of matrix Ws (and Wx, as considered the input "state"), the error of N can be thought of as the following.

The SUM of the Error of N over the Output of N, times the Output of N over the State of I, times the State of I over the Weights of S

[Back%20Propogation%20Through%20Time%202cf25f1e780f414b9788858d6ba9cb24/untitled%202](Back%20Propogation%20Through%20Time%202cf25f1e780f414b9788858d6ba9cb24/untitled%202)