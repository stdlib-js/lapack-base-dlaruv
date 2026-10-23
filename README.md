<!--

@license Apache-2.0

Copyright (c) 2026 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# dlaruv

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Return a vector of `N` random real numbers drawn from a uniform (0,1) distribution.



<section class="usage">

## Usage

```javascript
import dlaruv from 'https://cdn.jsdelivr.net/gh/stdlib-js/lapack-base-dlaruv@deno/mod.js';
```

#### dlaruv( seed, N, x )

Returns a vector of `N` random real numbers drawn from a uniform (0,1) distribution.

```javascript
import Int32Array from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-int32@deno/mod.js';
import Float64Array from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-float64@deno/mod.js';

var seed = new Int32Array( [ 0, 1, 2, 3 ] );
var x = new Float64Array( 3 );

dlaruv( seed, 3, x );
// x => <Float64Array>[ ~0.1319, ~0.2338, ~0.3216 ]
```

The function has the following parameters:

-   **seed**: [`Int32Array`][@stdlib/array/int32] seed array of four integers. Each element must be between `0` and `4095`, and `seed[3]` must be odd. On exit, the seed is updated.
-   **N**: number of random numbers to generate. Must be at most `128`.
-   **x**: output [`Float64Array`][@stdlib/array/float64].

Note that indexing is relative to the first index. To introduce an offset, use [`typed array`][mdn-typed-array] views.

<!-- eslint-disable stdlib/capitalized-comments -->

```javascript
import Int32Array from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-int32@deno/mod.js';
import Float64Array from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-float64@deno/mod.js';

// Initial arrays...
var seed0 = new Int32Array( [ 0, 0, 1, 2, 3 ] );
var x0 = new Float64Array( [ 0.0, 0.0, 0.0, 0.0 ] );

// Create offset views...
var seed1 = new Int32Array( seed0.buffer, seed0.BYTES_PER_ELEMENT*1 ); // start at 2nd element
var x1 = new Float64Array( x0.buffer, x0.BYTES_PER_ELEMENT*1 ); // start at 2nd element

dlaruv( seed1, 3, x1 );
// x0 => <Float64Array>[ 0.0, ~0.1319, ~0.2338, ~0.3216 ]
```

#### dlaruv.ndarray( N, seed, strideS, offsetS, x, strideX, offsetX )

Returns a vector of `N` random real numbers drawn from a uniform (0,1) distribution using alternative indexing semantics.

```javascript
import Int32Array from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-int32@deno/mod.js';
import Float64Array from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-float64@deno/mod.js';

var seed = new Int32Array( [ 0, 1, 2, 3 ] );
var x = new Float64Array( 3 );

dlaruv.ndarray( 3, seed, 1, 0, x, 1, 0 );
// x => <Float64Array>[ ~0.1319, ~0.2338, ~0.3216 ]
```

The function has the following additional parameters:

-   **strideS**: stride length for `seed`.
-   **offsetS**: starting index for `seed`.
-   **strideX**: stride length for `x`.
-   **offsetX**: starting index for `x`.

While [`typed array`][mdn-typed-array] views mandate a view offset based on the underlying buffer, the offset parameters support indexing semantics based on starting indices. For example,

<!-- eslint-disable max-len -->

```javascript
import Int32Array from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-int32@deno/mod.js';
import Float64Array from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-float64@deno/mod.js';

var seed = new Int32Array( [ 0, 0, 1, 2, 3 ] );
var x = new Float64Array( [ 0.0, 0.0, 0.0, 0.0, 0.0 ] );

dlaruv.ndarray( 3, seed, 1, 1, x, 1, 2 );
// x => <Float64Array>[ 0.0, 0.0, ~0.1319, ~0.2338, ~0.3216 ]
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   `seed` is updated in-place and should be reused across invocations in order to generate a continuous stream of random numbers.
-   At most `128` random numbers are generated per invocation. If `N > 128`, only the first `128` indexed elements of `x` are updated.
-   If `N <= 0`, the functions return `x` unchanged and do not update `seed`.
-   Generated values are always on the open interval `(0,1)`, as the largest representable output is `1 - 2^-48`.
-   `dlaruv()` corresponds to the [LAPACK][LAPACK] function [`dlaruv`][lapack-dlaruv].

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```javascript
import Int32Array from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-int32@deno/mod.js';
import Float64Array from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-float64@deno/mod.js';
import dlaruv from 'https://cdn.jsdelivr.net/gh/stdlib-js/lapack-base-dlaruv@deno/mod.js';

var seed = new Int32Array( [ 1, 23, 456, 3795 ] );
var x = new Float64Array( 10 );

dlaruv( seed, x.length, x );

console.log( x );
console.log( seed );
```

</section>

<!-- /.examples -->

<!-- C interface documentation. -->



* * *

<section class="references">

## References

-   Fishman, George S. 1990. "Multiplicative Congruential Random Number Generators with Modulus 2^β: An Exhaustive Analysis for β = 32 and a Partial Analysis for β = 48." _Mathematics of Computation_ 54 (189). American Mathematical Society: 331–44. doi:[10.2307/2008698][@fishman1990a].

</section>

<!-- /.references -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/lapack-base-dlaruv.svg
[npm-url]: https://npmjs.org/package/@stdlib/lapack-base-dlaruv

[test-image]: https://github.com/stdlib-js/lapack-base-dlaruv/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/lapack-base-dlaruv/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/lapack-base-dlaruv/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/lapack-base-dlaruv?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/lapack-base-dlaruv.svg
[dependencies-url]: https://david-dm.org/stdlib-js/lapack-base-dlaruv/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/lapack-base-dlaruv/tree/deno
[deno-readme]: https://github.com/stdlib-js/lapack-base-dlaruv/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/lapack-base-dlaruv/tree/umd
[umd-readme]: https://github.com/stdlib-js/lapack-base-dlaruv/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/lapack-base-dlaruv/tree/esm
[esm-readme]: https://github.com/stdlib-js/lapack-base-dlaruv/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/lapack-base-dlaruv/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/lapack-base-dlaruv/main/LICENSE

[lapack]: https://www.netlib.org/lapack/explore-html/

[lapack-dlaruv]: https://netlib.org/lapack/explore-html/d9/d0f/group__laruv.html

[@stdlib/array/int32]: https://github.com/stdlib-js/array-int32/tree/deno

[@stdlib/array/float64]: https://github.com/stdlib-js/array-float64/tree/deno

[mdn-typed-array]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray

[@fishman1990a]: https://doi.org/10.2307/2008698

</section>

<!-- /.links -->
