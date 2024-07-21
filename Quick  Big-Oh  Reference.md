- Simple loop -> O(n)
	- Examples include `max(array)` and generating checksums when validating network packets
- Nested loop -> O(n $\cdot$ m ) where n is the outer loop and m is the inner loop.
	- If m = n -> O($n^2$)
- Binary Chop, divides input by 2 on each iteration -> O(log(n))
- Divide an conquer - for algoritms that partition their output, usually results in O(nlog(n))

- When encountering a O($n^2$) algorithm. Think of the following question: could you leverage divide and conquer to bring it down to O(nlog(n))?