Solution for [Vector Addition](https://leetgpu.com/challenges/vector-addition).

This is a simple starting problem. 
The key is understanding how the index calculation is done, ie how the vector is split up across threads and blocks.

Finally, the index overflow is also cruicial since our vector size might not split perfectly into blocks, so the last block corresponding the the final few indices will have some threads that run without a valid index to refer to.