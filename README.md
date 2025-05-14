My llvm (libc) journey so far:

* Worked closely with the Google LLVM libc math maintainer and developed and tested floating point math functions
  - Independently developed 40 floating point math functions, increasing Basic Operations coverage by x percent. The pull request consisted of a 3500 line and 110 files change.
  - Developed `fmul` for double precision, with the guidance of the maintainer, by researching the problem, and applying my existing systems knowledge.
  - Co-authored: conducted performance benchmark analysis and carried out the programming that led to around 7x performance improvement of fmul
  - Interacted with the system at the level of bits and became familiar with hexadecimal.
* Continuously applied and grew my understanding of floating point math and C++.
* Added proxy headers enabling a smoother build process for llvm libc.
* Developed software that will be run millions of times in Linux, MacOS and embedded tool chains, e.g., ARM.


```
commit a205a854e06d36c1d0def3e3bc3743defdb6abc1
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Sat Sep 14 14:32:22 2024 -0700

    [libc][math] Improve fmul performance by using double-double arithmetic. (#107517)
    
    ```
     Performance tests with inputs in denormal range:
    -- My function --
         Total time      : 2731072304 ns
         Average runtime : 68.2767 ns/op
         Ops per second  : 14646276 op/s
    -- Other function --
         Total time      : 3259744268 ns
         Average runtime : 81.4935 ns/op
         Ops per second  : 12270913 op/s
    -- Average runtime ratio --
         Mine / Other's  : 0.837818
    
     Performance tests with inputs in normal range:
    -- My function --
         Total time      : 93467258 ns
         Average runtime : 2.33668 ns/op
         Ops per second  : 427957777 op/s
    -- Other function --
         Total time      : 637295452 ns
         Average runtime : 15.9324 ns/op
         Ops per second  : 62765299 op/s
    -- Average runtime ratio --
         Mine / Other's  : 0.146662
    
     Performance tests with inputs in normal range with exponents close to each other:
    -- My function --
         Total time      : 95764894 ns
         Average runtime : 2.39412 ns/op
         Ops per second  : 417690014 op/s
    -- Other function --
         Total time      : 639866770 ns
         Average runtime : 15.9967 ns/op
         Ops per second  : 62513075 op/s
    -- Average runtime ratio --
         Mine / Other's  : 0.149664
    ```
    
    ---------
    
    Co-authored-by: Tue Ly <lntue@google.com>

commit c0b7f1bb58633edbe12dcacee8e9d2c49163d87c
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Fri Sep 13 21:21:32 2024 -0700

    [libc][math][c23] add darwin entrypoints for fmul (#108680)

commit 1ace91f925ad87c3e5eb836ad58fdffe60c4aea6
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Thu Aug 29 11:14:18 2024 -0700

    [libc][math] Add performance tests for fmul and fmull. (#106262)

commit ff1cc5b97cffc184e5990bcaf6ea7c35090ef1e8
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Fri Aug 9 07:18:00 2024 -0700

    [libc][math][c23] Add totalorderl function. (#102564)

commit 9788368c37c319b11eb9a31af0f10aac62ba4f72
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Thu Aug 8 17:58:59 2024 -0700

    [libc][math][c23] Fix setpayloadsig smoke test on RV32 (#102538)

commit bb4f9c6ad430a12217deb11f0d5f73eb3725451c
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Wed Aug 7 21:35:49 2024 -0700

    [libc][math] fix yaml indentation bug (#102421)

commit aae7c38827ff7be9cc94b2e78d10742699ab506c
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Wed Aug 7 21:17:20 2024 -0700

    [libc][math][c23] Add entrypoints and tests for setpayloadsig{,f,l,f128} and setpayloadl. (#102413)

commit e3778a5d0ee78f3161f1d060c6db1c0dd0de6c4e
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Wed Aug 7 05:27:45 2024 -0700

    [libc][math] Add getpayloadl function. (#102214)

commit ed12f80ff0a8d304d10245c7bfb9f6af4a5c968c
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Wed Jul 31 20:16:42 2024 -0700

    [libc][math][c23] add entrypoints and tests for getpayload{,f,f128} (#101285)

commit 6aaf87021eda13727bfee690652cbbb9d1b3cdb2
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Tue Jul 30 18:15:48 2024 -0700

    [libc][math] fix header spec bug (#101273)

commit 546e4a210cb23e24a8086532c007280cb8ad3f13
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Tue Jul 30 16:52:47 2024 -0700

    [libc][math][c23] Add entrypoints and tests for setpayload{,f,f128} (#101122)

commit 0813260aa88827681da80bedd7f8737ad35c6895
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Tue Jul 30 09:58:44 2024 -0700

    [libc][math][c23] Add entrypoints and tests for totalorder{,f,f128} (#100593)

commit 7b51777ed89969ae86a0714565d195faf394b7db
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Wed Jul 24 16:53:23 2024 -0700

    [libc][math][c23] add entrypoints and tests for totalordermag{f,l,f128} (#100159)
    
    Fixes https://github.com/llvm/llvm-project/issues/100139

commit c1562374c8f24e5f873490639420b9c732b7e33d
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Sun Jul 21 12:55:11 2024 -0700

    [libc][math][c23] Add entrypoints and tests for dsqrt{l,f128} (#99815)

commit af0f58cf14329f5e0fe56fed7c9eb4cd3107a1ce
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Sun Jul 21 08:17:41 2024 -0700

    [libc][math][c23] Add entrypoints and tests for fsqrt{,l,f128} (#99669)

commit 6f60d2b807a4a719ac98288aec961dbb8433bb4b
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Mon Jul 1 21:38:15 2024 -0700

    [libc] Add mpfr tests for fmul. (#97376)
    
    Fixes https://github.com/llvm/llvm-project/issues/94834

commit 263be9fb0085001630e0431782a0ac0da7ab58ae
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Sat Jun 8 12:07:27 2024 -0700

    [libc][math][c23] fmul correcly rounded to all rounding modes (#91537)
    
    This is an implementation of floating point multiplication:
    
    It will consist of
       - `double x double -> float`

commit 75bbf4dd7cfda744d4a2487cfd06a58194d02db3
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Mon Apr 15 11:45:16 2024 -0700

    [libc] Add proxy headers for fenv types. (#88467)
    
    Fixes #88187

commit 49561181bdc8698aa28ee2a46d2faa4cf6767bbe
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Tue Apr 9 09:55:10 2024 -0700

    [libc] Add proxy header for fenv.h macro constants. #87863 (#87896)
    
    Hello, this addresses #87863.

commit 056b4043543cbc9e4ecad183db185bd26324b5b1
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Wed Mar 27 20:55:12 2024 -0700

    [libc][NFC] refactor fmin and fmax (#86718)
    
    Hello,
    
    So, I worked on the fmaximum and fminimum functions recently and the
    reviewers suggested the structure:
    
    ```
    if (bitsx ...)
      return ...;
    if (bitsy ..)
      return
    ...
    return ...;
    ```
    So I went ahead and did the same for fmin and fmax. I hope this isnt an
    issue for you all. thanks.
    
    ---------
    
    Co-authored-by: Job Hernandez <h93@protonmail.com>

commit 3e3f0c3175a8b83a8c51bef5712dbc384385db8b
Author: Job Henandez Lara <hj93@protonmail.com>
Date:   Mon Mar 25 12:19:10 2024 -0700
"""
