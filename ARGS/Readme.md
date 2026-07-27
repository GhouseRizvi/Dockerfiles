Args is the only instruction can be used before FROM
and cannot be accessed after from
basically Args cannot be access after one arguement .

ARG is the only instruction can be used before from and accessibility scope is till from.
Later cannot be accessed.

Arg declared before the from cannot be accessed after From

Using ENV and args for best results:
Create one env variable and assign the value of args to that then we can access args value through env from both the image and container.