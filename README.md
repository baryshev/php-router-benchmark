PHP Router Benchmark
====================

The intent here is to benchmark different PHP routing solutions. This is a micro-optimization, done purely out of 
dumb curiosity.


Installation
------------

Clone the repo, run `composer install`, run `php run-tests.php`.

You can install the Pux extension to test that as well. See Pux docs for more info.


Currently
---------

The current test creates 1000 routes, each with a randomized prefix and postfix, with 9 parameters each.

It was run with the Pux extension enabled.

An example route: `/9b37eef21e/{arg1}/{arg2}/{arg3}/{arg4}/{arg5}/{arg6}/{arg7}/{arg8}/{arg9}/bda37e9f9b`

## Worst-case matching
This benchmark matches the last route and unknown route. It generates a randomly prefixed and suffixed route in an attempt to thwart any optimization. 1,000 routes each with 9 arguments.

This benchmark consists of 12 tests. Each test is executed 1,000 times, the results pruned, and then averaged. Values that fall outside of 3 standard deviations of the mean are discarded.


Test Name | Results | Time | + Interval | Change
--------- | ------- | ---- | ---------- | ------
TreeRoute - unknown route (1000 routes) | 996 | 0.0000113306 | +0.0000000000 | baseline
TreeRoute - last route (1000 routes) | 992 | 0.0000244276 | +0.0000130969 | 116% slower
Symfony2 Dumped - unknown route (1000 routes) | 998 | 0.0002979821 | +0.0002866515 | 2530% slower
FastRoute - last route (1000 routes) | 999 | 0.0004127548 | +0.0004014242 | 3543% slower
FastRoute - unknown route (1000 routes) | 998 | 0.0004346588 | +0.0004233282 | 3736% slower
Symfony2 Dumped - last route (1000 routes) | 958 | 0.0004573724 | +0.0004460418 | 3937% slower
Pux ext - unknown route (1000 routes) | 998 | 0.0013391188 | +0.0013277882 | 11719% slower
Pux ext - last route (1000 routes) | 998 | 0.0014304962 | +0.0014191655 | 12525% slower
Symfony2 - unknown route (1000 routes) | 996 | 0.0017854581 | +0.0017741274 | 15658% slower
Symfony2 - last route (1000 routes) | 995 | 0.0018181590 | +0.0018068284 | 15946% slower
Aura v2 - last route (1000 routes) | 966 | 0.0740957912 | +0.0740844605 | 653841% slower
Aura v2 - unknown route (1000 routes) | 984 | 0.0947946792 | +0.0947833486 | 836522% slower


## First route matching
This benchmark tests how quickly each router can match the first route. 1,000 routes each with 9 arguments.

This benchmark consists of 6 tests. Each test is executed 1,000 times, the results pruned, and then averaged. Values that fall outside of 3 standard deviations of the mean are discarded.


Test Name | Results | Time | + Interval | Change
--------- | ------- | ---- | ---------- | ------
Pux ext - first route | 999 | 0.0000142710 | +0.0000000000 | baseline
TreeRoute - first route | 990 | 0.0000252103 | +0.0000109393 | 77% slower
FastRoute - first route | 999 | 0.0000266260 | +0.0000123550 | 87% slower
Symfony2 Dumped - first route | 992 | 0.0000344594 | +0.0000201884 | 141% slower
Symfony2 - first route | 997 | 0.0002561864 | +0.0002419154 | 1695% slower
Aura v2 - first route | 998 | 0.0003392988 | +0.0003250278 | 2278% slower
