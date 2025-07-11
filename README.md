My llvm (libc) journey so far:

* Worked closely with the Google LLVM libc math maintainer and developed and tested floating point math functions
  - Independently developed 40 floating point math functions, increasing Basic Operations coverage by x percent. The pull request consisted of a 3500 line and 110 files change.
  - Developed `fmul` for double precision, with the guidance of the maintainer, by researching the problem, and applying my existing systems knowledge.
  - Co-authored: conducted performance benchmark analysis and carried out the programming that led to around 7x performance improvement of fmul
  - Interacted with the system at the level of bits and became familiar with hexadecimal.
* Continuously applied and grew my understanding of floating point math and C++.
* Added proxy headers enabling a smoother build process for llvm libc.
* Developed software that will be run millions of times in Linux, MacOS and embedded tool chains, e.g., ARM.
