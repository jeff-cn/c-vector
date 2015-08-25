This is an implementation of a `std::vector` like growable array, but in plain 
C89 code. The result is a type safe, easy to use, dynamic array that has a 
familiar set of operations.

To allow the code to be maximally generic, it is implemented as all macros, and
is thus header only. Usage is simple:

	/* if this is defined, then the vector will double in capacity each 
	 * it runs out of space if it is not defined, then the vector will
	 * be conservative, and will have a capcity no larger than necessary.
	 * having this defined will minimize how often realloc gets called.
	 */
	#define LOGARITHMIC_GROWTH

	#include "vector.h"
	#include <stdio.h>

	int main(int argc, char *argv[]) {

		/* this is the variable that will store the array, you can have
		 * a vector of any type!
		 */
		int *v = NULL;

		/* add some elements to the back
		vector_push_back(v, 10);
		vector_push_back(v, 20);
		vector_push_back(v, 30);

		/* and remove one too */
		vector_pop_back(v);


		/* print out some stats about the vector */
		printf("pointer : %p\n",  v);
		printf("capacity: %lu\n", vector_capacity(v));
		printf("size    : %lu\n", vector_size(v));

		/* iterator over the vector using "iterator" style */
		if(v) {
			int * it;
			int i = 0;
			for(it = vector_begin(v); it != vector_end(v); ++it) {
				printf("v[%d] = %d\n", i, *it);
				++i;
			}
		}
		
		/* iterator over the vector standard indexing too! */
		if(v) {
			size_t i;
			for(i = 0; i < vector_size(v); ++i) {
				printf("v[%d] = %d\n", i, v[i]);
			}
		}		

		/* well, we don't have destructors, so let's clean things up */
		vector_free(v);

	}