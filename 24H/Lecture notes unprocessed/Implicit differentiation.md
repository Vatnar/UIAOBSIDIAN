A lot of times we have an function of the form $F(x,y)$. E.g curves. An example of this is $F(x,y) = x^{2} +y^{2} - 25$ A circle. Sometimes we can solve an equation $F(x,y)=0$ for y and so find explicit formulas for one or more functions $y=f(x)$ defined by the equation. Usually you cannot solve the equation, therefore you can define y as one or more functions of x *implicitly*, even if we cannot solve for these functions explicitly. The idea is to differentiate the given equation with respect to x, regarding y as a function of having derivative $\frac{dy}{dx}$ or $y'$. 

#### Example 1
###### <span style="color:rgb(192, 0, 0)">Solution</span> The equation $y^{2} = x$ defines two differentible functions of x; in this case we know them explicitly. They are $y_{1}=\sqrt{ x }$ and $y_{2}=-\sqrt{ x }$, having derivatives defined for $x>0$ by
$$
\frac{dy_{1}}{dx}=\frac{1}{2\sqrt{ x }}, \text{and},\frac{dy_{2}}{dx}=\frac{1}{2\sqrt{ x }}
$$
However, we can find the slope of the curve $y^{2}=x$ at any point $(x, y)$ satisfying that equation without first solving the equation for y. to find dy/dx, we simply differntiate both side of the equation $y^{2}=x$ with respect to x, treating y as a differentiable function of x and using the Chain Rule to differentiate $y^{2}$ 
$\frac{d}{dx}(y^{2})=\frac{d}{dx}(x)$
$2y \frac{dy}{dx}=1$
$\frac{dy}{dx}=\frac{1}{2y}$

